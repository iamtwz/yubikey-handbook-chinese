#### Commits 签名

在上文提到的 git 仓库中添加一个新文件，并使用 `-S` 标签来提交（commit）它。（注意不是 `-s` 标签，在 commit 命令下它意味着 `Signed-Off`）：

```
❯ touch biz
❯ git add biz
❯ git commit -S -m "Add biz"
```

你可以通过在 `~/.gitconfig.local` 文件中添加下列内容来开启 commit 自动签名功能：

```
[commit]
    gpgSign = true
```
