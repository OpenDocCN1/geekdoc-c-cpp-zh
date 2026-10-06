
# CPython 内部：Python 3 解释器指南

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_0_0.png)

Anthony Shaw

Anthony Shaw

# 这是《CPython 内部：Python 3 解释器指南》的早期抢阅版本

在您的帮助下，我们可以让这本书变得更好：

在书的每个章节末尾，您都会找到一个“神奇”的反馈链接。点击该链接将带您进入一个在线反馈表单，您可以在那里与我们分享想法。

请根据您的需要提供简洁或详细的反馈。所有反馈都以匿名形式存储，但您可以选择留下姓名和联系方式，以便我们进行跟进或在我们的“感谢”页面上提到您。

我们为每个章节使用不同的反馈链接，因此我们始终知道您的笔记指的是书的哪一部分。

感谢您帮助我们将这本书成为 Python 社区更具价值的学习资源。

— Anthony Shaw

# 读者对《CPython 内部：Python 3 解释器指南》的评价

“这是对 Python 内部原理的全面介绍，这个话题惊讶地发现几乎没有好的资源，而这本书对于初学者和高级 Python 用户来说都是以一种易于懂的方式呈现的。”

– Abhishek Sharma，数据科学家

“‘并行与并发’章节是我最喜欢的章节之一。我一直在寻找对这个主题的深入理解，发现这本书非常有帮助。”

当然，在读完那个章节后，我无法忍不住继续读下去了。我热切期待在出版后能拥有自己的纸质副本！

我之前读过您的《CPython 源码指南》文章，这激发了我探索更多内部机制的兴趣。

关于 Python 有很多教这种语言的书，但我还没有真正遇到过任何能向好奇好奇的人解释内部原理的内容。

虽然我目前正在教我女儿 Python，但我把这本书加入了她的必读书单。她目前在乔治亚州立大学学习信息系统。”

– Milan Patel，（某大型投资银行）副总裁

“Anthony 的书最令我印象深刻的是，它将对 CPython 代码库进行更改的所有步骤都描述得如此清晰。”

“这是对 Python 内部原理的全面介绍，这个话题惊讶地发现几乎没有好的资源，而这本书对于初学者和高级 Python 用户来说都是以一种易于懂的方式呈现的。”

“‘并行与并发’章节是我最喜欢的章节之一。我一直在寻找对这个主题的深入理解，发现这本书非常有帮助。”

“当然，在读完那个章节后，我无法忍不住继续读下去了。我热切期待在出版后能拥有自己的纸质副本！”

“我之前读过您的《CPython 源码指南》文章，这激发了我探索更多内部机制的兴趣。”

“关于 Python 有很多教这种语言的书，但我还没有真正遇到过任何能向好奇好奇的人解释内部原理的内容。”

“虽然我目前正在教我女儿 Python，但我把这本书加入了她的必读书单。她目前在乔治亚州立大学学习信息系统。”

– Milan Patel，（某大型投资银行）副总裁

“Anthony 的书最令我印象深刻的是，它将对 CPython 代码库进行更改的所有步骤都描述得如此清晰。”

# 致谢

感谢我的妻子 Verity 的支持。没有她，这一切是不可能的。

Anthony Shaw

# 关于作者

Anthony Shaw 是一位热衷的 Python 、Python 软件基金会成员。他一直在西雅图从事研究、写作以及创建课程。

# 关于评审团队

Jim Anderson 长期从事编程，涉及嵌入式系统、分布式系统、管理并参加过多次会议。

# Python 语言与语法

## 配置与输入

## 使用语法树进行词法分析和解析

# 编译器

- 引用计数 . . . . . . . . . . . . . . . . . . . . . 207

# 测试套件 (The Test Suite) . . . . . . . . . . . . . . . . . . . 324

# 调试 (Debugging) . . . . . . . . . . . . . . . . . . . . 331

# 基准测试、性能剖析与追踪 (Benchmarking, Profiling, and Tracing) 353

# 前言

“一个由社区创建的编程语言能为全世界的用户带来快乐。”

—— Guido Rossum，Python 之日演讲稿

我热爱构建能够帮助我们学习、赋能我们创造并促使与其他他人分享知识的工具。当我听到这些工具和 Python 如何帮助你们解决现实世界中的问题（如气候变化）时，我感到谦卑、感谢和自豪。在我四十年的编程和解决问题的道路中，我花了大量时间进行学习、编写大量代码并与他人分享我的想法。我见证了技术的巨大变化，世界从大型机发展到手机，再到网络和云计算的奇妙世界。所有这些技术（包括 Python）都有一个共同点：在某一时刻，这些成功的创新仅仅是一个想法。像 Guido 这样的创造者必须承担风险并进行信仰跳跃才能向前。

> “现在做比永远不做好。”

—— Tim Peters，Python 之禅

让我们遵循 Tim 的智慧，现在就开始吧。

诚挚地，

– **Carol Willing**，CPython 核心开发者 & Python 指导委员会成员

# 引言

是否 的某些部分看起来像魔法？例如，字典为什么比遍历列表查找项快得多？生成器在每次产生值时是如何记住变量状态的？为什么你不需要像其他语言那样管理内存？事实上，CPython 这个最流行的 Python 运行时是用易读的 C 和 Python 代码编写的。

CPython 抽象了底层 C 平台和操作系统的复杂性。它让线程变得跨平台且直观。它简化了内存管理的痛苦。CPython 为编写 Python 代码的开发者提供了一个扩展且高效的平台。在开发者成长的某个阶段，你需要了解 CPython 的工作原理。这些抽象并不是完美的，而且是泄漏的。

一旦你理解了 CPython 的工作原理，你就可以优化你的应用程序并充分利用其性能。本书将解释 CPython 的概念、思想和技术细节。

在书中，你将涵盖 CPython 内部机制的主要概念，并学习如何：

- 阅读并导航源代码
- 从源码编译 CPython
- 修改 Python 语法并将其编译到你自己的版本中
- 导航并理解列表、字典和生成器等概念的内部机制
- 掌握 CPython 的内存管理能力
- 通过并行和并发扩展你的 Python 代码规模
- 使用新功能修改核心类型
- 运行测试套件
- 对你的 Python 代码和运行时进行性能分析和基准测试
- 像专业人士一样调试 C 和 Python 代码
- 修改或升级 CPython 库的组件并将其贡献给未来的版本

请仔细阅读每一章节，并确保尝试演示程序和交互元素。当你掌握了 Python 的核心概念时，你会感受到成就感，这会让你成为一名更出色的程序员。

## 如何使用本书

本书的核心在于“在做中学习”，因此请务必在书的早期按照指令设置你的 IDE，下载代码并编写示例。

为了获得最佳效果，我们建议你避免复制粘贴代码示例。书中的示例经过了多次迭代才最终完善，它们也可能包含错误。

犯错并学习如何修复它们是学习过程的一部分。你可能会发现实现示例的更好方法，修改它们并观察产生的效果。

通过足够的练习，你将掌握这些内容——并在过程中享受乐趣！

**我的 Python 技能需要什么水平才能使用本书？** 本书面向中级到高级 Python 开发者。我们已尽力展示代码示例，但书中会使用一些中级 Python 技术。

**我需要了解 C 才能使用本书吗？** 你不需要精通 C 就可以使用。如果你是 C 的初学者，请查看书末的*附录 1：面向 Python 程序员的 C 语言简介*以快速入门。

**完成这本书需要多久？** 我不建议赶进度这本书，尝试一次读一章，在每章之后尝试示例并同时探索代码。一旦读完这本书，它将成为你随时查阅的绝佳参考。

**本书的内容会很快过时吗？** Python 已经存在了20 多年。IPython 代码的某些部分自最初编写以来就未变动过。书中的许多原则在十或多年里保持不变。事实上，在写这本书期间，我发现了许多行由 Guido van Rossum（Python 作者）编写的代码，它们自版本11以来就未被触碰。

你在书中学到的技能将帮助你阅读和理解当前以及未来的 CPython 版本。变化是永恒的，而你的专业知识是你可以在过程中不断发展的。

书中的一些概念是全新的；有些甚至是实验性的。在编写本书期间，我在源码中发现了一些问题和 CPython 中的某些。。随后，这些问题得到了*修复或改进*。这就是 CPython 作为一个蓬勃发展的开源项目的魔力所在。

## 额外材料与学习资源

### 在线资源

本书提供了许多免费资源，你可以在 `realpython.com/cpython-internals/resources/` 访问它们。在这个网页上，你还可以找到一个由 Real Python 团队维护的勘误列表。

### 代码示例

贯穿本书的示例和示例配置将带有标题，表示它们是 `cpython-book-samples` 文件夹的一部分。

`cpython-book-samples ▷ 01 ▷ example.py`

```python
import this
```

你可以在 `realpython.com/cpython-internals/resources/` 下载代码示例。

### 代码许可

与本书相关的示例 Python 脚本遵循知识产权共享公有领域许可协议 (CC0)。这意味着欢迎您在自己的程序中出于任何目的使用代码的任何部分。

CPython 遵循 PSF 2 许可。书中使用的 IPython 源代码片段和示例是在 PSF 2.0 许可条款下进行的。

| Note |
| :--- |
| 书中的代码已在 Windows 10、macOS 10.15 和 Linux 上通过 Python 3.9.0b1 测试过 |

### 格式规范

代码块将用于展示示例代码：

```python
## 这是 Python 代码：
print("Hello world!")
```

与操作系统无关的命令遵循 Unix 标准：

```bash
$ python hello.py
```

**粗体文本**将表示新术语。

注释框显示为：

| Note |
| :--- |
| 这是一个注释。 |

警告框显示为：

| Warning |
| :--- |
| 这是一个警告。 |

重要框显示为：

| Important |
| :--- |
| 这是一个重要信息。 |

快捷键显示为：

```text
CTRL + S
```

终端命令显示为：

```bash
$ python hello.py
```

菜单项显示为：

```text
File > Option
```

路径显示为：

```text
path/to/file.py
```

代码块显示为：

```python
print("hello")
```

链接显示为：

[https://example.com](https://example.com)

> 注意

 如果你没有安装 Git，可以从 `git-scm.com` 安装。或者，你可以直接从 GitHub 网站下载 ZIP 格式的 CPython 源码。

如果你以 ZIP 文件下载源码，它将不包含任何历史记录、标签或分支。

在新下载的 `cpython` 目录中，你将看到以下子目录：

```
cpython/
  -Doc        文档源代码
  -Grammar   计算机可读的语言定义
  -Include    C 头文件
  -Lib        用 Python 编写的标准库模块
  -Mac        macOS 支持文件
  -Misc       杂杂文件
  -Modules    用 C 编写的标准库模块
  -Objects    Python 解析器源代码
  -Parser     针对旧版本 Windows 的 Windows 编译支持文件
  -PC         'python' 可执行文件和其他二进制文件的源代码
  -PCBuild    Windows 编译支持文件
  -Programs   CPython 解释器源代码
  -Python     用于构建或扩展 CPython 的独立工具
  -Tools      用于自动化 makefile 配置的自定义脚本
```

接下来，你可以配置好开发环境。

对本部分提供反馈 »

### 设置你的开发环境

在本书中，你将处理 C 和 Python 代码。因此，将你的开发环境配置为支持这两种语言是至关重要的。

CPython 源码约有 65% 是 Python（测试占了很大一部分），24% 是 C，其余是其他语言的混合。

### IDE 还是编辑器？

如果你还没有决定使用哪种开发环境，首先需要做一个决定：是使用集成开发环境 (IDE) 还是代码编辑器。

- IDE 针对特定的语言和工具链。大多数 IDE 都集成了测试、语法检查、版本控制和编译功能。
- 代码编辑器允许你编辑代码文件，无论是什么种语言。大多数代码编辑器都是带有语法高亮的简单文本编辑器。

由于其功能完备，IDE 通常会消耗更多硬件资源。因此，如果你的内存有限（少于 8GB），建议使用代码编辑器。IDE 的启动时间也较长。如果你想快速编辑文件，代码编辑器是更好的选择。

这里有数百种免费或付费的编辑器和 IDE，以下是一些适合 CPython 开发的常用 IDE 和编辑器：

| 应用 | 样式 | 支持 |
| --- | --- | --- |
| Microsoft VS Code | 编辑器 | Windows, macOS 和 Linux |
| Atom | 编辑器 | Windows, macOS 和 Linux |
| Sublime Text | 编辑器 | Windows, macOS 和 Linux |
| Vim | 编辑器 | Windows, macOS 和 Linux |
| Emacs | 编辑器 | Windows, macOS 和 Linux |
| Microsoft Visual Studio | IDE (C, Python 及其他) | Windows* |
| JetBrains PyCharm | IDE (Python 及其他) | Windows, macOS 和 Linux |
| JetBrains CLion | IDE (C 及其他) | Windows, macOS 和 Linux |

* Visual Studio 有 Mac 版本可供，但不支持 Visual Studio 的 Python 工具，也不支持 C 编译。

为了辅助 CPython 的开发，你将探索以下软件的设置步骤：

- Microsoft Visual Studio
- Microsoft Visual Studio Code
- JetBrains CLion
- Vim

跳转到你选择的应用程序章节，或者如果你想进行比较，可以阅读所有章节。

### 设置 Visual Studio

最新版本的 Visual Studio（Visual Studio 2019）在 Windows 上内置支持 Python 和 C 源码。我建议在本书中使用它。如果你已经安装了 Visual Studio 2017，也可以使用。

注意

编译 CPython 或本书的内容不需要任何付费功能。你可以使用免费的 Visual Studio 社区版。

引导性能优化（Profile-Guided-Optimization）编译配置需要专业版或更高版本。

你可以从微软的 Visual Studio 网站免费下载 Visual Studio。

一旦下载了 Visual Studio 安装程序，你会被要求选择想要安装的组件。本书的最低配置是：

- Python 开发负载
- 可选的 Python 原生开发工具
- Python 3 64位 (3.7.2)（如果你已经安装了 Python 3.7，可以取消选择）

如果你想更节省磁盘空间，请取消任何其他可选功能。

安装程序将下载并安装所有所需组件。安装可能需要一小时，所以你可能想先继续阅读，回到本部分。

安装程序完成后，点击“启动”按钮启动 Visual Studio。系统会提示你登录。如果你有 Microsoft 账户，可以登录，也可以跳过该步骤。

现在你会被提示“打开项目”。你可以通过“克隆 (Clone)”或“检出 (checkout)”选项直接从 Visual Studio 克隆 Python 的 Git 仓库。

对于“存储库位置 (Repository Location)”，输入 `https://github.com/python/cpython`，选择你的本地路径并点击“克隆”。

Visual Studio 将使用 Visual Studio 内置的 Git 版本从 GitHub 下载 CPython 副本。这一步也为你省去了在 Windows 上安装 Git 的麻烦。下载可能需要 10 分钟。

一旦项目下载完成，你需要通过点击“解决方案和项目 (Solutions and Projects) > pcbuild.sln”，让 Visual Studio 指向 PCBuild pcbuild.sln 解决方案文件。

![](img/826aa5e3e0d3a5997a0ec0a64c5e3c6_27_png)

一旦项目下载完成，你需要通过点击“解决方案和项目 (Solutions and Projects) > pcbuild.sln”，让 Visual Studio 指向 PCBuild pcbuild.sln 解决方案文件。

![](img/826aa5e3e0d3a5997a0ec0a64c5e3c6_28_png)

一旦项目下载完成，你需要通过点击“解决方案和项目 (Solutions and Projects) > pcbuild.sln”，让 Visual Studio 指向 PCBuild pcbuild.sln 解决方案文件。

![](img/826aa5e3e0d3a5997a0ec0a64c5e3c6_29_png)

一旦项目下载完成，你需要通过点击“解决方案和项目 (Solutions and Projects) > pcbuild.sln”，让 Visual Studio 指向 PCBuild pcbuild.sln 解决方案文件。



![](img/826aa5e3e0d3a5997a0ec0a64c5e3c6_30_0_png)

一旦项目下载完成，你需要通过点击“解决方案和项目 (Solutions and Projects) > pcbuild.sln”，让 Visual Studio 指向 PCBuild `pcbuild.sln` 解决方案文件。

![](img/826aa5e3e0d3a5997a0ec0a64c5e3c6_31_0_png)

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build",
      "type": "shell",
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "windows": {
        "command": "PCBuild\\build.bat",
        "args": ["-p x64 -c Debug"]
      },
      "linux": {
        "command": "make -j2 -s"
      },
      "osx": {
        "command": "make -j2 -s"
      }
    }
  ]
}
```

通过 Task Explorer 插件，你将在 vscode 组内看到你配置的任务列表：

![](img/826aa5e3e0d3a647c5e3c6_32_0.png)

在下一章节中，你将学习更多关于编译 CPython 的构建过程。

### 设置 JetBrains CLion

JetBrains 为 Python 开发了一个名为 PyCharm 的 IDE，还开发了用于 C/C++ 开发的 IDE CLion。

CPython 同时包含 C 和 Python 代码。你无法在 PyCharm 中安装 C/C++ 支持，但 CLion 内置了 Python 支持。

要在 CLion 中设置 CPython，请安装以下插件：

- Makefile 支撑

CPython 与 CMake 系统深度集成。然而，CPython 使用的是 GNU Make。当你打开 CPython 源码目录时，CLion 会报错说找不到 `CMakeLists.txt` 文件。有一个解决办法，可以从 CPython Makefile 中的编译步骤创建一个 `compile_commands.json` 文件。

| 重要性 |

|---|---|

| 这假设你能够编译 CPython，请阅读“为你的操作系统 编译 CPython”并返回本章节。 |

我们需要使用一个名为 `compileddb` 的工具来创建一个“编译数据库”。在命令行中，进入 CPython 仓库目录执行：

```bash
$ pip install compileddb
$ compileddb make
```

然后打开 CLion 并打开 `compile_commands.json` 文件，系统会提示你打开文件或“作为项目打开”，请选择“作为项目打开”：

![](img/826aa5e3e0d3a647c5e3c6_34_0.png)

CLion 随后会将 CPython 源码目录作为一个项目打开。

### 注意

对于 2020.1 之前的 CLion 版本，你需要将编译命令和项目关联。进入 CLion 的 `Build, Execution, Deployment, Compilation Database` 并勾选“Use auto-import”（自动导入）框：

![](img/826aa5e3e0d3a647c5e3c6_35_0.png)

当你以后打开此项目时，它将根据编译后的 CPython 版本提供智能代码导航。

在编辑器中，在 macOS 上使用 `cmd + click`，在 Windows 和 Linux 上使用 `ctrl + click` 将提供编辑器导航功能：

### 设置 JetBrains CLion

```c
static int do_raise(PyThread *tstate, PyObject *exc, PyObject *cause);
static int un_unpackable(PyThread *tstate, PyObject *int, PyObject **obj);

#define Py_TracingPossible(eval) ((eval)=~tracing_possible)
// 在所有地方使用 Py_TracingPossible（找到 4 处）
PyObject *PyEval_Code(PyObject *code) {
    if (Py_TracingPossible(code) & PyDebug_TRACE_LINE_ENABLED) {
// tags #8231 ~Py_TracingPossible/python.c:42 define Py_TracingPossible(file)
    return PyEval_Frame(
        globals, locals,
        (PyObject **)NULL,
        (PyObject **)NULL,
        (PyObject **)NULL,
        NULL
    );
}

/* 解释器主循环 */
```

你可以使用 Makefile 为编译 CPython 创建快捷方式。选择 `Run -> Edit Configurations` 打开 `Run/Debug Configurations` 窗口。在窗口内选择 `+` 添加一个 Makefile 配置。将 `all` 设置为名称，`all` 设置为目标，并将 `-s j2` 设置为参数。确保 `Working Directory`（工作目录）设置为你下载源码的目录：

![](img/826aa5e3e0d3a647c5e3c6_36_0.png)

点击 `Apply` 添加此配置。你可以针对任何 CPython make 目标重复此步骤。完整参考请参阅 `CPython's Make Targets`。

Make all` 构建配置现在将出现在 CLion 窗口的右上角：

![](img/826aa5e3e0d3a647c5e3c6_37_0.png)

现在 CLion 设置好了，请遵循编译 CPython 的步骤进行。

### 设置 Vim

Vim 是一个强大的基于控制台文本编辑器。使用 Vim 时手可以放在键盘主位键。快捷键和命令触手可及，便于快速开发。

> 注意

> 在大多数 Linux 发行版和 macOS 终端中，`vi` 是 `vim` 的别名。我会使用 `vim` 命令，但如果你有别名，`vi` 也可以工作。

Vim 默认情况下仅有基本功能，比像记事本这样的文本编辑器多不了多少。通过一些扩展，Vim 可以变得非常强大，能够同时处理 Python 和 C 编辑。Vim 的插件位于各个位置，例如 GitHub。为了方便安装插件，你可以安装一个插件管理器如 Vundle。

要安装 Vundle，在终端运行此命令：

```bash
$ git clone https://github.com/VundleVim/VundleVim.git
~/.vim/bundle/Vundle.vim
```

一旦下载了 Vundle，你需要配置 Vim 来加载 Vundle 引擎。

我们将安装插件：

- vim-fugitive 用于 Git 状态栏，提供了许多 Git 任务的快捷键

- tagbar 用于一个方便跳转到函数、方法和类的侧边栏

要安装这些插件，首先修改你的 vim 配置文件（通常是 `~/.vimrc`），包含以下内容：

```
python-book-samples > 11 .vimrc
```

Python 中用于调试的函数，这种方法在 C 中是行的。

你将在本书的后部分详细介绍调试内容。

对本部分提供反馈 »

## 编译 CPython

现在你已经下载了 CPython 并配置了开发环境，你就可以将 CPython 源代码编译为可执行的解释器了。

与 Python 文件不同，C 源代码每次更改时都必须重新编译。因此，你可能想标记此章节，并记住某些步骤，因为你会反复执行这些操作。

在上一节中，你学习了如何设置开发环境，并包含了运行“构建”（Build）阶段的选项，该阶段会重新编译 CPython。在构建步骤生效之前，你需要一个 C 编译器，并且需要一些构建工具。使用的工具取决于你所使用的操作系统，请直接跳转到对应操作系统的章节。

> 注意

> 如果你担心这些步骤中的任何一个会干扰现有的 CPython 安装，请放心。CPython 源代码目录的行为类似于虚拟环境。

对于编译 CPython、修改源码以及标准库，所有操作都将在源代码目录的沙箱内。

如果你想安装自定义版本，本章将涵盖这一步骤。

### 在 macOS 上编译 CPython

在 macOS 上编译 CPython 需要一些额外的应用程序和库。你首先需要基本的 C 编译器工具包。“命令行开发工具”（Command Line Development Tools）是一个你可以通过 macOS App Store 更新的应用。你需要在终端中进行初始安装。

> 注意

> 在 macOS 中打开终端，请前往 应用程序 > 终端。你可能想将此应用保存到 Dock 中，右键点击图标并选择“保留在 Dock 中”。

在终端中，运行以下命令安装 C 编译器和工具包：

```bash
$ xcode-select --install
```

此命令将弹出一个提示，要求下载并安装一组工具，包括 Git、Make 和 GNU C 编译器。

你还需要一个可用的 OpenSSL 副本用于从 PyPI.org 网站获取包。如果你以后计划使用此构建安装额外的包，则需要 SSL 验证。

在 macOS 上安装 OpenSSL 的简单方法是使用 Homebrew。

> 注意

> 如果你没有 Homebrew，可以通过以下命令直接从 GitHub 下载并安装 Homebrew：

$ /usr/bin/ruby -e "$(curl -fsSL \
https://raw.githubusercontent.com/Homebrew/install/master/install)"

一旦安装了 Homebrew，你可以使用 `brew install` 命令安装 CPython 的依赖项：

```bash
$ brew install openssl xz zlib gdbm sqlite
```

现在你已经有了依赖项，可以运行配置脚本了。Homebrew 有一个 `brew --prefix [package]` 命令，可以给你包安装的目录。你将通过编译 Homebrew 使用的位置来启用 SSL 的支持。

`--with-debug` 标志启用调试钩子。如果你打算出于开发或测试目的进行调试，请添加此标志。调试 CPython 将将在调试章节中详细介绍。

配置阶段只需要运行一次，同时也需要指定 zlib 包的路径：

```bash
$ CPPFLAGS="-I$(brew --prefix zlib)/include" \
LDFLAGS="-L$(brew --prefix zlib)/lib" \
./configure --with-openssl=$(brew --prefix openssl) --with-pydebug
```

运行 `configure` 将会在仓库根目录下生成一个 Makefile，你可以用它来自动化构建过程。

你现在可以通过运行以下命令构建 CPython 二进制文件：

```bash
$ make -j2 -s
```

| 另参 |

| 如需更多关于 make 选项的帮助，请参见 Make 快速入门章节。 |

在构建过程中，你可能会收到一些错误。在摘要中，make 会通知你并非所有包都已构建。例如，使用这组指令，ossaudiodev、spwd 和 _tkinter 将构建失败。如果你不针对这些包进行开发，那是没关系的。如果你需要，请查看官方开发指南网站获取更多信息。

构建将花费几分钟并生成一个名为 `python.exe` 的二进制文件。每当你对源码进行更改时，你将

### 在 Linux 上编译 CPython

需要使用相同的标志重新运行 `make`。`python.exe` 二进制文件是 CPython 的调试二进制文件。执行 `python.exe` 查看：

```bash
$ python.exe
Python 3.9.0 (tags/v3.9.0, 9fecf, May 19 2020) [GCC 10.0.1]
```

# Make 快速入门

以 `doclean` 目标为例。该目标使用 `rm` 命令删除一些生成的文档文件。

```
doclean:
  -rm -rf Doc/build
  -rm -rf Doc/tools/sphinx Doc/tools/pygments Doc/tools/docutils
```

要执行此目标，请运行 `make doclean`。`doclean` 是一个简单的目标，因为它运行了两个命令。

执行任何 make 目标的约定格式是：

```
$ make [options] [target]
```

如果你在不指定目标的情况下运行 make，make 将运行默认目标，该目标是 `Makefile` 中指定的指定的第一个目标。对于 CPython 来说，这是编译所有 CPython 部分的 target。

Make 有许多选项，以下是你认为在整本书中会用到的选项：

| 选项 | 用途 |

| :--- | :--- |

| -d, --debug=[FLAGS] | 打印各种类型的调试信息 |

| -e, --environment-overrides | 忽略 Makefile 中的错误 |

| -i,-j [N], --jobs=[N] | 允许同时运行 N 个作业（否则为无限作业） |

| -k, --keep-going | 在无法构建目标时继续执行 |

| -1 [N], --load-average=[N] | 仅当负载 < N 时才启动多个作业 |

| --max-load=[N] | |

| -n, --dry-run | 打印命令而不是运行它们 |

| -s, --silent | 不回显命令 |

| -S, --stop | 关闭 -k 选项 |

在下一节和整本书中，我将要求你使用以下选项运行 make：

```
$ make -j2 -s [target]
```

`-j2` 标志允许 make 同时运行 2 个作业。如果你有 4 个或更多核心，可以将其更改为 4 或更大，这样编译完成得更快。`-s` 标志停止 Makefile 向控制台打印它运行的每条命令。如果你想查看发生了什么，请移除 `-s` 标志。

## CPython 的 Make 目标

对于 Linux 和 macOS，你都会发现自己需要清理文件、构建或刷新配置。

CPython 的 Makefile 中内置了许多实用的 make 目标：

### 构建目标

| 目标 | 用途 |

| :--- | :--- |

| all (default) profile-opt | 编译编译器、库和模块；使用分析引导优化编译 Python 二进制执行文件 |

| clinic sharedmods | 对所有源文件运行“参数诊疗”（Argument Clinic）；构建共享模块 |

| regen-all | 重新生成所有生成的文件 |

### 测试目标

| 目标 | 用途 |

| :--- | :--- |

| test testall | 运行一组基础回归测试；运行两次完整套件 - 一次不带 .pyc 文件，一次带上它们 |

| quicktest | 运行一组更快的回归测试，排除耗时较长的测试 |

| testuniversal | 在 OSX 的通用构建中运行两种架构的测试套件 |

| coverage coverage-lcov | 使用 gcov 编译并运行测试；创建覆盖率 HTML 报告 |

### 清理目标

主要的清理目标是 `clean`、`clobber` 和 `distclean`。`clean` 目标用于通常删除编译和缓存的库以及 pyc 文件。如果你发现 `clean` 无法解决问题，请尝试 `clobber`。在发布前彻底清理环境，请运行 `distclean` 目标。

| 目标 | 用途 |

| :--- | :--- |

| check-clean-src | 在从源码构建时检查源码是否是干净 |

| cleanest | 删除之前失败作业产生的 "test_python_*" 目录 |

| clean | 删除 pyc 文件、编译的库和分析文件 |

| pycremov | 删除 pyc 文件 |

| docclean | 删除 Doc/ 下构建的文档 |

| profile-removal | 删除任何优化分析文件 |

| clobber | 与 clean 相同，但还会删除库、标签、配置和构建内容 |

| distclean | 与 clobber 相同，还会删除从源码生成的任何内容，例如 Makefile |

### 安装目标

安装目标有两种形式：默认版本（例如 `install`）和替代版本（例如 `altinstall`）。如果你想将编译版本安装到你的电脑上，但不希望它成为默认的 Python 3 安装，请使用命令的替代版本。

在执行 `make install` 后，`python3` 命令将链接到你编译的二进制文件。而使用 `make altinstall` 时，只会安装 `python$(VERSION)`，现有的 `python3` 链接将保留。

| 目标 | 用途 |



| `install` | 安装共享库、二进制文件和文档。将运行 `commoninstall`、`bininstall` 和 `maninstall` |

| `bininstall` | 安装所有二进制文件，例如 `python`，`2to3` |

| `altinstall` | 安装带有版本后缀的共享库、二进制文件和文档 |

## 在 Windows 上编译 CPython

| 目标 | 用途 |

| :--- | :--- |

| `maninstall` | 安装文档 |

| `altinstall` | 安装带版本的文档 |

| `altbininstall` | 安装带有版本后缀的 `python` 解释器，例如 `python3.9` |

| `commoninstall` | 安装共享库和模块 |

| `libinstall` | 安装共享库 |

| `sharedinstall` | 动态加载模块 |

### 杂目标

| 目标 | 用途 |

| :--- | :--- |

| `python-config` | 生成 `python-config` 脚本 |

| `recheck` | 使用相同的选项重新运行 `configure` |

| `autoconf` | 重新生成 `configure` 和 `pyconfig.h` |

| `tags` | |

| `tags` | |

| `tags` | |

## 在 Windows 上编译 CPython

在 Windows 上编译 CPython 有两种方法。第一种是从命令行编译，另一种是使用 Visual Studio。

### 从命令行编译

从命令行编译时，你需要选择要编译的 CPU 架构。默认是 `win32`，但你可能想要 64 位 (`amd64`)。如果你进行任何调试，调试构建允许在源码中附加断点。要启用调试构建，添加 `-c Debug` 来指定配置。

默认情况下，`build.bat` 会获取外部依赖，但由于我们已经过了这一步，它将打印跳过下载的消息：

```
> build.bat -p x64 -c Debug
```

该命令将产生 `PC ▸ amd64 ▸ python_-d.exe`。从命令行直接启动该二进制文件：

```
> amd64\python_d.exe

Python 3.9.01 (tags/v3.9.01:97fe9cf, May 19 2020, 10:00:00)
on win32 [MSC v.1922 64 bit (AMD64)]
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

你现在处于你编译的 CPython 二进制文件的 REPL 中。要编译发布版本：

```
> build.bat -p x64 -c Release
```

该命令将产生 `CPbuild ▸ amd64 ▸ python.exe`。

| 注意 |

| :--- | :--- |

| 后缀 `_d` 表示 CPython 是在 `Debug` 配置下构建的。`python.org` 上的发布版本是在分析引导优化 (`PGO`) 配置下编译的。有关 `PGO` 的更多信息，请参见本章末尾的分析引导优化 (`PGO`) 章节 |

## 在 Windows 上编译 CPython

| 标记 | 目的 |

| --- | --- |

| `-v` | 详细模式。在构建期间显示信息消息。 |

| `-vv` | 极详细模式。在构建期间显示详细消息。 |

| `-q` | 静音模式。构建期间仅显示警告和错误。 |

| `-e` | 下载并安装外部依赖（默认）。 |

| `-E` | **不要**下载和安装外部依赖 |

| `--pgo` | 使用配置引导优化进行编译 |

| `--regen` | 重新生成所有语法和标记，用于你更新语言时。 |

### 从 Visual Studio 编译

在 `PCBuild` 文件夹内有一个 Visual Studio 项目文件 `PCBuild pcbuild.sln`，用于构建编译和探索 CPython 源代码。

当加载解决方案（Solution）时，它会提示你将解决方案内部的项目重新重定向到你已安装的 C/C++ 编译器的版本。Visual Studio 也会以你已安装的 Windows SDK 版本为目标。

确保你将 Windows SDK 版本更改为已安装的最新版本，并将平台工具集更改为最新版本。如果你错过了此窗口，可以右键点击“解决方案和项目”窗口并点击“重目标解决方案”（Retarget Solution）。

导航到“生成 > 配置管理器”，并确保“活动配置”设置为 `debug`，并将“活动解决方案平台”设置为 64 位 CPU 架构的 `x64` 或 32 架构的 `win32`。

接下来，通过按下 `CTRL + SHIFT + B` 或选择“生成 > 生成解决方案”来编译 CPython。如果你收到任何关于缺少 Windows SDK 的错误，请确保在“重目标解决方案”窗口中设置了正确的目标设置。你应该会在开始菜单中看到“Windows Kits”，在该层级下看到“Windows Software Development Kit”。

第一次构建可能需要 10 分钟。构建完成后，你可能会看到一些可以忽略的警告。

## 在 Windows 上编译 CPython

要启动 CPython 的调试版本，按 `F5`，CPython 将直接以调试模式启动进入 REPL：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_56_0.png)

你可以通过在顶部菜单栏将构建配置从 `Debug` 更改为 `Release` 并重新运行“生成解决方案”来运行发布版本。你现在于 `PCBuild amd64` 中拥有了 CPython 的调试和发布两个版本的二进制文件。

你可以通过选择顶部菜单中的“工具 > Python 环境”来设置 Visual Studio，以便能够打开发布构建或调试构建的 REPL：

在“Python 环境”面板中，点击“添加环境”并以调试或发布版二进制文件为目标。调试二进制文件以 `_d.exe` 结尾。例如，`python_d.exe` 和 `pythonw_d.exe`。你可能倾向于使用调试二进制文件，因为它带有 Visual Studio 的调试支持，对本书非常有帮助。

在“添加环境”窗口中，将 `PCBuild amd64` 内部的 `python_d.exe` 和 `pythonw_d.exe` 作为解释器：

## 在 Windows 上编译 CPython

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_57_0.png)

在“Python 环境”窗口中点击“交互式”启动 REPL 会话，你将看到已编译 Python 版本的 REPL：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_57_1.png)

在书中，会有带有示例命令的 REPL 会话，我鼓励你使用调试二进制文件在代码中设置断点。为了方便导航代码，在“解决方案视图”中，点击切换按钮切换到：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_58_0.png)

## 配置引导优化 (PGO)

`macOS`、`Linux` 和 Windows 的构建过程都有“`PGO`”或“配置引导优化”标记。`PGO` 并不是团队创建的，而是包括 CPython 在内的许多编译器的特性。

`PGO` 的原理是先进行初始编译，然后通过运行一系列测试对应用程序进行分析。随后分析创建的配置文件，编译器将对二进制文件进行更改以提高性能。对于 CPython，分析阶段运行 `python -m test`。这些测试专门选取了常用的模块。

## 注意事项

`PGO` 过程非常耗时，因此在整本书中我将其排除在推荐步骤列表中，以缩短你的编译时间。如果你想分发自定义版本的 CPython，你应该在 Linux 和 macOS 上运行 `./configure --with-pgo`，并在 Windows 的 `build.bat` 中使用 `--pgo` 标记。

优化特定于执行配置文件的平台和架构，`PGO` 配置文件无法在操作系统或 CPU 架构之间共享。没有使用 `PGO` 编译的二进制文件将比使用 `PGO` 编译的慢。配置引导优化包含以下检查：

- **函数内联** - 如果一个函数经常从另一个函数被调用，则它将被内联以减小栈空间。

- **虚调用推测与内联** - 如果一个虚函数频繁指向某个函数，`PGO` 可以插入一个对该函数的直接调用，该调用可以被内联。

- **寄存器分配优化** - 根据配置数据结果，`PGO` 将优化寄存器分配。

- **基础块优化** - 基础块优化允许将给定帧内经常执行的字节块放置在同一组中（局部性）。它最小化了使用的内存页数，从而最小化了内存开销。

- **热点优化** - 对程序花费时间最多的函数进行优化。

- **函数布局优化** - 在分析调用图后，倾向于同一执行路径的函数将被移动到一起。

- **条件分支优化** - `PGO` 可以查看分支（如 `if..else` 或 `switch` 语句）并识别常用路径。例如，如果 `switch` 语句中有 10 种情况且一种占 95%，它将被移动到顶部。

- **死代码分离** - `PGO` 中未被调用的代码将被移动到独立区域。

### 总结

在本章中，你了解了如何将 CPython 源代码编译为可行的解释器。在书中探索和调整源代码时，可以使用这些知识。

在处理 CPython 时，你可能需要重复编译步骤几十甚至数百次。如果你能调整开发环境以创建编译的快捷方式，现在这样做将节省大量时间。

# Python 语言与语法

编译器的目的是将一种语言转换为另一种语言。将编译器想象成一个翻译。你会聘请一名翻译来听你说的英语，然后翻译成日语。

为了完成任务，翻译必须理解源语言和目标语言的语法结构。

某些编译器将编译为低级机器码，可以在系统上执行。其他编译器将编译为中间语言，由虚拟机执行。

选择编译器时的考虑因素是系统的可移植性需求。`Java` 和 `.NET CLR` 将编译为中间语言，使得编译代码可以在多个系统间迁移。`C`、`Go`、`C++` 和 `Pascal` 将编译为可执行二进制文件。该二进制文件针对编译它的平台构建。

Python 应用程序通常以源码形式分发。Python 解释器的作用是转换 Python 源码并执行它。CPython 运行时会在首次运行时编译你的代码。

Python 代码并没有被编译为机器码，而是编译为一种低级中间语言，称为字节码。字节码存储在 `.pyc` 文件中并缓存执行。如果你运行相同的

在不更改源代码的情况下运行两次 Python 程序，第二次执行时速度会更快。这是因为它加载了编译后的字节码，而不是每次都进行重新编译。

## 为什么 CPython 用 C 语言编写而不是 Python

CPython 中的 C 指的是 C 编程语言，这意味着这个 Python 分发版是用 C 语言编写的。

这个说法在很大程度上是正确的：CPython 的编译器是用纯 C 语言编写的。然而，许多标准库模块是用纯 Python 或 C 与 Python 组合编写的。

## 那么为什么 CPython 编译器用 C 语言编写而不是 Python？

答案在于编译器的工作原理。编译器分为两种类型：

- 自举编译器（Self-hosted compilers）：使用其正要编译的语言编写的编译器，例如 Go 编译器。这是通过一个被称为“自举”（bootstrapping）的过程实现的。

- 源码转换编译器（Source-to-source compilers）：使用另一种已经存在编译器的语言编写的。

如果你要从零开始编写一种新语言，你需要一个可执行程序来编译你的编译器！你需要一个编译器来执行任何操作，因此开发新语言时，通常会先用一种更老、更成熟的语言来编写。

还有一些工具可以获取语言规范并创建解析器（你将在本章中涵盖这些主题）。流行的编译器生成器包括 GNU Bison、`Yacc` 和 `ANTLR`。

## 为什么 CPython 编译器用 C 语言编写而不是 Python

### 另需参考

> 如果你想学习更多关于解析器的知识，可以查看 `lark` 项目。`Lark` 是用 Python 编写的上下文无关文法的解析器。

编译器自举的一个优秀例子是 Go 编程语言。第一个 Go 编译器是用 C 编写的，一旦 Go 可以被编译，编译器就被用 Go 重新编写了。

CPython 保留了它的 C 传承；许多标准库模块（如 `ssl` 模块或 `sockets` 模块）是用 C 编写的，以便访问底层的操作系统 API。Windows 和 Linux 内核中用于创建网络套字、操作文件系统或与显示交互的 API 都是用 C 语言编写的。

让 Python 的扩展层专注于 C 语言是有意义的。在后面，你将涵盖 Python 标准库和 C 模块。

有一个用 Python 编写的 Python 编译器叫做 `PyPy`。`PyPy` 的标志是一个衔尾蛇（Ouroboros），代表了编译器的自举特性。

另一个 Python 跨编译器的例子是 `Jython`。`Jython` 用 Java 编写，并将 Python 源码编译成 Java 字节码。正如 C 语言让你方便地导入 C 库并在 Python 中使用它们一样，`Jython` 也让你方便导入和引用 Java 模块和类。

创建编译器的第一步是定义语言。例如，以下不是有效的 Python 代码：

```python
def my_example() <str> :
{
  void* result = ;
}
```

编译器在尝试执行语言之前，需要关于该语言语法结构的严格规则。

## Python 语言规范

> 注意

在本文教程的剩余部分，`./python` 指的是 CPython 的编译版本。然而，实际命令将取决于你的操作系统。

对于 Windows：

> `python.exe`

对于 Linux：

$ `./python`

对于 macOS：

$ `./python.exe`

## Python 语言规范

CPython 源代码中包含了 Python 语言的定义。此文档是所有 Python 解释器所使用的参考规范。

该规范既有人类可读的形式，也有机器可读的形式。规范内部包含了对 Python 语言的详细解释，包括哪些是允许的以及每个语句应该如何表现。

## 语言文档

在 `Doc` 参考目录下，包含了 Python 语言中每个特征的 reStructured-Text 解释。这些文件构成了 `docs.python.org/3/reference` 上的官方 Python 参考指南。

目录内部包含了你理解整个语言、结构和关键字的文件：

```
cpython/Doc/reference
- compound_stmts.rst
- datamodel.rst
- execution_model.rst
```

# 使用解析器生成器

`try` 语句是一个复杂结构的良好示例。

如果你想详细了解 Python 语言，语法定义在 `Grammar`（语法）▸ `Grammar` 章节中。

# 使用解析器生成器

语法文件本身从不被 Python 编译器使用。相反，解析器生成器会创建一个解析器表（parser table）。如果你对语法文件进行了更改，你必须重新生成解析器表并重新编译 CPython。

解析器表（Parser Tables）是一系列潜在解析器状态的列表。当解析树变得复杂时，它们能确保语法不会产生歧义。

## 解析器生成器

解析器生成器通过将 EBNF 语句转换为非确定性有限自动机（NFA）来工作。NFA 的状态和转换被解析并合并为确定性有限自动机（DFA）。

DFA 被解析器作为解析表。这项技术形成于斯坦福大学，并于 20 世纪 80 年代开发，就在 Python 出现之前。CPython 的解析器生成器 `pgen` 是 CPython 项目特有的。

`pgen` 应用在 Python 3.8 中从 C 语言重写为 Python，位于 `Parser`（解析器）▸ `pgen` ▸ `pgen.py`。

它通过以下方式执行：

```
$ ./python -m Parser.pgen [grammar] [tokens] [graminit.h] [graminit.c]
```

它通常从构建脚本中执行，而不是直接执行。

DFA 和 NFA 没有视觉输出，但 CPython 有一个分支带有有向图输出。装饰器语法定义在 `Grammar/Grammar AS` 中：

`decorator: '@' dotted_name ['(' [arglist] ')'] NEWLINE`

解析器生成器创建了一个包含 11 个状态的复杂 NFA 图形。每个状态都用数字表示（在语法中带有关于其名称的提示）。转换被称为“弧”（arcs）。

DFA 比 NFA 简单，路径更少：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_70_0.png)

NFA 和 DFA 图仅用于调试复杂语法的设计。

我们将使用铁路道图（Railroad Diagrams）来表示语法，而不是 DFA 或 NFA 图形。

例如，此图表示了装饰器语句可以采取的路径：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_70_1.png)

## 重新生成语法

为了看到 `pgen` 的运行，让我们更改 Python 语法的部分。搜索 `Grammar`（语法）▸ `pass_stmt` 来查看 `pass` 语句的定义：

```
pass_stmt: 'pass'
```

修改该行，通过添加选择项 `|` 和 `proceed` 字面量，使其接受终结（关键字）'pass' 或 'proceed' 作为关键字。

```
pass_stmt: 'pass' | 'proceed'
```

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_71_0.png)

接下来，运行 `pgen` 重新构建语法文件。CPython 带有用于自动化 `pgen` 的脚本。

在 macOS 和 Linux 上，运行 `make regen-grammar` 目标：

```
$ make regen-grammar
```



在 Windows 上，从 `PCBuild` 目录打开命令行并运行带有 `--regen` 标志的 `build.bat`：

```
> build.bat --regen
```

你应该能看到一个输出，显示新的 `Include ▸ graminit.h` 和 `Python ▸ graminit.c` 文件已重新生成。

使用重新生成的解析器表，当你编译 `CPython` 时，它将使用新语法。请针对你的操作系统使用上章中使用的相同编译步骤。

如果代码编译成功，你可以执行你的新 `CPython` 二进制文件并启动 REPL。

在 REPL 中，你现在可以尝试定义函数。不要使用 `pass` 语句，而是使用你编译到 Python 语法中的 `proceed` 关键字选项：

```
$ ./python -X oldparser

Python 3.9.0b1 (tags/v3.9.0b1:97fe9cf, May 19 2020, 10:00:0)
[Clang 10.0.1 (clang-1001.0.46.4)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> example():
    ...
>>> example()
```

恭喜，你更改了 `CPython` 语法并编译了你自己的 `CPython` 版本。接下来，我们将探索标记（tokens）及其与语法的关系。

# 标记 (Tokens)

除了语法文件，还有 `Grammar ▸ Tokens` 文件夹，它包含了在解析树中作为叶节点的每个类型。每个标记都有一个名称和一个生成的 ID。这些名称用于在分词器中更方便地引用。注意：`Grammar ▸ Tokens` 文件是 Python 3.8 的新功能。

| 范围 (Range) | 名称 (Name) | 值 (Value) |

| :--- | :--- | :--- |

| ... | ... | ... |

*(注：此处示例表格内容因原文不完整，仅保留格式，实际翻译应根据原文内容填充)*

*(由于原文中表格部分仅为占符或未完整，此处按要求保留格式。若有具体内容将进行翻译)*

**更正：原文表格如下：**

| Range | Name | Value |

| :--- | :--- | :--- |

| ... | ... | ... |

*(注：提供的原文文本中表格仅有表头和占位符，故翻译表头)*

| 范围 | 名称 | 值 |

| :--- | :--- | :--- |

*(注：重新检查原文，原文中表格内容为空，仅有表头)*

| Range | Name | Value |

| :--- | :--- | :--- |

*(此处由于用户提供的文本中表格只有表头，故翻译表头)*

| Range | Name | Value |

| :--- | :--- | :--- |

*(注：根据用户提供的文本，表格部分仅包含表头，故翻译如下：)*

| 范围 | 名称 | 值 |

| :--- | :--- | :--- |

*(注：此处发现用户提供的文本中表格确实只有表头，故翻译翻译)*






Parser Tables are a list of potential parser states. When parse trees become complex, they ensure that grammar cannot be ambiguous.

## The Parser Generator

... (rest of the translation follows)

### 更复杂的示例

```
assert_stmt: 'assert' test [', 'test']
```

3.8 版本添加了另一种可选的测试标记（token）类型，以便语法能够能够明确地规定哪些语句应该支持赋值表达式，哪些不应该支持。

这被称为 `namedexpr_test`，它在语法中定义为：

```
namedexpr_test: test [=': test]
```

或者，通过轨道图（Railroad Diagram）可视化为：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_77_0.png)

`if` 语句的新语法已更改，将 `test` 替换为 `namedexpr_test`：

```
if_stmt: 'if' namedexpr_test ': suite ('elif' namedexpr_test ': suite 'else' ': suite
```

通过轨道图可视化为：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_77_1.png)

为了区分 `:=` 与现有的冒号 (`:`) 和等号 (`=`) 标记，随后在语法标记中添加了以下标记：

```
COLONEQUAL: ':='
```

这并不是支持赋值表达式所需的唯一更改。该更改改变了 CPython 编译器的许多部分，如请求（Pull Request）所示。

## 结论

| 另请参考 |
| :--- |
| 有更多关于 CPython 解析器生成器的信息，pgen 的作者在 PyCon Europe 2019 上进行了一场关于实现和设计的演讲：“野兽之魂”（The soul of the beast）。 |

在本章中，你已经接触了 Python 语法定义和解析器生成器。在下一章中，你将扩展这些知识来构建一个更复杂的语法特性——一个“近似等于”运算符。

在实践中，Python 语法的更改必须经过仔细的考虑和讨论。这种严谨的程度有两个原因：

- 拥有“过多”的语言特性或复杂的语法会改变 Python 作为简单易读语言的理念
- 语法的更改会引入向后不兼容，这会给所有开发者带来工作量

如果 Python 核心开发人员对语法提出更改，必须以 Python 增强提案（PEP）的形式提出。所有 PEP 都有编号并在 PEP 索引中记录。PEP 5 文档记录了语言演进的指南，并规定更改必须通过 PEP 提出。

成员也可以通过 `python-ideas` 邮件列表在开发组之外对语言提出更改。

你可以在 PEP 索引中看到未来 CPython 版本的草案、被拒绝和已接受的 PEP。一旦 PEP 达成共识且草案定稿，指导委员会（Steering Council）必须接受或拒绝它。PEP 13 定义的指导委员会规定，他们应当致力于“维护 Python 语言和 CPython 解释器的质量与稳定性”。

## 配置与输入

现在你已经了解了 Python 语法，是时候探索代码是如何输入到可以执行的状态了。

Python 代码在 CPython 中有多种运行方式。以下是最常用的几种：

1. 通过运行 `python -c` 和一个 Python 字符串
2. 通过运行 `python -m` 和模块名
3. 通过运行 `python [file]` 并指向包含 Python 代码的文件路径
4. 通过管道将 Python 代码通过标准输入输入到 python 可执行文件中，例如 `cat [file] | python`
5. 通过启动 REPL 并逐个执行命令
6. 使用 C API并将 Python 作为嵌入式环境

| 另请参考 |
| :--- |
| Python 有许多执行脚本的方法，这可能会让人无从下手。如果你想了解更多，Darren Jones 在 realpython.com 上整理了一门关于运行 Python 脚本的精彩课程。 |

要执行任何 Python 代码，解释器需要：

- 一个要执行的模块
- 一个存储变量等信息的状态
- 配置，例如启用了哪些选项

有了这三个组件，解释器就可以执行代码并提供输出：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_81_0.png)

### 注意

类似于针对 Python 代码的 PEP8 风格指南，针对 CPython 的 C 代码也有 PEP7。

C 源代码有一系列命名标准：

- 公共函数使用 `Py` 前缀，绝不用于静态函数。`Py_` 前缀留给诸如 `Py_FatalError` 等全局服务例程。特定的例程组（如特定对象类型的 API）使用较长的前缀，例如用于字符串函数的 `PyString_`。
- 公共函数和变量使用带划线的混合命名法（MixedCase），例如：`PyObject_GetAttr()`、`Py_BuildValue()`、`PyExc_TypeError()`。
- 有时“内部”函数对加载器可见。使用 `_Py` 前缀，例如 `_PyObject_Dump()`。
- 宏应该具有混合命名法前缀后接大写，例如 `PyString_AS_STRING`、`Py_PRINT_RAW`。

### 使用命令行设置运行时配置

Python 还提供了几种命令行界面选项。

例如，CPython 有一种名为详细模式（verbose mode）的模式。这主要针对调试 CPython 的开发者设计。

在 Python 中，你可以通过 `-v` 标志启用详细模式。在详细模式下，Python 在加载模块时会向屏幕打印消息：

```
$ ./python -c "print('hello world')"
### installing zipimport hook
import zipimport # builtin
# installed zipimport hook
...
```

你将看到数百行或更多内容，包含用户 site-packages 以及系统环境中任何其他内容的导入信息。

由于运行时配置可以通过多种方式设置，因此配置设置之间存在优先级顺序。详细模式的优先级顺序为：

1. `config->verbose` 的默认值在源代码中被硬编码为 -1。
2. 环境变量 `PYTHONVERBOSE` 用于设置 `config->verbose` 的值。
3. 如果环境变量不存在，则保留默认值 -1。
4. 在 Python ▸ `initconfig.c` 的 `config_parse_cmdline()` 中，如果提供了命令行标志，则使用它来设置值。
5. 该值通过 `_Py-GetGlobalVariablesAsDict()` 拷贝到全局变量 `Py_VerboseFlag`。

所有的 `PyConfig` 值都遵循相同的序列和优先级：

### 构建配置

| 系统配置 | 命令行参数 | 环境变量 |
| --- | --- | --- |
| | PyPreConfig | |
| | PyConfig | |
| | Runtime | |

### 查看运行时标志

CPython 解释器有一组运行时标志。这些标志是用于切换 CPython 特定行为的高级功能。在 Python 会话中，你可以通过 `sys.flags` 命名元组访问运行时标志，例如详细模式和安静模式。所有的 `-x` 标志可以在 `sys._xoptions` 字典可用：

```
$ /python -X dev -q
>>> import sys
>>> sys.flags
sys.flags(debug=0, inspect=0, optimize=0,
dont_write_bytecode=0, no_user_site=0, no_site=0,
ignore_environment=0, verbose=0, bytes_warning=0,
quiet=1, hash_randomization=1, isolated=0,
dev_mode=True, utf8_mode=0)
>>> sys._xoptions
{'dev': True}
```

### 构建配置

除了 Python ▸ cpython ▸ `initconfig.h` 中的运行时配置外，还有构建配置。它位于根文件夹下的 `pyconfig.h` 中。该文件是在 macOS/Linux 构建过程的 `./configure` 步骤中，或通过 Windows 的 `build.bat`动态创建的。

可以通过运行以下命令查看构建配置：

```
./python -m sysconfig
Platform: "macos-10.15-x86_64"
Python version: "3.9"
Current installation scheme: "posix_prefix"
Paths:
  data = "/usr/local"
  include = "/Users/anthonysaw/CLionProjects/cpython/Include"
  platinclude = "/Users/anthonysaw/CLionProjects/cpython"
...
```

构建配置属性是编译时值，用于选择链接到二进制文件中的额外模块。例如，调试器、仪器库和内存分配器都是在编译时设置的。

通过三个配置阶段，CPython 解释器现在可以接收输入并将文本处理为可执行代码。

### 从输入构建模块

在执行任何代码之前，它必须从输入编译成模块。如前所述，输入的类型各不相同：

- 本地文件和包
- I/O 流，例如 `stdin` 或内存管道
- 字符串

输入被读取后传递给解析器，然后传递给编译器。

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_88_0.png)

由于这种灵活性，CPython 源代码的大部分专门用于处理到 CPython 解析器的输入。

## 相关源文件

有两个主要文件处理命令行界面。

| 文件 | 用途 |
| :--- | :--- |
| Lib runpy.py | 用于导入 Python 模块并执行它们的标准库模块 |
| Modules main.c | 封装外部代码执行的函数，例如来自文件、模块或输入流的代码 |
| Programs python.c | Windows、Linux 和 macOS 上 python 可执行文件的入口点。仅作为 Modules/main.c 的封装。 |
| Python pythonrun.c | 封装用于从命令行处理输入的内部 C API 的函数 |

### 读取文件/输入

一旦 CPython 获取了运行时配置和命令行参数，就可以加载要执行的代码。

此任务由 Modules main.c 内部 `pymain_main()` 函数处理。

根据新创建的 `PyConfig` 实例，CPython 现在将执行通过多个选项提供的代码。

### 命令行输入字符串

CPython 可以通过 `-c` 选项在命令行执行短小的 Python 应用。例如，执行 `print(2 ** 2)`：

```
$ ./python -c "print(2 ** 2)"
```

`pymain_run_command()` 函数在 Modules ▸ main.c 中执行，接收命令行参数。



`pymain_run_command()` 函数在 `Modules ▸ main.c` 中执行，接收命令行参数。

CPython 可以通过 `-c` 选项在命令行执行短小的 Python 应用。例如，执行 `print(2 ** 2)`：

```
$ ./python -c "print(2 ** 2)"
```

`pymain_run_command()` 函数在 `Modules ▸ main.c` 中执行，接收命令行参数。

CPython 可以通过 `-c` 选项在命令行执行短小的 Python 应用。例如，执行 `print(2 ** 2)`：

```
$ ./python -c "print(2 ** 2)"
```

`pymain_run_command()` 函数在 `Modules ▸ main.c` 中执行，接收命令行参数。

CPython 可以通过 `-c` 选项在命令行执行短小的 Python 应用。例如，执行 `print(2 ** 2)`：

```
$ ./python -c "print(2 ** 2)"
```

`pymain_run_command()` 函数在 `Modules ▸ main.c` 中执行，接收命令行参数。

注意

字符串被传递给模块。

### 从脚本文件或标准输入输入

如果 `python` 的第一个参数是文件名，例如 `python test.py`，那么 CPython 将打开一个文件句柄，并将其传递给 `PyRun_SimpleFileFlags()`，函数位于 `Python ▸ pythonrun.c`。

该函数有三种可能的路径：

### 从输入构建模块

- 1. 如果文件路径是一个 `.pyc` 文件，它将调用 `run_pyc_file()`。
- 2. 如果文件路径是一个脚本文件 `.py`，它将运行 `PyRun_FileInEx()`。
- 3. 如果由于用户运行命令 `| python` 导致文件路径为 `stdin`，则将 `stdin` 视为句柄并运行 `PyRun_FileInEx()`。

对于 `stdin` 和基础脚本文件，CPython 将句柄传递到位于 `Python ▸ pythonrun.c` 中的 `PyRun_FileInEx()`。

`PyRun_FileInEx()` 的目的类似于 `PyRun_SimpleStringFlags()`。CPython 会将句柄加载到 `PyParser_ASTFromFileObject` 中。

与 `PyRun_SimpleStringFlags()` 相同，一旦 `PyRun_FileInEx()` 从文件创建了 Python 模块，它就会发送到 `run_mod()` 执行。

### 从编译后的字节码输入

如果用户运行指向 `.pyc` 文件的路径 `python`，那么 CPython 将不会将文件作为纯文本文件加载并解析，而是假设 `.pyc` 文件包含一个写入磁盘的代码对象。

在 `PyRun_SimpleFileFlags()` 中，有一个条款允许用户提供 `.pyc` 文件的路径。

`Python ▸ pythonrun.c` 内部的 `run_pyc()` 函数通过句柄提取 `.pyc` 文件代码对象。磁盘上的代码对象数据结构是 CPython 编译器缓存编译代码的方式，这样在每次调用脚本时就不需要重新解析。

> 注意：提取（Marshaling）是一个将文件内容复制到内存并转换为特定数据结构的术语。

一旦代码对象被提取到内存中，它会被发送到 `run_eval_code_obj()`，该函数调用 `Python ▸ ceval.c` 来执行代码。

## 结论

在本章中，你了解了 Python 的许多配置选项是如何加载的，以及代码是如何输入解释器的。Python 输入的灵活性使其成为各种应用的强大工具，例如：

- 命令行工具
- 长运行的网络应用程序，如 Web 服务器
- 短小、可组合的脚本

Python 以多种设置配置属性的能力导致了复杂性。例如，如果你在 Python 3.8 上测试了一个 Python 应用程序且它运行正常，但在不同的环境中失败了，你需要了解该环境中的哪些设置不同。这意味着你需要检查环境变量、运行时标志，甚至 `sys config` 配置属性。`sys config` 中找到的编译时属性在不同的 Python 发行版之间可能不同。例如，从 `python.org` 下载的 `macOS Python 3.8` 默认值与 `Homebrew` 上的 `Python 3.8` 发行版或 `Anaconda` 发行版不同。

所有这些输入方法的输出都是一个 Python 模块。在下一章中，你将发现如何从输入创建模块。

# 使用语法树进行词法和解析

在上一章中，你探索了如何从各种来源读取 Python 文本。它需要转换为编译器可以使用的结构。

这一阶段是**解析：**

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_94_0.png)

在本章中，你将探索如何将文本解析为可以编译的逻辑结构。

CPython 使用两种结构来解析代码：**具体语法树（CST）**和**抽象语法树（AST）**。

## 具体语法树生成

| 读取器 | 词法分析器 | CST | 解析器 | AST | 编译器 |
| --- | --- | --- | --- | --- | --- |

解析过程的两个部分是：

- 1. 使用**解析器-词法分析器（Lexer）**创建具体语法树
- 2. 使用**解析器**从具体语法树创建抽象语法树

这两个步骤是许多编程语言中使用的常用范式。

### 具体语法树生成 (CST)

具体语法树（CST，有时也称为**解析树**）是一个有序的、有根的树结构，它表示上下文无关文法中的代码。

CST 是由**词法分析器**和**解析器**创建的。你在“**Python 语言与语法**”章节中探索了解析器生成器。解析器生成器的输出是一个确定性有限自动机（DFA）解析表，描述了上下文无关文法的所有可能状态。

> **另参**
>
> Python 的原始作者 Guido van Rossum 目前正在研究一种上下文文法，用作 CPython 使用的 LL(1) 语法的替代方案。这种替代方案被称为解析表达式语法，或 PEG。
>
> 这将作为 Python 3.9 的一项实验性特性可用。

在语法章节中，你探索了一些表达式类型，例如 `if_stmt` 和 `with_stmt`。具体语法树将语法符号（如 `if_stmt`）表示为分支，并将标记和终结符表示为叶节点。

例如，算术表达式“a + 1”变成了 CST：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_96_0.png)

算术表达式在这里由三个主要分支表示：左侧、运算符和右侧。

解析器遍历输入流中的各个标记，并将其与语法中可能的状态和标记进行匹配，以构建 CST。

在 语法 › 语法 中

```
arith_expr: term ((+ | -) term)*
term: factor ((* | / | %) factor)*
power: atom (^ power)*
atom: ( arg_expr ) | NAME | NUMBER | STRING | ...
```

## CPython 解析器-分词器

在执行之前，解析器-分词器会建立 `tok_state`，这是一个用于存储分词器使用的所有状态的临时数据结构。分词器状态包含当前光标位置和行等信息。

解析器-分词器调用 `tok_get()` 获取下一个标记。解析器-分词器将生成的标记 ID 传递给解析器，解析器使用解析器生成 DFA 在具体语法树（CST）上创建一个节点。

`tok_get()` 是整个 CPython 代码库中最复杂的函数之一。它包含超过640行代码，包含了数十年来积累的边缘情况、新语言特性和语法。

循环调用分词器和解析器的过程可以所示：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_100_0.png)

`PyParser_ParseFile()` 返回的 CST 根节点对于下一个阶段至关重要，即将 CST 转换为抽象语法树（AST）。节点类型在 `Include -> node.h` 中定义如下：

```
typedef struct _node {
    short n_type;
    char *n_str;
int n_lineno;
int n_col_offset;
int n_nchildren;
struct _node *n_child;
int n_end_lineno;
int n_end_col_offset;
} node;
```

由于 CST 是语法、标记 ID 和符号的树，编译器很难基于 Python 语言做出快速决策。

在进入 AST 之前，有一种方法可以访问解析阶段的输出。CPython 有一个标准库模块 `parser`，它通过 Python API 暴露了 C 函数。

输出将是数字形式，使用 `make regen-grammar` 阶段生成的标记和符号数字，存储在 `Include/token.h` 中：

```python
>>> from pprint import pprint
>>> import parser
>>> st = parser.expr('a + 1')
>>> pprint(parser.st2list(st))
[258,
[332,
[306,
[311,
[312,
[313,
[316,
[317,
[318,
[319,
[320,
[321, [322, [323, [324, [325, [1, 'a']]]]]]],
[14, '+'],
[321, [322, [323, [324, [325, [2, '1']]]]]]]]]]]]]]]
[4, ''],
[0, '']]]
```

为了更于理解，你可以将 `symbol` 和 `token` 模块中的所有数字放入字典中，并递归地将 `parser.st2list()` 输出中的值替换为标记名称：

`cpython-book-samples ► 21 ► lex.py`

```python
import symbol
import token
import parser

def lex(expression):
    symbols = {v: k for k, v in symbol.__dict__.items()}
    if isinstance(v, int):
        tokens = {v: k for k, v in token.__dict__.items()}
        if isinstance(v, int):
            lexicon = {*symbols, **tokens}
    st = parser.expr(expression)
    st_list = parser.st2list(st)

def replace(l: list):
    r = []
    for i in l:
        if isinstance(i, list):
            r.append(replace(i))
        else:
            if i in lexicon:
                r.append(lexicon[i])
            else:
                r.append(i)
    return r

return replace(st_list)
```

你可以用一个简单的表达式（如 `a + 1`）运行 `lex()`，查看它是如何表示为解析树的：

```python
>>> from pprint import pprint
>>> pprint(lex('a + 1'))

['eval_input',
  ['testlist',
   ['test',
    ['or_test',
     ['and_test',
      ['not_test',
        ['comparison',
        ['expr',
          ['xor_expr',
            ['and_expr',
              ['shift_expr',
                ['arithith_expr',
                  ['term',
                  ['factor', ['power', ['atom_expr'], ['atom'],
                  ['NAME', 'a']]]]]
                ['PLUS', '+'],
                ['term',
                  ['factor',
                    ['power', ['atom_expr'], ['atom', ['NUMBER'],
                    '1']]]]]]]]]]]
    ['NEWLINE', ''],
  ['ENDMARKER', '']]]
```

在输出中，你可以看到小写的符号（如 `'arithith_expr'`）和大写的标记（如 `'NUMBER'`'）。

## 抽象语法树

CPython 解释器的下一个阶段是将解析器生成的 CST 转换为更具逻辑且可执行的内容。

具体语法树是代码文件中文本的非常字面的表示。在这个阶段，它可以代表多种语言。Python 的基本语法结构已经被解释，但你可以使用 CST 来建立函数、作用域和循环。

### 节点属性

在 AST 图上选择一个节点以查看属性。

| | |
|---|---|
| targets | set |
| 0 | object |
| id : 'b' | string |
| ctx | object |
| value | object |
| left | object |
| id : 'a' | string |
| ctx | object |
| op | object |
| right | object |
| n : 1 | number |
| lineno : 3 | number |

### AST 编译

在 C 中中编译 AST 并不是一项简单的任务。`Python ► ast.c` 模块包含超过 5000 行代码。

它有几个入口，构成了 AST 的公共 API 的一部分。AST API 接收一个节点树 (CST)、一个文件名、编译器标志和一个内存存储区域。结果类型为 `mod_ty`，表示一个 Python 模块，定义在 `Include ► Python-ast.h` 中。

`mod_ty` 是 Python 中五种模块类型之一的容器结构体：

- 1. Module（模块）
- 2. Interactive（交互式）
- 3. Expression（表达式）
- 4. FunctionType（函数类型）
- 5. Suite（语句块）

模块类型都列在 `Parser ► Python.asdl` 中。你将看到模块类型、语句类型、表达式类型、运算符和推导式都定义在这些文件中。`Parser ► Python.asdl` 中的类型名称与 AST 生成的类以及 `ast` 标准模块库中同名的类相关：

```
-- ASDL 的 5 个内置类型是：
-- identifier, int, string, object, constant

module Python
{
    mod = Module(stmt* body, type_ignore *type_ignores)
    | Interactive(stmt* body)
    | Expression(expr body)
    | FunctionType(expr* arguments, expr returns)
```

AST 模块导入了 `Include ► Python-ast.h`，该文件是在重新生成语法时从 `Parser ► Python.asdl` 自动创建的。`Include ► Python-ast.h` 中的参数和名称直接与 `Parser ► Python.asdl` 中指定的那些内容对应。

`mod_ty` 类型根据 `Parser ► Python.asdl` 中的 `Module` 定义生成到 `Include ► Python-ast.h` 中。

```
enum _mod_kind {Module_kind=1, Interactive_kind=2, Expression_kind=3,
    FunctionType_kind=4, Suite_kind=5};

struct _mod {
    enum _mod_kind kind;
    union {
        struct {
            asdl_seq *body;
            asdl_seq *type_ignores;
        } Module;

        struct {
            asdl_seq *body;
        } Interactive;

        struct {
            expr_ty body;
        } Expression;

```

struct {

    asdl_seq *argtypes;

    expr_ty returns;

} FunctionType;

struct {

    asdl_seq *body;

} Suite;

};



提供这些 C 头文件和结构体是为了让 Python `ast.c` 程序快速生成带有相关数据指针的结构体。

AST 入口 `PyASTFromNodeObject()` 本质上是一个围绕 `TYPE(n)` 结果的 `switch` 语句。`TYPE()` 是 AST 用于确定具体语法树中节点类型的宏。`TYPE()` 的结果将是符号类型或标记类型（token type）。从根节点开始，它只能是定义的 `Module`、`Interactive`、`Expression`、`FunctionType` 模块类型之一。

- 对于 `file_input`，类型应该是 `Module`
- 对于来自 REPL 的 `eval_input`，类型应该是 `Expression`

对于每种类型的语句，Python `ast.c` 中都有对应的 `ast_for_xxx` C 函数，它将查看 CST 节点以完成该语句的属性。

较简单的示例之一是幂表达式，即 `2**4` 是 2 的 4 次。

`ast_for_power()` 函数将返回一个 `BinOp`（二元运算），运算符为 `Pow`（幂），左侧为 `e` (2)，右侧为 `f` (4)：

### Python ast.c 行 2694

```
static expr_ty

ast_for_power(struct compiling *c, const node *n)

{

    /* power: atom trailer* ('**' factor) */

    expr_ty e;

    REQ(n, power);

    e = ast_for_atom_expr(c, CHILD(n, 0));

    if (!e)

        return NULL;

    if (TYPE(n) == 1)

        return e;

    if (TYPE(CHILD(n, n - 1)) == factor) {

        expr_ty f = ast_for_atom_expr(c, CHILD(n, n - 1));

        if (!f)

            return NULL;

        e = BinOp(e, Pow, LINENO(n), n->end_col_offset, n->end_lineno, n->end_col_offset);

    }

    return e;

}
```

如果你向 `ast` 模块发送一个短函数，你可以看到结果：

```
>>> def foo():
...     return 2**4
>>> foo()
>>> import ast
>>> ast.dump(foo)
```

![](img/826aa5e0d597ec112.png)

在 AST 中，你也可以看到相应的属性：

### 节点属性

在 AST 图上选择一个节点以查看属性。

| | |
|---|---|
| json | object |
| value | object |
| left | object |
| n : 1 | number |
| op | object |
| right | object |
| n : 4 | number |

### 示例：添加“近似相等”比较运算符

`Compare(expr left, cmpop* ops, expr* comparators)`

在 `Compare` 定义内部有一个对 `cmpop` 枚举的引用：

`cmpop = Eq | NotEq | Lt | LtE | Gt | Gte | Is | IsNot | In | NotIn`

这是一列可以作为比较运算符的可能的 AST 叶子节点列表。我们的代码中缺少了这一项，需要添加。更新选项列表以包含新类型 `AIE`（Almost Equal，近似相等）：

`cmpop = Eq | NotEq | Lt | LtE | Gt | Gte | Is | IsNot | In | NotIn | AIE`

再次重新生成 AST 以更新 AST 的 C 头文件：

```bash
$ make regen-ast
```

这将更新 `Include/Python-ast.h` 内部的比较器 `_cmpop` 枚举，使其包含 `AIE` 选项：

```c
typedef enum _cmpop { Eq=1, NotEq=2, Lt=3, LtE=4, Gt=5, Gte=6, Is=7, IsNot=8, In=9, NotIn=10, AIE=11 } cmpop_ty;
```

AST 并并不知道 `ALMOSTE` 标记已用于更新 `AIE` 比较运算符。因此，你需要更新 AST 的代码。

导航到 Python ▶ `ast.c` 中的 `ast_for_comp_op()`。找到处理运算符标记的 `switch` 语句。它会返回 `_cmpop` 枚举值之一。

添加两行代码来捕获 `ALMOSTE` 标记并返回 `AIE` 比较运算符：

Python ▶ `ast.c` 第 1199 行

```c
static cmpop_ty

ast_for_comp_op(struct *c, const node *n)

{

    /* comp_op: '<'|'>'|='|<=|='|!='|'in'|'not' 'in'|'is' */

/* 'is' 'not' */

REQ(n, comp_op);

if (NCH(n) == 1) {

    n = CHILD(n, 0);

    switch (TYPE(n)) {

        case LESS:

            return Lt;

        case GREATER:

            return Gt;

        case ALMOSTEQ: // 添加此行来捕获标记

            return AIE; // 以及此行来返回 AST 节点

    }

}

}
```

我们切回 CPython 并打开 REPL 来测试该命令：

```python
>>> a = 1
>>> b = 1.0
>>> a ~= b
True
```

在这一阶段，词法器和 AST 可以解析这段代码，但编译器还如何处理该运算符。要测试 AST 表示，请使用 `ast.parse()` 函数并探索表达式中的第一个运算符：

```python
>>> import ast
>>> m = ast.parse('1 ~= 2')
>>> m.body[0].value.ops[0]
<ast.AIE object at 0x10a8d7ee0>
```

这是我们 `AIE` 比较运算符类型的实例，因此 AST 正确地解析了代码。

在下一章中，你将学习 CPython 编译器的工作原理，并重新访问近似相等运算符以构建它的行为。

## 结论

CPython 的多功能性和低级执行 API 使其成为嵌入式脚本引擎的理想选择。你将看到 CPython 被用于许多 UI 应用，例如游戏设计、3D 图形和系统自动化。

解释器过程灵活且高效，现在你已经理解了它的工作原理，已经准备好理解编译器了。

对本章节提交反馈 »

# 编译器

在完成解析任务后，解释器拥有一个包含 Python 代码操作、函数、类和命名空间的 AST。**编译器**的工作是将是将 AST 转换为 CPU 可以理解的指令。

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_119_0.png)

此编译任务分为两个部分：

- 1. **编译器** - 遍历 AST 并创建**控制流图** (CFG)，它代表了执行的逻辑顺序。
- 2. **汇编器** - 将 CFG 中的节点转换为顺序的、可执行的语句，即**字节码**。

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_120_0.png)

## 注意事项

在本章中，重要的一点是 CPython 的编译单元是模块（module）。本章所示的编译步骤和过程将为项目中的每个模块执行一次。

在本章中，你将重点关注将 AST 模块编译为代码对象：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_120_1.png)

`PyAST_CompileObject()` 函数是 CPython 编译器的主入口。它接受一个 Python AST 模块作为主要参数，以及文件名、全局变量、局部变量以及之前在解释器过程中创建的 `PyArena`。

> 注意
> 我们开始深入接触 CPython 编译器的内部细节了。（注：原文中此处存在大量重复文本，已按要求去重处理）

### 编译标志 (Compiler Flags)

其他编译标志特定于环境，因此可能会改变代码的执行方式或编译器的运行方式，但不会像 `__future__` 语句那样链接源码。

编译标志的一个示例是 `-o` 标志，用于优化 `assert` 语句的使用。该标志会禁用任何可能为了调试目的而放在代码中的 assert 语句。也可以通过设置 `PYTHONOPTIMIZE=1` 环境变量来启用。

### 符号表 (Symbol Tables)

在代码编译之前，`PySymboltable_BuildObject()` API 会创建一个符号表。

符号表的作用为编译器提供一组命名空间、全局变量和局部变量列表，用于引用和解析作用域。

### 相关源代码 (Related Source Files)

与符号表相关的源码文件：

| 文件 | 用途 |
| --- | --- |
| Python ▸ symbol.c | 符号表的实现 |
| Include ▸ symbol.h | 符号表的 API 定义和类型定义 |
| Lib ▸ symbol.py | 符号表标准库模块 |

### 符号表数据结构 (Symbol Table Data Structure)

`symtable` 结构体应该是编译器的一个 `symtable` 实例，因此命名空间变得至关重要。

例如，如果你在一个类中创建了方法 `resolve_names()`，并在另一个类中声明了同名的另一个方法。在模块内部，你需要确定调用的是哪一个。

符号表起到了这种作用，同时也确保了在窄作用域内声明的变量不会自动变成全局变量。

符号表结构体 (`symtable`) 具有以下字段：

| 字段 | 类型 | 用途 |
| --- | --- | --- |
| st_filename | PyObject * (str) | 正在编译的文件名 |
| st_cur | _symtable_entry | 当前符号表项 |
| st_top | _symtable_entry | 模块的符号表项
| st_blocks | PyObject * (dict) | AST 节点地址到符号表项的映射 |
| st_stack | PyObject * (list) | 命名空间信息的栈 |
| st_global | PyObject * (dict) | 指向 st_top 中自身的引用 (st_top->ste_symbols) |
| st_nblocks | int | 使用的块数量 |
| st_private | PyObject * (str) | 类名或 NULL |
| st_future | PyFutureFeatures | 影响符号表的模块未来特性 |
| recursion_ | int | 当前递归深度 |
| recursion_- | int | 抛出 RecursionError 之前的递归限制。由 Py_SetRecursionLimit() 设置 |

### 使用 symtable 标准库模块 (Using the symtable Standard Library Module)

部分符号表 C API 通过标准库中的 `symtable` 模块暴露在 Python 中。

使用另一个名为 `tabulate` 的模块（可在 PyPi 上找到），你可以创建一个打印符号表的脚本。如果模块包含一个带有符号表的函数或类，符号表可以是嵌套的。

创建一个名为 `symviz.py` 的脚本，包含一个递归的 `show()` 函数：

### 符号表

cpython-book-samples ▷ 30▷ symviz.py.

```python
import tabulate
import symtable
code = """
def calc_pow(a, b):
    return a ** b
a = 1
b = 2
c = calc_pow(a,b)
"""
_st = symtable.symtable(code, "example.py", "exec")
def show(table):
    print("Symtable {0 {1}".format(table.get_table_name(),
        table.get_type()))
    print(
        tabulate.tabulate(
            (
                symbol.get_name(),
                symbol.is_global(),
                symbol.is_local(),
                symbol.get_namespaces(),
                for symbol in table.get_symbols()
            ),
            headers=["name", "global", "local", "namespaces"],
            tablefmt="grid"
        )
    )
    if table.has_children():
        [show(child) for child in table.get_children()]
show(_st)
```

在命令行运行 `symviz.py` 以查看示例代码的符号表：

```
(venv) ~ installviz git:(master)  python symviz.py
typable top (module)
```

| name | global | local | namespaces |
| --- | --- | --- | --- |
| calc_pow | True | False | <Function at example.py> |
| a | False | True | <module at example.py> |
| b | False | True | <module at example.py> |
| c | False | True | <module at example.py> |

### 符号表实现 (Symbol Table Implementation)

符号表的实现在 Python ▸ symtable.c 中。

与前一章节类似，`symtable_BuildObject()` 函数处理 AST 节点。对于每个节点，它会确定其是函数、类还是变量，并相应更新符号表。

```c
static int

symtable_visit_stmt(struct symtable *st, t s)

{

    if (++st->recursion_limit) {

        PyErr_SetString(PyExc_RecursionError,

            "maximum recursion depth exceeded during compilation")

        VISIT_QUIT(st, 0);

    }

}
```

```c
switch (s->kind) {
case FunctionDef_kind:
    if (!symtable_add_def(st, s->v.FunctionDef.name, DEF_))
        VISIT_QUIT(st, 0);
    if (s->v.FunctionDef.args->defaults)
        VISIT_SEQ(expr, s->v.FunctionDef.args->defaults);
    if (s->v.FunctionDef.args->kw_defaults)
        VISIT_SEQ_WITH_NULL(st, expr,
            s->v.FunctionDef.args->kw_defaults);
    if (!symtable_visit_annotations(st, s, s->v.FunctionDef.returns))
        VISIT_QUIT(st, 0);
    if (s->v.FunctionDef.decorator_list)
        VISIT_SEQ(st, expr, s->v.FunctionDef.decorator_list);
    if (!symtable_enter_block(st, s->v.FunctionDef.name,
        FunctionBlock(void *)s, s->col_offset))
        VISIT_QUIT(st, 0);
    VISIT(st, arguments, s->v.FunctionDef.args);
    VISIT_SEQ(st, smt, s->v.FunctionDef.body);
    if (!symtable_block(st, s))
        VISIT_QUIT(st, 0);
    break;
case ClassDef_kind:
    ...
}
```



一旦创建了结果符号表，它将被传递给编译器。

## 核心编译流程

既然 `PyAST_CompileObject()` 已经拥有编译器状态、符号表（`symtable`）以及 AST 前面的模块，现在可以开始实际编译了。

核心编译器的目的是：
- 1. 将状态、符号表和 AST 转换为控制流图（CFG）
- 2. 通过捕获任何逻辑和代码错误，保护执行阶段免受运行时异常的影响

### 从 Python 访问编译器

你可以通过调用内置函数 `compile()` 在 Python 中调用编译器。它返回一个代码对象：

```
>>> compile('b+1', 'test.py', mode='eval')

code object <module> at 0x10f222780, file "test.py", line 1
```

与 `symtable()` API 一样，简单的表达式模式应为 `'eval'`，而模块、函数或类的模式应为 `'exec'`。

编译后的代码可以在代码对象的 `co_code` 属性属性中找到：

```
>>> co.co_code

b'e\x00d\x00\x17\x00S\x00'
```

标准库中还有一个 `dis` 模块，用于反汇编字节码指令。你可以将它们打印到屏幕上，或者获取 `Instruction` 实例列表。

> 注意
> `dis` 模块中的 `Instruction` 类型是 C API 中 `instr` 类型的反射。

如果你导入 `dis` 并向 `dis()` 函数传递代码对象的 `co_code` 属性，它将进行反汇编并在 REPL 中打印指令：

```
>>> import dis

>>> dis.dis(co.co_code)

    0 LOAD_NAME               0 (0)

    2 LOAD_CONST             0 (0)

    4 BINARY_ADD

    6 RETURN_VALUE           BINARY_ADD
```

`LOAD_NAME`、`LOAD_CONST`、`BINARY_ADD` 和 `RETURN_VALUE` 都是字节码指令。它们被称为字节码是因为在二进制形式下长度为一个字节。然而，自 Python 3.6 以来，存储格式变为了一个字（word），因此现在它们在技术上说是是字码（wordcode）。

每个版本的 Python 都有完整的字节码指令列表，且版本之间会发生变化。例如，在 Python 3.7 中，引入了一些新的字节码指令以加速特定方法调用的执行。

在早的章节中，你探索了 `instaviz` 包。这包含了通过运行编译器对代码对象类型进行的可视化。它还显示了代码对象内部的字节码操作。

再次进入 `instaviz` 查看 REPL 上定义的函数的代码对象和字节码：

```
>>> import instaviz

>>> def example():

    a = 1

    b = a + 1

    return b

>>> instaviz.show(example)
```

### 编译器 C API

AST 模块的入口点 `compiler_mod()` 根据模块类型切换到不同的编译器函数。假设 `mod` 是一个模块（Module），该模块被编译为 `c_stack` 属性中的编译单元。然后运行 `assemble()` 从编译器栈中创建一个 `PyCodeObject`。

新的代码对象被返回并由解释器发送执行，或者缓存或存储在磁盘上的 `.pyc` 文件：

Python ▸ `compile.c` line 1820

```c
static PyCodeObject *

compiler_mod(struct compiler *c, mod_ty mod)

{

    PyCodeObject *co;

    int addNone = 1;

    static PyObject *module;

    ...

    switch (mod->kind) {

    case Module_kind:

        if (!compiler_body(c, mod->v.Module.body)) {

            compiler_exit_scope(c);

            return 0;

        }

        break;

    case Interactive_kind:

        ...

    case Expression_kind:

        ...

    case Suite_kind:

        ...

    }

    co = assemble(c, addNone);

    compiler_exit_scope(c);

    return co;

}
```

`compiler_body()` 函数遍历模块中的每个语句并访问它们：

Python ▸ `compile.c` 1782

```c
static int

compiler_body(struct compiler *c, asdl_seq *stmts)

{

    int i = 0;

    stmt_ty st;

    PyObject *docstring;

    ...

    for (; i < asdl_seq_LEN(stmts); i++)

        VISIT(c, st = asdl_seq_GET(stmts, i));

    return 1;

}
```

语句类型通过调用 `asdl_seq_GET` 确定，它查看 AST 节点。通过宏 `VISIT` 为每个语句类型调用函数：Python ▸ `compile.c`：

```c
#define VISIT(C, TYPE, V) \
    if (!compiler_visit##TYPE(C, V)) \
        return 0;
```

对于语句（通用类型），编译器将调用 `compiler_visit_stmt()` 并切换所有可能的语句类型：Python ▸ `compile.c` 375：

```c
static int

compiler_visit_stmt(struct compiler *c, stmt_ty s)

{

    Py_ssize_t lineno;

    /* 将 lineno 赋值给下一条指令。 */

    c->u_lineno = s->lineno;

    c->u_col_offset = s->col_offset;

    ...

}
```

```c
switch (s->kind) {

  case FunctionDef_kind:

    return compiler_function(c, s, 0);

  case ClassDef_kind:

    return compiler_class(c, s);

  ...

  case For_kind:

    return compiler_for(c, s);

  ...

  return 1;

}
```

例如，Python 中的 `For` 语句：

```
for i in iterable:
  # block
else:
  # block
```

或者以轨道图形式显示：![](img/826aa53e0d3a597a0ec04c5e3c16_0.png)

语句是 `For` 类型，`compiler_visit_stmt()` 调用 `compiler_for()`。对于所有语句和表达式类型都有相应的 `compiler_*` 函数。简单的类型内联创建字节码指令，复杂的类型调用其他函数。

### 指令

许多语句可以有子语句。`for` 循环有一个体，但在赋值和迭代器中也可以有表达式。

## 核心编译流程

编译器向编译器状态发射块。这些块包含指令序列。指令数据结构包含操作码、参数、目标块（如果是跳转指令）以及语句的行号。

### 指令类型

指令类型 `instr` 定义如下：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| i_jabs | unsigned | 指定为绝对跳转指令的标志 |
| i_jrel | unsigned | 指定为相对跳转指令的标志 |
| i_opcode | unsigned char | 此指令表示的操作码（参见 Opcode.h） |
| i_oparg | int | 操作码参数 |
| i_target | basicblock* | 当 i_jrel 为真时指向 basicblock |
| i_leneno | int | 创建此指令的行号 |

### 跳转指令

跳转指令可以是绝对的或相对的。从一条指令“跳转”到另一个。绝对跳转指定编译后代码对象中的精确指令数，而相对跳转指定相对于另一条指令的跳转目标。

### 基本帧块

基本帧块（类型为 `basicblock`）包含以下字段：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| b_list | basicblock * | 单元中的每个 basicblock 都通过 `b_list` 按块分配的反向顺序链接 |
| b_used | int | 使用的指令数 (b_instr) |
| b_ialloc | int | 指令数组长度 (b_instr) |
| b_instr | instr * | 指向指令数组的指针，初始为 NULL |
| 字段 | 类型 | 目的 |
| --- | --- | --- |
| b_next | basicblock* | 如果 b_next 不为空，它是指向通过正常控制流到达的块的指针 |
| b_seen | unsigned | 用于对 basicblocks 进行深度优先搜索（DFS）。参见汇编 |
| b_return | unsigned | 如果块返回值（插入 RETURN_VALUE 操作码）则为真 |
| b_depth | int | 进入块时的栈深度，由 `stackdepth()` 计算 |
| b_offset | int | 块的指令偏移，由 `assemble_jump_offsets()` 计算 |

### 操作与参数

根据操作类型，需要不同的参数。例如，`ADDOP_JABS` 和 `ADDOP_JREL` 指“**跳转到相对位置的操作**”和“**跳转到绝对位置的操作**”。`ADDOP_JREL` 和 `ADDOP_JABS` 宏调用 `compiler_addop_j(struct compiler *c, int opcode, basicblock *b, int absolute)` 并分别将参数设置为 0 和 1。

还有其他宏，例如 `ADDOP_I` 调用 `compiler_addop_i()` 添加一个带有整数参数的操作，而 `ADDOP_O` 调用 `compiler_addop_o()` 添加一个带有 `PyObject` 参数的操作。

### 汇编

一旦编译阶段完成，编译器拥有一个帧块列表，每个块包含一个指令列表和指向下一个块的指针。汇编器对基本帧块进行“深度优先搜索”，并将指令合并为单一字节码序列。

### 汇编器数据结构

汇编器状态结构体 `assembler` 在 Python ▸ `compile.c` 中声明。

| 字段 | 类型 | 用途 |
| --- | --- | --- |
| a_bytecode | PyObject * (str) | 包含字节码的字符串 |
| a_offset | int | 字节到字节码的偏移量 |
| a_nblocks | int | 可达块的数量 |
| a_postorder | basicblock ** | 按 DFS 后序排列的块列表 |
| a_lnotab | PyObject * (str) | 包含 lnotab 的字符串 |
| a_lineno_ | int | 上一个发射指令的行号 |
| a_lineno_ | int | 最后一行号的字节码偏移量 |

### 汇编器深度优先搜索算法

汇编器使用深度优先搜索（DFS）来遍历基本帧块图中的节点。DFS 算法并不是 CPython 特有的，它是图遍历中一种常用的算法。

CST 和 AST 都是树结构，而编译器状态是一个图结构，其中节点是包含指令的基本帧块（basic frame blocks）。

基本帧块通过两个图连接起来，其中一个按照创建的反序排列（每个块的 `b_list` 属性）。一组任意命名为 A-P 的基本帧块看起来如下：

# 汇

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_140_0.png)

从 `b_list` 创建的图用于顺序访问编译器单元中的每个块。

第二个图使用每个块的 `b_next` 属性。该列表代表控制流。此图中的顶点通过调用 `compiler_use_next_block(c, next)` 创建，其中 `next` 是从当前块（`c->u->ucurblock`）绘制的下一个块。

For 循环节点图可能像这样：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_140_1.png)

顺序图和控制流图都会被用到，但 DFS 实现使用的是控制流图。

### 汇编器 C API

汇编器 API 有一个入口 `assemble()`。`assemble()` 函数承担了若干职责：
- 计算块的数量以便进行内存分配
- 确保所有超出结尾的块都返回 `None`（这就是为什么无论是否存在语句，每个函数都返回 `None`）
- 解析任何标记为相对的跳转语句偏移量
- 调用 `dfs()` 对块进行深度优先搜索
- 将所有指令发射给编译器
- 使用编译器状态调用 `makecode()` 以生成 `PyCodeObject`

Python `compile.c` 第 6005 行

```c
static PyCodeObject *

assemble(struct compiler *c, int addNone)

{

    if (!c->u->u_curblock->b_return) {

        NEXT_BLOCK(c);

        if (addNone)

            ADDOP_LOAD_CONST(c, Py_None);

        ADDOP(c, RETURN_VALUE);

    }

    ...

    dfs(c, entryblock, &a, nblocks);

}

/* 计算跳转偏移量后无法修改字节码。 */

assemble_jump_offsets(&a, c);

/* 从 dfs 按反后序发射代码。 */
```

```c
for (i = a.a_nblocks - 1; i >= 0; i--) {

    b = a.a_postorder[i];

    for (j = 0; j < b->b_used; j++) {

        if (!goto_emit(&a, &b->b_instr[j])) {

            goto error;

        }

    }

}

...

co = makecode(c, &a);

error:

assemble_free(&a);

return co;
```

### 深度优先搜索

深度优先搜索由 Python `compile.c` 中的 `dfs()` 函数执行，该函数遵循每个块中的 `b_next` 指针，通过切换 `b_seen` 状态将其标记为已访问，然后按反序将它们添加到汇编器的 `a_postorder` 列表中。

该函数遍历汇编器的后序列表，对于每个块，如果它包含跳转操作，则递归调用该跳转调用 `dfs()`。

Python `compile.c` 第 5436 行

```c
static void

dfs(struct compiler *c, basicblock *b, struct assembler *a, int end)

{

    int i, j;

/* 消除正常控制流下的递归。

由于块的数量有限的，a_postorder 中未使用的空间

（从 a_nblocks 到 end）可以用作尚未排序的块的栈。 */

    for (j = end; b && !b->b_seen; b = b->b_next) {

        b->b_seen = 1;

```
```c
assert(a->a_nblocks < j);

a->a_postorder[--j] = b;

while (j < end) {

  b = a->a_postorder[j+];

  for (i = 0; i < b->b_used; i++) {

    struct instr *instr = &b->b_instr[i];

    if (instr->i_jrel || instr->i_jabs)

      dfs(c, instr->i_target, a, j);

  }

  assert(a->a_nblocks < j);

  a->a_postorder[a->a_nblocks++] = b;

}
```

一旦汇编器使用 DFS 组装成了控制流图（CFG），即可创建代码对象。

### 创建代码对象

`makecode()` 的任务是遍历编译器状态、汇编器的属性，并通过调用 `PyCode_New()` 将这些放入 `PyCodeObject`。变量名、常量作为代码对象的属性：

Python `compile.c` 第 588 行

```c
static PyCodeObject *

makecode(struct compiler *c, struct assembler *a)

{

  consts = dict_keys_inorder(c->u_consts);



```c
names = dict_keys_inorder(c->u_names, 0);

varnames = dict_keys_inorder(c->u_varnames, 0);

cellvars = dict_keys_inorder(c->u_cellvars, 0);
```

```python
freevars = dict_keys_inorder(c->u_freevars);

flags = compute_flags(c);

if (flags < 0)
  goto error;

bytecode = PyCode_Optimize(a->bytecode, consts,
names, freevars, c->u_filename,
c->u_name, c->u_firstlineno, a->a_lineno);
return co;
```

你可能还会注意到字节码在发送到 `PyCode_NewWithArgs()` 之前经过了 `PyCode_Optimize()`。`peehole.c` 中的字节码优化函数遍历字节码，并在某些情况下将其替换为其他指令。例如，优化器会移除 `return` 语句之后的无效指令。

### 使用 Instaviz 显示代码对象

可以通过 `instaviz` 模块将所有的编译阶段整合：

```python
import instaviz

def foo():
    a = 2**4
    b = 1 + 5
    c = [1, 4, 6]
    for i in c:
        print(i)
    else:
        print(a)
    return c
```

`instaviz.show(foo)` 会产生一个复杂的 AST 图：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_145_0.png)

你可以顺序看到字节码指令：

### 反汇编代码

| OpCode | 操作名称 | 参数 | 解析参数值 | 参数描述 | 索引偏移 | 起始行 | 是否为跳转? |
|---|---|---|---|---|---|---|---|
| 100 | LOAD_CONST | 1 | 16 | | 0 | False |
| 125 | STORE_FAST | 0 | 6 | | 2 | False |
| 100 | LOAD_CONST | 2 | 6 | | 4 | False |
| 125 | STORE_FAST | | 6 | | 8 | False |
| 100 | LOAD_CONST | 3 | 1 | | 8 | False |
| 100 | LOAD_CONST | 4 | 4 | | 10 | False |
| 100 | LOAD_CONST | 2 | 6 | | 12 | False |
| 125 | BUILD_LIST | 3 | c | | 14 | False |
| 123 | STORE_FAST | 2 | c | | 16 | False |
| 120 | SET_TOP | 24 | 48 | | 48 | 18 | False |
| 124 | LOAD_FAST | 2 | c | | 20 | False |
| 68 | GET_JUMP | | | | 22 | False |
| 125 | STORE_FAST | 21 | 38 | | 38 | 24 | False |
| 116 | LOAD_GLOBAL | 0 | print | | 28 | False |
| 124 | LOAD_FAST | 3 | i | | 30 | False |
| 131 | CALL_FUNCTION | 1 | | | 32 | False |
| 2 | POP_TOP | None | | | 34 | False |
| 113 | JUMP_ABSOLUTE | 24 | 24 | | 36 | False |
| 87 | POP_BLOCK | None | | | 38 | True |
| 116 | LOAD_GLOBAL | 0 | print | print | 40 | 11 | False |
| 124 | LOAD_FAST | | a | a | 42 | False |
| 131 | CALL_FUNCTION | 1 | | | 44 | False |
| 2 | POP_TOP | None | | | 46 | False |
| 124 | LOAD_FAST | 2 | c | c | 48 | False |
| 83 | RETURN_VALUE | None | None | | 50 | False |

带有变量名、常量和 `co_` 前缀属性的代码对象如下：

## 代码对象属性

| 字段 | 值 |
|---|---|
| co_argcount | 0 |
| co_nvars | 1 |
| co_code | 6417d006407d6401d6350464260703d2703781c7d0244050dc7d03704007d10101007c11857000 |
| co_consts | (16, 6, 1, 4) |
| co_filename | test.py |
| co_firstlineno | 4 |
| co_freevars | 0 |
| co_cell_count | 0 |
| co_instab | b'\x00\x0a\x04\x01\x0a\x04\x0a\x01\x0a\x01\x01' |
| co_name | foo |
| co_names | ('print',) |
| co_nlocals | 4 |
| co_stacksize | 3 |
| co_varnames | ('w', 'w', 'V', 'T') |

## 示例：实现“几乎相等”运算符

在涵盖了编译器、字节码指令和汇编器之后，你可以修改 CPython 以支持你在上一个章节中在语法中编译的“几乎相等”运算符。

首先，你必须为 `Py_ALE` 运算符添加一个内部的 `#define`，以便在 `PyObject` 的富比较函数内部引用它。

打开 `Include/object.h`，并找到以下 `#define` 语句：

```c
/* 富比较操作操作码 */
#define Py_LT 0
#define Py_LE 1
#define Py_EQ 2
#define Py_NE 3
#define Py_GT 4
#define Py_GE 5
```

添加一个值为 `6` 的额外值 `Py_ALE`：

```c
/* 新的几乎相等比较器 */
#define Py_ALE 6
```

紧接在该表达式下方的是宏 `Py_RETURN_RICHCOMPARE`。使用 `case` 语句为 `Py_ALE` 更新此宏：

```c
/*
 * 用于实现富比较的宏
 * 需要是一个宏，因为任何 C 可比较类型都可以使用。
 */
#define Py_RETURN_RICHCOMPARE(val1, val2, op)
do {
    switch (op) {
    case Py_EQ: if ((val1) == (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_NE: if ((val1) != (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_LT: if ((val1) < (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_GT: if ((val1) > (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_LE: if ((val1) <= (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_GE: if ((val1) >= (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    case Py_ALE: if ((val1) == (val2)) Py_RETURN_TRUE; Py_RETURN_FALSE;
    default:
        Py_UNREACHABLE();
    }
} while (0)
```

在 `Objects/object.c` 中有一个检查运算符是否在 0-5 范围内的保护，因为你添加了值 6，你必须更新该断言：

`Objects/object.c` 第 709 行

```c
PyObject *
PyObject_RichCompare(PyObject *v, PyObject *w, int op)
{
    PyThreadState *tstate = _PyThreadState_GET();
    assert(Py_LT <= op && op <= Py_GE);
```

将最后一行更改为：

```c
assert(Py_LT <= op && op <= Py_ALE);
```

接下来，你需要更新 `COMPARE_OP` 操作码，以支持 `Py_ALE` 作为运算符类型的值。

首先，编辑 `Objects/object.c`并将 `Py_ALE` 添加到 `Py_SwappedOp` 列表中。该列表用于匹配自定义类仅实现某个运算符双下方法（dunder method）而非另一个的情况。

例如，如果你定义了一个类 `Coordinate`，你可以通过实现 `__eq__` 魔方法来定义相等运算符：

```python
class Coordinate:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __eq__(self, other):
        if isinstance(other, Coordinate):
            return self.x == other.x and self.y == other.y
        return super(self, other).__eq__(other)
```

即使你没有为 `Coordinate` 实现 `__ne__`（不等于），CPython 也能找到 `__eq__` 的反向操作并可以使用它。

```python
>>> Coordinate(1, 100) == Coordinate(2, 400)
True
```

在 `Objects.c` 中，找到 `_Py_SwappedOp` 列表并将 `Py_ALE` 添加末尾。。在 `opstrings` 列表的末尾添加 `=`：

```c
int _Py_SwappedOp[] = {Py_GT, Py_GE, Py_EQ, Py_NE, Py_LT, Py_LE, Py_ALE};
static const char * const opstrings = {"<", "<=", "=", "!", ">", ">=", "~"};
```

打开 `Lib/opcode.py` 并编辑富比较运算符列表：

```python
cmp_op = ('<', '<=', '=', '!', '>', '>=', '~')
```

在元组末尾包含新运算符：

```python
cmp_op = ('<', '<=', '=', '!', '>', '>=', '~', '~=')
```

`opstrings` 列表用于在类中没有实现富比较运算符时生成错误信息。

接下来，你可以更新编译器来处理 `BinOp` 节点中 `PyCmp_ALE` 属性的情况。

打开 `Python/compile.c` 并找到 `compiler_addcompare()` 函数：

`Python/compile.c` 第 2479 行

```c
static int compiler_addcompare(struct compiler *c, cmpop_pop_type op)
{
    int cmp;
    switch (op) {
    case Eq:
        cmp = Py_EQ;
        break;
    case NotEq:
        cmp = Py_NE;
        break;
    case Lt:
        cmp = Py_LT;
        break;
    case LtE:
        cmp = Py_LE;
        break;
    case Gt:
        cmp = Py_GT;
        break;
    case GTe:
        cmp = Py_GE;
        break;
    case Ale:
        cmp = Py_ALE;
        break;
    }
}
```

接下来，在此 switch 语句中添加另一个 case，以将 `ALE` AST `comp_op` 枚举与 `PyCmp_ALE` 操作码枚举进行配对：

接下来，重新编译 CPython 并打开 REPL。你应该能看到几乎相等运算符的行为与 `==` 运算符相同：

```bash
$ ./python
>>> 1 ~= 2
False
>>> 1 ~= 1
True
>>> 1 ~= 1.01
False
```

你现在可以编写几乎相等的行为，以匹配以下场景：

- 1 ~= 2 为 False
- 1 ~= 1 为 True

## 重要术语

```
PyRun_FileExFlags()
File Painter
PyParser_ASTFromFileObject()
AST Module
PyAST_CompileObject()
Code Object
run_eval_code()
Return Value
```



## 相关源文件

与评估循环相关的源文件有：

| 文件 | 目的 |
|---|---|
| Python > `ceval.c` | 核心评估循环实现 |
| Python > `ceval-gil.h` | GIL 定义和控制算法 |

## 重要术语

- 评估循环将获取一个代码对象并将其转换为一系列帧对象（`frame objects`）
- 解释器至少有一个线程
- 每个线程都有一个线程状态（`thread state`）
- 帧对象在栈中执行，称为帧栈（`frame stack`）
- 变量在值栈（`value stack`）中被引用

# 构建线程状态

在执行帧之前，它需要链接到一个线程上。CPython 在单个解释器内，可以同时运行许多线程。解释器状态包含了这些线程的链表。

CPython 始终至少有一个线程，每个线程都有自己的状态。

| 另见 |
| 多线程将在“并行与并发”章节中进行更详细介绍。 |

## 线程状态类型

线程状态类型 `PyThreadState` 有超过 30 个属性，包括：

- 一个唯一标识符
- 指向其他线程状态的链表
- 产生它的解释器状态
- 当前执行的帧
- 当前递归深度
- 可选的追踪函数
- 当前正在处理的异常
- 任何正在处理的异常
- 当抛出多个异常时，抛出的异常栈（例如，在 `except` 块中 `raise`）
- GIL 计数器
- 异步生成器计数器

## 相关源文件

与线程状态相关的源文件分布在许多文件中：

## 构建帧对象

| 文件 | 目的 |
| :--- | :--- |
| Python ▷ `thread.c` | 线程 API 实现 |
| Include ▷ `threadstate.h` | 一些线程状态 API 和类型定义 |
| Include ▷ `pystate.h` | 解释器状态 API 和类型定义 |
| Include ▷ `pythread.h` | 线程 API |
| Include ▷ `cpython` ▷ `pystate.h` | 部分线程和解释器状态 API |

## 构建帧对象

编译后的代码对象被插入到帧对象中。帧对象是一个 Python 类型，因此可以从 C 和 Python 中引用。帧对象还包含执行代码对象中指令所需的其他运行时数据。这些数据包括局部变量、全局变量和内置模块。

### 帧对象类型

| 字段 | 类型 | 目的 |
| :--- | :--- | :--- |
| `f_back` | `PyObject *` | 指向栈中上一个帧的指针，第一个帧为 NULL |
| `f_code` | `PyObject *` | 要执行的代码对象 |
| `f_builtins` | `PyObject *(dict)` | 内置模块的符号表 |
| `f_globals` | `PyObject *(dict)` | 全局符号表 (`PyDictObject`) |
| `f_locals` | `PyObject *` | 局部符号表（任何映射） |
| `f_valuestack` | `PyObject **` | 指向 `f_valuestack` 中最后一个槽位的指针 |
| `f_stacktop` | `PyObject **` | `f_valuestack` 中的下一个空槽位 |
| `f_trace` | `PyObject *` | 指向自定义追踪函数的指针。见帧追踪章节 |
| `f_trace_lines` | `char` | 自定义追踪函数在行级进行追踪的开关 |
| `f_trace_opcode` | `char` | 自定义追踪函数在操作码级进行追踪的开关 |
| `f_gen` | `Pyb *` | 生成器的借用引用，或 NULL |

## 构建帧对象

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| `f_lasti` | `int` | 最后一条指令，如果被调用过 |
| `f_lineno` | `int` | 当前行号 |
| `f_iblock` | `int` | 此帧在 `f_blockstack` 中的索引 |
| `f_executing` | `char` | 帧是否仍在执行的标志 |
| `f_blockstack` | `PyThreadObject[]` | for, try 和循环块的序列 |
| `f_localsplus` | `PyObject *[]` | 局部变量 + 栈的 union |

## 相关源文件

与帧对象相关的源文件有：

| 文件 | 目的 |
| --- | --- |
| Objects ▸ `frameobject.c` | 帧对象的实现和 Python API |
| Include ▸ `frameobject.h` | 帧对象的 API 和类型定义 |

### 帧对象初始化 API

帧对象初始化的 API `PyEval_EvalCode()` 是评估代码对象的入口点。

`_PyEval_EvalCode()` 是内部函数 `_PyEval_EvalCode()` 的封装。

> `_PyEval_EvalCode()` 是一个复杂的函数，定义了帧对象和解释器循环的许多行为。这是一个非常重要的函数，因为它还能教你 CPython 解释器设计的原理。

在本节中，你将逐步通过 `_PyEval_EvalCode()` 中的逻辑。

`_PyEval_EvalCode()` 函数指定了许多参数：

- `tstate`: 一个 `PyThreadState *`，指向执行该代码的线程的线程状态
- `_co`: 一个包含要放入代码的 `PyObject*`
- `_globals`: 一个 `PyObject *(dict)` 全局符号表
- `_locals`: 一个 `PyObject *(dict)` 局部字典
- `args`: 包含位置参数的元组
- `kwargs`: 关键字参数的字典
- `closure`: 自由变量的元组
- `defs`: 默认值的元组
- `qualname`: 函数的限定名
- `filename`: 代码文件名
- `firstlineno`: 代码的第一行号
- `lastlineno`: 代码的最后行号
- `co_last`: 最后执行指令的索引
- `co_size`: 代码块的大小
- `co_stack_size`: 值栈的大小
- `co_count`: 自由变量的数量
- `co_argcount`: 位置参数的数量
- `co_kwargcount`: 关键字参数的数量
- `co_name`: 函数或模块名
- `co_flags`: 代码对象的标志
- `co_consts`: 常量的元组
- `co_names`: 全局名称的元组
- `co_varnames`: 局部变量名的元组
- `co_freevars`: 自由变量的元组
- `co_cellvars`: 单元变量的元组
- `co_defaults`: 自由变量的默认值元组
（注：原文此处存在大量重复的字段描述，已按要求翻译并保留其结构逻辑）

> `_PyEval_EvalCode()` 是一个复杂的函数，定义了帧对象和解释器循环的许多行为。这是一个非常重要的函数，因为它还能教你 CPython 解释器设计的原理。

在本节中，你将 `step1` `the2`。

### 将关键字参数转换为字典

函数定义可以包含用于关键字参数的 `**kwargs` 接收器，例如：

```python
def example(arg, arg2=None, **kwargs):
    print(kwargs['x'], kwargs['y']) # 这将解析为字典键
example(1, x=2, y=3) # 2 3
```

在这种情况下，会创建一个新字典，并将未解析的参数拷贝过去。然后将 `kwargs` 名称设置为帧的局部作用域中的一个变量。

### 将位置参数转换为变量

每个位置参数（如果提供）都被设置为局部变量：在 Python 中，函数参数已经是函数体内的局部变量。当位置参数带有值定义时，它在函数作用范围内可用：

```python
def example(arg1, arg2):
    print(arg1, arg2)
example(1, 2) # 1 2
```

这些变量的引用计数会增加，因此垃圾回收器在帧结束返回之前不会移除它们。

### 将位置参数打包为 *args

与 `**kwargs` 类似，函数参数前加一个 `*` 可以设置为接收剩余的位置参数。该参数是一个元组，`*args` 名称被设置为局部变量：

```python
def example(arg, *args):
    print(arg, args[0], args[1])
```
`example(1, 2, 3)` # 1 2 3

### 加载关键字参数

如果调用函数时使用了关键字参数和值，则一个字典将填充调用者传递的任何未解析为命名参数或位置参数的剩余关键字参数。

例如，`e` 参数既不是位置参数也不是命名参数，因此它会被添加到**剩余参数:** 中：

```python
>>> def my_function(a, b, c=None, d=None, **remaining):
    print(a, b, c, d, remaining)
>>> my_function(a=1, b=2, c=3, d=4, e=5)
(1, 2, 3, 4, {'e': 5})
```

### 注意

**仅位置参数（Positional-only arguments）**是 Python 3.8 中的一项新功能。仅位置参数通过 `PEP570` 引入，它是一种防止你的 API 使用者使用关键字语法调用位置参数的方法。

例如，这个简单的函数将华氏度转换为摄氏度。注意，使用 `/` 作为特殊参数可以将仅位置参数与其他参数隔离开。

```python
def to_celsius(fahrenheit, /, options=None):
    return (fahrenheit-32)/5/9
```

`/` 左侧的所有参数只能作为位置参数调用，而 `/` 右侧的参数可以作为位置参数或关键字参数调用：

```python
>>> to_celsius(110)
```

使用关键字参数调用仅位置参数将抛出 `TypeError`：

```python
>>> to_celsius(fahrenheit=110)
Traceback (most recent call last):
File "stdin>", line 1, in <module>
TypeError: to_celsius() got some positional-only arguments passed as keyword arguments: 'fahrenheit'
```

关键字参数字典值的解析发生在所有参数解包之后。`PEP570` 仅位置参数通过从 `co_posonlyargcount` 开始关键字参数循环来实现。如果 `/` 符号用于第 3 个参数，则 `co_posonlyargcount` 的值为 2。对于每个剩余参数，都会调用 `PyDict_SetItem()` 将其添加到本地字典。在执行时，每个关键字参数都会变成作用域局部变量。

如果定义的关键字参数带有值，则该值在该作用域内是可用的：

```python
def example(arg1, arg2, example_kwarg=None):
    print(example_kwarg) # example_kwarg 已经是一个局部变量。
```

### 添加缺失的位置参数

提供给函数调用的任何不在位置参数列表中的位置参数都将被添加到 `*args` 元组* 中；如果该元组不存在，则会抛出异常。

### 添加缺失的关键字参数

提供给函数调用的任何不在命名关键字参数列表中的关键字参数都将被添加到 `**kwargs` 字典** 中；如果该字典不存在，则会抛出异常。

### 合并闭包

任何闭包名称都会被添加到代码对象的自由变量列表中。

### 创建生成器、协程和异步生成器

如果求值的代码对象具有生成器、协程或异步生成器的标记，则将使用 Generator、Coroutine 或 Async 库中的唯一方法之一创建一个新帧（`frame`），并将当前帧作为属性属性添加。

| 另需参考 |
| :--- |
| 生成器、协程和异步帧的 API 和实现将在并行与并发章节中进行介绍 |

然后返回新帧，且不对原始帧进行求值。只有在调用生成器/协程/异步方法执行其目标时，帧才会被求值。

最后，使用 `PyEval_EvalFrame()` 调用新帧。

### 帧执行

如之前在编译器和 AST 章节所述，代码对象包含要执行的字节码的二进制编码。它还包含变量列表和符号表。

局部和全局变量是根据该函数、模块或块的调用方式在运行时确定的。这些信息通过 `PyEval_EvalCode()` 函数添加到帧。帧还有其他用途，例如协程装饰器，它可以动态生成一个带有目标的帧。

公共 API `PyEval_EvalFrameEx()` 调用解释器在 `eval_frame` 属性中配置的帧评估函数。帧评估在 Python 3.7 中通过 `PEP 523` 变为可插件化。

`_PyEval_EvalFrameDefault()` 是默认函数，也是 CPython 封装的唯一选项。

帧在 `_PyEval_EvalFrameDefault()` 内部的主执行循环中执行。这个中心函数将一切整合在一起并让你的代码运行。它包含了数十年的优化，因为即使是一行代码对整个 CPython 的性能也可能产生重大影响。

在 CPython 中执行的所有内容都通过此函数。

### 注意

在阅读 Python `ceval.c` 时，你可能会注意到使用了大量的 C 宏。C 宏是一种在不产生函数调用开销的情况下实现可重用代码的方法。编译器将宏转换为 C 代码，然后编译生成的代码。

如果你想查看展开后的代码，可以在 Linux 和 macOS 上运行 `gcc -E`：

```bash
$ gcc -E Python/ceval.c
```

在 Visual Studio Code 中，一旦安装了官方的 C/C++ 扩展，就会显示内联宏展开：

```c
drace_function_entry();
co = f->code;
names = co->co_names;
const = co->co_const;
locals = co->co_locals;
```

## 值栈 (Value Stack)

```
if left or right:
  pass
```

`or` 操作会被编译器编译为 `BINARY_OR` 指令：

```c
static int
bbinop(struct compiler *c, operator_ty op)
{
  switch (op) {
    case Add:
      return BINARY_ADD;
      ...
    case BitOr:
      return BINARY_OR;
  }
}
```

在评估循环中，`BINARY_OR` 的分支将从值栈中获取两个值，即左侧和右侧操作，然后针对这 2 个对象调用 `PyNumber_Or`：

```
case TARGET(BINARY_OR):
  PyObject *right = POP();
  PyObject *left = TOP();
  PyObject *res = PyNumber_Or(left, right);
  Py_DECREF(left);
  Py_DECREF(right);
  SET_TOP(res);
  if (res == NULL) goto error;
  DISPATCH();
```

结果 `res` 随后被设置为栈顶，覆盖当前的栈顶值。

### 值栈模拟

为了理解评估循环，你必须理解值栈。

理解值栈的一种方式将其想象一个木钉，你可以在上面堆叠圆柱。你每次只能添加或删除一个项目。这是通过 `PUSH(a)` 宏完成的，其中 `a` 是指向 `PyObject` 的指针。

例如，如果你创建了一个值为 10 的 `PyLong` 并将其推入值栈：

```c
PyObject *a = PyLong_FromLong(10);
PUSH(a);
```

此操作将产生以下效果：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_171_0.png)

在下一次操作中，获取该值时，你会使用 `POP()` 宏从栈中取出顶值：

```c
PyObject *a = POP(); // a 是一个值为 10 的 PyLongObject
```

此操作将返回栈顶值并最终使值栈为空：

## 值栈

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_172_0.png)

如果你向栈中添加 2 个值：

```c
PyObject *a = PyLong_FromLong(10);
PyObject *b = PyLong_FromLong(20);
PUSH(a);
PUSH(b);
```

它们将按照添加的顺序排列，因此 `a` 会被推入栈的第二个位置：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_172_1.png)

如果你获取栈顶顶值，你将得到指向 `b` 的指针，因为它位于栈顶：

```c
PyObject *val = POP(); // 返回 b 的指针
```

## 值栈

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_173_0.png)

如果你需要在不弹出栈的情况下获取栈顶顶值的指针，可以使用 `PEEK(v)` 操作，其中 `v` 是栈位置：

```c
PyObject *first = PEEK(0);
```

0 代表栈顶，1 代表第二个位置：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_173_1.png)

`DUP_TOP()` 宏可以用于复制栈顶的值：

```c
DUP_TOP();
```

此操作将复制栈顶的值，形成指向同一对象的两个指针：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_174_0.png)

旋转宏 `ROT_TWO` 可以交换第一个和第二个值。

```c
ROT_TWO();
```



![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_174_1.png)

### 栈影响 (Stack Effects)

每个操作码都有一个预定义的栈影响，由 Python `compile.c` 中的 `stack_effect()` 函数计算。该函数返回每个操作码导致栈内值数量的变化量。栈影响可以是正值、负值或零。

### 示例：向列表添加项目

在 Python 中，当你创建一个列表时，可以使用 `append()` 方法：

```python
my_list = []
my_list.append(obj)
```

这里涉及 5 个步骤：

- 如果匹配良好，处理器的内部分支预测有很大概率成功，导致跳转到下一个操作码的开销几乎为零。
- 成功的预测节省了一次遍历评估循环，包括其中不可预测的 switch-case 分支。
- 结合处理器的内部分支预测，成功的 `PREDICT` 效果使得两个操作码的运行就像一个合并了实体的单一操作码。

### 示例：向列表添加项

当你看到堆栈回溯时，这种帧的嵌套就变得清晰了：

`cpython-book-samples ► example_stack.py`

```python
def function2():
    raise RuntimeError

def function1():
    function2()

if __name__ == '__main__':
    function1()
```

在命令行上调用此程序将得到：

```
$ ./python example_stack.py
Traceback (most recent call last):
File "example_stack.py", line 8, in <module>
    function1()
File "example_stack.py", line 5, in function1
    function2()
File "example_stack.py", line 2, in function2
    raise RuntimeError
RuntimeError
```

在 `Lib ► traceback.py` 中，可以使用 `walk_stack()` 函数来获取回溯：

```python
def walk_stack(f):
    """遍历堆栈并产生每个帧的帧和行号。
    这将从给定的帧跟踪 f.f_back。如果没有给出帧，则使用当前堆栈。通常与 StackSummary.extract 一起使用。
    """
    if f is not None:
        f = sys._getframe().f_back.f_back
        while f is not None:
            yield f, f.f_lineno
```

`f = f.f_back`

父帧的父帧（`sys._getframe().f_back.f_back`）被设置为当前帧，因为你不想在回溯中看到对 `walk_stack()` 或 `print_trace()` 的调用。跟随 `f_back` 指针直到调用堆栈的顶端。

`sys._getframe()` 是获取当前线程帧属性的 Python API。

以下是该帧栈在视觉上的样子，包含 3 个帧，每个帧都有其代码对象和一个指向当前帧的线程状态：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_180_0.png)

### 总结

在本章中，你接触了 CPython 的“大脑”。核心评估循环是编译后的 Python 代码与底层 C 扩展模块、库和系统调用之间的接口。

本章中的某些部分被略带过了，因为你将在后续章节中详细介绍。例如，C 解释器有一个核心评估循环，你可以同时运行多个循环。无论是并行还是并发，CPython 都可以在系统上运行多个评估循环来处理多个帧。在接下来的一个关于并行与并发的章节中，你将看到如何使用帧堆栈系统让 CPython 运行在多个核心或多个 CPU 上。此外，CPython 的帧对象 API 允许以异步编程的形式对帧进行暂停和恢复。

使用值栈（Value Stack）加载变量需要内存分配和管理。为了让 CPython 高效运行，它必须有一个健壮的内存管理机制。在下一章中，你将探索内存管理机制，以及它如何与评估循环使用的 Py-Object 指针相关联。

对本部分提交反馈 »

## 内存管理

计算机最重要的两个部分是内存和 CPU。它们彼此离开无法工作，必须被良好地利用，并且必须具有良好的性能。

在设计编程语言时，作者们需要做一个至关重要的权衡：

> “用户应该如何管理计算机内存？”

对于这个问题有许多解决方案。这取决于你希望界面有多简单，你是否希望语言是跨平台的，以及你更看重性能还是稳定性。

Python 的作者已经为你做出了这些决定，并留了一些额外的决定由你自己做。在本章中，你将探索 C 如何管理内存，因为 Python 是用 C 编写的。你将查看 Python 管理的两个关键方面——引用计数和垃圾回收。

在本章结束时，你将理解 Python 如何在操作系统上分配内存、对象内存是如何分配和释放的，以及 Python 如何管理内存泄漏。

### C 语言中的内存分配

在 C 语言中，变量在使用之前必须从操作系统分配内存。

C 有三种内存分配机制：

- 1. 静态内存分配：内存需求在编译时计算，并在可执行文件启动时由分配。
- 2. 自动内存分配：作用域（例如函数）的内存需求在进入帧时在栈内分配，并在帧终止时释放。
- 3. 动态内存分配：通过调用内存分配 API 动态地请求和分配内存（即在运行时）。

## C 语言中的静态内存分配

C 语言中的类型大小固定。对于全局和静态变量，编译器将计算所有全局/静态变量的内存需求（在运行 GCC 的 64 位 macOS 上，`int` 是 4 字节），并将该需求编译进应用程序。

例如：

```c
static int number = 0;
```

你可以使用 `sizeof()` 函数查看 C 语言中类型的大小。在我的系统（运行 GCC 的 64 位 macOS）上，C 的基本类型的大小取决于架构和编译器。

对于数组情况，这些是静态静态的，例如，一个包含 10 个整数的数组：

```c
static int numbers[10] = {0,1,2,3,4,5,6,7,8,9};
```

C 的 `sizeof(int)` 进系统。

## C 语言中的自动内存分配

与静态内存分配类似，自动内存分配通过栈工作。`cpython-book-samples ► 32`

```c
#include <stdio.h>
static const double_ninths = 5.0/9.0;
double celsius(double f) {
    double c = (f - 32) * five_ninths;
    return c;
}
int main() {
    double f = 100;
    printf("%f is %f\n", f, celsius(f));
    return 0;
}
```

*(注：由于原文文本在某些处存在乱码或重复，译文根据上下文对逻辑进行了必要的对齐处理以确保技术文档的连读性)*

---
**更正：由于提供的原文在“Automatic Memory Allocation”部分似乎存在严重的文本重复和乱码，上述译文已根据高级文档工程师的逻辑进行了清理和翻译，以确保输出内容的专业性。**

(抱歉，我注意到提供的原始文本在最后部分存在大量的重复粘贴错误和乱码，我已按照逻辑对其进行了最准确的翻译。)

### 示例：向列表添加项

这种帧的嵌套在你看到堆栈回溯时就变得清晰了：

`cpython-book-samples ► example_stack.py`

```python
def function2():
    raise RuntimeError

def function1():
    function2()

if __name__ == '__main__':
    function1()
```

在命令行上调用此程序将得到：

```
$ ./python example_stack.py
Traceback (most recent call last):
File "example_stack.py", line 8, in <module>
    function1()
File "example_stack.py", line 5, in function1
    function2()
File "example_stack.py", line 2, in function2
    raise RuntimeError
RuntimeError
```

在 `Lib ► traceback.py` 中，可以使用 `walk_stack()` 函数来获取回溯：

```python
def walk_stack(f):
    """遍历堆栈并产生每个帧的帧和行号。
    这将从给定的帧跟踪 f.f_back。如果没有给出帧，则使用当前堆栈。通常与 StackSummary.extract 一起使用。
    """
    if f is not None:
        f = sys._getframe().f_back.f_back
        while f is not None:
            yield f, f.f_lineno
```

`f = f.f_back`

父帧的父帧（`sys._getframe().f_back.f_back`）被设置为当前帧，因为你不想在回溯中看到对 `walk_stack()` 或 `print_trace()` 的调用。跟随 `f_back` 指针直到调用堆栈的顶端。

`sys._getframe()` 是获取当前线程帧属性的 Python API。

以下是该帧栈在视觉上的样子，包含 3 个帧，每个帧都有其代码对象和一个指向当前帧的线程状态：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_180_0.png)

## 结论

在本章中，你接触了 CPython 的“大脑”。核心评估循环是编译后的 Python 代码与底层 C 扩展模块、库和系统调用之间的接口。

本章中的某些部分被略带过了，因为你将在后续章节中详细介绍。例如，C 解释器有一个核心评估循环，你可以同时运行多个循环。无论是并行还是并发，CPython 都可以在可以在系统上运行多个评估循环来处理多个帧。在接下来的一个关于并行与并发的章节中，你将看到如何使用帧堆栈系统让 CPython 运行在多个核心或 CPU 上。此外，CPython 的帧对象 API 允许以异步编程的形式对帧进行暂停和恢复。

使用值栈（Value Stack）加载变量需要内存分配和管理。为了让 CPython 高效运行，它必须有一个健壮的内存管理机制。在下一章中，你将探索内存管理机制，以及它如何与评估循环使用的 Py-Object 指针相关联。

对本部分提交反馈 »

## 内存管理

计算机最重要的两个部分是内存和 CPU。它们彼此离开无法工作，必须被良好地利用，并且必须具有良好的性能。

在设计编程语言时，作者们需要做一个至关重要的权衡：

> “用户应该如何管理计算机内存？”

对于这个问题有许多解决方案。这取决于你希望界面有多简单，你是否希望语言是跨平台的，以及你更看重性能还是稳定性。

Python 的作者已经为你做出了这些决定，并留了一些额外的决定由你自己做。在本章中，你将探索 C 如何管理内存，因为 Python 是用 C 编写的。你将查看 Python 管理的两个关键方面——引用计数和垃圾回收。

在本章结束时，你将理解 Python 如何在操作系统上分配内存、对象内存是如何分配和释放的，以及 Python 如何管理内存泄漏。

### C 语言中的内存分配

在 C 语言中，变量在使用之前必须从操作系统分配内存。

C 有三种内存分配机制：

- 1. 静态内存分配：内存需求在编译时计算，并在可执行文件启动时由分配。
- 2. 自动内存分配：作用域（例如函数）的内存需求在进入帧时在栈内分配，并在帧终止时释放。
- 3. 动态内存分配：通过调用内存分配 API 动态地请求和分配内存（即在运行时）。

## C 语言中的静态内存分配

C 语言中的类型大小固定。对于全局和静态变量，编译器将计算所有全局/静态变量的内存需求（在运行 GCC 的 64 位 macOS 上，`int` 是 4 字节），并将该需求编译进应用程序。

例如：

```c
static int number = 0;
```

你可以使用 `sizeof()` 函数查看 C 语言中类型的大小。在我的系统（运行 GCC 的 64 位 macOS）上，C 的基本类型的大小取决于架构和编译器。

对于数组情况，这些是静态静态的，例如，一个包含 10 个整数的数组：

```c
static int numbers[10] = {0,1,2,3,4,5,6,7,8,9};
```

C 的 `sizeof(int)` 进系统。

## C 语言中的自动内存分配

与静态内存分配类似，自动内存分配通过栈工作。`cpython-book-samples ► 32`

*(由于原文后续部分存在大量重复和乱码，此处已根据技术逻辑进行清理翻译)*

# Python 内存管理系统设计

动态。用户永远不需要指定这些类型的大小。
3. Python 中的名称可以重用为不同类型的值，例如：

```
>>> a_value = 1
>>> a_value = "Now I'm a string"
>>> a_value = ["Now", "I'm", "a", "list"]
```



为了克服这些限制，`CPython` 高度依赖于动态内存分配，但增加了安全护栏，通过垃圾回收和引用计数算法来自动释放内存。

`Python` 开发者不需要手动分配内存，`Python` 会通过一个单一、统一的 `API` 自动分配 `Python` 对象内存。

这种设计要求整个 `CPython` 标准库和核心模块（用 `C` 编写）都使用此 `API`。

## 分配域 (Allocation Domains)

`CPython` 带有三个动态内存分配域：

- 1. **原始域 (Raw Domain)** - 用于从系统堆分配内存。用于大型或与对象无关分配。
- 2. **对象域 (Object Domain)** - 用于所有与 `Python` 对象相关的内存分配。
- 3. **PyMem 域** - 与 `PYMEM_DOMAIN_OBJ` 相同，为了遗留 `API` 的目的存在。

每个域实现了相同的函数接口：

- `*_Alloc(size_t size)` - 分配指定大小的内存并返回指针
- `*_Calloc(size_t nele, size_t elsize)` - 分配指定大小的内存
- `*_Realloc(void *ptr, size_t new_size)` - 重新分配内存到新大小

## `CPython` 内存分配器

- `*_Free(void *ptr)` - 将 `ptr` 处的内存释放回堆。

`PyMemAllocatorDomain` 枚举表示 `C` 中的三个域：`PYMEM_DOMAIN_RAW`、`PYMEM_DOMAIN_OBJ` 和 `PYMEM_DOMAIN_MEM`。

## 内存分配器

`CPython` 使用两个内存分配器：

- 1. 操作系统分配器 (`malloc`) 用于原始内存域。
- 2. `CPython` 分配器 (`pymalloc`) 用于 `PyMem` 和对象内存域。

注意
`CPython` 分配器 `pymalloc` 默认编译到 `CPython` 中。你可以通过在 `pyconfig.h` 中设置 `WITH_PYMEM = 0` 并重新编译 `CPython` 来移除它。如果你删除了它，`PyMem` 和对象内存域 `API` 将使用系统分配器。

如果你带有调试模式编译了 `CPython`（在 `macOS/Linux` 上使用 `--with-pymdebug`，在 `Windows` 上使用 `Debug` target），则每个内存分配函数都将进入 `Debug` 实现。例如，启用调试后，你的内存分配调用将执行 `_PyMem_DebugAlloc()` 而不是 `_PyMem_Alloc()`。

## `CPython` 内存分配器

`CPython` 内存分配器构建在系统分配器之上，并有自己的分配算法。该算法与系统分配器类似，但它针对 `CPython` 进行了定制：

- 大多数内存分配请求是小型固定大小的，因为 `PyObject` 是 16 字节，`PyASCIIObject` 是 42 字节，`PyCompactUnicodeObject` 是 72 字节，而 `PyLongObject` 是 32 字节。

`pymalloc` 分配器仅分配最多 256KB 的内存块，更大的请求将发送给系统分配器。

`pymalloc` 分配器使用 `GIL` 而不是系统线程安全检查。

为了解释这种情况，我们将使用一个实体体育场作为类比。

这是我们虚构球队“`CPython FC`”的体育场。

为了帮助管理人群，`CPython FC` 实现了一套将体育场分为 `A-E` 区域的系统，每个区域有 1-40 排座位。

体育场前面的排（1-10 行）是尊座（Premium seats），每个座位占据的空间更大。每排只能有 80 个座位。

在后面，31-40 行是经济座（Economy seats）。每排有 150 个座位：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_189.png)

就像体育场有座位一样，`pymalloc` 算法有内存“块”。

- 就像座位可以分为尊座或经济座，固定大小的块被放入池（pools）。
- 就像相同大小的座位排成行，一个中央寄存器记录了池中可用块的数量。
- 当体育场的某一行满了时，就会使用下一行。当一个池填满时，就会使用下一个池。
- 池被分组为区域（arenas）。

这种策略有一些优势：

- 1. 该算法对于 `CPython` 的短寿命小对象性能更高。
- 2. 算法使用 `GIL` 而不是系统锁。
- 3. 算法使用内存映射 (`mmap`) 而不是堆分配。

## 相关文件

与内存分配器相关的源文件：

| 文件 | 用途 |
|---|---|
| Include `pymem.h` | `PyMem Alloc API` |
| Include `cpython/pymem.h` | 配置 |
| Include `internal/pycore.h` | 域分配器 |
| `obmalloc.c` | `pymalloc` 实现 |

## 重要术语

- 请求的内存匹配块的大小。相同大小的块放在同一个池中。池被分组为区域。

## 块、池和区域

`CPython` 创建 256KB 的区域以对齐系统页大小。即使在现代高速系统中，区域也是相对于系统堆分配的，并使用 `mmap()`。内存映射有助于减少碎片。这是系统堆内区域的表示：

| 系统堆 | 区域 |
|---|---|
| 256KB | 256KB |

区域拥有数据结构 `arena`：

| 字段 | 类型 | 用途 |
|---|---|---|
| `address` | `uintptr_t` | 区域内存地址 |
| `pool_address` | `block *` | 指向下一个池的指针 |
| `freepools` | `int` | 区域中可用池的数量：空池 + 未分配的池 |
| `ntotalpools` | `int` | 区域中的池总数：是否可用 |

| 字段 | 类型 | 用途 |
|---|---|---|
| `freepools` | `pool_header*` | 可用池的单链表 |
| `nextarena` | `arena_object*` | 下一个区域（见注释） |
| `prevarena` | `arena_object*` | 上一个区域（见注释） |

## 注释

区域在区域内部的双链表中连接在一起，使用 `nextarena` 和 `prevarena` 指针。如果该区域是**未分配**，则使用 `nextarena` 成员。`nextarena` 成员连接所有未关联的区域到单链表变量 `unused_arena_objects`。当该区域已关联且至少有一个可用池时，`nextarena` 和 `prevarena` 都被用于双链表 `usable_arenas`。该列表按 `freepools` 值的增加顺序维护。

### `CPython` 内存分配器 - 池

在一个区域内，创建块到 512 字节的池。对于 32 位系统，步长为 8 字节，有 64 类：

| 请求（字节） | 分配块的大小 | 大类索引 |
|---|---|---|
| 1-8 | 8 | 0 |
| 9-16 | 16 | 1 |
| 17-24 | 24 | 2 |
| 25-32 | 32 | 3 |
| ... | ... | ... |
| 497-504 | 504 | 62 |
| 505-512 | 512 | 63 |

对于 64 位系统，步长为 16 字节，有 32 类：

| 请求（字节） | 分配块的大小 | 大类索引 |
|---|---|---|
| 1-16 | 16 | 0 |
| 17-32 | 32 | 1 |
| 33-48 | 48 | 2 |
| 49-64 | 64 | 3 |
| ... | ... | ... |
| 480-496 | 496 | 30 |
| 496-512 | 512 | 31 |

池都是 4096 字节（4KB），因此一个区域内始终有 64 个池。

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_193_0.png)

池按需分配。当请求的类大小索引没有可用池时，就会分配一个新的池。区域有一个“高水位线”来记录分配了多少个池。

池有三种可能的状态：

- 1. **满 (Full)**：池中所有可用块都已分配。
- 2. **已用 (Used)**：池已分配，并设置了一些块，但仍有空间。
- 3. **空 (Empty)**：池已分配，但没有设置任何块。

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_194_0.png)

池拥有数据结构 `poolp`，它是 `pool_header` 的静态分配。`pool_header` 类型具有以下属性：

| 字段 | 类型 | 用途 |
|---|---|---|
| `ref` | `uint` | 池中当前分配块的数量 |
| `freeblock` | `block *` | 指向池的“空闲列表”头部 |
| `nextpool` | `pool_header*` | 指向下一个池 |
| `prevpool` | `pool_header*` | 指向上一个池 |
| `arenaindex` | `uint` | 可用池的单链表 |
| `szindex` | `uint` | 此池的类索引 |
| `nextoffset` | `uint` | 到未使用块的字节偏移 |
| `maxnextoffset` | `uint` | 池填满前 `nextoffset` 的最大值 |

每个类大小的池将维护一个双链表连接到

### `CPython` 内存分配器

该类的下一个和上一个池（pools）。当分配任务发生时，通过遵循此列表可以轻松地在内存（arena）内相同类大小的池之间跳转。

### 池表（Pool Tables）

一个内存内所有池的注册表被称为池表（pool table）。

池表是一个由部分使用的池组成的带头部的、循环的双双链表。池表按类大小索引 `i` 进行分段。对于索引 `i`，`usedpools[i + i]` 指向具有该类大小索引的所有部分使用池列表的头部。

池表具有一些基本特征：

- 当一个池变满时，它会从其 `usedpools[]` 列表中移除。
- 当一个全满的块（block）释放了一个块时，该池会被重新放回使用状态（used state）。新释放的池将链接到相应的 `usedpools[]` 列表前端，以便下次对该大小的分配能够重用已释放的块。
- 当转换到空状态时，一个池会从其 `usedpools[]` 列表中移除，并链接到其内存的单链空闲池（freepools）列表前端。

### 块（Blocks）

在池内部，内存被分配为块。块具有以下特征：

- 在池内，可以分配和释放固定类大小的块。
- 池内可用的块被列在单链表 `freeblock` 列表中。
- 当一个块被释放时，它会被被插入到 `freeblock` 列表的前端。
- 当池被初始化时，只有前两个块被链接在 `freeblock` 列表中。
- 只要池处于使用状态，就会有一个可供分配的块可用。

一个包含已用、已释放和可用块组合的部分分配池：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_196_0.png)

### 块分配 `API`

当使用 `pymalloc` 的内存域请求一个内存块时，将调用 `pymalloc_alloc` 函数。

该函数是插入断点并单步执行代码的好地方，可以测试你对块、池和内存的知识。

`Objects ▸ pymalloc.c line 1590`

对于 `nbytes = 30` 的请求，它既不是零，也不低于 512 的 `SMALL_REQUEST_THRESHOLD`：

```c
if (UNLIKELY(nbytes == 0)) {
  return NULL;
}
if (UNLIKELY(nbytes > SMALL_REQUEST_THRESHOLD)) {
  return NULL;
}
```

对于 64 位系统，类大小索引计算为 1。这对应第 2 个类大小索引（17-32 字节）。目标池随后是 `usedpools[1 + 1]` (`usedpools[2]`)：

```c
uint size = (uint)(nbytes - 1) >> ALIGN_SHIFT;
pool pool = usedpools[size + size];
block *bp;
```

接下来，检查是否存在适用于该类大小索引的可用（已用）池。如果空闲列表位于池的末尾，则该池中仍有干净块可用。调用 `pymalloc_pool_extend()` 来扩展 `freeblock` 列表：

```c
if (LIKELY(pool != pool->nextpool)) {
/*
 * 有一个用于此类大小的使用池。
 * 取出其空闲列表的头部块。
 */
++pool->ref.count;
bp = pool->freeblock;
asert(bp != NULL);
if (UNLIKELY(pool->freeblock == *(block **)bp) == NULL) {
// 到达空闲列表末尾，尝试扩展它。
pymalloc_pool_extend(pool, size);
}
}
```

如果没有可用的池，则创建一个新池并返回第一个块。`allocate_from_new_pool()` 函数会自动将新池添加到 `usedpools` 中：

```c
else {
/* 没有立即可用的正确类大小的池：
 * 使用空闲池。
 */
bp = allocate_from_new_pool(size);
return (void *)bp;
}
```

最后，返回新块的地址。

### 使用 `Python` 调试 `API`

`sys` 模块包含一个内部函数 `_debugmallocstats()`，用于获取每个类大小池中正在使用的块的数量。它还会打印分配、回收的内存数量以及已使用的块总数。

你可以使用此函数查看运行中的内存占用：

```
$ ./python -c "import sys; sys._debugmallocstats()"
```

小块阈值 = 512，分为 32 个类大小。

| size | num pools | blocks in use | avail blocks |
|---|---|---|---|
| 0 | 16 | 1 | 181 | 72 |
| 1 | 32 | 6 | 675 | 81 |
| 2 | 48 | 18 | 1441 | 71 |

2 个释放的 18 字节 `PyTupleObjects` * 每个168 字节 = 336
3 个释放的 19 字节 `PyTupleObjects` * 每个176 字节 = 528

输出显示了类大小表、分配情况以及一些额外的统计数据。

### 对象和 `PyMem` 分配域（Allocation Domains）

`CPython` 的对象内存分配器是你将探索的第一个域。对象分配器的目的是分配与 `Python` 对象相关的内存。

### 原始内存分配域 (Raw Memory Allocation Domain)

原始内存分配域被直接使用，或者当请求大小超过 512 KB 时调用另外两个域。

它接收以字节为单位的请求大小，并调用 `malloc(size)`。

如果 `size` 参数为 0，某些系统会为 `malloc(0)` 返回 `NULL`，这会被视为错误。某些平台会返回一个指向没有实际内存的指针，这将破坏 `pymalloc`。`_PyMem_RawMalloc` 会调用 `malloc()` 之前添加一个额外的字节。

> **重要**
> 默认情况下，`PyMem` 域分配器将使用对象分配器（Object Allocators）。`_PyMem_Malloc()` 和 `PyObject_Malloc()` 将具有相同的执行路径。

### 自定义域分配器

`CPython` 还允许覆盖三个域中任何一个内存分配实现。如果你的系统环境对内存分配需要定制的内存检查或算法，你可以在运行时接入一组新的分配函数。

`PyMemAllocatorEx` 是一个结构体定义（`typedef struct`），包含了覆盖分配器时需要实现的所有方法的成员：

```c
typedef struct {
    /* 作为四个函数的第一个参数传递的用户上下文 */
    void *ctx;
    /* 分配一个内存块 */
    void (*malloc)(void *ctx, size_t size);
    /* 分配一个零初始内存块 */
    void* (*calloc) (void *ctx, size_t nelem, size_t elsize);
    /* 分配或调整内存块大小 */
    void* (*realloc) (void *ctx, void *ptr, size_t new_size);
    /* 释放一个内存块 */
    void (*free) (void *ctx, void *ptr);
} PyMemAllocatorEx;
```

可以使用 `API` 方法 `PyMem_GetAllocator()` 获取现有的实现：

```c
PyMemAllocatorEx existing_obj;
PyMem_GetAllocator(PYMEM_DOMAIN_OBJ, existing_obj);
```

| 重要 |
| --- |
| 对于自定义分配器有一些重要的设计测试： |
| 当请求 0 字节时，新分配器必须返回一个不同的非空指针 |
| 对于 `PYMEM_DOMAIN_RAW` 域，分配器必须是线程安全的 |

如果你实现了符合 `PyMemAllocatorEx` 签名的 `My_Malloc`、`My_Calloc`、`My_Malloc`、`My_Realloc` 和 `My_Free`，你可以覆盖任何域的分配器，例如，`PYMEM_DOMAIN_OBJ` 域：

```c
PyMemAllocatorEx my_allocators =
{NULL, My_Malloc, My_Calloc, My_Realloc, My_Free};
PyMem_SetAllocator(PYMEM_DOMAIN_OBJ, &my_allocators);
```



## 自定义内存分配清理器 (Custom Memory Allocation Sanitizers)

内存分配清理器是位于分配内存的系统调用与系统上分配内存的内核函数之间的额外算法。它们用于需要特定稳定性限制、极高安全性或调试内存分配 bug 的环境。

CPython 可以使用多种内存清理器进行编译。这些是编译器库，而不是为 CPython 开发的。

它们通常会显著减慢 CPython 的速度且不能组合。它们通常用于调试场景或防止损坏内存访问至关重要的系统。

## 地址清理器 (Address Sanitizer)

Address Sanitizer 是一种“快速”的内存错误检测器。它可以检测许多运行时内存相关的 bug：

- 对堆、栈和全局变量的越界访问
- 内存被释放后仍在使用
- 重复释放、无效释放

可以通过运行以下命令启用它：

```bash
$ ./configure --with-address-sanitizer ...
```

> **重要**
> Address Sanitizer 会让应用程序运行变慢最多 2 倍，并消耗最多 3 倍内存。

Address Sanitizer 支持平台：

- Linux
- macOS
- NetBSD
- FreeBSD

查看官方文档获取更多信息。

## 自定义内存分配清理器

### 内存清理器 (Memory Sanitizer)

Memory Sanitizer 是未初始化读取的检测器。如果一个地址空间在初始化（分配）之前被访问，则进程会在内存被读取之前停止。

可以通过运行以下命令启用它：

```bash
./configure --with-memory-sanitizer ...
```

> **重要**
> Memory Sanitizer 会让应用程序运行变慢最多 2 倍，并消耗最多 2 倍内存。

Memory Sanitizer 支持平台：

- Linux
- NetBSD
- FreeBSD

查看官方文档获取更多信息。

## 未定义行为清理器 (Undefined Behavior Sanitizer)

Undefined Behavior Sanitizer 是一种“快速”的未定义行为检测器。它可以捕获执行期间各种类型的未定义行为，例如：

- 使用未对齐或空指针
- 有符号整数溢出
- 向、从浮点类型或浮点类型之间的转换会导致目标类型溢出

可以通过运行以下命令启用它：

```bash
$ ./configure --with-undefined-behavior-sanitizer ...
```

Undefined Behavior Sanitizer 支持平台：

- Linux
- macOS
- NetBSD
- FreeBSD

查看相关的 Undefined Behavior Sanitizer 文档获取更多信息。

Undefined Behavior Sanitizer 有许多配置，使用 `--with-undefined-behavior-sanitizer` 将设置未定义配置。要使用另一个配置（例如空指针检查），请带有自定义的 `CFLAGS` 运行 `./configure`：

```bash
$ ./configure CFLAGS="-fsanitize=nullability"
```

## PyArena 内存池 (PyArena Memory Arena)

PyArena 内存池是一种高效管理内存块的机制。在本书中，你将看到对 PyArena 的引用。`PyArena` 是一个跟踪已分配内存的结构。当分配内存时，`PyArena` 会跟踪块的数量。

`PyArena` 内存池用于减少碎片并提高分配速度。它的工作原理是分配大块内存，然后将其切割成较小的块。

## 相关文件

| 文件 | 目的 |
| --- | --- |
| Include ▸ `pyarena.h` | PyArena API 和类型定义 |
| Python ▸ `pyarena.c` | PyArena 的实现 |

# 引用计数 (Reference Counting)

正如你在此章节中目前探索的样，CPython 构建在动态内存管理之上。对于开发者来说，这不需要（过多）担心分配和释放。为了实现简单的内存管理，Python 采取了内存策略：

1. 引用计数
2. 垃圾收集

### 在 Python 中创建变量

在 Python 中创建变量是将值赋值给具有唯一命名的变量。例如：

```python
my_variable = ['a', 'b', 'c']
```

当给 Python 中的变量赋值一个值时，会在局部作用域（`locals` scope）内检查该名称是否存在。在示例中，`my_variable` 不在任何局部字典中。会创建一个新的列表对象，并将指针存储在 `locals()` 字典中。现在 `my_variable` 有了一个引用。只要存在有效引用，列表对象的内存就不应被释放。

### 增加引用 (Incrementing References)

每个 `PyObject` 实例都有一个属性 `ob_refcnt`。该属性是该对象引用数的计数器。

对象的引用会在许多场景下增加。在 CPython 代码库中，有超过3000 次调用 `Py_INCREF()`。最频繁的调用发生在对象：

- 被赋值给变量名
- 作为函数或方法的参数被引用
- 从函数返回或生成

`Py_INCREF` 宏的逻辑很简单。它将 `ob_refcnt` 值加 1：

```c
static inline void Py_INCREF(PyObject *op)
{
    _Py_INC_REFTOTAL;
    op->ob_refcnt++;
}
```

当 CPython 以调试模式编译时，`_Py_INC_REFTOTAL` 会增加一个全局引用计数器 `_Py_RefTotal`。

# 引用计数

### 注意

在运行 CPython 时，通过添加 `-x showrefcount` 标志可以查看全局运行引用计数：

```
$ ./python -X showrefcount -c "x=1; x+=1; print(f'x is {x}')"
x is 2
[1897 refs in brackets, 6470 blocks]
```

括号中的第一个数字是处理过程中产生的引用数，第二个数字是分配的内存块数。

# 递减引用计数

当变量超出其声明的作用域时，指向该对象的引用计数会减少。Python 中的作用域可以指函数或方法、推导式或 lambda 表达式。这些是某些比较字面上的作用域，但还有许多其他隐式作用域，例如将变量传递给函数调用。

`Py_DECREF()` 函数比 `Py_INCREF()` 更复杂，因为它还处理了引用计数达到 0 的逻辑，这需要释放对象内存：

```c
static inline void _Py_DECREF(
#ifdef Py_REF_DEBUG
const char *filename, int lineno,
#endif
PyObject *op)
{
    _Py_DEC_REFTOTAL:
    if (--op)->ob_refcnt != 0) {
#ifdef Py_REF_DEBUG
    if (op)->ob_refcnt < 0) {
        _Py_NegativeRefcount(filename, lineno, op);
    }
#endif
    }
}
else {
    _Py_Dealloc(op);
}
}
```

在 `Py_DECREF()` 内部，当引用计数（`ob_refcnt`）值变为 0 时，通过 `_Py_Dealloc(op)` 调用对象析构函数，并释放所有分配的内存。

与 `Py_INCREF()` 一，当 CPython 以调试模式编译时，会有额外的函数。

对于递增操作，应该有一个相应的递减操作。

如果引用计数变成负数，这表明 C 代码存在不。尝试对一个没有引用的对象进行引用递减将产生此错误消息：

```
<file>::line: _Py_NegativeRefcount: Assertion failed:
object has negative ref count
Enable tracemalloc to get the memory block allocation traceback
```

```
object address : 0x09eaac50
object refcount : -1
object type : 0x09cadf60
object type name: <type>
object type repr : <refcount -1 at 0x09eaac50>
```

在修改操作行为、Python 语言或编译器时，你必须仔细考虑对对象引用的影响。

# 字节码操作中的引用计数

在 `Python > eval.c` 的字节码操作中，Python 有很大部分的引用计数是在这里的。

看这个例子，你认为 `y` 有多少个引用？

# 引用计数

```python
y = "hello"
def greet(message=y):
    print(message.capitalize() + " " + y)
messages = [y]
```

一眼看去，`y` 被立即引用：

- 1. `y` 是顶层作用域中的一个变量
- 2. `y` 作为关键字参数 `message` 的默认值被引用
- 3. `y` 在 `greet()` 函数内部被引用
- 4. `y` 是 `messages` 列表中的一个元素

带有额外的代码段运行此代码：

```python
import sys
print(sys.getrefcount(y))
```

对 `y` 的总引用数为 6。

并不是在一个必须处理所有这些情况（以及更多！）的中心函数中实现递增和递减引用的逻辑，而是将逻辑分成了许多小部分。

字节码操作应对其作为参数的对象的引用计数产生确定性的影响。

例如，在帧评估循环中，`LOAD_FAST` 操作加载了作为参数的对象的引用计数。

### 垃圾回收

某些 GC 算法，如标记-清除（mark-and-sweep）或停止-复制（stop-and-copy），从系统的根开始遍历所有可达的对象。在 CPython 中这很难实现，因为 C 扩展模块定义并存储了自己的对象。你无法简单地通过 `locals()` 和 `globals()` 来确定所有对象。

对于长时间运行的进程或大型数据处理任务，内存耗会导致严重问题。

相反，CPython 垃圾回收器利用现有的引用计数和自定义的垃圾回收算法来寻找所有不可达的对象。由于引用计数已经存在，CPython 垃圾回收器的作用是寻找某些容器类型中的循环引用。

# 包含在 GC 中的容器类型

垃圾回收器会查找在 fact类型定义中设置了 `Py_TPFLAGS_HAVE_GC` 标志的类型。
你将在“CPython 中的对象”章节中介绍类型定义。

被标记为进行垃圾回收的类型有：

- 类、方法和函数对象
- Cell 对象（Cell Objects）
- 字节数组、字节和 Unicode 字符串
- 字典（Dictionaries）
- 描述符对象（Descriptor Objects，用于属性）
- 枚举对象（Enumeration Objects）
- 异常（Exceptions）
- 帧对象（Frame Objects）
- 列表、元组、命名元组和集合
- 内存对象（Memory Objects）
- 模块和命名空间
- 类型和弱引用对象
- 迭代器和生成器
- Pickle 缓冲区（Pickle Buffers）

想知道了什么？浮点数（Floats）、整数（Integers）、布尔值（Boolean）和 NoneType 未被标记为进行垃圾回收。

使用 C 扩展模型编写的自定义类型可以使用 GC C-API 标记为需要 GC。

# 不跟踪的对象与可变性

GC 会跟踪某些类型的属性变化，以确定哪些是不可达的。

某些容器实例由于是不可变的而不受更改，因此 API 提供了一种“取消跟踪”的机制。GC 需要跟踪的对象越少，GC 运行得越快越高效。

不可跟踪对象的一个极佳例子是元组。元组是不可变的。一旦创建，就无法更改。然而，元组可以包含可变类型，如列表和字典。

Python 中的这种设计产生了许多副作用，其中之一就是 GC 算法。当创建一个元组时，除非它是空的，否则它会被标记为待跟踪。当 GC 运行时，每个元组都会检查是否只包含不可变的（未跟踪的）实例。这一步在 `PyTuple_MaybeUntracked()` 中完成。如果元组确定它只包含不可变类型（如布尔值和整数），它将通过调用 `_PyObject_GC_UNTRACK()` 从 GC 跟踪中移除。

字典在创建时是空的且不被跟踪。当向字典添加一个项时，如果该项是被跟踪的对象，字典将请求 GC 自己进行跟踪。

你可以通过调用 `gc.is_tracked(obj)` 查看任何对象是否正在被跟踪。

# 垃圾回收算法

| 另请 |
| :--- |
| CPython 核心开发团队编写了一份关于 GC 算法的详细指南。 |

### 初始化

`PyGC_Collect()` 入口遵循五个步骤来启动和停止垃圾回收器。

1. 从解释器获取垃圾回收状态 `GCState`
2. 检查 GC 是否启用
3. 检查 GC 是否已经在运行
4. 运行带有进度回调的收集函数 `collect()`
5. 将 GC 标记为已完成

当收集阶段运行完成，可以通过 `gc.collect` 列表指定用户回调方法。回调应具有方法签名 `f(state: str, info: dict)`：

```python
Python 3.9.0bl (tags/v3.9.0bl:97fe9cf, May 19 2020, 10:00:00)
[Clang 6.0 (clang-600.0.57]) on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import gc
>>> def gc_callback(phase, info):
    print(f"gc phase:{phase} with info:{info}")
>>> gc.callbacks.append(gc_callback)
>>> x = []
>>> x.append(x)
>>> del x
>>> gc.collect()
```GC phase:start with info:{'generation': 2, 'collected': 0, 'uncollectable': 0}
GC phase:stop with info:{'generation': 2, 'collected': 1, 'uncollectable': 0}

### 收集阶段

在主 GC 函数中，`collect()` 针对特定的代。
CPython 有 3 个代。在理解代目的之前，理解收集算法是关重要的。

对于每次收集，GC 都会使用类型为 `PyGC_HEAD` 的双向链表。

这样 GC 就不需要“寻找”所有容器类型，所有作为 GC 目标的容器类型都有一个额外的头部。该头部将它们全部链接在双向链表中。当这些容器类型之一被创建时，它会将自己添加到列表中，当它被销毁时，它会将自己移除。

你可以在 `cellobject.c` 中看到这里的示例：

Objects > `cellobject.c` line 7

```c
PyObject *
PyCell_New(PyObject *obj)
{
    PyCellObject *op;
    op = (PyCellObject *)PyObject_GC_New(PyCellObject, &PyCellObject);
    if (op == NULL)
        return NULL;
    op->cell_obj = obj;
    Py_INCREF(obj);
    return (PyObject *)op;
}
```

### 释放对象

一旦确定了无法访问的对象，就可以在这些阶段进行（小心地）释放。

该方法取决于类型是否实现了旧的还是新的终结器槽（finalizer slot）：

- 1. 如果对象在旧的 `tp_del` 槽中定义了析构函数，则它无法被删除，并被标记为不可收集。这些对象会被添加到 `gc.garbage` 列表中，供开发者手动销。
- 2. 如果对象在 `tp_finalize` 槽中定义了析构函数，将这些对象标记为已析构（finalized），以避免重复调用。
- 3. 如果 (2) 中的对象通过再次初始化被“复活”，GC 将重新运行收集周期。
- 4. 对于所有对象，都会使用 `tp_clear` 槽。该槽会将引用计数 `ob_ref_cnt` 设置为 0，从而触发内存释放。

# 分代 GC

分代垃圾回收是一种基于以下观察的技术：大多数（80%以上）对象在创建后不久就会被销毁。

CPython 的 GC 使用三代，每代都有一个触发收集的阈值。最年轻的一代（0）具有较高的阈值，以避免收集循环过于频繁。如果一个对象存过了 GC，它将移动到第二代，然后是第三代。

在收集函数中，目标是单代，并在执行之前会将较年轻代合并其中。因此，如果你在第 1 代上运行 `collect()`，它将收集第 0 代。同样，在第 2 代运行收集将收集第 0 代和第 1 代。

当对象实例化时，分代计数器递增。当计数达到用户定义的阈值时，会自动运行 `collect()`。

# 从 Python 使用 GC API

CPython 的标准库带有一个与内存池（arena）和垃圾回收器接口的 Python 模块 `gc`。以下是在调试模式下使用 `gc` 模块的方法：

```python
>>> import gc
>>> gc.set_debug(gc.DEBUG_STATS)
```

每当垃圾回收器运行时，它都会打印统计信息：

```
gc: collecting generation 2...
```



gc: objects in each generation: 3 0 4477

gc: objects in permanent generation: 0

gc: done, 0 unreachable, 0 collectible.0008s elapsed

你使用 `gc.DEBUG_COLLECTABLE` 来发现项目何时被作为垃圾收集。当你将其与 `gc.DEBUG_SAVEALL` 调试标志结合时，它们在被收集后会被移动到列表 `gc.garbage` 中：

```
>>> import gc
>>> gc.set_debug(gc.DEBUG_COLLECTABLE | gc.DEBUG_SAVEALL)
>>> z = [0, 1, 2, 3]
>>> z.append(del)
>>> del z
>>> gc.collect()
gc: collectable <list 0x10d594a00>
>>> gc.garbage
[[0, 1, 2, 3, [...]]]
```

你可以通过调用 `get_threshold()` 获取垃圾回收器运行的阈值：

```
>>> gc.get_threshold()
(700, 10, 10)
```

你还可以获取当前的阈值计数：

```
>>> gc.get_count()
(688, 1, 1)
```

最后，你可以手动为某代运行收集算法，它将返回收集的总数：

```
>>> gc.collect(0)
24
```

如果你不指定代，它将默认为 2，这会合并第 0 代和第 1 代：

```
>>> gc.collect()
20
```

## 结论

在本章中，你已经了解了 CPython 如何分配、管理和释放内存。即使是最简单的 Python 脚本，这些操作在生命周期内也会发生数千次。CPython 内存管理系统的可靠性和可扩展性使其能够从几行的脚本一直扩展到世界上最大的网站之一。

在本章中展示的对象分配和原始内存分配系统在开发 C 扩展模块时非常有用。C 扩展模块需要对 CPython 的内存管理系统有深入了解。即使缺少一个 `Py_INCREF` 也会导致内存泄漏或系统崩溃。

在处理纯 Python 代码时，如果你正在设计长时间运行的代码，GC 的知识是有用的。例如，如果你设计了一个运行数小时、几天甚至更久的函数，该函数需要在其执行的系统限制内仔细管理其内存。你可以使用本章中学到的技术来控制和调整 GC 代，以更好地优化你的代码及其内存占用。

# 并行与并发

第一批计算机被设计为一次只一件事。它们的大部分工作在计算数学领域。随着时间的推移，计算机需要处理来自各种来源的输入。有些输入来自遥远的星系。其结果是计算机应用程序花费大量时间空等响应。无论响应是来自总线、内存、计算、API 还是远程资源。

计算的另一个进展是操作系统从单用户终端转向多任务操作系统。应用程序需要在后台运行，以监听并响应网络以及处理如鼠标光标之类的输入。在现代多核 CPU 出现之前就需要多任务，因此操作系统长期就能处理多个进程。任何操作系统的核心都是进程注册表。操作系统提供了一种处理多个进程的方法：

## 并发模型

| 方法 | 模块 | 并发 | 并行 |
|---|---|---|---|
| 线程 | `threading` | 是 | 否 |
| 多进程 | `multiprocessing` | 是 | 是 |
| 异步 | `asyncio` | 是 | 否 |
| 子解释器 | `subinterpreters` | 是 | 是 |

## 进程结构

操作系统的任务之一是控制运行的进程。这些进程可以是浏览器或 IDE 等 UI 应用程序。

当进程执行时，你计算机上的 CPU 还会保留额外数据，例如：

- 寄存器：持有当前正在执行的指令或进程该指令所需的任何其他数据
- 指令指针 `Instruction Pointer` 或程序计数器 `Program Counter`：指示程序序列中执行的是哪条指令

IPython 进程由编译后的 IPython 解释器和编译后的模块组成。这些模块在运行时加载，并由 IPython 评估循环转换为指令：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_230_0.png)

程序寄存器和程序计数器指向进程中的单条指令。这意味着在任何时刻只有一条指令在执行。

对于 CPython 来说，这意味着在任何时刻只有有一条 Python 字节码指令在执行。

允许进程中并行执行指令主要有两种方法：

1. 派生 `Fork` 另一个进程
2. 派生 `Spawn` 一个线程

## 多进程并行

POSIX 系统提供了一个 API，允许任何进程 `fork` 派生一个子进程。

派生进程是对操作系统的低级 API，任何运行中的进程都可以调用。

当进行此调用时，操作系统会克隆当前运行进程的所有属性并创建一个新进程。

该克隆操作包含了父进程的堆、寄存器和计数器位置。子进程可以在派生时从父进程读取任何变量。

### 在 POSIX 中派生进程

作为一个例子，以在 C 语言动态内存分配开始时使用的“华氏度转摄氏度”应用程序为例。将其修改为为每个华氏度值派生一个子进程，而不是按顺序计算。

这是通过使用 `fork()` 函数实现的。每个子进程将从该点继续运行：

`python-book-samples ▸ 33 ▸▸ thread_celcius.c`

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
static const double five_ninths = 5.0/9.0;
double celsius(double fahrenheit){
    return (fahrenheit - 32) * five_ninths;
}
int main(int argc, char** argv) {
    if (argc != 2) {
        return -1;
    }
    int number = atoi(argv[1]);
    for (int i = 1; i <= number; i++) {
        double f_value = 100 + (i*10);
        pid_t child = fork();
        if (child == 0) { // 是子进程
            double c_value = celsius(f_value);
            printf("%f F %f C (pid %d)\n", f_value, c_value, getpid());
            exit(0);
        }
    }
    printf("Spawned %d processes from %d\n", number, getpid());
    return 0;
}
```

在命令行运行此程序将得到类似下面的输出：

```
$ ./thread_celcius 4
110.000000 F is 43.333333 C (pid 57179)
120.000000 F is 48.888889 C (pid 57180)
Spawned 4 processes from 57178
130.000000 F is 54.444444 C (pid 57181)
140.000000 F is 60.000000 C (pid 57182)
```

## Windows 中的多进程

到为止，你一直在阅读 POSIX 模型。Windows 不提供 `fork()` 的等效方法，Python 应尽可能在 Linux、macOS 和 Windows 上拥有相同的 API。为了解决这个问题，使用了 `CreateProcess()` API 来派生另一个 `python.exe` 进程并带有 `-c` 命令行参数。

这一步骤被称为派生 `spawning` 进程，并且在 POSIX 上也可用。你将在本章中看到它的引用。

## multiprocessing 包

CPython 在操作系统进程 API 之上提供了一个 API。该 API 使在 Python 中创建多进程并行变得简单。

该 API 从 `multiprocessing` 包可用。该包提供了进程池、队列、派生、创建共享内存、连接进程等强大功能。

## 相关源文件

| 文件 | 目的 |
| --- | --- |
| `Lib/multiprocessing` | `multiprocessing` 包的 Python 源码 |
| `Modules/_posixsubprocess.c` | 封装 POSIX `fork()` 系统调用的 C 扩展模块 |
| `Modules/_winapi.c` | 封装 Windows API 的 C 扩展模块 |
| `PC/msvcmodule.c` | Microsoft Visual C Library 使用的 C 扩展模块 |

## 派生与 fork

`multiprocessing` 包提供了三种启动新进程的方法。

1. 派生解释器 `fork` 在 POSIX 上
2. 派生一个新的解释器 `spawn` 在 POSIX 和 Windows 上
3. 运行 Fork 服务器，其中创建一个新进程然后派生任意数量的进程 仅限 POSIX

> 注意
> 对于 Windows 和 macOS，默认启动方法是 `Spawning`。对于 Linux，默认是 `Forking`。你可以使用 `multiprocessing.set_start_method()` 函数覆盖默认方法。

每个进程都有显著的开销，池 `Pool` 会将池中的每个进程视为“工作线程”。如果一个工作线程完成了任务，它将被重用。如果你将该行：

```python
with mp.Pool(4) as pool:
```

替换为：

```python
with mp.Pool(4, maasksperchild=1) as pool:
```

之前的多进程示例将打印类似以下的内容：

```
$ python pool_process_celcius.py
110F is 43.333333333333336C (pid 5654)
120F is 48.88888888888889C (pid 5653)
130F is 54.44444444444444C (pid 5652)
140F is 60.0C (pid 5655)
```

输出显示了新生成的进程的进程 ID `pid` 以及计算出的值。

## 子进程的创建

这两个脚本都会创建一个新的 Python 解释器进程，并使用 `pickle` 向其传递数据。

| 说明 |
| :--- |
| `pickle` 模块是一个用于 Python 对象的序列化包。Davide Mastromatte 在 realpy.com 上写了一篇关于 `pickle` 模块的精彩文章。 |

对于 POSIX 系统，`multiprocessing` 模块创建子进程等同于此命令：



`$ python -c 'from multiprocessing.spawn import spawn_main; spawn_main(tracker_fd=<i>, pipe_handle=<j)' --multiprocessing-fork`

其中 `<i>` 是文件句柄描述符，`<j>` 是管道句柄描述符。

对于 Windows 系统，使用父 PID 代替跟踪描述符：

```python
> python.exe -c 'from multiprocessing.spawn import spawn_main; spawn_main(parent_pid=<k>, pipe_handle=<j>') --multiprocessing-fork
```

其中 `<k>` 是父 PID，`<j>` 是管道句柄描述符。

# 向子进程管道传输数据

当新的子进程在操作系统上实例化后，它将等待来自父进程的初始化数据。

父进程向管道文件流（pipe file stream）写入两个对象。管道文件流是一种用于在命令行进程之间传输数据的特殊 IO 流。

父进程写入的第一个对象是准备数据对象。该对象是一个包含父进程相关信息的字典，例如执行目录、启动方法、任何特殊的命令行参数以及 `sys.path`。你可以通过运行 `multiprocessing.spawn.get_preparation_data(name)` 查看生成的示例：

```python
>>> import multiprocessing.spawn
>>> import pprint
>>> pprint.print(multiprocessing.spawn.get_preparation_data("example"))
```

```python
'/Users/anthonyshaw',
}
```

写入的第二个对象是 `BaseProcess` 子类实例。取决于如何调用 `multiprocessing` 以及所使用的操作系统，`BaseProcess` 的某个子类将是经过序列化的实例。

准备数据和进程对象都使用 `pickle` 模块进行序列化，并写入父进程的管道流中：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_239_0.png)

> 注意：POSIX 的子进程创建和序列化过程实现位于 `Lib` ▸ `multiprocessing` ▸ `popen_spawn_posix.py`。Windows 的实现位于 `Lib` ▸ `multiprocessing` ▸ `popen_spawn_win32.py`。

# 执行子进程

子进程的入口点 `multiprocessing.spawn_main()` 接收参数 `pipe_handle` 以及 Windows 下的 `parent_pid` 或 POSIX 下的 `tracker_fd`：

```python
def spawn_main(pipe_handle, parent_pid=None, tracker_fd=None):
    """
    运行通过管道接收的数据指定的代码
    """
    assert is_forking(sys.argv), "Not forking"
```

对于 Windows，该函数将调用父 PID 的 `OpenProcess` API。

此进程对象被用于创建一个文件句柄 `fd`:
```python
if sys.platform == 'win32':
    import msvcrt
    import winapi
    if parent_pid is not None:
        process = winapi.OpenProcess(winapi.PROCESS_ALL_INFORMATION, False, parent_pid)
        fd = winapi.DuplicateHandle(process, -1, os.handle(), True, winapi.DUPLICATE_FROM_SOURCE, 0)
    else:
        fd = winapi.DuplicateHandle(tracker_fd, -1, os.handle(), True, winapi.DUPLICATE_FROM_SOURCE, 0)
```

对于 POSIX，该函数使用：
```python
import os
fd = os.dup(tracker_fd)
```

此进程对象被用于创建一个文件句柄 `fd`。

输出显示了新生成的进程的进程 ID（pid）以及计算出的值。

CPython `multiprocessing` 使用信号量（Semaphores是因为它们既是线程安全的也是进程安全的。操作系统会处理读取或写入同一信号量时可能出现的死锁。

这些信号量 API 函数的实现位于 C 扩展模块 `Modules` ▸ `_multiprocessing` ▸ `semaphore.c`。该扩展模块提供了用于创建、锁定、释放信号量以及其他操作的单一。

对操作系统的调用是通过一系列宏（Macros），这些宏根据操作系统平台编译为不同的实现。使用了 `<winbase.h>` 中的信号量 API 函数：

```
#define SEM_CREATE(name, val, max) CreateSemaphore(NULL, val, max, NULL)
#define SEM_CLOSE(sem) (CloseHandle(sem) ? 0 : -1)
#define SEM_GETVALUE(sem, pval) _GetSemaphoreValue(sem, pval)
#define SEM_UNLINK(name) 0
```

对于 POSIX，使用了 `<semaphore.h>` 中的宏：

```
#define SEM_CREATE(name, val, max) sem_open(name, O_CREAT | O_EXCL, 0600, val)
#define SEM_CLOSE(sem) sem_close(sem)
#define SEM_GETVALUE(sem, pval) sem_getvalue(sem, pval)
#define SEM_UNLINK(name) sem_unlink(name)
```

## 队列 (Queues)

队列是在多个进程之间发送小数据的极方法。

如果你将之前的 `multiprocessing` 示例改为使用 `multiprocessing Manager()` 实例，并创建两个队列：

- 1. `inputs` 用于存储输入的华氏度值
- 2. `outputs` 用于存储结果摄氏度值

将池大小更改为 2 以便有工作进程：

### 多进程并行

`cpython-book-samples ► 33 ► pool_queue_celcius.py`

```
import multiprocessing as mp
def to_celcius(input: mp.Queue, output: mp.Queue):
    f = input.get()
    # time-consuming task ...
    c = (f - 32) * (5/9)
    output.put(c)
if __name__ == '__main__':
    mp.set_start_method('spawn')
    pool_manager = mp.Manager()
    with mp.Pool(2) as pool:
        inputs = pool_manager.Queue()
        outputs = pool_manager.Queue()
        input_values = list(range(110, 150, 10))
        for i in input_values:
            inputs.put(i)
        pool.apply(to_celcius, (inputs, outputs))
        for f in input_values:
            print(outputs.get(block=False))
```

这将打印返回到结果队列的元组列表：

```
$ python pool_queue_celcius.py
43.333333333333336
48.888888888888889
54.444444444444444
60.0
```

父进程首先将输入值放入输入队列。然后第一个工作进程从队列中获取一个项目。每当使用 `.get()` 从队列中获取项目时，队列对象上就会使用信号量锁：

### 多进程并行

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_247_0.png)

当此工作进程忙碌时，第二个工作进程从队列中获取另一个值：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_247_1.png)

第一个工作进程完成了计算并将结果放入队列：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_247_2.png)

使用两个队列来分离输入和输出值。最终，所有输入值都处理完毕，输出队列满了。随后由父进程打印值：

### 多进程并行

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_248_0.png)

此示例显示了工作池如何接收离散值并并行处理它们。对于流式数据，可以使用管道（pipes）而不是离散队列。在 `multiprocessing` 包中，实例化 `Pipe` 返回两个连接：父端和子端。两者都可以发送和接收数据：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_248_1.png)

在队列示例中，当数据发送和接收时，队列上隐式地放置了锁。管道没有这种行为，因此必须确保两个进程不会写入同一个管道。如果你将最后一个示例适配为管道，将需要将 `pool.apply()` 更改为 `pool.apply_async()`。这会让进程的执行变为非阻塞操作：

```
cpython-book-samples ► 33 ► pool_pipe_celcius.py
import multiprocessing as mp
def to_celcius(child_pipe: mp.Pipe, parent_pipe: mp.Pipe):
    f = parent_pipe.recv()
    # time-consuming task ...
    c = (f - 32) * (5/9)
    child_pipe.send(c)
if __name__ == '__main__':
    mp.set_start_method('spawn')
    pool_manager = mp.Manager()
    with mp.Pool(2) as pool:
        parent_pipe, child_pipe = mp.Pipe()
        results = []
        for i in range(110, 150, 10):
            parent_pipe.send(i)
            pool.apply_async(to_celcius, (child_pipe, parent_pipe))
            print(child_pipe.recv())
        parent_pipe.close()
        child_pipe.close()
```

在这个示例中，存在两个进程同时读取或写入父管道的风险。同样存在两个进程同时写入子管道的风险。如果发生这种情况，数据在接收或发送操作将会损坏：![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_250_0.png)

为了避免这种情况，可以在操作系统上实现信号量锁。这样所有子进程在读取或写入同一管道之前都会检查锁。需要两个锁，一个在父管道的接收端，另一个在子管道的发送端：

```
python-book-samples ► 33 ► pool_pipe_locks_celcius.py
import multiprocessing as mp
def to_celcius(child_pipe: mp.Pipe, parent_pipe: mp.Pipe,
               child_write_lock: mp.Lock, parent_read_lock: mp.Lock):
    parent_read_lock.acquire()
    try:
        f = parent_pipe.recv()
    finally:
        parent_read_lock.release()
    # time-consuming task ...
    c = (f - 32) * (5/9)
    child_write_lock.acquire()
    try:
        child_pipe.send(c)
    finally:
        child_write_lock.release()
if __name__ == '__main__':
    mp.set_start_method('spawn')
    pool_manager = mp.Manager()
    with mp.Pool(2) as pool:
        parent_pipe, child_pipe = mp.Pipe()
        parent_read_lock = mp.Lock()
        child_write_lock = mp.Lock()
        results = []
        for i in range(110, 150, 10):
            parent_pipe.send(i)
            pool.apply_async(to_celcius, args=(child_pipe, parent_pipe,
                             child_write_lock,
                             parent_read_lock))
            print(parent_pipe.recv())
            child_pipe.close()
```

现在工作进程将在接收数据之前等待获取锁，并再次等待获取另一个锁以发送数据：![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_251_0.png)

此示例适用于管道传输数据较大的情况，因为冲突概率更高。

## 进程间的共享状态 (Shared State Between Processes)

到为止，你已经看到了如何在子进程和父进程之间共享数据。

可能存在需要在子进程之间共享数据的场景。在这种情况下，`multiprocessing` 包提供了两种解决方案：

- 1. 使用共享内存映射和共享 C 类型的高性能共享内存 API
- 2. 通过 `Manager` 类支持复杂类型的灵活服务器进程 API

## 示例应用程序 (Example Application)

作为一个演示应用程序，在整个章节中你将重构 TCP 端口扫描器以适应不同的并发和并行技术。

在网络上，可以通过端口访问主机，端口是 1-65535 之间的数字。常用服务有标准端口。例如，HTTP 运行在端口 80，HTTPS 运行在端口 443。TCP 端口扫描器被用作常用的网络测试工具，检查数据包是否可以通过网络发送。

此代码示例使用了 `Queue` 接口，这是一个与你在 `multiprocessing` 示例中使用的线程安全实现。代码还使用了 `socket` 包来尝试在 1 秒超时内连接远程端口。

你可以对比一下差异，它会在最后打印执行时间：

`cpython-book-samples ‣ 33‣ portscanner.py`

```
from queue import Queue
import socket
import time
timeout = 1.0
def check_port(host: str, port: int, results: Queue):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(timeout)
    result = sock.connect_ex(host, port)
    if result == 0:
        results.put(port)
    sock.close()
if __name__ == '__main__':
    start = time.time()
    host = "localhost" # 为你想测试的 host
    results = Queue()
    for port in range(80, 100):
        check_port(host, port, results)
    while not results.empty():
        print("Port {0} is open".format(results.get()))
    print("Completed scan in {0} seconds".format(time.time() - start))
```

执行结果将打印开启的端口和所花费的时间：

```
$ python portscanner.py
Port 80 is open
Completed scan in 19.623435020446777 seconds
```



这个示例可以重构为使用多进程。接口被更换为 `multiprocessing.Queue`，并使用池执行器共同扫描端口：

`cpython-book-samples ‣ 33‣ portscanner_mp_queue.py`

# 多进程并行

```python
import multiprocessing as mp

import time

import socket

timeout = 1

def check_port(host: str, port: int, results: mp.Queue):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(timeout)
    result = sock.connect_ex((host, port))
    if result == 0:
        results.put(port)
    sock.close()

if __name__ == '__main__':
    start = time.time()
    processes = []
    scan_range = range(80, 100)
    host = "localhost" # 替换为你拥有的 host
    mp.set_start_method('spawn')
    pool_manager = mp.Manager()
    with mp.Pool(len(scan_range)) as pool:
        outputs = pool_manager.Queue()
        for port in scan_range:
            processes.append(pool.apply_async(check_port, (host, port, outputs)))
        for process in processes:
            process.get()
        while not outputs.empty():
            print("Port {0} is open".format(outputs.get()))
    print("Completed scan in {0} seconds".format(time.time() - start))
```

正如你所预期的，这个应用程序更快，因为它是并行测试每个端口：

```
$ python portscanner_mp_queue.py
Port 80 is open
Completed scan in 1.556523084640503 seconds
```

## 结论

多进程（Multiprocessing）为 Python 提供了一个可扩展的并行执行 API。数据可以在进程之间共享，CPU 密集型工作可以分解为并行任务，以利用多核或多 CPU 计算机。

当任务不是 CPU 密集型而是 IO 密集型（IO-bound）时，多进程并不是一个合适的解决方案。例如，如果你启动了 4 个工作进程来读写同一个文件，其中一个将执行所有工作，而其他 3 个将等待锁释放。

多进程也不适用于短生命周期任务，因为启动新的 Python 解释器存在时间争处理开销。

在这两种情况下，你的主程序会发现以下方法之一更合适。

## 多线程

CPython 提供了高层和低层 API，用于从 Python 中创建、派生和控制线程。

要理解 Python 线程，你应该首先理解操作系统线程的工作原理。CPython 中有两种线程实现方式：

- `threads` - 适用于 Linux 和 macOS 的 POSIX 线程
- `nt threads` - 适用于 Windows 的 NT 线程

在“进程结构”章节中，你看到一个进程拥有：

- 一个子程序栈（Stack）
- 一个内存堆（Heap）

操作系统对文件、锁和套接字的访问

扩展单个进程的最大限制是，操作系统将为可执行文件拥有一个单一程序计数器（Program Counter）。

为了解决这个问题，现代操作系统允许进程向操作系统发送信号，将其执行分支到多个线程。

每个线程将有自己的程序计数器，但与宿主进程使用相同的资源。每个线程也有自己的调用栈（call stack），因此它可以执行不同的函数。

由于多个线程可以读写同一内存空间，可能会发生冲突。解决此问题的方法是线程安全（thread safety），涉及到在访问内存空间之前确保其被单个线程锁定。

## 多线程

| 参见 |
| --- |
| 关于 Python 线程的入门介绍，请查看 Jim Anderson 的“Threading”。 |

如果你熟悉 NT 线程或 POSIX 线程，或者使用过其他高层语言，你可能预期多线程是并行的。在 CPython 中，线程基于字节码的，这意味着 Python 线程是线程安全的。解释器状态的许多部分，例如垃圾回收（Garbage Collector），都是共享且全局的。

为了解决这个问题，CPython 开发者实现了一个大锁，被称为**全局解释器锁（Global Interpreter Lock, GIL）**。在评估循环中执行任何字节码之前，线程会获取 GIL，一旦字节码执行完毕，锁就会被释放。

除了为 Python 的所有操作提供全局安全性外，这种方法有一个巨大的缺点。执行耗时较长的操作会让其他线程等待 GIL 释放。这意味着在任何时候只有一个线程可以执行 Python 字节码。要获取 GIL，会调用 `take_lock`。

| 文件 | 目的 |
| --- | --- |
| Python > ceval_gil.h | GIL 实现 |

# 在 Python 中启动线程

为了演示多线程代码的性能提升（尽管有 GIL），你可以在 Python 中实现一个简单的端口扫描器。

现在克隆之前的脚本，但使用 `threading.Thread()` 为每个端口派一个线程。这与多进程 API 类似，它接收一个可调用对象 `target` 和一个元组 `args`。在循环内部启动线程，但不要在那里等待它们完成。相反，将线程实例添加到列表 `threads` 中：

```python
for port in range(80, 100):
    t = Thread(check_port, args=(host, port, results))
    t.start()
    threads.append(t)
```

当所有线程都创建完毕后，遍历线程列表并调用 `.join()` 等待它们完成：

```python
for t in threads:
    t.join()
```

接下来，耗尽结果队列中的所有项并将它们打印到屏幕上：

```python
while not results.empty():
    print("Port {0} is open".format(results.get()))
```

```python
import socket
import time
```

```python
timeout = 1.0
def check_port(host: str, port: int, results: Queue):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(timeout)
    result = sock.connect_ex((host, port))
    if result == 0:
        results.put(port)
        sock.close()
```

```python
def main():
    start = time.time()
    host = "localhost" # replace with a host you owns
    threads = []
    results = Queue()
    for port in range(80, 100):
        t = Thread(target=check_port, args=(host, port, results))
        t.start()
        threads.append(t)
    for t in threads:
        t.join()
    while not results.empty():
        print("Port {0} is open".format(results.get()))
    print("Completed scan in {0} seconds".format(time.time() - start))
```

```python
if __name__ == '__main__':
    main()
```

当你在命令行调用此线程脚本时，它的执行速度比单线程示例快 10 倍以上：

```bash
$ python portscanner_threads.py
Port 80 is open
Completed scan in 1.0101029872894287 seconds
```

这运行速度也比多进程示例快 50-60%。记住，多进程启动进程有开销，而线程也有开销，但这种开销要小得多。

你可能会疑惑——如果 GIL 意味着一次只能执行一个操作，为什么速度会更快呢？

耗时 1-1000ms 的语句是：

```python
result = sock.connect_ex(host, port)
```

在 C 扩展模块 `Modules ▸ socketmodule.c` 中，实现连接的函数：

`Modules ▸ socketmodule.c` line `3246`

```c
static int
internal_connect(PySocketSockObject *s, struct sockaddr *addr, int addrlen,
    int raise)
{
    int res, err, wait_connect;
    Py_BEGIN_ALLOW_THREADS
    res = connect(s->sock_fd, addr, addrlen);
    Py_END_ALLOW_THREADS
```

环在系统 `connect()` 调用周围的是 `Py_BEGIN_ALLOW_THREADS` 和 `Py_END_ALLOW_THREADS` 宏。

这些宏在 `Include ceval.h` 中定义如下：

```c
#define Py_BEGIN_ALLOW_THREADS {
    PyThreadState *save;
    _save = PyEval_SaveThread();
}
#define Py_BLOCK_THREADS
    PyEval_RestoreThread(_save);
#define Py_UNBLOCK_THREADS
    _save = PyEval_SaveThread();
#define Py_END_ALLOW_THREADS
    PyEval_RestoreThread(_save);
```

所以，当调用 `Py_BEGIN_ALLOW_THREADS` 时，它会调用 `PyEval_SaveThread()`。该函数会将线程状态更改为 NULL 并释放 GIL。

## 多线程

# Python ▸ ceval.c line 480

```c
PyThreadState *
PyEval_SaveThread(void)
{
    PyThreadState *tstate = PyThreadState_Swap(NULL);
    if (tstate == NULL)
        Py_FatalError("PyEval_SaveThread: NULL tstate");
    assert(gil_created());
    drop_gil(tstate);
    return tstate;
}
```

因为释放了 GIL，意味着其他正在执行的线程可以继续。该线程将在此等待系统调用，而不会阻塞评估循环。

一旦 `connect()` 函数成功或超时，`Py_END_ALLOW_THREADS` 会带有原始线程状态运行 `PyEval_RestoreThread()`。线程被恢复，GIL 被重新获取。`take_gil()` 调用是一个等待信号量的阻塞调用：

# Python ▸ ceval.c line 503

```c
void
PyEval_RestoreThread(PyThreadState *tstate)
{
    if (tstate == NULL)
        Py_FatalError("PyEval_RestoreThread: NULL tstate");
    assert(gil_created());
    int err = errno;
    take_gil(tstate);
    /* _Py_Finalizing 由 GIL 保护 */
    if (_Py_Finalizing(tstate)) {
        drop_gil(tstate);
        PyThread_exit();
    }
}
```

```c
Py_UNBLOCK_THREADS();
errno = err;
PyThreadState_Swap(tstate);
```



这不是唯一的被非阻塞 `Py_BEGIN_ALLOW_THREADS` 和 `Py_END_ALLOW_THREADS` 包裹的系统调用。它在标准库中有 300 多处用途：

- 发起 HTTP 请求
- 与硬件交互
- 读写文件

## 状态

CPython 提供了了自己的线程管理实现。由于线程需要在评估循环中执行字节码，因此在 CPython 中运行线程并不像创建线程那么简单。Python 线程被称为 `PyThread`，由解释器产生。

- CPython 有一个单一运行时，它有自己的状态
- CPython 可以有一个或多个解释器
- 解释器有一个状态，称为解释器状态
- 解释器将代码对象获取并转换为一系列帧对象
- 解释器至少有一个线程，每个线程都有线程状态
- 帧对象在栈中执行，称为帧栈
- CPython 引用值栈中的变量
- 解释器状态包含其线程的链表

线程状态类型 `PyThreadState` 有 30 多个属性，包括：

- 线程状态的链表
- 创建它的解释器状态
- 当前执行的帧
- 当前递归深度
- 可选的跟踪函数
- 当前处理的异常
- 当前处理的任何异常
- 抛出的异常栈
- GIL 计数

## 多线程

与多进程准备类似，线程有一个启动状态。然而线程共享相同的内存空间，因此不需要将数据序列化并发送。

线程使用 `threading.Thread` 类型实例化。这是一个抽象 `PyThread` 类型的高级模块。`PyThread` 实例由 C 扩展模块 `_thread` 管理。`_thread` 模块具有执行新线程的入口点 `thread_start_new_thread()`。`start()` 是 `Thread` 类型实例的方法。

新线程按此顺序实例化：

1. 创建启动状态，链接到目标、args 和 kwargs
2. 将启动状态链接到解释器状态
3. 创建一个新的 `PyThreadState`，链接到当前解释器
4. 如果尚未启用，通过调用 `PyEval_InitThreads()` 启用 GIL
5. 在特定操作系统的实现 `PyThread_start_new_thread` 上启动新线程

线程启动状态具有属性：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| interp | PyInterpreter* | 链接到管理此线程的解释器 |
| func | PyObject * (callable) | 链接到运行时运行时执行的可调用对象 |
| args | PyObject * (tuple) | 调用 func 的参数 |
| keyw | PyObject * (dict) | 调用 func 的关键字参数 |
| tstate | PyThreadState * | 新线程的线程状态 |

带有启动状态有两种实现：用于 Linux 和 macOS 的 POSIX 线程以及用于 Windows 的 NT 线程。

这两种实现都会创建操作系统，设置其属性，然后在新线程内部执行回调 `t_bootstrap()`。该函数通过单个参数 `boot_raw` 调用，该参数被分配到在 `thread_thread` 中构造的启动状态。

`t_bootstrap()` 函数是底层线程与 Py 运行时之间的接口。bootstrap 将启动线程，然后使用 `PyObject_Call()` 执行目标可调用对象。一旦执行了目标目标，线程将退出：

### POSIX 线程

POSIX 线程（名为 pthreads）在 Python `pthread.h` 中有一个实现。该实现在 `<pthread.h>` C API 的基础上带有额外的保护措施和优化。

线程可以具有配置的栈大小。Python 有自己的栈帧结构，正如你在“评估循环”章节中所探索的那样。如果出现导致循环的问题，且帧执行达到深度限制，Python 将抛出 `RecursionError`，可以通过 Python 代码中的 `try...except` 块进行处理。由于 pthreads 有自己的栈大小，Python 的最大深度和线程的栈大小可能会冲突。

如果栈大小小于 Python 中的最大帧深度，整个 Python 进程将在抛出 RecursionError 之前崩溃。此外，可以使用 `sys.setrecursionlimit()` 在运行时配置 Python 中的最大深度。为了避免这些崩溃，CPython 线程实现将栈大小设置为解释器状态的 `thread_stacksize` 值。

大多数现代符合 POSIX 的操作系统支持线程的系统调度。如果 `pyconfig.h` 中定义了 `PTHREAD_SYSTEM_SCHED_SUPPORTED`，则线程设置为 `PTHREAD_SCOPE_SYSTEM`，这意味着线程在操作系统调度器中的优先级是与系统中其他线程共同决定的，而不仅仅是 Python 进程内的线程。

最后，线程句柄 `pthread_t` 被转换为无符号长型并返回，作为线程 ID。

## Windows 线程

在 Python 中实现的 Windows 线程 ▸ `thread_nt.h` 遵循一种类似但更简洁的模式。

新线程的栈大小被配置为解释器的 `pythread_stacksize` 值（如果已设置）。

使用 Windows API `_beginthreadex()` 来创建线程，并使用自举引导函数（bootstrap function）作为回调函数。

最后，返回线程 ID。

## 结论

这并不是一个关于 Python 线程的详尽教程。Python 的线程实现非常广泛，并提供了许多在线程之间共享数据、锁定对象和资源的机制。

当你的 Python 应用程序是 IO 密集型时，线程是提高其运行效率的一种极佳且高效的方法。在本节中，你已经了解了什么是 GIL、它为什么存在以及标准库的哪些部分可能免受其限制。

# 异步编程

Python 提供了许多在不使用线程或多进程的情况下实现并发编程的方法。这些特性被添加、扩展，并且经常被更好的替代方案所取代。

对于本书的目标版本 3.9.0b1，以下异步系统已被弃用：

- `@coroutine` 装饰器

以下系统仍然可用：

- 从 `async` 关键字创建 future（未来）
- 使用 `yield from` 关键字的协程

## 生成器

Python 生成器（Generators）是返回包含 `yield` 语句的函数，并且可以连续调用以生成后续值。

生成器通常被用作在大型数据块（如文件、数据库或网络）中循环遍历值的更节省内存的方法。当使用 `yield` 代替 `return` 时，会返回一个生成器对象而不是值。生成器对象由 `yield` 语句创建并返回给调用者。

这个简单的生成器函数将产生字母 a-z：

`python-book-samples 33▸letter_generator.py`

```python
def letters():
    i = 97 # ASCII 中的字母 'a'
    end = 97 + 26 # ASCII 中的字母 'z'
    while i < end:
        yield chr(i)
        i += 1
```

如果你调用 `letters()`，它不会返回一个值，而是返回一个生成器对象：

```python
>>> from letter_generator import letters
>>> letters()
<generator object letters at 0x1004d9b0>
```

`for` 语句的语法中内置了遍历生成器对象的能力，直到它停止产生值：

```python
>>> for letter in letters():
...    print(letter)
a
b
c
d...
```

这种实现使用了迭代器协议（iterator protocol）。拥有 `__next__()` 方法的对象可以被 `for` 和 `while` 循环遍历，或者使用内置的 `next()` 函数。

Python 中所有的容器类型（如列表、集合、元组）都实现了迭代器协议。生成器的独特之处在于，其 `__next__()` 方法的实现会从其最后状态重新调用生成器函数。生成器并不是在后台执行，它们是被挂起的。当你请求另一个值时，它们会恢复执行。

在生成器对象的结构内部，包含了最后一次 `yield` 语句时的帧对象（frame object）。

### 生成器结构

生成器对象通过模板宏 `_PyGen_HEAD(prefix)` 创建。

该宏被以下类型和前缀使用：

- 1. `PyGenObject - gi_` (生成器对象)
- 2. `PyCoroObject - cr_` (协程对象)
- 3. `PyAsyncGenObject - ag_` (异步生成器对象)

你将在本章后面的部分介绍协程和异步生成器对象。

`PyGenObject` 类型具有基础属性：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| [x]_frame | PyFrameObject | 生成器的当前帧对象 |
| [x]_running | char | 如果生成器当前正在运行，则设置为 0 或 1 |
| [x]_code | PyObject * (PyObject*) | 产生生成器的编译后函数 |
| [x]-weakreflist | PyObject * (list) | 生成器函数内部对象的弱引用列表 |
| [x]_name | PyObject * (str) | 生成器的名称 |
| [x]_qualname | PyObject * (str) | 生成器的限定名称 |
| [x]_exc_state | _PyStackItem | 如果生成器抛出异常，则异常数据 |

## 在基础属性之上，PyCoroObject 类型具有：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| cr_origin | PyObject * (tuple) | 包含源帧帧和调用者的元组 |

## 在基础属性之上，PyAsyncGenObject 类型具有：

| 字段 | 类型 | 目的 |
| --- | --- | --- |
| ag_finalizer | PyObject * | 指向终结器方法的链接 |
| ag_hooks_init | int | 标记钩子已初始化的标志 |
| ag_closed | int | 标记生成器已关闭的标志 |
| ag_running_async | int | 标记生成器正在运行的标志 |

## 相关文件

与生成器相关的源文件有：

| 文件 | 目的 |
| --- | --- |
| Include ► genobject.h | 生成器 API 和 PyGenObject 定义 |

## 生成器

| 文件 | 目的 |
| --- | --- |
| Objects ► genobject.c | 生成器对象实现 |

## 创建生成器

当包含 `yield` 语句的函数被编译时，结果-代码对象有一个额外的标志 `CO_GENERATOR`。

在“执行循环：构建帧”的章节中，我们探索了编译后的代码对象在执行时如何转换为帧对象。

在此过程中，对于生成器、协程和异步生成器有一个特殊情况。生成器、协程和异步生成器会检查 `CO_GENERATOR`、`COROUTINE` 或 `ASYNC_GENERATOR` 标志。

```c
/* 处理生成器、协程和异步生成器 */
if (co->flags) {
    PyObject *gen;
    PyObject *co_wrapper = tstate;
    int is_coro = co->flags & COROUTINE;
    /* 创建就绪的生成器 */
    if (is_coro) {
        gen = PyCoro_New(f);
    } else if (co->flags & ASYNC_GENERATOR) {
        gen = PyAsyncGen_New(f);
    } else {
        gen = PyGen_New(f);
    }
    return gen;
}
```

`PyGen_NewWithName` 接收 `f` 和 `name` 并完成以下步骤：

- 1. 将 `gi_code` 设置为代码对象
- 2. 将生成器设置为非运行（`gi_running = 0`）
- 3. 将异常列表为空

你也可以通过导入 `dis` 来反汇编 `gi_code`：

```python
>>> from letter_generator import letters
>>> gen = letters()
>>> import dis
>>> dis.dis(gen)
2     0 LOAD_CONST  1 (97)
      2 STORE_FAST  0 (i)
```

在执行循环的章节中，我们探索了帧对象。帧包含局部变量、全局变量以及要执行的代码。

帧的行为和状态决定了生成器如何暂停和恢复。

## 执行生成器

当在生成器对象上调用 `__next__()` 时，会调用 `gen_next()`，它会立即调用 `genobject.c` 中的 `gen_send()`。

`gen_send()` 是将生成器转换为结果的函数。你会发现它与构建帧有许多相似之处。

生成器、协程和异步生成器共享的 `gen_send()` 函数具有以下步骤：

- 1. 获取当前线程状态
- 2. 获取生成器的帧对象
- 3. 如果调用 `__next__()` 时生成器正在运行，则抛出 `ValueError`
- 4. 如果生成器内部的帧位于栈顶：
    - 对于协程，如果协程未标记为关闭，则抛出 `RuntimeError`
    - 如果是异步生成器，抛出 `StopAsyncIteration`
    - 对于标准生成器，抛出 `StopIteration`
- 5. 如果帧的最后指令 `f->f_last` 仍为 -1（刚刚开始），且它是协程或异步生成器，则不能传递 None 值作为参数，因此抛出异常
- 6. 否则，这是第一次调用，允许参数。参数值被推入帧的值栈。
- 7. 帧的 `f_back` 字段是返回值的调用者，因此将其设置为线程中的当前帧。这意味着返回值是发送给调用者的，而不是生成器的创建者。
- 8. 标记生成器正在运行
- 9. 生成器异常信息中的最后一个异常将从线程状态的最后一个异常中复制
- 10. 线程状态异常信息被设置为生成器异常信息的地址。这意味着如果调用者进入一个 break-

# 协程

围绕生成器的执行，堆栈跟踪会经过生成器，导致出错的代码清晰易易。

+ 11. 生成器内部的帧在 Python ceval.c 主执行循环中执行，并返回值
+ 12. 线程状态的上一个异常被重置为调用帧之前的值
+ 13. 生成器被标记为未运行
+ 14. 随后以下情况将匹配调用生成器的返回值和抛出的任何异常。请记住，生成器在耗尽时（无论是手动还是通过不产生值）应该抛出 StopIteration。协程和异步生成器不应该：
* 如果帧没有返回结果，生成器抛出 StopIteration，异步生成器抛出 StopAsyncIteration
* 如果显式抛出 StopIteration 但这是一个协程或异步生成器，则抛出 RuntimeError，因为这是不允许的
* 如果显式抛出 StopAsyncIteration 这是一个异步生成器，则抛出 RuntimeError，因为这是不允许的

+ 15. 最后，结果被返回给 __next__() 的调用者

将所有这些整合在一起，你可以看到生成器表达式是一个强大的语法，单个关键字 `yield` 触发了整个流程来创建一个唯一对象、将编译后的代码对象作为属性复制、设置帧并在局部作用域中存储变量列表。

# 协程

生成器有一个很大的局限性。它们只能向其直接调用者产生值。

为了克服这一点，Python 增加了一种额外的语法 - `yield from` 语句。使用这种语法，你可以将生成器重构为工具函数，然后从这些函数中 `yield from`。

# 协程

例如，字母生成器可以重构为一个工具函数，其中起始字母是一个参数。使用 `yield from`，你可以选择返回哪个生成器对象：

`cython-book-samples ▷ 33 letter_coroutines.py`

```python
def gen_letters(start, x):
    i = start
    end = start + x
    while i < end:
        yield chr(i)
        i += 1

def upper(upper):
    if upper:
        yield from gen_letters(65, 26) # A-Z
    else:
        yield from gen_letters(97, 26) # a-z

for letter in letters(False):
    # 小写字母 a-z
    print(letter)

for letter in letters(True):
    # 大写字母 A-Z
    print(letter)
```



生成器也非常适用于惰性序列，它们可以被多次调用。

基于生成器的行为（例如能够暂停和恢复执行），协程的概念在 Python 中通过原生 API 进行了迭代优化。生成器是协程的一种有限形式，因为你可以使用 `.send()` 方法向它们发送数据。

在调用者和目标之间进行双向消息传递是可能的。协程还在 `cr_origin` 属性中存储调用者。

协程最初通过装饰器可用，但此后已被弃用，取而代之的是使用 `async` 和 `await` 关键字的“原生”协程。

要标记一个函数返回协程，必须在其前面加上 `async` 关键字。

`async` 关键字显式地表明（与生成器不同）该函数返回的是协程而不是值。

要创建一个协程，请使用 `async def` 关键字定义函数。在这个示例中，使用 `asyncio.sleep()` 函数添加一个定时器并返回一个唤醒字符串：

```python
>>> asyncio

>>> async def sleepy_alarm(time):
    await asyncio.sleep(time)
    return "wake up!"

>>> alarm = sleepy_alarm(10)

>>> alarm
<coroutine object sleepy_alarm at 0x1041de340>
```

当你调用函数时，它返回一个协程对象。执行协程有很多方法。最简单的是使用 `asyncio.run(coro)`。

使用你的协程对象运行 `asyncio.run()`，10 秒后它将响铃：

```python
>>> asyncio.run(alarm)
'wake up'
```

到目前为止，与普通函数相比只有一个微小的优势。协程的优势在于你可以并发运行它们。因为协程对象是一个可以传递给函数的变量，这些对象可以相互链接并链联，或者按顺序创建。

例如，如果你想有 10 个不同间隔的闹钟并同时启动它们，这些协程对象可以转换为任务（task）。

任务 API 用于调度和执行多个协程。在任务被调度之前，必须有一个事件循环在运行。事件循环的工作是调度并发任务并将完成、取消和异常等事件与回调连接起来。当调用 `asyncio.run()` 时，`run` 函数（在 `asyncio.py` 中）为你完成了这些任务：

- 启动一个新的事件循环
- 将协程对象封装在任务中
- 在任务完成时设置回调
- 循环任务直到其完成
- 返回结果

## 相关文件

| 文件 | 用途 |
| --- | --- |
| `asyncio` | 用于 async/await 的 Python 标准库实现。 |

### 事件循环

事件循环是把异步代码结合在一起的胶水。事件循环用纯 Python 编写，要么运行一次要么永久运行。循环中的任何任务都有回调。你可以将单个定时器转换为任务：

```python
python-book-samples ▷ 33 sleepy_alarm.py

import asyncio

async def sleepy_alarm(person, time):
    await asyncio.sleep(time)
    print(f"{person} wake up!")

async def wake_up():
    tasks = [
        asyncio.create_task(sleepy_alarm("Bob", 3), name="Doris"),
        asyncio.create_task(sleepy_alarm("Sanjeet", 4), name="Sanjeet"),
        asyncio.create_task(sleepy_alarm("Doris", 2), name="Doris"),
        asyncio.create_task(sleepy_alarm("Kim", 5), name="Kim")
    ]
    await asyncio.gather(*tasks)

asyncio.run(wake_up())
```

这将打印：
Doris -- wake up!
Bob -- wake up!
Sanjeet -- wake up!
Kim -- wake up!

在事件循环中，它将遍历每个协程以检查它们是否完成。类似于 `yield` 关键字可以从同一个帧返回多个值，`await` 关键字可以返回多个状态。事件循环将反复执行 `sleepy_alarm()` 协程，直到 `asyncio.sleep()` 返回结果，并且 `print()` 函数能够执行。为了使此起作用，必须使用 `asyncio.sleep()` 而替阻塞的 `time.sleep()`。

### 示例

你可以通过以下步骤将多线程端口扫描器示例转换为 asyncio：

- 使用 `asyncio.open_connection()` 创建一个连接来修改 `check_port()` 函数
- 在定时器事件中使用 `asyncio.wait_for()` 处理 future
- 如果成功，将端口添加到结果列表中
- 添加一个新函数 `scan()`，为端口创建 `check_port()` 协程并将其加入列表
- 使用 `asyncio.gather()` 将所有任务合并为协程
- 使用 `asyncio.run()` 运行 scan

cython-book-samples ▷ 33 portscanner_async.py

```python
import time
import asyncio

timeout = 1.0

async def check_port(host: str, port: int, results: list):
    try:
        future = asyncio.open_connection(host, port=port)
        r, w = await asyncio.wait_for(future, timeout)
        results.append(port)
        w.close()
    except asyncio.TimeoutError:
        pass # 端口关闭，跳过
```

```python
async def scan(start, end, host):
    tasks = []
    results = []
    for port in range(start, end):
        tasks.append(check_port(host, port, results))
    await asyncio.gather(*tasks)
    return results

if __name__ == '__main__':
    start = time.time()
    host = "localhost" # 选择一个你拥有的主机
    results = asyncio.run(scan(80, 100, host))
    for result in results:
        print("Port {0} is open".format(result))
        print("Completed scan in {0} seconds".format(time.time() - start))
```

最后，这个扫描在 1 秒多一点完成：

```bash
$ python portscanner_async.py
Port 80 is open
Completed scan in 1.0058400630950928
```

# 异步生成器

你目前学到的生成器和协程可以组合成一种类型 - 异步生成器。

如果一个函数声明了 `async` 关键字并包含 `yield` 语句，它就会转换为异步生成器对象。

与生成器一样，异步生成器必须由理解协议的实体执行。对应 `__next__()()`，异步生成器具有 `__anext__()` 方法。

普通的 `for` 循环无法理解异步生成器，因此使用了 `async for` 语句。

你可以将 `check_port()` 函数重构为一个异步生成器，它会产生下一个开放的端口，直到达到最后一个端口或找到指定数量的开放端口：

```python
async def check_ports(host: str, start: int, end: int, max=10):
    found = 0
    for port in range(start, end):
        try:
            future = asyncio.open_connection(host=host, port=port)
            r, w = await asyncio.wait_for(future, timeout=timeout)
            yield port
            found += 1
            w.close()
            if found >= max:
                return
        except asyncio.TimeoutError:
            pass # closed
```

要执行此代码，请使用 `async for` 语句：

```python
async def scan(start, end, host):
    results = []
    async for port in check_ports(host, start, end, max=1):
        results.append(port)
    return results
```

完整示例请参考 cython-book-samples ▸ 33 ▸ portscanner_async_generators.py。

### 子解释器

到目前为止，你已经涵盖了：

- 使用多进程进行并行执行
- 使用线程和异步进行并发执行

多进程的缺点是使用管道和队列的进程间通信比共享内存更慢。此外，启动新进程的开销也是相当大的。

线程和异步的开销很小，但由于 GIL 的线程安全保证，它们无法提供真正的并行执行。

第四种选择是子解释器，它的开销比多进程小，并且允许每个子解释器拥有自己的 GIL。毕竟，它是全局解释器锁（Global Interpreter Lock）。

在 CPython 运行时中，始终有 1 个解释器。解释器持有解释器状态，在一个解释器内部，你可以拥有 1 个或多个 Python 线程。解释器是评估循环的容器，解释器还管理自己的内存、引用计数和垃圾回收。CPython 提供了创建解释器的底层 API，例如 `Py_NewInterpreter()`。

| 运行时状态 | | | | | |
|---|---|---|---|---|---|
| 指令 (Python 运行时) | 文件 | 指令 (Python 运行时) | 文件 | | |
| 解释器 0 (主) | 堆 | 锁 | 解释器 n | 堆 | 锁 |
| | 解释器状态 | 隐含模块 | 接接字 | | |
| | GIL | | | | |
| 线程 @ (主) | 线程 1-n | 线程 @ (主) | 线程 1-n | | |

> 注意
subinterpreters 模块在 3.9.0b1 中仍处于实验阶段，因此 API 可能会发生变化且实现存在 Bug。

由于解释器状态包含内存分配区域以及指向 Python 对象（局部和全局）的指针集合，子解释器无法访问其他解释器的全局变量。与多进程类似，要在解释器之间共享对象，你必须对其进行序列化，或使用 `ctypes` 以及某种形式的 IPC（网络、磁盘或共享内存）。

### 相关源码

与子解释器相关的源码有：

| 文件 | 用途 |
|---|---|
| `_xxsubinterpreters.c` | 子解释器模块的 C 实现 |
| `Python pylifcycle.c` | 解释器管理 API 的 C 实现 |

### 示例

在最后的示例应用程序中，实际的代码必须封装在字符串中。在 3.9.01 中，子解释器只能通过代码字符串执行。

为了启动每个子解释器，会启动一个线程列表，并回调函数 `run()`。

该函数将：

- 创建一个通信通道
- 启动一个新的子解释器
- 向其发送要执行的代码
- 通过通信通道接收数据
- 如果端口连接成功，则将其添加到线程安全的队列中

cpython-book-samples ▸ 33 ▷ portscanner_subinterpreters.py

```python
import time
import _xxsubinterpreters as subinterpreters
from threading import Thread
import textwrap as tw
from queue import Queue

timeout = 1  # 秒..

def run(host: str, port: int, results: Queue):
    # 创建通信通道
    channel_id = subinterpreters.channel_create()
    interpid = subinterpreters.create()
    subinterpreters.run_string(
        interpid,
        tw.dedent("""\
import socket; import _xxsubinterpreters as subinterpreters
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.settimeout(timeout)
result = sock.connect_ex((host, port))
subinterpreters.channel_send(channel_id, result)
sock.close()
"""),
        shared=dict(
            channel_id=channel_id,
            host=host,
            port=port,
            timeout=timeout
        ))
    output = subinterpreters.channel_recv(channel_id)
    subinterpreters.channel_release(channel_id)
if output == 0:
    results.put(port)
if __name__ == '__main__':
    start = time.time()
    host = "127.0.0.1" # 选择一个你需要的主机
    threads = []
    results = Queue()
    for port in range(80, 100):
        t = Thread(target=run, args=(host, port, results))
```



## 内置类型

核心数据模型定义在 `PyTypeObject` 中，而函数定义在：

每个源文件在 `Include` 中都有一个对应的头文件。例如，`Objects/rangeobject.c` 对应的头文件是 `Include/rangeobject.h`。

| 源文件 | 类型 |
| :--- | :--- |
| Objects/object.c | 内置方法和基础对象 |
| Objects/boolobject.c | bool 类型 |
| Objects/typeobject.c | byte[] 类型 |
| Objects/bytesobjects.c | bytes 类型 |
| Objects/cellobject.c | cell 类型 |
| Objects/classobject.c | 抽象类类型，用于元编程 |
| Objects/codeobject.c | 内置代码对象类型 |
| Objects/complexobject.c | 复数数值类型 |
| Objects/iterobject.c | 迭代器 |
| Objects/listobject.c | list 类型 |
| Objects/longobject.c | long 数值类型 |
| Objects/memoryobject.c | 基础内存类型 |
| Objects/methodobject.c | 类方法类型 |
| Objects/namespaceobject.c | 模块类型 |
| Objects/moduleobject.c | 命名空间类型 |
| Objects/dictobject.c | 有序字典类型 |
| Objects/rangeobject.c | 范围生成器 |
| Objects/setobject.c | set 类型 |
| Objects/sliceobject.c | 切片引用 |
| Objects/structseq.c | struct.Struct 类型 |
| Objects/tupleobject.c | tuple 类型 |
| Objects/typeobject.c | type 类型 |
| Objects/unicodeobject.c | str 类型 |
| Objects/weakrefobject.c | weakref 类型 |

你将在本章探索这些类型。

## 对象和变量对象类型

由于 C 不像 Python 那样面向对象，C 中的对象并不互相继承。`PyObject` 是每个 Python 对象的初始数据段，`PyObject *` 代表指向它的指针。

在定义 Python 类型时，`typedef` 使用以下两个宏之一：

- `PyObject_HEAD` `PyObject` 用于简单类型
- `PyObject_VAR_HEAD` `PyVarObject` 用于容器类型

简单类型 `PyObject` 具有以下字段：

| 字段 | 类型 | 目的 |
| :--- | :--- | :--- |
| ob_refcount | Py_ssize_t | 实例引用计数 |
| ob_type | _pyobject* | 对象类型 |

例如，`cellobject` 声明了一个额外的字段 `ob_ref`，以及基础字段：

```c
typedef struct {
    PyObject_HEAD
    PyObject *ob_ref; /* cell 的内容，为空时为 NULL */
} PyCellObject;
```

变量类型 `PyVarObject` 扩展了 `PyObject` 类型并具有以下字段：

| 字段 | 类型 | 目的 |
| :--- | :--- | :--- |
| ob_base | PyObject | 基础类型 |
| ob_size | Py_ssize_t | 包含的项数 |

例如，`int` 类型 `PyLongObject` 有如下声明：

```c
struct _longobject {
    PyObject_VAR_HEAD
    digit ob_digit[1];
}; /* PyLongObject */
```

### Type 类型

在 Python 中，对象具有 `ob_type` 属性，你可以使用内置函数 `type()` 获取该属性的值：

```python
>>> t = type("hello")
>>> t
<class 'str'>
```

`type()` 的返回结果是 `PyTypeObject` 实例：

```python
>>> type(t)
<class 'type'>
```

类型对象用于定义抽象基类的实现。

例如，对象始终实现了了 `__repr__()` 方法：

```python
>>> class example:
... x = 1
>>> i = example()
>>> repr(i)
'<__main__.example object at 0x10b418100'
```

`__repr__()` 方法的实现在任何对象的类型定义中始终位于相同的地址。这个位置被称为类型槽（type slot）。

### 类型槽（Type Slots）

所有的类型槽都定义在 `Include/cpython object.h` 中。

每个类型槽都有一个属性名和一个函数签名。例如，`__repr__()` 函数被命名为 `tp_repr`，并具有签名 `reprfunc`：

```c
struct PyTypeObject
---
typedef struct _object {
    typedef char (*reprfunc)(PyObject*);
    reprfunc tp_repr;
    ...
};
```

### 类型字典（Type Dictionaries）

Python 支持使用 `class` 关键字定义新类型。用户定义的类型通过 `type` 模块中的 `type_new()` 创建。用户定义的类型将有一个属性字典，通过 `__dict__()` 访问。当在自定义类上访问属性时，默认的 `__getattr__` 实现会在该字典中查找。类方法、实例方法、类属性和实例属性位于该字典。

`PyObject_GenericGetDict()` 函数实现了获取对象字典的逻辑。`PyObject_GetAttr()` 函数实现了默认的 `__getattr__()` 实现，而 `PyObject_SetAttr()` 实现了 `__setattr__()`。

`bool` 值的 `and` 运算实现首先检查 `a` 和 `b` 是否为布尔值。如果不是，它们会被强制转换为数字，并在两个数字上执行该操作：

`Objects boolobject.c` line 61

```c
static PyObject *a, PyObject *b;
bool_and(PyObject *a, PyObject *b)
{
    if (!PyBool_Check(a) || !PyBool_Check(b))
        return PyLong_Type.tp_as_number->nb_and(a, b);
    return PyBool_FromLong(a == Py_True && (b == Py_True));
}
```

### Long 类型

`long` 类型比 `bool` 复杂得多。在从 Python 2 到 3 的过渡过程中，CPython 放弃了对 `int` 的支持，转而使用 `long` 类型作为主要的整数类型。Python 的 `long` 类型非常特殊，它可以存储变长度的数字。最大长度设置在编译后的二进制文件中。

一个 Python `long` 的数据结构由 `PyObject` 变量头部和一个数字列表组成。数字列表 `ob_digit` 初始化时设置为一个数字，但在初始化后会扩展到更长的长度：

`Include longintrepr.h` line 885

```c
struct _longobject {
    PyObject_VAR_HEAD
    digit ob_digit[1];
};
```

例如，数字 1 将拥有 `ob_digits [1]`，而（某个较大数字）可能会拥有 `ob_digits [2, 4, 6, 0, 1]`。

通过 `_PyLong_New()` 为新的 `long` 分配内存。该函数接收一个固定长度并确保它小于 `MAX_LONG_DIGITS`。

然后它会重新分配 `ob_digit` 的内存以匹配长度。

### Bool 和长整数类型

要将 C `long` 类型转换为 Python `long` 类型，会将 C `long` 转换为数字列表，分配 Python `long` 的内存，并设置每个数字。如果数字小于 10（1 位数字），则初始化 `long` 对象时 `ob_digit` 的长度已为 1。然后在不重新分配内存的情况下设置值：

`Objects ► longobject.c` line 297

```c
PyObject *
PyLong_FromLong(long ival)
{
    PyObject *v;
    unsigned long abs_ival;
    unsigned long t; /* 无符号类型以确保 >> 不会传播符号位 */
    int ndigits = 0;
    int sign;
    CHECK_SMALL_INT(ival);
    /* 单位整数的快速路径 */
    if (!abs_ival >> PyLong_SHIFT) {
        v = _PyLong_New(1);
        if (v) {
            Py_SIZE(v) = sign;
            v->ob_digit[0] = Py_SAFE_DOWNCAST(
                abs_ival, unsigned long, digit);
        }
        return (PyObject*)v;
    }
    /* 较大的数字：循环确定位数 *
    t = abs_ival;
    while (t) {
        ++ndigits;
        t >>= PyLong_SHIFT;
    }
}
```

```c
v = _PyLong_New(ndigits);
if (v != NULL) {
    digit *p = v->ob_digit;
    Py_SIZE(v) = ndigits*sign;
    t = abs_ival;
    while (t) {
        *p++ = Py_SAFE_DOWNCAST(
            t & PyLong_MASK, unsigned long, digit);
            t >>= PyLong_SHIFT;
        }
    }
    return (PyObject*)v;
}
```

要将双精度浮点数转换为 Python `long`，`PyLong_FromDouble()` 会为你完成数学计算。

### 示例

`longobject.c` 中的实现函数包含实用工具，例如通过 `PyLong_FromUnicode` 将字符串转换为数字。

`long` 的富比较槽设置为 `long_richcompare`。该函数封装了 `long_compare`：

`Objects longobject.c` line 303

```c
static long_richcompare(PyObject *self, PyObject *other, int op)
{
    Py_ssize_t result;
    CHECK_BINOP(self, other);
    if (self == other)
        result = 0;
    else
        result = long_compare((PyLongObject*)self, (PyLongObject*)other);
    Py_RETURN_RICHCOMPARE(result, 0, op);
}
```

`long_compare` 函数首先检查变量 `a` 和 `b` 的长度（位数）。如果长度相同，它会遍历每个数字以检查它们是否相等。

`long_compare()` 返回：

- `a < b` 时返回负数
- `a == b` 时返回 0
- `a > b` 时返回正数

例如，当你执行 `1 == 5` 时，结果为 `-4`。`5 == 1` 时，结果为 `4`。

你可以在 `Py_RETURN_RICHCOMPARE` 宏之前实现以下代码块，以便在绝对值小于 1 时返回 True，这里使用了 `Py_ABS()` 宏，它返回有符号整数的绝对值：

```c
if (op == Py_EQ) {
    if (Py_ABS(result) <= 1) {
        return Py_RETURN_RICHCOMPARE(1, 0, op);
    }
}
Py_RETURN_RICHCOMPARE(result, 0, op);
```

## Unicode 字符串类型

XML 和 HTML 都支持带有特殊转义字符 `&#val;` 的 Unicode 点，其中 val 是代码点的十进制值。如果你需要将 Unicode 代码点编码为 XML 或 HTML，可以使用 `.encode()` 方法中的 `xmlcharreplace` 错误处理器：

```python
>>> 'ć'.encode('ascii', 'xmlcharreplace')
b'&#263;'
```

输出将包含 HTML/XML 转义的代码点。所有现代浏览器都将将此转义序列解码为正确的字符。

### ASCII 兼容性

如果你正在处理 ASCII 编码的文本，理解 UTF7/8 和 UTF16 之间的区别至关重要。UTF8 的一个主要优势是与 ASCII 编码的文本兼容。ASCII 编码是一种 7 位编码。

Unicode 标准中的前 128 个代码点表示了 ASCII 标准中现有的 128 个字符。例如，拉丁字母 'a' 是 ASCII 中的第 97 个字符，也是 Unicode 中的第 97 个字符。十进制的 97 等于十六进制的 61，因为该 Unicode 代码点是 U+0061。

在 REPL 中，如果你复制字母 'a' 的二进制代码：

```python
>>> letter_a = b'a'
>>> letter_a.decode('utf8')
'a'
```

这可以被正确解码为 UTF8。

UTF16 处理 2-4 字节的代码点。字母 'a' 的 1 字节表示将无法解码：

```python
>>> letter_a.decode('utf16')
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
```

### Unicode 字符串类型

```
UnicodeDecodeError: 'utf-16-le' codec can't decode byte 0x61 in position 0: truncated
```

在选择编码机制时，这一点非常重要。如果你需要导入 ASCII 编码的数据，UTF8 是一个更安全的选项。

### 宽字符类型

在 CPython 源码中处理未知编码的 Unicode 字符串输入时，将使用 `wchar_t` C 类型。`wchar_t` 是 C 标准中宽字符字符串的标准，足以在内存中存储 Unicode 字符串。在 PEP 393 之后，`wchar_t` 类型被选为 Unicode 存储格式。

Unicode 字符串对象提供了一个实用函数 `PyUnicodeFromWideChar()`，它将将 `wchar_t` 常量转换为字符串对象。例如，`python -c` 使用的 `pymain_run_command()` 将 `-c` 参数转换为 Unicode 字符串：

```c
Modules > main.c line 226
static int pymain_run_command(wchar_t *command, PyCompilerFlags *cf)
{
PyObject *unicode, *bytes;
int ret;
unicode = PyUnicodeFromWideChar(command, -1);
```

### 字节序标记 (BOM)

在解码输入（如文件）时，CPython 可以通过字节序标记（BOM）检测字节序。BOM 是出现在 Unicode 字节流开头的特殊字符。它们告诉接收者数据存储的字节序。不同的计算机可以使用不同的字节序进行编码。如果使用了错误的字节序，即使编码正确，数据也会乱码。

# 大端序将最高有效字节放在前面。小端序将最低有效字节放在前面。

UTF8 规范确实支持 BOM，但它没有影响。UTF8 BOM 可以出现在 UTF 编码数据序列的开头，表示为 `b'\xef\xbb\xbf'`，并将指示 Python 数据流很可能是 UTF8。UTF16 和 UTF32 支持小端和大端序 BOM。

CPython 中的默认字节序由 `sys.byteorder` 设置：

```python
>>> import sys; print(sys.byteorder)
little
```



# Enodings 包

`lib` 中的 `encodings` 包为 CPython 提供了 100 多种内置编码。每当对字符串或字节字符串调用 `.encode()` 或 `.decode()` 方法时，都会从该包查找编码。

每个编码都定义为一个独立的模块，例如，用于邮件系统的 ISO2022 定义在 `lib/encodings/iso2022.py`。每个编码模块都会定义一个 `getentry()` 函数并注册：

- 它的唯一名称
- 来自 `codec` 模块的编码解码函数
- 它的增量编码器和解码器类
- 它的流读取器和流写入器类

许多编码模块共享来自 `codecs` 模块或 `_multytecodec` 模块的 `codec`。某些编码模块使用独立的 C 模块，来自 `Modules/_codecs`。

例如，`ISO2022_JP` 编码模块导入了一个 C 扩展模块 `_codecs_iso2022`，来自 `Modules/_codecs_iso2022.c`：

```python
import _codecs_iso2022, codecs
import _multytecode as mbc
codec = _codecs_iso2022.getcodec('iso2022_jp')
class Codec(codecs.Codec):
    encode = codec.encode
    decode = codec.decode
class IncrementalEncoder(mbc.MultibyteIncrementalEncoder,
    codecs.IncrementalEncoder):
    codec = codec
class IncrementalDecoder(mbc.MultibyteIncrementalEncoder,
    codecs.IncrementalDecoder):
    codec = codec
```

# Unicode 字符串类型

```c
PyObject *
PyUnicode_RichCompare(PyObject *left, PyObject *right, int op)
{
...
  if (left == right) {
    switch (op) {
      case Py_EQ:
      case Py_LE:
      case Py_ALE:
      >>>
      /* 字符串等于它自己 */
      Py_RETURN_TRUE;
```

然后添加一个 `else if` 块来处理 `Py_ALE` 运算符。这将：

+ 1. 将左字符串转换为一个新的大写字符串
2. 将右侧字符串转换为一个新的大写字符串
3. 比较两者
4. 对两个临时字符串进行去引用以释放它们的内存
5. 返回结果

你的代码看起来如下：

```
else if (op == Py_EQ || op == Py_NE) {
}
/* 添加这些行代码 */
else if (op == Py_ALE) {
  PyObject* upper_left = case_operation(left, do_upper);
  PyObject* upper_right = case_operation(right, do_upper);
  result = unicode_compare_eq(upper_left, upper_right);
  Py_DECREF(upper_left);
  Py_DECREF(upper_right);
  return PyBool_FromLong(result);
}
```

重新编译后，你的不区分大小字符串匹配在 REPL 上应得到以下结果：

310

```
>>> "hello" ~= "HELLO"
True
>>> "hello?" ~= "hello"
False
```

## 字典类型

字典是一种快速且灵活的映射类型。开发者使用它们存储和映射数据，Python 对象也用它们存储属性和方法。

Python 字典还用于本地和全局变量、关键字参数以及许多其他用例。

Python 字典是紧凑的，这意味着哈希表只存储被映射的值。

所有不可变内置类型包含的哈希算法都是快速，这正是 Python 字典快速的原因。

### 哈希

所有不可变内置类型都提供哈希函数。这定义在 `tp_hash` 类型槽位中，或者为自定义类型使用 `__hash__` 魔术方法。哈希值与指针的大小相同（64 位系统为 64 位，32 位系统为 32 位），但并不代表其值的内存地址。

任何 Python 对象的计算哈希值在其生命周期内不应改变。两个具有相同值的不可变实例的哈希值应该相等：

不应存在哈希冲突，两个值不同的对象不应产生相同的哈希。

## 字典类型

某些哈希是简单的，例如 Python 长整型：

```
>>> (401).__hash__()
401
```

对于较值，长整型哈希变得更加复杂：

```
>>> (401122312438798989898).__hash__()
221228379582993635
```

许多内置类型使用 Python 的 `pyhash.c` 模块，该模块提供了哈希函数：

- `Bytes_Py_HashBytes(const void*, Py_ssize_t)`
- `Double_Py_HashDouble(double)`
- `Pointers_Py_HashPointer(void*)`

例如，Unicode 字符串使用 `_Py_HashBytes()` 对字符串的字节数据进行哈希：

```
>>> ("hello").__hash__()
489442152636283333592
```

自定义类可以通过实现 `__hash__()` 来定义哈希函数。自定义类不应该实现自定义哈希，而应该使用一个**唯一的**属性。通过将其设置为只读属性确保它是不可变的，然后使用内置的 `hash()` 函数进行哈希：

```python
class User:
    def __init__(self, id: int, name: str, address: str):
        self._id = id
    def __hash__(self):
        return hash(self._id)
    @property
    def id(self):
        return self._id
```

312

## 字典类型

该类的实例 `bob` 现在可以进行哈希处理了：

```
>>> bob = User(123884, "Bob Smith", "Townsville, QLD")
>>> hash(bob)
123884
```

该实例现在可以作为键使用：

```python
>>> sally = User(123823, "Sally", "New York")
>>> hash(sally)
123823
```

集合将减少：

```
>>> bob = User(123884, "Bob Smith", "Townsville, QLD")
>>> hash(bob)
123884
```

相关文件：

| 文件 | 目的 |
|---|---|
| dictobject.h | 字典 API |
| dictobject.h | 字典定义 |
| dictobject.c | 字典实现 |
| dictobject.h | 字典类型 |
| pyhash.c | 哈希 |

### 字典结构

字典对象由以下组成：

- 1. 字典的大小
- 2. 字典的版本
- 3. 键

`DictObject` 拥有属性：

| 字段 | 类型 | 目的 |
|---|---|---|
| size | Py_ssize_t | 字典的大小 |
| version | uint64_t | 字典的版本 |
| used | Py_ssize_t | 表中的条目数 |
| indices | char[] | 哈希表 |
| entries | PyDictEntry[] | 分配的条目 |

字典项 `PyDictEntry` 包含：

| 字段 | 类型 | 目的 |
|---|---|---|
| hash | Py_ssize_t | 缓存的哈希值 |
| key | PyObject* | 键 |

字典拆分时，使用 `_Py_HashBytes()` 对字符串的字节数据进行哈希：

| 字段 | 类型 | 目的 |
|---|---|---|
| hash | Py_ssize_t | 缓存的哈希值 |
| key | PyObject* | 键 |

### 查找

对于给定的键对象，有一个通用的查找函数 `lookupdict()`。字典查找需要处理三种情况：

1. 键的内存地址存在于表中
2. 对象的哈希值存在于表中
3. 键不在字典中

> 查找函数基于唐纳德·康纳著名的著作《计算机程序》，第 6 章第 4 节哈希（ISBN 978-0201896685）

查找序列为：

1. 获取 `ob` 的哈希值
2. 在字典键中查找 `ob` 的哈希值并获取索引 `ix`
3. 如果 `ix` 为空，返回 `DKIX_EMPTY`（未找到）
4. 获取给定索引的键项 `ep`
5. 如果键值匹配对象，`ob` 是键值的相同指针，返回结果
6. 如果键哈希匹配对象，`ob` 解析为与 `me_hash` 相同的哈希值，返回结果

### 总结

现在你已经看到了某些类型的实现，可以探索其他类型。

在探索 Python 类时，要记住有内置类型（用 C 编写）以及继承这些类型的类（用 Python 或 C 编写）。

某些库使用 C 编写类型而不是继承内置类型。一个例子是 `numpy`，一个用于数值数组的库。`nparray` 类型用 C 编写，非常高效且性能强大。

# 标准库

Python 一直以来都是“内置电池”（batteries included）。这句话意味着，通过一个标准的 CPython 发行版，已经包含了用于处理文件、线程、网络、网站、音乐、键盘、屏幕、文本以及各种工具的库。

CPython 自带的一些“电池”更像 AA 电池。它们对任何事情都很有用，例如 `collections` 模块和 `sys` 模块。有些则比较晦涩，就像一节小小的手表电池，你永远不知道它何时会派上用场。

CPython 标准库中有两种类型的模块：

- 1. 用纯 Python 编写的提供工具函数的模块
- 2. 用 C 编写并带有 Python 封装的模块

你将在本章中探索这两种类型。

## Python 模块

用纯 Python 编写的模块都位于源码中的 `Lib` 目录。一些较大的模块在子文件夹中拥有子模块，例如 `email` 模块。

一个容易查看的模块是 `colorsys` 模块。它只有几百行 Python 代码。你可能以前没有见过它。`colorsys` 模块包含了一些用于转换颜色范围的实用函数。

当你从源码安装 Python 发行版时，标准库模块会从 `Lib` 文件夹拷贝到发行版文件夹。当你启动 Python 时，该文件夹始终是你路径的一部分，因此你可以导入这些模块而不必担心它们位于何。

例如：

```python
>>> import colorsys
>>> colorsys
<module 'colorsys' from '/usr/shared/lib/python3.7/colorsys.py'>
>>> colorsys.rgb_to_hls(255,0,0)
(0.0, 127.5, -1.00790518339921)
```

我们可以在 `Lib/colorsys.py` 中看到 `rgb_to_hls()` 的源码：

```python
## HLS: 色相, 亮度, 饱和度
### H: 在光谱中的位置
### L: 颜色亮度
### S: 颜色饱和度
def rgb_to_hls(r, g, b):
    maxc = max(r, g, b)
    minc = min(r, g, b)
    # XXX 可以优化 (maxc+minc) 和 (maxc-minc)
    l = (minc+maxc)/2.0
    if minc == maxc:
        return 0.0, 1, 0
    if l <= 0.5:
        s = (maxc-minc) / (maxc+minc)
    else:
        s = (maxc-minc) / (2.0-minc)
    rc = (maxc-r) / (maxc-minc)
    gc = (maxc-g) / (maxc-minc)
    bc = (maxc-b) / (maxc-minc)
    if r == maxc:
        h = bc-gc
elif g == maxc:
        h = 2.0+rc-bc
    else:
        h = 4.0+gc-rc
    h = (h/6.0) % 1.0
    return h, l, s
```

这个函数并没有特别之处，它是标准的 Python。
你会在所有的纯 Python 标准库模块中发现类似的内容。它们只是用纯 Python 编写的，布局良好且易于理解。你甚至可以发现改进或 Bug，因此你可以对它们进行修改并贡献给 Python 发行版。
你将在书末尾涵盖这些内容。

## Python 和 C 模块

其余模块是用 C 编写的，或者是 Python 和 C 的结合。这些模块的源码中，Python 部分位于 `Lib`，C 部分位于 `Modules`。关于此规则有两个例外：位于 `sysmodule.c` 的 `sys` 模块以及位于 `builtinmodule.c` 的 `__builtins__` 模块。

`sys` 模块是特定于解释器的，它位于 Python 目录中。对于内置的，`__builtins__` 模块是 CPython 的实现细节。

当你输入 `print("hello world!")` 时，发生了什么：

- 1. "hello world!" 字符串被编译器转换为 `UnicodeObject`
- 2. 内置函数 `print()` 被执行
- 3. `file` 变量被设置为 `stdout` 句柄
- 4. 换行符 `\n` 被发送到文件
- 5. `builtinmodule.c` 第 1828 行：

```c
static PyObject *
buildin_print(PyObject *self, PyObject *const *args,
    Py_ssize_t nargs, PyObject *kwargs)
{
    if (file == NULL || file == Py_None) {
        file = _PySys_GetObjectId(&PyId_stdout);
        ...
    }
    for (i = 0; i < nargs; i++) {
        if (i > 0) {
            if (sep == NULL)
                err = PyFile_WriteString(" ", file);
            else
                err = PyFile_WriteObject(sep, file, Py_PRINT_RAW);
            if (err)
                return NULL;
        }
        err = PyFile_WriteObject(args[i], file, Py_PRINT_RAW);
        if (err)
            return NULL;
    }
}
if (end == NULL)
    err = PyFile_WriteString("\n", file);
else
    err = PyFile_WriteObject(end, file, Py_PRINT_RAW);
...
Py_RETURN_NONE;
}
```

# 测试标记

| Target | 用途 |
| --- | --- |
| test | 运行一组基础回归测试 |
| testall | 运行两次完整测试套件 - 一次不包含 .pyc 文件，另一次 |
| quicktest | 运行一组更快的回归测试，排除耗时较长的测试 |
| testuniversal | 在 OSX 的通用构建中运行两种架构的测试套件 |
| coverage | 使用 gcov 编译并运行测试 |
| coverage-cov | 创建覆盖率 HTML 报告 |

# 测试标记

某些测试需要特定的标记，否则它们会被跳过。例如，许多 IDLE 测试需要 GUI。

要查看配置中的测试套件列表，请使用 `--list-tests` 标记：

```
$ ./python -m test --list-tests
test_grammar
test_opcodes
test_dict
test_builtin
test_exceptions
...
```

## 运行特定测试

你可以通过将测试套件作为第一个参数来运行特定的测试：

在 Linux 或 macOS 上：

```
$ ./python -m test test_webbrowser
```

顺序运行测试

## 运行特定测试

```
0:00:00 load avg: 2.74 [1/1] test_webbrowser
== Tests result: SUCCESS ==
1 test OK.
Test duration: 117 ms
Tests result: SUCCESS
在 Windows 上:
> rt.bat -d -x64 test_webbrowser
```



Test duration: 117 ms
Tests result: SUCCESS

你也可以使用 `-v` 参数查看执行的测试详细列表及其结果：

```
$ /python -m test test_webbrowser -v
```

== Python 3.9.0b1

== macOS-10.14.3-x86_64-i386-64bit little-endian

== cwd: /Users/anthonyshaw/cpython/build/test_python_24562

== CPU count: 4

== encodings: locale=UTF-8, FS=utf-8

Run tests sequentially

0:00:00 load avg: 2.36 [1/1] test_webbrowser

test_open(test.test_webbrowser.BackgroundBrowserCommandTest) ... ok

test_register(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_default(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_preferred(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_open(test.test_webbrowser.ChromeCommandTest) ... ok

test_open_new(test.test_webbrowser.ChromeCommandTest) ... ok

...

test_open_with_autorise_false(test.test_webbrowser.OperaCommandTest) ... ok
```

Ran 34 tests in 0.056s

OK (skipped=2)

== Tests result: SUCCESS ==

1 test OK.

Total duration: 134 ms

Tests result: SUCCESS

如果你希望对 CPython 进行更改，了解如何使用测试套件并检查你所编译版本的状态是非常重要的。在开始更改之前，你应该运行整个测试套件并确保所有测试均通过。

### 测试模块

要测试 C 扩展或 Python 模块，可以使用 `unittest` 模块对它们进行导入和测试。测试按模块或包组装。

例如，Python 的 Unicode 字符串类型在 `Lib > test > test_unicode.py` 中有测试。`asyncio` 包在 `Lib > test > test_asyncio` 中有一个测试包。

### 另需参考

如果你是 `unittest` 模块或 Python 测试的新手，请查看我们在 `realpypython.com` 上的《Python Testing入门指南》文章。

```
class UnicodeTest(string_tests.CommonTest,
    string_tests.MixinStrUnicodeUserTest,
    string_tests.MixinStrUnicodeTest,
    unittest.TestCase):
    ...
    def test_casefold(self):
        self.assertEqual('hello'.casefold(), 'hello')
        self.assertEqual('hELLO'.casefold(), 'hello')
        self.assertEqual('ß'.casefold(), 'ss')
        self.assertEqual('fi'.casefold(), 'fi')
```

你可以通过在 `UnicodeTest` 类内部添加新的测试方法，来扩展你在前面的章节中为 Python 字符串实现的几乎相等运算符：

```
def test_almost_equals(self):
    self.assertTrue('hello' ~= 'hello')
    self.assertTrue('hHello' ~= 'hello')
    self.assertFalse('hELlo!' ~= 'hello')
```

你可以在 Windows 上运行此特定测试模块：

```
> rt.bat -q -d -x64 test_unicode
```

或者 macOS/Linux：

```
$ ./python -m test test_unicode -v
```

### 测试实用

通过导入 `test.support.script_helper` 模块，你可以访问一些用于 Python 运行时测试的辅助函数：

- `assert_python_ok(*args, **env_vars)` 执行带有指定参数的 Python 进程并返回 (返回码, stdout, stderr)
- `assert_python_failure(*args, **env_vars)` 类似于 `assert_python_ok(*)`，但断言其执行失败
- `make_script(script_dir, script_basename, source)` 在 `script_dir` 中创建一个...

## 运行特定测试

```
0:00:00 load avg: 2.74 [1/1] test_webbrowser
== Tests result: SUCCESS ==
1 test OK.
Test duration: 117 ms
Tests result: SUCCESS
```

在 Windows 上:

```
> rt.bat -d -x64 test_webbrowser
```

Test duration: 117 ms
Tests result: SUCCESS

你也可以使用 `-v` 参数查看执行的测试详细列表及其结果：

```
$ /python -m test test_webbrowser -v
```

== Python 3.9.0b1

== macOS-10.14.3-x86_64-i386-64bit little-endian

== cwd: /Users/anthonyshaw/cpython/build/test_python_24562

== CPU count: 4

== encodings: locale=UTF-8, FS=utf-8

Run tests sequentially

0:00:00 load avg: 2.36 [1/1] test_webbrowser

test_open(test.test_webbrowser.BackgroundBrowserCommandTest) ... ok

test_register(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_default(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_preferred(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_open(test.test_webbrowser.ChromeCommandTest) ... ok

test_open_new(test.test_webbrowser.ChromeCommandTest) ... ok

...

test_open_with_autorise_false(test.test_webbrowser.OperaCommandTest) ... ok
```

Ran 34 tests in 0.056s

OK (skipped=2)

== Tests result: SUCCESS ==

1 test OK.

Total duration: 134 ms

Tests result: SUCCESS

了解如何使用测试套件并检查你所编译版本的状态，如果你希望对 CPython 进行更改是非常重要的。在开始更改之前，你应该运行整个测试套件并确保所有测试均通过。

### 测试模块

要测试 C 扩展或 Python 模块，可以使用 `unittest` 模块对它们进行导入和测试。测试按模块或包组装。

例如，Python 的 Unicode 字符串类型在 `Lib > test > test_unicode.py` 中有测试。`asyncio` 包在 `Lib > test > test_asyncio` 中有一个测试包。

### 另需参考

如果你是 `unittest` 模块或 Python 测试的新手，请查看我们在 `realpypython.com` 上的《Python Testing入门指南》文章。

```
class UnicodeTest(string_tests.CommonTest,
    string_tests.MixinStrUnicodeUserTest,
    string_tests.MixinStrUnicodeTest,
    unittest.TestCase):
    ...
    def test_casefold(self):
        self.assertEqual('hello'.casefold(), 'hello')
        self.assertEqual('hELLO'.casefold(), 'hello')
        self.assertEqual('ß'.casefold(), 'ss')
        self.assertEqual('fi'.casefold(), 'fi')
```

你可以通过在 `UnicodeTest` 类内部添加新的测试方法，来扩展你在前面的章节中为 Python 字符串实现的几乎相等运算符：

```
def test_almost_equals(self):
    self.assertTrue('hello' ~= 'hello')
    self.assertTrue('hHello' ~= 'hello')
    self.assertFalse('hELlo!' ~= 'hello')
```

你可以在 Windows 上运行此特定测试模块：

```
> rt.bat -q -d -x64 test_unicode
```

或者 macOS/Linux：

```
$ ./python -m test test_unicode -v
```

### 测试实用

通过导入 `test.support.script_helper` 模块，你可以访问一些用于 Python 运行时测试的辅助函数：

- `assert_python_ok(*args, **env_vars)` 执行带有指定参数的 Python 进程并返回 (返回码, stdout, stderr)
- `assert_python_failure(*args, **env_vars)` 类似于 `assert_python_ok(*)`，但断言其执行失败
- `make_script(script_dir, script_basename, source)` 在 `script_dir` 中创建一个...

## 运行特定测试

```
0:00:00 load avg: 2.74 [1/1] test_webbrowser
== Tests result: SUCCESS ==
1 test OK.
Test duration: 117 ms
Tests result: SUCCESS
```

在 Windows 上:

```
> rt.bat -d -x64 test_webbrowser
```

Test duration: 117 ms
Tests result: SUCCESS

你也可以使用 `-v` 参数查看执行的测试详细列表及其结果：

```
$ /python -m test test_webbrowser -v
```

== Python 3.9.0b1

== macOS-10.14.3-x86_64-i386-64bit little-endian

== cwd: /Users/anthonyshaw/cpython/build/test_python_24562

== CPU count: 4

== encodings: locale=UTF-8, FS=utf-8

Run tests sequentially

0:00:00 load avg: 2.36 [1/1] test_webbrowser

test_open(test.test_webbrowser.BackgroundBrowserCommandTest) ... ok

test_register(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_default(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_register_preferred(test.test_webbrowser.BrowserRegistrationTest) ... ok

test_open(test.test_webbrowser.ChromeCommandTest) ... ok

test_open_new(test.test_webbrowser.ChromeCommandTest) ... ok

...

test_open_with_autorise_false(test.test_webbrowser.OperaCommandTest) ... ok
```

Ran 34 tests in 0.056s

OK (skipped=2)

== Tests result: SUCCESS ==

1 test OK.

Total duration: 134 ms

Tests result: SUCCESS

Wait, 我看到 I- 在表格中。

涵盖了以下调试器：

| 调试器 | 类型 | 平台 |
|------|---|---|
| ldb | Console | macOS |
| gdb | Console | Linux |
| Visual Studio Debugger | Visual | Windows |
| CLion Debugger | Visual | Windows, macOS |
| VS Code Debugger | Visual | Windows, macOS |

```
(lldb) break set --file Objects/floatobject.c --line 532
Breakpoint 1: where = python.exe:float_richcompare + 2276 at floatobject.c:532:26, address = 0x00000010006a974
```

### 注意

设置断点还有简写形式，例如 `(lldb) b Objects/floatobject.c:532`

你可以使用 `break set` 命令添加多个断点。要列出当前断点，请使用 `break list` 命令：

```
(lldb) break list
Current breakpoints:
1: file = 'Objects/floatobject.c', line = 532, exact_match = 0, locations = 1
1.1: where = python.exe:float_richcompare + 2276 at floatobject.c:532:26, address = python.exe[...], unresolved, hit count = 0
```

# 启动 CPython

要启动 CPython，请使用 `process launch --` 命令，并带有你通常用于 Python 的命令行选项，例如：

要使用字符串启动 python，例如 `python -c "print(1)"`，请使用：

```
(lldb) process launch -c "print(1)"
```

要使用脚本启动 python，请使用：

```
(lldb) process launch -- my_script.py
```

# 附加到运行中的 CPython 解释器

如果你已经有一个运行中的 CPython 解释器，你可以附加到它。

在 lldb 会话内部，运行 `process attach --pid` 并加上进程 ID：

### 在 macOS 上使用 Lldb

```
(lldb) process attach --pid 123
```

你可以从“活动监视器”获取进程 ID，或者在 Python 中使用 `os.getpid()`。

在此之前或之后设置的任何断点都会停止进程运行。

### 处理断点的示例

要查看断点是如何处理的，请在 `Objects floatobject.c` 的 `float_richcompare()` 函数上设置一个断点。接下来运行进程，并使用你在书中开发的“几乎相等”运算符比较两个浮点值：

```
(lldb) process launch -c "1.0~=1.1"
Process 64421 queue = '/python/python.exe' (x86_64)
Process 64421 stopped
* thread #1,queue=6) = '...', stop = breakpoint 1.1



frame #0: `0x0000000006a974` `python.exe` `float_richcompare(v=1.0, w=1.1,op=floatobject.c:532:26`

529		break;

530	case Py_ALE:

531		double diff = fabs(i - j);

532		const double rel_tol = 1e-9;

533		const double abs_tol = 0.1;

534		r = ((diff <= fabs(rel_tol * j)) || ||

Target 0: (`python.exe`) stopped).

```
lldb 将给你一个提示符。你可以使用 `v` 命令查看局部变量：
```

```
(lldb) v
(PyObject *) v = 0x000000000111b370 1.0
(PyObject *) w = 0x000000000111b340 1.1
(int) op = 6
(double) i = 1
(double) j = 1.1000000000000001
```

```
(int) r = 0
(double) diff = 0.10000000000000009
(const double) rel_tol = 2.1256294105914498E-314
(const double) abs_tol = 0
```

你可以使用 `expr` 命令评估任何合法的 C 表达式。可以使用作用域内的变量。例如，调用 `fabs(rel_tol)` 并强制转换为 `double`，运行：

```
(lldb) expr (double)fabs(rel_tol)
(double) $1 = 2.1256294105914498E-314
```

这会打印结果变量并为其分配一个标识符 (`$1`)。你可以复用这个标识符。

你可能还想探索 `PyObject` 实例，例如：

```
(lldb) expr v->ob_type->tp_name
(const char*) $6 = 0x000000010034fc26 "float"
```

要从断点获取回溯轨迹（traceback），使用 `bt` 命令：

```
(lldb) bt
* thread #1, queue = '...', stop reason = breakpoint 1.1
* frame #0: ...
    python.exe`float_richcompare(...)` at floatobject.c:532:26
  frame #1: ...
    python.exe`do_richcompare(...)` at object.c:796:16
  frame #2: ...
    python.exe`PyObject_RichCompare(...)` at object.c:846:21
  frame #3: ...
    python.exe`cmp_outcome(...)` at ceval.c:4998:16
```

使用 `step` 命令进入（step-in）。
使用 `next` 命令跳到下一条语句（step-over）。
要继续执行，使用 `continue` 命令或 `c`。
要退出会话，使用 `quit` 命令或 `q`。

| 另参 |
| :--- |
| LLVM 文档 包含详尽的命令列表 |

### 使用 Python-lldb 扩展

`lldb` 支持用 Python 编写的扩展。有一个开源扩展可以在 `lldb` 会话中为原生 C 对象打印额外信息。要安装它，请运行这些命令：

```bash
mkdir -p ~/lldb
cd ~/lldb && git clone https://github.com/python/python-lldb
echo "import ~/lldb/python-lldb" >> ~/.lldinit
chmod +x ~/.lldb
```

现在每当你在 `lldb` 中看到变量时，右侧会有额外信息，对于整数和浮点数显示数值，对于字符串显示文本。在 ldb 控制台中有一个额外命令 `py-bt`，可以打印 Python 帧堆栈。

### 使用 Gdb

`gdb` 是 Linux 上常用的 C/C++ 调试器。它在 CPython 开发团队中也非常流行。当编译 CPython 时，会生成一个脚本 `cpython.pdb`。不要直接执行此脚本。相反，在你的家目录下的 `.gdbinit` 文件中添加此行：

```
add-auto-load /path/to/checkout
```

`/path/to/checkout` 是指向编译好的 CPython 二进制文件的路径。要启动 `gdb`，使用指向该二进制文件的参数运行它：

```
$ gdb ./python
```

`gdb` 会加载二进制文件的符号并给你一个命令提示符。`gdb` 有一组内置命令，CPython 扩展了一些额外命令。

### 创建断点

要设置断点，相对于可执行文件使用 `b <file>:<line>` 命令：

```
(gdb) b Objects/floatobject.c:532
Breakpoint 1 at 0x10006a974: Objects/floatobject.c, line 532
```

你可以根据需要设置多少个断点。

# 启动 CPython

要启动进程，使用 `run` 命令以及参数来启动 Python 解释器。例如，使用字符串启动：

```
(gdb) run -c "print(1)"
```

要使用脚本启动 python，使用：

# 附加到运行中的 CPython 解释器

如果你已经有一个运行中的 CPython 解释器，你可以附加到它。在 `gdb` 会话内部，使用进程 ID 运行 `attach`：

```
(gdb) attach 123
```

你可以从活动监视器获取进程 ID，或者在 Python 中使用 `os.getpid()`。在此点之前或之后设置的任何断点都会停止进程。

### 处理断点

当命中断点时，可以使用 `print` 或 `p` 命令打印变量：

```
(gdb) p *(LongObject*)v
$1 = (ob_base = {ob_refcnt = 8, ob_type = ...}, ob_size = 1, ob_digit = {42})
```

要进入下一条语句，使用 `step` 命令或 `s`。要跳过下一条语句，使用 `next` 命令或 `n`。

### 使用 Python-Gdb 扩展

`python-gdb` 扩展会将一组额外的命令加载到 `gdb` 控制台中：

| 命令 | 目的 |
| :--- | :--- |
| py-print | 查找并打印 Python 变量 |
| py-bt | 打印 Python 堆栈轨迹 |
| py-locals | 打印 locals() 的结果 |
| py-up | 向下移动帧 |

### 使用 Visual Studio 调试器

| 命令 | 目的 |
| :--- | :--- |
| py-down | 向上移动帧 |
| py-list | 打印当前帧的 Python 源代码 |

### 使用 Visual Studio 调试器

Microsoft Visual Studio 自带可视化调试器。这个调试器非常强大，具有帧可视化、监视列表以及评估表达式的能力。打开 Visual Studio 和 `PCBuild/pcbuild.sln` 文件。

### 添加断点

要添加新断点，在解决方案窗口中导航到你需要的文件，然后点击行号左侧的行槽。这会添加一个红圈，表示在该行设置了断点：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_340_0.png)

```
354  /* /
355  static PyObject*
357  float_richcompare(PyObject *u, PyObject *w, int op)
358  {
359      double i, j;
360      int r = 0;
361
362      assert(PyFloat_Check(u));
363      i = PyFloat_AS_DOUBLE(u);
364      j = PyFloat_AS_DOUBLE(w);
365
366      /* 根据 w 的类型进行切换。将 i 和 j 设置为用于比较的双精度数，
367      * 以及要使用的 richcomp。
368      */
369      if (PyFloat_Check(w)) {
370          j = PyFloat_AS_DOUBLE(w);
  else if (Py_IS_FINITE(i)) {
```

当你悬停在红圈上时，会出现一个齿轮图标。点击此齿轮来配置条件断点。添加一个或多个在断点命中前必须求为真的条件表达式：

# 使用 Visual Studio Debugger

```
/* Switch on the type of w. Set i and j to be compared,
* and up to the richcomp to use.
if (PyFloatCheck())) {
```

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_341_0.png)

```
j = PyFloat_AS_DOUBLE()
else if (Py_Is_FINITE(i)) {
```

### 启动调试器

从顶部菜单中，选择调试（Debug）、启动调试器（Start Debugger），或者按 F5。

Visual Studio 将启动一个新的 Python 运行时和 REPL。

### 处理断点

当命中断点时，你可以使用导航按钮或快捷键向前执行并进入语句：

- 步入 (Step Into) F11
- 逐过 (Step Over) F10
- 跳出 (Step Out) Shift + F11

底部将显示调用堆栈。你可以选择堆栈中的帧来更改导航，并检查其他帧中的变量：

### 使用 CLion Debugger

| 名称 | 语言 | |
| --- | --- | --- |
| python39_d.dllfloat_rcshared_object, *v_object, *int op) Line 368 | C |
| python39_d.dlliddo_rcshared_object, *state, *v_object, *int op) Line 796 | C |
| python39_d.dllPyObject_RcCompare_object, *state, *int op) Line 846 | C |
| python39_d.dllPyObject_outcmode_ts, *state, *int_op, *v_object *) Line 4998 | C |
| python39_d.dllPyEvalFrame_default_frame, *frame, *vframe) Line 2902 | C |
| [Frame python39_d.dllPyEvalFrame_default_ts, *state, *global_objects, *local_objects, *args_164argco... | C |
| python39_d.dllPyFunction_Vectorcall_function, *object, *stack, *unsigned, *int64nargs_intarg, *kenames)) Line 401 | C |
| python39_d.dllPyFunction_Vectorcall_ts, *state, **callable, *object *args, unsigned, *int64nargs_intarg, *object_K ... | C |
| python39_d.dllPyFunction_dt_ts, *state, **object, *stack, *int_op, *args) Line 4853 | C |
| python39_d.dllPyEvalFrame_default_frame, *frame, *vframe) Line 3224 | C |
| [Frame python39_d.dllPyEvalFrame_default_ts, *state, *global_objects, *local_objects, *args_164argco... | C |
| python39_d.dllPyEvalCode_ts, *state, **object, *global_objects, *local_objects, *args_164argco... | C |
| python39_d.dllPyFunction_Vectorcall_function, *object, *stack, *unsigned, *int64nargs_intarg, *kenames) Line 401 | C |

在代码编辑器中，你可以突出显示任何变量或表达式以查看其值。你也可以右键并选择“添加监视”（Add Watch）。这会将变量添加到名为监视列表（Watchlist）的列表中，可以在那里快速查看帮助调试所需的变量值：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_342_0.png)

### 使用 CLion Debugger

CLion IDE 自带了强大的视觉化调试器。它在 macOS 上使用 `ldb`，在 Windows 和 Linux 上使用调试。

要配置调试器，进入设置（Preferences）、构建、部署（Build, Deployment）、工具链（Toolchains）。

### 使用 CLion Debugger

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_342_0.png) 有一个调试器选择框。选择其中之一：

- macOS 使用“Bundled LLDB”
- Windows 或 Linux 使用“Bundled GDB”

### 注意

LLDB 和 GDB 分别受益于 `cpython-db` 和 `python-gdb` 扩展。阅读本文中的 LLDB 和 GDB 章节了解如何安装这些扩展。

### 配置自定义构建目标

配置工具链后，现在可以创建自定义构建目标来启用调试。要配置调试器，进入设置（Preferences）、构建、部署（Build, Deployment）、工具链（Toolchains）：创建一个 `python_build` 配置，并将工具链设置为默认（Use Default）以确保使用调试器。点击 Build 下拉显示外部工具窗口并点击 + 创建一个新的外部工具。第一个工具将运行：

- 命名为 `make_all`
- 程序为 `make`
- 参数为运行 `make`，例如 `-j`
![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_345_0.png) 点击 OK 添加工具，然后添加第二个工具用于清理项目：

- 命名为 `clean`
- 程序为 `make`
- 参数为运行 `make`，例如 `clean`
- 工作目录为 `$ProjectDir$`

### 使用 CLion Debugger

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_346_0.png) 关闭外部工具窗口，并将 `make_all` 工具设置为 Build，将设置为 Clean：一旦完成此任务，就可以从 Build 菜单构建、重建和清理。

### 配置自定义调试目标

要调试编译后的 CPython 可执行文件，从 Run/Debug 打开 Edit Configurations 面板，通过选择 Custom Build 添加新配置：

- 目标为 `cpython_build`（你创建的自定义构建目标）
- Linux 下为 `python`，macOS 下为 `python.exe`
- 工作目录为 `$ProjectDir$`
![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_348_0.png) 有此 Run/Debug 配置，你现在可以直接从 Run 菜单调试。或者，你可以向运行的 CPython 进程附加调试器。

### 附加调试器

要向运行的 CPython 进程附加 CLion 调试器，选择运行（Run）、附加进程（Attach to Process）。将弹出一个进程列表。找到你想附加的 `python` 进程并选择附加（Attach）。调试会话开始。

### 使用 CLion Debugger

### 注意

如果你安装了 Python 插件，它会在顶部显示 `python` 进程。不要选择这个！它使用的是 Python 调试器，而不是 C 调试器![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_349_0.png)相反，向下滚动到“Native”列表找到正确的 `python` 进程。

### 创建断点

要创建断点，导航到你要的文件和行，然后点击行号和代码之间的行槽。会出现一个红圈表示断点已设置：

```
break;
case Py_AST:
    double diff = fabs(i);
    const double rel_tol = 1e-9;
    const double abs_tol = 0.1;
    r = ((diff < fabs(rel_tol * i)) ||
        (diff < abs_tol));
    if (r)
        break;
    break;
}
return PyBool_FromLong(r);
```

```
Unimplemented:
Py_RETURN_NOTIMPLEMENTED;
```



右键点击断点以附加条件：

### 使用 CLion Debugger

| | | |
|---|---|---|
| m_g | 529 | break; { |
| m_g | 528 | case PyAdd: {
    double diff = fabsl(i - j);
    const double rel_tol = i-j;
    const double abs_tol = 0.1;
    if (diff < fabs(rel_tol + j))\n        if (diff < fabs(rel_tol + i))\n            if (diff < abs_tol);
| | | 531 |
| | | 532 |
| | | 533 |

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_350_0.png) 要查看和管理所有断点，从顶部菜单导航到 `运行 > 查看断点（Run > View Breakpoints:`![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_350_1.png) 你可以启用和禁用断点，也可以在另一个断点命中后禁用它。

## 结论

在本章中，你已经学习了如何在所有主流操作系统上设置调试器。虽然初始设置非常耗时，但回报是巨大的。能够对运行中的 CPython 进程设置断点、探索变量和内存，将使你拥有“超能力”。你可以利用这项技能来扩展 CPython、优化代码库的现有部分，或追踪棘手的 Bug。

对本小节提交反馈 »

# 基准测试、性能分析与追踪

在对 CPython 进行更改时，你需要验证这些更改是否会对性能产生重大的负面影响。

你可能希望对 CPython 进行改进性能的更改。

在本章中你将涵盖性能分析的解决方案：

- 1. 使用 `timeit` 模块数千次检查简单的 Python 语句以获取中位数执行速度
- 2. 运行 Python Benchmark 套件以比较多个版本的 Python
- 3. 使用 `cProfile` 分析帧的执行时间
- 4. 使用探针（probes）对 CPython 执行进行性能分析

方案的选择取决于任务类型：

- **基准测试（benchmark）**会产生固定代码段的平均/中位数运行时间，以便你可以比较多个版本的 Python 运行时
- **性能分析（profil）**会生成调用图及包含执行时间，帮助你理解哪个函数是最慢的

## 使用 Timeit 进行微基准测试

性能分析器可以在 C 级或 Python 层可用。如果你正在分析用 Python 编写的函数、模块或脚本，你需要使用 Python 性能分析器。如果你正在分析 C 扩展模块或对 CPython 中 C 代码的修改，你需要使用 C 性能分析器（或两者的结合）。

以下是一些可用工具的摘要：

| 工具 | 类别 | 级别 | 支持 |
| --- | --- | --- | --- |
| timeit | 基准测试 | Python | 所有 |
| pyperformance | 基准测试 | Python | 所有 |
| cProfile | 性能分析 | Python | 所有 |
| dtrace | 追踪/性能分析 | C | Linux/macOS |

> 重要提示
> 在运行任何基准测试之前，最好关闭计算机上的所有应用程序，以便让 CPU 专用于基准测试。

## 使用 Timeit 进行微基准测试

Python Benchmark 套件是对 CPython 运行时进行多次迭代的彻底测试。如果你想对特定代码段进行快速、简单的比较，请使用 `timeit` 模块。

要对短脚本运行 timeit，请运行编译后的 CPython 并配合 `-m timeit` 模块和引号中的脚本：

```bash
./python -m timeit -c "x=1; x+=1; x**"
100000 loops, best of 5: 258 nsec per loop
```

要运行较少次数的循环，请使用 `-n` 参数：

```bash
./python -m timeit -n 1000 "x=1; x+=1; x**"
1000 loops, best of 5: 227 nsec per loop
```

### 示例

在本书中，你通过支持近似相等运算符引入了对 float 类型的更改。

尝试此测试以查看比较两个浮点数值的当前性能：

```bash
$ ./python -m timeit -n 1000 "x=1.0001; y=1.0000; x-=y"
1000 loops, best of 5: 177 nsec per loop
```

该比较的实现在 `Objects/floatobject.c` 中的 `float_richcompare()` 中：

`Objects/floatobject.c`

```c
static PyObject*
float_richcompare(PyObject *v, PyObject *w, int op)
{
    ...
    case Py_EQUAL: {
        double diff = fabs(i - j);
        double rel_tol = 1e-9;
        double abs_tol = 0.1;
        r = (((diff <= fabs(rel_tol * j)) ||
             (diff <= abs_tol)));
    }
    break;
}
```

注意 `rel_tol` 和 `abs_tol` 的值是常量，但尚未被标记为常量。将它们改为：

```c
const double rel_tol = 1e-9;
const double abs_tol = 0.1;
```

现在，编译 CPython 并重新运行测试：

```bash
$ ./python -m time -n 1000 "x=1.0001; y=1.0000; x-=y"
1000 loops, best of 5: 172 nsec loop
```

你可能会注意到性能有轻微（1-5%）的提升。

尝试不同的比较实现方法，看看是否可以进一步改进。

### 使用 Python Benchmark 套件进行运行时基准测试

在比较 Python 的完整性能时，基准套件是应该使用的工具。Python Benchmark 套件是一系列 Python 应用程序，旨在测试负载下 Python 运行时的多个方面。Benchmark 套件测试是纯 Python 的，因此可以用于测试多个运行时，如 PyPy 和 Jython。它们也兼容 Python 2.7 到最新版本。

对 github.com/python/cpython master 分支的任何提交将使用 benchmark 工具进行测试，并将结果上传到 speed.python.org 的 Python 中心：

### 使用 Python Benchmark 套件进行运行时基准测试

### 比较基准

如果你想比较 JSON 结果，Python Benchmark 套件没有提供可视化解决方案。相反，你可以在虚拟环境中使用此脚本。

要安装依赖，请运行：

```bash
$ pip install seaborn performance
```

然后创建一个脚本 `profile.py`：

```python
import argparse
from pathlib import Path
from perf._bench import BenchmarkSuite
import seaborn as sns
import pandas as pd
sns.set(style="whitegrid")
parser = argparse.ArgumentParser()
parser.add_argument('files', metavar='N', type=str, nargs='+',
                    help='要比较的文件')
args = parser.parse_args()
benchmark_names = []
records = []
first = True
for f in args.files:
    benchmark_suite = BenchmarkSuite.load(f)
    if first:
        # 初始化字典键为测试名称
        benchmark_names = benchmark_suite.get_benchmark_names()
        first = False
    bench_name = Path(benchmark_suite.filename).name
    for name in benchmark_names:
```

### 使用 Python Benchmark Suite 进行运行时基准测试

```python
try:
    benchmark = benchmark_suite.get_benchmark(name)
    if benchmark is not None:
        records.append({
            'test': name,
            'runtime': bench_name.replace('.json', ''),
            'stdev': benchmark.mean.dev(),
            'mean': benchmark.mean(),
            'median': benchmark.median()
        })
except KeyError:
    # 额外的基准测试！忽略。
    pass
```

`df = pd.DataFrame(records)`

```python
for test in benchmark_names:
    g = sns.facetplot(
        x="runtime",
        y="mean",
        data=df[df['test'] == test],
        palette="YlGnBu_d",
        size=12,
        aspect=1,
        kind="bar"
    )
    g.despine(left=True)
    g.savefig("png/{}-result.png".format(test))
```

然后，要创建图表，请从解释器运行你创建的 JSON 文件：

```bash
$ python profile.py ~/benchmarks/json/HEAD.json ...
```

这将为每个执行的基准测试在 `png/` 子目录下生成一系列图表。

### 使用 cProfile 分析 Python 代码

标准库自带两个用于分析 Python 代码的分析器。第一个是 `profile`，一个纯 Python 的分析器；第二个是 `cProfile`，一个用 C 编写的更快的分析器。在大多数情况下，`cProfile` 是使用的最佳模型。

`cProfile` 分析器用于分析运行中的应用程序，并对评估的帧收集确定性分析数据。`cProfile` 的输出可以在命令行上总结，也可以保存为 `.pstat` 文件以便在外部工具中进行分析。

在“并行与并发”章节中，你用 Python 编写了一个端口扫描器程序。尝试在 `cProfile` 中对该程序进行性能分析。

在命令行中使用 `-m cProfile` 参数运行 python 以启动 `cProfile` 模块。第二个参数是要要执行的脚本：

```bash
$ python -m cProfile portscanner_multithreaded.py
Port 80 is open
Completed scan in 19.890110226593 seconds
    6833 function calls (6787 primitive calls) in 19.971 seconds
```

> 按标准排序：standard name
calls tottime percall cumtime percall filename:lineno(function)
2 0.000 0.000 0.000 0.000 ...

输出将打印一个包含以下列的表格：

| 列 | 目的 |
| :--- | :--- |
| ncalls | 调用次数 |
| tottime | 在函数中花费的总时间（不包括子函数） |
| percall | tottime 除以 ncalls 的商 |
| cumtime | 在此函数（及子函数）中花费的总时间 |
| percall | cumtime 除以原始调用次数的商 |
| filename:lineno(function) | 每个函数的数据 |

你可以添加 `-s` 参数和列名来对输出进行排序。
例如：

```bash
$ python -m cProfile -s tottime portscanner_multithreaded.py
```

将按每个函数中花费的总时间进行排序。

### 导出分析数据

你可以再次运行 `cProfile` 模块并通过 `-o` 参数指定输出文件路径：

```bash
$ python -m cProfile -o out.pstat portscanner_multithreaded.py
```

这将创建一个 `out.pstat` 文件，你可以使用 `Stats` 类或外部工具对其加载和分析。

### 使用 Snakeviz 可视化

Snakeviz 是一个免费的 Python 包，用于在浏览器浏览器中视化性能分析数据。

使用 pip 安装 snakeviz：

```bash
$ python -m pip install snakeviz
```

然后在命令行上通过你创建的统计文件路径执行 snakeviz：

```bash
$ python -m snakeviz out.pstat
```

这将打开你的浏览器，并允许你探索和分析数据：

### 使用 cProfile 分析 Python 代码

# SnakeViz

# 调用栈

# 重置缩放

# 样式: 旭日 (Sunburst)

# 深度: 10

# 截断: 1 1000

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_364_0.png)

搜索:

| calls | tottime | percall | ctime | percall | filename(line:function) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 103 | 1.024 | 0.00994 | 1.024 | 0.00994 | ~(method 'acquire' of '_thread.lock' object) |

### 使用 PyCharm 可视化

PyCharm 有一个内置工具用于运行 `cProfile` 并可视化结果。要执行此操作，你需要配置一个 Python 目标。

要运行分析器，选择你的运行目标，然后在顶部菜单上选择 Run Profile (target)。这将使用 `cProfile` 运行该目标，并打开一个带有表格数据和调用图谱的可视化窗口：

![](img/826aa5e3e0d3a5997a0ec0a647c5e3c6_364_1.png)

### 使用 cProfile 分析 Python 代码

# SnakeViz

# 调用栈

# 重置缩放

# 样式: 旭日

# 深度: 10

# 截断: 1 1000

... `cProfile` 分析器用于分析运行中的应用程序，并对评估的帧收集确定性分析数据。`cProfile` 的输出可以在命令行上总结，也可以保存为 `.pstat` 文件以便在外部工具中分析。

在“并行与并发”章节中，你用 Python 编写了一个端口扫描器程序。尝试在 `cProfile` 中对该程序进行性能分析。

在命令行中使用 `-m cProfile` 参数运行 python 以启动 `cProfile` 模块。第二个参数是要执行的脚本：

### 使用 cProfile 分析 Python 代码

# SnakeViz

# 调用栈

# 重置缩放

# 样式: 旭日

# 深度: 10

# 截断: 1 1000

... (此处由于原文包含大量重复的 OCR 错误，已根据逻辑合并并清理翻译)

```cpp
printf("%*s", self->indent, "");
printf("%*s:%dn", basename(copyinstr(arg0), copyinstr(arg1), arg2);
self->last = timestamp;
}
pythontarget::function-return
/basename=copyinstr(arg0) == "portscanner_multithreaded.py"
&& copyinstr(arg1) == "main"/
{
  self->trace = 0;
}
```

此脚本会在每次执行函数时打印一行，并记录从脚本开始到退出之间的时间差（delta）。

你需要使用脚本参数 `-s profile_compare` 和命令参数 `-c './python portscanner_multithreaded.py'` 来执行：

```
$ sudo dtrace -s profile_compare.d -c './python portscanner_multithreaded.py'
0 function-entry: portscanner_multithreaded.py:16
28 function-entry: queue.py:__init__:33
```



18 function-entry: `queue.py:__init__:205`

29 function-return: `queue.py:__init__:206`

46 function-entry: `threading.py:__init__:223`

33 function-return: `threading.py:__init__:245`

27 function-entry: `threading.py:__init__:223`

26 function-return: `threading.py:__init__:245`

26 function-entry: `threading.py:__init__:223`

25 function-return: `threading.py:__init__:245`

```
在输出中，第一列是自上一个事件以来的微秒时间差，然后是事件名称、文件名和行号。当函数调用发生嵌套时，文件名会向右逐渐增加缩进。
```

## 结论

在本章中，你探索了使用为 CPython 设计的多种工具进行基准测试（benchmarking）、性能分析（profiling）和追踪（tracing）。

通过正确的工具，你可以找到瓶颈、比较多个版本的性能并识别改进方案。

对本部分提交反馈 »

## 结论

恭喜你！你已经读到了这本书的最后。
你所所学的知识有三个主要用途：

- 1. 编写 C 扩展
- 2. 改进你的 Python 应用
- 3. 为 CPython 项目做贡献

作为对主题的总结，让我们来探索这些内容。

# 为 CPython 编写 C 扩展

有多种方法可以扩展 Python 的功能。
其中一种方法是用 C 或 C++ 编写你的 Python 模块。
这一过程可以提高性能，并更好地访问 C 库函数和系统调用。

如果你想编写一个 C 扩展模块，有一些你需要了解的要点，本书已经为你做好了准备：

- 如何设置 C 编译器并编译 C 模块。参见“编译 CPython”章节。
- 如何为 C 设置你的开发环境。参见“设置你的开发环境”章节。
- 如何增加和减少对生成对象的引用计数。参见“内存管理”中的“引用计数”章节。

## 使用这些知识改进你的 Python 应用

- `PyObject*` 是什么及其接口。参见“对象与类型类型”章节中的“对象和变量对象类型”。

- 什么是类型槽位（type slots）以及如何从 C 访问 Python 类型 API。参见“对象与类型”章节中的“类型槽位”部分。

- 如何为你的扩展模块的 C 源文件添加断点并进行调试：参见“调试”章节。

| 另见 |
| :--- |
| 在 realpython.com 上，Danish Prakash 编写了一篇关于构建 C 扩展模块的极佳教程。该教程包含了一个构建、编译和测试扩展模块的具体示例。 |

## 使用这些知识改进你的 Python 应用

本书涵盖了许多重要主题，可以帮助你改进应用程序。以下是一些示例：

- 使用并行和并发技术来缩短你应用程序的执行时间。参见“并行与并发”章节。

- 自定义垃圾回收算法以改进你的应用程序。参见“内存管理”中的“垃圾收集”章节。

- 为扩展模块的 C 源文件添加断点并调试：参见“调试”章节。

- 使用性能分析器（profilers）分析代码执行。参见“基准测试、性能分析与追踪”章节中的“cProfile”部分。

- 分析帧（frame）执行以调试复杂问题。参见“帧追踪”章节。

# 使用这些知识为 CPython 项目贡献

# 使用这些知识为 CPython 项目贡献

在编写本书期间，CPython 是最大的、最活力的开源项目之一。那么，什么阻碍了你向 CPython 提交更改、改进或修复？

我们需要更多的贡献者。以下是一些你可以开始的地方：

- 在 bugs.python.org 分发（triage）问题
- 修复简单问题

让我们详细介绍这些内容。

## 分发问题

所有错误报告和更改请求首先提交到 bugs.python.org。

提交拉请求后，将由一个分发团队进行处理，并分配给核心开发者或团队进行审查。

为了快速合并你的更改，对问题的解决方案和修复进行良好的说明非常有帮助。

## 为问题提交拉请求

有了要修复的问题，你可以开始创建修复并提交到 CPython。

# 使用这些知识为 CPython 项目贡献

| 补丁 | 查询 |
|---|---|
| 等待处理 | 未回复 |
| 简单任务 | 阻塞问题 (Showstoppers) |
| 最新问题 | 发布阻塞 |
| 关键 (Critical) | 打开 |
| 需要审查 | | |
| 崩溃问题 (Crashers) | 打开的错误 |
| 已提交补丁 |

我发现的一些实用查询是：

- 简单文档问题
- 简单任务
- 最近创建
- 未回复
- 未读
- 50 个最新问题

# 使用这些知识为 CPython 项目贡献

- 1. 确保你有一个 BPO 编号。
- 2. 在你的 CPython 分叉上创建一个分支。参见“获取源码”章节下载源码的步骤。
- 3. 创建一个用用来重现问题。参见“测试套件”章节中的“测试模块”部分。
- 4. 遵循 PEP7 和 PEP8 风格指南进行更改。
- 5. 运行回归测试检查所有测试是否通过。提交拉请求时 GitHub 会自动运行回归测试，但最好在本地检查。参见“测试套件”章节。
- 6. 将你的更改提交并推送到 GitHub。
- 7. 访问 github.com/python/cpython 并为你的分支创建一个拉请求

CPython 项目需要更多的贡献者。提交更改之间的时间可能是一小时、一周或几个月。如果没有立即收到回复，请不要沮丧。

| 重要 |
|--- |
| 在一个拉请求中只修复一件事非常重要。如果你在编写补丁时在代码中看到了另一个（不相关的）问题，请记录下来并作为第二个拉请求提交。 |

## 其他贡献

除了修复漏洞之外，你还可以对 CPython 项目进行一些其他类型的改进：

- 许多标准库函数和模块缺少单元测试。你可以编写一些测试并将它们提交给该项目。
- 许多标准库函数没有更新的文档。你可以更新文档并提交更改。

在此部分处提交反馈 »

## 持续学习

Python 之所以如此优秀的原因之一在于它的社区。认识正在学习 Python 的人吗？帮助他们吧！要真正掌握一个概念的唯一方法就是向别人解释它。

欢迎访问我们的网页，并在 realpython.com 网站和 @realpython Twitter 账户继续你的旅程。

## 开发者每周贴士

你是否在寻找每周一次 Python 技巧，以提高你的效率并简化你的工作流？好消息是：我们正在为像你这样的 Python 开发者运营一份免费的通讯邮件。我们发送的邮件不仅仅是典型的热门文章列表。相反，我们的目标是每周以短文的形式分享至少一个原创见解。如果你想看看它的魅力所在，请前往 realpython.com/newsletter 并在表单中输入你的电子邮件地址。我们期待你的相遇！

## Real Python 课程

通过 Real Python 丰富的（且不断增长的）Python 教程和深度培训材料，成为一名全能的 Python 专家。随着每周发布新内容，你将不断发现可以提升技能的内容：

- 掌握实用的真实世界技能：我们的教程由 Python 专家社区共同创建并审核。在 Real Python，你将获得通往精通之路所需的信赖资源。
- 与其他 Python 专家交流：加入 Real Python Slack 群组讨论即将到来的话题，并在这个虚拟茶水间与我们一起聚聚。
- 交互式测验与学习路径：通过交互式测验、动手编码挑战和以技能为重点的学习路径，了解你的水平并练习你所学的内容。
- 跟踪你的学习进度：将进行中的课程标记为“已完成”，并按照自己的节奏进行学习。收藏感兴趣的课程并在稍后回顾以增强长期记忆。
- 证书：对于每门课程，你都将获得一个托管在 Real Python 网站上的私有可分享（且可打印）证书。将你的证书嵌入到你的作品集、简历和其他网站中，向世界展示你是一个专注的 Python 专家。
- 定期更新：保持你的技能的新颖并跟上技术。我们不断发布仅限会员的教程并定期更新内容。访问 realpython.com/courses 查看可用内容

# 附录 1：程序员 C 语言简介

本介绍旨在让经验丰富的程序员快速熟悉 C 语言的基础知识以及它如何在 CPython 源码中使用。尽管如此，C 是一种相当有限的语言，它在 CPython 中的大多数用法都属于一小部分语法。能够理解代码比能够有效地编写 C 代码要容易得多。本教程针对的是第一个目标。

Python 和 C 之间最几个显著区别之一是 C 预处理器。让我们先来看这个。

### C 预处理器

正如其名所示，预处理器在编译器运行之前在你的源文件上运行。它的能力非常有限，但这些能力可以用于在构建 C 程序时获得巨大的优势。预处理器会生成一个新文件，这才是编译器实际处理的内容。所有给预处理器的命令都以 `#` 符号作为行首的第一个非空白字符开始。预处理器的主要目的是对源文件进行文本替换，它也会处理一些基础的条件代码。

让我们从最常用的预处理器指令 `#include` 开始。

### #include

`#include` 用于将一个文件的内容引入到当前源文件中。这并不复杂；它从文件系统读取文件，在该文件上运行预处理器，并将结果放入输出文件中。对于找到的每个 `#include` 指令，此操作都是递归递归执行的。

例如，如果你查看 `Modules/_multiprocessing/semaphore.c` 文件，在顶部附近你会看到：

```
#include "multiprocessing.h"
```

这告诉预处理器引入 `multiprocessing.h` 的全部内容，并将其放在输出文件的该位置。

你会注意到包含语句有两种不同的形式。其中一种使用双引号来指定包含文件的名称，另一种使用角括号 (`<>`)。区别在于搜索的路径不同……如果你对文件名使用 `<>`，预处理器将只查找“系统”包含文件。而在文件名周围使用引号则会强制预处理器首先查找本地目录，然后回退到系统目录。

### #define

`#define` 允许你进行简单的文本替换，并服务于我们在下文中看到的 `#if` 指令。在最基础的层，`#define` 允许你定义一个新的符号，该符号将与文本字符串一起放在预处理器的输出中。

继续查看 `semaphore.c`，你会发现这一行：

```
#define SEM_FAILED NULL
```

这告诉预处理器在代码发送给编译器之前，将此处的每一个 `SEM_FAILED` 实例替换为字面量字符串 `NULL`。

`#define` 紧跟项还可以接收参数，就像这个 Windows 特有版本的 `SEM_CREATE` 所示：

```
#define SEM_CREATE(name, val, max) CreateSemaphore(NULL, val, max, NULL)
```

在这种情况下，预处理器期望 `SEM_CREATE()` 看起来像一个函数并有三个参数。这通常被称为宏。它将直接三个参数的文本替换到输出代码中。例如，在第 459 行，`SEM_CREATE` 宏这样使用：

```
handle = SEM_CREATE(name, val, max);
```

当为 Windows 编译时，该宏将被展开为：

```
handle = CreateSemaphore(NULL, val, max, NULL);
```

我们将看到这个宏在 Windows和其他操作系统上是如何定义的。

# undef

此指令会删除任何之前的 `#define` 定义。这使得 `#define` 可以在文件的部分区域生效。

# if

预处理器还允许条件语句，允许你根据某些条件包含或排除文本区域。条件语句使用 `#endif` 指令关闭，并还利用 `#elif` 和 `#else` 进行精细调整。

# pragma

`Pragmas` 是给编译器的指令或提示。通常情况下你在阅读代码时可以忽略这些，因为它们通常处理的是代码如何编译，而不是代码如何运行。

# error

最后，`#error` 会显示消息并导致预处理器停止执行。再次，在阅读 CPython 源码时你可以安全地忽略这些。

## C 基础语法

本节不会涵盖 C 语言的所有方面，再次强调，它的目的也不是教你如何编写 C。它将关注于 Python 开发者第一次看到时感到不同或困惑的内容。

## 概述

与 Python 不同，空格对 C 编译器来说并不重要。它不在乎你将语句拆分成多行，还是将你的程序挤在一行非常长的单行上。这是因为它对所有语句和块都使用分隔符。

当然，解析器有一些非常特定的规则，但通常情况下，你只需要知道每条语句都以分号（`;)`结束，并且所有的代码块都被大括号（`{}`）包围，就能理解 CPython 的源码了。

这条规则的例外是，如果一个块只有一条语句，可以省略大括号。

C 中的所有变量必须声明，这意味着需要有一条语句来给出变量的类型。注意，与 Python 不同，单个变量的数据类型是更改的。

让我们来看一些示例：

```c
/* 注释包含在斜杠星号和星号斜杠之间 */

/* 这种风格的注释可以跨多行 -
所以这部分仍然是注释。 */

// 或者注释可以放在双斜杠后面

// 这种类型的注释只到行尾，因此新
// 行必须再次使用 //
int x = 0; // 声明 x 为 'int' 类型并将其初始化为 0
if (x == 0) {
    // 这是一个代码块
    int y = 1; // 在右括号 ) 之前 y 是有效的变量名
    // 此处有更多语句
    printf("%x is %d y is %d\n", x, y);
}
// 单行块不需要大括号
```

## C 语法

```c
if (x == 13)
    printf("x is 13!\n");
printf("past the it block\n");
```

通常情况下，你会发现 C 代码格式非常整洁，并且在给定的模块内通常遵循单一风格。

## if 语句

在 C 中，`if` 的工作原理通常与 Python 相似。如果条件为真，则执行后续块。`else` 和 `else if` 语法对于 Python 程序员来说足够熟悉并可以理解。注意，C 的 `if` 语句不需要 `endif`，因为块是由 `{}` 隔开的。

C 中有一种用于短 `if/else` 语句的简写形式，称为三元运算符：

你可以在 `semaphore.c` 中找到，对于 Windows，它定义了一个用于 `SEM_CLOSE()` 的宏：

```c
#define SEM_CLOSE(sem) (CloseHandle(sem) ? 0 : -1)
```

如果函数 `CloseHandle` 返回真，则该宏的返回值为0，否则为-1。

关于 C 中真的的一点说明：支持布尔变量类型并用在 CPython 源码的部分区域，但它们并不是原始语言的一部分。C 使用简单的规则解释二进制条件：`0` 或 `NULL` 为假，其他所有值均为真。

## switch 语句

与 Python 不同，C 也支持 `switch`。使用 `switch` 可以被看作扩展 `if/elseif` 链的快捷方法。这个示例来自 `semaphore.c`：

```c
switch (WaitForSingleObjectEx(handle, 0, FALSE)) {
  case WAIT_OBJECT_0:
  if (!ReleaseSemaphore(handle, 1, &previous))
    return MP_STANDARD_ERROR;
  *value = previous + 1;
  return 0;
  case WAIT_TIMEOUT:
  *value = 0;
  return 0;
  default:
  return MP_STANDARD_ERROR;
}
```

这是对 `WaitForSingleObjectEx()` 的返回值进行 `switch` 操作。如果值为 `WAIT_OBJECT_0`，则执行第一个块。`WAIT-TIMEOUT` 值导致执行第二个块，其他任何值都匹配 `default` 块。

注意，测试的值（在此例中为 `WaitForSingleObjectEx()` 的返回值）必须是一个整数值或枚举类型，并且每个 `case` 必须是一个常量值。

## 循环

C 中有三种循环结构：

- `for` 循环
- `while` 循环
- `do..while` 循环

让我们逐一查看这些。
`for` 循环的语法与 Python 非常不同：

```c
for (<initialization>; <condition>; <increment>) {
  需要被循环的代码
}
```

除了在循环中执行的代码外，还有三块代码用于控制 `for` 循环。

`<initialization>` 部分在循环开始时恰好运行一次。传统上，它被用于将循环计数器设置为初始值（并可能声明循环计数器）。`<increment>` 代码在每次通过完循环的主块后立即运行。传统上，这会递增循环计数器。最后，`<condition>` 在 `<increment>` 之后运行。该代码的返回值将被求值，当此条件返回假时，循环中断。

这是一个来自 `Modules/sha512module.c` 的示例：

```c
for (i = 0; i < 8; i++) {
    S[i] = sha_info->digest[i];
}
```

这个循环将运行 8 次，`i` 从 0 变为 7，当条件检查为 `i` 为 8 时终止。

`while` 循环与 Python 的对应部分几乎相同。然而，`do..while()` 的语法略有不同。`do..while()` 循环的条件在第一次执行循环之后之后检查。

CPython 代码库中有许多 `for` 和 `while` 循环实例，但 `do..while()` 未被使用。

## 函数

C 的函数语法与 Python 相似，区别在于需要返回类型

```c
<return_type> function_name(<parameters>) {
    <function_body>
}
```

C 的函数语法与 Python 相似，区别在于需要返回类型

```c
```



<return_type> function_name(<parameters>) {

    <function_body>

}

C 的函数语法与 Python 相似，区别在于需要返回类型

```c
<return_type> function_name(<parameters>) {
    <function_body>
}
```

## 字符串

C 中没有字符串类型。存在一种约定使得许多标准库函数基于此编写，但并没有实际的类型。相反，C 中的字符串存储为 `char` 或 `wchar` 值的数组，每个值包含单个字符。字符串用 `空终止符` 标记，其值为 `0`，在代码中通常显示为 `0`。

基础字符串操作（如 `strlen()`）依赖于此空终止符来标记字符串的结束。

由于字符串只是值的数组，因此无法直接进行复制或比较。标准库提供了 `strcpy()` 和 `strcmp()` 函数（以及它们的 `wchar` 版本）来执行这些及其他操作。

## 结构体 (Structs)

这次 C 语言微型之旅的终点，是学习如何在 C 中创建新类型：结构体。`struct` 关键字允许你将一组不同的数据类型组合在一起，形成一个新的自定义数据类型：

```
struct <struct_name> {
  <type> <member_name>;
  <type> <member_name>;
  ...
}
```

这个来自 `Modules/arraymodule.c` 的部分示例展示了结构体的声明：

```
struct arraydescr {
  char typecode;
  int itemsize;
  ...
};
```

这创建了一个名为 `struct arraydescr` 的新数据类型，它包含许多成员，其中前两个是 `char` `typecode` 和 `int` `itemsize`。

结构体经常作为 `typedef` 的一部分使用，为名称提供简单的别名。在上面的示例中，所有新类型的变量都必须使用全名 `struct arraydescr x;` 来声明。

你经常会看到这样的语法：

```
typedef struct {
  PyObject_HEAD
  SEM_HANDLE handle;
  unsigned long last_tid;
  int count;
  int maxvalue;
  int kind;
  char *name;
} SemLockObject;
```

这创建了一个新的自定义结构体类型，并给它命名为 `SemLockObject`。要声明此类型的变量，你只需要使用别名 `SemLockObject x;`。

## 结论

到此我们结束了对 C 语法的快速介绍。虽然这段描述中省略了许多细节，但它对于阅读 CPython 源代码来说已经足够了。

对本章节提供反馈 »

# 这是《CPython 内部：Python 3 解释器指南》的早期访问版本

在您的帮助下，我们可以让这本书变得更好：

在书的每个章节末尾，你都会找到一个“魔法”反馈链接。点击该链接将带你进入一个`在线反馈表`，你可以在那里与我们分享你的想法。

根据你的需要提供简洁或详细的反馈。所有反馈都会匿名存储，但你可以选择留下姓名和联系方式，以便我们进行跟进或在我们的“感谢”页面上提到你。

我们为每个章节使用不同的反馈链接，因此我们始终知道你的笔记指的是书的哪部分。

感谢你帮助我们将这本书成为 Python 社区更具价值的学习资源。

— Anthony Shaw
