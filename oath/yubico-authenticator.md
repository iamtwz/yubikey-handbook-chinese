### 使用 Yubico 认证器

下载 [Yubico 认证器（Yubico Authenticator）](https://developers.yubico.com/yubioath-desktop/Releases/)，然后点击 `File > Add`.

如果屏幕上有二维码的话点击 `Scan a QR code` ，二维码通常使用图形表示下方链接格式的。

```
otpauth://totp/<email>?issuer=<issuer>&secret=<secret>
```

- `Credential name`：提供者的名字（比如 `GitHub` ）。
- `Secret key (base32)`：密钥（32 个字符）。
- `Credential type`：通常是 TOTP，但是 HOTP 也可以。
- `Number of digits`：通常是 6，最大也可以是 8。
- `Algorithm`：通常是 SHA-1，也可以是 SHA-256
- `Require touch`：开启

可以按照上述说明解析修改 URL 让 OTP 密钥可以存储在 1Password 中。
