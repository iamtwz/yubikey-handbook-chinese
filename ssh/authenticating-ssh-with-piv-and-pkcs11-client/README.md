## 使用 PIV 和 PKCS#11 验证 SSH（客户端）

Yubikey 很酷的用法之一就是通过 PKCS#11 来验证 SSH。 把私钥存储在 Yubikey 上，当它被访问时，就可以让你请求触摸操作。

除了常见的远程登录，所有通过 SSH 连接的操作（比如使用远程 git 服务器（比如 Github））都可能出发这一行为。这是客户端的保护，用来防止在未授权的情况下访问到 SSH 私钥。

需要注意的是，只有 RSA 密钥支持这种操作。

1. 创建一对 2048-bit  的 RSA 钥匙串：

  ```sh
  ❯ yubico-piv-tool -s 9a -a generate -k --pin-policy=once --touch-policy=always --algorithm=RSA2048 -o public.pem
  ```

  输入你的 Yubikey 的 _管理密钥_。

2. 创建一个自签名证书（或者使用证书签名请求替代）:

  ```sh
  ❯ yubico-piv-tool -a verify-pin -a selfsign-certificate -s 9a -S '/CN=ssh/' --valid-days=365 -i public.pem -o cert.pem
  ```

  输入 PIN 码然后触摸一下你的 Yubikey。

  或者用 `selfsign-certificate` 替代 `request-certificate` ，并把得到的 `.csr` 文件进行内部 CA 认证。

3. 导入已（自）签名的证书：

  ```sh
  ❯ yubico-piv-tool -k -a import-certificate -s 9a -i cert.pem
  ```

  输入你的 Yubikey 的 _管理密钥_。

4. 以正确的格式导出 OpenSSH 使用的存储在 Yubikey 上的公钥：

  ```sh
  ❯ ssh-keygen -D /usr/local/opt/opensc/lib/pkcs11/opensc-pkcs11.so -e
  ```

  或者，如果你没有删掉的话你也可以使用先前生成的公钥。

  ```sh
  ❯ ssh-keygen -i -m PKCS8 -f public.pem
  ```

  你现在可以分享这个公钥用作 SSH 验证了（比如放在 `~/.ssh/authorized_keys`）。

5. 检查 9a 插槽的状态（可选）：

  ```sh
  ❯ yubico-piv-tool -a status
  ```

6. 将使用 PKCS#11 的私钥添加到本地 ssh-agent：

  ```sh
  ❯ ssh-add -s /usr/local/opt/opensc/lib/pkcs11/opensc-pkcs11.so
  ```

  当它询问密码时输入你的 Yubikey 的 PIN 码。

7. 确定私钥已经被添加：

  ```sh
  ❯ ssh-add -L
  ```

8. 也可以选择性的把 PKCS11Provider 添加到 `~/.ssh/config` 中：

  ```sh
  Host github.com
    PKCS11Provider /usr/local/opt/opensc/lib/pkcs11/opensc-pkcs11.so
    Port 22
    User foobar
  ```
