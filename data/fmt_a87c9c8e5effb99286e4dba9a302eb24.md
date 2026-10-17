
| ESTAB | 0 | 0 | 192.168.61.128:55262 | 216.58.222.64 |

| LISTEN | 0 | 5 | ::1 | *:*

## tcpdump

`tcpdump` is a powerful command-line tool for network traffic monitoring and analysis. The `tcpdump` command is used to create "dumps" or "traces" of network traffic and can also be launched in the background by other tools. Monitoring network traffic through `tcpdump` requires high privileges, so most commands are prefixed with `sudo`. As already mentioned at the beginning of this section, our aim is not to reference tools but rather introduce few examples and point out a specific reference. This section discusses the basic options. It is worth mentioning that `-in` is a combination of `-i` and `-n`. Below, a chunk of data packets is shown as an example.

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode listening on ens3, link-type Ethernet, capture size 262144 bytes
```

The command `sudo tcpdump -i any` may be adopted to listen on all interfaces. Now, use one of the lines shown above. For instance, consider the line

```
16:28:07.471548 ubuntu.ntp > a.stl.ntp.br.ntp: NTPv4, client length 48
```

This first field (`16:28:07.471548`) depicts that the packets were traveling, in this format: hh:mm:ss. The second field shows the source hostname, by the destination hostname, `ubuntu.ntp > a.stl.ntp.br.ntp`. The third field is Network Time Protocol (`NTP4`). The fourth field shows whether a host is a client or server. In this case, it is a client (`Client`), and the last field represents the TCP packet length in Bytes (`48`).

## 性能测量

主要的区别在于源主机和目的主机名被 IP 地址和端口取代。因此，第二个字段显示源主机地址和端口，随后是目的主机地址和端口，`192.168.61.128 > 200.186.195.123`。

也可以使用选项 `-c` 来指定要就绪的数据包数量，例如 `sudo tcpdump -i any -c 10`，其中 `-c` 之后的数字表示捕获的数据包数量。在命令中，`tcpdump` 在获取十 (`10`) 个数据包后就会完成进程。下面展示了收集到的段信息示例。

```
tcpdump: verbose output, -v or -vv for full protocol listening on any, link-type LINUX_XX (Linux connected), capture size 262144 bytes
21:53.47.023515 192.168... ...
```

```
21:53.47.17619 192.168.61.128.17500 > 54.225.82.232.123: 192.168.61.128.123: IPv4, Client,
```

```
21:53.47.98319 192.168.61.128.17500 > 255.255.255.17500: UDF, length 242
```

```
21:53.47.96808 192.168.61.128.17500 < 255.255.255.17500: UDF, length 242
```

```
21:53.47.98629 192.168.61.128.17500 > 255.255.255.17500: UDF, length 242
```

```
21:53.47.98738 192.168.61.128.17500 > 192.168.61.128.130:130: UDP, length 242
```

```
21:53.47.96118 192.168.61.128.17500 < 255.255.255.17500: UDP, length 242
```

```
21:53.51.02394 192.168.61.128.123 > 192.36.143.130.123: IPv4, Client,
```

+ 10 packets

过滤器接收了 10 个包

内核丢弃了 0

选项 `-X` 除了每个数据包的头部外，还会以十六进制和 ASCII 格式打印每个数据包的数据。例如，考虑命令行 `sudo tcpdump -i any -c 3`。该命令切换所有接口、源和目的地址以及相应的端口，并以十六进制和 ASCII 格式显示每个包的内容（选项 `-A` 仅以 ASCII 显示内容）。这当管理员想要分析数据包内容时非常有用。典型输出如下：

```
tcpdump: verbose output, -v or -vv for full protocol listening on any, link-type LINUX_XX (Linux connected), capture size 262144 bytes
16:37:23.034421 192.168.61.128.123 > 164.146.48.5: IPv4, Client,
```

```
0000 4b8b 000c 5e25 4000 401f a1fa c0a9 3d80 E..L%8...
0010 925a 30d5 0070 003b 0078 1fbc 2302 08e6 ....0.(I..#..
0020 0000 265d 0000 08c1 05f5 f2c1 02b6 10f5 ...f........
0030 6619 98d2 e8c6 10b4 f57da 22c1 02b6 10f5 ...f........
0040 f000 f000 f000 f000 f000 f000 f000 f0000 .........
```

```
16:37:23.168734 164.146.48.5 > 192.168.61.128.123: IPv4, Server,
```

```
0000 4500 02c6 2000 8011 a8ae 92a4 0305 ....E..L.......O,
```

```
0010 0c1a 38d0 0077 003b 00e4 0241 0060 ....W.(I..S..
```

```
0020 0000 0000 0012 4750 5300 02e6 10ef 00ec ....GPS.1....
```

```
0030 241f 7404 02e6 10f3 08e7 00d4 02e6 10f2 ..S.t......1...
```

```
0040 e5f3 dd38 e2c 02e6 10f2 e5fd 4eaf ....f...3...1......
```

16:37:24.034421 192.168.61.128.123 > 110.195.253.123: IPv4, Client

## 性能、可靠性与可用性

例如，如上所示，在第一个数据包头部之后，`16:37:23.034792 192.168.61.128.123 > 164.48.53.123: IPv4, Client`，我们获取数据包的内容：

```
0000 4500 02c6 2000 8011 a8ae 92a4 0305 ....E..L.......
```

（注：OCR 文本在地址处有一些乱码，但根据上下文，我已经清理了它们）。等等，让我们重新检查流：例如，如上所示，`16:37:23.034792 192.168.61.128.123 > 164.48.53.123: IPv4, Client`。

```
0000 4500 02c6 2000 8011 a8ae 92a4 0305 ....E..L.......
```

### 表 23.1 TCP 标志

| 值 | 标志类型 | 描述 |

| :--- | :--- | :--- |

| S | SYN | 连接开始 |

| F | FIN | 连接结束 |

| P | PUSH | 数据推送 |

| R | RST | 连接重置 |

| - | ACK | 确认 |

`50394` 是端口号。在源和目的地址之后，提供了 TCP 标志；在这种特定情况下，它是（表 23.1 显示了一些典型标志）。下一个是捕获数据包中的序列号。后续数据包使用相对数以便于跟踪。在此示例中，序列为 `2921:4381`，这意味着该包包含了 `2921` 到 `4381` 的流。这是确认号 `ack`。在发送数据包时，`ack` 值为 `430`。窗口大小 (`win 62440`) 指定接收缓冲区中的可用字节数。最后，数据包长度（in字节）是最后一个 (`4381`) 和第一个 (`2921`) 字节之间的差，即 `4381 - 2921 = 1460`。

`tcpdump` 允许通过各种参数过滤捕获的数据包，例如源和目的 IP 地址、端口。例如，我们想要捕获 ICMP 包。命令行 `tcpdump -i any icmp > tcpdump_test` 嗅探所有接口的 ICMP 包并将流量头部写入 `tcpdump_test`。下面显示了典型的数据段：

```
18:10:44.754016 ubuntu > ec2-54-204-132.compute.amazonaws.com: ICMP request,
id12648, seq 1, length 64
18:10:44.953102 ubuntu > ec2-54-204-132.compute.amazonaws.com : ubuntu: ICMP reply,
id12648, seq 1, length 64
18:10:45.396782 ubuntu > ec2-54-204-132.compute.amazonaws.com: ICMP
```

头部的内容取决于数据包的类型。然而，TCP 头部有一个第一个字段表示接收或发送数据包的时间戳。该字段表示网络层协议（IPv4 为 IP，IPv6 为 IP6）。在这种情况下，我们有 IP。下一个字段是源 IP 和端口 (`80`)。用于 HTTP 流量。下一个字段是目的 IP 地址和端口 `192.168.61.128.50394`。

`tcpdump` 命令能够监控许多协议，如 IP、UDP、ICMP 等。这里的目的不是帮助读者入门。不同协议的细节和格式可以在 `tcpdump` 的手册中找到。假设 `tcpdump` 捕获的数据包如下：

```
16:14:06.396782 192.168.61.128.50394 > 192.168.61.128.50394: Flags [], seq 2921:4381, ack 430, win 62440, length 1460
```

同样，我们可以根据源或目的主机名嗅探数据包。命令行 `sudo tcpdump -i any -c 4 -n src 54.204.39.132 > tcpdump_test` 嗅探来自 `54.204.39.132` 的数据包并将流量头部写入文件 `tcpdump_test`。下面显示了典型的数据段：

```
18:10:02.273334 192.168.61.128.50394 > 192.168.61.128.50394: Flags [], seq 2921:4381, ack 430, win 62440, length 1460
```

同样，命令行 `sudo tcpdump -i any -c 4 -n dst 54.204.39.132 > tcpdump_test` 嗅探发送到 `54.204.39.132` 的数据包并将流量头部写入文件 `tcpdump_test`。下面显示了典型的数据段：

```
18:10:03.286058 192.168.61.128.50394 > 192.168.61.128.50394: Flags [], seq 2921:4381, ack 430, win 62440, length 1460
```

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

我们也可以通过使用 `portrange` 选项来查找端口范围内的流量，例如 `tcpdump port 21-23`。值得注意的是，端口号被分为三个范围：已知端口、注册端口和动态或私有端口 [`404`]。已知端口也称为系统端口，范围从 0 到 1023。表 23 描述了一些重要的系统端口。

可以使用逻辑运算符（如 `and`、`or`、`not`）组合选项以创建更复杂的过滤器。例如，命令 `sudo tcpdump -ni any -c10 src`

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
