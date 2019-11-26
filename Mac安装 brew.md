# Mac 安装 brew

1. 打开终端复制命令

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

中间会提示多次输入密码

2. 卸载

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

3. 替换国内阿里云

```shell
# 替换brew.git
cd "$(brew --repo)" && \
git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git && \
# 替换homebrew-core.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && \
git remote set-url origin
https://mirrors.aliyun.com/homebrew/homebrew-core.git && \
# 刷新源
brew update
```

