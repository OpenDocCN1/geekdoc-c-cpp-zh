
# 关于使用 `locate` 命令搜索文件，你需要知道的几点：

- 使用 `locate` 查找文件名相比 `find` 命令有优点。`locate` 命令找到文件更快，因为它搜索的是数据库而不是整个文件系统。缺点是 `locate` 命令无法找到自上次数据库创建以来添加到系统的任何文件。文件系统中的每个文件都存储在数据库中。`/etc/updateddb` 配置文件的通过裁剪挂载类型、文件系统类型和挂载点来收集名称。例如，从远程挂载的文件系统（cifs, nfs 等）或本地挂载的 CD 或 DVD（iso9660）收集的文件。包含临时文件（`/tmp`）和池化文件（`/var/sp/cups`）的路径也会被裁剪。你可以根据需要向 `locate` 数据库添加裁剪项（移除你不需要某些项）。在 RHEL 7 中，`updateddb.conf` 文件包含：

```
PRUNE_MOUNTS = "yes"

PRUNEPATHS = "/9fs afn inodefs autofs binfmf_misc cgroup
cifs coda config nfs cpuset devpts devtmp exctfs fuse cups
cfs coda fuse ushslect1 gfs gfs2 hugetlibfs notifyfs iso9660 jjfs2 lustre
meuepc nfs nfs4 nfsed pipe proc ramfs rootfs rpc-pipe
security selinuxfs s sfs soffs sysofs tmpfs udbifs uids usbfs"
```

```
PRUNENAMES = ".git .hg .svn"

PRUNEPATHS = "/afs /media /mnt /net /sfs /tmp /udev/var/cache/ccache /var/lib/yum/yumdb /var/spool/cups /var/squid /var/*"
```

- 作为普通用户，你无法看到 locate 数据库中任何在系统中不可见的文件。例如，如果你使用 `ls` 查找 `/root` 目录中的文件，你就无法定位存储在里面的文件。

- 当你搜索字符串时，该字符串可以出现在文件路径的任何地方。例如，如果你搜索 `password`，你可能会找到 `/etc/passwd`、`usr/bin/passwd`、`/home/chris/passwd/pwfiles.txt` 以及路径中许多许多 `password` 文件。

- 如果你在 `updateddb` 运行后向系统添加了文件，在 `updateddb` 再次运行（可能是当晚）之前无法定位这些文件。要让数据库包含直到目前的所有文件，你可以直接以 root 身份从 shell 运行 `updateddb`。

以下是使用 `locate` 命令搜索文件的几个示例：

```
$ locate .bashrc
etc/skel/.bashrc
/home/cnegus/.bashrc
# locate .bashrc
etc/skel/.bashrc
/home/bill/
/home/joe/.bashrc
/root/.bashrc
```

当作为普通用户运行时，`locate` 仅在 `/etc/skel` 和用户家目录下找到 `.bashrc`。以 root 身份运行相同的命令可以在每个人的家目录下找到 `.bashrc` 文件。

```
$ locate muttrc
usr/share/doc/mut-1.5.20/sample.muttrc

$ locate -i muttrc
etc/Muttrc
etc/Muttrc.local
usr/share/doc/mut-1.5.20/sample.muttrc
```

使用 `-i`，无论大小写如何都能找到文件名。在上一个示例中，通过该选项找到了 `Muttrc.local`。

```
$ locate services
etc/services
usr/share/services
```

## 使用 `find` 搜索文件

`find` 命令是根据各种属性搜索文件的最佳命令。找到文件后，你还可以对它们进行操作（使用 `-exec` 或 `-ok` 选项），运行任何你想要的命令。

当你运行 `find` 时，它实时搜索文件系统，导致它比 `locate` 慢，但提供了最新的视图。然而，你也可以告诉 `find` 从文件系统的特定点开始，这样搜索可以更快。

你可以想到的任何文件属性都可以作为搜索选项。你可以根据文件名、所有者、权限、大小、修改时间等进行搜索。以下是使用 `find` 命令的一些基本示例：

```
$ find
$ find /etc
# find /etc
$ find $HOME -ls
```

单独一行运行时，`find` 命令会查找当前目录下的文件和目录。如果你愿意，只需添加要搜索的目录名称（例如 `/etc`）。如果你作为普通用户运行 `find`，你没有特殊权限查找 root 用户只读的文件。因此 `find` 会产生大量的错误信息。如果你以 root 用户身份运行，`/etc` 会查找 `/etc` 下的所有文件。

`find` 命令的一个特殊选项是 `-ls`。当你将 `-ls` 添加到 `find` 时，每个文件都会打印详细列表（所有者、权限、大小等）。该选项在后面的示例中可以帮助你验证你是否找到了包含特定所有者、大小、修改时间或其他属性的文件。

> 注意
>
> 作为普通用户，如果你正在搜索一个你没有权限访问其中所有文件的文件系统（例如 `/etc` 目录），当你使用 `find` 搜索时可能会收到大量的错误信息。要消除这些信息，将标准错误重定向到 `/dev/null`。`2>/dev/null`。`2>` 将标准错误 `STDERR` 重定向到下一个选项（在本例中为 `/dev/null`，输出将被丢弃）。

### 按名称查找文件

要按名称查找文件，可以使用 `-name` 和 `-iname` 选项。搜索是基于文件的基进行的；默认不搜索目录名称。要搜索

## 第二部分：成为 Linux 高级用户

更加灵活，你可以使用文件匹配字符，例如星号（`*`）和问号（`?`），如下例所示：

```
# find /etc -name passwd
/etc/pam.d/passwd
/etc/passwd
# find /etc -iname '*password*'
/etc/pam.d/passwd
/etc/passwd-
/etc/passwd.OLD
/etc/passwd
/etc/MYPASSWORD
/etc/security/opasswd
```

使用 `-name` 选项且不使用星号，上面的第一个示例列出了 `/etc` 目录中名称恰好为 `passwd` 的文件。通过使用 `-iname` 代替它，你可以匹配任意大小写的组合。通过使用星号，你可以匹配任何包含 `"passwd"` 单词的文件名。

### 按大小查找文件

如果你的磁盘空间快满了，你想找出最大的文件在哪里，你可以按文件大小搜索系统。`-size` 选项允许你搜索与所选大小完全相等、小于或大于该大小的文件，如下例所示：

```
$ find /usr/share/ -size +10M
$ find /mostlybig -size -1M
$ find /bigdata -size +500M -size -5G -exec du {} {} \
4.1G /bigdata/images/rhel6.img
606M /bigdata/Fedora-linux-x86-Live-Desktop.iso
560M /bigdata/dance2.avi
```

上述代码中的第一个示例查找大于 `10MB` 的文件。第二个查找小于 `1MB` 的文件。在第三个示例中，我正在搜索 `500MB` 到 `5GB` 之间的 ISO 镜像和视频文件。这包含了一个 `-exec` 选项的示例（我稍后会描述），用于根据每个文件的大小运行命令。

### 按用户查找文件

在尝试查找文件时，你可以搜索特定的所有 `(-user)` 或组 `(-group)`。通过使用 `-not` 和 `-or`，你可以精炼对特定用户和组关联文件的搜索，如下例所示：

# 第 5 章：处理文本文件

```
$ find /home -user chris -ls
131077 4-rw-r-- 1 chris chris 379 Jun 29 2014 ..bashrc
# find /home -user chris -or -user joe -ls
131077 4-rw-r-- 1 chris chris 379 Jun 29 2014 ..bashrc
181022 4-rw-r-- 1 joe joe 375 Jun 15 2014 ..bashrc
# find /etc -group ntp -ls
3 root ntp 4096 Mar 9 22:16 /etc/ntp
# find /var/spool -not -user -ls
262100 0-rw-r-- 1 rpc mail Jan 27 2014 /var/spool/rpc
278504 0-rw---- 1 joe mail Apr 3 2014 /var/spool/joe
261230 0-rw-r-- 1 bill mail Dec 18 2014 /var/spool/mail/bill
277373 0-rw-xr-x 1 chris chris Mar 15 2014 /var/spool/mail/chris
```

第一个示例输出了 `/home` 目录下所有由用户 `chris` 拥有的文件列表。下一个列出了 `chris` 或 `joe` 的文件。`/etc` 的 `find` 命令列出了所有主组分配为 `ntp` 的文件。最后一个示例显示了 `/var/spool` 下所有不属于 `root` 的文件。你可以在示例输出中看到其他用户拥有的文件。

### 按权限查找文件

按权限搜索是调优系统安全问题或发现访问问题的极佳方法。使用数字或字母（通过 `chmod` 命令）可以同样根据权限来查找文件。（参考第 4 章“移动文件系统”以了解如何配合 `chmod` 使用数字和字母。）

如果你使用数字表示权限，如下所示，请记住这三个数字代表用户、组和其他人的权限。这三个数字从无权限（`0`）到完全读/写/执行权限（`4`、`2`、`1`）。在数字前加减号 `-` 表示从现在起几分钟或天前，加号 `+` 表示更早的分钟或天。如果没有减号或加号，则匹配数字。考虑以下示例：

```
$ find /bin -perm -rwxr-xr-x 1 root
788884 28 -rwxr-xr-x 1 root Mar 10 2014 /bin/echo
```

```
$ find /home/chris/ -perm -222 -type d -ls
144503 4 drwxr-wx chris chris Jun 23 /home/chris
```

通过搜索 `-perm 755`，匹配具有 `rwxr-xr-x` 权限的文件或目录。使用 `-perm -222`，匹配具有用户、组和其他人写权限的文件。注意，在这种情况下，添加 `-type d` 以仅匹配目录。

```
$ find /myreadonly -perm +222 -type f
685035 -rw-rw-- 1 chris 0 Dec 30 2014 /tmp
```

```
$ find -perm -002 -type f
266230 -rw-rw- 1 chris 0 Dec 2014 /tmp
```

使用 `-perm +222`，你可以找到文件系统特定部分（在本例中为 `/myreadonly`）中只读权限的文件。为了查找超过 300 天未被访问的文件，以便查看它们是否需要删除：

```
$ find /etc -mmin -10
```

```
$ find /bin /usr/sbin -ctime -3
```

```
$ find /var/ftp /var/www -atime +300
```

从示例中可以看出，你可以搜索在天或分钟内的内容或元数据更改。`-atime`、`-ctime` 和 `-mtime` 选项允许你搜索文件被访问、更改或元数据更改之后的天数。`min` 选项（`-amin`、`cmin` 和 `-min`）在分钟级别执行相同的操作。作为 `min` 和 `time` 选项参数的数字带有减号（表示从现在起几分钟或天前）或加号（表示更老的分钟或天）。

# 第 5 章：处理文本文件

在查找文件时使用 `'not'` 和 `'or'` 选项可以进一步精炼你的搜索。有时你可能想查找特定用户但不属于特定组的文件。你可能想查找大于某个大小但小于另一个大小的文件。或者你可能想查找属于几个用户中任何一个人的文件。`-not` 和 `-or` 选项可以帮助你。考虑以下示例：

- 有一个名为 `/var/all` 的共享目录。此命令允许你查找由 `joe` 或 `chris` 拥有的文件。

```
$ find /var/all/ -user joe -or -user chris
699797 -rw-r-- 1 chris 0 Dec 31 2014 /var/all/cn
699797 -rw-r-- 1 joe 43790 Dec 31 2014 /var/all/jj
699792 -rw-r-- 1 joe sales 0 Dec 31 2014 /var/all/js
```

- 此命令搜索用户拥有的文件，但仅不属于该组的文件：

```
$ find /var/all/ -user joe -not -group joe -ls
699792 -rw-r-- 1 joe 0 Dec 31 2014 /var/all/js
```

- 你可以在搜索中添加多个要求。在这里，文件必须由用户 `joe` 拥有且大小必须大于 `+1MB`：

```
$ find /var/all/ -user joe -and -size +1M -ls
699797 -rw-r-- 1 joe 43790 Dec 31 2014 /var/all/jj
```

### 查找文件并执行命令

`find` 命令最强大的功能之一是在你找到的任何文件上执行命令的能力。通过 `-exec` 选项，你使用的命令将在每个找到的文件上执行，如果没有问题，则不会停止。`-ok` 选项会向你显示每个匹配的文件并询问你是否想在其上运行命令。

使用 `-ok` 的优势在于，如果你正在进行破坏性操作，可以确保在对其运行命令之前单独检查每个文件。使用 `-exec` 和 `-ok` 的语法为：

```
$ find [options]-exec command {} \;
$ find [options]-ok command {} \;
```

使用 `-exec` 或 `-ok`，你可以带有任何选项运行 `find` 来查找你要找的文件。然后输入 `-exec` 或 `-ok` 选项，后跟要在找到的文件上运行的命令。每个大括号 `{}` 可以在命令行中包含多次，

## 第二部分：成为 Linux 高级用户

如果你需要。在末尾，你需要添加一个反斜杠和分号 `(\;)`。以下是一些示例：

- 此命令在 `/etc` 目录下查找任何名为 `iptables` 的文件，并将该名称包含在 `echo` 命令的输出中：

```bash
$ find /etc -iname iptables -exec echo "found " \;\nfound /etc/bash_completion.d/iptables\nfound /etc/sysconfig/iptables
```

- 此命令在 `/usr/share` 目录下查找所有大小大于 `5MB` 的文件。它使用 `du` 命令列出每个文件的大小。然后将 `find` 的输出按大小从大到小进行排序。输入 `-exec` 后，所有条目都会被处理，无需提示：

```bash
$ find /usr/share -size +5M -exec du {} | | sort -nr\n16932 /usr/share/icons/HighContrast/icon-theme.cache\n69048 /usr/share/icons/gnome/icon-theme.cache\n20564 /usr/share/fonts/cjkuni-ming/uming.ttc
```

- `-ok` 选项允许你一次性对每个文件由你输入的命令进行操作。例如，如果你想在 `/var/users` 目录（及其子目录）中找到所有属于 `joe` 的文件并将它们移动到 `/tmp/joe` 目录：

```bash
$ find /var/users -user joe -ok mv {} /tmp/joe/ \\nmv /var/users/dict.data ? ? y\nmv /var/users/file ? ? y
```

注意代码中，在每个文件被移动到 `/tmp/joe` 目录之前，系统会对其进行提示。你只需在每行输入 `y` 并按回车键来移动文件，或者按回车键跳过它。

有关 `find` 命令的信息，请输入 `man find`。

## 使用 `grep` 搜索文件

如果你想搜索包含特定搜索词的文件，可以使用 `grep` 命令。通过 `grep`，你可以搜索单个文件或递归搜索整个目录结构。

在搜索时，包含该文本的每一行都会打印在屏幕上（标准输出），或者仅列出包含搜索词的文件列表。默认情况下，`grep` 是区分大小敏感的，尽管你也可以进行不区分大小的搜索。

除了搜索文件，你还可以使用 `grep` 搜索标准输出。因此，如果一个命令输出了文本，而你只想找到包含文本的行，可以使用 `grep` 过滤出你想要的内容。

以下是一些 `grep` 命令的示例，用于在一个或多个文件中查找文本字符串：

## 第 5 章：处理文本文件

```bash
$ grep desktop /etc/services
dktop-dna 2763/tcp # Desktop DNA
dktop-dna 2763/udp # Desktop DNA
```

```bash
$ grep -i /etc/services
sco-dtmgr 617/tcp # Desktop Administration Server
sco-dtmgr 617/udp # Desktop Administration Server
airsync 2175/tcp # Microsoft Desktop AirSync Protocol
```

在第一个示例中，在 `/etc/services` 文件中搜索 `"desktop"` 词发现了两行。再次搜索时，使用 `-i` 进行不区分大小搜索（如第二个示例所示），产生了 29 行文本。
