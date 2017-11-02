#### 为 OpenSSH 启用双因素认证

在 `/etc/ssh/sshd_config` 中加入下面的选项启用双因素认证：

```sh
# Require public key *and* password authentication. Without this, a valid public
# key would bypass the Yubikey requirement.
AuthenticationMethods publickey,password

# Enable the password authentication backend.
PasswordAuthentication yes

# Disable the keyboard-interactive mode which could be used to ask for the
# password.
ChallengeResponseAuthentication no

# Enable PAM integration for authentication as this is the system that Yubikey
# integrates with.
UsePAM yes
```

如果你要通过 root 用户登录，添加或修改同一个文件中的 `PermitRootLogin` 选项，将 `prohibit-password` 替换成 `yes`：

```sh
# Enable root login via ssh.
PermitRootLogin yes
```

重新启动 `ssh` 服务，注意这不会中断你现有的会话。

```sh
❯ service ssh restart
```
