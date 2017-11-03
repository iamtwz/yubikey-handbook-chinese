### Yubikey PIV 管理器

[Yubikey PIV 管理器](https://developers.yubico.com/yubikey-piv-manager)是一个可以管理 PIV 相关内容的图形界面管理工具。它的命令行版本可以使用 Homebrew 来安装【译者注：macOS 平台】：

```
❯ brew install yubico-piv-tool
```

命令行版本的工具拥有更加强大的功能（例如 允许覆盖 PIN 和修改默认插槽的触摸策略），但它更容易导致用户误操作。（它很容易会覆盖现有密钥）

完成 [下载](https://developers.yubico.com/yubikey-piv-manager) 和安装 Yubikey PIV 管理器和 `yubico-piv-tool`后，插入你的 Yubikey，你会被提示 [初始化你的设备](../device-initialization/README.md)。
