
### 步骤 5：输入另一个猜测

在下一个提示符处，如果你的系统说第一次猜测太低，输入 750 并按 *Enter*；否则，输入 250 并按 *Enter*。在本例中，我们输入了 250，应用程序显示“太高了。再试一次。”，因为该值大于正确猜测：

```text
~/Documents/examples/ch01 ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
? 500
Too high. Try again.
? 250
Too high. Try again.
?
```

### 步骤 6：输入更多猜测

继续输入值来玩游戏，直到你猜中正确数字。当你猜对时，应用程序会显示“太好了！你猜对了。”：

```text
? 125
Too high. Try again.
? 62
Too low. Try again.
? 93
Too low. Try again.
? 109
Too high. Try again.
? 101
Too low. Try again.
? 105
Too high. Try again.
? 103
Too high. Try again.
? 102

Excellent! You guessed the number!
Would you like to play again (y or n)?
```

### 步骤 7：再次玩游戏或退出应用程序

在猜中正确数字后（你应始终能够在 10 次或更少猜测内做到），应用程序会询问你是否想再玩一局。在“你想再玩一次吗（y 或 n）？”提示符处，输入 y 会使应用程序选择一个新数字并开始新游戏。输入 n 会终止应用程序并返回 shell。

## 1.11.3 在 GCC Docker 容器中使用 g++ 编译和运行

无论你的操作系统是什么，你都可以在系统上使用最新的 GNU C++ 编译器。实现这一点最方便的跨平台方法之一是使用 GNU 编译器集合（GCC）Docker 容器。本节假设你已经执行了前言之后的“开始之前”一节中描述的以下步骤：

- 1. 已安装 **Docker Desktop**（Windows 或 macOS）或 **Docker Engine**（Linux）。
- 2. 已安装 **GCC Docker 容器**。
- 3. 已将本书的示例放入你的用户账户的 `Documents/examples` 文件夹中。

### 执行 GNU 编译器集合（GCC）Docker 容器

打开命令提示符（Windows）、终端（macOS/Linux）或 shell（Linux），然后执行以下步骤来启动 GCC Docker 容器：

- 1. 使用 `cd` 导航到包含本书示例的 examples 文件夹。
- 2. Windows 用户：使用以下命令⁶⁸启动 GCC Docker 容器：

  ```bash
  docker run --rm -it -v "%CD%":/usr/src gcc:latest
  ```

- 3. macOS/Linux 用户：使用以下命令启动 GCC Docker 容器：

  ```bash
  docker run --rm -it -v "$(pwd)":/usr/src gcc:latest
  ```

在上述命令中：

- `--rm` 在你最终关闭容器时清理容器资源。
- `-it` 以交互模式运行容器，因此你可以输入命令来切换文件夹，并使用 GNU C++ 编译器编译和运行程序。
- `-v "%CD%":/usr/src`（Windows）或 `-v "$(pwd)":/usr/src`（macOS/Linux）将 Docker 容器的 `/usr/src` 文件夹映射到你执行 Docker run 命令时所在的本地计算机文件夹，使 Docker 容器能够访问本地文件夹中的文件。你将使用 `cd` 命令导航到 `/usr/src` 的子文件夹，以编译和运行本书的示例。
- `gcc:latest` 是容器名称。`:latest` 指定你要使用 gcc 容器的最新版本。⁶⁹

容器运行后，你将看到类似以下的提示符：

```text
root@67773f59d9ea:/#
```

该容器使用 Linux 操作系统。其提示符在 `:` 和 `#` 之间显示当前文件夹位置。

### 在 Docker 容器中切换到 ch01 文件夹

上面指定的 `docker run` 命令会将你的示例文件夹挂载到容器的 `/usr/src` 文件夹。在 Docker 容器中，使用 `cd` 命令切换到 `/usr/src` 的 ch01 子文件夹：

```text
root@01b4d47cadc6:/# cd /usr/src/ch01
root@01b4d47cadc6:/usr/src/ch01#
```

要在 Docker 容器中编译、运行 GuessNumber 应用程序并与之交互，请按照 1.11.1.2 节“在 Linux 上使用 GNU C++ 编译和运行”中的*步骤 2–7*进行操作。

### 终止 Docker 容器

你可以在容器的提示符处输入 *Ctrl + d* 来终止 Docker 容器。

## 1.11.4 在 Docker 容器中使用 clang++ 编译和运行

与 g++ 一样，无论你的操作系统是什么，你都可以在系统上使用最新的 LLVM/Clang C++⁷⁰（clang++）命令行编译器。目前，LLVM/Clang 团队没有官方 Docker 容器，但 https://hub.docker.com 上有许多可用的容器。本节假设你已经执行了前言之后的“开始之前”一节中描述的以下步骤：

- 1. 已安装 **Docker Desktop**（Windows 或 macOS）或 **Docker Engine**（Linux）。
- 2. 已安装 **teeks99/clang-ubuntu Docker 容器**。
- 3. 已将本书的示例放入你的用户账户的 `Documents/examples` 文件夹中。

### 执行 teeks99/clang-ubuntu Docker 容器

打开 **命令提示符**（Windows）、**终端**（macOS/Linux）或 **shell**（Linux），然后执行以下步骤来启动 **teeks99/clang-ubuntu** Docker 容器：

- 1. 使用 `cd` 导航到包含本书示例的 examples 文件夹。
- 2. Windows 用户：使用以下命令⁷¹启动 Docker 容器：

  ```bash
  docker run --rm -it -v "%CD%":/usr/src teeks99/clang-ubuntu:16
  ```

- 3. macOS/Linux 用户：使用以下命令启动 Docker 容器：

  ```bash
  docker run --rm -it -v "$(pwd)":/usr/src teeks99/clang-ubuntu:16
  ```

在上述命令中：

- `--rm` 在你最终关闭容器时清理容器的资源。
- `-it` 以交互模式运行容器，因此你可以输入命令来切换文件夹，并使用 clang++ 编译器编译和运行程序。
- `-v "%CD%":/usr/src`（Windows）或 `-v "$(pwd)":/usr/src`（macOS/Linux）将 Docker 容器的 `/usr/src` 文件夹映射到你执行 `docker run` 命令时所在的本地计算机文件夹，使 Docker 容器能够访问本地文件夹中的文件。你将使用 `cd` 命令导航到 `/usr/src` 的子文件夹，以编译和运行本书的示例。
- `teeks99/clang-ubuntu:16` 是容器名称。

容器运行后，你将看到类似以下的提示符：

```text
root@9753bace2e87:/#
```

该容器使用 Linux 操作系统。其提示符在 `:` 和 `#` 之间显示当前文件夹位置。

### 在 Docker 容器中切换到 ch01 文件夹

上面指定的 `docker run` 命令会将你的示例文件夹挂载到容器的 `/usr/src` 文件夹。在 Docker 容器中，使用 `cd` 命令切换到 `/usr/src` 的 ch01 子文件夹：

```text
root@9753bace2e87:/# cd /usr/src/ch01
root@9753bace2e87:/usr/src/ch01#
```

### 编译应用程序

在运行应用程序之前，你必须先编译它。此容器使用 clang++ 命令，如下所示：

```bash
clang++ -std=c++20 GuessNumber.cpp -o GuessNumber
```

其中：

- `-std=c++20` 选项表示我们正在使用 C++20。
- `-o` 选项指定用于运行程序的可执行文件（`GuessNumber`）的名称。如果未包含此选项，clang++ 会自动将可执行文件命名为 a.out。

### 运行应用程序

要在 Docker 容器中运行 GuessNumber 应用程序并与之交互，请按照 1.11.1.2 节“在 Linux 上使用 GNU C++ 编译和运行”中的*步骤 3–7*进行操作。

### 终止 Docker 容器

你可以在容器的提示符处输入 `Ctrl + d` 来终止 Docker 容器。

## 1.11.5 在 macOS 上使用 Xcode 编译和运行

在本节中，你将使用 Apple 的 Xcode IDE 在 macOS 上运行一个 C++ 程序。⁷² Xcode 使用某个版本的 LLVM/Clang C++ 编译器；在撰写本文时，该编译器缺少我们在本书中使用的若干重要 C++20 特性。请访问

```text
https://deitel.com/cpphtp11
```

获取有关使用 Xcode 运行本书第 4 章及更高章节示例的说明。

### 步骤 1：检查你的设置

如果你尚未这样做，请阅读 **开始之前** 一节，以安装 Xcode 并下载本书的代码示例。

### 步骤 2：启动 Xcode

在 Finder 的“前往”菜单中，选择“应用程序”，然后双击 Xcode 图标：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_95_0.png)

如果这是你第一次运行 Xcode，会出现 **欢迎使用 Xcode** 窗口。关闭此窗口——你可以通过选择 **窗口 > 欢迎使用 Xcode** 来访问它。我们使用 > 字符

68. 可能会出现一条通知，要求你允许 Docker 访问当前文件夹中的文件。你必须允许此操作；否则，你将无法在 Docker 中访问我们的源代码文件。
69. 如果你希望让 GCC 容器保持为最新版本，可以在运行容器之前执行命令 `docker pull gcc:latest`。
72. 在撰写本文时，Xcode 版本为 14.2。

