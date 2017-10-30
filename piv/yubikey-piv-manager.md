### Yubikey PIV 管理器

[Yubikey PIV 管理器](https://developers.yubico.com/yubikey-piv-manager) 是一个拥有图形界面的可以管理 PIV 相关内容的管理器。它的命令行版本可以使用 Homebrew 安装（译者注：macOS 平台）：

```
❯ brew install yubico-piv-tool
```

这个命令行版本的工具功能更强大（比如 可以覆盖 PIN 和修改默认插槽的触摸策略），但它也更容易导致用户操作错误。比如它可以很方便的覆盖现有密钥。

完成 [下载](https://developers.yubico.com/yubikey-piv-manager) 和安装 Yubikey PIV 管理器和 `yubico-piv-tool`后，插入你的 Yubikey，你应该会被提示应该 [初始化你的设备](../device-initialization/README.md)。
