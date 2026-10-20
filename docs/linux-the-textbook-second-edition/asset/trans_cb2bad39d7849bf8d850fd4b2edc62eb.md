

Debian 系列系统使用 apt 包管理工具，而 RHEL 系列的 CentOS 使用 YUM。这些其他 shell 在特定应用和使用 Linux 系统的工作方式上具有优势。当你使用非图形化、基于文本的 CLI 登录 Linux 系统时，一种特定类型的 shell 会开始执行。这个 shell 被称为你的 *登录 shell*，它通常由你的 Linux 系统管理员决定。如果你想使用不同的 shell，你可以先使用相应的包管理系统安装该 shell 程序，然后运行系统上可用的相应命令来执行该 shell 程序。

例如，如果你的登录 shell 默认是 Bash，但你想使用 C shell，你可以先通过 apt-get 命令在 Debian 系列 Linux 系统上安装 C shell，如以下示例所示，然后使用 csh 命令。

```shell
$ sudo apt-get install csh
Output truncated…
$ csh
%
```

### 2.8.1 Shell 程序

本质上，shell 程序本身是用 C 编程语言实现的，允许你进行解释型编程（相对于编译型编程）。它通过两种方式实现这一点。第一，你可以使用简单、单一的，或复杂、多个的 Linux 命令，通过重定向操作符和/或诸如 sed、awk 或 grep 等实用工具连接起来，以完成常见任务。第二，通过用户编写的脚本文件，使用 shell 解释型语言编码，自动化和简化那些常见的、可能高度重复的任务。这种解释型语言具备其他任何结构化高级编程/脚本语言（如 Perl、Tcl 或 Python）的所有特性。shell 语言只是没有这些常见脚本语言那么复杂。这一事实应该告诉你为什么会有这么多不同的 shell，就像有这么多不同的高级编程和脚本语言一样。

编程语言往往会随着用户的需求而随时间演变和发展，shell 程序就是这种演变的典型代表。表 2.4 列出了最常见的 shell、其位置以及这些 shell 的程序名称。

**表 2.4** *Shell 位置和程序名称*

| Shell | 大多数 Linux 系统上的默认位置（如果该 shell 已安装！） | Shell 程序（命令）名称 |
|---|---|---|
| rc | /bin/rc | rc |
| Bourne shell | /bin/sh | sh |
| C shell | /bin/csh | csh |
| Bourne again shell (Bash) | /bin/bash | bash |
| Z shell | /bin/zsh | zsh |
| Korn shell | /bin/ksh | ksh |
| TC shell | /bin/tcsh | tcsh |

表 2.4 中显示的位置对于大多数 Linux 系统来说是典型的。如果你在系统上找不到 shell 所示的位置，或者无法使用 `whereis` 命令（如第 2.5.1 节所示），请咨询你的讲师或系统管理员。

![](img/2a18e06cd9c6395e451f26126ecba1fd_76_0.png)

*图 2.4 各种 Linux shell 的开发层次结构。*

图 2.4 追溯了各个 shell 家族的发展，并表明了每个家族在层级中出现时功能逐渐增强的趋势。Bourne shell（sh）是主要 shell 家族的*祖母*，功能水平几乎最低。层级顶部附近是 Korn shell（ksh），它包含 Bourne shell 的所有功能，并且更多。rc 和 zsh shell 是例外，不能轻易与任何主要 shell 家族关联。

### 2.8.2 哪种 Shell 适合你的需求？

大多数 shell 执行类似的功能，了解它们如何执行这些功能的细节对于决定在特定任务中使用哪种 shell 很重要。此外，在一个会话期间使用多个 shell 是一种常见做法，尤其在 shell 脚本文件程序员中。例如，你可能会使用 Bourne 或 Korn shell 进行编程，并使用 C shell 执行单个命令。我们将在第 2.8.3 节进一步讨论这个示例。主要 shell 功能的相似性总结在表 2.5 中。

### 2.8.3 更换 Shell 的方法

当你首次登录计算机系统时，只需在命令行输入 `echo $SHELL`，即可轻松确定你的默认 shell。

问题是：为什么要更改默认 shell，或者就此而言，甚至使用额外的 shell？答案是，你想要另一个 shell 更强大，或在某种意义上性质不同的功能。

例如，你的默认 shell 可能是 Bash shell（bash）。你的一个朋友向你提供了一个简洁有用的 Z shell 脚本，该脚本允许你利用 Z shell 脚本编程能力，这个脚本在 Bash shell 下运行是行不通的。你可以通过在运行默认 Bash shell 的同时运行 Z shell 来使用这个脚本。因为 Linux 是一个多进程操作系统，所以可以同时激活多个命令行解释器。这并不意味着单条命令会被多次解释；它只是意味着输入、输出和错误被“挂钩”到当前控制它们的任何 shell 进程上。[有关进程和 shell 命令输入/输出（I/O）的更多信息，请参见第 10 章。]

**表 2.5** *Shell 相似之处*

| 功能 | 描述 |
|---|---|
| 执行 | 执行程序和命令的能力 |
| I/O 处理 | 控制程序和命令的输入与输出 |
| 编程 | 执行程序和命令序列的能力 |

你可以通过以下两种方式之一更换 shell：

-   **方法 1.** 为系统上后续每次登录会话更改为新的默认 shell，以及
-   **方法 2.** 仅在当前登录会话期间，在默认 shell 之上或与之并发地创建额外的 shell 会话。

这两种方法的前提是，你希望更换到的 shell 在系统上可用。如果没有，你可以使用第 2.8 节中所示的 `apt` 命令进行安装。

**方法 1.** 要更改默认 shell，在以普通用户身份登录后，输入以下命令：

```shell
$ chsh
password for bob: www
Changing the login shell for bob
Enter the new value, or press ENTER for the default
    Login Shell [/bin/bash]: /bin/csh
$
```

如我们的 Linux Mint 系统所示，系统会提示你输入要更换到的 shell 名称。你输入要更换到的 shell 位置的完整路径——例如，输入 `/bin/sh` 更改为 Bourne shell。有关系统上常见 Linux shell 的完整路径，请参阅表 2.4。

如果此方法在你的系统上不起作用，请咨询你的讲师或系统管理员以获取更多帮助。

**方法 2.** 要在默认 shell 之上创建或运行额外的 shell，只需在命令行输入 shell 程序的名称（参见表 2.4），即可在你想要运行该 shell 时运行它。以下会话演示了如何使用此方法将使用 `$` 作为 shell 提示符的默认 Bash shell 更换为显示 `%` 作为 shell 提示符的 C shell。

```shell
$ echo $SHELL
/bin/bash
$ csh
%
```

第一个命令行允许你确定默认 shell。在这种情况下，系统会向你显示默认设置为 Bash shell。第二个命令行允许你运行 C shell。第四行显示你已经成功，因为默认的 C shell 提示符出现在你的显示器上。如果 C shell 在你的系统上不可用或无法访问，你将在第三行之后收到一条错误消息。如果你的搜索路径不包含 `/bin`，你必须在输入 `csh` 的位置输入 `/bin/csh`，或者将 `/bin` 包含在 shell 的搜索路径中，然后使用 `csh` 命令。

要终止或离开这个新的临时 shell 并返回默认登录 shell，请在空白行按住 `<Ctrl+D>`。如果这种终止新 shell 的方式不起作用，请在命令行输入 `exit`，然后按 `<Enter>`。这样，你就停止了新 shell 的运行，默认 shell 提示符会出现在你的显示器上。如果你在桌面上打开了控制台或终端窗口，输入 `exit` 也会关闭该控制台或终端窗口。

### 章内练习

-   29. 使用第 2.5.1 节中演示的 `whereis` 命令，验证表 2.4 中列出的各个 shell 的位置。所有这些 shell 在你的系统上都可用吗？如果你在表 2.4 所示的位置没有找到它们，它们位于何处？

