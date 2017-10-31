## 设备初始化

![](../images/yubikey-4-trio.png)

_图源：Yubico_

设备初始化很简单，但在隐私保护方面需要一些方法。在将来，可以通过 MDM 组策略来改进这些下面提到的设置。

1. 如果你要进行 macOS 登录的话，请设置一个 8 个数字字符的 PIN 码。如果 PIN 码中包含字母等其他字符，macOS 将无法正常运行。使用一个安全的密码管理器生成和存储 PIN 码。
2. 设置 _钥匙管理（Management Key）_ 选项为 _使用单独的密钥（Use a separate key）_。
3. 在 _存储管理密钥（Store management key）_ 下，随机生成一个密钥并把它保存在密码管理器中。
4. 输入一个由密码管理器生成的 8 位的包含字母和数字的 PUK 码。（可以输入 A-Z、a-z、0-9 和特殊字符）
5. 当你被询问是否通过证书 _在 macOS 上设置 Yubikey（Set up Yubikey for macOS）_ 时， 选择 _否（No）_。在稍后可以更有选择性地处理。
