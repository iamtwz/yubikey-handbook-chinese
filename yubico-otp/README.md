## 使用 Yubico OTP 进行双因素验证（服务端）

提高环境安全的第一步是提高客户端安全性（利用 PIV 进行 SSH 认证）和简化服务器上的管理任务（通过用户证书进行 SSH 认证），不过它们依然只依赖一个契机进行认证，是时候让双因素认证改变这一切了。

在远程服务器上为 SSH 或 `sudo` 启用双因素认证需要进行线上验证。验证服务可以选择使用由 YubiCloud 提供的 YubiHSM（硬件安全模块），或者使用在私有网络上自行托管的服务。

在私有服务器上运行 OTP 验证服务可以确保你的 Yubikey 中的 AES 密钥完全由你自己控制。不过，如果你使用 YubiCloud 管理 AES 密钥会更利于维护而且将拥有其无缝的操作体验。

YubiCloud 提供付费统计服务，每个月将通过邮件向您汇报个人化信息（包含了服务器在线时间和 Yubikey 使用率报告），付费服务选项中还有一个未定价的 SLA（服务级协议）可供需求选择。

或者你也可以考虑离线验证，例如 HMAC-SHA1 Challenge-Response（HMAC-SHA1 质询-响应）或者 U2F（Universal 2nd Factor，通用第二因素）。但是因为架构限制（HMAC-SHA1 质询-响应要求把你的 Yubikey 插入到远程服务器中）和缺乏软件支持（[OpenSSH 尚未支持 U2F 标准](https://bugzilla.mindrot.org/show_bug.cgi?id=2319)）所以目前并未广泛支持。
