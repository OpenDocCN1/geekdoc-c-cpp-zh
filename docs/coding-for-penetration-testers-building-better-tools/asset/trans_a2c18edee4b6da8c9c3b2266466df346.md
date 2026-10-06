

```
C:\WINDOWS\system32>net user admin SecUr3P4Sw0Rd! /add
The password entered is longer than 14 characters. Computers with Windows prior to Windows 2000 will not be able to use this account. Do you want to continue this operation? (Y/N) [Y]: y
The command completed successfully.
```

```
C:\WINDOWS\system32>net localgroup "System Admins" /add
The command completed successfully.
```

```
C:\WINDOWS\system32>net localgroup Administrators "System Admins" /add
The command completed successfully.
```

```
C:\WINDOWS\system32>net localgroup "System Admins" admin /add
The command completed successfully.
```

```
C:\WINDOWS\system32>_
```

# 图 10.4 添加新组并将用户分配其中。

## 收集网络信息

一旦我们获得了网络上新主机的访问权限，我们就希望尽可能地了解该主机所在的网络。我们想要知道还有哪些其他主机、该主机可以访问什么类型的网络，以及它正在与谁通信。为了确定这些内容，如果手头有一些基础的 脚本可以快速提取这些信息，将非常有帮助。

## Windows 网络信息收集

在查看 Windows 机器时，有许多事情引起我们感兴趣。我们想知道机器拥有哪些接口，以确定主机位于哪个网络以及该网络有多大。我们需要路由表，以了解更多关于网关和任何特殊路由规则的信息。我们想了解开放的连接以及管理这些连接的进程，以便识别系统的功能以及它正在与哪些系统通信。

```powershell
ipconfig /all >> c:\network.txt
route print >> c:\network.txt
arp -a >> c:\network.txt
netstat -ano >> c:\network.txt
tasklist /V >> c:\network.txt
```

（此处代码保持翻译）

我们使用 `ipconfig` 命令来收集系统上网络接口的信息，并包含一些重要内容，如域名系统（DNS）服务器、动态主机配置协议（DHCP）服务器和 DNS 名称。`/all` 参数告诉 `ipconfig` 向我们提供有关网络接口的任何信息。这确保了我们不会遗漏任何内容。我们将输出重定向到 `network.txt` 文件，这样我们就可以通过一个文件导出所有数据。

`route` 命令配合 `print` 参数显示系统所有的路由信息。从这里我们可以确定默认网关并查看任何特殊路由规则。这对于确定哪些类型的攻击能为我们跳转到下一个资源提供最佳结果非常有用。

`arp` 命令允许我们操作系统的地址解析协议（ARP）表，`-a` 参数告诉 `arp` 打印它已缓存的所有 ARP 条目。这将告诉我们主机知道本地网络上的哪些其他系统。这有助于我们在无需发送额外流量的情况下，了解本地网络上还有哪些主机。

`netstat` 命令列出开放的连接和其他网络统计。使用 `netstat -a` 选项时，告诉它列出所有连接；`-n` 选项告诉它只使用数字输出，无需尝试进行 DNS 解析；而 `-o` 列出拥有连接的进程。虽然这告诉了我们哪些连接是开启的，但我们也知道了哪个进程 ID（PID）正在使用这些连接。我们将此信息与 `tasklist` 命令合并时，就可以看到哪个应用程序在使用每个连接。

`tasklist` 命令列出系统上运行的所有进程，当我们使用详细选项 `/V` 时，可以获得进程名称、ID 甚至二进制文件的路径。这在我们查看目标主机的系统信息时，以及在排查恶意软件时都非常有用。

## Linux 网络信息收集

我们在收集 Windows 信息时使用的许多命令在 Linux 上将是相似的。我们想要收集系统上的 IP 地址、路由、DNS 信息以及网络连接，以及拥有这些连接的进程。为了收集关于哪个进程拥有每个连接的信息，我们需要在系统中拥有 root 权限。让我们构建脚本。

```bash
ip addr >> /tmp/net
echo "----------------" >> /tmp/net
cat /etc/resolv.conf >> /tmp/net
echo "----------------" >> /tmp/net
netstat -rn >> /tmp/net
echo "----------------" >> /tmp/net
netstat -anlp >> /tmp/net
```

对于我们运行的每个命令，我们可能没有明显的标题来指示它是新命令，因此我们在每个命令之间添加了行分隔符，以便方便地找到每个命令的输出。我们从 `ip` 命令开始，它显示有关 IP 栈的信息。`addr` 选项告诉命令列出系统的每个 IP 地址。要确定 DNS 信息，没有像在 Windows 中那样有一个简单的命令可以运行。收集 DNS 信息最简单的方法是查看 `/etc/resolv.conf` 文件。该文件是系统 DNS 信息的配置文件，如果所有系统工具都查询此文件，对我们来说就足够了。

要收集路由信息和其他连接信息，我们可以像 Windows 一样使用 `netstat` 命令。收集路由信息时可以使用 `-r` 选项。通过在任何命令中指定 `-n` 选项，我们指示 `netstat` 不要使用 DNS 解析，这会加快我们的执行速度。一旦路由信息打印到文件中，我们再次使用 `netstat` 打印所有连接以及拥有每个连接的进程。`-a` 参数告诉 `netstat` 显示所有连接，`-l` 参数告诉它显示监听套接字，`-p` 参数显示所有接字的程序名称和 PID。`-n` 参数显示数字地址和端口，而不是解析它们。

