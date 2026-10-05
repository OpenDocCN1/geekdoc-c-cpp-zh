

# 操作系统特定需求

C++ 可以在任何操作系统上运行，但对于新手来说，收集所有必要的组件可能会让人困惑。以下是针对 C++ 的操作系统特定说明。

## LINUX

Linux 用户是幸运的，因为他们的操作系统已经内置了编译器和文本编辑器。任何文本编辑器都可以让你编写 C++ 代码，当以 .cpp 扩展名保存时，使用 g++ 进行进行编译。

![](img/588364e02a77f179099fae91a1713f0a_48_0.png)

## WINDOWS

我们之前提到过，优秀的 IDE 是微软的 Visual Studio。然而，更好的 IDE 和编译器是 Code::Blocks，它定期通过发布新版本保持更新。否则，Windows 用户可以在 Notepad++ 中输入代码，然后像下面所示使用 MinGW 进行编译。

![](img/588364e02a77f179099fae91a1713f0a_48_1.png)

## 树莓派

树莓派的操作系统基于 Linux。因此，你可以使用文本编辑器编写代码，然后像在其他 Linux 发行版中一样使用 g++ 进行编译。

![](img/588364e02a77f179099fae91a1713f0a_48_2.png)

## MAC

Mac 用户需要下载并安装 Xcode 才能能够原生编译他们的 C++ 代码。MacOS 的其他选项包括 NetBeans、Eclipse 或 Code::Blocks；注意：由于缺乏开发者，Mac 无法使用最新的 Code::Blocks。

![](img/588364e02a77f179099fae91a1713f0a_48_3.png)

# 如何在 Windows 中设置 C++

在进行 C++ 编程时，Windows 用户有大量的选择。有许多 IDE 和编译器可用，包括微软的 Visual Studio。然而，我们认为，开始学习的最佳 C++ IDE 是 Code::Blocks。

### Code::BLOCKS

Code:Blocks 是一个免费的 C++、C 和 Fortran IDE，功能丰富，并且可以通过插件轻松扩展。它易于使用，背后有一个编译器和活跃的社区支持。

- **步骤 1** 首先访问 Code:Blocks 网站：www.codeblocks.org/downloads。从那里，点击“Download the binary releases”链接进入 Windows 的最新可下载版本。
- **步骤 3** 找到文件后，点击行末尾的 Sourceforge.net 链接，弹出下载通知窗口；点击 Save File 保存下载，保存已下载的 CodeBlocks 安装程序并双击开始。按照屏幕上的指示开始安装。

![](img/588364e02a77f179099fae91a1713f0a_49_0.png)

- **步骤 2** 你可以看到有三个 Windows 版本可用。你需要下载版本号结尾为“codeblocks-20.03-19.mingw-setup.exe” 的一个。本文编写的时间是：Codeblocks-17.12-mingw-setup.exe。区别在于 mingw-setup 包含一个 C++ 编译器和调试器 (TDM-GCC)。
- **步骤 4** 一旦到达许可条款，就有安装选项供选择。你可以选择较小的安装，省略某些组件，但我们建议你默认选择 Full（完整）选项。

![](img/588364e02a77f179099fae91a1713f0a_49_1.png)

# 如何在 Windows 中设置 C++

- **步骤 5** 接下来为 Code::Blocks 文件选择安装位置。由你决定，除非你有特殊要求，否则使用默认即可。当你点击 Next 时，安装开始；如果完成后会弹出通知询问你现在是否启动 Code::Blocks，所以点是。
- **步骤 6** Code::Blocks 首次运行时，它会自动检测你可能在系统上安装的 C++ 编译器。如果你没有任何，点击第一个检测到的 GCC 编译器并点击 Default 将其设置为系统 C++ 编译器。准备好继续时点击 OK。

![](img/588364e02a77f179099fae91a1713f0a_50_2.png)

- **步骤 7** 在启动 Code::Blocks 之前，有必要解释一下为什么你需要最新的编译器。目前是 C++20。在等待 CodeBlocks 安装期间请稍候。
- **步骤 8** 当程序启动时会出现另一个消息，通知你 Code::Blocks 不是默认编译器。你有几个选项：选择全部以允许 Code::Blocks 处理 C++ 类型。再次，我们建议你选择最后一个选项以 Code::Blocks 关联文件类型。
- **步骤 9** 你可以看到 Xcode 已经为你完成了一个基础的 Hello World 程序。例如，在屏幕上输出“Hello World”。
- **步骤 10** 当你想运行代码时，点击运行。程序执行后，输出显示在底部。

