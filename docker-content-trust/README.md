## Docker 内容信任

Docker 内容信任允许你在不安全的网络上通过签名容器传递信任的映像。Docker 引擎可以在整个 Docker 工作流 (`push`, `pull`, `build`, `create` 和 `run` 操作）中验证映像的完整和更新程度。Docker 中的 Notary 是一种常见的集成设施。

Notary 是一个基于 [The Update Framework](http://theupdateframework.com/) 的工具。它提供了一些解决在网络中安全传递更新的问题和防范某些常见攻击类型的措施：

- 通过对每一层进行数字签名防范映像被篡改。
- 通过提供开箱即用的密钥轮换机制防范密钥盗取攻击。
- 通过使用时间戳密钥确保内容最新防范重放攻击。

Docker Hub 提供一个 Notary 服务用于验证官方签名的映像。如果你在运行一个私有仓库（例如在 Amazon ECR 上），你需要设置一个私有 Notary 服务。
