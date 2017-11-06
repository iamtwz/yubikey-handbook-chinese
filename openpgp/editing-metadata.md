### 修改元数据

现在私钥已经被移动到 Yubikey 当中了，也是时候做一些基本的设置了。比如改变默认的管理员 PIN（GPG 中叫做 _Admin PIN_）和访问私钥时需要的普通 PIN。

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

Your selection? 3
PIN changed.

1 - change PIN
2 - unblock PIN
3 - change Admin PIN
4 - set the Reset Code
Q - quit

Your selection? 1
PIN changed.

gpg/card> q

gpg/card> login
foobar

gpg/card> sex
m

gpg/card> name
Cardholder\'s surname: Bar
Cardholder\'s given name: Foo

gpg/card> lang
Language preferences: en

gpg/card> login
Login data (account name): foobar

gpg/card> list

gpg/card> quit
```
