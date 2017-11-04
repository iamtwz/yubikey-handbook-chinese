## 设备初始化

![](../images/yubikey-4-trio.png)

_图源：Yubico_

设备初始化非常简单，但在安全隐私管理方面需要一些系统性方法。在将来，这可以通过定义 MDM 分发的组策略来加强这些下面提到的措施。

1. 设置一个 8 个数字字符的 PIN 码使 macOS 如期登录。如果 PIN 码中包含字母等其他字符，macOS 将无法工作。你可以使用一个安全的密码管理器生成和存储 PIN 码。
2. 设置 _钥匙管理（Management Key）_ 选项为 _使用单独的密钥（Use a separate key）_。
3. 在 _存储管理密钥（Store management key）_ 下，随机生成一个密钥并把它保存在密码管理器中。
4. 输入一个由密码管理器生成包含字母和数字的 8 位 PUK 码。（可以输入 A-Z、a-z、0-9 和特殊字符）
5. 当你被询问是否通过证书 _在 macOS 上设置 Yubikey（Set up Yubikey for macOS）_ 时， 如果选择 _否（No）_，在稍后可以更有选择性地处理。
