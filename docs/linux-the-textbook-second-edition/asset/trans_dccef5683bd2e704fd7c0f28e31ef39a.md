

你可以使用 findmnt 命令显示所有已挂载文件系统的信息，包括其类型如 ext4。使用 -t 选项的该命令可用于显示特定类型的文件系统。例如，你可以使用 findmnt -t ext4 命令显示系统上已挂载的所有 ext4 文件系统的列表。

表 4.4 显示了 Linux 文件系统 XFS、Ext4 和 ZFS 的汇总比较。浏览“Web 资源”中列出的相关网站（表 4.5，见本书 GitHub 站点）以了解更多关于 Ext4、XFS 和 ZFS 的信息。

## Exercise 4.8

使用 findmnt 命令显示系统上已挂载的所有文件系统的信息。你的系统上挂载了多少个文件系统？

## Exercise 4.9

使用 findmnt 命令显示系统上已挂载的所有 ext4 文件系统的信息。这些文件系统中有多少个挂载在你的系统上？

### 4.7.1 Displaying Disk Usage of Files and Directories

你可以使用 du 命令显示文件和目录的磁盘使用情况。这对于有日志文件失控、达到配额的新 Linux 用户来说是一个有用的命令。下面是对该命令的简要描述。

```
Syntax:
  du [option]... file-list...
Purpose: Display a summary of the disk usage of files in file-list, recursively for directories
Commonly used options/features:
  -a    Display disk usage for all files, not only directories
  -h    Display in humanly readable format, e.g., 1.7 K, 31.9 M, and 3 G
  -s    Display only total disk usage each file in file-list
```

在下面的会话中，我们使用 du 命令不带任何选项，以及带 -s 和 -h 选项，来显示各种文件和目录的磁盘使用情况，以 1 K 块大小和 K、M、G 字节为单位。

```
$ du ~
4               /home/sarwar/.linuxmint/mintMenu/applications
34724           /home/sarwar/.linuxmint/mintMenu
...
27450108        /home/sarwar
$ du -h ~
4.0K    /home/sarwar/.linuxmint/mintMenu/applications
34M     /home/sarwar/.linuxmint/mintMenu
```

## TABLE 4.4

A Summary Comparison of Linux File Systems

| Feature | Ext4 | ZFS | XFS |
|---|---|---|---|
| Introduced to Linux or Open Source | 2006 | 2005 | 2001 |
| Maximum file size | 16 tebibytes (TiBᵃ) | 16 exbibytes (EiBᵇ) | 8 EiB |
| Maximum volume size | 1 EiB | 2¹²⁸ bytes = 256 trillion yobibytes (YiBᶜ) | 8 EiB |
| Maximum number of files | 4 billion | Unlimited (2⁴⁸ per directory) | 16 EiB |
| Maximum filename length | 255 bytes | 255 bytes | 255 bytes |

a. TiB = 2⁴⁰ = 1024⁴.
b. EiB = 2⁶⁰ = 1024⁶.
c. YiB = 2⁸⁰ = 1024⁸.

```
27G      /home/sarwar
$ du -s linux2e/ch14
27401844      linux2e/newch14
$ du -s -h linux2e/ch14
27G      linux2e/newch14
$ du -s -h /usr/bin
163M     /usr/bin
$
```

## Exercise 4.10

使用 du 命令以 1 K 块和 K、M、G 字节为单位显示你的系统上主目录、/lib 和 /dev 目录的磁盘使用情况？

### 4.8 End-of-File Marker

每个 Linux 文件都有一个文件结束符（eof）标记。读取其输入来自文件的命令在到达文件末尾时会读取 eof 标记。当输入文件连接到键盘时，新行上的 <Ctrl-D> 是 Linux eof 标记。这就是为什么像 cat 这样的命令在读取来自键盘的输入时（见第 6 章），当你在新行上按下 <Ctrl-D> 时会终止。

## Summary

在 Linux 中，文件是一系列字节。这种简单而强大的概念及其实现导致系统中几乎所有东西都是文件；用户和进程不是。Linux 支持七种文件类型：普通文件、目录、符号链接、字符特殊文件、块特殊文件、命名管道（也称为 FIFO）和套接字。任何类型的文件都不支持文件扩展名，但运行在 Linux 系统上的应用程序可以要求自己的扩展名。

Linux 中的每个文件都与其关联若干属性，包括文件名、所有者名称、上次修改日期、链接计数和文件在磁盘上的位置。这些属性存储在磁盘上的一个区域，称为 inode。当文件被打开时，其 inode 会被复制到内核的一个区域，称为 inode 表，以便更快地访问其属性。目录中的每个文件都有一个与其关联的条目，该条目包含文件名称及其 inode 号码。内核通过从其目录条目中读取文件的 inode 号码并用该 inode 号码索引 inode 表来访问打开文件的属性，包括其内容。

Linux 文件结构是分层的，有一个根目录，系统中的所有文件和目录都在其下。每个用户都有一个目录，称为用户的主目录，在登录系统时他或她会被放置到该目录下。多个磁盘驱动器和/或磁盘分区可以挂载在同一个文件系统结构上，从而允许将其作为目录访问，而不是像 MS-DOS 和 Microsoft Windows 中那样作为命名驱动器 A:、B:、C: 等。这种方法提供了对系统中所有文件和目录的统一视图，用户不必担心记住驱动器名称以及它们包含的文件（和目录）。

目录（主要）在用户的主目录下可以创建和删除。可以使用各种命令（mkdir、rmdir、cd、ls 等）导航文件结构。你可以使用文件的绝对或相对路径名指定系统中的文件。绝对路径名以根目录开头，相对路径名以用户的主目录或当前工作目录开头。

以下命令可用于显示文件内容、了解文件内容的类型、创建目录、删除目录、显示目录内容、创建空文件、创建任意大小的随机数据文件等：cat、cd、du、echo、fallocate、file、findmnt、getconf、ls、mkdir、more、pwd、rmdir 和 touch。

你可以通过多种方法在 Linux 系统上创建文件，包括使用 nano 或 vim 等文本编辑器、使用编译器生成程序的可执行映像、使用 touch 命令创建空文件，以及使用 fallocate 命令创建任意大小的未初始化文件。

Linux 会为每个命令自动打开三个文件，以便其从中读取输入并向其发送输出和错误消息。这些文件称为标准输入（stdin）、标准输出（stdout）和标准错误（stderr）。默认情况下，这些文件附加到命令执行的终端上；即命令输入来自终端键盘，命令输出和错误消息发送到终端的屏幕显示。默认文件可以使用重定向原语更改为其他文件：< 用于输入重定向，> 用于输出和错误重定向。

内核为每个打开的文件关联一个小整数。该整数称为文件描述符。内核使用文件描述符对文件执行操作（例如，读）。stdin、stdout 和 stderr 的文件描述符分别为 0、1 和 2。

文件系统通常被认为是一个高度组织化且快速访问的数据集合，以在任何现代介质上持久存储该数据。扩展文件系统、XFS 和 ZFS 是最当代和最重要的 Linux 文件系统。支持非常大的文件大小、允许极大量的目录并保持数据一致性是这些系统的标志性功能。

du 命令可用于以 1 K 块和 K、M、G 字节为单位显示文件和目录的磁盘使用情况。

每个 Linux 文件都有一个 eof 标记。如果命令从键盘读取输入，则 eof 标记为 <Ctrl-D>。

## Questions and Problems

- 1. 什么是 Linux 中的文件？字符特殊和块特殊在 Linux 中代表什么？你的系统上有多少个字符特殊和块特殊文件？你是如何获得你的答案的？展示你的工作。
- 2. Linux 是否支持任何文件类型？如果是，列出它们。Linux 是否支持文件扩展名？
- 3. 什么是目录条目？它由什么组成？
- 4. 什么是 Linux 中的特殊文件？什么是字符特殊文件和块特殊文件？运行 ls /dev | wc -w 命令来查找你的系统有多少个特殊文件。
- 5. 什么是进程间通信？列出 Linux 提供的三种用于进程间通信的工具。
- 6. 绘制与图 4.2 所示类似的层次文件结构，针对你的 Linux 机器。显示前两个级别的文件和目录。也显示你的主目录的位置，以及主目录下的文件和目录。
- 7. 给出三个可用于列出你的主目录绝对路径名的命令。
- 8. 写下你的系统上 /etc/passwd 文件中包含你登录信息的行。你的登录 shell、用户 ID、主目录和组 ID 是什么？你的系统是否在 /etc/passwd 或 /etc/shadow 文件中包含加密密码？
- 9. 如果 /etc/passwd 文件中行的最后一个字段被替换为 /usr/bin/date 会发生什么？为什么？
- 10. 你机器上根目录和你的主目录的 inode 号码是什么？给出你用来查找这些 inode 号码的命令。
- 11. 在你的主目录中创建一个名为 memos 的目录。进入该目录并使用 vi 等编辑器之一创建一个名为 memo.james 的文件。给出该文件的三个路径名。
- 12. 给出一个用于在你在问题 11 中创建的 memos 目录下创建名为 personal 的子目录的命令。
- 13. 复制 memo.james 文件并将其放入你的主目录。将复制的文件命名为 temp.memo。给出完成此任务的两个命令。
- 14. 为你的 memos 目录绘制一个像图 4.5 所示的图表。清楚地显示所有目录条目，包括其中所有文件和目录的 inode 号码。

