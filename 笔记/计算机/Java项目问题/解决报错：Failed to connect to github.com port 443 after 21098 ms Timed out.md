今天在连接[github](https://so.csdn.net/so/search?q=github&spm=1001.2101.3001.7020)仓库时遇到了一个报错：  Failed to connect to github.com port 443 after 21098 ms: Timed out（译为：21098 毫秒后无法连接到 github.com 端口 443：超时）。

**原因：** 这样的问题往往是由于网络慢访问超时，这时候我们可以在终端选择使用设置代理和取消代理的命令解决。

### 设置代理：

```lua
git config --global https.proxy
```

### 取消代理：

```scss
git config --global --unset https.proxy
```

###  解决步骤：我们直接在终端先输入设置代理的命令，再输入取消代理的命令即可解决