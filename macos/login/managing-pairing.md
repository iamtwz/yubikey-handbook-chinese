#### 管理配对

随 macOS 提供的 `sc_auth` 工具 (_smart card authorization setup script，智能卡认证设置脚本_) 可以执行大量的和智能卡相关的操作。

1. 列出用户 `foobar` 的智能卡 hash：

  ```sh
  ❯ sc_auth list -u foobar
  ```

2. 为用户 `foobar` 取消配对名为 `bar` 的智能卡：

  ```sh
  ❯ sc_auth unpair -u foobar -h bar
  ```

3. 为用户 `foobar` 取消配对所有的智能卡：

  ```sh
  ❯ sc_auth unpair -u foobar
  ```

4. 当插入新智能卡时不显示配对窗口：

  ```sh
  ❯ sc_auth pairing_ui -s disable
  ```
