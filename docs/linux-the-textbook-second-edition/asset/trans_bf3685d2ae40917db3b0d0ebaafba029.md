

```
local: kernel.txz remote: kernel.txz
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for kernel.txz (32255748 bytes).
226 Transfer complete.
32255748 bytes received in 295.89 secs (106.4592 kB/s)
ftp> ls
kernel.txz
ftp> quit
421 Timeout.
$
```

一旦建立了 ftp 连接，大多数站点会将你置于二进制模式，以便你可以传输非 ASCII 文件，例如包含音频和视频剪辑的文件。你可以通过使用 binary 命令显式地将 ftp 会话置于二进制模式，这可确保正确的文件传输。你可以通过使用 ascii 命令恢复到 ASCII 模式。

在下面的章节练习中，你将使用 ftp 命令从互联网上的远程主机传输文件。

## Exercise 11.14

使用主机 **ftp.FreeBSD.org** 建立匿名 ftp 会话，并使用前面命令行会话的技术传输与软件最新版本相关的所有文件。使用 mget 命令将它们 ftp 传输到你的系统中。

## 11.8.5 SSH and Related Commands

BSD 起源的 r 命令（rsh、rcp、rlogin、r utime 等，且在 Linux 中不可用）在 *plaintext*（也称为 *cleartext*）上运行，并且不安全，就像 telnet 一样。SSH 是它们的现代替代品，消除了对 **.rhosts** 和 **hosts.equiv** 文件的需求，并且可以通过加密密钥对用户进行身份验证。它还提高了其他基于 TCP/IP 的应用程序的安全性，例如 X Windows *forwarding*，它通过 SSH 加密连接透明地“隧道传输”。处理安全连接协议的程序被称为 SSH daemon，sshd。

ssh 协议使用强大的加密来传输数据，包括命令、命令输出、密码和文件。每当你的数据传输到你的网络时，ssh 会自动对其进行加密，并在数据到达预期接收者时自动对其进行解密。结果是 *transparent encryption*——即发送方和接收方都不知道加密/解密过程。

由于这些原因，ssh 已成为 LAN 或互联网内安全终端连接的事实标准。例如，ssh、scp 和 sftp 使用的加密会话可防止任何人在 *packet sniffing* 时理解正在进行的通信。此外，ssh 中使用的身份验证方法可防止任何类型的 *spoofing*，例如 IP 地址欺骗。

SSH 版本 2 是默认协议。它有三个组件：

+   1. SSH Transfer Protocol: 处理服务器识别、加密算法和密钥加密，并管理客户端与服务器之间的通道
+   2. SSH Authentication Protocol: 验证客户端机器上用户登录角色的有效性
+   3. SSH Channel Protocol: 处理加密通道和远程 shell 会话、端口转发或 X11 转发的逻辑连接状态

在第 2 章第 2.3.3 节中，我们给出了如何使用 ssh 命令登录 Linux 系统的详细信息，ssh 命令是 SSH 协议的客户端。在该部分中，我们还描述了一些与远程系统上的 sshd（SSH Daemon）服务交互的可能方式。以下小节假定 ssh 服务已在你的主机（即客户端机器）上安装并启用，并且 sshd 守护进程在远程服务器主机上运行。

### 11.8.5.1 Remote Login with ssh

大多数 Linux 系统支持两个允许你登录远程主机的命令。它们是 telnet 和 ssh，都基于用于远程登录的 Internet 服务。当你使用 telnet 时，命令和数据以明文形式在传输通道上传输，并且在传输过程中可能被嗅探。因此，如今 telnet 几乎从未用于远程登录，我们在书中也不讨论它。在 ssh 的情况下，命令和数据通过加密通道传输。

ssh 命令允许你基本上执行与 telnet、rlogin 和 rsh 命令相同的任务，但方式更安全。如果你允许登录到远程主机或在上面执行命令，则 ssh 服务器（sshd）必须在远程机器上运行，并且你的机器必须列在服务器机器上的 /etc/hosts.equiv 或 /etc/ssh/shosts.equiv 中，并且两个机器上的用户名相同。或者，如果用户的主目录中存在 ~/.rhosts 或 ~/.shosts 文件，并且包含包含客户端机器名称和该机器上用户名称的行，则用户将被视为可登录。ssh 使用的额外安全功能包括公钥加密，以在允许用户登录到远程机器之前对用户及其主机进行身份验证。特别是，服务器必须能够在 ~/.ssh/known_hosts 中验证客户端的主机密钥，然后才允许登录。该文件包含服务器的域名和/或 IP 地址及其公钥。你可以在客户端机器上运行 more ~/.ssh/known_hosts 命令来查看此文件的内容。当你第一次运行 ssh user@domain_name 或 ssh user@IP_address 时，它会被创建。

我们只描述 ssh 命令的一些相当基本的功能，这些功能用于远程登录、远程执行命令以及在客户端和服务器机器之间传输文件。下面是 ssh 命令的简要描述：

# Syntax:

```
ssh [-option(s)] [-option argument(s)] [user@]hostname [command]
```

Purpose: ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine. It is intended to replace rlogin and rsh, and provide secure encrypted communications between two untrusted hosts over an insecure network

Output: A remote connection over a secure channel to a host on a network or the Internet

# Commonly used options/features:

+   -D [bind_address:]port
+   指定本地“动态”应用级端口转发。这通过分配套接字来侦听本地侧的端口来实现，可选择绑定到指定的 bind_address。
+   -L [bind_address:]port:host:hostport
+   指定本地（客户端）主机的给定端口应转发到远程侧的给定主机和端口。
+   -C
+   请求对所有数据进行压缩。压缩算法与 gzip 命令使用的相同。
+   -l login_name
+   指定在远程机器上登录的用户。这也可以在配置文件中按主机指定。
+   -o option
+   指定没有显式选项/标志的选项，使用配置文件中给出的格式。
+   -p port
+   如果 sshd 未在众所周知的端口（22）上运行，则指定要连接的端口。

在下面的会话中，我们在运行 SSH 服务器的远程主机 192.168.0.12 上启动一个 ssh 会话，使用默认用户名（在这种情况下与本地客户端机器上的用户名相同），执行 shell 命令，并从远程主机注销。远程机器碰巧是一台从未从此客户端建立过 ssh 连接的 OpenIndiana UNIX 机器，即你的主机。

```
$ ssh 192.168.0.12
The authenticity of host '192.168.0.12 (192.168.0.12)' can't be established.
RSA key fingerprint is 37:a2:db:ce:97:17:ce:37:26:bf:58:9d:a2:ed:1c:0f.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.12' (RSA) to the list of known hosts.
Password: xxxxxx
Last login: Tue Sep 23 08:51:38 2014
OpenIndiana (powered by illumos)    SunOS 5.11    oi_151a9    November 2013
$
...
[ Execute command line commands ]
...
$ <Ctrl+D>
Connection to 192.168.0.12 closed.
$
```

请注意，由于这是从本地客户端到远程服务器主机的第一次 ssh 连接，因此需要交换身份验证密钥。在每次后续连接中，如果密钥未更改，则不需要密钥交换。

使用以下命令，你使用用户名 sarwar 登录到主机 202.147.169.195（运行 Linux Mint18 4.4.0 的 ssh 服务器），使用 uname -a 命令显示服务器端机器的机器信息（运行 Linux Mint18 4.4.0），注销，然后在客户端机器（运行 Darwin 10.8.0）上使用 uname -a 命令显示客户端机器的信息。请注意，在此特定会话中没有交换身份验证密钥，因为这不是客户端和服务器机器之间的第一次 ssh 连接。

```
$ ssh -l sarwar 202.147.169.195
sarwar@202.147.169.195's password: xxxxxxx
Welcome to Linux Mint 18 Sarah (GNU/Linux 4.4.0-21-generic x86_64)

* Documentation: https://www.linuxmint.com
Last login: Fri Oct 27 13:56:47 2017 from 119.160.96.60
$ uname -a
Linux Mint18 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
$
...
[ Your use of the remote Linux machine using the command line interface ]
...
$ <Ctrl+D>
Connection to 202.147.169.195 closed.
$ uname -a
Darwin Sarwars-MacBook-Pro.local 10.8.0 Darwin Kernel Version 10.8.0: Tue Jun 7 16:32:41 PDT 2011; root:xnu-1504.15.3~1/RELEASE_X86_64 x86_64
$
```

以下是 somewhat atypical，但同样重要且非常有指导意义的 ssh 登录会话，以优雅的注销和 ssh 通道的终止结束。它是在 Linux Mint 客户端（192.168.0.13）和 Linux Mint 主机（192.168.0.8）之间进行的，其中 sshd 已在主机系统上安装。此示例说明了 ssh 的 known hosts 概念的使用。Known hosts 是为了使客户端和服务器相互认证以在两者之间建立安全连接而建立的。当你第一次连接到任何主机时，主机的公钥副本会存储在客户端。known host 概念可防止所谓的中间人攻击。

在第一次尝试建立 ssh 连接失败后，错误消息表明主机上的身份验证密钥已更改。这可能由于任何数量的原因而发生，包括你自己所做的更改，而不是某个攻击者。因此，在我们下面的场景中，通过删除该文件，在客户端机器上的文件 /home/bob/.ssh/known_hosts 中删除有问题的密钥。然后在你再次尝试从客户端 ssh 到主机时生成新的密钥，交换可以

