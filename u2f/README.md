## U2F（安全钥匙）

U2F 是 FIDO 联盟创立的用于网站进行公钥加密的开放认证标准。身份验证是通过提供的公钥给每个服务新建一个钥匙对来进行的。验证期间，客户端通过对服务器发起的挑战进行签名来证明它拥有私钥。【译者注：挑战即 挑战—应答验证 - Challenge–response authentication】

交换过程中不需要手动输入或复制代码也让 U2F 更加方便，且不容易收到网络钓鱼和中间人攻击（MITM），只需要触摸 Yubikey 即可批准签名。

最新版本的的 Chrome 和 Opera 浏览器默认支持 U2F 协议。尽管需要模拟 UA （`Develop > User Agent > Chrome for Mac`），但 Safari 可以在安装 [Safari-FIDO-U2F](https://github.com/blahgeek/Safari-FIDO-U2F) 插件的情况下使用 U2F。

当把 Yubikey 作为安全钥匙时，我们建议把 `Yubikey (<serial number in decimal format>)` 作为别名的格式。

[许多网站](http://www.dongleauth.info) 支持 U2F，如【译者注：[这里是官方列表](https://www.yubico.com/solutions/)】：

- Google
- GitHub
- Dropbox
- Sentry

![](../images/sentry-u2f.png)

_在 [sentry.io](https://sentry.io)_ 注册 U2F 设备

在这篇文章中 *[Security Keys: Practical Cryptographic Second Factors for the Modern Web](http://fc16.ifca.ai/preproceedings/25_Lang.pdf)* Google  详细介绍了给它的 50000 余名员工部署安全钥匙的经验。
