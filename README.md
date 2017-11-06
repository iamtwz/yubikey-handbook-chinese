# Yubikey 使用手册

_Now featured on the [3rd-Party Labs (3PL) - YubiKey Innovations and Inspirations](https://forum.yubico.com/viewtopic.php?f=8&t=1942) compilation_.

Yubikey 是由 Yubico 制作的一个硬件设备，它能提供多种形式的高强度的认证与加密，能运用在不同的地方。除此之外，Yubico还有许多有趣的软件。

_Yubikey 使用手册_ 意在发掘这些用途并生动形象的展示给你。 它主要内容是讲述 Yubikey 4 和 Yubikey 4 Nano的使用方法。事实上，经过一些改动之后，部分内容也同样适用于 Yubikey NEO。

![](./images/yubikey-plugged-in.jpg)

_图源: Yubico_

这本书现在可以 [免费在线阅读](https://ruimarinho.gitbooks.io/yubikey-handbook/content/)，并且可以下载它的 [PDF](https://www.gitbook.com/download/pdf/book/ruimarinho/yubikey-handbook), [ePUB](https://www.gitbook.com/download/epub/book/ruimarinho/yubikey-handbook) 或者 [Mobi/Kindle](https://www.gitbook.com/download/mobi/book/ruimarinho/yubikey-handbook) 版本。

# 关于

## 英文原版

https://github.com/ruimarinho/yubikey-handbook

## 作者

Rui Marinho （[github](https://github.com/ruimarinho)，[twitter](https://twitter.com/ruipmarinho)，[npm](https://www.npmjs.com/~ruimarinho)）日常是一名软件开发者，下班后是一名安全工程师，在周末时是个网络管理员。掌握丰富技能的他能够规划并建设大型基础建设项目。他有处理棘手任务的专业性，例如维护要求安全保障措施严格的高可用性系统。[阅读更多](introduction/about-the-author.md)

## 译者

目前这本书的译者有：

* 使用二把刀初中英语的 [Wenzel Tian](@iamtwz)，未特别注明的应该都是他翻译的了。

* 某谜之 [Horo](@KenOokamiHoro) 

* 咸鱼一只 [inkiron](@inkiron)

如果有问题，请提交 Issues。

我们遵循 [中文排版指北](https://github.com/sparanoid/chinese-copywriting-guidelines) 进行排版。

许多专有名词不知道怎么翻译比较好，Docker 部分因为不会 Docker 可能需要另外一个人帮忙翻译，如果你有兴趣欢迎加入我们。

在本书中，译者注的内容均写在「【】」中。

## 协议

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />这个作品使用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a> 协议共享。

 # 翻译进度

- [介绍](README.md) （100%）
  - [关于作者](introduction/about-the-author.md)（100%）
- [个人身份验证 (PIV)](piv/README.md)（100%）
  - [在 Yubikey 上使用 PIV](piv/use-cases.md)（100%）
  - [Yubikey PIV 管理器](piv/yubikey-piv-manager.md)（100%）
- [设备初始化](device-initialization/README.md)（100%）
- [使用  PIV 和 PKCS#11 验证 SSH（客户端）](ssh/authenticating-ssh-with-piv-and-pkcs11-client/README.md)（100%）
  - [故障排除](ssh/authenticating-ssh-with-piv-and-pkcs11-client/troubleshooting.md)（100%）
- [使用用户证书验证 SSH （服务端）](ssh/authenticating-ssh-via-user-certificates-server/README.md)（100%）
  - [生成密钥吊销列表 (KRL) ](ssh/authenticating-ssh-via-user-certificates-server/generating-the-key-revocation-list-krl.md)（100%）
- [验证 SSH 服务器证书（客户端）](ssh/authenticating-ssh-host-certificates-client/README.md)（100%）
  - [附加内容](ssh/authenticating-ssh-host-certificates-client/additional-resources.md)（100%）
- [通过 Yubico OTP 进行双因素认证（服务端）](yubico-otp/README.md)（100%）
  - [设置远程服务器](yubico-otp/setting-up-a-remote-server/README.md)（100%）
    - [环境配置（仅限演示）](yubico-otp/setting-up-a-remote-server/prerequisites-demonstration-only.md)（100%）
    - [为 OpenSSH 启用双因素认证（sshd）](yubico-otp/setting-up-a-remote-server/configuring-openssh-sshd-for-2fa-authentication.md)（100%）
    - [安装 libpam-yubico](yubico-otp/setting-up-a-remote-server/installing-libpam-yubico.md)（100%）
    - [创建 Yubikey PAM 验证策略](yubico-otp/setting-up-a-remote-server/creating-the-yubikey-pam-authentication-policy.md)（100%）
    - [Yubikey 验证模块](yubico-otp/setting-up-a-remote-server/yubikey-authentication-module.md)（100%）
  - [测试](yubico-otp/testing.md)（100%）
- [OATH 认证（TOTP 和 HOTP）](oath/README.md)（100%）
  - [使用 Yubico 认证器](oath/yubico-authenticator.md)（100%）
- [U2F （安全钥匙）](u2f/README.md)（100%）
- [Docker 内容信任](docker-content-trust/README.md)
  - [钥匙管理](docker-content-trust/key-management.md)
  - [运行 Notary 服务](docker-content-trust/notary/README.md)
    - [配置 Notary](docker-content-trust/notary/configuring.md)
    - [管理证书](docker-content-trust/notary/certificates.md)
    - [附加内容](docker-content-trust/notary/additional-resources.md)
  - [发布一个已签名的 Docker 镜像](docker-content-trust/pushing-signed-image/README.md)
    - [在 Yubikey 上生成根证书](docker-content-trust/pushing-signed-image/generating-the-root-key.md)
    - [发布镜像](docker-content-trust/pushing-signed-image/pushing-a-signed-docker-image.md)
  - [在远程仓库上列出已签名的镜像](docker-content-trust/listing-signed-images-on-a-remote-repository.md)
  - [角色授权](docker-content-trust/delegation-roles/README.md)
    - [生成一个授权密钥](docker-content-trust/delegation-roles/generating-a-delegation-key.md)
    - [导入授权证书](docker-content-trust/delegation-roles/importing-a-delegation-certificate.md)
    - [使用授权密钥](docker-content-trust/delegation-roles/using-a-delegation-key.md)
    - [在 CI 系统上自动签名镜像](docker-content-trust/delegation-roles/automating-image-signing-on-ci-systems.md)
  - [删除一个授权密钥](docker-content-trust/removing-a-delegation-key.md)
  - [轮换钥匙](docker-content-trust/key-rotation/README.md)
    - [钥匙镜像](docker-content-trust/key-rotation/snapshot-key.md)
    - [时间戳钥匙](docker-content-trust/key-rotation/timestamp-key.md)
    - [目标钥匙](docker-content-trust/key-rotation/targets-key.md)
  - [阈值签名验证](docker-content-trust/threshold-validation-signing.md)
- [OpenPGP 套件](openpgp/README.md)（100%）
  - [触摸保护](openpgp/touch-protection/README.md)（100%）
    - [启用触摸保护](openpgp/touch-protection/enabling-touch-protection.md)（100%）
  - [导入钥匙](openpgp/importing-keys.md)（100%）
  - [修改元数据](openpgp/editing-metadata.md)（100%）
  - [Git 签名](openpgp/git-signing/README.md)（100%）
    - [Tags 签名](openpgp/git-signing/signing-tags.md)（100%）
    - [Tags 验证](openpgp/git-signing/verifying-tags.md)（0%）
    - [Commits 签名](openpgp/git-signing/signing-commits.md)（0%）
    - [Commits 验证](openpgp/git-signing/verifying-commits.md) （0%）
    - [Merges 签名](openpgp/git-signing/signing-merges.md)（0%）
    - [Pushes 签名](openpgp/git-signing/signing-pushes.md)（0%）
  - [使用 GPG 进行 SSH 验证](openpgp/authenticating-ssh-with-gpg.md)（0%）
  - [故障排除](openpgp/troubleshooting/README.md)（0%）
    - [GPG 无法签名数据](openpgp/troubleshooting/gpg-failed-to-sign-the-data.md)（0%）
- [集成至 macOS](macos/README.md)（100%）
  - [使用 HMAC-SHA1 进行线下挑战答应](macos/offline-authentication/README.md)（100%）
    - [配置 HMAC-SHA1 挑战答应](macos/offline-authentication/configuration.md)（100%）
  - [登录和钥匙串验证](macos/login/README.md)（100%）
    - [配对管理](macos/login/managing-pairing.md)（100%）
