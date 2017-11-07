### 使用 GPG 进行 SSH 验证

技术上来讲的话，使用 GPG 来验证 SSH 会话并没有问题。但是 `gpg-agent`  对 `ssh-agent` 的支持并不友好。

相比而言更推荐使用 PIV 来进行 SSH 验证。

在 `~/.gnupg/gpg-agent.conf` 文件下启用 `enable-ssh-support` 和 `write-env-file` ：

```
default-cache-ttl 600
  max-cache-ttl 7200
  pinentry-program /usr/local/MacGPG2/libexec/pinentry-mac.app/Contents/MacOS/pinentry-mac
  enable-ssh-support
  write-env-file
```
