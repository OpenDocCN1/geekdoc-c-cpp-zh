

10. 给出一个命令，完成与以下命令相同的任务。
`rsh upsun29 sort < students > sorted_students`

11. 通过绘制类似于图11.8和图11.9的示意图，说明以下命令的语义。假设本地机器名为 **upsun10**。
`cat students | ssh upsun29 sort | ssh upsun21 uniq > sorted_uniq_students`

12. 显示系统中的 **/etc/services** 文件，并列出以下服务的知名端口号：daytime、time、quote-of-the-day（qotd）、echo、smtp 和 finger。你找到了所有这些端口吗？这些端口号是否与问题8中找到的端口号一致？

13. 使用 **telnet** 命令，通过 **mit.edu** 的 daytime 服务获取当前时间。写下你使用的命令。

14. 使用匿名 ftp 从主机 **nic.merit.edu** 的 **nsfnet/statistics** 目录中获取文件 **history.netcount** 和 **history.hosts**。这些文件包含 NSFNET 基础设施上的国内外网络和主机数量。根据这些文件中的统计，就网络和主机数量而言，Internet 的规模是多少？尽管这些统计数据有些过时，你预测一年后 Internet 的规模会是多少？为什么？展示你的工作过程。

15. 你在网络中某台主机的 **~/.rhosts** 文件中创建了以下条目：
`host1    john.doe`
`host2    mike.brich`
如果 **john.doe** 和 **mike.birch** 是你网络中 **host1** 和 **host2** 主机上的用户，会有什么后果？这两个用户都属于你的用户组。

16. 给出一个命令，显示你网络中所有主机的简单名称。

17. 使用 **telnet** 命令显示 **mit.edu** 上所有名字中包含 **Smith** 的用户信息。展示你用来获取答案的命令。

18. 给出一个命令，逐页显示 **mit.edu** 上名字中包含 **Chen** 的用户信息。这样的用户有多少个？

19. 描述以下命令的语义。清楚说明哪些命令在本地执行，哪些在远程主机上执行。该命令的输出是什么？
`ssh cs00.syi.pcc.edu " ps -el | grep d$ " | grep '\<httpd$' | wc -l`

20. 使用 **traceroute** 命令确定从你的主机到 loc.gov 的路由。数据从你的主机到 locis.loc.gov 的大致传输时间是多少？如果他们的站点阻止了 traceroute，可以跳过此问题，或者使用一个为你执行 traceroute 的网站，如 traceroute.org 或 ping.eu/traceroute。

21. 找到一个提供 quote-of-the-day（qotd）服务的主机。今天的每日名言是什么？

22. 当一个 IP 数据报发送到 **localhost** 时，会产生什么类型的网络流量？

23. 以下域名中哪些没有 IPv6 地址：google.com、twitter.com、amazon.com、instagram.com、ibm.com？展示你的命令及其输出。

24. Google 和 IBM 分别使用多少台机器（主机）来处理其邮件服务？你是如何发现的？展示你用来获取答案的命令以及这些命令的输出。

25. 使用 **ifconfig** 命令，提供你的机器上本地和网络接口的 IPv4 和 IPv6 地址相关信息：localhost 地址和网络 IP 地址及其 MTU。

26. 以下 IPv6 地址对应的主机域名是什么：**2a03:2880:2130:cf05:face:b00c:0:1**？展示你用来获取答案的命令以及这些命令的输出。

27. 当前的 RFC 数量是多少？最后一个 RFC 是关于什么的？它的类别是什么（标准、提议标准等）？你是如何获得答案的？

28. 解释命令 `ssh sarwar@202.147.169.195 'pgrep inetd'` 的语义。清楚说明 `pgrep inetd` 命令在哪里执行，以及命令的输出会到哪里。

29. 描述以下命令的语义。特别要说明命令行中哪些命令在本地机器上执行，哪些在远程机器上执行。

- a. cat students | ssh 122.147.110.13 'sort | grep David'
- b. cat students | ssh 122.147.110.13 'sort' | grep David

# 高级问题和习题

30. 使用附录 A 第 17.2.3.4 节中的说明，在你的 Linux 系统上安装 vsftpd 应用程序。然后，执行第 11.8.4 节中所示的 ftp 命令行会话。

31. 在你的 Linux 系统的 GUI 桌面环境中安装 Filezilla 应用程序。然后，使用 Filezilla 执行第 11.8.4 节中的 ftp 命令行会话。你更喜欢哪种方式，键入命令的会话还是 Filezilla？

32. 在你 Linux 系统上运行的 Virtualbox 虚拟机（VM）实例中安装 openssh-server，然后完成所有必要的操作，以便从你内网 LAN 上的另一台机器或从 Internet 通过 ssh 连接到该 VM 实例。

33. 在你的 Linux 系统上安装 openssh-server，然后完成所有必要的操作，以便从你内网 LAN 上的另一台机器或从 Internet 通过 ssh 连接到你的系统。

# 项目

# 项目 1. 适用于 Debian 9.1、Ubuntu 16.04 或 Linux Mint 18.2 及更高版本

为准备本项目，需要完成书网站上第 W23 章，第 W23.1–W23.2.6 节的内容，特别是示例 W23.1 和 W23.2。然后，在你的 Linux Debian 系列系统上，按照示例 W23.2“在 LXD 容器中启用 ssh 服务器”中的步骤，在 LXD 容器内安装 openssh-server。最后，从 LXD 容器和宿主机之间进行 ssh 连接，并与你内网 LAN 上的另一台机器进行 ssh 连接。

# 项目 2. 适用于 CentOS 7.4 及更高版本

为准备本项目，需要按照书网站上第 W23 章第 2.7 节的说明，在 CentOS 7 上安装 LXC。然后，在你的 CentOS 7 系统上，使用 CentOS LXC 中可用的 Debian 9（Stretch）模板，执行以下操作：

- a. 创建 LXC 容器，启动它，并在容器内以 root 身份使用 adduser 命令添加一个用户，
- b. 从 Debian 容器内部，使用你在 a. 中创建的用户账户，通过 ssh 连接到宿主机 CentOS 7 系统，
- c. 从宿主机 CentOS 7 系统，使用宿主机上的用户账户，通过 ssh 连接到你在 Debian 容器上创建的用户账户。

# 项目 3. 适用于 CentOS 7.4 或更高版本

重复项目 2，但允许你内网 LAN 上的另一台机器上的用户通过 ssh 连接到你在项目 2 中创建的 Debian LXC 容器。

想获取更多内容？请访问我们的网站，获取更多阅读材料、推荐资源和练习。
CRC Press e-Resource： https://www.crcpress.com/9781138710085
作者 GitHub： https://github.com/bobk48/linuxthetextbook

## 12

## Bash 编程入门

## 目标

- 介绍 shell 编程的概念
- 讨论 shell 程序的执行方式
- 描述 shell 变量的概念和使用
- 讨论命令行参数如何传递给 shell 程序
- 解释命令替换的概念
- 描述一些基本编码原则
- 讨论 Bash 脚本的各种控制结构
- 解释 Bash 中各种运算符的语法和语义及其优先级顺序
- 编写并讨论一些 Bash 脚本
- 描述 Bash 命令如何分组并顺序执行
- 涵盖以下命令和原语：

```
*, =, " , ' , ` , & , && , < , > , ^ , ; , | , || , \ , / , [] , : , ; , bash, break, case, continue, exit, export, env, for, if, ls, read, readonly, set, sh, shift, test, uname, while, until, unset
```

## 12.1 引言

Bourne again shell（Bash）不仅仅是一个命令解释器。它拥有自己的编程语言，可用于编写 shell 程序，以执行任何现有命令都无法完成的各种任务。shell 程序通常称为 shell 脚本，由在 shell 中逐条执行的 shell 命令组成，并存储在一个普通的 Linux 文件中。shell 允许使用一个可读写的存储位置，称为 shell 变量，供用户和程序员在完成任务时作为草稿纸使用。shell 还包含程序控制流命令（也称为语句），允许非顺序执行 shell 脚本中的命令，以及重复执行一组命令——类似于 C 等高级编程语言。

## 12.2 运行 Bash 脚本

运行 Bash 脚本有三种方法。对于所有三种方法，第一步都是通过向文件的现有访问权限添加执行权限来使脚本文件可执行。你可以运行 `chmod u+x hello_world` 命令来实现，其中 `hello_world` 是包含 shell 脚本的文件名。如果不使脚本文件可执行，Bash 会显示错误消息，指出 `hello_world` 文件中的脚本无法执行。

```
$ cat hello_world
echo "Hello, world!"
```
