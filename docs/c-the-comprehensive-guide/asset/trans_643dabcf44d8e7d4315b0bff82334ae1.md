
![](img/74416a2c3cfc2d60ea17cab4deeb9a13_40_0.png)

**图2.2** 用于 C++ 开发的 Microsoft 产品。

在 Mac 上，Apple 提供的 Xcode 是事实上的标准。这让你可以在一个优秀的 IDE 和一套命令行工具之间进行选择。你可以从 Apple 网站下载这些工具（https://developer.apple.com/xcode/）。目前你可以获得 Xcode 15，其编译器版本为 15。不带 IDE 的编译器也可以用于 Linux，最新版本 18 可用（https://releases.llvm.org/）。

GCC 可以作为 Unix、Windows 和 Mac 上的另一种选择。这个 C++ 编译器叫作 *g++*——目前版本为 14.1。你主要在命令行中使用它，但它也集成到 Eclipse CDT、NetBeans、KDevelop、Code::Blocks、Qt Creator 等 IDE 中。其中一些工具甚至支持多个平台。如果你想在 Windows 上使用 g++ 进行开发，请寻找 MinGW 集成，并确认是需要单独下载还是已经包含在内（*Minimalist GNU for Windows*）。

## Windows 下的 Linux 子系统

在 Windows 下，有一个可选的 *适用于 Linux 的 Windows 子系统*（WSL）。在那里你可以启动 bash shell，并获得与 Ubuntu 等系统下相同的命令——包括 `apt-get` 安装命令。然后你就可以在 Windows 下安装 GCC 以及其他许多东西。

一个完全商业化但有趣的解决方案是 JetBrains 的 *CLion*。这个 IDE 设计得非常周到，基于成功的 IntelliJ IDEA，这使它吸引了一些 Java 开发者。它自带的编译器在标准支持方面略有落后，但你可以配置已安装的 GCC 或 Clang 编译器。

## 2.5 Ubuntu 下的命令行

作为命令行开发的一个示例，我将为你提供 Ubuntu 当前长期支持版本的快速指南。Ubuntu 是一个广泛使用的 Linux 发行版。如果你使用的是其他 Linux 发行版，命令可能会有所不同。

你可以这样安装 g++ 和一些有用的工具：

```bash
sudo apt-get install g++ make
```

你在编辑器中输入程序代码，而真正的选择困难就从这里开始。如果你使用 IDE，编辑器已经包含在内。如果没有 IDE，你可以在任何普通文本编辑器中输入程序。文本编辑器比比皆是。

我只建议两个满足不同需求的编辑器：*gedit* 和 *kate*。在 gedit 和 kate 之间做出选择，应该取决于你的桌面环境是 Gnome 还是 KDE。只需试试下面两条命令中哪一条会自动安装更少的软件包，然后选择对应的编辑器即可：

```bash
sudo apt-get install gedit
sudo apt-get install kate
```

在纯文本编辑器和功能全面的 IDE 之间，还有微软的 *Visual Studio Code* 和 JetBrains 的 *Fleet* 这两个新产品，后者目前仍处于预览阶段。两者都能在所有平台上运行，而且非常受欢迎。

如果你加入一个有多名开发者的团队，请了解他们是否会使用 *Emacs* 或 *Vim*。这些是程序员中非常流行的文本编辑器，但学习曲线较为陡峭。如果你有同事能帮助你入门，可以随意选择这两个编辑器之一：

```bash
sudo apt-get install emacs
sudo apt-get install vim
```

### 2.5.1 创建一个程序

稍后当我们以 Windows 下的 Visual Studio Code 为例进行讨论时，就会讲到 IDE。现在，我们先走一遍流程。

打开命令行，有时也称为 *终端* 或 *控制台*。你肯定能在菜单中找到它的入口。在带有 Gnome 的 Ubuntu 中，你还可以按 `Ctrl`+`Alt`+`T`。一个新窗口应该会打开，其中有一个闪烁的光标，显示类似这样的命令行，也就是所谓的提示符：

```bash
towi@havaloc:~$
```

在本书的其余部分，我不会再提及 `towi@havaloc:`（它代表用户名和计算机名），也不会提及表示当前工作目录的波浪号 `~`。提示符 `$` 表示你应该在其后输入命令。练习创建一个新目录并进入该目录：

```bash
~$ mkdir quellcode
~$ cd quellcode
```

你的提示符现在应该包含你已进入的目录：

```bash
~/quellcode$
```

由于 Linux 发行版众多，即使你一切操作正确，显示结果也可能有所不同。你可以使用 `pwd` 来检查你当前所在的目录。

现在打开你选择的编辑器。你可以通过菜单打开，也可以在命令行中输入要编辑的文件名。在命令末尾添加一个和号 `&`，这样即使编辑器已打开，你也能继续输入（如果你忘记这样做，请在命令行中按 `Ctrl`+`Z`，然后输入命令 `bg`，再按 `Enter`）。我自己是 Emacs 用户，但你可以在这里使用你喜欢的编辑器：

```bash
$ emacs modern101.cpp &
```

在编辑器窗口中输入以下源代码。你应该能在某个地方看出你确实在编辑 `modern101.cpp`。

```cpp
// https://godbolt.org/z/911fxx3nq
// modern101.cpp: Fibonacci console
#include <iostream>

int fib(int n) {
    return n<=1 ? n : fib(n-2) + fib(n-1);
}

int main() {
    std::cout << "Which Fibonacci number?";
    int n = 0;
    std::cin >> n;
    std::cout << "fib(" << n << ")=" << fib(n) << "\n";
}
```

**清单2.1** 每个斐波那契数都是其前两个数之和。

将该源代码编译为可执行程序 `modern101.x`：

```bash
$ g++ modern101.cpp -o modern101.x
```

这里的 g++ 就是编译器。用 `modern101.cpp` 指定源文件。如果你有多个源文件要编译成一个程序，就在这里列出多个 `.cpp` 文件。用 `-o modern101.x` 告诉编译器所需的输出文件名。如果忘记这个选项也没关系；编译好的程序最终会以 `a.out` 命名。

自己试一试：

```bash
$ ./modern101.x
Which Fibonacci number? 33
fib(33)=3524578
```

这是你的第一个 C++ 程序。恭喜！

顺便说一句：在 Windows 下，可执行程序通常带有 `*.exe` 扩展名。在 Linux 下，可执行的 C++ 程序带扩展名则相当不寻常。为了说明这一点，我在这里创建 Linux 程序时使用了 `*.x` 扩展名——这也是我在“现实世界”中偶尔会采用的做法。你是否效仿我的示例，完全由你决定。

如果你对如何加速该程序感兴趣，可以跳到第 2.7 节。

### 2.5.2 使用 Makefile 实现自动化

然而，以这种方式反复调用编译器很繁琐，因此最好创建一个 Makefile，在其中列出必要的命令。为此，请创建以下 Makefile 文件：

```bash
$ emacs Makefile &
```

文件内容很简单：

```makefile
# -*- Makefile -*-
all: modern101.x
modern101.x: modern101.cpp
[Tab] g++ modern101.cpp -o modern101.x
# clean up:
clean:
[Tab] rm -f *.x *.o
```

带有 # 的注释行并不关键。请确保缩进的行不是以空格开头，而是以 *制表符* 开头，我用 [Tab] 来表示它。这里我不打算深入所有细节，但下面两行，

```makefile
modern101.x: modern101.cpp
[Tab] g++ modern101.cpp -o modern101.x
```

是在告诉 make：“如果你需要创建 modern101.x，那么你需要 modern101.cpp；要创建它，请运行命令 g++ modern101.cpp -o modern101.x”。

如果你现在运行

```bash
$ make
```

那么 `all:` 规则会查找你想要构建的内容。你可以在其中列出其他规则，make 将依次执行它们。现在你应该已经重新构建了你的程序。make 可能会注意到没有任何更改，这种情况下，`make clean`（执行清理规则）或 `make -B`（假装所有内容都已更改）会有所帮助。

你也可以使用 `make all`、`make modern101.x` 或 `make clean` 来执行其他规则。是不是很方便？

## 2.6 Windows 下的 Visual Studio Code IDE

要安装 Visual Studio Code（VS Code），只需在浏览器的搜索栏中输入“vscode download”，然后点击出现的下载链接。接着下载安装程序并运行它。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_44_0.png)

**图2.3** Visual Studio Code 可用于主流操作系统。

