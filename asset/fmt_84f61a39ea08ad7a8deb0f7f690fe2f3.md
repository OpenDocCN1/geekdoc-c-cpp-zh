
- **xfs**—最初由 Silicon Graphics 开发的高性能文件系统，能够有效处理大文件。该文件系统是 RHEL 7 的默认类型。

- **gfs2**—一种共享磁盘文件系统，允许多台机器使用同一个共享磁盘，而无需通过 CIFS、NFS 等网络层。

要查看当前正在使用的内核的文件系统列表，输入 `ls /lib/modules/kernelversion/fs/`。实际模块存储在该目录的子目录下。挂载支持类型的文件系统会导致该文件系统被加载（如果它尚未加载）。

输入 `man fs` 查看 Linux 文件系统的描述。

## 启用交换区

交换区是磁盘上当系统内存（RAM）耗尽时供 Linux 使用的区域。如果你的内存满了，且你尝试启动另一个应用程序但没有交换区，该应用程序将失败。

有了交换区，Linux 可以临时将数据从内存交换到交换区，并在需要时将其取回。这会产生性能影响，但总比让进程失败要好。

要从分区或文件创建交换区，请使用 `mkswap` 命令。例如，这里是如何使用可用的交换空间、创建交换文件、启用交换文件，然后检查系统上是否有可用空间的方法：

```
# free -m
       total used free shared buffers cached
Mem:         1955 663 1291 0 42 283
-/ buffers/cache     337 1617
Swap:            819 0 819
# dd if=/dev/zero of=/var/tmp/myswap bs=1M count=1024
# mkswap /var/opt/myswap
# swapon /var/opt/myswap
```

`free` 命令显示了在使用 `swapon` 命令创建、制作和启用交换区前后的交换空间。要让交换区立即且永久地对你的系统生效，你需要将其添加到 `/etc/fstab` 文件中。以下是一个示例：

```
/var/opt/myswap swap defaults 0 0
```

这表示名为 `/var/opt/myswap` 的交换文件应在启动时启用。由于交换区没有挂载点，因此第二个字段被设置为 swap，分区类型也是如此。为了让该交换文件在重启后仍然可用，你可以立即启用它（`swapon -a`）并检查额外的交换区是否已出现：

```
# swapon -a
```

## 禁用交换区

如果你在任何时候想要禁用交换区，可以使用 `swapoff` 命令。你可能会这样做，特别是当交换区不再需要，且你想要回收被交换文件占用的空间，或者移除提供交换分区的 USB 驱动器时。

首先，确保没有空间被交换设备占用（使用 `free` 命令），然后使用 `swapoff` 关闭交换区，以便重用该空间。以下是一个示例：

```
# free -m
       total used free shared buffers cached
Mem:         1955 1720 235 0 42 1310
-/ buffers/cache: 367 1588
Swap:            1843 0 1843
# swapoff /var/opt/myswap
```

```
# free -m
Mem: 1955 1720 235 0 42 1310
-/+ buffers/cache: 367 1588
Swap: 819 0 819
```

## 使用 fstab 文件定义可挂载的文件系统

你本地计算机上的硬盘以及你每天使用的远程系统可能都设置为在启动 Linux 时自动挂载。`/etc/fstab` 文件包含了每个分区的定义，其中带有选项描述了如何挂载该分区。以下是 `/etc/fstab` 的一个示例：

```
/dev/mapper/vg_abc-lv_root / ext4 defaults 1 1
UUID=78bdaea46-9389-43bd-bfee-06d934fae28 /boot ext4 defaults 1 2
/dev/mapper/vg_abc-lv_home /home nfs users,_netdev 0 0
/dev/mapper/vg_abc-lv_swap swap swap defaults 0 0
# 后续添加的挂载项
/dev/sdb1 vfat ro 1 2
192.168.0.27/nfsstuff /remote nfs users,_netdev 0 0
192.168.0.28/myshare /share cifs guest,_netdev 0 0
# Linux 文件系统
tmpfs /dev/tmpfs defaults 0 0
devpts /dev/pts devpts gid=5,mode=620 0 0
sysfs /sys defaults 0 0
proc /proc defaults 0 0
```

所示 `/etc/fstab` 文件来自一个 Red Hat Enterprise Linux 6 器的安装，并添加了几行。

目前，你可以忽略 tmpfs、devpts、sysfs 和 proc 条目。这些是分别与共享内存、终端窗口、设备信息和内核参数关联的特殊设备。

通常，`/etc/fstab` 的第一列显示设备或共享项（挂载了什么），第二列显示挂载点（挂载在何处）。之后是文件系统类型、任何选项（默认），以及用于告诉 dump 和 fsck 等命令如何处理该文件系统的两个数字。

前三个条目代表分配给文件系统根目录 `/`、`/boot` 目录和 `/home` 目录的分区。三个都是 ext4 文件系统。第四个是交换设备（用于在内存溢出时存储数据）。注意 `/`、`/home` 和 swap 的设备名称都以 `/dev/mapper` 开始。这是因为 LVM 逻辑卷是从一个名为 LVM 组的空间池分配的（关于 LVM 的更多信息，请参见本章后后的“使用逻辑卷分区”部分）。

`/fstab` 条目第一列中的任何设备名称都可以被 UUID 标识符所替换。然而，它不是使用 `/dev/sda`，而是使用一个唯一标识符（UUID）来标识设备。要查看系统上所有设备的 UUID，请输入 `blkid` 命令，如下：

```
### blkid
/dev/sda:
UUID="78bdaea46-9389-43bd-bfee-06d934fae28" TYPE="ext4"
/dev/mapper/vg_abc-lv_root:
UUID="36eff49a-86ec-45e1-9049-38431284699" TYPE="LVM2"
/dev/mapper/vg_abc-lv_swap:
UUID="7762950-2cc2-4bd9-a860-34669535369" TYPE="swap"
/dev/mapper/vg_abc-lv_home:
UUID="7ffcc33-36b9-4ccb-8b71-091efb17970" TYPE="ext4"
/dev/sdb1:
SEC_TYPE="msdos" UUID="75E0-96AA" TYPE="vfat"
```

所示etc/fstab 文件来自一个 Red Hat Enterprise Linux 6 服务器的安装，并添加了几行。

我在 `/etc/fstab` 中添加了三个条目以说明某些实体。我连接了一个来自旧 Microsoft Windows 系统的硬盘，并将其挂载到 `/win` 目录。我添加了 ro 选项使其变为只读。

接下来的两个代表远程文件系统。从 `/remote` 目录，`/nfsstuff` 目录从主机地址 `192.168.0.27` 以读写（rw）方式挂载 NFS 共享。从 `/share` 目录，名为 myshare 的 Windows 共享从主机 `192.168.0.28` 挂载。在这两种情况下，我们都添加了 `_netdev` 选项，它告诉 Linux 在尝试挂载共享之前等待网络启动。（有关挂载 CIFS 和 NFS 共享的更多信息，请分别参考第 19 章“配置 Windows 文件共享（Samba）服务器”和第 20 章“配置 NFS 文件服务器”。）

## 来自自

“使用 fstab 定义可挂载文件系统”节展示了如何挂载在 Windows 中使用的旧 FAT 文件系统的硬盘分区。大多数 Windows 系统现在使用 NTFS 文件系统。然而，对该系统的支持并不是每个 Linux 系统都提供：NTFS 可以从 Fedora 的 nfs-3g 包获取。

## 第 12 章：管理磁盘和文件系统

为了帮助你理解 `/etc/fstab` 文件的内容，这里是文件中每个字段的含义：

- **字段 1**—代表文件系统的设备名称。此字段可以包含 LABEL 或 UUID 选项，通过它们你可以指定卷标签或通用唯一标识符（UUID）来代替设备名称。这种方法的优点是可以通过卷名来识别分区，你可以将卷卷移动到不同的设备名称，而无需更改 fstab 文件。（有关创建和使用标签的信息，请参阅“创建文件系统的 mkfs 命令”节中对 `mkfs` 命令的描述）。

- **字段 2**—文件系统中的挂载点。文件系统包含了从挂载点一直到目录树底的所有数据，除非在其下方的某处挂载了另一个文件系统。

- **字段 3**—文件系统类型。有效的文件系统类型在本章前面的“支持的文件系统”节中描述（尽管你只能使用内核中包含其驱动程序的类型）。

- **字段 4**—挂载该条目时使用的默认选项或逗号分隔的选项列表（中间无空格）。有关其他选项的信息，请参阅 mount 手册页（-o 选项下）。

> 通常，只允许 root 用户使用 mount 命令挂载文件系统。然而，为了允许任何用户挂载文件系统（如 CD 文件系统），你可以在 `/etc/fstab` 的字段 4 中添加 user 选项。

- **字段 5**—此字段中的数字表示文件系统是否需要 dump（即是否有备份）。1 表示文件系统需要 dump，0 表示不需要。（这已不再特别有用，因为 Linux 员员使用比 dump 命令更复杂的备份选项。通常使用 0）。

- **字段 6**—此字段中的数字表示在需要检查时是否应该用 fsck 检查：1 表示需要首先检查，2 表示在所有由 1 指定的分区已检查完成后进行检查，0 表示不检查。

如果你想了解有关挂载选项以及 `/etc/fstab` 文件的其他功能，可以参考几个 man 手册页，例如 `man nfs` 和 `man 8` 的输出。

## 使用 mount 命令挂载文件系统

Linux 系统在每次启动时会自动运行 `mount -a`（挂载 `/etc/fstab` 文件中的所有文件系统）。由于这个原因，你通常只在特殊情况下使用 mount 命令。特别是，普通用户或管理员通常以两种方式使用：

- 显示当前挂载的磁盘、分区和远程文件系统

- 临时挂载文件系统

任何用户都可以执行挂载（不带选项）来查看当前本地 Linux 系统上挂载了哪些文件系统。以下是 `mount` 命令的一个示例。它显示了一个包含根（/)文件系统的单硬盘分区 `/dev/sda`，以及分别挂载在 `/proc` 和 `/dev` 上的 proc 和 procdev 文件系统。

```
$ mount
/dev/sda3 on / type ext4 (rw)
/dev/sda2 on /boot type ext4 (rw)
/dev/sda1 on /mnt type vfat (rw)
/dev/proc on /proc type proc (rw)
/dev/sys on /sys type sysfs (rw)
/dev/devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/shm on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
none on /cdrom on /media/MyOwnedDVD type iso8660 (ro,nosuid,nodev)
```

传统上，挂载最多的设备来自可移动介质，如 CD 或 DVD。然而，取决于你使用的桌面类型，在插入 CD 和 DVD 时，它们会自动挂载。（在某些情况下，插入介质后应用程序会自动启动。例如，当你插入的媒体包含音乐或数字图像时，CD 播放器或照片编辑器将启动。）

然而，有时你可能会发现手动挂载文件系统很有用。例如，你想查看一个旧硬盘的内容，因此将其安装为计算机的第二块磁盘。如果磁盘上的分区没有自动挂载，你可以挂载你那个旧的 ext3 唯一的磁盘分区 sdb1：

```
$ mkdir /mnt/tmp
$ mount -t ext3 -o rw /dev/sdb1 /mnt/tmp
```

使用 `mount` 命令的另一个原因是挂载分区以更改其挂载选项。假设你想将 `/dev/sdb1` 挂载为读/写模式，但你不想卸载它（可能有人正在使用它）。你可以如下所示使用 remount 选项：

```
$ mount -t ext3 -o remount,rw /dev/sdb1
```

## 在回环设备中挂载磁盘镜像

使用 `mount` 命令的另一个有效方法是处理磁盘镜像。如果你从网上下载了 CD 或软盘镜像并想查看其内容，可以在不将其刻录到 CD 或软盘的情况下实现。当镜像位于硬盘时，创建一个挂载点并使用 `-o loop` 选项将其本地挂载。这是一个示例：

```
# mkdir /mnt/mycdimage
# mount -o loop whatever-i86-disk.iso /mnt/mycdimage
```

在此示例中，创建了 `/mnt/mycdimage` 目录，并将当前目录下的磁盘文件 (`whatever-i86-disk.iso`) 挂载到那里。你现在可以进入该目录查看其内容并复制任何内容。这对于想要从无需刻录到 CD 的下载镜像进行安装非常有用。你还可以通过 NFS 共享挂载点，以便从另一台计算机安装软件。完成后，只需输入 `umount /mnt/mycdimage` 即可卸载它。

其他选项仅适用于特定的文件系统。请参阅 mount 手册页以获取这些和其他有用选项。

## 使用 unmount 命令

当你完成临时文件系统的使用，或想临时挂载永久文件系统时，请使用 `unmount` 命令。这会将文件系统从你的 Linux 文件系统中的挂载点卸载。使用 `unmount` 时，你可以提供目录名或设备名称。例如：

```
umount /mnt/tmp
```

通常情况下，使用设备名称更好。如果遇到设备忙，卸载将失败，因为有文件已打开或有进程正在使用该文件系统。另一种方案是使用懒惰卸载（lazy unmount），它会将文件系统从目录树中分离，但在文件系统不再忙时清理对该文件系统的所有引用：

```
umount -l /mnt/tmp
```

```
257024 inodes, 1027300 blocks
51365 blocks (5.0%) reserved for the super user
First data block=0
Maximum filesystem blocks=1052770304
32 block groups
32768 blocks per group, 32768 fragments per group
8032 inodes per group
Superblock stored on blocks:
32768, 98304, 163840, 229376, 249412, 819200, 884736
Allocating group tables:
Writing inode tables:
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done
```

你可以看到 `mkfs` 命令输出的格式化统计信息。输出中包含了已创建的 inode 和块的数量，以及每组的块和碎片数量。inode 存储每个文件的所有权和时间戳等元数据，文件系统中的每个文件和目录都会消耗一个 inode。这里的 inode 数量限制了你在该文件系统中可以创建的文件总数。

现在，挂载此文件系统 `[mkdir /mnt/myusb ; mount /dev/sdcl /mnt/myusb]`，切换到 `/mnt/myusb` 作为当前目录 (`cd /mnt/myusb`)，并根据意愿在上面创建文件。

## 总结

文件系统是管理 Linux 系统的关键部分。使用 `fdisk` 等命令，你可以查看并更改磁盘分区。可以使用 `mkfs` 命令向分区添加文件系统。创建完成后，可以使用 `mount` 和 `umount` 命令分别对文件系统进行挂载和卸载。

逻辑卷（LVM）提供了一种更强大、更灵活的磁盘分区管理方式。通过 LVM，你可以创建称为卷的存储池，允许你扩展和缩小逻辑卷，并通过添加更多物理卷来扩展卷组的大小。

本书到此处已涵盖了成为系统管理员所需的大部分基础，第 13 章引入了扩展这些技能以管理网络服务器的概念。本章主题包括如何安装、管理和保护服务器的信息。

# 练习

使用这些练习题来测试你对创建磁盘分区、逻辑卷管理以及处理文件系统的知识。你需要一个至少 1GB 的 USB 闪盘用于这些练习。

# 第三部分：成为 Linux 系统管理员

这些任务假设你正在运行 Fedora 或 Red Hat Enterprise Linux 系统（尽管某些任务也适用于其他 Linux 系统）。如果你遇到困难，可以在附录 B 中查看任务解决方案（在 Linux 中，完成任务通常有多种方法）。

- 1. 运行命令监控 `/var/log/messages` 文件并插入你的 USB 闪盘。确定 USB 闪盘的设备名称。

- 2. 运行命令列出 USB 闪盘的分区表。

- 3. 删除 USB 闪盘上的所有分区，保存更改，并确保更改已应用于磁盘分区表和 Linux 内核。

- 4. 为 USB 闪盘添加三个分区：100MB Linux 分区、200MB交换分区和500MB LVM 分区。保存更改。

- 5. 在 Linux 分区上建立 ext3 文件系统。

- 6. 创建名为 `/mnt/myapp` 的挂载点，并将 Linux 分区挂载其上。

- 7. 启用交换分区并开启它，使额外的交换空间立即可用。
