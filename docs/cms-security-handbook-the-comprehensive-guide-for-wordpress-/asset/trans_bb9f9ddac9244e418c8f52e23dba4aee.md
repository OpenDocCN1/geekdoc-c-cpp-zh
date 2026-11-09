
- **常规扫描** — 这会执行默认的 Nmap 扫描
- **缓慢全面扫描** — 这会生成以下命令：

```
nmap -sS -sU -T4 -A -v -PE -PP -PS21,22,23,25,80,113,31339 -PA80,113,143,10042 -PO --script all
```

> **注意** 有关这些选项的更多信息，请参见 http://nmap.org/book/docs/nmap-usage.txt。

## Telnet

尽管应从服务器中移除 Telnet，但它作为测试工具非常出色，并且仍是连接特定类型网络设备的常规方式。Telnet 是一种非常古老的协议，允许你连接到一台机器并发出命令。默认情况下，Telnet 运行在端口 23 上。

要在 Windows 机器上开始使用 Telnet，请单击“开始” » “附件” » “命令提示符”。在命令提示符下，键入 telnet。将出现 TELNET> 提示符。

要 Telnet 到另一台机器，请输入以下内容：

```
machine name port
```

将 machine name 替换为 IP 或主机名，将 port 替换为端口号。Telnet 可用于在配置错误的服务器上连接并发送电子邮件。例如，以下命令将尝试将你连接到邮件服务：

```
telnet machine name 25
```

如果连接成功，你通常可以通过服务器发送未经授权的电子邮件。这也是检查邮件系统中是否存在开放中继的一种方法。

以下是 Windows 版 Telnet 常用的参数列表：

- `c` — 关闭连接。
- `d` — 显示操作参数。
- `o` — 连接到主机名（默认端口 23）。
- `q` — 退出 Telnet。
- `set` — 设置选项（更多信息请参见 `set ?`）。
- `send` — 向服务器发送字符串（命令）。
- `st` — 打印状态信息。
- `-u` — 取消设置选项。
- `-? /h` — 帮助。

## Netstat

Netstat 是一个非常宝贵的工具，可用于故障排除和观察网络状况。你可以随时使用此工具查看网络连接、路由表、接口统计信息等。

以下是 Netstat 的常用选项：

- `-a` — 显示所有活动的传输控制协议（TCP）连接，以及计算机正在侦听的 TCP 和用户数据报协议（UDP）端口。
- `-e` — 显示以太网统计信息，例如发送和接收的字节数和数据包数。此参数可与 `-s` 结合使用。
- `-i` — 显示网络接口及其统计信息。
- `-n` — 显示活动的 TCP 连接。但是，地址和端口号以数字形式表示，并且不会尝试确定名称。
- `-o` — 显示哪些进程正在使用哪些套接字。
- `-r` — 显示 IP 路由表的内容。
- `-s` — 按协议显示统计信息。默认情况下，显示 TCP、UDP、Internet 控制消息协议（ICMP）和 IP 协议的统计信息。如果安装了 Windows XP 的 IPv6 协议，则显示 TCP over IPv6、UDP over IPv6、ICMPv6 和 IPv6 协议的统计信息。可使用 `-p` 参数指定一组协议。
- `-v` — 设置详细模式。
- `-V`（大写）— 显示版本信息。
- `-h` — 显示帮助。

## WireShark

WireShark 被称为*嗅探器*。它侦听网络连接并捕获每个数据包。根据网站 `www.wireshark.org/about.html` 的说法：“Wireshark 是世界上最重要的网络协议分析器。它允许你捕获并交互式浏览计算机网络中运行的流量。它是许多行业和教育机构中的事实标准（且往往是法定标准）。”

你应熟悉这个强大的工具。它是网络和服务器管理员用于排查问题的绝佳工具。

> **警告** 仅在获得许可的情况下才能在公司网络上使用 WireShark。切勿将此工具用于任何非法或不道德的任务（例如捕获密码）。仅将其用于适当的管理需求。

目前，WireShark 可用于以下平台：

- Windows 安装程序（32 位）
- Windows 安装程序（64 位）
- Windows U3（32 位）
- Windows PortableApps（32 位）
- OS X 10.5（Leopard）Intel 32 位 .dmg
- OS X 10.6（Snow Leopard）Intel 64 位 .dmg
- OS X 10.5（Leopard）PPC 32 位 .dmg

下载后，请按照适用于你的平台的安装说明进行操作。对于 Windows，必须安装 WinPcap（安装程序已包含），否则捕获将无法工作。

Windows 安装是一个相当简单的点击式过程。除非你有其他理由，否则应选择默认设置。

在 Windows 机器上，单击相应的图标即可启动 WireShark。从工具栏打开“捕获” > “接口选择”。这将提供机器上已安装的网络接口卡（NIC）列表。你的机器可能有一块有线网卡和一块无线网卡，两者都会列出。选择要从中收集数据包的网卡，然后单击“开始”。

收集过程开始后，你会看到收集窗口填满数据包。这些列表显示 IP 源、IP 目标、协议以及有关数据包的其他信息。使用此信息，你可以定位网络上的各种问题，例如损坏的网卡和非法流量（黑客）。

WireShark 可以捕获各种设备使用的许多协议。例如，你会看到的最常见数据包是用于正常 Internet 流量的 TCP/IP。IP 语音（VoIP）将使用不同的协议。选择或取消选择你要捕获信息的协议。

收集到足够的数据包后，你可以查看 WireShark 发现的错误、警告和其他信息。错误可能表明软件或配置问题。例如，如果你正在排查网络风暴，记录的错误可用于追踪违规设备。WireShark 还可以检测可能导致网络问题（如性能缓慢）的坏补丁线缆等问题。

一个非常强大的功能是搜索特定信息的能力。例如，你可以搜索来自或发往 `mail.google.com` 的所有流量。

## 后门入侵者

表 A-1 显示了已知（截至本文撰写时）的端口以及尝试使用这些端口的后门病毒和木马列表。其中许多可能已很古老，但考虑到病毒作者倾向于重用彼此的代码，追踪历史病毒非常重要。这份来自 www.sans.org/security-resources/idaq/oddports.php 和其他来源的汇编列表，如果你认为自己已被黑客入侵，可以用来交叉参考。

### 表 A-1：常见端口与后门入侵者

| 端口号 | 木马名称 |
|---:|---|
| 2 | Death |
| 20 | Senna Spy FTP server |
| 21 | Back Construction, Blade Runner, Doly Trojan, Invisible FTP, Juggernaut 42, Larva, Motly FTP, Net Administrator, Senna Spy FTP server, Traitor 21, WebEx, WinCrash |
| 22 | Shaft |
| 23 | Fire, Hacker, Tiny, Telnet, Server, TTS, Truva, Ati |
| 25 | Ajan, Antigen, Email, Password, Sender, EPS II, Gip, Gris, Happy99, Hpteam, mail, I love you, Kuang2, Magic, Horse, MBT |
| 31 | Agent 31, Hackers, Paradise, MasterParadise |
| 41 | Deep Throat, Foreplay or Reduced Foreplay |
| 48 | DRAT |
| 50 | DRAT |
| 59 | DMSetup |
| 79 | CDK, Firehotcker |
| 80 | AckCmd, BackEnd, CGI, Backdoor, Executor, Hooker, RingZero |
| 81 | RemoConChubo |
| 99 | Hidden Port |
| 110 | ProMail trojan |
| 113 | Identd, Invisible, Deamon, Kazimas |
| 119 | Happy99 |
| 121 | JammerKillah |
| 123 | Net, Controller |
| 133 | Farnaz |
| 142 | NetTaxi |
| 146 | Infector |
| 146 | (UDP) Infector |
| 170 | A-trojan |
| 180 | (TCP/UDP) amanda |
| 334 | Backage |
| 420 | Breach |
| 421 | TCP Wrappers, trojan |
| 456 | Hackers Paradise |
| 513 | Grlogin |
| 514 | RPC Backdoor |
| 531 | Rasmin |
| 559 | (TCP/UDP) teedtap |
| 605 | Secret Service |
| 666 | Attack FTP, Back Construction, Cain & Abel, NokNok, Satans Back Door, SBD, ServU, Shadow Phyre |
| 667 | SniperNet |
| 669 | DP trojan |
| 692 | GayOl |
| 777 | AimSpy, Undetected |
| 808 | WinHole |
| 911 | Dark Shadow |
| 999 | Deep Throat, Foreplay, Reduced Foreplay, WinSatan |
| 1000 | Der Späher / Der Spaether |
| 1001 | Der Späher, Der Spaether, Le |
| 1010 | Doly Trojan |
| 1011 | Doly Trojan |
| 1012 | Doly Trojan |

