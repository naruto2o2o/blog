# go mod 使用



## 为什么使用go mod



之前我们开发golang,需要在gopath下新建项目,再使用其他工具将依赖打包进vendor目录.现在使用go mod可以摆脱go path的限制 并且在`go build` 或者 `go run` 时可以自动下载依赖

## 基本使用

```shell
go mod download # 下载依赖的 module 到本地 cache
go mod edit     # 编辑 go.mod
go mod graph    # 打印模块依赖图
go mod init     # 在当前目录下初始化 go.mod(就是会新建一个 go.mod 文件)
go mod tidy     # 整理依赖关系，会添加丢失的 module，删除不需要的 module
go mod vendor   # 将依赖复制到 vendor 下
go mod verify   # 校验依赖
go mod why      # 解释为什么需要依赖
```

## 开始

```shell
#go env -w 设置 goenv 也可以 export 
go env -w GO111MODULE="auto"   # 设置 gomod 为自动 在 gopath 外自动使用 gomod
go env -w GOPROXY="https://goproxy.cn,direct"  # 设置 go源为七牛云
go env -w GOPRIVATE="你的项目" # 设置私有库 如 gitlab 等
mkdir gomodtest ## 在任意目录创建项目目录
vim main.go
```

main.go 内容
```go
package main

import (
	"github.com/gin-gonic/gin"
)

func main() {
	gin.New()
}

```

继续

```shell
go mod init ## 初始化 生成go.mod文件

go: cannot determine module path for source directory /home/mac/Desktop/learn/gomodetest (outside GOPATH, module path must be specified)

Example usage:
	'go mod init example.com/m' to initialize a v0 or v1 module
	'go mod init example.com/m/v2' to initialize a v2 module

Run 'go help mod init' for more information.
```

你需要给你的mod起一个名字

```shell
go mod init nimabi
cat go.mod

# go.mod内容
module nimabi  # 模块名称

go 1.13   # go版本信息

# 下面执行 go run 或者go build 就会自动安装相关依赖 并且声称依赖表文件 go.sum
go mod  tidy # 同步所有依赖
```



