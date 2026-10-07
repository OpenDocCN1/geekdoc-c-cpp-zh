
任何发往 `192.168.2.0` 网络的数据包将通过 `192.168.0.1` 网关发送。如果你想添加更多路由，可以将它们添加到 `ifcfg` 文件中。

## 企业级网络配置

到目前为止，本章的网络配置集中在设置单个系统连接网络上。Linux 可用的功能可以通过支持主机通信所需的实际网络基础设施来进一步扩展。

本节介绍了 Linux 中的一些网络功能。这些功能的完整实现超出了本书的范围，但如果你发现自己需要管理网络功能，本节将让你对这些功能的实现方式有一个直的了解。

# 第四部分：成为 Linux 服务器管理员

`ip_forward_live`，去掉了 `/proc/sys` 并用点替换了斜杠。你可以通过这种方式更改在 `/proc/sys` 目录结构中设置的任何内核参数。

当 Linux 系统被用作路由器时，它通常被用私有网络与公共网络（如互联网）之间的防火墙。如果是这样，你可能还想将该系统作为具有地址转换（NAT）并提供 DHCP 服务的防火墙，这样私有网络上的系统就可以使用私有 IP 地址通过 Linux 系统进行路由。（有关使用 `iptables` 工具操作 Linux 防火墙规则的信息，请参见第25章“网络上的 Linux 安全”。）

# 配置 Linux 为 DHCP 服务器

Linux 系统不仅可以使用 DHCP 服务器获取其 IP 地址和其他信息，还可以配置为自己充当 DHCP 服务器。在最基本的形式下，DHCP 服务器可以从地址池向任何收到的请求分发 IP 地址。然而，DHCP 服务器还会分发 DNS 服务器的位置和默认网关。

配置 DHCP 服务器不是一项可以在不经思考的情况下完成的工作。不要在你不控制且已经有工作良好的 DHCP 服务器的网络上添加 DHCP 服务器。许多客户端被设置为从任何分发地址的 DHCP 服务器获取信息。

DHCP 服务由 Fedora 和 RHEL 中的 `dhcp` 软件包提供。在 RHEL 6 中，该服务命名为 `dhcp`，在 RHEL 7 和最新的 Fedora 版本中命名为 `dhcpd`。用于 IPv4 网络的主要配置文件是 `/etc/dhcp/dhcp.conf`（同一目录下有一个 `dhcp6.conf`，用于为 IPv6 网络提供 DHCP 服务）。默认情况下，`dhcp` 守护进程监听 UDP 端口 `67`，因此请记住在你的防火墙上开启该端口。

要配置 DHCP 服务器，你可以从 `/usr/share/doc/dhcp-*` 目录复制 `dhcpd.conf` 文件并替换 `/etc/dhcp/dhcpd.conf` 文件。然后根据你的需要进行修改。在使用之前，你想要将域和 IP 地址范围更改为你你正在使用的范围。文件中的注释将帮助你完成此操作。

你在 Linux 系统上安装虚拟化和云服务时，默认会在该系统中为你设置一个 DHCP 服务器。例如，当你在 RHEL 或 Fedora 中安装 KVM 和 `libvirtd` 时，它会自动配置一个 `192.168.122.0/24` 地址范围内的私有网络。当你启动虚拟机时，它们将获得该范围内的 IP 地址。在这些 Linux 发行版上安装并启动 Docker 服务时，同样会设置私有网络并向在该系统启动的 Docker 容器分发 IP 地址。

# 配置 Linux 为 DNS 服务器

在 Linux 中，专业的域名系统（DNS）服务器是使用伯克利互联网域名（BIND）服务实现的。它在 Fedora 和 RHEL 中通过安装 `bind`、`bind-utils` 和 `bind-libs` 软件包来实现。为了增加安全性，有些人人会安装 `bind-chroot` 软件包。

默认情况下，通过编辑 `/etc/named.conf` 文件来配置 `bind`。主机名-IP 地址映射在位于 `/var/named` 目录下的区域文件中完成。如果你安装了 `bind-chroot` 软件包，`bind` 配置文件会被移动到 `/var/named/chroot` 目录下，该目录尝试从 `/etc` 和 `var` 复制配置 `bind` 所需的文件，因此 `named` 守护进程（提供服务）被限制在 `/etc/named/chroot` 目录。

如果你有兴趣尝试 `bind`，我建议你先尝试为小型家庭网络配置 DNS，这样可以让你家中的成员之间的通信变得更简单。你可以通过将每台电脑网络接口的 MAC 地址附加到 DHCP 服务器上以指定 IP 地址，从而锁定家中机器的 IP 地址，然后在 DNS 服务器中将这些名称映射到地址。

> **注意：**在创建创建公共 DNS 服务器之前，请记住，妥善地保护你的 DNS 服务器非常重要。一个被破解的公共 DNS 服务器可能被用于将流量定向到坏人选择的任何服务器。因此，如果你这样做，你就面临着访问并非你认为的网站的危险。

# 配置 Linux 为代理服务器

代理服务器提供了一种限制从私有网络到公共网络（如互联网）网络流量的方法。此类服务器是锁定学校计算机房或限制员工访问的网站的极佳方法。

通过物理上将 Linux 设置为路由器，但将其配置为代理服务器，你家庭或业务网络上的所有系统都可以配置为使用某些协议访问互联网，并且仅在你过滤流量后进行。

使用大多数 Linux 系统自带的 Squid 代理服务器（Fedora 和 RHEL 中的 `squid` 软件包），你可以让系统接受对 Web 服务器（HTTP 和 HTTPS）、FTP 以及其他服务的请求。你可以限制哪些系统可以使用你的代理（通过主机名或 IP 地址），甚至限制它们可以访问哪些网站（通过特定地址、地址范围或域名）。

配置 `squid` 代理服务器可以变得如安装 `squid` 软件包、编辑 `/etc/squid/squid.conf` 文件并启动 `squid` 服务一样简单。该文件带有一个推荐的最小配置。然而，你可能想要定义你允许服务访问的主机（基于 IP 地址或名称）。`squid` 提供了黑列表，允许你拒绝访问可能不适合儿童访问的网站。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_412.png)

www.it-ebooks.info

373

# 第四部分：成为 Linux 服务器管理员

## 总结

大多数来自 Linux 桌面或笔记本系统的网络连接可以在很少或没有用户干预的情况下完成。如果你在有线或无线连接上使用 `NetworkManager`，启动所需的地址和服务器信息可以从 DHCP 服务器自动获取。

通过 `NetworkManager` 的图形界面，如果你喜欢可以进行一些网络配置。你可以设置静态 IP 地址并选择要使用的网络服务器和网关计算机。对于手动和复杂的网络配置，考虑关闭 `NetworkManager` 并直接通过配置文件工作。

Linux 中的网络配置文件可以用于设置更高级的功能，例如以太网绑定（Ethernet bonding）。要使用这些高级服务，你可以启用网络服务。

除了 Linux 网络连接的基础知识外，还有功能可以让你提供基础设施类型的服务。本章介绍了路由、DHCP 和 DNS 等服务，你在处理高级网络功能时需要了解。

配置好网络后，你现在可以开始配置在网络上运行的服务。第15章描述了你用于启用、禁用、启动、停止和检查系统配置的服务所需的工具。

# 练习

本节的练习帮助你检查和更改 Linux 系统上的网络接口，并了解如何配置高级网络功能。在具有活动网络连接的 Linux 系统上开始这些练习。

通常有多种方法可以完成这些练习描述的任务。如果你卡住了，请参考附录 B 中显示的任务解决方案。

- 1. 使用桌面检查 `NetworkManager` 是否成功启动了你的网络接口（有线或无线）并连接到网络。如果没有，请尝试启动你的网络接口。
- 2. 运行命令检查你计算机上可用的活动网络接口。
- 3. 尝试从命令行连接 `google.com`，并确保 DNS 正常工作。
- 4. 运行命令以检查与本地网络之外通信时使用的路由。
- 5. 追踪连接到 `google.com` 经过的路径。
- 6. 关闭并禁用 `NetworkManager` 并启动网络服务。
- 7. 创建一个主机条目（host entry），允许你使用 `myownhost` 与本地主机系统进行通信。
- 8. 将公有 Google DNS 服务器（IP 地址 `8.8.8.8`）添加到你的 DNS 服务器列表的末尾。
- 9. 创建一个自定义路由，将目标为 `192.168.99.0/255.255.255.0` 网络的流量重定向到本地网络上的某个 IP 地址，例如 `192.168.0.5`（首先确保你所在的位置没有使用 `10.0.99` 网络）。
- 10. 检查你的系统是否配置为允许 IPv4 数据包在系统的不同网络接口之间路由。

## 第 15 章

## 服务的启动与停止

## 本章内容

- 理解各种 Linux init 服务
- 审计由 Linux 守护进程（daemon）控制的服务
- 停止和启动服务
- 修改 Linux 服务器的默认运行级别（runlevel）
- 移除服务

Linux 服务器系统的主要工作是为本地或远程用户提供服务。服务器可以提供 Web 页面、文件数据库信息、流媒体音乐或其他类型的内容的访问。名称服务器提供主机计算机或用户名列表的访问。在你的 Linux 系统上，可以配置数百种此类或其他类型的服务。

Linux 系统提供的持续服务（例如访问打印机服务或登录服务）通常由所谓的“守护进程”（daemon process）实现。大多数 Linux 系统都有一种方法，使用几种流行的初始化系统之一（也称为 init 系统）来将每个守护进程作为服务进行管理。使用 init 系统的优点包括能够实现以下：

- **识别运行级别**——将一组服务组合在所谓的运行级别（runlevels）或目标（targets）中
- **建立依赖关系**——设置服务依赖关系，例如，需要网络接口的服务在所有启动服务成功启动之前不会启动。
- **设置默认运行级别**——选择系统启动时启动哪个运行级别或目标。
- **管理服务**——运行命令指示单个服务启动、停止、重启或重新加载配置文件

如今，Linux 系统使用了多种不同的 init 系统。你使用的哪一个取决于你正在使用的 Linux 发行版和版本。在本章中，我将介绍在 Fedora、红帽企业 Linux（Red Hat Enterprise Linux）和 Ubuntu 中使用的以下 init 系统：

- **Sysinit**——这种传统的 init 系统为 20 世纪 80 年代初的 UNIX 系统创建。它提供了一种基于运行级别的简单启动和停止方法。直到几年前，大多数 UNIX 和 Linux 系统都使用 Sysinit。
- **Upstart**——在 Ubuntu 中流行并在 Fedora 和 RHEL 中短暂使用过，该系统改进了服务之间依赖关系的处理，并可以显著提高启动时间。它最近在 Fedora 和 RHEL 中被 systemd 取代。
- **Systemd**——最新版本的 Fedora 和 RHEL 使用 systemd init 系统。它是 init 系统中最复杂的，但提供了更大的灵活性。Systemd 不仅提供了启动和处理服务的特性，还允许你管理设备、挂载点、交换区域和其他单元类型。

本章描述了这三个 init 系统。在在使用与你的 Linux 发行版匹配的 init 系统过程中，你将学习启动过程是如何启动服务的、你如何如何单独停止服务，以及如何启用和禁用。

### 理解初始化守护进程（或 systemd）

为了理解服务管理，你需要理解初始化守护进程。初始化守护进程可以被认为是“所有进程之母”。这个守护进程是内核在 Linux 服务器启动的第一个进程。对于使用 Sysinit 或 Upstart 的 Linux 发行版，init 守护进程的名字就叫 `init`。对于 `systemd`，内核的进程 ID（PID）为 `0`。因此，初始化进程（或 `systemd`）的父进程 ID 为 `1`。一旦启动，它负责在引导启动时产生（启动）进程，例如登录 shell（`getty`）。它还负责管理服务。

`init` 守护进程基于 Unix V init。它被称为 Sysinit。然而，它并不是唯一的经典 init 守护进程。它不是 Linux 内核的一部分。因此，它可以有不同的变体，Linux 发行版可以选择使用哪种版本。另一个经典的 init 守护进程基于 Berkeley UNIX，也称为 BSD。因此，原始的 init 守护进程是 BSD 和 Sysinit。

经典的 init 守护进程多年来运行良好。然而，这些守护进程的设计是为了在静态环境中工作。随着新硬件（如热插拔设备）的出现，经典 init 守护进程只能大致处理这些其他设备。计算机硬件从静态转变为事件驱动。需要新的 init 守护进程来处理这些流动的环境。

此外，随着新服务的出现，经典的 init 守护进程必须处理更多的服务启动。整个系统初始化过程效率降低且速度变慢。

现代的初始化守护进程试图解决系统启动效率低下和非静态环境的问题。这些 init 守护进程中的两个是 Upstart 和 `systemd`。最近，Ubuntu、RHEL 和 Fedora 发行版已转向较新的 `systemd`，同时保持了对经典 Sysinit、Upstart 或 BSD 守护进程的向后兼容。

Upstart 可于 http://ubuntu.com，Ubuntu、RHEL 和 Fedora 发行版已转向较新的 `systemd`，同时保持了对经典 Sysinit、Upstart 或 BSD 守护进程的向后兼容。

- RHEL 6
- Fedora 9 到14
- openSUSE 11
- Ubuntu 6.4

为了正确管理服务，你需要知道你的系统是什么初始化守护进程。确定这一点可能有点困难。如果你的初始化进程是 `init`，请查看以下内容：

- 你的 Linux 发行版和版本出现在上述 Upstart 列表中吗？如果是，你的初始化守护进程就是 Upstart。
- 尝试使用 Upstart 和 `grep` 命令搜索你的 Linux 发行版的初始化守护进程。下面的示例显示了在 Linux Mint 上搜索 `systemd`。对于 `systemd` 的结果为空。但在第二个示例中，Linux Mint 使用 Upstart。

```
$ sudo /bin/init | -i systemd

$ sudo /bin/init | -i upstart

upstart-dev-lists.ubuntu.com

UPSTART_CONFDIR

UPSTART_NO_SESSIONS
```

在旧版本的 Fedora 上，搜索 Upstart 的结果为空。然而，你可以看到搜索 `systemd` 显示了 `systemd` 的存在。

```
# /bin/init | -i upstart

# /bin/init | -i systemd

systemd.unit=

systemd.log_target=

systemd.log_level=
```

> 提示
> 如果你不知道哪个守护进程管理你的 Linux 系统，可以通过 `binutils` 包进行。在 RHEL 和 Fedora 上，使用命令安装 `binutils`。在 Ubuntu 上，使用命令 `sudo apt-get install binutils`。

如果你的初始化进程是 `init`，运行 `ps -e` 可以立即判断是否是 `systemd`：

```
# ps -e | head
PID TIME CMD
1 ? 00:04:36 systemd
2 ? 00:00:03 kthreadd
3 ? 00:00:15 ksoftirqd/0
```

## 第15章：启动与停止服务

差异仍然存在。例如，旧版本的 BSD init 进程会从 `/etc/ttytab` 文件获取信息。现在，像 SysVinit 进程一样，BSD init 的配置在启动时从 `/etc/inittab` 文件读取。以下是一个 SysVinit 的 `/etc/inittab` 文件：

```
# cat /etc/inittab
# initab 文件描述了 INIT 进程如何设置
# 默认运行级别。运行级别由 RHS 使用：
# 0 halt (不要设置 initdefault)
# 1 Single user mode (单用户模式)
# 2 Multiuser, no NFS (如果没有网络，则与 3相同)
# 3 Full multiuser mode (全多用户模式)
# 4 unused (未使用)
# 5 X1
# 6 reboot (不要将 initdefault 设置为此值)
id:initdefault:
```

# 系统初始化。
sii:sysinit:/etc/rd/rc.sysinit

```
10:0:wait:/etc/rd/rc 0
11:1:wait:/etc/rd/rc 1
12:2:wait:/etc/rd/rc 2
13:3:wait:/etc/rd/rc 3
14:4:wait:/etc/rd/rc 4
15:5:wait:/etc/rd/rc 5
16:6:wait:/etc/rd/rc 6
```

> # 捕获 CTRL-ALT-DELETE
ca:ctrlaltld:/sbin/shutdown -t3 -r now
pf:powerfail:/sbin/shutdown -f -h +2
"断电；系统正在关机"

> # 如果关机启动前电源恢复，则取消。
pr:12345:powerorkit:/sbin/shutdown -c
"电源恢复；关机已取消"

```
# 在标准运行级别运行 getty
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

```
# 在运行级别 5 运行 xdm
```
