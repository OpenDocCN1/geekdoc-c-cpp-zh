

递归复制之前

递归复制之后

![](img/2a18e06cd9c6395e451f26126ecba1fd_159_0.png)

图 6.2 执行 `cp -r ~/courses ~/backups` 命令前后的当前目录。

该命令创建 ~/courses 目录的副本，包括 ~/courses 目录下的所有文件和目录层次结构，并将其放置在 ~/backups 目录下。图 6.2 显示了执行该命令前后你的主目录（~）的状态。

## 6.3.2 移动文件

文件可以从文件结构中的一个目录移动到另一个目录。在 Linux 中，此操作如果在同一文件系统上，也可能只是重命名文件。重命名操作等效于为文件创建硬链接（参见第 8 章），然后删除/移除（参见第 6.3.3 节）原始文件。如果源文件和目标文件位于不同的文件系统，则移动操作会将源文件的物理副本复制到目标位置，然后删除源文件。移动文件的命令是 mv。以下是该命令的简要说明。

```
Syntax:
  mv [options] file1 file2
  mv [options] file-list directory
Purpose: First syntax: Move file1 to file2 or rename file1 to file2
  Second syntax: Move all the files in file-list to directory
Commonly used options/features:
  -f Force move regardless of the permissions of the destination file
  -i Prompt the user before overwriting the destination file
```

你必须具有包含源文件（描述中的 file1）的目录的写和执行访问权限，但不需要对文件本身具有读、写或执行权限。同样，你必须具有包含目标/目标文件（描述中的 file2）的目录的写和执行权限，具有目标文件路径中每个目录的执行权限，以及如果目标文件已存在则具有对目标文件的写权限。如果目标文件存在，默认情况下它会在不通知你的情况下被覆盖。如果你使用 -i 选项，则会在覆盖目标文件之前提示你。

以下命令将 temp 移动到 temp.moved。在这种情况下，temp 文件被重命名为 temp.moved。如果 temp 不存在，或者你没有其所在目录的执行权限，mv 命令会返回错误消息。如果 temp.moved 已存在，但你没有它的写权限，则该命令会提示你移动文件。

![](img/2a18e06cd9c6395e451f26126ecba1fd_160_0.png)

图 6.3 执行 `mv temp backups/temp.old` 命令前后的当前目录。

以下命令将 temp 移动到 backups 目录作为 temp.old 文件。图 6.3 显示了 temp 文件移动前后的当前目录状态。

```
$ mv temp backups/temp.old
```

以下命令是强制移动；你可以使用它来强制移动，无论目标文件 temp.moved 的权限如何。

```
$ mv -f temp temp.moved
```

以下命令将 dir1 中的所有文件和目录（排除隐藏文件）移动到 dir2 目录。如果 dir2 不是目录、不存在，或者你没有它的写和执行权限，则命令会失败，并在屏幕上显示错误消息。

```
$ mv dir1/* dir2
```

执行命令后，dir1 仅包含隐藏文件。你可以使用 ls -a 命令来确认 dir1 的状态。

### 练习 6.7

在你的主目录下创建本节讨论的文件目录结构，包括目录 dir1 和 dir2，并在你的系统上重复本节所示的命令。命令执行结果是否如预期？

当文件不再需要时，应将其从文件结构中删除以释放磁盘空间供新文件和目录重复使用。Linux 中用于删除（删除）文件的命令是 rm。以下是该命令的简要说明。

```
rm: cannot remove 'd1/f1': Permission denied
$ ls -l d1
ls: cannot open directory 'd1': Permission denied
$
```

### 练习 6.8

在你的系统上重复本节讨论的 rm、ls、cp 和 touch 命令。命令执行结果是否如预期？

## 6.3.4 确定文件大小

你可以使用多种 Linux 命令来确定文件大小。用于此目的且在所有 Linux 版本中都可用的两个常用命令是 ls -l 和 wc。我们在第 5 章中描述了 ls -l 命令，我们在其中使用它来确定文件的访问权限。我们在此在确定文件大小的上下文中重新讨论此命令。

如前所述，ls -l 命令以长列表形式显示作为其参数指定的目录（或目录）中的文件和目录。你必须具有目录的读和执行权限才能成功在其上运行 ls 命令；无需对目录中的文件具有任何权限即可查看列表。如果未指定参数，则该命令会给出当前目录的输出。该命令的输出有九个字段，第五行字段给出文件大小（以字节为单位）（参见第 5.5 节）。在以下命令中，lab2 文件的大小为 709 字节。

```
$ ls -l lab2
-rw-r--r-- 1 sarwar faculty 709 Apr  5 11:23 lab2
$
```

该命令还显示目录文件的大小。你也可以通过在命令行中指定多个文件并用空格分隔来获取多个文件的大小。例如，以下命令显示 lab1 和 lab2 文件的大小分别为 163 字节和 709 字节。

```
$ ls -l lab1 lab2
-rw-r--r-- 1 sarwar faculty 163 Jul  9 16:47 lab1
-rw-r--r-- 1 sarwar faculty 709 Apr  5 11:23 lab2
$
```

以下命令使用 shell 元字符 * 来显示 ~/courses/ee446 目录中所有文件的长列表。

```
$ ls -l ~/courses/ee446/*
... output of the command ...
$
```

虽然 ls -l 是一个通用命令，可用于确定一个或多个文件的许多属性，包括它们以字节/字符为单位的大小，但 wc 是一个专用命令，仅显示文件大小。以下是 wc 命令的简要说明。

```
Syntax:
  wc [options] file-list
Purpose: Display sizes of the files in file-list as number of lines, words, and characters
Commonly used options/features:
  -c  Display only the number of characters
  -l  Display only the number of lines
  -w  Display only the number of words
```

![](img/2a18e06cd9c6395e451f26126ecba1fd_164_0.png)

```
$ wc sample
4 44 227 sample
```

第一个命令显示当前工作目录中 sample 文件的行数、单词数和字符数。sample 的大小为 4 行、44 个单词、227 字节。第二个命令显示当前工作目录中 letter、sample 和 test 文件的相同信息。该命令输出的最后一行还显示了三个文件的总行数、总单词数和总字节数。第三个命令显示可以在单个命令中使用多个选项；在这种情况下，输出是命令行中三个文件 的单词数和行数。

```
$ wc letter sample test
44 250 1687 letter
4 44 227 sample
2 12 90 test
50 306 2004 total
```

```
$ wc -c letter sample test
1687 letter
227 sample
90 test
2004 total
```

```
$ wc -lw letter sample test
44 250 letter
4 44 sample
2 12 test
50 306 total
```

在 FreeBSD 上，带目录参数的 wc 命令会返回三个数字以及目录名称：0、1 和目录中目录项的数量，包括 .（点）和 ..（点点）目录，如

```
$ wc /etc
0 1 116 /etc
```

这仅适用于其内容包含普通文件和目录的目录。然而，对于包含设备（字符特殊和块特殊）文件和其他类型文件 的目录，不会产生这种样式的输出。

wc 命令可与 shell 元字符如 * 和 ? 一起使用。以下命令显示 /usr/include/x86_64-linux-gnu/sys 目录中所有文件 的大小。最后一行显示目录中所有文件的大小。

```
$ wc /usr/include/x86_64-linux-gnu/sys/*
108 501 3319 /usr/include/x86_64-linux-gnu/sys/acct.h
37 192 1282 /usr/include/x86_64-linux-gnu/sys/auxv.h
3 16 86 /usr/include/x86_64-linux-gnu/sys/bittypes.h
444 2124 15412 /usr/include/x86_64-linux-gnu/sys/cdefs.h
88 559 3575 /usr/include/x86_64-linux-gnu/sys/debugreg.h
27 142 921 /usr/include/x86_64-linux-gnu/sys/dirent.h
29 159 1023 /usr/include/x86_64-linux-gnu/sys/elf.h
```

