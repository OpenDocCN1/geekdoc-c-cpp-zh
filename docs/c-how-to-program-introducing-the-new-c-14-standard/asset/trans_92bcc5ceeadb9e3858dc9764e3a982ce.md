
### 步骤 8：输入更多猜测

继续通过输入值来玩游戏（**图 1.19**），直到你猜中正确数字。当你猜中时，应用程序显示 `"Excellent! You guessed the number."`

### 步骤 9：再次玩游戏或退出应用程序

在你猜中正确数字后，应用程序会询问你是否想再玩一局。在 `"Would you like to play again (y or n)?"` 提示符处，输入单个字符 `y` 会使应用程序选择一个新数字，并显示消息 `"Please type your first guess."`，随后是一个问号提示符，以便你在新游戏中做出第一次猜测。输入字符 `n` 会终止应用程序。每次你从头开始执行此应用程序（*步骤 5*）时，它都会选择相同的数字供你猜测。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_157_0.png)

**图 1.19** 输入更多猜测并猜中正确数字。

## 1.10.2 在 Linux 上使用 GNU C++ 编译和运行

对于本次试运行，我们假设你已阅读“开始之前”部分，并且已将下载的示例放在 Linux 系统的主目录中。如果你对将文件复制到主目录有任何疑问，请咨询你的讲师。在本节的图中，我们使用**粗体**文本突出显示你输入的文本。我们系统上 shell 中的提示符使用波浪号（`~`）字符表示主目录，每个提示符以美元符号（`$`）字符结尾。提示符会因 Linux 系统而异。

### 步骤 1：定位完整应用程序

在 Linux shell 中，使用 `cd` 命令切换到完整应用程序目录（**图 1.20**），方法是输入

```bash
cd examples/ch01
```

然后按 *回车*。

```bash
~$ cd examples/ch01
~/examples/ch01$
```

**图 1.20 切换到 `GuessNumber` 应用程序的目录。**

### 步骤 2：编译应用程序

在运行应用程序之前，必须先编译它（**图 1.21**），方法是输入

```bash
g++ -std=c++14 GuessNumber.cpp -o GuessNumber
```

此命令为 C++14（当前 C++ 版本）编译应用程序，并生成一个名为 `GuessNumber` 的可执行文件。

```bash
~/examples/ch01$ g++ -std=c++14 GuessNumber.cpp -o GuessNumber
~/examples/ch01$
```

**图 1.21 使用 `g++` 命令编译 GuessNumber 应用程序。**

### 步骤 3：运行应用程序

要运行可执行文件 `GuessNumber`，请在下一个提示符处输入 `./GuessNumber`，然后按 *回车*（图 1.22）。`./` 告诉 Linux 从当前目录运行，并且是表明 `GuessNumber` 是可执行文件所必需的。

```text
~/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
?
```

**图 1.22 运行 GuessNumber 应用程序。**

### 步骤 4：输入第一次猜测

应用程序显示 `"Please type your first guess."`，然后在下一行显示问号（`?`）作为提示符（图 1.22）。在提示符处，输入 `500`（图 1.23）。[注意，输出可能因你使用的编译器而异。]

```text
~/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
? 500
Too high. Try again.
?
```

**图 1.23 输入初始猜测。**

### 步骤 5：输入另一次猜测

应用程序显示 `"Too high. Try again."`，这意味着你输入的值大于应用程序选作正确猜测的数字（图 1.23）。在下一个提示符处，输入 `250`（图 1.24）。这次应用程序显示 `"Too low. Try again."`，因为你输入的值小于正确猜测。

```text
~/examples/ch01$ ./GuessNumber
I have a number between 1 and 1000.
Can you guess my number?
Please type your first guess.
? 500
Too high. Try again.
? 250
Too low. Try again.
?
```

**图 1.24 输入第二次猜测并接收反馈。**

### 步骤 6：输入更多猜测

继续通过输入值来玩游戏（图 1.25），直到你猜中正确数字。当你猜中时，应用程序显示 `"Excellent! You guessed the number."`

```text
Too low. Try again.
? 375
Too low. Try again.
? 437
Too high. Try again.
? 406
Too high. Try again.
? 391
Too high. Try again.
? 383
Too low. Try again.
? 387
Too high. Try again.
? 385
Too high. Try again.
? 384
Excellent! You guessed the number.
Would you like to play again (y or n)?
```

**图 1.25 输入更多猜测并猜中正确数字。**

### 步骤 7：再次玩游戏或退出应用程序

在你猜中正确数字后，应用程序会询问你是否想再玩一局。在 `"Would you like to play again (y or n)?"` 提示符处，输入单个字符 `y` 会使应用程序选择一个新数字，并显示消息 `"Please type your first guess."`，随后是一个问号提示符，以便你在新游戏中做出第一次猜测。输入字符 `n` 会结束应用程序，返回到 shell 并等待你的下一条命令。每次你从头开始执行此应用程序（即 *步骤 3*）时，它都会选择相同的数字供你猜测。

## 1.10.3 在 Mac OS X 上使用 Xcode 编译和运行

在本节中，我们介绍如何在 Mac OS X 上使用 Apple 的 Xcode IDE 运行 C++ 程序。

### 步骤 1：检查你的设置

阅读本书的“开始之前”部分很重要，以确保你已正确安装 Apple 的 Xcode IDE 并将本书的示例复制到硬盘。

### 步骤 2：启动 Xcode

打开 Finder 窗口，选择**应用程序**，然后双击 Xcode 图标（🖥️）。如果这是你第一次运行 Xcode，将出现**欢迎使用 Xcode**窗口（**图 1.26**）。暂时关闭此窗口——你可以随时通过选择**窗口 > 欢迎使用 Xcode**来访问它。我们使用 > 字符表示从菜单中选择一个菜单项。例如，**文件 > 打开…**表示你应该从**文件**菜单中选择**打开…**菜单项。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_165_0.png)

**图 1.26 欢迎使用 Xcode 窗口。**

### 步骤 3：创建项目

一个**项目**是一组相关文件，例如组成一个应用程序的 C++ 源代码文件。我们为本书示例创建的 Xcode 项目是**OS X 命令行工具**项目，你将直接在 IDE 中执行它们。要创建项目：

- 1. 选择**文件 > 新建 > 项目...**
- 2. 在 OS X 子类别**应用程序**中，选择**命令行工具**并点击**下一步**。
- 3. 在**产品名称**字段中为你的项目提供名称——我们指定了 `Guess Number`。
- 4. 确保所选**语言**为 **C++**，然后点击**下一步**。
- 5. 指定要存储项目的位置，然后点击**创建**。
- （有关配置项目以使用 C++14 的信息，请参阅“开始之前”部分。）

**图 1.27** 显示了创建项目后出现的**工作区窗口**。默认情况下，Xcode 会创建一个 `main.cpp` 源代码文件，其中包含一个显示 `"Hello, world!"` 的简单程序。窗口在工具栏下方分为四个主要区域：最初显示的是**导航器区域**、**编辑器区域**和**实用工具区域**。我们稍后将解释如何显示**调试区域**，你将在其中运行程序并与程序交互。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_166_0.png)

**图 1.27** 选中 `main.cpp` 的示例 Xcode C++ 项目。

工作区窗口的左侧是**导航器区域**，其顶部有图标，用于显示可在此处显示的*导航器*。对于本书，你主要会使用

- **项目**（🗂️）——显示项目中的所有文件和文件夹。
- **问题**（⚠️）——显示编译器生成的警告和错误。

你通过点击窗口**导航器**区域上方的相应按钮来选择要显示哪个导航器。

**导航器**区域的右侧是用于编辑源代码的**编辑器**区域。此区域始终显示在工作区窗口中。当你在**项目**导航器中选择一个文件时，文件内容会显示在**编辑器**区域中。工作区窗口的右侧是**实用工具**区域，本书中你不会使用它。**调试**区域在显示时出现在**编辑器**区域下方。

工具栏包含用于执行程序的选项（**图 1.28(a)**）、用于显示 Xcode 中执行任务进度（例如编译状态）的显示区域（**图 1.28(b)**），以及用于隐藏和显示工作区窗口中各区域的按钮（**图 1.28(c)**）。
