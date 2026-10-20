

Current open archive is tmp-math2lib.a
rw-r--r-- 0/0  1416 Jan  1 05:00 1970 compute.o
rw-r--r-- 0/0  1736 Jan  1 05:00 1970 input.o
...
AR >save
AR >end
$

你也可以通过使用提供给 MRI 图书管理员的标准输入脚本来创建归档，或使用现有归档。在下面的会话中，我们将 ar_script 文件中的脚本提供给 MRI 图书管理员。该脚本创建 math3lib.a 归档并对其执行与本节开头命令行会话中对 math2lib.a 执行的相同的操作。

```
$ more ar_script
create math3lib.a
addmod input.o compute.o
delete compute.o
list
addmod compute.o
list
save
end
$ ar -M < ar_script
Current open archive is tmp-math3lib.a
input.o
Current open archive is tmp-math3lib.a
compute.o
input.o
$ ar t math3lib.a
compute.o
input.o
$
```

你可以通过浏览 ar 的手册页了解有关 MRI 图书管理员附加功能的更多信息。请注意，与修改现有归档（即从归档中删除和添加现有对象）相比，删除现有归档并从头开始创建全新的归档更有效。

## Exercise 14.10

在你的系统上重复之前的会话，以了解 MRI 图书管理员的工作方式。

## 14.5.6 Working with Libraries Using ranlib and nm

库是对象模块的归档。因此，使用库涉及创建库、对库中的模块进行排序以及显示库信息。我们在上一节中以几种方式讨论了库的创建和操作。在本节中，我们讨论剩余的两个操作：对归档进行排序和显示库信息。

### 14.5.6.1 Ordering Archives

ar 命令创建的归档文件中的对象文件没有保持特定的顺序。在某些 Linux 系统上，被调用函数必须出现在调用函数之前，无论它们是否在同一模块或不同模块中。这是一个问题，因为 gcc 和 ld 命令无法定位对象模块，除非它们被正确排序。当它们无法定位对象模块时，这些命令在遇到归档中对象模块的函数调用时会显示未定义符号错误消息。处理此问题的最简单方法是使用 ranlib 实用程序，该实用程序

将目录表添加到作为其参数传递的一个或多个归档中。此实用程序执行与 ar 命令使用 s 键相同的任务。以下是 ranlib 实用程序的简要说明。

**Syntax:**
    ranlib [archive-list]**
**Purpose**: Adds a table of contents to each archive in archive-list

以下 ranlib 命令将目录表添加到 mathlib.a 归档中。ar s mathlib.a 命令也可以用来执行相同的任务。

```
$ ranlib mathlib.a
$
```

### 14.5.6.2 Displaying Library Information

nm 实用程序可用于显示库、对象文件和可执行文件的符号表（名称、类型、大小、入口点等）。该命令为指定文件中的每个对象（函数和全局变量）显示一行。此输出告知你在库中可用的函数以及这些函数所依赖的函数。每行输出包括对象的大小（以字节为单位）、对象的类型（数据对象、函数、文件等）、对象的范围以及对象的名称。此信息对于调试库非常有用。以下是该实用程序的简要说明。

**Syntax:**
    nm key archive-name [file-list]**
**Purpose**: Allows display of the symbol table of the library and object files specified in file-list
**Commonly used options/features:**
    -A  Display before each symbol the name of the input file (or archive) in which it was found
    -v  Display the version number of the command
    -n  Display symbols according to their address and not alphabetically
    -s  Display names of the modules that contain the definitions of the symbols

以下字符指定符号类型：

+   A/a        Global/local absolute symbol
+   B/b        Global/local symbol in the uninitialized data segment (also known as bss)
+   D/d        Global/local symbol in the initialized data segment
+   f          Symbol name in the source file
+   L/l        Global/static thread-local symbol
+   R/r        Global/local symbol in a read-only data segment
+   T/t        Global/local symbol in the text (code) segment
+   U          Undefined symbol

在下面的会话中，使用 nm -v 命令显示 nm 命令的版本，并使用 nm mathlib.a 命令显示我们在第 14.5.5.1 节中创建的 mathlib.a 库的信息。

```
$ nm -v
GNU nm (GNU Binutils for Ubuntu) 2.26.1
Copyright (C) 2015 Free Software Foundation, Inc.
This program is free software; you may redistribute it under the terms of
the GNU General Public License version 3 or (at your option) any later version.
```

```
This program has absolutely no warranty.
$ nm mathlib.a
compute.o:
0000000000000000 T compute
                         U pow

input.o:
0000000000000000 T input
                         U __isoc99_scanf
                         U printf
                         U __stack_chk_fail
$
```

nm 命令的输出显示它包含两个对象模块：**input.o** 和 **compute.o**。此外，printf、scanf 和 pow 符号是未定义的（U），并且符号 input 和 compute 位于库中相关对象模块的文本（代码）段中。

nm 和 grep 命令通常一起运行以检索有关特定对象的信息。以下命令用于显示当前目录中所有归档文件中 pow 符号的信息。输出显示该符号未定义并在 math2lib.a 和 math3lib.a 两个归档中找到。

```
$ nm -A *.a | grep pow
math2lib.a:compute1.o:                 U pow
math3lib.a:compute2.o:                 U pow
$
```

你可以使用 –u 选项与 nm 命令一起使用以显示对象、可执行文件或归档文件中的所有未定义符号。以下命令用于显示 **math2lib.a** 中的所有未定义符号。请注意，所有未定义符号都在各个库中，并由链接器解析。

```
$ nm -u *.a

math2lib.a:

compute.o:
                         U pow

input.o:
                         U __isoc99_scanf
                         U printf
                         U __stack_chk_fail
$
```

## Exercise 14.11

在你的系统上重复上一节中的命令，以验证它们是否生成相同的输出。

## 14.5.7 Version Control with git

请参阅附录 A，了解如何在我们四个代表性的 Linux 系统上安装 git 的说明。它可以非常有效地用于你的 Linux 系统上的版本控制。我们在本书网站第 W24 章第 5.7 节中对 git 命令进行了完整描述。有关通过 Web 浏览器界面获取本书 GitHub 站点上材料的说明在前言中给出。要使用 git 命令将 https://github.com/bobk48/linuxtextbook 上的整个存储库“拉取”到你自己的 Linux 系统，请执行以下步骤。

1. 首先在你自己的 Linux 系统上设置一个新的本地存储库工作目录并将其初始化为 git 仓库。

```
$ mkdir linuxthetextbook3
$ cd linuxthetextbook3
$ git init
$ git remote add origin https://github.com/bobk48/linuxthetextbook
```

这已在 /usr/home/your_username/linuxthetextbook3/. git/ 中初始化了一个空的 git 仓库，其中 your_username 是你在 Linux 系统上的用户名。它还设置了从远程 GitHub 站点拉取的 origin。

2. 在新仓库中放入一个文件。

```
$ touch Readme.txt
```

3. 检查新仓库的状态。

```
$ git status
On branch master
Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	Readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```

4. 暂存 Readme.txt 文件，并在新仓库中进行初始提交。

```
$ git add Readme.txt
$ git commit -m "First commit"
[master (root-commit) 57e0400] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 Readme.txt
```

5. 使用 git pull 命令从名为 master 的分支拉取并合并整个书的 GitHub 仓库。

```
$ git pull https://github.com/bobk48/linuxthetextbook master
From https://github.com/bobk48/linuxthetextbook
```

你现在已在自己的 Linux 系统上拥有了本书 GitHub 站点的全部内容。

## 14.6 Static Analysis Tools

对程序的静态分析涉及在不执行程序的情况下分析程序的结构和属性。这些分析通常用于确定代码在多个平台上的可移植性水平、代码行数（LOC）、程序中的函数调用/点（FPs）数量以及代码中每个函数所花费的时间百分比。在软件项目的规划阶段，LOC 和 FPs 等参数通常用于软件成本模型中，用于估计完成软件项目所需的人月数，从而得出软件成本。

