
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
