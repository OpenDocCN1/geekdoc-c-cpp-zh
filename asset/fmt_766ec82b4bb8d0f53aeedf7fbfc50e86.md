
本章将涵盖 Zephyr 应用环境的设置。Zephyr 已集成到 Nordic Semiconductor 的应用平台 `nRF Connect SDK` 中。`nRF Connect SDK` 包含了 Zephyr 框架，以及 Nordic Semiconductor 为其系列处理器开发的额外库和示例。`nRF Connect SDK` 可用于开发针对 nRF 以外处理器的应用程序。

Zephyr 有一个名为 Zephyr SDK 的 SDK，它包含 Zephyr 支持的处理器架构的工具链，还包含了主机工具，例如自定义的 QEMU 和 OpenOCD。

Zephyr RTOS 应用开发可以使用带有插件的 IDE。这些包括 Eclipse 和 Microsoft VS Code。VS Code 有 Zephyr SDK 和 nRF Connect 插件，且 VS Code 被 Zephyr 开发者广泛使用。

也完全可以遵循“老派”做法，使用 vim 和 emacs 等文本编辑器开发代码，然后使用工具进行构建和烧录应用程序。在这里，我们将探索设置 VS Code 和传统的命令行开发环境。

## 参考文献

- 1. 维基百科条目 `https://en.wikipedia.org/wiki/Hardware_Protocol` own 2. Zephyr 关于 HAL（硬件抽象层）的文档 `https://docs.zephyrproject.org/latest/services/portability/index.html`
- 3. `https://community.arm.com/arm-blog/architectures-and-processors/posts/beginner-guide-on-interrupt-latency`

其第 15 版对于想要深入学习 CMake 的人来说是一个很好的入门点 [1]。Ninja 和 Make 之间的类比关系是“ninja 之于汇编语言，就如 make 之于高级程序语言语言”。Ninja 的开发是为了在构建大型复杂项目时提供比 Make 更好的工具。其意图是让开发者使用如 CMake 等工具来生成 ninja 构建脚本，而不是手动编写脚本。要深入研究 Ninja，有必要查阅 ninja 的官方文档 [2]。

对于大型复杂项目，相应的 CMake 文件可能会变得非常复杂，因为它们通常包含了来自项目各个部分的 CMake 组件。Zephyr 项目就是如此。应用目录下的 CMake 文件通常很小。驱动构建的实际 CMake 文件是通过“拉取”来自 Zephyr 源码其他部分的 CMake 文件来构建的。CMake 提供了产生详细输出的命令行选项（在 Zephyr 应用构建的情况下，会有大量的输出），可以通过命令行选项 `--trace`、`--trace-expand` 和 `--trace-source=some_cmake_source` 来调用。在尝试理解构建 Zephyr 应用时的 CMake 用法时，一种方法是学习如何“阅读并理解”CMake 文件，然后逐个探索各种 Zephyr CMake 文件。

## 在 Microsoft Windows 上设置 Zephyr SDK CLI 开发环境

在最新版本的 Windows 10 或 Windows 11 上安装 Zephyr 的基本设置步骤在 Zephyr 项目的入门指南中有描述。Zephyr 项目的依赖包括 CMake（版本 3.20 或更高）、Python（版本 3.8 或更高）以及 Devicree 编译器（版本 1.4.6 或更高）。使用 Windows 的 Chocolatey 包管理工具（`https://docs.zephyrproject.org/latest/develop/getting_started/index.html`）可以极大简化这些依赖的安装。

Chocolatey 网站提供了易于遵循的 Chocolatey 安装说明（`https://chocolatey.org/install`）。然后可以使用 Chocolatey 可执行代码，在 `cmd.exe` 终端窗口中以管理员权限运行以下命令来安装所需的包：

```
choco install cmake --installargs 'ADD_CMAKE_TO_PATH=System'
choco install ninja grep python dt-msys2 wget unzip
```

随后，可以在 `cmd.exe` 窗口中以普通用户身份运行并安装 Zephyr SDK 及相关工具。如果在运行着多个版本 Python 的工作站上安装，并且用于开发其他项目，那么使用自定义 Python 虚拟环境来处理构建 Zephyr 应用所需的各种 Python 包是一个好主意。这可以在 `cmd.exe` 或 PowerShell 中完成。

在 Python 虚拟环境中安装需要创建和激活 Python 虚拟环境。可以通过进入目标目录并按照如下方式创建虚拟环境 `venv`：

```
cd %HOMEPATH%
python -m venv zephyrproject\.venv
```

激活虚拟环境的命令在 `cmd.exe` 中为 `zephyrproject\.venv\Scripts\activate.bat`，在 powershell 中为 `zephyrproject\.venv\Scripts\Activate.ps1`。

一旦激活了 venv，shell 提示符将以前缀 `(.venv)`。可以随时通过运行 `deactivate` 命令退出虚拟环境。

### 第三章 Zephyr RTOS 应用开发环境与 Zephyr 应用构建原理

虚拟环境在退出后或在启动新的 shell 窗口工作时需要重新激活。

设置好 Python 环境后，下一步是安装 `west` 工具。`west` 是一个 Python 包，使用 `pip` 通过以下命令安装：

```
pip install west
```

安装完成后，可以使用 `west` 获取 zephyr 源码，如下：

```
west init zephyrproject
cd zephyrproject
west update
```

下一步是将 Zephyr CMake 包导出到 CMake 用户包注册表中心。这是为了让 CMake 可以下载构建 Zephyr 应用所需的样板代码。

```
west zephyr-export
```

CMake 是一个强大且复杂的工具，学习曲线非常陡峭。幸运的是，在开始进行 Zephyr 应用编程并使用 `west` 以及 Zephyr 源码附带的各种示例时，仅需具备基础 CMake 就能取得很大进展。

Zephyr 本身有许多 Python 包依赖，列在文本文件 `requirements.txt` 中。可以通过运行以下命令安装必要的包：

```
pip install -r %HOMEPATH\zephyrproject\zephyr\scripts\nrequirements.txt
```

安装过程的最后一步是安装 Zephyr 软件开发包 `SDK` 本体。SDK 包含了 Zephyr 支持的种架构的工具链。每个工具链都包含编译器、汇编器、链接器以及构建 Zephyr 应用所需的其他程序。SDK 还提供了主机工具，例如自定义的 QEMU（快速仿真器）和 OpenOCD（开放芯片上调试器）版本以及软件刷录工具，可用于仿真、刷录和调试 Zephyr 应用。

为了测试安装，请构建一个基础示例，例如针对特定板的 LED 闪烁示例。构建命令为：

```
cd %HOMEPATH%\zephyrproject\zephyr
west build -p -b <your-board-name> samples\basic\blinky
```

其中 `<your-board-name>` 是特定板的名称。可以使用 `west boards` 命令获取 Zephyr 支持的所有板列表。在构建命令中，`-p` 选项强制进行 pristine（全新的）构建。`-p auto` 选项会让 west 使用启发式方法判断是否需要全新构建。

构建成功后，可以使用以下命令将执行文件刷录到板：

```
west flash
```

对于某些板，为了能够刷录，可能需要安装额外的主机工具。

## 入门板与开发板的选择

入门板的选择取决于长期兴趣和目标。如果你对 BLE（低功耗蓝牙）应用感兴趣，那么基于 Nordic Semiconductor `nRF52` 或 `nRF53` 处理器的板（如 `nRF52840 DK` 板或 `nRF5340` 板）值得考虑。这些是相对廉价且支持良好的板。其他更便宜的 `nRF52840` 板包括 Adafruit `nRF52840 ItsyBits` 和 SparkFun Pro `nRF5240 Mini` 蓝牙开发板。

并非主要面向 BLE 的低成本 ARM Cortex M 处理器板是各种 STM32 Nucleo 板。这些板具有 Arduino 兼容引脚且支持良好。STM 还制造了各种 Arduino 引脚格式的扩展板，提供了各种额外功能，例如直流电机和步进电机的电机驱动控制板，以及一个带有 MEMS（微机电系统）和环境传感器的板。STM Nucleo 板是价格适中的、适合学习和原型设计的板。针对不同的 STM32 处理器都有 Nucleo 板。例如，`Nucleo-F401RE` 如图 3-1 所示。

# 第 3 章 ZEPHYR RTOS 应用开发环境与 ZEPHYR 应用构建原理

![](img/d625a3dc80e999570aa2c88dcc398b17_91_0.png)

图 3-1. Nucleo-F401RE

对于涉及各种无线网络协议的物联网（IoT）原型原型，STM 生产了诸如用于 IoT 节点的 `B-L475E-IOT01A Discovery` 开发板，该板包含了蓝牙 V4.1、符合 802.11 b/g/n 标准的 Wi-Fi 以及动态 NFC 标签模块，其如图 3-2 所示。

![](img/d625a3dc80e999570aa2c88dcc398b17_92_0.png)

图 3-2.STM-B475E-IOT01A Discovery 开发板

涉及到低成本开发和原型设计时，Feather 板格式（羽毛板格式）是值得了解的。Zephyr RTOS 支持的 Feather 板包括 Adafruit Feather M0 Basic Proto、Adafruit Feather M0 LoRa、Adafruit Feather `nRF52840 Express` 以及 Adafruit Feather STM32F405 板。图 3-3 显示了 STM32F405 板。

![](img/d625a3dc80e999570aa2c88dcc398b17_93_0.png)

**图 3-3.** Adafruit Feather STM32F405 开发板

一种与符合 Feather 板格式的板兼容的实用原型技术是 feather click shield（扩展板），它使得各种 Micro “click 板”连接到“feather”板上成为可能。图 3-4 和 3-5 显示了裸板的 feather click shield 和已扩展的 feather click shield。Micro 开发了广泛的“click 板”，这些板子的接口可以在各种嵌入式系统开发包中找到。

![](img/d625a3dc80e999570aa2c88dcc398b17_93_1.png)

**图 3-4.** Micro feather click shield

最后，在介绍 Zephyr SDK 支持的嵌入式处理器时，如果没有基于 RISC-V 处理器的系统是不完整的。RISC-V 的重要性在于，与设计基于 ARM 的系统相比，RISC-V 核心设计和指令集是完全开源的。RISC-V 还由 Linux 基金管理。存在 32 位和 64 位 RISC-V 处理器架构。可用于 Zephyr RTOS 的 32 位 RISC-V 板包括 SiFive 的 HiFive1 Rev B 开发板和 SparkFun 的 RED-V SIFIVE RISC-V REDBOARD，如图 3-6 所示。

乐鑫科技（Espressif）还开发了 ESP32 C3 处理器，其具有 RISC-V 核心处理器。此外， Nordic 半导体（Nordic Semiconductor）开始推出包含 ARM Cortex M33 和 RISC-V 处理器核心的多处理器芯片系列——`nRF54H20`。

![](img/d625a3dc80e999570aa2c88dcc398b17_95_0.png)

图 3-6. SparkFun's RED-V SIFIVE RISC-V REDBOARD

## 使用基于 Microsoft VS Code 的 IDE 设置 nRF Connect SDK 开发环境

Nordic 半导体的 `nRF Connect SDK` 基于 Zephyr RTOS SDK。它本质上增加了许多专门针对 Nordic 半导体处理器的额外库和示例。该 SDK 包含了 Zephyr RTOS SDK，并可用于开发针对 Zephyr RTOS SDK 支持的其他板的 Zephyr RTOS 应用。Nordic 半导体还开发了一个名为 `nRF Connect for Desktop` 的桌面应用程序，它极大简化了开发 Zephyr RTOS 应用的 IDE 安装和设置。它最初为 Microsoft Windows 开发，现在也有 Linux 和 Mac OS X 的变体。

可以从 nordicsemi 网站下载 `nRF Connect for Desktop`（见图 3-7）：`www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-desktop/Download#infotabs`。

![](img/d625a3dc80e999570aa2c88dcc398b17_96_0.png)

图 3-7. nRF Connect for Desktop 下载

`nRF Connect for Desktop` 框架是一个跨平台工具，通过提供用于监控、测量、优化和编程应用程序的 App，有助于在 nRF 设备上开发应用程序。

`nRF Connect for Desktop` 框架是一个跨平台工具，通过提供用于监控、测量、优化和编程应用程序的 App，有助于在 nRF 设备上开发应用程序。

`nRF Connect for Desktop` 框架是一个跨平台工具，通过提供用于监控、测量、优化和编程应用程序的 App，有助于在 nRF 设备上开发应用程序。

`nRF Connect for Desktop` 框架是一个跨平台工具，通过提供用于监控、测量、优化和编程应用程序的 App，有助于在 nRF 设备上开发应用程序。

# 第 3 章 ZEPHYR RTOS 应用开发环境

## ZEPHYR 应用构建原理

按照前面的方法获取 `nRF Connect SDK` 后，现在有两种可能的应用程序开发方式：一种是在 Visual Studio Code `VS Code` 中使用 `nRF Connect for VS Code` 扩展进行开发，另一种是使用命令行开发。

要使用 VS Code IDE 进行开发，请点击“Open VS Code”（打开 VS Code）按钮。如果是首次安装，将弹出的通知对话框，列出必须安装的缺失扩展。该列表将包含来自 `nRF Connect for Visual Studio Code` 扩展包（pack）的扩展。一旦安装了这些扩展，点击“Open VS Code”按钮即可启动 VS Code。`nRF Connect for VS Code` 扩展与 VS Code 共同构成了一个完整的 IDE，可以在其中为 `nRF91`、`nRF53` 和 `nRF52` 系列 Nordic 设备开发应用程序。它包含指向编译器的接口、感知 RTOS 的调试器接口，以及指向 `nRF Connect SDK` 的接口和串口终端。

## 在 VS Code 中工作

使用 `nRF Connect for Desktop` 工具链管理器安装 `nRF Connect SDK` 时，同时也会安装 `nRF Connect for VS Code` 扩展，这使得在 VS Code 中开发运行在 nRF 设备上的 Zephyr 项目成为可能。接几页基于 `nRF Connect SDK` 文档 [3] 和 Linux Foundation 博客文章 [4]，提供了在 VS Code 中使用 `nRF Connect SDK` 的入门概述。详细信息请参阅 `nRF Connect SDK` 文档。

要在 VS Code 中创建 `nRF Connect SDK` 项目，第一步是点击活动栏（Activity Bar）中的 `nRF Connect` 图标（见图 3-10）。

![](img/d625a3dc80e999570aa2c88dcc398b17_101_0.png)

图 3-10 活动视图中的 nRF Connect 图标

`nRF Connect SDK Extension UI` VS Code 用户界面包含许多组件，初看起来可能看起来有些杂乱。然而，一旦掌握了它们的基本结构，大部分的“表面复杂性”就会消失。GUI 的四个主要部分是扩展视图（Extension Views）、编辑器（Editor）、面板（Panel）和状态栏（Status Bar）。开发过程中使用的绝大多数工具可以在侧边栏的 `nRF Connect` 侧边栏视图（Sidebar Views）中找到（见图 3-11）。

![](img/d625a3dc80e999570aa2c88dcc398b17_102_0.png)

图 3-11 nRF Connect for VS Code 概

图 3-12 和 3-13 显示了左侧和右侧的放大视图。

![](img/d625a3dc80e999570aa2c88dcc398b17_103_0.png)

图 3-12 活动栏和 nRF Connect 侧边栏视图

![](img/d625a3dc80e999570aa2c88dcc398b17_104_0.png)

图 3-13 编辑器窗口、面板视图和状态栏

![](img/d625a3dc80e999570aa2c88dcc398b17_105_0.png)
