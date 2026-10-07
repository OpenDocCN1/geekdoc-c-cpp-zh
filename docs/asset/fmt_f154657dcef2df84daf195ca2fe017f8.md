
图 12.1 展示了与 Linux 文件系统相关的不同分区、卷组和逻辑卷。`sda` 设备被格式化为文件系统并挂载在 `/boot` 目录。`sda2` 设备为 `vg_abc` 卷组提供了空间。然后逻辑卷 `lv-home` 和 `lv-root` 分别挂载在 `/home/` 目录下。

## 图 12.1

LVM 逻辑卷可以像普通分区一样挂载到 Linux 文件系统上。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_337_0.png)

如果任何逻辑卷的空间用尽了，你可以从卷组中分配更多空间。如果卷组空间不足，你可以添加另一个硬盘或网络存储驱动器，并将该驱动器的空间添加到卷组，以便获得更多空间。

# 第 12 章：管理磁盘和文件系统

现在你已经了解 LVM 的工作原理，下一节将向介绍如何从零创建 LVM 逻辑卷。

## 创建 LVM 逻辑卷

LVM 逻辑卷是从上到下创建的，但它们是从下到上构建的。如图 12.1 所示，你首先创建一个或多个物理卷 `pv`，使用物理卷创建卷组 `vg`，然后从卷组创建逻辑卷 `lv`。

用于操作每个 LVM 组件的命令以 `pv`、`vg` 和 `lg` 开头。例如，`pvdisplay` 显示物理卷，`vgdisplay` 显示卷组，`lvdisplay` 显示逻辑卷。

以下步骤将带你完成从零创建 LVM 卷的步骤。要执行此操作，你可以使用本章之前描述的 USB 闪存和分区。使用这些步骤：

- 1. 获取一个带有一些空间的磁盘，并在其上创建一个 LVM 类型 `be` 的磁盘分区。然后使用 `pvcreate` 命令将此分区识别为 LV 物理卷。该操作过程在示例中使用 `/dev/sdx` 设备的“创建多分区磁盘”一节中已描述。

- 2. 使用 `vgcreate` 命令将物理卷添加到新的卷组中。以下命令显示了如何使用 `/dev/sd6` 设备创建一个名为 `myvg0` 的卷组：

```bash
# vgcreate myvg0 /dev/sd6
Volume group "myvg0" successfully created
```

- 3. 要查看新卷组，请输入以下内容：

```bash
# vgdisplay myvg0
--- Volume group             myvg0

VG Size                         396.00 MiB
  PE Size                         4.00 MiB
  Total PE                      99
  Alloc  PE / Size               0 / 0
  Free  PE / Size               99 / 396.00 MiB
```

- 4. 在 400MiB 分区中，396MiB 的空间可以按 4MiB 块使用。这里是从该卷组的某些空间创建一个逻辑卷，然后检查该逻辑卷是否存在：

```bash
# lvcreate -n music -L 100m myvg0
Logical volume "music" created
# ls /dev/mapper/myvg0-music
```

- 5. 该过程创建了一个名为 `/dev/mapper/myvg0-music` 的设备。现在可以使用该设备挂载文件系统，就像你在本章的第一部分对普通分区所做的那样：

```bash
# mkfs -t ext4 /dev/mapper/myvg0-music
# mkdir /mnt/mymusic
# mount /dev/mapper/myvg0-music /mnt/mymusic
# df -h /mnt/mymusic
```

| 文件系统 | 已用大小 | 可用 | 使用率 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/mapper/myvg0-music` | 97M | 5.6M | 87M | 7% | `/mnt/mymusic` |

- 6. 对于普通分区，可以通过向 `/etc/fstab` 文件添加条目来永久挂载逻辑卷，例如：

`/dev/mapper/myvg0-music /mnt/mymusic ext4 defaults 1 2`

下次重启时，逻辑卷将自动挂载到 `/mnt/mymusic`。（如果你想从计算机中移除 USB 驱动器，请确保移除逻辑卷并删除此行）。

## 扩展 LVM 逻辑卷

如果逻辑卷的空间用尽了，你可以在不卸载的情况下为其添加空间。要做到这一点，你必须在卷组中有可用空间，扩展逻辑卷并扩展文件系统以填充它。基于上一节的操作，以下是扩展逻辑卷的方法：

- 1. 注意逻辑卷上当前有多少空间，然后检查逻辑卷卷组中是否有可用空间：

```bash
# vgsdisplay myvg0
...
VG Size 396.0 MiB
PE Size 4.00 MiB
Total PE 99
Alloc  PE / Size 25 / 100.0 MiB
Free  PE / Size 74 / 296.0 MiB
# df -h /mnt/mymusic
Filesystem Size Used Avail Use% Mounted on
/dev/mapper/myvg0-music 97M 5.6M 87M 7% /mnt/mymusic
```

- 2. 使用 `lvextend` 命令扩展逻辑卷：

```bash
# lvextend -L +100M /dev/mapper/myvg0-music
Extending logical volume music
200.0 MiB
```

- 3. 调整文件系统以适应：

```bash
# resize2fs /dev/mapper/myvg0-music
```

- 4. 检查新文件系统的大小：

```bash
# df -h /mnt/mymusic
Filesystem Size Used Avail Use% Mounted on
/dev/mapper/myvg0-music 97M 5.6M 187M 5% /mnt/mymusic
```

### 文件系统类型

- **swap**—用于交换分区。交换区用于内存 `RAM` 用尽时临时存放数据。数据被交换到交换区，并在再次需要时返回内存中。

- **squashfs**—一种压缩的、只读文件系统类型。`Squashfs` 在现场光盘 `live CDs` 上非常流行，因为光盘空间有限且是只读介质（如 CD 或 DVD）。

- **nfs**—网络文件系统 `NFS` 类型的文件系统。`NFS` 用于在 Linux 或 UNIX 计算机上挂载文件系统。

- **hpfs**—用于对 OS/2 HPFS 文件系统进行只读挂载。

- **ncpfs**—与 Novell NetWare 使用的文件系统。NetWare 文件系统可以通过网络挂载。

- **ntfs**—Windows NT 文件系统。根据你所使用的发行版，它可能作为只读文件系统受到支持（这样你可以挂载并从中复制文件）。

- **affs**—用于 Amiga 计算机的文件系统。

- **ufs**—在 Sun Microsystems 操作系统（即 Solaris 和 SunOS）上流行的文件系统。

- **jfs**—由 IBM 开发的 64 位日志文件系统，对于其提供的功能来说相对轻量。
