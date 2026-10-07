
# 第六部分：将 Linux 扩展到云端

云实例的内容在本质上往往是通用的。云用户或云提供者预计通过如 `cloud-init` 等服务在镜像上附加更多信息。这些信息分为两个大类：元数据 `meta-data` 和用户数据 `user-data`：

- **meta-data（元数据）**——元数据包含了在镜像启动之前所需的信息。这些数据是镜像内容之外的，通常由云提供者管理。其中一些数据源于存储、内存和处理能力等是从资源池中提取的，而不是来自你正在安装的物理机器。因此，元数据告诉云提供者在启动实例的过程中早期分配多少此类资源。

- **user-data（用户数据）**——用户数据被插入到镜像中存在的操作系统中。这些数据是由使用虚拟机的人员提供的。这可能包括用户账户和密码、配置文件、首次启动时运行的命令、软件仓库清单，或你可能想在操作系统内部运行或更改的任何内容。

你用于运行 Linux 虚拟机的云可能是公有云、私有云或混合云：

- **公有云（Public cloud）**——`Amazon EC2` 和 `Google Compute Engine` 是云平台的示例，它们允许你从基于 Web 的界面启动并使用 Linux 虚拟机。你为实例运行的时间付费。
- **私有云（Private cloud）**——通过私有云，你部署了自己的计算基础设施。
- **混合云（Hybrid cloud）**——许多公司正转向混合云解决方案。混合云允许由一个中央设施管理多个云平台。

## 为云创建 Linux 镜像

回想你在第 9 章安装 Linux 系统时考虑了哪些内容。在手动安装过程中，你设置了 `root` 密码，创建了普通用户账户和密码，可能定义了网络接口以及其他任务。

当你从一个预构建的云镜像作为你的 Linux 系统开始时，你可以使用 `cloud-init` 让 Linux 系统准备好运行。`cloud-init` 工具会设置一个通用的虚拟机实例，并以你想要的方式运行，而无需通过安装过程。

## 配置并运行 cloud-init 云实例

在接下来的步骤中，我将向你展示如何手动创建可以与可启动云镜像结合的数据，这样当该镜像启动时，它将根据你的数据在运行时进行配置，而不是每次都永久地安装在镜像中。

我建议你在第 26 章配置的其中一个虚拟化管理程序上运行此过程。这不仅允许你为 Linux 镜像创建自定义数据，还让你能够该镜像作为虚拟机运行。

## 将 Linux 扩展到云端

为了添加数据并运行现有的云镜像，此过程要求你获取云镜像、创建数据文件并生成一个结合这些元素的新镜像。要配置和运行云镜像，请遵循以下步骤：

### 1. 创建 cloud-init 元数据文件

创建一个名为 `meta-data` 的文件，从外部识别云实例。例如，你可以添加一个名称 `instance-id`、一个主机名 `local-hostname` 和其他信息：

```
instance-id: fedora01

local-hostname: fedora01
```

### 2. 创建 cloud-init 用户数据文件

创建一个名为 `user-data` 的文件，用于保存使用镜像上操作系统的配置。对于这个简单的情况，我仅为默认用户 `fedora` 设置了密码，并告诉 `cloud-init` 不要使其过期：

```
password: cloudpass

expire
```

### 3. 将数据合并到镜像中

建议你手动创建可以与可启动云镜像结合的数据，这样当该镜像启动时，它将根据你的数据在运行时进行配置，而不是每次都永久地安装在镜像中。

## 第六部分：将 Linux 扩展到云

基础的云配置在 `/etc/cloud/cloud.cfg` 文件中完成。你可以在这里看到 `root` 用户账户默认是禁用的。在文件的底部，你可以看到用户名 `fedora` 是默认用户，并且拥有无需密码的 `sudo` 权限。

```
$ sudo cat /etc/cloud/cloud.cfg

users:
  - default
    disable_root: 1
  ...
system_info:
  default_user:
    name: fedora
    lock_passwd: true
    gecos: Fedora Cloud User
    groups: [wheel, amd, systemd-journal]
    sudo: "ALL=(ALL) NOPASSWD:ALL*"
    shell: /bin/bash
distro: fedora
pathbs:
cloud_dir: /var/lib/cloud
templates_dir: /etc/cloud/templates
ssh_svcmname: sshd
```

由于你的存储库已启用，只要你有可用的网络连接，你就可以从 Fedora 存储库中安装任何可用软件包。

## 克隆云实例

如果你喜欢你创建的云实例，稍后可以通过克隆组成云实例的两个镜像来保存它的副本。使用 `virt-manager` 创建云实例的副本请按照以下步骤操作：

1. 启动 `virt-manager`。在运行虚拟机的宿主机系统上，运行 `virt-manager` 命令，或从桌面的“活动”屏幕上启动“虚拟机管理器”。
2. 暂停虚拟机。在 `virt-manager` 窗口中右键点击虚拟机实例条目，并选择“暂停” `Pause`。
3. 克隆虚拟机。再次右键点击虚拟机实例条目，并选择“克隆” `Clone`。
4. 选择设置。对于云基础镜像和数据镜像，你可以选择创建新副本或与现有的虚拟机共享它们。完成后，选择“克隆”。

现在，克隆的云实例已可以从“虚拟机管理器”窗口或 `virsh` 命令随你意愿地启动、停止或其他管理。

## 尝试 Ubuntu 云镜像

任何启用了 `cloud-init` 的 Linux 镜像都可以以与上述 Fedora 所示的方式进行配置。

1. 下载 Ubuntu 云压缩包。访问 Ubuntu 网站，选择你需要的发布版本和镜像。我从以下网站下载了 `ubuntu-14.10-server-cloudimg-amd64.tar.gz` 云镜像：
   `http://cloud-images.ubuntu.com/releases/`
2. 解压压缩包。
   `tar xf ubuntu-14.10-server-cloudimg-amd64.tar.gz`
3. 将数据合并到单独的镜像中。从用于 Fedora 的 `meta-data` 和 `user-data` 文件开始。将 `meta-data` 的名称从 `fedora` 改为 `ubuntu`。用户是 `ubuntu`，但你可以在其中分配密码。运行此命令创建数据镜像：
   `genisoimage -output ubuntu-data.iso -valid coliso -joliet -rock user-meta-data`
4. 为镜像创建快照。
   `qemu create -f qcow2 -o backing file=ubuntu-server-cloudimg-amd64.img ubuntu-server-01.img`
5. 复制镜像文件。
   `cp ubuntu-data.iso ubuntu-server-cloudimg-amd64-floppy ubuntu-server-cloudimg-amd64.img /var/lib/libvirt/images/`
6. 启动云实例。
   `cd /var/lib/libvirt`
   `virt-install --import --name ubuntu14.10-01 --ram 4096 --vcpus`

## 第27 章：将 Linux 部署到云端

```yaml
myownrepo:
  baseurl: http://myrepo.example.com/pub/myrepo/
  enabled: true
  gpgcheck: true
  gpgkey: file:///etc/rpm/RPM/RPM-KEY-GPG-GPG-MYREPO
  name: My personal software repository
packages:
  - nmap
  - locals
  - libymstuff, 3.10.1-fc21.noarch
```

在上面的示例中，在 `/etc/yum.repos.d/myownrepo.repo` 文件中创建了一个新仓库。提供了一个 `gpgkey` 来检查已安装软件包的有效性，并开启了 gpg 检查。

为 Ubuntu 配置 `apt` 仓库略有不同。默认配置了故障备和安全 `apt` 镜像，并在镜像的 `cloud.cfg` 文件中设置了配置。要添加更多仓库，可以在你的 `user-data` 文件中列出如下：

```yaml
apt_mirror: http://archive.ubuntu.com/ubuntu/
apt_mirror:
  - http://myownrepo.example.com
  - http://archive.ubuntu.com
packages:
  - nmap
  - locals
  - libymstuff, 3.16.05
```
