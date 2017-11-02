#### 创建 Yubikey PAM 验证策略

##### 获取 YubiKey 的令牌 ID

Yubikey 令牌 ID 用于唯一标识一个 Yubikey。你可以用多种方法获得它。

最简单的方法是移除 Yubikey 生成的一次性密码的最后 32 位：

1. 打开一个终端.
2. 长按 Yubikey.
3. 一个一次性密码会输入到终端中:

```sh
❯ cccccccgklgcvnkcvnnegrnhgrjkhlkfhdkclfncvlgj
bash: cccccccgklgcvnkcvnnegrnhgrjkhlkfhdkclfncvlgj: command not found
```

相应的令牌 ID 是 `cccccccgklgc`:

```
cccccccgklgcvnkcvnnegrnhgrjkhlkfhdkclfncvlgj
┊←       →┊┊←            32              →┊
```

如果你有兴趣试试其他的方法的话，你可以激活本地 Yubikey PAM 模块中的调试模式然后使用它，这会将 ID 输出到调试信息中。也有一个输入令牌的 [https://demo.yubico.com/modhex.php](网页版 modhex 转换工具) 选择 _OTP_ 作为输入模式，令牌 ID 会输出到 _Modhex encoded_ 变量中。

##### 创建系统级别的 Yubikey 用户映射

创建 `/etc/yubikeys` , 它必须包含远程服务器上的 UNIX 用户名和它们的 Yubikey 令牌 ID，如果一个用户有多个 Yubikey 令牌 ID 的话用冒号分割隔开，例如：

```sh
<user-1>:<yubikey-id-1>
<user-2>:<yubikey-id-1>
<user-3>:<yubikey-id-2>:<yubikey-id-3>
```

所以在这个例子中，我们为两个不同的用户设置相同的令牌 ID：

```sh
root:cccccccgklgc
foobar:cccccccgklgc
```

然后设置正确的权限:

```sh
❯ chmod 644 /etc/yubikeys
```

##### 使用用户独立的 Yubikey 用户映射

也可以为每个用户设置独立的映射文件，在这种情况下需要移除 `authfile` 指示 。

首先在主文件夹下建立 `.yubico` 目录:

```
❯ mkdir -m700 /home/<user>/.yubico
```

然后将映射添加到 `/home/<user>/.yubico/authorized_yubikeys`:

```
<user>:<yubikey-id-1>
```
