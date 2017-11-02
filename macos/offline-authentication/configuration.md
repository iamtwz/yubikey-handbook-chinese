#### 配置 HMAC-SHA1 Challenge-Response 验证

第一步是为验证设置你的 Yubikey，可以通过 [Yubikey 设置工具](https://itunes.apple.com/us/app/Yubikey-personalization-tool/id638161122?mt=12) 或 `ykpersonalize` 命令行工具完成。

##### 通过 _ykpersonalize_ 工具

从安装 `ykpers` 开始:

```sh
❯ brew install ykpers
```

然后:

```sh
❯ ykpersonalize -2 -ochal-resp -ochal-hmac -ohmac-lt64 -ochal-btn-trig
```

基本含义为:

- 使用 2 号插槽 (`-2`)
- 使用 challenge-response 模式（`-ochal-resp`）
- 生成 HMAC-SHA1 challenge 响应（`-ochal-hmac`）
- 在小于 64 字节的输入集上计算 HMAC（`-ohmac-lt64`）
- 允许通过 API 调用读取这个 Yubikey 的序列号（`-oserial-api-visible`）。 -

##### 使用 _Yubikey 设置 Tool_

1. 插入你的 Yubikey
2. 点击 _Challenge-Response_
3. 选择 _HMAC-SHA1_ 模式
4. 选择 _Configuration Slot 2_
5. 选择 _Require user input (button press)_
6. 设置 _Variable input_ 为 HMAC-SHA1 模式
7. 点击 _Write Configuration_ 不要写入任何日志，因为这会暴露写入到 Yubikey 中的私钥。

##### 生成初始 challenge

安装 `pam_yubico`:

```sh
❯ brew install pam_yubico
❯ mkdir -m0700 -p ~/.yubico
```

生成初始 Challenge 请求:

```
❯ ykpamcfg -2
```

##### 启用 Challenge-Response 验证模块

为了避免被 `sudo` 锁定确定 `pam_yubico.so` 是否存在 :

```sh
❯ test -e /usr/local/opt/pam_yubico/lib/security/pam_yubico.so && echo "File exists, you may proceed."
```

用 `sudo` 打开一个新的 shell（确保你在把 PAM 文件改坏以后还能改回来）。

然后用另一个 shell 将下面一行添加到 `/etc/pam.d/sudo` 起始：

```sh
auth       required     /usr/local/opt/pam_yubico/lib/security/pam_yubico.so mode=challenge-response
```

开启一个新的 shell ，确认你在运行相应的命令时需要 Yubikey 操作:

```sh
❯ sudo -l
```

记住你要按 Yubikey 两次————一次用于验证现有的 challenge ，一次用于在成功以后生成新的 challenge。
