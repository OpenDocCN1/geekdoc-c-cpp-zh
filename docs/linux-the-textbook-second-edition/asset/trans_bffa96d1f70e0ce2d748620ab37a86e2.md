

并不是 USB 闪存盘格式化为 FAT32，而是当设备插入时，制造商已提供设备驱动程序供自动使用。这并不总是成立。

在许多情况下，了解系统上磁盘驱动器的物理设备名称、实例名称和逻辑设备名称是很重要的，但从实际角度来看，对于 Linux 系统管理员而言，轻松查出磁盘驱动器的逻辑设备名称最为重要。

你可能想向 Linux 系统添加一块之前在另一台计算机操作系统上使用过的硬盘。在这种情况下，我们展示的主要和次要示例可以部署来重新分区并为该硬盘在 Linux 系统上的新使用做好准备。

## 17.4.2 查找磁盘逻辑设备名称的五种快速简便方法

在将新磁盘驱动器连接到 Linux 系统之前，了解如何以非常快速简便的方式确定当前已安装且实际连接并可在系统上使用的磁盘驱动器的逻辑设备名称是很重要的。我们所说的“已连接且可用”是指磁盘驱动器已正确连接并被系统识别，并且系统可以使用设备驱动程序与其通信。

前后对比：如果想查出要添加到系统中的新磁盘的逻辑设备名称，请在添加新磁盘之前使用以下方法之一查看系统上的磁盘，然后在新磁盘添加后使用相同方法并注意差异。出现的不同或新的逻辑名称将是新磁盘的逻辑设备名称。

下面介绍的五种简单方法展示了如何确定系统上已连接且可用的磁盘驱动器，以及这些磁盘和你可能想添加到系统中的其他磁盘的逻辑设备名称。

方法 1：将当前工作目录更改为 /dev。输入 ls。硬盘，例如，在 ls 列表中显示为 sda、sdb 等。这些磁盘上第一个分区或分片的完整路径指定为 /dev/sda1。USB 总线设备，如闪存盘，会在 ls 列表中显示为 /dev/sdc，或在硬盘之后出现的任何字母编号，其上第一个分片的完整路径为 /dev/sdc1。

方法 2：在命令行输入 df -h 以查出系统上文件系统名称及其挂载路径。在我们的 Linux Mint 系统上，当我们执行此操作以查看 Lexar 60 Gb USB 闪存盘是否最近成功连接到系统时，输出如下

```
$ df -h
file system     Size    Used    Avail   Use%    Mounted on
udev            2.8G    0       2.8G    0%      /dev
tmpfs           584M    8.5M    576M    2%      /run
/dev/sda1       105G    90G     9.4G    91%     /
tmpfs           2.9G    1.5M    2.9G    1%      /dev/shm
tmpfs           5.0M    0       5.0M    0%      /run/lock
tmpfs           2.9G    0       2.9G    0%      /sys/fs/cgroup
cgmfs           100K    0       100K    0%      /run/cgmanager/fs
tmpfs           584M    80K     584M    1%      /run/user/1000
/dev/sdb1       60G     1.1G    59G     2%      /media/bob/Lexar
$
```

我们在第 8.1.4 节中更详细地介绍了 df 命令。

方法 3：与使用 df 命令非常相似，使用 lsblk -a 命令。当我们在 Linux Mint 系统上使用此命令和选项时，在我们连接 Lexar 60 Gb USB 闪存盘后，得到以下输出

```
$ lsblk -a
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
loop1   7:1     0       0   loop
sdb     8:16    1   59.6G 0   disk
└─sdb1  8:17    1   59.6G 0   part /media/bob/Lexar
loop6   7:6     0       0   loop
loop4   7:4     0       0   loop
```

```
sr0      11:0     1   1024M    0   rom
loop2     7:2     0            0   loop
loop0     7:0     0            0   loop
sda       8:0     0   111.8G   0   disk
├─sda2    8:2     0   1K       0   part
├─sda5    8:5     0   5.9G     0   part  [SWAP]
└─sda1    8:1     0   105.9G   0   part  /
loop7     7:7     0            0   loop
loop5     7:5     0            0   loop
loop3     7:3     0            0   loop
$
```

方法 4：首次在第 4 章第 4.7 节中展示，使用 **findmnt** 命令。当我们在 Linux Mint 系统上使用它时，得到以下输出

```
$ findmnt
TARGET                              SOURCE       FSTYPE   OPTIONS
/                                   /dev/sda1    ext4     rw,relatime,errors=remount-ro...
├─/sys                              sysfs        sysfs     rw,nosuid,nodev,noexec,relatime...
│ ├─/sys/kernel/security             securityfs   security  rw,nosuid,nodev,noexec,relatime...
│ ├─/sys/fs/cgroup                   tmpfs        tmpfs     rw,mode=755
│ │ ├─/sys/fs/cgroup/systemd         cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/blkio           cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/freezer         cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/devices         cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/pids            cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/hugetlb         cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/memory          cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/net_cls,        cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ │                         net_prio cgroup
│ │ ├─/sys/fs/cgroup/rdma            cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ ├─/sys/fs/cgroup/                cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ │                         perf_event
│ │ ├─/sys/fs/cgroup/cpu,            cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ │ │                         cpuacct
│ │ └─/sys/fs/cgroup/cpuset          cgroup       cgroup    rw,nosuid,nodev,noexec,relatime,...
│ ├─/sys/fs/pstore                   pstore       pstore    rw,nosuid,nodev,noexec,relatime...
│ ├─/sys/fs/fuse/connections         fusectl      fusectl   rw,relatime
│ ├─/sys/kernel/config               configfs     configfs   rw,relatime
│ └─/sys/kernel/debug               debugfs      debugfs    rw,relatime
│   └─/sys/kernel/debug/             tracefs      tracefs    rw,relatime
│                             tracing
├─/proc                             proc         proc      rw,nosuid,nodev,noexec,relatime...
│ └─/proc/sys/fs/binfmt_misc         systemd-1    autofs    rw,relatime,fd=24,pgrp=1,timeout...
│   └─/proc/sys/fs/binfmt_misc       binfmt_misc  binfmt_misc rw,relatime
├─/dev                              udev         devtmpfs   rw,nosuid,relatime,size=2926944k...
│ ├─/dev/pts                        devpts       devpts     rw,nosuid,noexec,relatime,gid=5,...
│ ├─/dev/shm                        tmpfs        tmpfs      rw,nosuid,nodev
│ ├─/dev/hugepages                  hugetlbfs    hugetlbfs  rw,relatime,pagesize=2M...
│ └─/dev/mqueue                     mqueue       mqueue     rw,relatime
├─/run                              tmpfs        tmpfs      rw,nosuid,noexec,relatime,size=5...
│ ├─/run/lock                        tmpfs        tmpfs      rw,nosuid,nodev,noexec,relatime,...
│ ├─/run/cgmanager/fs                cgmanager    tmpfs      rw,relatime,size=100k,mode=755...
│ ├─/run/rpc_pipefs                  sunrpc       rpc_pipe   rw,relatime
│ ├─/run/user/1000                   tmpfs        tmpfs      rw,nosuid,nodev,relatime,size=59...
│ │ └─/run/user/1000/gvfs             gvfsd-fuse    fuse.gvfs  rw,nosuid,nodev,relatime,user_id...
└─/media/bob/Lexar                  /dev/sdb1    vfat      rw,nosuid,nodev,relatime,uid=100...
$
```

请注意，部分文件系统类型（FSTYPE）显示为 ext4、sysfs、tmpfs、cgroup、proc、vfat（用于挂载为 /dev/sdb1 在 /media/bob/Lexar 的 Lexar USB 闪存盘）。

方法 5：你也可以非常高效地使用基于 GUI 的 Gparted 分区编辑器，如示例 17.5 所示。使用 Gparted，其安装方法在附录 A 第 17.4.3 节中针对我们所有代表性的 Linux 系统进行了说明，你可以轻松查出系统上磁盘的逻辑设备名称。此外，使用 Gparted，你可以使用图形编辑方法影响媒体的若干重要特性，例如驱动器的格式和分区。

