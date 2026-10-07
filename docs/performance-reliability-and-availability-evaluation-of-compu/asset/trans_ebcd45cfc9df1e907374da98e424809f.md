

## 性能测量

## 403

20:37:27.179439 192.168.61.128 > 54.204.39.132: ICMP echo request, id 18958, seq 1, length 64
20:37:28.180844 192.168.61.128 > 54.204.39.132: ICMP echo request, id 18958, seq 2, length 64
20:37:29.182550 192.168.61.128 > 54.204.39.132: ICMP echo request, id 18958, seq 3, length 64
20:37:30.184904 192.168.61.128 > 54.204.39.132: ICMP echo request, id 18958, seq 4, length 64

假设我们需要捕获与特定服务相关的包，或者常用的命令 `sudo tcpdump -i any -c5 -n port 80 > tcpdump_sniff` 用于捕获端口 80（HTTP 流量）的包并将流量头写入文件 `tcpdump.log`。下面是一个示例展示的信息块。

20:55:56.878693 192.168.61.51116 > 150.161.2.980: Flags [S], seq 326656976, win 29200, options [ms 1460, sackOK, TS val 6698408, ecr 0, wscale 7], length 0

20:55:57.036618 150.161.2.980 > 192.168.61.51116: Flags [S], seq 1039757299, ack 326656976, win 64240, options [ms 1460], length 0

20:55:57.036647 192.168.61.51116 > 150.161.2.980: Flags [,], ack 1, win 29200, length 0

20:56:00.920350 192.168.61.51116 > 150.161.2.980: Flags [P], seq 1460, ack 1, win 29200, length 459: HTTP: GET /wp-content/uploads/thesis/Erico.Erico HTTP/1.1

20:56:00.921007 150.161.2.980 > 192.168.61.51116: Flags [], ack 460, win 64240, length 0

20:56:01.148625 150.161.2.980 > 192.168.61.51116: Flags [], seq 1461, ack 460, win 64240, length 1460: HTTP: HTTP/1.1 200

20:56:01.148648 192.168.61.51116 > 150.161.2.980: Flags [,], ack 1461, win 32120, length 0

我们也可以通过使用 portrange 选项来查找端口范围内的流量，例如 `tcpdump port 21-23`。值得注意的是，端口号被分为三个范围：已知端口、注册端口和动态或私有端口 [404]。已知端口也称为系统端口，范围从 0 到 1023。表 23 描述了一些重要的系统端口。

可以使用逻辑运算符（如 and、or、not）组合选项以创建更复杂的过滤器。例如，命令 `sudo tcpdump -ni any -c10 src`

## 404 计算系统的性能、可靠性和可用性评估

### 表 23.2 一些系统端口

| 端口号 | 分配 | 传输 |
| :--- | :--- | :--- |
| 20 | File Transfer (FTP) | 数据传输 |
| 21 | File Transfer (FTP) | 控制 |
| 22 | Secure Shell (SSH) | 安全登录 |
| 23 | Telnet | 远程登录 |
| 25 | Mail Transfer (SMTP) | 邮件传输 |
| 53 | Domain Name (DNS) | 域名系统 |
| 67, 68 | Dynamic Host Configuration (DHCP) | 主机配置 |
| 80 | Hypertext Transfer (HTTP) | 超文本传输 |
| 110 | Office Protocol (POP) | 邮局协议 |
| 119 | News Protocol (NNTP) | 新闻协议 |
| 123 | Network Time Protocol (NTP) | |
| 143 | Internet Message Access (IMAP) | 消息访问 |
| 161 | Simple Network Management (SNMP) | 网络管理 |
| 194 | Internet Relay (IRC) | 聊天 |
| 443 | HTTP over TLS/SSL | |
| 3306 | MySQL | |

192.168.61.128 and 80 > tcpdump_test 仅包含来自 192.168.61.128 和 80 的流量。使用逻辑运算符可以创建更复杂的过滤器。对于上述命令，tcpdump_test 的典型内容如下：

12:25:28.713401 192.168.61.128 > 150.161.2.90:80: Flags [S], seq 2199567800, win 29200, options [ms 1460, sackOK, TS val 69756968, ecr 0, wscale 7], length 0

12:25:28.909354 192.168.61.128 > 150.161.2.90:80: Flags [], ack 21364378, win 29200, length 0

12:25:29.932347 192.168.61.128 > 150.161.2.90:80: Flags [P], seq 0:458, ack 1, win 29200, length 458: HTTP: GET /wp-content/uploads/thesis/Tese-Joao.pdf HTTP/1.1

12:25:30.186727 192.168.61.128 > 150.161.2.90:80: Flags [], ack 161, win 32120, length 0

12:25:30.186787 192.168.61.128 > 150.161.2.90:80: Flags [], ack 2921, win 35040, length 0

12:25:30.186822 192.168.61.128 > 150.161.2.90:80: Flags [], ack 4273, win 37960, length 0

12:25:30.200124 192.168.61.128 > 150.161.2.90:80: Flags [], ack 5733, win 40880, length 0

## 性能测量

```
12:25:30.200250 IP 192.168.61.128.51282 > 150.161.2.90:80 Flags [], ack 7193, win 43800, length 0
```

```
12:25:30.200345 IP 192.168.61.128.51282 > 150.161.2.90:80 Flags [], ack 8653, win 46720, length 0
```

```
12:25:30.200422 IP 192.168.61.128.51282 > 150.161.2.90:80 Flags [], ack 9969, win 49640, length 0
```

tcpdump 命令可以使用 -w 选项生成二进制格式的 dump 文件。该选项将输出保存在 `file-name.pcap` 文件中，可以使用 tcpdump 的 -r 选项进行读取。值得注意的是，除非是……无法使用文本编辑器打开 pcap 后的文件。

这些基本功能将帮助你开始使用 tcpdump。有关 tcpdump 选项和过滤器的详细说明，请参考 [426]。同样重要的是，分析师可能不仅限于 tcpdump 工具。还有许多用于监控和分析流量的有用工具，例如 Wireshark [467]、NetworkMiner [303]、SolarWinds [405]、WinDump [466] 和 Ngrep [307]。

## ping 命令

ping 用于检查主机的可达性。上述命令 tcpdump_test 文件的典型内容如下：（为了简洁已省略）。

iperf 是一个用于测量 TCP 和 UDP 吞吐量的开源工具。它可以在许多操作系统上运行。

## 计算系统的性能、可靠性和可用性评估

让我们配置客户端和服务器。如上所述，我们的服务器是一个基于 Windows 的系统。我们使用以下 PowerShell 命令行将其配置为服务器：

```
iperf -s -il
```

客户端计算机是一台 Linux 机器，通过执行命令行将其配置为客户端：

```
iperf -c 192.168.61.1 -il -t60
```

上述选项允许我们设置许多配置。在这里，我们展示了测试 TCP 和 UDP 流量的简单设置。首先，让我们配置客户端和服务器来测试 TCP 流量。

