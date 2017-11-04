## 使用用户证书验证 SSH （服务端）

在以安全为前提下要保障可靠性、可控性和一致性是非常复杂的。我们可以利用 SSH 又或者说 OpenSSH 来替代所依赖的中央身份验证（比如 LDAP 或者 Kerberos）

除了 [通过 PIV 和 PKCS#11 验证 SSH](#authenticating-ssh-client-access-with-piv-and-pkcs-11) 之外，还可以增加远程 SSH 验证的安全性。Facebook 和 Yahoo 已经更换使用 SSH 用户证书来避免中心认证系统宕机。因为他不支持拓展（需要 1:1  匹配），所以也利于维持 `authorized_keys` 文件先后一致。

一个 _数字证书认证机构_ 可以对连接到服务器上的每个客户端进行签名和安全认证。

签名的证书还可以指向当前证书的用户（登录身份）。每个用户会记录在一个文件中：

```sh
❯ mkdir /etc/ssh/auth_principals
❯ echo -e 'access-root' > /etc/ssh/auth_principals/root
❯ echo -e 'access-databases' > /etc/ssh/auth_principals/foobar
```

上例中，任何一个签名主体带有 `access-root` 的证书都可以使用 `root` 用户名通过 SSH 连接进主机， 任何一个签名主体带有 `access-databases` 的证书都可以使用 `foobar` 用户名登录。

现在让我们来创建 _数字证书认证机构_。

1. 使用一台处于气隙系统下【译者注：即与互联网物理隔离】的计算机，生成用户证书颁发机构的根证书：

  ```sh
  ❯ ssh-keygen -C "SSH User Certificate Authority" -f sshuser.root.ca
  ```

2. 把根证书（`sshuser.root.ca.pub`）放到每个主机的 `/etc/ssh/` 目录下，保证文件权限是 `chmod 644`。

3. 更新 `/etc/ssh/sshd_config` 文件加入新的 CA 和 principals 文件：

  ```sh
  TrustedUserCAKeys /etc/ssh/sshuser.root.ca.pub
  AuthorizedPrincipalsFile /etc/ssh/auth_principals/%u
  ```

4. 让用户或客户端从 Yubikey 中提取他们的公钥以便在处于气隙系统下的计算机中使用新 CA 签名来认证：

  ```sh
  ssh-keygen -D /usr/local/opt/opensc/lib/pkcs11/opensc-pkcs11.so -e
  ```

5. 在被处于气隙系统下的计算机签名的用户证书， 要特别注意一下登录名（`<user>`），确保这个证书能够指向被声明的主体（`<principals>`，使用逗号分隔），证书到期时间（`+52w`）和序列号（`<serial>`）。

  ```sh
  ❯ ssh-keygen -s sshuser.root.ca -I <user> -n <principals> -V +52w -z <serial> <user>.pub

  Signed user key foobar-cert.pub: id "foobar" serial 1928121 for access-root valid from 2016-12-10T00:10:00 to 2017-12-09T00:10:10
  ```

6. 确认用户证书无误：

  ```sh
  ❯ ssh-keygen -Lf <user>-cert.pub

  user-cert.pub:
      Type: ssh-rsa-cert-v01@openssh.com user certificate
      Public key: RSA-CERT SHA256:NWmw3siRlxn3bsIhzaFrCsh66KKIWapFuZsNiDXhRLw
      Signing CA: RSA SHA256:HLD1Eb4XiCoyXew23skyisJt+3P02MOsrHHbK/DmlgY
      Key ID: "foobar"
      Serial: 1928121
      Valid: from 2016-12-10T00:10:00 to 2017-12-09T00:10:10
      Principals:
              access-root
      Critical Options: (none)
      Extensions:
              permit-X11-forwarding
              permit-agent-forwarding
              permit-port-forwarding
              permit-pty
              permit-user-rc
  ```

7. 复制 `<user>-cert.pub` 到客户端的 `~/.ssh` 目录下并重命名为 `id_rsa-cert.pub`。 这个名字需要十分具体， 因为在 `opensc-pkcs11` 中有一个限制规则去排除 `id_rsa-cert.pub` 之外的证书。
