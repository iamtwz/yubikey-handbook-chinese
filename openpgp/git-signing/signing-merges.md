#### Merges 签名

`git merge` 命令可以在合并没有使用 `--verify-signatures` 命令带有不可信 GPG 签名的 commit/branch 时检查和拒绝

如果被合并的分支中有任何没有被有效签名认证的提交，合并将不会继续。

Merge commit 本身也是可以被签名的（使用 `-S`）：

```
❯ git checkout -b enhancement/foo
❯ touch qux
❯ git add qux
❯ git commit -S -m "Add qux"
❯ git checkout master
❯ git merge --verify-signatures -S enhancement/foo
```
