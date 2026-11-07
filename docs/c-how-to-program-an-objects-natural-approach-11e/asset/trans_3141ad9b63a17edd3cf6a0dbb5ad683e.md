

## 我们使用的编译器

请确保你安装了最新的 C++ 编译器。我们使用以下免费编译器测试了本书中的代码示例：

- 对于 Microsoft Windows，我们使用了 Microsoft Visual Studio Community 版，其中包含 Visual C++ 编译器和其它 Microsoft 开发工具。
- 对于 Linux，我们使用了 GNU C++ 编译器（g++）——它是 GNU 编译器套件（GCC）的一部分。通常，大多数 Linux 系统上会预装某个版本的 GNU C++。你可能需要将编译器更新到更新的版本。GNU C++ 也可以安装在 macOS 和 Windows 系统上。
- 对于 macOS，我们同时使用了 GNU C++ 编译器（g++）和 Apple Xcode<sup>2</sup> C++ 编译器，后者使用的是 LLVM Clang C++ 编译器（clang++）的一个版本。
- 你可以通过 Docker 容器在 Windows、macOS 和 Linux 上方便地运行最新版本的 GNU C++（g++）和 LLVM Clang C++（clang++）<sup>3</sup>。请参阅本“开始之前”章节中的“Docker 与 Docker 容器”一节。

**在撰写本文时，Apple Xcode 不支持我们在本书中使用的若干关键 C++20 特性，因此我们建议使用最新版本的 g++。当 Xcode 对 C++20 的支持发生变化时，我们会在以下网址发布更新：**

https://deitel.com/cpphtp11

本“开始之前”章节介绍了编译器和 Docker 的安装。第 1.11 节的测试驱动演示了如何使用这些编译器编译和运行 C++ 程序。

- 1. 撰写本文时使用的是 GNU C++（g++）13.1。
- 2. 撰写本文时使用的是 Xcode 14.3.1。
- 3. 撰写本文时使用的是 Clang C++（clang++）16。

### 在 Windows 上安装 Visual Studio Community 版

如果你是 Windows 用户，首先请确保你的系统满足 Microsoft Visual Studio Community 版的要求，请访问：

https://docs.microsoft.com/en-us/visualstudio/releases/2022/system-requirements

接下来，访问：

https://visualstudio.microsoft.com/downloads/

然后执行以下安装步骤：

- 1. 在 **Community** 下方点击 **免费下载**。
- 2. 根据你的网络浏览器，屏幕底部可能会弹出一个窗口，你可以在其中点击 **运行** 以启动安装过程。如果没有，请在下载完成后双击 **Downloads** 文件夹中的安装程序文件。
- 3. 在 **用户帐户控制** 对话框中，点击 **是** 以允许安装程序对系统进行更改。
- 4. 在 **Visual Studio 安装程序** 对话框中，点击 **继续** 以允许安装程序下载配置安装所需的组件。
- 5. 对于本书中的示例，请选择 **使用 C++ 的桌面开发** 选项，其中包含 Visual C++ 编译器和 C++ 标准库。
- 6. 点击 **安装**。安装过程可能需要相当长的时间。

### 在 macOS 上安装 Xcode

在 macOS 上，执行以下步骤安装 Xcode：

- 1. 点击 Apple 菜单并选择 **App Store...**，或者点击 Mac 屏幕底部 Dock 中的 App Store 图标。
- 2. 在 App Store 的 **搜索** 字段中，输入 Xcode。
- 3. 点击 **获取** 按钮安装 Xcode。

### 在 macOS 上安装 GNU C++（g++）13

在 macOS 上，执行以下步骤安装 GNU C++：

- 1. 在 Finder 的 **前往** 菜单中，选择 **实用工具**，然后双击 **终端** 打开一个 **终端**（命令行）窗口。
- 2. 输入 `brew` 并按 *Enter*（或 *return*）检查 brew 命令是否已安装。如果 macOS 无法识别该命令，请访问 https://brew.sh 并复制 Install Homebrew 下方的安装命令。将此命令粘贴到终端窗口中，然后按 *Enter*（或 *return*）。
- 3. 输入以下命令，然后按 *Enter*（或 *return*）安装包含 g++ 的 GNU 编译器套件（GCC）：

```
brew install gcc@13
```

### 在 Linux 上安装 GNU C++（g++）13

Linux 发行版众多，且通常使用不同的软件升级技术。请查阅你所使用的发行版的在线文档，了解如何将 GNU C++ 升级到最新版本。你也可以在以下网址为各种平台下载 GNU C++：

```
https://gcc.gnu.org/install/binaries.html
```

### Docker 与 Docker 容器

[Docker](https://www.docker.com/) 是一种将软件打包到[容器](https://www.docker.com/resources/what-container/)（也称为[镜像](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/)）中的工具，容器捆绑了跨平台执行该软件所需的全部内容，这对于安装和配置复杂的软件包尤其有用。对于许多此类软件包，都有免费的预置 Docker 容器（通常位于 https://hub.docker.com），你可以下载并在本地系统上执行。Docker 是快速上手新技术、尝试新编译器版本的绝佳方式。

#### 安装 Docker

要使用 Docker 容器，你必须先安装 Docker。Windows 和 macOS 用户应从以下网址下载并运行 **Docker Desktop** 安装程序：

```
https://www.docker.com/get-started
```

然后按照屏幕上的说明操作。同时，请在该网站上注册一个 **Docker Hub** 帐户，该帐户可让你访问 `https://hub.docker.com` 上的大量容器。Linux 用户应从以下网址安装 **Docker Engine**：

```
https://docs.docker.com/engine/install/
```

#### 获取 GNU 编译器套件 Docker 容器

GNU 团队在以下网址维护官方 Docker 容器：

```
https://hub.docker.com/_/gcc
```

Docker 安装并运行后，打开命令提示符⁴（Windows）、终端（macOS/Linux）或 shell（Linux），然后执行命令：

```
docker pull gcc:latest
```

Docker 会下载一个配置了 GNU 编译器套件（GCC）最新版本——撰写本文时为 13.1——的容器。在第 1.11 节的某个测试驱动中，我们将演示如何执行该容器并使用它编译和运行 C++ 程序。

#### 获取 LLVM Clang C++ Docker 容器

目前，LLVM Clang 团队不提供官方 Docker 容器，但 `https://hub.docker.com` 上有许多可用的容器。对于本书，我们使用了以下网址中的一个流行容器：

```
https://hub.docker.com/r/teeks99/clang-ubuntu
```

打开命令提示符（Windows）、终端（macOS/Linux）或 shell（Linux），然后执行命令：

```
docker pull teeks99/clang-ubuntu:16
```

Docker 会下载一个配置了 LLVM Clang 最新版本——撰写本文时为 16——的容器。在第 1.11 节的某个测试驱动中，我们将演示如何执行该容器并使用它编译和运行 C++ 程序。

## 获取 C++ 相关问题解答

在阅读本书时，如果你有问题，可以通过以下方式轻松联系我们：

```
deitel@deitel.com
```

以及

```
https://deitel.com/contact-us
```

我们会及时回复。

互联网上充斥着编程信息。对非程序员和程序员来说，一个非常宝贵的资源是网站：

```
https://stackoverflow.com
```

在该网站上，你可以：

- 搜索常见编程问题的答案，
- 搜索错误信息，了解它们的成因，
- 提出编程问题，从世界各地的程序员那里获得答案，
- 并深入了解有关编程的一般性见解。

如需进行 C++ 实时讨论，请查看 Slack 频道 cpplang：

```
https://cpplang-inviter.cppalliance.org
```

以及 Discord 服务器 #include<C++>：

```
https://www.includecpp.org/discord/
```

## 在线 C++ 文档

有关 C++ 标准库文档，请访问：

```
https://cppreference.com
```

另外，请务必查看 C++ FAQ：

```
https://isocpp.org/faq
```

## 静态代码分析工具

我们使用了以下静态代码分析器来检查代码示例是否遵循 C++ 核心指南、是否符合编码标准、是否使用现代 C++ 惯用法、是否存在潜在安全问题、常见错误、潜在性能问题、代码可读性等：

- **clang-tidy**——https://clang.llvm.org/extra/clang-tidy/
- **cppcheck**——https://cppcheck.sourceforge.io/
- **Microsoft 的 C++ 核心指南静态代码分析工具**，内置于 Visual Studio 的静态代码分析器中

你可以使用以下命令在 Linux 上安装 clang-tidy：

```
sudo apt-get update -y
sudo apt-get install -y clang-tidy
```

你可以按照 https://cppcheck.sourceforge.io/ 上的说明，为各种操作系统平台安装 cppcheck。

对于 Visual C++，一旦你在第 1.11 节的测试驱动中学会了如何创建项目，就可以按如下方式配置 Microsoft 的 C++ 核心指南静态代码分析工具：

- 1. 在**解决方案资源管理器**中右键单击项目名称，然后选择**属性**。
- 2. 在出现的对话框中，在左列选择**代码分析 > 常规**，然后在右列将**对生成启用代码分析**设置为**是**。
- 3. 接下来，在左列选择**代码分析 > Microsoft**。然后在右列中，你可以从下拉列表中选择部分分析规则。我们使用了**<选择多个规则集...>** 选项来选择所有以 **C++ Core Check** 开头的规则。点击**另存为...**，为自定义规则集命名，点击**保存**，然后点击**应用**。

