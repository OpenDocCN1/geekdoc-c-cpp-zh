
- A.3.1 概念总结 ................................................................................ 550
- A.3.2 练习题 ....................................................................... 551

你在计算机上所做的一切都涉及软件的运行。在最基础的层，你的计算机运行着某个操作系统，它控制着发生的一切，组织数据并允许你在其中执行其他程序。你选择使用什么操作系统和工具对你处理工作的方式有重大影响。本章将带你了解一些你可能使用但可能并不熟悉的工具。随后，我们将介绍在书中其余部分使用的标准 Scala 分发中的某些工具。

你对工具的选择从选择操作系统开始。你很可能熟悉 Windows PC 或 Macintosh 环境中常见的图形化界面。由于如此，我们不会花时间来介绍它们。相反，本附录将介绍如何使用文本界面与各种操作系统进行交互。能够使用这种界面有很多理由。对于我们的目的来说，最重要的一点是，这是我们与我们将要使用的某些 Scala 工具交互的方式。

# A.1 Unix/Linux（包含 Mac OS X）

本节涵盖了你在 Linux 和 Unix 环境中遇到的环境。Mac OS X 是在 BSD Unix 之上构建的，这里的所有内容适用于 Mac。如果你使用的是 Mac，可以打开终端（terminal）来访问命令行工具。

## A.1.1 命令行

如今大多数人已经习惯了图形用户界面（GUI）那种指向并点击的操作方式。这并不是人们一直与计算机交互的方式。事实上，GUI 的运行需要大量的处理能力。多年来，计算机必须拥有更简单的界面。即使在今天，有时你需要在没有 GUI 的情况下与计算机交互。这可能发生在计算机出现故障时，或者你需要使用位于远程的命令时。

即使计算机正在运行 GUI，你也可以选择使用命令行界面进行交互。使用命令行可以为你提供在 GUI 中不易实现的能力。许多人选择不使用提示符（prompt）是因为它有一定的学习曲线。你需要了解一些基础知识才能完成任何事情。如果你打算花大量时间在计算机上工作，那么花一点精力学习你操作系统命令行界的基本命令是值得的。

### A.1.1.1 文件与目录

在 GUI 中，你将文件组织在文件夹中。你拥有代表不同文件类型或文件夹的实体，可以将文件/文件夹放在文件夹内部以进行组织。这些概念源于命令行中已经存在的系统。唯一的区别是术语。“folder”一词从图形角度来看很好。在命令行中，它们长期以来被称为“directories”。

我们将学习的第一组用于处理文件和目录的命令，以便我们进行导航。以下是命令列表以及每个命令的简要描述。你会发现，通常这些命令是其功能的缩写。

- `cat` 显示一个或多个文件的内容。
- `cd` 目录。
- `cp` 将一个文件复制到指定的名称或位置。
- `less` - 显示一个或多个文件的内容，并具备向前向后移动、搜索等功能。（少即是多，少于多）。
- `ls` - 列出目录的内容。
- `mkdir` - 创建目录。
- `more` - 显示一个或多个文件的内容，并具备分页查看或搜索的功能。
- `pwd` - 代表“print working directory”。它会打印出你当前所在的目录。
- `rm` - 删除文件。
- `rmdir` - 如果目录为空，则删除该目录。

命令行的优势在于每个命令都可以跟上参数。仅仅输入命令等同于双击程序图标。正是参数让你能够指定额外信息。除非你给它们提供一个或多个文件/目录名称进行操作，否则这些命令中的大多数都不会执行任何操作。

为了让你了解如何使用这些命令，我们将从 `pwd` 开始。这是一个非常简单的命令，如果你迷失了在目录结构中的位置，它就会派用场。在命令提示符下只需输入 `pwd` 并按回车键。具体得到什么取决于许多因素，但它应该打印出一行显示当前目录的输出。它看起来像这样。

```
mlewis@mlewis-laptop:~$ pwd
/home/mlewis
mlewis@mlewis-laptop:~$ 
```

在这种情况下，目录是 `/home/mlewis`。打印输出后，我们得到了一个新的输入下一个命令的提示符。

> 备注
>
> 在 Unix 和 Linux 系统，整个文件系统的根是 `/`。这就是为什么它出现在 `/home/mlewis` 目录开头。以 `/` 开头的目录是绝对目录。

我们想要输入的下一个命令是 `ls` 命令。输入 `ls`，后跟一个参数，你将获得当前目录下所有文件的列表。这是该命令最基本的用法。你也可以通过 `ls` 命令后跟随一个目录名称来查看任何其他目录的内容。在这里我们看到根目录内容的列表。

```
mlewis@mlewis-laptop:~$ ls /
bin dev initrd list-found opt sbin tmp vminuz
boot initrd.img lib32 media proc srv usr vminuz
cdrom home initrd.img lib64 mnt root sys var
```

如果你列出的目录不以 `/` 开头，那么它将是一个相对目录，这意味着该目录的位置相对于当前工作目录。你所列出的目录将附加到当前目录的末尾。例如，你可能在当前目录下有一个名为 `Desktop` 的目录。输入 `ls Desktop` 将列出当前目录下 `Desktop` 目录的内容。

```
mlewis@mlewis-laptop:~$ ls Desktop
AdobeReader.desktop QtCreator.desktop
```

你还可以指定多个文件或目录，它们将如所示全部列出。

```
mlewis@mlewis-laptop:~$ ls Desktop /
bin dev initrd list-found opt sbin tmp vminuz
boot initrd.img lib32 media proc srv usr vminuz
cdrom home initrd.img lib64 mnt root sys var
```

Desktop:

AdobeReader.desktop QtCreator.desktop

如你所见，当前目录的内容列在 `:` 下方的行中，而 Desktop 的内容列在 Desktop 下方：

你可能不会认为你平时会一直使用通配符。实际上，这是 shell 的一个功能。如果你在名称中放入 `*`，当 `*` 被替换为零或多个字符时，系统将将其替换为所有匹配的文件或目录。这里是该用法的示例。

```
mlewis@mlewis-laptop:~$ ls /home/mle*
/home/mlewis
```

对于第一行，`*` 被替换为空。对于第二行，它被替换为“old”。你也可以使用 `?` 代表任意一个字符。这些通配符不会被 `ls` 命令看到，它会将它们替换为传递给命令的所有匹配文件名。

`ls` 还有很多其他选项。这些选项都以连字符开头。最常用的选项是 `-l`，它告诉 `ls` 使用长格式。这是它的例子：

```
mlewis@mlewis-laptop:~$ ls -l Desktop
total 8
drwxr-xr-x 2 root root 4096 Oct 27 12:21 AdobeReader.desktop
rw-r--r-- 1 mlewis mlewis 256 Oct 27 12:23 QtCreator.desktop
```

长格式将每个文件或目录放在一行。除了文件外，它还显示了指向该文件的链接数。前面的字符显示权限。在之后是该文件所属的用户和所有者。最后的信息是文件大小以及最后修改的日期和时间。

下一个常用的选项是 `-a`。它告诉 `ls` 列出所有文件，包括隐藏文件。Unix 和 Linux 中的隐藏文件是以点开头的文件。在这里我们看到结合长格式的用法。选项合并时只需要一个连字符：

```
mlewis@mlewis-laptop:~$ ls -al Desktop
total 16
drwxr-xr-x 2 root root 4096 Oct 27 12:22 ..
drwxr-xr-x 2 mlewis mlewis 4096 Oct 27 12:21 AdobeReader.desktop
rw-r--r-- 1 mlewis mlewis 256 Oct 27 12:23 QtCreator.desktop
```

这额外增加了两行。左侧的字母 `d` 告诉我们这些实际上是目录。`.` 是当前目录的名字。`..` 是当前目录所在的目录的名称。我们也可以将其称为父目录。默认情况下，命令在当前目录运行。由于这个原因，你最常用的命令之一是 `cd`，它改变当前目录。`cd` 后面跟着一个目录名称。该目录将成为当前目录。正如我们刚刚看到的，每个目录内部都有 `.` 和 `..` 名称。如果你想向上移动目录，只需随时执行 `cd ..` 即可返回你的主目录。后面的命令改变了当前目录。

```
mlewis@mlewis-laptop:~$ cd Desktop
mlewis@mlewis-laptop:~$ 
```

# 了解工具

![](img/06d4e84f27a8884ea40ba6182ec7c778_555_0.png)

图 A.1: 一个带有命令提示符的 Linux 终端示例。

- `less` - 显示一个或多个文件的内容，并具备向前向后移动、搜索等功能。（少即是多，少于多）。
- `ls` - 列出目录的内容。
- `mkdir` - 创建目录。
- `more` - 显示一个或多个文件的内容，并具备分页查看或搜索的功能。
- `pwd` - 代表“print working directory”。它会打印出你当前所在的目录。
- `rm` - 删除文件。
- `rmdir` - 如果目录为空，则删除该目录。

命令线的优势在于每个命令都可以跟上参数。仅仅输入命令等同于双击程序图标。正是参数让你能够指定额外信息。除非你给它们提供一个或多个文件/目录名称进行操作，否则这些命令中的大多数都不会执行任何操作。

为了让你了解如何使用这些命令，我们将从 `pwd` 开始。这是一个非常简单的命令，如果你迷失了在目录结构中的位置，它就会派用场。在命令提示符下只需输入 `pwd` 并按回车键。具体得到什么取决于许多因素，但它应该打印出一行显示当前目录的输出。它看起来像这样。

```
mlewis@mlewis-laptop:~$ pwd
/home/mlewis
mlewis@mlewis-laptop:~$ 
```

在这种情况下，目录是 `/home/mlewis`。打印输出后，我们得到了一个新的输入下一个命令的提示符。

> 备注
>
> 在 Unix 和 Linux 系统，整个文件系统的根是 `/`。这就是为什么它出现在 `/home/mlewis` 目录开头。以 `/` 开头的目录是绝对目录。

我们想要输入的下一个命令是 `ls` 命令。输入 `ls`，后跟一个参数，你将获得当前目录下所有文件的列表。这是该命令最基本的用法。你也可以通过 `ls` 命令后跟随一个目录名称来查看任何其他目录的内容。在这里我们看到根目录内容的列表。

```
mlewis@mlewis-laptop:~$ ls /
bin dev initrd list-found opt sbin tmp vminuz
boot initrd.img lib32 media proc srv usr vminuz
cdrom home initrd.img lib64 mnt root sys var
```

如果你列出的目录不以 `/` 开头，那么它将是一个相对目录，这意味着该目录的位置相对于当前工作目录。你所列出的目录将附加到当前目录的末尾。例如，你可能在当前目录下有一个名为 `Desktop` 的目录。输入 `ls Desktop` 将列出当前目录下 `Desktop` 目录的内容。

```
mlewis@mlewis-laptop:~$ ls Desktop
AdobeReader.desktop QtCreator.desktop
```

你还可以指定多个文件或目录，它们将如所示全部列出。

```
mlewis@mlewis-laptop:~$ ls Desktop /
bin dev initrd list-found opt sbin tmp vminuz
boot initrd.img lib32 media proc srv usr vminuz
cdrom home initrd.img lib64 mnt root sys var
```

Desktop:

AdobeReader.desktop QtCreator.desktop

如你所见，当前目录的内容列在 `:` 下方的方的中，而 Desktop 的内容列在 Desktop 下方：

你可能不会认为你平时会一直使用通配符。实际上，这是 shell 的一个功能。如果你在名称中放入 `*`，当 `*` 被替换为零或多个字符时，系统将将其替换为所有匹配的文件或目录。这里是该用法的示例。

```
mlewis@mlewis-laptop:~$ ls /home/mle*
/home/mlewis
```

对于第一行，`*` 被替换为空。对于第二行，它被替换为“old”。你也可以使用 `?` 代表任意一个字符。这些通配符不会被 `ls` 命令看到，它会将它们替换为传递给命令的所有匹配文件名。

`ls` 还有很多其他选项。这些选项都以连字符开头。最常用的选项是 `-l`，它告诉 `ls` 使用长格式。这是它的例子：

```
mlewis@mlewis-laptop:~$ ls -l Desktop
total 8
drwxr-xr-x 2 root root 4096 Oct 27 12:21 AdobeReader.desktop
rw-r--r-- 1 mlewis mlewis 256 Oct 27 12:23 QtCreator.desktop
```

长格式将每个文件或目录放在一行。除了文件外，它还显示了指向该文件的链接数。前面的字符显示权限。在之后是该文件所属的用户和所有者。最后的信息是文件大小以及最后修改的日期和时间。

下一个常用的用的选项是 `-a`。它告诉 `ls` 列出所有文件，包括隐藏文件。Unix 和 Linux 中的隐藏文件是以点开头的文件。在这里我们看到结合长格式的用法。选项合并时只需要一个连字符：

```
mlewis@mlewis-laptop:~$ ls -al Desktop
total 16
drwxr-xr-x 2 root root 4096 Oct 27 12:22 ..
drwxr-xr-x 2 mlewis mlewis 4096 Oct 27 12:21 AdobeReader.desktop
rw-r--r-- 1 mlewis mlewis 256 Oct 27 12:23 QtCreator.desktop
```

这额外增加了两行。左侧的字母 `d` 告诉我们这些实际上是目录。`.` 是当前目录的名字。`..` 是当前目录所在的目录的名称。我们也可以将其称为父目录。默认情况下，命令在当前目录运行。由于这个原因，你最常用的命令之一是 `cd`，它改变当前目录。`cd` 后面跟着一个目录名称。该目录将成为当前目录。正如我们刚刚看到的，每个目录内部都有 `.` 和 `..` 名称。如果你想向上移动目录，只需随时执行 `cd ..` 即可返回你的主目录。后面的命令改变了当前目录。

```
mlewis@mlewis-laptop:~$ cd Desktop
mlewis@mlewis-laptop:~$ 
```

默认情况下，`rm` 不删除目录。要删除目录，可以使用该命令。像 `mkdir` 一样，你需要在命令后面加上想要删除的一个或多个目录名称。`rmdir` 仅在目录为空时才会删除。因此，你必须先删除目录中的内容，才能将其删除。

## A.1.1.2 旁注

如果你确实想删除整个目录及其所有内容，包括可能的其他目录，`rm` 有一个选项可以做到。`-r` 选项允许 `rm` 或 `cp` 递归地进入目录，并删除或复制其所有内容。如果你想复制目录，这非常有帮助。记住要小心操作。使用 `-r` 标志的 `rm` 可能会删掉许多你想保留的文件。下面的命令使用 `-r` 将一个整个目录及其所有内容复制到当前目录。
