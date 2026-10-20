

# 练习 7.1

在你的系统上重复上述会话并验证 sort 命令在你的系统上是否按预期工作。

# 练习 7.2

假设 numbers 文件包含以下数据，每行一个：10, 20, 30, 40, 100, 200, 300, 400。使用 sort numbers 对命令进行排序。输出对你来说有意义吗？为什么或为什么不？对于 `sort -c numbers` 命令的输出回答这些问题。

# 练习 7.3

你会使用什么命令对 numbers 文件中的数据进行正确的（预期）排序，即保持数据按给定顺序？

## 7.3 搜索命令和文件

有时，你需要查找某个特定命令或文件是否存在于你的文件结构中。或者，如果你有多个版本的命令，你可能想知道当你运行该命令时执行的是哪一个。我们讨论了可用于此目的的三个命令：find、whereis 和 which。

你可以使用 find 命令搜索满足作为参数传递给它的表达式（参见命令说明）所描述条件的目录列表。命令会递归搜索目录列表；也就是说，目录列表下所有层级的所有子目录都会被搜索。以下是该命令的简要说明。

```
Syntax:
  find directory-list expression
```

Purpose: Search the directories in directory-list to locate files that meet the “criteria” described by the expression (the second argument); the expression comprises one or more “criteria” (see the examples)

Output: None unless it is explicitly requested in expression

# 常用选项/功能：

- -L Follow symbolic links
- -exec CMD The file being searched meets the criteria if the command CMD returns 0 as its exit status (true value for commands that execute successfully); CMD must terminate with a quoted semicolon (\;)
- -group name Search for files belonging to group name or ID name
- -inum N Search for files with inode number N
- -links N Search for files with N links
- -mtime N Search for files whose data was modified within the last N days (for -N) and more than N days (for +N); 0 acts as -1
- -name pattern Search for files that are specified by the pattern
- -newer file Search for files that were modified after file (i.e., are newer than file)
- -ok CMD Like -exec except that the user is prompted first
- -perm octal Search for files if permission of the file is octal
- -print Display the pathnames of the files found by using the rest of the criteria; works even if file names contain white spaces such as newline characters
- -size ±N[C] Search for files of size N blocks; N followed by C can be used to measure size in characters; +N means size > N blocks, and -N means size < N blocks
- -type t File is of type t: b (block special), c (character special), d (directory), f (regular), l (symbolic link—never true with -L option), p (named pipe—FIFO), s (socket)

| -user name | Search for files owned by the user name or ID name |
| \( expr \) | True if expr is true; used for grouping criteria combined with OR or AND |
| ! expr | True if expr is false |

你可以使用 [-a] 或空格进行逻辑 AND，使用 -o 进行逻辑 OR 两个条件。注意在左括号 (\( ) 或右括号 (\) ) 之前和之后，以及 -o 之前和之后至少需要一个空格。复杂的表达式可以用括号 \( 和 \) 括起来。我们现在讨论一些说明性示例。

find（或 find .）命令列出当前目录下所有文件和目录的路径名。find 命令最常见的用途是在一个或多个目录中搜索文件，如第一个示例所示。在这里，命令在你的主目录中搜索 USA.gif 和 Pakistan.gif 文件并显示包含它们的目录的路径名。如果搜索的文件在多个目录中出现，则会显示所有目录的路径名。

```
$ find ~ -name USA.gif -o -name Pakistan.gif
/home/sarwar/myweb/USA.html
/home/sarwar/myweb/Pakistan.html
$
```

以下命令显示你主目录中以 .c 和 .C 结尾的所有文件的绝对路径名。

```
$ find ~ -name '*.c' -o -name '*.C'
...
$
```

下一个命令递归搜索 /usr/include 目录以查找名为 socket.h 的文件并打印该文件的绝对路径名。

```
$ find /usr/include -name socket.h
/usr/include/asm-generic/socket.h
/usr/include/x86_64-linux-gnu/sys/socket.h
/usr/include/x86_64-linux-gnu/asm/socket.h
/usr/include/x86_64-linux-gnu/bits/socket.h
/usr/include/linux/socket.h
$
```

你可能想知道对某个文件的所有硬链接（在第 8 章中讨论）的路径名——即具有相同 inode 号码的文件。以下命令递归搜索根目录以查找所有 inode 号码为 36700164 的文件并打印所有此类文件的绝对路径名。

```
$ find /usr . -inum 36700164
/usr/include
$
```

你可以使用 -perm 选项显示具有给定权限的目录层次结构下的文件。例如，你可以使用 find . -perm 755 命令显示当前目录中具有八进制权限 755 的文件列表（即文件所有者可读、可写、可执行，其他用户可读、可执行）。你可以使用 ls -l 命令验证 find 命令的输出。

```
$ find . -perm 755
.
./sandbox_dir
./my_cat
$ ls -l
total 1916
...
```

以下命令搜索当前工作目录中名称为 core 或扩展名为 .jpg 或 .o 的文件，显示其绝对路径名，并将其从文件结构中删除。括号用于包含复杂条件。确保你在 \(、\) 和 -o 之前和之后使用空格。该命令不会提示你确认删除；要提示确认，请将 -exec 替换为 -ok，或使用 rm -i 命令。

```
$ find . \( -name core -o -name '*.jpg' -o -name '*.o' \) -print -exec rm {} \;
...
$
```

你可以使用 whereis 命令查找你的系统是否具有特定命令，如果有，则在文件结构中的位置。你通常需要在尝试执行你知道有效但 shell 无法定位的命令时获取此类信息，因为包含该命令可执行文件的目录不在你的搜索路径中（参见第 2 章和第 4 章）。在这种情况下，你可以使用 whereis 命令找到命令的位置并更新你的搜索路径。虽然 whereis 是 Berkeley Software Distribution (BSD) 命令，但今天大多数 Linux 系统都有它，因为它们具有 BSD 兼容性包。根据你使用的系统，该命令不仅会给出你正在搜索的命令的绝对路径名，还会给出其手册页和源文件的绝对路径名（如果在你的系统上可用）。以下是该命令的简要说明。

Syntax:
    whereis [options] [file-list]
Purpose: Locate binaries (executable files), source codes, and manual pages for the commands in file-list—a space-separated list of command names
Output: Absolute pathnames for the files containing binaries, source codes, and manual pages for the commands in file-list
Commonly used options/features:
    -b Search for binaries (executable files) only
    -s Search for source code only

以下示例说明了 whereis 命令的使用。第一个命令用于定位 ftp 命令。第二个命令用于定位 cat 命令的可执行文件。最后一个命令定位 find 和 tar 命令的信息。

```
$ whereis ftp
ftp: /usr/bin/ftp /usr/share/man/man1/ftp.1.gz
$ whereis -b cat
cat: /bin/cat
$ whereis find tar
find: /usr/bin/find /usr/share/man/man1/find.1.gz /usr/share/info/find.info.gz
tar: /usr/lib/tar /bin/tar /usr/include/tar.h /usr/share/man/man1/tar.1.gz
$
```

在这些命令的输出中，/bin 目录包含基本用户命令的可执行文件（也称为二进制文件），/usr/bin 目录包含实用程序、应用程序和命令的可执行文件，/usr/share/man 目录包含多个子目录，其中包含 Linux 在线手册的各个部分，/usr/lib 包含编程语言和包的库，而 /usr/include 目录包含头文件。

在一个具有多个版本命令的系统中，which 实用程序可用于确定当你在使用的 shell 中输入命令时被执行的版本的位置（绝对路径名）。以下会话显示了该命令的示例运行。

