# oh-my-zsh

`zsh` 在mac下的安装和使用

## 安装

```shell
# 安装
#linux下没有自带zsh需要手动安装 
yum -y install zsh.x86_64
#mac下自带zsh无需安装
#安装oh-my-zsh
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
# 创建配置文件
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
# 这只zsh为默认和终端
chsh -s /bin/zsh
# 安装其他主题 下载到~/.oh-my-zsh/themes
# 下载链接 https://github.com/robbyrussell/oh-my-zsh/wiki/themes
```

## .zshrc 配置文件

```shell
	export ZSH="/Users/{你的用户名}/.oh-my-zsh"
  ZSH_THEME="amuse" # 主题设置
  DEFAULT_USER=$USER
  plugins=(git last-working-dir wd) # 插件
  # wd插件 可以给目录添加索引，进入/a/b/c/d然后执行wd add test，之后无论在哪里执行wd test都会进入到/a/b/c/d
  export PATH="/usr/local/opt/redis@4.0/bin:$PATH" # 环境变量
  source $ZSH/oh-my-zsh.sh 
  source /Users/jinzhiwen/.zshSource/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh  #命令高亮
  source /etc/profile #开机加载其他环境变量配置
```

这里需要注意使用zsh后,环境变量文件不再在`~/.bash_profile`和`/etc/profile`配置 环境变量的设置应该在`~/.zshrc`中

## 命令高亮配置

```shell
#下载插件： 
1. 下载插件： git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
#在.zshrc的plugins中添加
zsh-syntax-highlighting，plugins={... zsh-syntax-highlighting}
```



## 自动补全插件

```shell
#下载：http://mimosa-pudica.net/zsh-incremental.html
#进入plugins文件夹：
cd ~/.oh-my-zsh/plugins
#创建一个新的文件夹并进入：
mkdir incr; cd incr
#创建一个新的文件：
touch incr-0.2.zsh
#把下载下来的文件拷贝过来：
cp /Users/jasper/Downloads/incr-0.2.zsh incr-0.2.zsh
#赋予该文件最高权限：
chmod 777 ~/.oh-my-zsh/plugins/incr/incr-0.2.zsh
#在./zshrc中加入这样一句话：source ~/.oh-my-zsh/plugins/incr/incr-0.2.zsh
#让配置文件生效：
source ~/.zshrc
#配置完成，现在已经有自动补全了	
```

