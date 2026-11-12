

本页故意留空

## 第 2 章

## 入门

我们希望第 1 章已经让你迫不及待地开始学习 CUDA C 了。由于本书旨在通过一系列编码示例来教你这门语言，你需要一个正常运行的开发环境。当然，你可以站在场边观看，但我们认为，如果你尽快跳进去，亲手编写一些 CUDA C 代码并积累实践经验，你会玩得更开心，并且保持兴趣更久。本着这个目的，本章将带你了解入门所需的一些硬件和软件组件。好消息是，你可以免费获得所有需要的软件，这样你就有更多的钱去做任何让你开心的事情了。

## 2.1 本章目标

在本章学习过程中，你将完成以下任务：

- 你将下载本书所需的所有软件组件。
- 你将搭建一个可以编译 CUDA C 代码的环境。

## 2.2 开发环境

在踏上这段旅程之前，你需要搭建一个可以使用 CUDA C 进行开发的环境。使用 CUDA C 开发代码的先决条件如下：

- 支持 CUDA 的图形处理器
- NVIDIA 设备驱动程序
- CUDA 开发工具包
- 标准 C 编译器

为了使本章尽可能轻松，我们现在将逐一介绍这些先决条件。

### 2.2.1 支持 CUDA 的图形处理器

幸运的是，你应该很容易找到一款基于 CUDA 架构构建的图形处理器，因为自 2006 年 GeForce 8800 GTX 发布以来，每一款 NVIDIA GPU 都支持 CUDA。由于 NVIDIA 定期发布基于 CUDA 架构的新 GPU，下面的列表无疑只能是支持 CUDA 的 GPU 的部分列表。尽管如此，这些 GPU 都具备 CUDA 功能。

要查看完整列表，你应该查阅 NVIDIA 网站 www.nvidia.com/cuda，尽管可以安全地假设，所有近期 GPU（2007 年及以后的 GPU）且显存超过 256MB 的都可以用于开发和运行使用 CUDA C 编写的代码。

### 表 2.1 支持 CUDA 的 GPU

| GeForce GTX 480 | GeForce 8300 mGPU | Quadro FX 5600 |
| --- | --- | --- |
| GeForce GTX 470 | GeForce 8200 mGPU | Quadro FX 4800 |
| GeForce GTX 295 | GeForce 8100 mGPU | Quadro FX 4800 for Mac |
| GeForce GTX 285 | Tesla S2090 | Quadro FX 4700 X2 |
| GeForce GTX 285 for Mac | Tesla M2090 | Quadro FX 4600 |
| GeForce GTX 280 | Tesla S2070 | Quadro FX 3800 |
| GeForce GTX 275 | Tesla M2070 | Quadro FX 3700 |
| GeForce GTX 260 | Tesla C2070 | Quadro FX 1800 |
| GeForce GTS 250 | Tesla S2050 | Quadro FX 1700 |
| GeForce GT 220 | Tesla M2050 | Quadro FX 580 |
| GeForce G210 | Tesla C2050 | Quadro FX 570 |
| GeForce GTS 150 | Tesla S1070 | Quadro FX 470 |
| GeForce GT 130 | Tesla C1060 | Quadro FX 380 |
| GeForce GT 120 | Tesla S870 | Quadro FX 370 |
| GeForce G100 | Tesla C870 | Quadro FX 370 Low Profile |
| GeForce 9800 GX2 | Tesla D870 | Quadro CX |
| GeForce 9800 GTX+ | QUADRO MOBILE PRODUCTS | Quadro NVS 450 |
| GeForce 9800 GTX | Quadro FX 3700M | Quadro NVS 420 |
| GeForce 9800 GT | Quadro FX 3600M | Quadro NVS 295 |
| GeForce 9600 GSO | Quadro FX 2700M | Quadro NVS 290 |
| GeForce 9600 GT | Quadro FX 1700M | Quadro Plex 2100 D4 |
| GeForce 9500 GT | Quadro FX 1600M | Quadro Plex 2200 D2 |
| GeForce 9400GT | Quadro FX 770M | Quadro Plex 2100 S4 |
| GeForce 8800 Ultra | Quadro FX 570M | Quadro Plex 1000 Model IV |
| GeForce 8800 GTX | Quadro FX 370M | GEFORCE MOBILE PRODUCTS |
| GeForce 8800 GTS | Quadro FX 360M | GeForce GTX 280M |
| GeForce 8800 GT | Quadro NVS 320M | GeForce GTX 260M |
| GeForce 8600 GTS | Quadro NVS 160M | GeForce GTS 260M |
| GeForce 8600 GT | Quadro NVS 150M | GeForce GTS 250M |
| GeForce 8500 GT | Quadro NVS 140M | GeForce GTS 160M |
| GeForce 8400 GS | Quadro NVS 135M | GeForce GT 150M |
| GeForce 9400 mGPU | Quadro NVS 130M | GeForce GT 240M |
| GeForce 9300 mGPU | Quadro NVS 135M | GeForce GT 230M |
| GeForce GT 130M | GeForce 9700M GTS | GeForce 9200M GS |
| GeForce G210M | GeForce 9700M GT | GeForce 9100M G |
| GeForce G110M | GeForce 9650M GS | GeForce 8800M GTS |
| GeForce G105M | GeForce 9600M GT | GeForce 8700M GT |
| GeForce G102M | GeForce 9600M GS | GeForce 8600M GT |
| GeForce 9800M GTX | GeForce 9500M GS | GeForce 8600M GS |
| GeForce 9800M GT | GeForce 9500M G | GeForce 8400M GT |
| GeForce 9800M GTS | GeForce 9300M GS | GeForce 8400M GS |
| GeForce 9800M GS | GeForce 9300M G | |

### 2.2.2 NVIDIA 设备驱动程序

NVIDIA 提供系统软件，允许你的程序与支持 CUDA 的硬件进行通信。如果你已正确安装 NVIDIA GPU，那么你的机器上很可能已经安装了此软件。确保你拥有最新驱动程序绝无坏处，因此我们建议你访问 www.nvidia.com/cuda 并单击“Download Drivers”链接。选择与你计划用于开发的显卡和操作系统相匹配的选项。按照你所选平台的安装说明操作后，你的系统将更新至最新的 NVIDIA 系统软件。

### 2.2.3 CUDA 开发工具包

如果你拥有支持 CUDA 的 GPU 和 NVIDIA 设备驱动程序，那么你就可以运行已编译的 CUDA C 代码了。这意味着你可以下载基于 CUDA 的应用程序，它们将能够在你的图形处理器上成功执行代码。然而，我们假设你想做的不仅仅是运行代码，否则，这本书就没有必要了。如果你想使用 CUDA C 为 NVIDIA GPU 开发代码，你将需要额外的软件。但如前所述，这些软件都不会花费你一分钱。

你将在下一章了解这些细节，但由于你的 CUDA C 应用程序将在两个不同的处理器上进行计算，因此你将需要两个编译器。一个编译器将为你的 GPU 编译代码，另一个将为你的 CPU 编译代码。NVIDIA 为你的 GPU 代码提供编译器。与 NVIDIA 设备驱动程序一样，你可以在 http://developer.nvidia.com/object/gpucomputing.html 下载 CUDA Toolkit。单击 CUDA Toolkit 链接以到达图 2.1 所示的下载页面。

![](img/d5750f02645080d2a91292047fbe0f98_37_0.png)

### 图 2.1 CUDA 下载页面

你将再次被要求从 Windows XP、Windows Vista、Windows 7、Linux 和 Mac OS 的 32 位和 64 位版本中选择你的平台。从可用的下载中，你需要下载 CUDA Toolkit 以构建本书中包含的代码示例。此外，我们鼓励你（但不是必须的）下载 GPU Computing SDK 代码示例，其中包含几十个有用的示例程序。GPU Computing SDK 代码示例不会在本书中介绍，但它们很好地补充了我们打算涵盖的材料，与学习任何编程风格一样，示例越多越好。你还应该注意，尽管本书中几乎所有代码都可以在 Linux、Windows 和 Mac OS 平台上运行，但我们将应用程序的目标定为 Linux 和 Windows。如果你使用 Mac OS X，你将冒着风险使用不受支持的代码示例。

### 2.2.4 标准 C 编译器

如前所述，你需要一个用于 GPU 代码的编译器和一个用于 CPU 代码的编译器。如果你按照上一节的建议下载并安装了 CUDA Toolkit，那么你已经拥有了用于 GPU 代码的编译器。用于 CPU 代码的编译器是我们 CUDA 检查清单上仅剩的组件，所以让我们解决这个问题，以便进入有趣的部分。

### Windows

在 Microsoft Windows 平台上，包括 Windows XP、Windows Vista、Windows Server 2008 和 Windows 7，我们建议使用 Microsoft Visual Studio C 编译器。NVIDIA 目前支持 Visual Studio 2005 和 Visual Studio 2008 产品系列。随着 Microsoft 发布新版本，NVIDIA 可能会为较新版本的 Visual Studio 添加支持，同时放弃对旧版本的支持。许多 C 和 C++ 开发者的机器上已经安装了 Visual Studio 2005 或 Visual Studio 2008，所以如果这适用于你，你可以安全地跳过本小节。

如果你无法获得受支持版本的 Visual Studio 并且不打算购买一份，Microsoft 确实在其网站上提供 Visual Studio 2008 Express 版的免费下载。虽然通常不适合商业软件开发，但 Visual Studio Express 版是开始在 Windows 平台上开发 CUDA C 的绝佳方式，无需投资软件许可证。因此，如果你需要 Visual Studio 2008，请访问 www.microsoft.com/visualstudio！

