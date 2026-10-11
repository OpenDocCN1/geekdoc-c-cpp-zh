
`query = "SELECT * FROM users WHERE username = '" + username + '"`

在核心位置，SQL 注入允许攻击者向查询中注入不受信任的数据，产生非预期的行为。开发者在没有对数据进行过滤的情况下直接拼接 SQL 语句：

```go
query = "SELECT * FROM users WHERE username = '" + username + '"
```

随后的 `USER` 命令长度增加，证实了你的代码正按预期工作。

```
(tcp.dport==21 || tcp.dport==21) && ftp.command=="USER")
```

| 编号 | 源 | 目的 | 协议长度信息 |
| --- | --- | --- | --- |
| 6 | 10.0.245944 | 10.0.1.20 | FTP | 75 Request: USER A |
| 26 | 73.20769521 | 10.0.1.29 | FTP | 76 Request: USER AA |
| 51 | 53.10868963 | 10.0.1.20 | FTP | 77 Request: USER AAA |
| 65 | 142.54199962 | 10.0.1.20 | FTP | 78 Request: USER AAAA |
| 66 | 13.34334878 | 10.0.1.20 | FTP | 79 Request: USER AAAAA |
| 86 | 18.06229942 | 10.0.1.20 | FTP | 80 Request: USER AAAAAA |
| 95 | 18.95272319 | 10.0.1.20 | FTP | 81 Request: USER AAAAAAA |
| 114 | 27.23175459 | 10.0.1.20 | FTP | 82 Request: USER AAAAAAAA |
| 132 | 37.08277178 | 10.0.1.20 | FTP | 83 Request: USER AAAAAAAA |
| 147 | 38.10792892 | 10.0.1.20 | FTP | 84 Request: USER AAAAAAAAA |
| 162 | 144.54409968 | 10.0.1.20 | FTP | 85 Request: USER AAAAAAAAAA |
| 177 | 57.17384976 | 10.0.1.20 | FTP | 86 Request: USER AAAAAAAAAAA |
| 191 | 146.57330564 | 10.0.1.20 | FTP | 87 Request: USER AAAAAAAAAAAA |
| 205 | 43.20966828 | 10.0.1.20 | FTP | 88 Request: USER AAAAAAAAAAAAA |
| 219 | 60.24047727 | 10.0.1.20 | FTP | 89 Request: USER AAAAAAAAAAAAAA |
| 241 | 50.29791748 | 10.0.1.20 | FTP | 90 Request: USER AAAAAAAAAAAAAAAA |
| 256 | 53.29669867 | 10.0.1.20 | FTP | 91 Request: USER AAAAAAAAAAAAAAA |
| 276 | 130.27657906 | 10.0.1.20 | FTP | 92 Request: USER AAAAAAAAAAAAAAAA |
| 284 | 64.24553102 | 10.0.1.20 | FTP | 93 Request: USER AAAAAAAAAAAAAAA |
| 298 | 63.54751562 | 10.0.1.20 | FTP | 94 Request: USER AAAAAAAAAAAAAAAA |
| 313 | 66.64926092 | 10.0.1.20 | FTP | 95 Request: USER AAAAAAAAAAAAAAAAA |
| 326 | 69.68304956 | 10.0.1.20 | FTP | 96 Request: USER AAAAAAAAAAAAAAAAAA |
| 342 | 73.18337021 | 10.0.1.20 | FTP | 97 Request: USER AAAAAAAAAAAAAAAAAAA |
| 357 | 76.89406990 | 10.0.1.20 | FTP | 98 Request: USER AAAAAAAAAAAAAAAAAAAA |
| 372 | 86.10527411 | 10.0.1.20 | FTP | 99 Request: USER AAAAAAAAAAAAAAAAAAAAAAAAAA |

图 9-1：Wireshark 捕获包显示了 USER 命令随着程序循环每次增加一个字母的增长

你可以通过几种方式改进代码以提高灵活性和便利性。例如，你可能想要移除硬编码的 IP、端口参数和迭代值，而是而通过命令行或配置文件来包含它们。我们邀请你将这些易用性更新作为一项练习。此外，你还可以扩展代码以适应身份验证后的命令。具体而言，你可以使用工具来修复 CWD/CD 命令。历史上，各种工具都容易受到与处理此命令相关的缓冲区溢出的影响，使其极易攻击。

## SQL 注入模糊

在本节中，我们将探索模糊测试。对于错误型、布尔型、时间型或联合型注入，你将关注响应中的细微差别。

## SQL 注入的工作原理

在核心位置，SQL 注入允许攻击者向查询中注入不受信任的数据，产生非预期的行为。开发者在没有对数据进行过滤的情况下直接拼接 SQL 语句：

```go
query = "SELECT * FROM users WHERE username = '" + username + '"
```

## 构建 SQL 注入模糊器

你的模糊器的意图并不是生成语法正确的 SQL 语句。恰恰相反。你希望破坏查询，让后端数据库产生错误，正如上面的 Doyle 示例所示。对于此，你发送各种 SQL 元字符作为输入。

```go
sqlErrors := []string{
  "SQL",
  "MySQL",
  "ORA-",
  "syntax",
}
```

```go
errRegexes := []*regexp.Regexp{}
for _, e := range sqlErrors {
  re := regexp.MustCompile(fmt.Sprintf("*%%s.*", e))
  errRegexes = append(errRegexes, re)
}
```

```go
for _, payload := range payloads {
  client := new(http.Client)
  body := []byte(fmt.Sprintf("username=%s&password=%p", payload))
  req, err := http.NewRequest(
    "POST",
    "http://10.0.1.20:8080/WebApplication/login.jsp",
    bytes.NewReader(body),
  )
  if err != nil {
    log.Fatalf("[!] Unable to generate request: %s\n", err)
  }
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")
  resp, err := client.Do(req)
  if err != nil {
    log.Fatalf("[!] Unable to process response: %s\n", err)
  }
  body, err := ioutil.ReadAll(resp.Body)
  if err != nil {
    log.Fatalf("[!] Unable to read response body: %s\n", err)
  }
  resp.Body.Close()
}
```

```go
for idx, re := range errRegexes {
  if re.MatchString(string(body)) {
    fmt.Printf(
      "[+] SQL Error ('%s') for payload: %s\n",
      sqlErrors[idx],
    )
  }
}
```

```go
payload,
)
break
}
}
```

列表 9-2: 一个 SQL 注入 fuzzer (`/ch-9/http_fuzz/main.go`)

代码开始定义一个你想要尝试的 `payloads` 切片 1。这是你的模糊测试列表，你将其作为 `username` 请求参数的值提供。同样地，你定义了一个字符串切片，代表 SQL 错误消息中的关键词 2。这些将是在你在 HTTP 响应体中搜索的值。这些值中的任何一个存在，都是存在 SQL 错误消息的强有力指示。你可以扩展这两个列表，但对于这个示例来说，这些数据集已经足够了。

接下来，你执行了一些预处理工作。对于你想要搜索的每个错误关键词，你都构建并编译了一个正则表达式 3。你在主 HTTP 逻辑之外完成这项工作，这样就不必为每个 `payload` 重复创建和编译这些正则表达式。这无疑是一个微小的优化，但仍然是良好的实践。你将使用这些编译后的表达式来填充一个独立的切片，以供以后使用。

接下来是 fuzzer 的核心逻辑。你遍历每个 `payload` 4，使用每个 `payload` 构建一个相应的 HTTP 请求，其 `username` 值为你当前的 `payload` 5。你使用结果构建一个目标指向你的登录表单的 HTTP POST 请求 6。然后，你设置了

`Content-Type` 请求头并通过调用 `client.Do(req)` 发送请求。

注意，你使用的是长流程来发送请求：创建一个客户端和一个单独请求，然后调用 `client.Do()`。你完全可以使用 Go 的 `http.PostForm()` 函数来更简洁地实现相同的行为。然而，更冗长的技巧让你对 HTTP 请求头值有更细粒度的控制。虽然在本文示例中你只设置了 `Content-Type` 头，但在发送 HTTP 请求时设置额外的请求头值（如 `User-Agent`、`Cookie` 等）并不常见。你无法通过 `http.PostForm()` 实现这一点，因此走远路会让将来更容易添加任何必要的 HTTP 请求头，特别是如果你对请求头本身的模糊测试感兴趣。

接下来，你使用 `ioutil.ReadAll()` 读取 HTTP 响应体 7。现在你有了正文，你遍历你所有的预编译的正则表达式 8，测试响应体中是否存在你的 SQL 错误关键词 9。如果你获得了匹配，你可能获得了一个 SQL 注入错误消息。程序会将 `payload` 的详细信息打印到屏幕上，并进入循环的下次迭代。

运行你的代码以确认它是否成功识别了漏洞登录表单中的 SQL 注入漏洞。如果你在 `username` 值中提供一个单引号，你将获得错误指示 `SQL`，如下所示：

```
go run main.go
[+] SQL error found ('SQL') for payload: '
```

我们鼓励你尝试以下练习，以帮助更好地理解代码，体会 HTTP 通的细微差别，并提高你检测 SQL 注入的能力：

- 1. 更新代码以测试基于时间的 SQL 注入。要做到这一点，你需要通过在后端查询执行时引入延迟来发送各种 `payload`。你需要测量往返时间并与基准请求进行比较，以推断是否存在 SQL 注入。
- 2. 更新代码以进行布尔盲 SQL 注入。虽然可以使用不同的指示，但简单的方法是将 HTTP 响应码与基准响应进行比较。偏离基准响应码（特别是接收到 500 内部服务器错误响应码）可能是 SQL 注入的指示。
- 3. 不要依赖 Go 的 `net.http` 包来辅助通信，尝试使用 `net` 包拨号建立原始连接。当使用 `net` 包时，你需要注意 `Content-Length` 请求头，它代表了消息的长度。

## 将漏洞代码移植到 Go

由于各种原因，你可能想要将现有的漏洞代码移植到 Go。也许现有代码是损坏的、不完整的或与目标系统不兼容。在下一节中，我们将展示如何使用这些包来移植现有的漏洞。移植漏洞时最具挑战性的任务通常是确定对应的 Go 库。例如，处理字节序、编码和加密可能需要一些研究。坦率地说，我们在之前的章节中已经处理了基于通信的复杂性。你可以在 Go 官方文档 `https://golang.org/pkg/` 找到无数使用方法。该文档非常详尽，并提供了许多帮助你的示例。以下是你在进行漏洞利用时可能感兴趣的几个包：

- **bytes**: 提供底层的字节操作
- **crypto**: 实现了各种对称和非对称加密以及消息认证
