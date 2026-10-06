
稍微在 Google 上搜索一下通常很快就能找到副本，但获取 Windows 编译版本的 Netcat，一个比较可靠的处是位于 http://joncration.org/blog/46 的网站。

## 警告

默认情况下，许多版本的 Windows 版 Netcat 在编译时都启用了 `-e` 选项，这允许我们使用 Netcat 在系统上运行可执行文件，并通过 Netcat 的功能将其连接到网络。Windows 上的许多防病毒软件会对此感到反感，并将 Netcat 标记为恶意软件。如果这是一个问题，我们可以重新获取不带此选项的 Netcat，或者从 http://www.rodneybeede.com/Compile_Netcat_on_Windows_using_MinGW.html 载一个不包含 `-e` 选项的编译版本。

## Netcat 变体

正如我们之前提到的，Netcat 是一个开源工具。这为广大程序员和想要成为程序员的人们提供了改进的空间，他们可能倾向于对其进行重新改造，以添加功能、进行更改等。互联网上流传着大量的 Netcat 衍生版本，让我们快速查看几个，看看它们之间有什么区别。一些比较有趣的变体包括 Socat、CryptCat 和 Ncat，但这绝不是详尽列表。

Socat¹ 是 Netcat 的一种实现，提供了几个非常有趣的功能。最实用的部分之一是 Socat 可以使用许多通道来发送和接收数据，包括 TCP/IP、串口线、文件、管道等。这允许我们大幅扩展 Socat 的用途。Socat 还具有许多大其他扩展了 Netcat 能力的其它功能，更多信息可以在 http://www.destreach.org/socat/doc/README 找到。Socat 适用于 UNIX 类和 Microsoft 平台。

CryptCat² 是对 Netcat 源码的相对标准的实现，增加了一个有趣的功能：加密。CryptCat 支持 Twofish 加密，使我们能够对发送的网络流量进行加密。CryptCat 适用于 UNIX 类和 Windows 操作系统。

Ncat 是一个随 Nmap 扫描器发行一起销售的 Netcat 实现。Ncat 在本质上与 Socat 非常相似，是 Netcat 的衍生版本，添加了大量功能，包括将多个 Ncat 实例链在一起、增强了对将 Ncat 作为代理的支持、SSL 支持以及许多其他功能。Ncat 和 Nmap 一样，在多个平台上都可以运行。

现在我们已经简单讨论了 Netcat 的可能性，让我们来看一下代码。

## 简单的 Netcat 用法

在深入研究使用 Netcat 脚本可以做什么之前，让我们快速看看使用简单命令可以做什么。我们可以通过运行类似 `nc -vvvn -w 5 -z 10.0.0.1 50-80` 的命令，非常轻松地使用 Netcat 执行原始的端口扫描。在这里，我们指定运行 Netcat (nc) 时带有额外的详细输出 (vv)，并且不解析域名系统或 DNS (n)，设置 5 秒的超时时间 (-w 5)，并针对 IP 地址 10.0.0.1 的 50–80 端口使用 I/O 模式 (-z)。我们应该会得到类似下面的结果，以及针对我们扫描的对象以及在哪些端口上正在监听：

```
(UNKNOWN) [10.0.0.1] 80 (www) : Connection refused
(UNKNOWN) [10.0.0.1] 79 (finger) : Connection refused
(UNKNOWN) [10.0.0.1] 78 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 77 (rje) : Connection refused
(UNKNOWN) [10.0.0.1] 76 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 75 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 74 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 73 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 72 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 71 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 70 (gopher) : Connection refused
(UNKNOWN) [10.0.0.1] 69 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 68 (bootpc) : Connection refused
(UNKNOWN) [10.0.0.1] 67 (bootps) : Connection refused
(UNKNOWN) [10.0.0.1] 66 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 65 (tacacs-ds) : Connection refused
(UNKNOWN) [10.0.0.1] 64 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 63 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 62 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 61 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 60 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 59 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 58 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 57 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 56 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 55 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 54 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 53 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 52 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 51 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 50 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 49 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 48 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 47 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 46 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 45 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 44 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 43 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 42 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 41 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 40 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 39 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 38 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 37 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 36 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 35 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 34 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 33 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 32 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 31 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 30 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 29 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 28 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 27 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 26 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 25 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 24 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 23 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 22 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 21 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 20 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 19 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 18 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 17 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 16 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 15 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 14 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 13 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 12 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 11 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 10 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 9 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 8 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 7 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 6 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 5 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 4 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 3 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 2 (?) : Connection refused
(UNKNOWN) [10.0.0.1] 1 (?) : Connection refused
```
