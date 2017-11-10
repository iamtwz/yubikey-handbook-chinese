#### Yubikey 验证模块

##### 在 YubiCloud 上创建一个 API 

从 [Yubico](https://upgrade.yubico.com/getapikey/) 获得一个 API 密钥，应用程序、上下文和服务器各需要一个 client id。

输入你的邮件地址 ，选择 `Yubikey OTP` 输入后触摸 Yubikey，你会获得这样的一组字符串：

```
Client ID: <clientId>
Secret Key: <secretKey>
```

把它们保存在一个安全的地方以备接下来使用（比如一个密码管理器内）

##### 创建 Yubikey 验证模块

在系统级别的映射设置完毕和生成了 API 凭据以后，新建 `/etc/pam.d/yubikey-auth`，加入下面的内容：

```sh
# Enable YubiCloud OTP Validation (implicitly includes `mode=client` and the default validation `urllist`).
auth    required        pam_yubico.so id=<clientId> key=<secretKey> authfile=/etc/yubikeys
```

要启用调试模式的话，创建日志文件然后加入相应的参数（`debug` and `debug_file`）到 `pam_yubico.so` 中：

```sh
❯ touch /var/log/yubikey-auth.log
❯ chmod go+w /var/log/yubikey-auth.log
```

修改 `/etc/pam.d/yubikey-auth` 文件:

```sh
auth    required        pam_yubico.so id=<clientId> key=<secretKey> authfile=/etc/yubikeys debug debug_file=/var/log/yubikey-auth.log
```

当不需要调试时记得移除它们。

##### 修改 _common-auth_ authentication 模块

在 `/etc/pam.d/common-auth` 中为 `pam_unix.so` 添加 `try_first_pass` 指示。但不是所有发行版都存在 `common-auth` 文件，你可能需要寻找其他有效文件的路径。

当然别忘了包含刚刚创建的 Yubikey 验证模块：

```sh
auth    include                         yubikey-auth
auth    [success=1 default=ignore]      pam_unix.so nullok_secure try_first_pass
```
