

你可以使用以下命令再次删除该地址：

```
$ sudo ip address del 192.168.0.100/24 dev enp2s0
```

这些更改在重启机器后会丢失。

+   2. 要使网卡上的额外 IP 地址永久生效，你可以编辑文件 /etc/network/interfaces，并在保留该文件中找到的默认值的情况下，将之前的 IP 地址添加到网卡中。这就是在添加了之前的分配后 interfaces 文件的样子：

```
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback
# The primary network interface, the default
auto enp2s0
iface enp2s0 inet dhcp
# The address added to the default
iface enp2s0 inet static
    address 192.168.0.100/24
```

上面的文件显示你可以保留网络接口的默认设置，并添加额外的接口。

要将网卡 enp2s0 恢复为默认网络接口设置，只需编辑 /etc/network/interfaces 文件并删除添加 IP 地址的行即可。

+   3. 这一步提出了一个非常有趣的问题。我们希望新的设置在不重启机器的情况下生效。在之前的两个步骤中，我们实际上是通过 ssh 访问系统的。因此，为了使新的设置生效，我们需要执行以下多条命令。这是因为对我们来说，其中的第一部分 sudo ifdown enp2s0 会中断我们的 ssh 会话连接。作为一条多命令（同一命令行上的两条命令），ssh 会话得以保持，我们不会从系统注销。此外，设置会在不重启系统的情况下生效。

要使这些设置在不重启的情况下生效，我们使用以下多条命令中的 ifdown/ifup 命令：

```
$ sudo ifdown enp2s0 && sudo ifup enp2s0
Killed old client process
Internet Systems Consortium DHCP Client 4.3.3
Copyright 2004-2015 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/enp2s0/e4:11:5b:12:c2:77
Sending on   LPF/enp2s0/e4:11:5b:12:c2:77
Sending on   Socket/fallback
DHCPRELEASE on enp2s0 to 192.168.0.1 port 67 (xid=0x7dc0aeea)
RTNETLINK answers: No such process
RTNETLINK answers: Cannot assign requested address
Internet Systems Consortium DHCP Client 4.3.3
Copyright 2004-2015 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/enp2s0/e4:11:5b:12:c2:77
Sending on   LPF/enp2s0/e4:11:5b:12:c2:77
Sending on   Socket/fallback
DHCPDISCOVER on enp2s0 to 255.255.255.255 port 67 interval 3
(xid=0xc6039266)
DHCPDISCOVER on enp2s0 to 255.255.255.255 port 67 interval 8
(xid=0xc6039266)
DHCPREQUEST of 192.168.0.6 on enp2s0 to 255.255.255.255 port 67
(xid=0x6692036c)
DHCPOFFER of 192.168.0.6 from 192.168.0.1
DHCPACK of 192.168.0.6 from 192.168.0.1
bound to 192.168.0.6 -- renewal in 288071 seconds.
$
```

## Exercise 17.38

你如何在本次会话中删除地址 192.168.0.100 分配给 enp2s0？

## Exercise 17.39

你如何确保删除在系统重启之间仍然有效？

结论：我们在 Linux 系统上的一块网卡上分配了多个局域网 IP 地址。

## 17.9 System Security

当谈到计算机时，单词“security”有两个含义。我们只考虑其中一个。

第一个含义表示可靠性。换句话说，磁盘上的文件和数据可以被认为在一段时间内是持久的。这不仅是拥有持久介质的目标，也是备份操作系统本身以及用户文件和数据的目标。例如，如果操作系统崩溃且无法恢复，用户文件和数据会被归档，安全，并且可以完全恢复。

第二个含义表示免受恶意入侵，即由代理（如机器人破解程序）或对象（如程序执行的进程基础）造成的入侵，这些代理或对象没有权限访问系统的特定部分或其任何组件、文件或数据。无论是普通单用户系统还是多用户环境中，都应实施这种第二意义上的系统安全的原因应该是显而易见的。尤其是在当代隐私问题的背景下，互联网上目前普遍存在的广泛黑客攻击和系统渗透。

我们主要处理第二种含义。

从根本上说，根据这种第二种含义，你可以至少在四个地方布置系统安全措施，如本节所示。它们如下：

+   1. **At the Process Level**—Linux 系统的进程模型使该站点最为重要。该模型强制通过身份验证和凭证技术在进程上实施安全。进程是 Linux 中程序执行的基础，并架起内核和用户空间之间的桥梁。这些措施的例子如下：
+      - 设置传统的 UNIX 权限位、特殊权限位 SUID、SGID 和第 5 章中详细说明的粘滞位。权限位的设置，如第 5 章所述，意味着 shell 命令创建的进程是文件所拥有的权限位所针对的对象，或应用于的对象。这适用于 Linux 中创建进程的一切，这意味着用户编写的程序和所有其他应用程序程序和系统程序也是如此。
+      - 部署 ACL 和本章中详细说明的扩展 POSIX1.e ACL。
+      - 使用本章中详细说明的适用于进程的 Linux 特定“功能”。
+      - 使用 Linux 内核命名空间 API 以及其六个主要实现，对进程进行命名空间隔离。我们在本书网站的第 W26 章第 9.9 节中对此进行了简要描述。
+   
+   2. **At the Physical Level**—当有人直接坐在计算机前并尝试登录和使用它时。可以通过使用用户账户的密码保护来实现其中一种方式。在公共 Linux 计算机系统上，这是维护一般访问安全和用户/账户安全最有价值的方式。在此位置还有许多安全技术可以限制对系统硬件的物理访问，例如将机器所在的房间门锁上或制定限制对机器物理访问的协议。

3. At the Network Level—通过对计算机网络连接设置保护来实现。这是通过使用 systemd journalctl 进行监控以及使用各种形式的入侵检测来实现的，也使用我们稍后说明的入侵防御系统（IPS）。

4. At the Persistent Media Level—对物理或虚拟连接到计算机本身的持久介质上。这些技术应用于系统磁盘和其他附加介质，如用户数据磁盘或挂载的网络文件系统（NFS）。例如，使用传统卷上的虚拟化“沙箱”机器，或使用 ZFS 卷，我们在第 17.2.1 节中推荐的用户数据存储模型，以及磁盘数据加密的各种域。

此外，上述站点使用以下特定技术。我们将在以下各节中描述其中的一些重要技术。一些这些技术的进一步阐述在本书网站的第 W26 章第 9.2 和 9.3 节中给出，标题为“Access Control Credentials: Discretionary (DAC), Mandatory (MAC), and Role-Based (RBAC)”和“Using Access Control Lists (ACLs) in Linux”。

+   - Password-based authentication
+   - Access control, either DAC, MAC, or RBAC
+   - The sudo command
+   - Setting POSIX1.e ACLs and extended ACLs for files and directories
+   - Intrusion Detection and Intrusion Prevention
+   - Security Software
+   - ufw System Firewall
+   - Process Credentialing
+   - User namespace process isolation
+   - Whole disk, partition, directory, or file-level data encryption

### 17.9.1 Password-Based Authentication

系统安全的第一道防线，也是几乎普遍应用于许多类型计算机系统的技术，是基于密码的身份验证。Linux 系统在用户登录用户 ID 时比较用户输入的密码，将密码与为该用户保存在密码文件中的先前建立并存储的密码进行比较，并基于比较结果对用户进行身份验证。ID 不仅决定用户是否可以访问系统本身，还决定用户拥有的特权。例如，超级用户特权。此外，ID 在 DAC 中使用，如第 9 章第 2 节所示。密码文件和一个使用 SHA256 哈希算法进行密码加密的哈希/盐方案共同作用以对用户 ID 进行身份验证。系统上的密码文件位于 /etc/passwd 中，保存用户信息并与 /etc/shadow 文件协同工作以对用户 ID 进行身份验证。

## Exercise 17.40

检查你 Linux 系统上 /etc/passwd 文件的内容。参考该文件中你的用户名条目，有多少个冒号分隔的字段，这些冒号分隔字段的含义是什么？

### 17.9.2 Access Control Credentials: DAC, MAC, and RBAC

本节中我们使用的命名法很重要，如果你想了解不同类型的访问控制。 当我们谈论通过安全检查进行访问控制时，这里有重要的术语

