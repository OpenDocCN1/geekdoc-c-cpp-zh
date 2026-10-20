

命令行中 y 后面的星号被称为元字符或代表模式的字符；在此情况下，该模式是任意一组字符。当你在键盘上按下 <Enter> 键后 Linux 解析命令时，它会在当前工作目录中搜索所有以字母 my 开头且以其他任何内容结尾的文件。

## In-Chapter Exercise

18. 使用 cd 命令上移到 Linux 文件系统的根目录（/），然后使用它递归地向下进入根目录下的每个子目录，深度为两个子目录，绘制系统中找到的组件文件的图表。使图表中的命名条目尽可能完整，列出你认为必要的尽可能多的文件。保留此图表作为你特定 Linux 发行版文件系统的有用地图。

组织你的目录的另一个方面是文件在目录之间的移动或更改文件在目录中的位置。例如，你现在在主目录中有文件 myfile2，但你希望将其移动到名为 first 的子目录中。参见图 2.3，了解在此阶段更改文件组织的图形描述。要实现这一点，你可以使用为 mv file-list directory 命令说明的第二种语法方法，将文件 myfile2 移到名为 first 的子目录中。要实现这一点，输入以下内容：

```
$ mv myfile2 first
$
```

要验证 myfile2 是否确实在名为 first 的子目录中，输入以下内容：

```
$ cd first
$ ls
myfile2
$
```

你现在将上移到主目录并尝试使用 rm 命令删除或删除一个文件。注意：使用此命令时应非常小心，因为一旦文件被删除，恢复它的唯一方法是从你或系统管理员对文件系统所做的归档备份中恢复。

```
$ cd
$ rm myfile2
rm: myfile2: No such file or directory
$
```

你收到错误消息，因为在主目录中，名为 myfile2 的文件不存在。它已被移入名为 first 的子目录。

目录组织还包括删除空或非空目录的能力。完成删除空目录的命令是 rmdir。rmdir 命令的一般语法如下：

Syntax:
rmdir [options] dirnames
Purpose: Remove the empty directories specified in dirnames
Output: Remove directories
Commonly used options/features:
-p Removes empty parent directories as well
-r Recursively deletes files and subdirectories beneath the current directory

要删除当前工作目录下方的整个目录，输入以下内容：

```
$ rmdir first
rmdir: first: Directory not empty
$
```

由于文件 myfile2 仍在名为 first 的子目录中，first 不是空目录，你会收到错误消息，rmdir 命令不会删除该目录。如果目录为空，rmdir 将完成删除。删除非空目录的一种方法是使用带有 -r 选项的 rm 命令。-r 选项会递归地深入子目录并在实际删除目录本身之前删除其中的任何文件。使用此命令时要谨慎，因为你可能会无意中删除目录和文件。要了解此命令如何删除非空目录，输入以下内容：

```
$ rm -r first
$
```

目录 first 和文件 myfile2 现在已从文件结构中删除。

## 2.4.5 Obtaining Help with the man Command

Linux 系统上提供的一个非常方便的实用程序是在线帮助功能，通过使用 man 命令实现。man 命令的一般语法如下：

Syntax:
  man [options][-s section] command-list
  man -k keyword-list
Purpose: First syntax: Display Linux Reference Manual pages for commands in command-list one screen at a time
Second syntax: Display summaries of commands related to keywords in keyword-list
Output: Manual pages one screen at a time
Commonly used options/features:
  -k keyword-list    Searches for summaries of keywords in keyword-list in a database and display them
  -s sec-num         Searches section number sec-num for manual pages and display them

要使用 man 命令获取帮助，例如 ls 命令的使用和选项，输入以下内容：

```
$ man ls
```

LS(1)                User Commands                LS(1)

NAME
    ls - list directory contents

SYNOPSIS
    ls [OPTION]... [FILE]...

DESCRIPTION
    List information about the FILEs (the current directory by default).
    Sort entries alphabetically if none of -cftuvSUX nor -sort is specified.

    Mandatory arguments to long options are mandatory for short options too.

+   -a, --all
+     do not ignore entries starting with .
+   
+   -A, --almost-all
+     do not list implied . and ..
+   
+   --author

# Manual page ls(1) line 1 (press h for help or q to quit)

Linux 的此输出是 Linux 手册页，或 man 页，它提供了命令用法的概要，显示选项，并提供简要描述，帮助你理解命令应如何使用。显示一页后输入 q，如示例所示，会返回到命令行提示符。按下键盘上的空格键会一次显示一屏与 ls 命令相关的手册页内容。

要获取所有 Linux 命令及其选项的帮助，使用 man man 命令转到 Linux 参考手册页。

手册页本身根据描述的主题和适用于特定系统的主题组织成八个部分。表 2.1 列出了手册的各部分及其包含内容。大多数用户在第 1 节中找到所需的页面。软件开发人员主要使用库和系统调用，因此在第 2 节和第 3 节中找到所需的页面。从事文档准备的用户从第 7 节获得最多的帮助。管理员主要需要参考第 1、4、5 和 8 节的页面。

手册页包含 Linux 中每个命令、系统调用和库调用的多页、专门格式化的描述性文档。此格式由七个一般部分组成：名称、概要、描述、文件列表、相关信息、错误、警告和已知错误。你可以使用 man 命令查看命令的手册页。由于此命令的名称，手册页通常称为 Linux man 页。当你在屏幕上显示手册页时，页面的左上角有命令名称及其所属的部分，用括号括起来，如 ls(1)，在输出的手册页顶部可见。

```
$ man passwd
```

passwd 命令的手册页现在出现在屏幕上，但我们不显示其输出。由于它们是多页文本文档，每个主题的手册页占用超过一屏的文本来显示其全部内容。要一次查看一屏手册页，按键盘上的空格键。要退出查看手册页，按键盘上的 Q 键。

```
$ man pwd
```

| Section | What It Describes |
|---------|-------------------|
| 1       | User commands     |
| 2       | System calls      |
| 3       | Language library calls (C, FORTRAN, etc.) |
| 4       | Devices and network interfaces |
| 5       | File formats      |
| 6       | Games and demonstrations |
| 7       | Environments, tables, and macros for troff |
| 8       | System maintenance-related commands |

如果手册页的多个部分对同一个词有信息，并且你对特定部分的手册页感兴趣，可以使用 -S 选项。因此，以下命令行显示 read 系统调用的手册页，而不是 shell 命令 read 的手册页。

```
$ man -S2 read
```

命令 man -S3 fopen fread strcmp 依次显示三个 C 库调用 fopen、fread 和 strcmp 的手册页。

使用 man 命令并输入带有 -k 选项的命令可以指定一个关键字来限制搜索。它等同于使用 apropos 命令。然后搜索会产生来自系统中包含该关键字引用的所有手册页的有用手册页标题。例如，以下会话在我们的 Linux 系统上产生屏幕输出：

```
$ man -k passwd
chpasswd (8)          - update group passwords in batch mode
chpasswd (8)          - update passwords in batch mode
Crypt::PasswdMD5 (3pm) - Provides interoperable MD5-
                        based crypt() functions
fgetpwent_r (3)        - get passwd file entry reentrantly
getpwent_r (3)         - get passwd file entry reentrantly
gpasswd (1)            - administer /etc/group
                        and /etc/gshadow
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
pam_localuser (8)      - require users to be listed
                        in /etc/passwd
passwd (1)             - change user password
passwd (lss1)          - compute password hashes
passwd (5)             - the password file
```

Output truncated...

## 2.4.6 Other Methods of Obtaining Help

要获取任何特定 Linux 命令的简短描述，可以使用 whatis 命令。这与命令 man -f 相似。whatis 命令的一般语法如下：

| Syntax: |
| whatis keywords |
| Purpose: Search the whatis database for abbreviated descriptions of each keyword |
| Output: Prints a one-line description of each keyword to the screen |

以下是如何使用 whatis 的说明。

两个命令的输出都被截断。

```
$ whatis man
man (7)                - macros to format man pages
man (1)                - an interface to the on-line
                        reference manuals
$
```

你还可以通过在同一命令行上输入多个参数，用空格分隔，来获取多个命令的简短描述。以下是此方法的说明：

```
$ whatis login set setenv
login (1)              - begin session on the system
login (3)              - write utmp and wtmp entries
setenv (3)             - change or add an environment
```

