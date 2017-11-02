### 使用 HMAC-SHA1 进行线下 Challenge–response 验证

新 Yubikei 支持一种称作 HMAC-SHA1 Challenge–response 验证的支持线下验证机制。适用于不需要联网又需要加强验证的环境。

典型用例是获得 `root` 权限。例如可以设置为在获得 `root` 权限上除了提供密码还需要提供 Yubikey 进行设置。
