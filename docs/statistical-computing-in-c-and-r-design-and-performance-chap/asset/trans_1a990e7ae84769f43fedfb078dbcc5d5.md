

## 附录 A

## Unix 简介

在本附录中，我们将对一些基础的 Unix 命令进行简要概述。更详细的处理可以在大量的在线教程和书籍中找到，例如 Kochan 和 Wood (2003)。

本附录的重点环境是 Unix shell 的命令行；虽然本文中的许多工作可以通过各种图形用户界面完成，但即使在远程登录时，命令行也总是可用的。因此，了解如何在该环境中工作是值得的。

用户与 Linux 操作系统之间的接口由通常称为 shell（外壳）的命令行解释器提供。有许多 shell 选项，包括 Bourne 类型 (sh, bash 和 tsh)、C 类型 (csh 和 tsch) 以及 Korn 类型 (ksh) shell。它们每种都代表一种不同的编程语言，其目的是解释在 shell 提示符（通常形式为 $ 或 %）所在的 shell 命令行上输入的 Unix 命令。在我们的工作中，我们将专门地使用 bash shell。可以通过在命令行中输入以下命令来启动它：

```
$ bin/bash
```

Unix 使得传输和复制文件、编译代码、启动应用程序等成为可能。这些通用命令的格式为：

```
commandName -option arguments
```

其中 `commandName` 是一个单一的、区分大小写的“单词”，由几个字母组成，通常是命令目的缩写。命令可能包含也不包含额外的选项。此类额外规格的细节可以通过在命令行中输入相关的命令帮助页来获取：

```
man commandName
```

一组相关但有时不同的信息可以通过 `info commandName` 访问。如果你能记得一个命令的名字但回想不起它的作用是什么，那么通过输入 `what commandName` 可以返回该信息。如果你只记得命令的一部分 `commandNamePart`，那么执行 `apropos commandNamePart` 将在 `whatis` 数据库中搜索字符串 `commandName` 的出现情况。

磁盘内存在 Unix 中被组织为树形结构。它从根目录开始，根目录代表树的顶端，子目录从根目录开始派分支。这些子目录又有进一步的子目录，等等。当你首次登录时，shell 会打开你的个人主目录，其名称类似于：

```
/home/yourUserName
```

或

```
/Users/yourUserName
```

其中 `UserName` 是你在系统中给出的用户名。通过在命令行中输入 `pwd`（代表当前工作目录）可以获取你在目录树中的当前位置。

## 480 Unix 简介

从我们最初的登录位置开始，我们想要去不同的地方并完成不同的事情。此类目的的命令将在后续章节中讨论。介绍是根据具有相似或相关目的的命令分组进行组织的。

### A.1 移动与查找

在 Unix 中从点 A 移动到点 B的主要工具是切换目录命令 `cd`。例如，通过输入：

```
cd pathToDirectory/directoryName
```

你将从当前位置沿着 `pathToDirectory` 指定的路径移动，并到达 Unix 树上的 `directoryName`。有多种指定路径的快捷方式。但有效的是由 `/` 分隔的列表，它从根目录开始，并详细列出从根目录到感兴趣位置沿中的每一个站点。通常，这就是我们在全文中所指的路径（path）。例如，命令 `cd /usr/local/share` 将带你从目录树中的当前位置，通过根目录 `/` 进入 `usr` 子目录，然后进入其 `local` 子目录，最后到达 `share` 子目录。

一个非常有用的快捷方式是符号 `~`，它可以始终用来代替你的主目录名称。一些实用的相关快捷命令包括：

```
cd .. 将带你向下移动一层到根目录，以及
cd 在不带参数时，它总是将你返回到主目录。
```

### A.2 查看那里有什么

现在，你已经到达了一个位置（或知道感兴趣的位置），并想找出那里有什么。列出命令 `ls` 可用于此目的。具体来说：

```
ls pathToDirectory/directoryName
```

将提供通过 `pathToDirectory` 到达的 `directoryName` 中所有文件的列表。更通地说，

```
ls -l pathToDirectory/directoryName
```

给出一个完整的列表，从左到右为目录中的每个文件提供以下信息：

- 读、写和执行权限（将在下文详细讨论），
- 硬链接数（即引用该文件或目录的目录条目数），
- 所属用户，
- 所属组，
- 文件或目录的大小（字节字节），
- 创建日期以及
- 文件或目录名称。

事实证明 `ls` 或 `ls -l` 都没有说明全部情况。很多时候，你的目录中有以 `.` 开头的文件，例如 `.bashrc` 和 `.emacs`。要看到这些，你必须使用 `ls -a`。在不指定路径的情况下使用 `ls` 将返回将其应用于当前目录的结果。

## 创建与销毁事物

`find` 命令为我们确定目录内容所需的信息。对于大型目录（以及其他原因），有时自动搜索目录内部感兴趣的内容是理想的。这可以通过 `find` 命令实现。例如：

```
find pathToDirectory/directoryName -name filename
```

将定位任何在 `directoryName` 中名为 `filename` 的文件。通常，与其寻找特定的文件，不如真正需要的是所有与 `name` 名字相似的文件列表。如果你只记得命令的一部分 `commandNamePart`，那么 `apropos commandNamePart` 将在 `whatis` 数据库中搜索字符串 `commandName` 的出现情况。

磁盘内存在 Unix 中被组织为树形结构。它从根目录开始，根目录代表树的顶端，子目录从根目录开始派分支。这些子目录又有进一步的子目录，等等。当你首次登录时，shell 会打开你的个人主目录，其名称类似于：

```
/home/yourUserName
```

or

```
/Users/yourUserName
```

其中 `UserName` 是你在系统中给出的用户名。通过在命令行中输入 `pwd`（代表当前工作目录）可以获取你在目录树中的当前位置。

### A.3 创建与销毁事物

到目前为止，与 Unix 的交互是相对静态的。但一旦你可以创建和删除文件，事情就会变得有趣。创建一个文件的最简单方法是通过 `touch` 命令，在输入时创建一个空文件：

```
touch fileName
```

要删除文件，使用删除命令 `rm`，例如：

```
rm fileName
```

最重要的事情之一创建一个目录，创建目录命令 `mkdir` 可用于实现这一点。例如：

```
mkdir directoryName
```

向当前目录添加一个新目录。该目录可以使用删除命令 `rmdir` 移除：

```
rmdir directoryName
```

前提是 `directoryName` 是空的。如果不是这种情况，则必须使用 `rm` 的递归选项 `-r`。特别是：

```
rm -r directoryName
```

这将删除 `directoryName` 及其所有内容。
如果所有文件都从头开始，生活将变得非常复杂。复制命令通过允许从一个地方复制到另一个地方避免了我们必须这样做。将 `fileName pathToDirectory` 复制到新的 `fileName pathToDirectory`：

```
cp pathToDirectory/fileName pathToTargetDirectory
```

要移动而不是复制文件，可以使用移动命令 `mv`，格式如下：

```
mv pathToDirectory/fileName pathToTargetDirectory
```

输出重定向对于许多目的。其中之一是从程序创建文件。输出重定向通过符号 `>` 实现，语法如下：

```
command options > fileName
```

例如，将 `pwd` 命令的文件内容写入文本文件 `temp.txt`。`cat` 命令的目的是连接文件。当与输出重定向序列配合使用时，例如：

```
cat temp.txt temp2txt temp.txt
```

创建一个新文件 `temp.txt`，由 `temp1.txt` 并在末尾追加 `temp2.txt`。

