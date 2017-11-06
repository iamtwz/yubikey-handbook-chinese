### 导入钥匙

GPG 私钥可以被复制或者导入进 Yubikey，下面的例子是把私钥导入 Yubikey。

【译者注：私钥一旦被导入 Yubikey 即无法导出，**建议冷备份**】

```sh
❯ gpg --edit-key <keyId>

gpg> toggle
gpg> key 1
gpg> keytocard

Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection? 1

gpg> key 1
gpg> key 2
gpg> keytocard

Please select where to store the key:
   (2) Encryption key
Your selection? 2

gpg> key 2
gpg> key 3
gpg> keytocard

Please select where to store the key:
   (3) Authentication key
Your selection? 3

gpg> quit
```

确保私钥已经被移动到 Yubikey 中：

```sh
❯ gpg --list-secret-keys
```

如果你看到 `ssb>`，它显示的的是 Yubikey 上私钥的存根，意味着导入已经成功。

然后检查一下设备状态：

```sh
❯ gpg --card-status
```
