

编程器可同时为 AVR 电路供电并对其编程，电力来源于主机计算机的 USB 端口。最后，Atmel-ICE 插入主机计算机的 USB 端口后，即可与 Microchip Studio 一起使用。爱好者编程器最初需要在 Microchip Studio 中进行一些额外设置，本附录将对此进行说明。

### A.1.2 Programming Interfaces

大多数爱好者编程器支持 ISP/SPI 编程接口，但通常不支持较新 AVR 上的许多其他接口。ISP/SPI 编程涵盖第 1 章第 1.3 节表 1.1 中显示的所有 ATtiny 微控制器。支持的接口取决于这些编程器中的固件以及运行在主机计算机上的编程软件。固件和编程软件的更新可能已提供，或将来可用，这些更新允许通过其他接口进行编程。本附录涵盖三种广泛可用的爱好者编程器。可能有其他支持其他 AVR 编程接口的编程器可用。撰写本文时，没有一种是广泛可用的。

### A.1.3 Using Hobby USB Programmers with this Book

本书旨在使用带有 ISP/SPI 接口并提供 DIP 封装的 ATtiny 微控制器。这样一来，读者可以构建本书中的所有电路，并使用廉价的爱好者编程器加载软件。希望使用 TPI 接口的 ATtiny4/5/9/10 系列进行实验的读者，可能需要获取支持 TPI 的额外爱好者编程器，或使用 Atmel-ICE。ATtiny4/5/9/10 微控制器是表面贴装器件，需要焊接到扩展板上才能用于面包板电路。使用 UPDI 接口的现代 ATtiny 微控制器也全是表面贴装器件，且未在本书中涵盖，因此不需要 UPDI 编程器。

## A.2 Overview of External Programmer Setup

以下列表包含在 Microchip Studio 中设置外部 USB 爱好者编程器所需的所有基本步骤。每个步骤的设置详情可在后续章节中找到。

- 1) 为编程器安装驱动程序。
- 2) 下载编程软件（名为 avrdude 的程序）。
- 3) 构建 AVR 电路并连接编程器以进行测试。
- 4) 确定必须传递给 avrdude 的参数，以适用于特定的编程器和 AVR 微控制器。
- 5) 打开 Microchip Studio 并设置外部工具及其按钮。
- 6) 通过编程目标 AVR 微控制器来测试设置。
- 7) 修复任何编程问题。

## A.3 External Programmer Setup

以下小节中的步骤涵盖了上一节列表中所有步骤，用于在 Microchip Studio 中设置 USB 爱好者编程器。

### A.3.1 Install a Driver

必须为每个编程器安装驱动程序，以便其在 Windows 计算机上工作。Arduino Uno 不需要安装驱动程序，但需要将 ArduinoISP 草图加载到其中，以将其转换为 ISP 编程器。请按照以下适用于您使用的编程器（无论是 USBasp、USBtinyISP 还是 Arduino Uno）的正确标题下的驱动程序安装过程进行操作。

#### A.3.1.1 USBasp Driver

有关 USBasp 的固件、驱动程序和其他信息的链接，可在该设备设计者 Thomas Fischl 的网页 www.fischl.de/usbasp/ 上找到。

名为 Zadig 的驱动程序安装工具用于在 Windows 计算机上为 USBasp 安装驱动程序。访问 zadig.akeo.ie，通过单击网页“下载”标题下的链接下载 Zadig 可执行文件。撰写本文时，Zadig 的最新版本为 2.5 版，文件名为 zadig-2.5.exe。

将 USBasp 插入 Windows 计算机上的空闲 USB 端口。Windows 会尝试为 USBasp 安装驱动程序，但会失败，即使它报告设备已就绪。要验证 Windows 已找到 USBasp 但自动驱动程序安装失败，请右键单击 Windows 开始按钮，然后在弹出的菜单中选择“设备管理器”。USBasp 应该在设备管理器窗口的“其他设备”下可见。它上面会有一个三角形图标，表示未安装驱动程序，如图 A.2 所示。

![](img/83ef13a6c66cc7882b2f357e97f451dc_336_0.png)

图 A.2: USBasp 驱动程序安装失败

使用 Windows 资源管理器导航到 Zadig 可执行程序并双击它来运行。Windows 会弹出一个对话框，询问“是否允许此应用对您的设备进行更改？”在该对话框中单击“是”。在 Zadig 更新策略对话框中，您可以选择单击“否”以阻止 Zadig 在线检查应用程序更新，因为如果已下载最新版本的软件，则无需此操作。当 Zadig 应用程序窗口打开时，它应该自动选中 USBasp，如图 A.3 所示（假设 USBasp 已插入计算机的 USB 端口）。单击包含 WinUSB 的框旁边的向下箭头，如图 A.3 所示，以便选择 libusb-win32，如图 A.4 所示。

单击“安装驱动程序”按钮以安装所选驱动程序。Zadig 现在会弹出一个对话框，显示驱动程序正在安装。驱动程序安装完成后，会弹出一个对话框显示驱动程序已成功安装。单击该对话框中的“关闭”按钮。关闭 Zadig 应用程序窗口。

![](img/83ef13a6c66cc7882b2f357e97f451dc_337_0.png)

图 A.3: 首次打开时的 Zadig 应用程序窗口

![](img/83ef13a6c66cc7882b2f357e97f451dc_337_1.png)

图 A.4: Zadig 中选定的 USBasp 正确驱动程序

经发现，在已安装 Microchip Studio 的计算机上，安装驱动程序后，USBasp 会出现在设备管理器对话框的“Atmel USB Devices”或“Microchip Tools”下。在未安装 Microchip Studio 的计算机上，USBasp 会出现在设备管理器对话框的“libusb-win32 devices”下。请注意，USBasp 必须插入 USB 端口才能在设备管理器对话框中看到。一旦拔下，它就会从设备管理器中消失。在将 USBasp 连接到电路之前，请先将其从 USB 端口拔下。

此时，如果 USBasp 可以在设备管理器中找到且没有任何警告图标，则表示驱动程序已成功安装，USBasp 已准备就绪。请转到 A.3.2 节以下载并安装 avrdude 编程软件。

#### A.3.1.2 USBtinyISP Driver

USBtinyISP 基于 USBtiny 对 USB 低速协议的软件实现。USBtinyISP 由 Adafruit 开发，有关程序员的文档和更多信息可在 learn.adafruit.com/usbtinyisp 上找到。Adafruit 提供了任何人构建自己的 USBtinyISP 编程器所需的所有信息，还提供一套零件套件以方便构建编程器。有多种 USBtinyISP 变体可用，例如本章开头图 A.1 左侧所示的变体。

有关 USBtinyISP 的 Adafruit 驱动程序链接可在 USBtinyISP 驱动程序页面 learn.adafruit.com/usbtinyisp/drivers 上找到。单击该页面上的“下载 Adafruit 驱动程序安装程序”按钮将打开 GitHub 上的一个页面。可在 GitHub 页面上找到可执行驱动程序安装程序的链接。撰写本文时，安装程序版本为 2.5.0.0，可执行文件名为 adafruit_drivers_2.5.0.0.exe。单击链接以下载此文件。

![](img/83ef13a6c66cc7882b2f357e97f451dc_338_0.png)

图 A.5: Microsoft Defender SmartScreen 对话框

下载 Adafruit 驱动程序可执行文件后，使用 Windows 资源管理器导航到该文件并双击它以运行。由于驱动程序安装程序和驱动程序

