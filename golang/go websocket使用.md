# go websocket使用

## websocket是什么

> websocket其实就是 使用http请求来进行tcp握手的 tcp链接
>
> 客户端会通过http请求发送将链接升级为websocket的请求
>
> 如果握手成功那么就会建立websocket链接

## go websocket实现

上面已经提到wesocket是给予http的所以go的websocket也要给予httpserver

大概思路就是 当收到符合某种规则的请求时 将他升级为websocket链接接下来就是收发消息了

### 构建http服务

`net/http` 是golang原生提供的http服务

```go
package main
 
import (
	"fmt"
	"io"
	"net/http"
)
 
func main()  {
	http.HandleFunc("/", helloWorld)   // 注册路由 设置回调函数
	e:=http.ListenAndServe(":8888",nil)  // 监听ip端口
	if e!=nil{
		fmt.Println(e.Error())
	}
}
 
func helloWorld(w http.ResponseWriter, r *http.Request)  {
	str:="Hello World"
	n,e:=io.WriteString(w, str)
	if e!=nil{
		fmt.Println(e.Error())
	} else {
		fmt.Println(n," " ,len(str))
	}
```

`n,e:=io.WriteString(w, str)`

这里注意这一行 golang的说有输入输出 其实都可以理解为读取文件与写入文件

### golang的websocket包

golang没有原生支持websocket 所以我这里选用了 

`gorilla/websocket`包

GitHub：https://github.com/gorilla/websocket
Doc：https://godoc.org/github.com/gorilla/websocket

###gorilla/websocket 介绍

上面提到了 websocket的核心就是将http请求升级为websocket

#### [Upgrader](https://github.com/gorilla/websocket/blob/master/server.go#L26)


```go
type Upgrader struct {
  // 握手的超时时间
	HandshakeTimeout time.Duration

	// 读写的缓冲区大小 如果设置为0 则自动读取 http服务的缓冲区大小
	ReadBufferSize, WriteBufferSize int

	// 写操作的缓冲池 可以理解为一个 缓冲队列 需要实现GET方法和PUT方法
	WriteBufferPool BufferPool

	// 支持的协议列表 客户端在请求头中通过Sec_WebSocket-Protocol 指定要使用的协议
  // 如果不在我们定义的协议列表中则res header中不会返回协议成功
	Subprotocols []string

  // 自定义http错误 如果不设置则使用默认http错误码
	Error func(w http.ResponseWriter, r *http.Request, status int, reason error)

	// 验证这个请求是否为握手请求 返回false拒绝握手
	CheckOrigin func(r *http.Request) bool

  // ture表示服务器是否尝试支持 压缩(RFC 7692) 不能保证压缩一定生效
	EnableCompression bool
}
```

#### func (*Upgrader) [Upgrade](https://github.com/gorilla/websocket/blob/master/server.go#L123)

Upgrade 函数将 http 升级到 WebSocket 协议。定义如下：

```go
// responseHeader包含在对客户端升级请求的响应中。 
// 使用responseHeader指定cookie（Set-Cookie）和应用程序协商的子协议（Sec-WebSocket-Protocol）。
// 如果升级失败，则升级将使用HTTP错误响应回复客户端
// 返回一个 Conn 指针，拿到他后，可使用 Conn 读写数据与客户端通信。
func (u *Upgrader) Upgrade(w http.ResponseWriter, r *http.Request, responseHeader http.Header) (*Conn, error)
```

