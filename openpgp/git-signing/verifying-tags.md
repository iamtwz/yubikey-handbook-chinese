#### Tags 验证

首先导入签名者的 GPG 公钥，然后执行以下任意命令来获得 `Good signature` 消息：

```sh
❯ git tag -v 1.0.0
❯ git cat-file -p 1.0.0
❯ git verify-tag 1.0.0
```
