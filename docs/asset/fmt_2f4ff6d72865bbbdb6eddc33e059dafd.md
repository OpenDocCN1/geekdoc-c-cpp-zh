
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

在完成 Samba 服务器的基础配置后，你可以创建自定义节来共享特定的打印机并根据需要对其进行安全保护。对于第一个示例，以下是本章之前 `system-config-samba` 演示中创建的共享（名为 `salesdata`）在 `smb.conf` 中的对应所示：

```
[salesdata]
comment = Sales data for current year
path = /var/salesdata
read only = no
browseable = yes
valid users = chris
```

在创建此之前，创建了 `/var/salesdata` 目录，并将 `chris` 分配为用户和组，同时设置该目录 `chris` 可读可写。（如果 SELinux 处于强制模式，还必须设置 SELinux 上文。）

# 第四部分：成为 Linux 服务器管理员

访问共享时必须提供 Samba 用户名以及关联密码。在 `chris` 连接到共享后，`chris` 具有读写权限（`read only = no`）。

现在你已经了解了 Samba 的默认设置以及简单共享目录（文件夹）的示例，请阅读接几节查看如何配置共享。特别是，示例演示了如何让特定的用户、主机和网络接口可以使用共享。

## 通过网络接口限制 Samba 访问

要限制对共享的访问，你可以在 `smb.conf` 文件中设置全局 `interfaces` 配置。Samba 设计更多用于局域网上的本地文件共享。如果你的计算机有一个连接本地网络和互联网的网络接口，请考虑仅允许访问本地网络。

要设置监听哪些接口，请取消注释 `smb.conf` 文件 `[global]` 节中的 `interfaces` 行。添加允许访问你计算机的接口名称或 IP 地址范围。这是一个示例：

```
interfaces = lo 192.168.22.15/24
```

此条目允许本地系统上的所有用户访问 Samba 服务 (`lo`)。它还允许 192.168.22 网络上的任何系统访问。请参考 `smb.conf` 手页关于识别主机和网络接口的不同方式的描述。

## 通过主机限制 Samba 访问

对 Samba 服务器的主机访问可以针对整个服务或单个共享设置。语法与 TCP wrapper 功能中的 `hosts.allow` 和 `hosts.deny` 类似。然而，这里的 `hosts allow` 和 `deny` 条目是直接添加到 `smb.conf` 文件中的。

以下是 `hosts allow` 和 `hosts deny` 条目的一些示例：

```
hosts allow = 192.168.22.0 EXCEPT 192.168.22.99
hosts allow = 192.168.5.0/255.255.255.0
hosts allow = .example.com market.net
hosts deny = evil.example.org 192.168.99
```

这些条目可以放在 `[global]` 节或任何共享目录节中。第一个示例允许访问 192.168.22 网络中的任何主机，但拒绝了 192.168.22.99。注意数字格式末尾需要一个点。`192.168.5.0/255.255.255.0` 示例使用网络掩码符号将 192.168.5 标识为允许的地址集。

在示例代码的第三行中，允许 `.example.com` 的任何主机，例如单独主机 `market.example.net`。`hosts deny` 示例显示你可以使用相同的格式来识别 IP 和地址以防止来自某些主机的访问。

# 第 19 章：配置 Windows 文件共享 (Samba) 服务器

## 通过用户限制 Samba 用户

通过在 `smb.conf` 文件的共享中识别特定的用户和组，可以允许特定的 Samba 用户和组访问特定的 Samba 共享。除了访客用户之外……（此处文本损坏，我将提供剩余的可读部分）。

# 第 19 章：配置 Windows 文件共享 (Samba) 服务器

图 19.7

在 Nautilus 的“连接到服务器”中打开 Samba 共享。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_562_0.png)

由于 Samba 共享目录可以被视为远程文件系统，你可以使用 Linux 工具将 Samba 共享（临时或永久）连接到你的 Linux 系统。使用标准的 `mount` 命令，你可以将远程 Samba 共享挂载为 Linux 中的 CIFS 文件系统。本示例将来自 IP 地址为 192.168.0.119 的宿主上的 `salesdata` 共享挂载到本地目录 `/mnt/sales`：

```
# mkdir /mnt/sales
# mount -t cifs -user=chris,password=mypass //192.168.0.119/salesdata /mnt/sales
Password: *************
# ls /mnt/sales
hosts services
```

在提示时，用户输入 chris 的密码。鉴于示例中的用户 chris 对共享目录具有读写权限，你的系统应该能够读取和写入挂载的目录。无论人们在共享目录的何处保存文件，服务器上的文件所有者都将是 chris。此挂载将持续到系统重启或你在该目录上运行 `umount` 命令为止。如果你希望将其永久挂载（即每次系统启动时都）到相同位置，你可以进行一些额外配置。首先，打开 `/etc/fstab` 文件并向其添加条目：

```
//192.168.0.119/salesdata /mnt/sales cifs credentials=/root/cif.txt 0 0
```

# 第四部分：成为 Linux 服务器管理员

接下来，创建一个凭据文件（在本示例中为 `/root/cif.txt`）。在该文件中，放入当系统尝试挂载文件系统时你想要提供的用户名和用户密码。以下是该文件内容的示例：

```
user=chris
pass=mypass
```

在重启检查该条目是否正确之前，尝试从命令行挂载它。`mount -a` 命令会尝试挂载 `/etc/fstab` 文件中列出的任何尚未挂载的文件系统。`df` 命令显示挂载目录的磁盘空间信息。例如：

```
# mount -a
# df -h /mnt/sales
Filesystem Size Used Avail Usesec% Mounted on
//192.168.0.119/salesdata 20G 5.7G 14G 30% /mnt/sales
```

你现在可以使用共享的 Samba 目录作为本地系统上的任何目录。

## 在 Windows 中访问 Samba 共享

作为 Linux，你可以从文件管理器窗口（在此情况下为 Windows 资源管理器）访问 Samba 共享。为此打开 Windows 中的任何文件夹，并从左侧面板选择“网络”。屏幕上会出现一个代表 Samba 服务器的图标。点击该图标，并在提示时输入密码。你应该能看到该服务器的所有共享打印机和文件夹（见图 19.8）。

> 图 19.8

从 Windows 访问 Samba 共享。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_563_0.png)

# 第 19 章：配置 Windows 文件共享 (Samba) 服务器

在图 19.8 中，你可以看到有两个共享文件夹（目录）：chris 和 salesdata。还有几个共享打印机。要使用这些文件夹，双击并输入所需的身份验证信息。由于打印机默认设置为使用原始驱动程序，你需要获取 Windows 驱动程序才能使用任何 Samba 打印机。

## 在企业中使用 Samba

尽管这超出了本书的范围，但通过 Samba 服务器进行 Windows 文件和打印机共享是大型企业中非常流行的应用。尽管 Linux 已经在企业级服务器市场取得了巨大进展，但 Microsoft Windows 系统仍然是桌面上使用的最主要系统。

将 Samba 服务器集成到具有许多 Windows 桌面的大型企业中所需的主要功能与认证有关。大多数大型企业使用 Microsoft Active Directory Services (ADS) 进行认证。在 Linux 侧，这意味着在 Linux 系统上配置 Kerberos，并在 `samba.conf` 文件中使用 ADS（而不是 `user`）作为 Samba 的安全类型。

集中认证的优势是用户在整个企业中只需要记住一组凭据，系统管理员需要管理的更少的用户账户和密码。如果你对研究这个主题感兴趣，我建议你阅读 Samba.org wiki 上的 Samba & Active Directory 页面：

```
http://wiki.samba.org/Index.php/Samba__Active_Directory
```

### 总结

由于 Windows 桌面的普及，Samba 服务器已成为 Windows 和 Linux 系统之间共享文件和打印机的热门。Samba 通过实现 Server Message Block (SMB) 或 Common Internet File (CIFS) 协议提供了一种在网络上共享资源与 Windows 系统交互的方法。

本章介绍了在 Linux 系统上安装、启动、安全、配置和访问 Samba 服务器的过程。可以使用图形界面和命令行工具设置 Samba 服务器，并从 Linux 和 Windows 系统访问它。

下一章将介绍网络文件系统 (NFS) 功能。NFS 是 Linux 用于通过网络与其他 Linux 和 UNIX 系统共享和挂载文件系统的原生功能。

## 练习

本节中的练习描述了与在 Linux 中设置 Samba 服务器以及使用 Samba 客户端访问该服务器相关的任务。如往常，完成某些任务通常有多种方法。如果你执行练习的方式与答案所示的不完全相同，不要担心，只要得到相同的结果即可。建议的解决方案见附录 B。

不要在运行 Samba 服务器的 Linux 系统上进行这些练习，因为它们几乎肯定会产生干扰。这些练习是在 Fedora 系统上测试过的。在另一个 Linux 系统上某些步骤可能会略有不同。

- 1. 安装 `samba` 和 `samba-client` 包。
- 2. 启动并启用 `smbd` 和 `nmb` 服务。
- 3. 将 Samba 服务器的工作组设置为 `TESTGROUP`，netbios 名称设置为 `MYTEST`，服务器字符串设置为 Samba Test System。
- 4. 在你的系统中添加一个名为 `phil` 的 Linux 用户，并为 `phil` 设置 Linux 密码和 Samba 密码。
- 5. 设置 `[homes]` 部分，使目录可浏览 (`yes`) 可写 (`yes`)，且 `phil` 是唯一的有效用户。
- 6. 设置必要的 SELinux 布尔值，以便 `phil` 通过 Samba 访问其家目录。
- 7. 从本地系统使用 `smclient` 命令列出可用共享。
- 8. 从本地系统的 Nautilus（文件管理器）窗口连接到 `phil` 的共享。
- 9. 开放防火墙允许访问 Samba 服务 (`smbd` 和 `nmb` 守护进程)。
- 10. 从网络上的另一个系统（Windows 或 Linux）再次尝试打开 homes共享。

# 配置 NFS 文件服务器

## 本章内容

- 获取 NFS 软件
- 启用并启动 NFS
- 导出 NFS 目录
- 设置 NFS 安全功能
- 挂载远程 NFS 目录

不像微软操作系统使用驱动器号（A、B、C 等）表示存储设备，Linux 系统透明地连接多个磁盘、软磁盘、CD-ROM 和其他本地设备以形成单个 Linux 文件系统。网络文件系统 (NFS) 功能允许你将 Linux 文件系统扩展到其他计算机。

NFS 文件服务器为组织内的用户和计算机之间共享大量数据提供了方便的方法。配置了共享文件系统的 Linux 系统管理员需要执行以下任务来设置 NFS：

- 1. **设置网络**。NFS 通常用于私有局域网，而不是互联网等公共网络。
- 2. **启动 NFS 服务**。需要启动多个守护进程以运行完整的 NFS 服务。在 Fedora 中，你可以启动 `nfs-server` 服务；在 Red Hat Enterprise Linux 中，你启动 `nfs` 服务。
- 3. **从服务器选择共享内容**。决定你的 Linux 服务器上的哪些文件系统对其他计算机可用。你可以选择文件系统中的任何点，并将该点以下的所有文件和目录对其他计算机开放。
- 4. **设置服务器安全**。你可以使用多种不同的安全功能来应用你认为合适的安全级别。挂载级安全允许你限制可以挂载资源的计算机，并对于允许挂载的计算机，

# 第四部分：成为 Linux 服务器管理员

允许你指定其是否可以以读/写或只读模式挂载。NFS 的用户级安全通过将来自客户端系统的用户映射到 NFS 服务器上的用户（基于 UID 而非用户名）来实现，这样它们就可以依赖标准的 Linux 读/写/执行权限、文件所有权和组权限来访问和保护文件。

- **在客户端上挂载文件系统。** 任何允许访问服务器共享文件系统的客户端计算机都可以将其挂载到客户端选择的任何位置。例如，你可以将一个名为 `maple` 的客户端计算机上的文件系统挂载到你本地文件系统的 `/mnt/maple` 目录。挂载后，你可以通过输入 `ls /mnt/maple` 来查看该目录的内容。然后你可以使用 `cd` 命令进入 `/mnt/maple` 挂载点，以查看其包含的文件和目录。

图 20.1 展示了一个使用 NFS 分享（导出）文件系统的 Linux 服务器，以及一个挂载该文件系统以供本地用户使用的客户端计算机。

# 图 20.1

NFS 可以让选定的文件系统对其他计算机可用。

```
/etc/exports file:
/apps/bin pins(rw) maple(rw) spruce(rw)
```

```
# mount -t nfs oak:/apps/bin /oak/apps
```

![](img/3886a4c1a684ab63e25e82e0a2d63de9_567_0.png)

在此示例中，一台计算机通过向 `/etc/exports` 文件中添加条目，使其 `/apps/bin` 目录对网络上的客户端（pine、maple 和 spruce）可用。客户端计算机（pine）看到该资源可用，并将其挂载到其本地文件系统的 `/oak/apps` 挂载点上，之后来自 oak 上的 `/apps/bin` 的任何文件、目录或子目录供 pine 上的用户使用（在权限适当的情况下）。

528

www.it-ebooks.info

# 第 20 章：配置 NFS 文件服务器

尽管 Linux 经常被作文件服务器（或其他类型的服务器），但 Linux 是一台通用操作系统，因此任何 Linux 系统都可以作为服务器分享文件系统（导出），或作为客户端使用其他计算机的文件系统（挂载）。

## 注意

文件系统通常是存在于单个设备（如硬盘分区或 CD-ROM）上的文件和目录结构。Linux 文件系统术是指从单台计算机的根目录（/）开始的整个目录结构（可能包括来自多个磁盘分区的文件系统、NFS 或各种网络资源）。共享目录可以代表计算机文件系统的所有部分，它可以（从共享目录向下到整个目录树）挂载到另一台计算机的文件系统上。

## 安装 NFS 服务器

要运行 NFS 服务器，你需要一组内核模块（这些模块随内核本身提供）以及一些用户级工具来配置服务、运行守护进程、以各种方式查询服务。对于 Fedora 和 RHEL，你需要的组件并不已在内核中，可以通过安装 `nfs-utils` 软件包来添加：

```
# yum install nfs-utils
```

除了 `/usr/share/doc/nfs-utils*` 目录下的几份文档外，`nfs-utils` 软件包中的大多数文档包含了其各种组件的 man 手页（帮助文档）。要查看文档列表，请输入以下命令：

```bash
# rpm -qd nfs-utils | less
```

针对 NFS 服务器（用于与他人共享目录）和客户端（用于在本地挂载远程 NFS）都有工具和 man 手页。要配置服务器，你可以参考 `exports` man 手页（设置 `/etc/exports` 文件以共享你的目录）。`exports` 命令的 man 手页描述了如何通过 `/etc/exports` 文件共享并查看你共享的目录列表。你可以使用的 `nfsd` man 手页选项引用 `rpc nfsd` 守护进程，它允许你执行如以调试模式运行服务器等操作。

客户端的 man 手页包括 `mount.nfs` man 手页（查看在本地系统上挂载远程 NFS 目录时可以使用哪些 man 选项）。还有一个 `nfsmount.conf` man 手页，它描述了如何使用 `/etc/nfsmount.conf` 文件配置配置系统在本地挂载远程资源时的行为。`showmount` man 手页描述了如何使用 `showmount` 命令查看来自 NFS 服务器的可用共享目录。

# 第四部分：成为 Linux 服务器管理员

要了解 `nfs-utils` 软件包，你可以运行以下命令分别查看有关该软件包、配置文件和命令的信息：

```
# rpm -qi nfs-utils
# rpm -qc nfs-utils
# rpm -q1 nfs-utils | grep bin
```

## 启动 NFS 服务

NFS 服务器涉及启动多个服务守护进程。不同的 Linux 发行版以不同的方式启动服务。Fedora 和 RHEL 7 中的基本 NFS 服务称为 `nfs-server`。要启动它，请启用它（使其在每次系统启动时启动）并通过运行以下命令检查状态：
