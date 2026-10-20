

```
% alias
dir	ls -la
rename	mv
spr	lpr -Pspr
ls	ls -C
ll	ls -ltr
page	more
%
```

你可以使用 `unalias` 命令从别名列表中删除一个或多个别名。

在下面的 Bash 会话中，两个 `unalias` 命令中的第一个删除了 `ls` 的别名，第二个删除了别名列表中的所有别名。请注意，在执行 `unalias ls` 命令后，第一次 `alias` 命令的输出中不再包含 `ls` 命令的别名。使用第二个 `alias` 命令不会产生输出，因为 `unalias -a` 命令删除了别名列表中的所有别名。

```
$ unalias ls
$ alias
dir='ls -la'
rename='mv'
spr='lpr -Pspr'
ll='ls -ltr'
page='more'
$ unalias -a
$ alias
$
```

在下面的章节练习中，你将使用 `write`、`alias` 和 `unalias` 命令来练习它们的语法并更深入地了解其用途。你还将检查一个跟踪可以登录用户的系统文件。

# In-Chapter Exercises

- 25. 使用 `write` 命令与已登录到系统的朋友进行通信。
- 26. 使用 `alias` 命令显示 Linux 系统上命令的昵称（别名），如果有的话。如果没有，请为自己创建几个有用的别名，根据你可能经常且有益地作为别名命令使用的情况。然后，使用 `unalias` 删除其中一个或多个别名。使用 `unalias -a` 删除所有别名。在你取消了所有默认或定义的别名之后，如何重新启用它们？
- 27. 显示系统上 `/etc/passwd` 文件的内容，以确定有多少用户可以登录到系统。此文件的内容对你的用户名显示了什么？

表 2.3 显示了一些初学者有用的命令。

## 2.7 Introduction to Linux Shells

当你登录并使用控制台窗口或终端进入 CUI 时，Linux 系统会启动一个充当你与 Linux 内核之间接口的程序。此程序称为 Linux shell，它执行你在键盘上输入的命令。当 shell 开始运行时，它会给你一个提示并等待你的命令。当你输入命令并按 <Enter> 时，shell 会解释你的命令并执行它。如果输入不存在的命令，shell 会告诉你，然后重新显示提示并等待你输入下一个命令。由于 shell 的主要目的是解释你的命令，因此它也被称为 Linux 命令行解释器。

# TABLE 2.3

| Command | What It Does |
|---|---|
| `<Ctrl+D>` | Terminates a process or command |
| `alias` | Allows you to create pseudonyms for commands |
| `biff` | Notifies you of new e-mail |
| `cal` | Displays a calendar on screen |
| `cat` | Allows joining of files |
| `cd` | Allows you to change the current working directory |
| `cp` | Allows you to copy files |
| `exit` | Ends a shell that you have started |
| `hostname` | Displays the name of the host computer that you are logged on to |
| `login` | Allows you to log on to the computer with a valid username/password pair |
| `lpr or lp` | Allows printing of text files |
| `ls` | Allows you to display the names of files and directories in the current working directory |
| `man` | Allows you to view a manual page for a command or topic |
| `mesg` | Allows or disallows writing messages to the screen |
| `mkdir` | Allows you to create a new directory |
| `more` | Allows you to view the contents of a file one screen at a time |
| `mv` | Allows you to move the path location of, or rename, files |
| `passwd` | Allows you to change your password on the computer |
| `pg` | Displays one screen of a file at a time |
| `pwd` | Allows you to see the name of the current working directory |
| `rm` | Allows you to delete a file from the file structure |
| `rmdir` | Allows you to delete directories |
| `talk` | Allows you to send real-time messages to other users |
| `telnet` | Allows you to log on to a computer on a network or the Internet |
| `unalias` | Allows you to undefine pseudonyms for commands |
| `uname` | Displays information about the operating system running the computer |
| `whatis` | Allows you to view a brief description of a command |
| `whereis` | Displays the path(s) to commands and utilities in certain key directories |
| `who` | Allows you to find out login names of users currently on the system |
| `whoami` | Displays your username |
| `write` | Allows real-time messaging between users on the system |

shell 命令可以是内部/内置的或外部的。执行内部命令的代码是 shell 进程的一部分，但执行外部命令的代码驻留在文件系统中，以二进制可执行程序文件或 shell 脚本的形式存在。（我们在第 10 章详细描述了 shell 如何执行命令。）

由于 shell 执行从键盘输入的命令，因此当它发现无法再从键盘读取任何内容时就会终止。你可以通过在新行开头按 <Ctrl+D> 来通知你的 shell。只要 shell 收到 <Ctrl+D>，如果你在纯文本控制台上登录，它就会终止并注销你。系统随后会再次显示 login: 提示，告知你需要再次登录才能使用它。如果你使用的是桌面环境，例如 Linux Mint Cinnamon 桌面，并且在桌面上打开了终端或控制台窗口，按下 <Ctrl+D> 的效果是关闭终端或控制台窗口。

shell 解释根据第 2.2 节结构化的单个 Linux 命令——即假设命令行中的第一个词是你想要执行的命令的名称。它假设从连字符（−）开始的任何剩余字符都是选项（可能后跟选项参数），其余的是命令参数。

在读取你的命令行后，shell 会确定命令是内部命令还是外部命令。它通过使用 shell 自身代码中的相应代码段来处理所有内部命令。要执行外部命令，它会在文件系统结构中搜索多个目录（参见第 4 章），查找具有命令名称的文件。然后它假设该文件包含要执行的代码并运行该代码。

shell 搜索以查找对应于外部命令的文件的目录名称存储在名为 PATH（或 C shell 中的 path）的 shell 变量中。Bourne、Korn 和 Bash shell 中目录名称由冒号分隔，而 C shell 中由空格分隔。PATH 变量中存储的目录名称构成了 shell 的搜索路径。你可以使用 Bourne、Korn、Bash 和 C shell 中的 `echo $PATH` 命令查看你的变量的搜索路径。

以下是我们在 Linux Mint 系统的终端窗口上使用此命令运行的两个示例会话。第一个在 Bash shell 中完成，第二个在 C shell 中完成。请注意，在我们的 Linux 系统的默认 Bash shell 中，搜索路径包含由冒号分隔的目录名称，而在 C shell 中目录名称由空格分隔。

```
```text
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:
/sbin:/bin:/usr/games:/usr/local/games
$

% echo $path
/usr/local/sbin /usr/local/bin /usr/sbin /usr/bin
/sbin /bin /usr/games /usr/local/games
%
```
```

PATH（或 path）变量定义在名为 **.profile** 或 **.login** 的隐藏文件（也称为点文件）中。如果你在这些文件中找不到此变量，它就在你使用的 shell 特定的启动文件（也是一个点文件）中。你可以通过更改此变量的值来更改 shell 的搜索路径。要仅临时更改当前会话的搜索路径，你可以在命令行更改 PATH 的值。要永久更改，你需要在相应的点文件中更改此变量的值。

在下面的 Bash shell 示例中，搜索路径增加了两个目录，**~/bin** 和 **.**（当前目录）。而且搜索从 **~/bin** 开始，以当前目录结束。

在编辑或更改 PATH 变量时要小心，以免丢失系统管理员为系统所有用户设置的默认搜索路径的任何组件。

```
```text
$ PATH=~/bin:$PATH:.
$
```
```

你可以使用第 2.8.3 节中描述的 `echo $SHELL` 命令确定你的登录 shell。每个 shell 在与其关联的隐藏文件中设置了几个其他环境变量。我们在第 2.8.4 节中描述这些文件，并在第 4 章中对 Linux 文件进行详细讨论。

# In-Chapter Exercise

- 28. 什么命令会在你的 Linux 系统上将你主目录中仅有的点文件名称打印到标准输出？这些点文件的名称是什么？每个点文件实现了什么？列出它们，并在列表中每个条目旁边用你自己的话写下该点文件实现的功能的简短描述。

## 2.8 Various Linux Shells

我们所有的代表性 Linux 系统都预装了 Bash shell，并且 Bash 是默认 shell。C、Bourne、Korn、TENEX C（TC）和 Z shell 不那么流行。但它们可以被安装

