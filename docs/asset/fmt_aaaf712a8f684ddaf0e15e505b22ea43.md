
```go
type result struct {
	IPAddress string
	Hostname string
}
```

你将为此工具查询两个主要的记录类型——`A` 和 `CNAME`。你将在单独的函数中执行每次查询。将函数尽可能小并让每个函数只做好一件事是一个好主意。这种开发风格允许你从以后编写更小的测试。

## 查询 A 和 CNAME 记录

你将两个函数来执行查询：一个用于 `A` 记录，另一个用于 `CNAME` 记录。这两个函数都接受 `FQDN` 作为第一个参数，并将 `DNS` 服务器地址作为第二个参数。每个函数都应该返回一个字符串切和一个错误。将这些函数添加到你在 `5-3` 中开始的代码中。

```go
func lookupA(fqdn, serverAddr string) ([]string, error) {
	var m dns.Msg
	var ips []string
	m.SetQuestion(fqdn, dns.TypeA)
	in, err := dns.Exchange(&m, serverAddr)
	if err != nil {
		return nil, err
	}
	if len(in.Answer) < 1 {
		return ips, errors.New("no answer")
	}
	for _, answer := range in.Answer {
		if a, ok := answer.(*dns.A); ok {
			ips = append(ips, a.String())
		}
	}
	return ips, nil
}
```

```go
func lookupCNAME(fqdn, serverAddr string) ([]string, error) {
	var m dns.Msg
	var fqdn []string
	m.SetQuestion(fqdn, dns.TypeCNAME)
	in, err := dns.Exchange(&m, serverAddr)
	if err != nil {
		return nil, err
	}
	if len(in.Answer) < 1 {
		return fqdn, errors.New("no answer")
	}
	for _, answer := range in.Answer {
		if c, ok := answer.(*dns.CNAME); ok {
			fqdn = append(fqdn, c.Target)
		}
	}
	return fqdn, nil
}
```

这段代码看起来很熟悉，因为它和你在本节节的代码几乎相同。第一个函数 `lookupA` 返回 `IP` 地址列表，而 `lookupCNAME` 返回主机名列表。`CNAME`或别名记录将一个 `FQDN` 指向另一个作为前者的别名。例如，假设 `example.com` 的所有者想要托管一个 `WordPress` 服务。该服务可能由于其所有用户有数百个 `IP` 地址，提供单个网站的 `IP` 地址是不可行的。该服务可以提供一个别名（`CNAME`），供 `example.com` 的所有者引用。因此，`www.example.com` 可能有一个指向 `server.hostingcompany.org` 的 `CNAME`，后者又指向一个 `IP` 地址。这允许 `example.com` 的所有者在他们没有 `IP` 信息的服务器上托管站点。

这通常意味着你需要跟踪 `CNAME` 链以最终找到一个有效的 `A` 记录，因为可能会出现无限的 `CNAME` 链。将函数放在以下代码之外 `main()` 查看如何利用 `CNAME` 链跟踪有效记录：

```go
func lookup(fqdn, serverAddr string) []result {
	var results []result
	var cfdn = fqdn // 不要修改原始值
	cnames, err := lookupCNAME(fqdn, serverAddr)
	if err != nil && len(cnames) > 0 {
		cfdn = cnames[0]
		continue // 我们必须处理下一个 CNAME。
	}
	ips, err := lookupA(fqdn, serverAddr)
	if err != nil {
		break // 此主机名没有 A 记录。
	}
	for _, ip := range ips {
		results = append(results, result(IPAddress: ip, Hostname: fqdn))
	}
	break // 我们已经处理了所有结果。
	return results
}
```

没有发生错误且至少有一个 `CNAME` 返回了结果 `4`，将 `cfqdn` 设置为返回的 `CNAME` `5`，使用 `continue` 返回循环开头 `6`。此过程允许你追踪 `CNAME` 的路径，直到发生失败。如果发生失败（意味着你已到达链的末端），你可以查找 `A` 记录 `7`；但如果发生其他错误（表示记录查找出现问题），则提前跳出循环。如果有有效的 `A` 记录，将返回的每个 `IP` 地址追加到你的结果切切片中 `8`，并跳出循环 `9`。最后，将结果返回给调用者。

我们与名称解析相关的逻辑似乎是合理的。然而，你还没有考虑到性能。让我们让示例中的 `goroutine` 变得友好型，以便你添加并发处理。

## 传递给工作函数

你将创建一个 `goroutine` 池，并将工作传递给执行单元工作的工作函数。你将通过通道（`channels`）协调工作分发和结果收集。回想你在第 `2` 章构建并发端口扫描器时过的类似操作。

继续扩展列表 `5-3` 中的代码。首先，创建 `worker()` 函数并将其放在 `main()` 之外。该函数接收三个通道参数：一个用于工作者信号其已关闭的通道，一个用于接收任务的域名通道，以及一个用于发送结果的通道。该函数还需要一个最后的字符串参数来指定使用的 `DNS` 服务器。以下代码展示了 `worker()` 函数的示例：

```go
type empty struct() {
```

```go
func worker(tracker chan empty, fqdns chan string, gather chan []result,
serverAddr string) {
  for fqdn := range fqdns {
    results := lookup(fqdn, serverAddr)
    if len(results) > 0 {
      gather <- results
    }
  }
  var e empty
  tracker <- e
}
```

在引入 `worker()` 函数之前，先定义类型 `empty` 以跟踪工作者何时完成。这个结构体没有任何字段；你使用空结构体是因为它的大小为 `0` 字节，使用时几乎不会产生影响或开销。然后，`worker()` 函数遍历用于传入 `FQDN` 的域名通道。在从你的 `lookup()` 函数获取结果并确保至少有一个结果后，将结果发送到 `gather` 通道，该通道会在 `main()` 中累积结果。当工作循环因通道已关闭而退出时，会向 `tracker` 通道发送一个空结构体，以通知调用者所有工作已完成。在 `tracker` 通道上发送空结构体是重要的最后一步。如果不这样做，将会产生竞态条件，因为调用者可能会在 `gather` 接收到结果之前就退出。

由于此时所有基础结构都已就绪，让我们重新关注 `main` 以完成我们在列表 `5-3` 中开始的程序。定义一些存储结果的变量以及传递给 `worker()` 的通道。然后将以下代码追加到 `main()`：

```go
var results []result
fqdns := make(chan string, *flWorkerCount)
gather := make(chan []result)
tracker := make(chan empty)
```

使用用户提供的工作者数量将 `fqdns` 通道创建为缓冲通道。这允许工作者启动得快一点，因为通道在阻塞发送者之前可以持有多条消息。

## 使用 bufio 创建扫描器

接下来，打开用户提供的文件作为词列表。打开文件后，使用 `bufio` 包创建一个新的扫描器。扫描器允许你逐行读取文件。将以下代码追加到 `main()`：

```go
fh, err := os.Open(*flWordlist)
if err != nil {
    panic(err)
}
defer fh.Close()
scanner := bufio.NewScanner(fh)
```

当返回的错误不为 `nil` 时，使用内置函数 `panic()`。当你编写包供他人使用时，应该考虑以更整洁的展示这些信息。你将使用新的扫描器从提供的词列表中获取行文本，并结合用户提供的文本创建 `FQDN`。你会将结果发送到 `fqdns` 通道。但必须先启动工作者，顺序非常重要。如果你在启动工作者之前向 `fqdns` 通道发送工作，缓冲区最终会填满，导致你的生产者阻塞。你会将以下代码添加到 `main()` 函数中。其目的是启动 `goroutine`、读取输入文件并处理 `fdns` 通道。

```go
for i := 0; i < *flWorkerCount; i++ {
  go worker(tracker, fqdns, gather, *flServerAddr)
}
```

```go
for scanner.Scan() {
  fmt.Printf("%s.%s", scanner.Text(), *flDomain)
}
```

这种模式与你构建并发扫描器时的做法相似：直到用户提供的数字循环使用 `scanner.Scan()`。当文件中没有更多可读行时，循环结束。获取扫描文件的每一行的字符串表示。工作已启动！花点时间思考你在程序中的位置，然后我们将引导你完成剩余部分。

## 收集并显示结果

为了完成任务，首先启动一个匿名 `goroutine` 从工作者那里收集结果。将以下代码追加到 `main()`：

```go
go func() {
  for r := range gather {
    results = append(results, r...)
  }
  var e empty
  tracker <- e
}()
```

通过遍历 `gather` 通道，将接收的结果追加到 `results` 切片。由于你是将一个切片追加到另一个切片，必须使用 `...` 语法。在关闭 `gather` 通道后，向 `tracker` 通道发送一个空结构体，正如你之前做的那样。这样做是为了防止在向用户展示结果时 `append()` 未完成导致的竞态条件。在 `main()` 的底部包含以下代码以关闭通道并展示结果：

```go
close(fdns)
for i:=0; i < *flWorkerCount; i++ {
  <-tracker
}
close(gather)
<-tracker
```

第一个可以关闭的通道是 `fdns`，因为你已经向该通道发送了所有工作。接下来，为每个工作者从 `tracker` 通道接收一次，允许工作者信号已退出。考虑到所有工作者，你就可以关闭 `gather` 通道，因为没有更多结果可以接收。最后，在 `tracker` 通道上接收一次以允许收集程序完全完成。

结果尚未展示给用户。让我们修复这个问题。你可以轻松遍历结果并使用 `fmt.Fprintf()` 打印 `Hostname` 和 `IPAddress` 字段。我们更倾向于使用 `Go` 的几个内置包来展示数据；`tabwriter` 是我们最喜之一。它允许你通过制表符展示整齐的列数据。在 `main()` 的末尾添加以下代码使用 `tabwriter` 处理结果：

```go
w := tabwriter.NewWriter(os.Stdout, 0, 8, 4, '\t', 0)
for _, r := range results {
    fmt.Fprintf(w, "%s\t%s\t\n", r.Hostname, r.IPAddress)
}
w.Flush()
```

### 列表 5-4 显示完整的程序。

```go
package main

import (
	"bufio"
	"errors"
	"flag"
	"fmt"
	"os"
	"text/tabwriter"

	"github.com/miekg/dns"
)

func lookupA(fqdn, serverAddr string) ([]string, error) {
	var m dns.Msg
	var ips []string
	m.SetQuestion(dns.Fqdn(fqdn), dns.TypeA)
	in, err := dns.Exchange(&m, serverAddr)
	if err != nil {
		return nil, err
	}
	if len(in.Answer) < 1 {
		return ips, errors.New("no answer")
	}
	for _, answer := range in.Answer {
		if a, ok := answer.(*dns.A); ok {
			ips = append(ips, a.A.String())
			return ips, nil
		}
	}
	return ips, nil
}

func lookupCNAME(fqdn, serverAddr string) ([]string, error) {
	var m dns.Msg
	var fqdn []string
	m.SetQuestion(dns.Fqdn(fqdn), dns.TypeCNAME)
	in, err := dns.Exchange(&m, serverAddr)
	if err != nil {
		return fqdn, err
	}
	if len(in.Answer) < 1 {
		return fqdn, errors.New("no answer")
	}
	for _, answer := range in.Answer {
		if c, ok := answer.(*dns.CNAME); ok {
			fqdn = append(fqdn, c.Target)
		}
	}
	return fqdn, nil
}

func lookup(fqdn, serverAddr string) []result {
	var results = []result{result}
	var cfdn = fqdn // Don't modify the original.
	For {
		cnames, err := lookupCNAME(fqdn, serverAddr)
		if err == nil && len(cnames) > 0 {
			cfdn = cnames[0]
			continue // We have to process the next CNAME.
		}
	}
}
```

```go
ips, err := lookupA(cfdn, serverAddr)
if err != nil {
    break // 此主机名没有 A 记录。
}
for _, ip := range ips {
    results = append(results, result{IPAddress: ip, Hostname: fqdn})
}
break // 我们已经处理了所有结果。
return results
```

```go
func worker(tracker empty, fqdns chan, gather chan []result,
serverAddr string) {
    for fqdn := range fqdns {
        results := lookup(fqdn, serverAddr)
        if len(results) > 0 {
            gather <- results
        }
    }
    var e empty
    tracker <- e
}
```

```go
type empty struct {}
type result struct {
    IPAddress string
    Hostname string
}
```

```go
func main() {
    var (
        flDomain = flag.String("domain", "", "用于进行猜测的域名。")
        flWordlist = flag.String("wordlist", "", "用于猜测的字典列表。")
        flWorkerCount = flag.Int("c", 100, "使用的 worker 数量。")
        flServerAddr = flag.String("server", "8.8.8.8:53", "使用的 DNS 服务器。")
    )
    flag.Parse()
}
```

```go
if *flDomain == "" || *flWordlist == "" {
    fmt.Println("-需要 -domain 和 -wordlist")
    os.Exit(1)
}
```

```go
var results []Result

fdns := make(chan string, *flWorkerCount)
gather := make(chan []Result)
tracker := make(chan empty)
```

```go
fh, err := os.Open(*flWordlist)
if err != nil {
    panic(err)
}
defer fh.Close()
scanner := bufio.NewScanner(fh)
```
