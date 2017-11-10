#### Tags 签名

假设你有一个额外的文件可以在主 `~/.gitconfig` 中添加 gitconfig 设置：

```
[include]
    path = .gitconfig.local
```

配置 `~/.gitconfig.local` 文件让其指向你插入的 GPG 签名钥匙：

```sh
[user]
    signingkey = <signingKeyId>
```

开启 `git tag -m <message>` 来自动强制签名 tags：

```
[tag]
    forceSignAnnotated true
```

在临时项目上创建 tag 来测试签名钥匙是否工作正常：

```sh
❯ cd /tmp
❯ mkdir foo
❯ cd foo
❯ git init
❯ touch bar
❯ git add bar
❯ git ci -m "Add bar"
❯ git tag 1.0.0 -s -m "Release 1.0.0"
```

输入 Yubikey GPG PIN 然后触摸它，确保 GPG 签名已经被加入 tag 中：

```
❯ git show 1.0.0
```
