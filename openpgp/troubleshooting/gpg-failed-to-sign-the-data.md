#### GPG 无法签名数据

如果当你在对 tag 或者 commit 签名时遇到以下提示：

```
error: gpg failed to sign the data
error: unable to sign the tag
```

首先，物理插拔一下 Yubikey 并确保安全卡状态可以被正确的列出：

```
❯ gpg --card-status
```

如果你看到：

```
PIN retry counter : 0 0 3
```

这意味着你的正常 PIN 码因为输错次数太多而被锁定。第三个数字表示的是管理员 PIN 码的重试计数器。

通过输入管理员 PIN 码来解锁正常 PIN 码：

```
❯ gpg --card-edit

gpg/card> admin
Admin commands are allowed

gpg/card> passwd
gpg: OpenPGP card no. … detected

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? 2
PIN unblocked and new PIN set.

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? q
```
