## OATH 认证（TOTP 和 HOTP）

开放认证（OATH）负责开发被 [广泛](https://twofactorauth.org/) 使用的两种标准 ——  TOTP （基于时间） 和 HOTP（基于计数）。

Yubikey 可以在触摸时反馈一个 HOTP 的 Token， 但是由于 Yubikey 没有内部时钟，所以需要配合应用程序（[Yubico Authenticator](https://developers.yubico.com/yubioath-desktop)）使用 TOTP 认证。

**为什么使用 Yubikey 进行 OATH 认证**？

- 共享密钥只被安全的存储在 Yubikey 中。
- 可以在任意计算机上使用，不容易受到传统移动设备的限制（比如没电）。
