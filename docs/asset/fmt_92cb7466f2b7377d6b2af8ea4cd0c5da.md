
virtualbox-ose 位于 universe 仓库。启用此社区维护的软件仓库，请前往“系统 -> 软件源”并选择“universe”。安装后，可以转换之前在“开始使用”部分下载的镜像，以便在 VirtualBox 中使用。执行此操作，请运行命令（将 .img 文件名替换为你下载的文件）：

```
$ vboxmanager convertdd ubuntu-9.04-mid-lpia.img ubuntu-9.04-beta-mid-lpia.vdi
```

该命令将 `ubuntu-9.04-mid-lpia.img` 转换为 .vdi 格式，以便在 VirtualBox 中作为“硬盘”使用（后文将详细介绍）。

## 开始使用

从 `http://cdimage.ubuntu.com/releases/jaunty/release/` 下载 Jaunty Ubuntu 版本，并将其保存到硬盘上的文件夹中。

本章演示的所有技术（除 ARM 部分外）都使用 Ubuntu MID 版本，然而它们也经过了测试并与 Ubuntu Remix 版本兼容。如果你的目标是笔记本电脑，请下载此版本。

## 熟悉 Ubuntu 移动环境

本节介绍了 Ubuntu 移动环境。

xVM VirtualBox 是一组虚拟机工具，允许开发者同时运行多个操作系统镜像。要查看其功能，首先安装软件：

```
$ sudo apt-get install virtualbox-ose
```

## 第 2 章：开发环境

现在，通过选择应用程序 ⇨ 附件 ⇨ VirtualBoxOSE 来启动 VirtualBox。你将看到图 2-1 所示的界面。

![](img/001c747b841ab338ed35c50dbdd0c933_48_0.png)

点击“新建”，启动设置向导。点击“下一步”，它将显示“虚拟机名称”和“操作系统类型”对话框。按照图 2-2 所示填写这些数据，然后点击“下一步”。

![](img/001c747b841ab338ed35c50dbdd0c933_48_1.png)

在下一个屏幕上，为你的虚拟机选择允许的最大内存量（当超过了硬件允许的最大内存量时，“下一步”按钮将无法点击）。下一个屏幕如图 2-3 所示，是用于硬盘的。

![](img/001c747b841ab338ed35c50dbdd0c933_49_0.png)

图 2-3

点击“新建”，然后点击“下一步”。选择“动态扩展”选项并点击“下一步”。磁盘镜像默认将保存在 `~/VirtualBox/HardDisks/<name>`，因此在本例中，图 2-4 所示的硬盘将保存为 `mid.vdi`，位于 `/home/ian/.VirtualBox/HardDisks` 目录。

![](img/001c747b841ab338ed35c50dbdd0c933_49_1.png)

图 2-4

选择“下一步”然后点击“完成”，你应该能看到图 2-5。

![](img/001c747b841ab338ed35c50dbdd0c933_50_0.png)

图 2-5

此主硬盘被允许使用 8GB 的空间。选择“下一步”然后点击“完成”，这将创建图 2-6 所示的新 mid 虚拟机。

![](img/001c747b841ab338ed35c50dbdd0c933_50_1.png)

图 2-6

现在需要在此硬盘上安装 Ubuntu MID，以便进行软件的开发和测试。点击图 2-6 中的“设置”按钮，虚拟机的设置界面就会出现，如图 2-7 所示。

![](img/001c747b841ab338ed35c50dbdd0c933_51_0.png)

选择“硬盘”，这会弹出另一个屏幕，如图 2-8 所示。

![](img/001c747b841ab338ed35c50dbdd0c933_51_1.png)

图 2-8

有必要向虚拟机中添加另一个硬盘（包含 Ubuntu MID 操作系统的硬盘）。要执行此操作，选择右侧带有加号的磁盘镜像，然后点击文件夹图标。这将显示图 2-9 所示的屏幕。

![](img/001c747b841ab338ed35c50dbdd0c933_52_0.png)

图 2-9

选择“添加”并浏览包含在本节早之前通过以下命令创建转换镜像的文件夹：

```
$ vboxman convertdd ubuntu-9.04-mid-lpia.img ubuntu-9.04-beta-mid-lpia.vdi
```

选择转换后的镜像，屏幕应该看起来像图 2-10 所示。

![](img/001c747b841ab338ed35c50dbdd0c933_52_1.png)

图 2-10

点击“选择”返回“硬盘”屏幕（见图 2-11）。添加的 `ubuntu-9.04-mid-beta-lpia.vdi` 必须被设置为 IDE 主从设备（IDE Primary Slave）。

![](img/001c747b841ab338ed35c50dbdd0c933_53_0.png)

点击“确定”，你将返回到之前在图 2-6 中看到的 VirtualBox 管理界面。

现在可以通过点击“启动”箭头来启动虚拟机。

你可能会看到显示的错误，类似于图 2-12 所示。

![](img/001c747b841ab338ed35c50dbdd0c933_53_1.png)

图 2-12

## ARM 开发环境

这将在文件夹中创建一个 .img 文件。从 `http://people.ubuntu/~/agra/qemu/kernel/vmlinux-2.6.28-versatile` 下载一个适用于 ARM 的内核，然后运行 `qemu-system-arm -M Versatilepb -kernel`，并将 .img 文件和内核作为参数：

```
qemu-system-arm -M Versatilepb -kernel /vmlinux-2.6.28-versatile -hda qemu-arm-200904291613.img -m 256 -append root=/dev/sda mem=256M ro
```

你需要将 .img 的名称替换为脚本创建的名称；`build-arm-roots` 脚本已经过时，因此运行它将产生类似 `qemu-arm-YYYYMMDDHMMSS.img` 的文件。

这将执行 QEMU 并允许使用创建 .img 步骤中指定的用户名和密码登录。原生架构已创建，如图 2-18 所示。

![](img/001c747b841ab338ed35c50dd0933_58.png)

图 2-18

### 使用 KVM

如果你的硬件支持 KVM，下一步是安装必要的软件包：

- `sudo apt-get install kvm`

接下来，将你的用户添加到 kvm 组。将用户添加意味着你不需要以 root 用户运行 KVM。要执行此操作，请运行：

- `sudo adduser <username> kvm`

在添加新用户后，需要重启虚拟机。接下来，使用以下命令在 KVM 中运行 .img：

- `kvm -localtime -m 512 -boot ubuntu-04-beta.img`

要安装 Ubuntu 镜像，将遵循与 VirtualBox 相似的流程。将 .img 设置为第二个硬盘，这样你就可以将其安装在第一块磁盘上。你可能会考虑类似这样的操作：

```
kvm -localtime -m 512 -hda installed.img -hdb ubuntu-04-beta.img
```

然而，上述命令将不起作用！除了 `installed.img` 不存在之外，QEMU 和 KVM 中使用的操作系统不支持从第二个硬盘启动。作为变通办法，Ubuntu 提供了一个较小的（小于 400KB）ISO 镜像，从中可以选择第二个硬盘。这可以在 `http://people.ubuntu/~/ubuntu-dev/` 获取。

某些问题将在后面详细讨论：使用以下命令启动 KVM：

```
kvm -m 512 -cdrom isolinux.iso -hda installed.img -hdb ubuntu-04-beta.img
```

.img 命令是通过以下命令创建的：

```
qemu-img create installed.img 4G
```

4GB 代表虚拟磁盘空间。由于 `installed.img` 是空的，它将使用上述命令指定的 `-cdrom` 选项启动。选择此选项并安装到第一块磁盘（grub 也会安装在其中）。VirtualBox 安装过程本身；在虚拟机上，顶栏包含一个菜单，允许你更改显示的程序组。点击下拉菜单并选择首选项（Preferences）。点击图标进行安装。

尝试使用最大分辨率，因为 KVM 显示给客体操作系统的分辨率与主机相同。在较低的分辨率下，安装界面上的按钮会被隐藏，你可能需要移除主机上的面板才能看到它们。这在 jaunty 版本中应该会被修复。安装过程完成后重启虚拟机，KVM 将从 `installed.img` 启动。

```
kvm -localtime -m 512 -hda installed.img
```

## 网络

在 VirtualBox 和 KVM 中进行网络都需要以下命令。首先，在客体电脑上，使用之前创建的账户登录，打开终端并安装 openssh-server：

```
sudo apt-get install openssh-server
```

然后添加用户：

```
sudo adduser <username>
```

这设置了网络所需的工具。如果你希望主机和客体之间实现全网络连接，请使用“VirtualBox 和 KVM/QEMU 高级网络”部分。

### VirtualBox 中的网络

在主机上，使用 `VBoxManage` 命令打开一个用于 SSH 的 TCP 端口。然后运行：

```
VBoxManage setextradata "mid" "VBoxInternal/Devices/pcnet/0/Config/ssh/HostPort" 2222
VBoxManage setextradata "mid" "VBoxInternal/Devices/pcnet/0/Config/ssh/GuestPort" 22
VBoxManage setextradata "mid" "VBoxInternal/Devices/pcnet/0/Config/ssh/Protocol" TCP
```

上述三个命令应单独成行。`VBoxManage` 命令允许你从虚拟机获取更多信息，并允许你执行操作和配置调整。虚拟机的名称——上述示例中的 `mid`——是通过运行以下命令获得的：

```
VBoxManage list vms | grep Name
```

使用 VirtualBox 管理控制台完全关闭客体电脑。在主机电脑上输入：

```
ssh -l <username> -p 2222 localhost
```

你已经获得了对客体的 SSH 访问：

```
ssh -l <username> -p 2222 localhost
```

主机端口（在此例中为 2222）必须大于或等于 1024，因为监听低位端口需要 root 权限。

### KVM 中的网络

KVM/QEMU 的默认网络是 `usermode`（用户模式网络）。`usermode` 模式使得虚拟机表现就像在防火墙后面，但它无法访问主机。为了启用主机和客体之间的网络连接，可以像这样启动 KVM：

```
kvm -localtime -m 512 -hda installed.img
```

### VirtualBox 和 KVM/QEMU 高级网络

如果有许多虚拟机运行在主机上，需要设置桥接。首先，在主机上安装 `vde`：

```
sudo apt-get install vde
```

`vde` 是一个连接主机和客体的虚拟交换机。接下来，设置 `tap0` 接口：

```bash
auto tap0
iface tap0 inet static
address 172.120.1
netmask 255.255.255.0
```

`tap0` 是为客体开启的网络接口。现在，在主机上重启网络：

```bash
sudo /etc/init.d/networking restart
```

接下来的操作是：设置 DNS 缓存服务器。为此，编辑 `/etc/dnsmasq.conf` 文件并找到接口（第 85 行）：

```
#interface=
```

将其更改为

```
interface=tap0
```

或者你为该接口选择的任何名称。然后查找第 147 行：

```
#dhcp-range=192.168.0.50,192.168.0.150,12h
```

将其更改为

```
dhcp-range=172.12.120.100,172.12.120.150,12h
```

保存文件并重启 dnsmasq：

```bash
sudo /etc/init.d/dnsmasq restart
```

现在当你运行 `ifconfig` 时，你可以看到新的网络接口：

```
$ ifconfig
tap0
Link encap:Ethernet HWaddr:23:d3:a9:96:88:36
inet 172.12.120.1 Broadcast:172.12.120.255 Mask:255.255.255.0
inet6 fe80::d0d3:a9ff:fe6:8836/64 Scope:Link
UP RUNNING MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:29 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuel:500
RX bytes:0 (0.0 B) TX bytes:5836 (5.8 KB)
```

有必要将你的用户名添加到主机和 `vde2-net` 组中，然后注销并重新登录：

```bash
$ sudo adduser username vde2-net
$ logout
```

### 在 VirtualBox 中使用桥接

在 VirtualBox 管理控制台中，进入虚拟机的设置并选择“网络”（Network）。适配器需要连接到已创建的 `qtap0` 接口。在下拉菜单中，选择“主机界面”（Host Interface），并在底部选项卡中选择 `qtap0`，如图 2-19 所示。

![](img/001c747b841ab338ed35c50dbdd0c933_63_0.png)

现在当虚拟机启动时，它将使用 `qtap0` 接口。可以通过查看 `/var/lib/misc/dnsmasq.leases` 找到 `dnsmasq.leases` 文件，或者在虚拟机上打开终端运行 `ifconfig` 来获取客机的 IP 地址。之后，可以像下面的示例所示 ssh 登录虚拟机：

```bash
$ ssh 172.12.12.115 -l <username>
```

可以通过以下方式从主机拷贝文件到虚拟机：

```bash
$ scp pumd.tar.gz <username>@172.12.12.115:/home/<username>/
```

现在虚拟机已经可以 ping 通主机了。

### 在 KVM 中使用桥接

为了使用此新接口，使用命令 `vdekv` 启动 KVM：

```bash
$ vdekv -localtime -m 512 -net vde,vlan=0 \
-net nic,model=rt18139,vlan=0,macaddr=00:16:3e:12:34:56 -hda installed-mid.img
```

上述命令中的 `macaddr` 可以任意 MAC 地址；这里只是一个示例地址。

当只使用一台虚拟机时，没有必要指定 MAC 地址。但对于多台虚拟机，这变得至关重要。建议从 `00:16:3e:xx:xx:xx` 范围内选择地址，因为该范围已分配给虚拟化。

若要在 qEMU 中该接口，请使用以下命令：
