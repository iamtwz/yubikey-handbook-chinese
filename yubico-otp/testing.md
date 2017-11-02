### 测试

如果你允许 `root` 用户登录，你应该可以通过暴露的 `2222` 端口连接到容器：

```sh
❯ ssh root@127.0.0.1 -p 2222
Authenticated with partial success.
root@127.0.0.1 password:
```

你应该能看到 _Authenticated with partial success_ 的提示，这就表示对公钥的认证已经成功了。

现在，请输入你的密码，**不要按** Enter 键。长按你的 Yubikey 直到自动换行。

If you consider the password `foobar` for the `root` user, the actual password that will get sent is:
如果你为 `root` 设置的密码是 `foobar` 的话，实际发送的密码大概像这样：

```
root@127.0.0.1 password: foobarcccccccgklgcvnkcvnnegrnhgrjkhlkfhdkclfncvlgj
```

`libpam-yubico` 会取出和 OTP 相关的字符并将它发送到 YubiCloud ，成功的话便会将剩下的字符转发给下一个 PAM 模块（在这个例子里是 `pam_unix.so`）来验证用户的密码。

如果没问题的话，大约 2-3 秒之后，你就能成功登录了。接下来退出然后以 `foobar` 用户登录，然后尝试通过 `su root` 命令提升权限，你会发现需要 `root` 用户的 Yubikey（同样的方法，输入密码然后长按你的 Yubikey）

你也许注意到了在 SSH 的过程中其实是通过三个因素完成了认证（而不是两个）———— 公钥认证、密码、和 Yubikey OTP。这其实是 OpenSSH 的限制，目前还做不到在使用公钥验证和 Yubikey 时跳过密码验证。
