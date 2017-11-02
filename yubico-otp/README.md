## 使用 Yubico OTP 进行双因素验证（服务端）

提高环境安全性的第一步是提高客户端安全性（利用 PIV 进行 SSH 认证）和简化服务器上的管理任务（通过用户证书进行 SSH 认证），不过它们仍然依赖一个因素进行认证，是时候让双因素认证改变这一切了。

在 SSH 或者 `sudo` 时启用双因素认证需要在服务器上进行线上验证。可以使用由 YubiCloud 自己的 YubiHSM（硬件安全模块）提供的验证服务，或者在私有网络上自行托管。

在私有服务器上运行 OTP 验证服务可以确保你的 Yubikey 中的 AES 密钥完全由你自己控制。另一个方面，如果使用 YubiCloud 管理你的 AES 密钥可以提供无缝且易于维护的体验。

YubiCloud 也提供付费服务（价格未公开），包括统计信息（包含服务器在线时间和 Yubikey 使用统计的月度报告电子邮件）和 SLA（服务级别协议）。

或者也可以考虑离线验证，例如 HMAC-SHA1 Challenge-Response（HMAC-SHA1 质询-响应）或者 U2F（Universal 2nd Factor，通用第二因素）。虽然目前因为架构限制（HMAC-SHA1 质询-响应要求把你的 Yubikey 插入到远程服务器中）和缺乏软件支持（[OpenSSH 尚未支持 U2F 标准](https://bugzilla.mindrot.org/show_bug.cgi?id=2319)）而并未广泛支持。
