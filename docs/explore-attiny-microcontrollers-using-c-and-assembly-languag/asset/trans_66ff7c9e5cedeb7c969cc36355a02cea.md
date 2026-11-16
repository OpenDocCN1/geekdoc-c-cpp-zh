

在附录 B 中每个图表的 J2 旁边，以便从 USBasp 到面包板电路进行连接。此图像与 J2 具有相同的引脚定义，但已翻转，并且是面对排线末端母连接器孔洞的视图。使用此图像可以轻松地将 USBasp 连接到 AVR 电路，方法是将图像用作母连接器的映射。

### 6 针适配器 (ISP/SPI)

如果将 10 针转 6 针适配器与 USBasp 一起使用，请使用附录 B 中每个图表上方 SPI 标头 J1 处的插图，将 USBasp 连接到电路。使用两端均带有公连接器的杜邦线，或单股导线，从 USBasp 适配器的 6 针母连接器连接到 AVR 电路。插图与 J1 具有相同的引脚定义，只是已翻转，并且是面对适配器上 6 针母连接器孔洞的视图。使用此图像作为映射，从 USBasp 连接到 AVR 电路。

## A.3.3.2 连接 USBtinyISP

USBtinyISP 编程器以及原始 USBtinyISP 设计的变体，通常带有 6 针 ISP/SPI 连接器。这可能是公标头形式，也可能是排线末端的 6 针母连接器。对公标头和母排线连接器的连接将在以下标题中说明。

### 6 针公标头

可以使用一端带有母连接器、另一端带有公连接器的杜邦线，直接将 USBtinyISP 上的 6 针公标头连接到 AVR 电路。进行此连接时，请使用附录 B 电路中的连接器 J1（即 SPI 标头）来连接到 AVR 电路。

### 排线上的 6 针母连接器

使用两端均带有公针的杜邦线，或单股导线，从 USBtinyISP 的 6 针母连接器连接到 AVR 电路。如果进行此连接，请使用附录 B 电路中 J1 上方的 6 针母连接器插图。该图像是面对母连接器孔洞的视图。

## A.3.3.3 连接 Arduino Uno ArduinoISP

附录 B 中的每个电路都显示了将 Arduino Uno 连接到 ATtiny 微控制器所需的连接，前提是将 Arduino 用作 ISP 编程器。名为 ArduinoISP 的草图必须加载到 Arduino 中，如本附录中已所述。

在附录 B 中包含 Arduino Uno 连接的每个电路的插图中，仅显示了 Arduino Uno 边缘连接器及其 ICSP 标头中一个连接器的连接。这些连接器适用于板子顶部朝上且 USB 连接器在左侧的 Arduino Uno。所有编程连接都可以从板子边缘的左上角 Arduino 标头引出，该标头提供了所有可用的 ISP/SPI 引脚——GND、SCK、MISO、MOSI 和 RESET。如果使用此连接器连接到 AVR 电路，可以使用两端均带有公针的杜邦连接器或单股导线来进行连接。要从 Arduino Uno 为电路供电，请使用板子另一侧 Arduino POWER 连接器上的 5V 连接，或使用 Arduino Uno ICSP 标头上的 5V。

作为使用边缘连接器连接到目标 AVR 电路的替代方案，可以将导线从 ICSP 标头连接到 AVR 电路。在这种情况下，可以使用一端带有母连接器、另一端带有公连接器的杜邦线。请注意，RESET 仍必须从边缘连接器的引脚 10 引出，而不是从 ICSP 标头引出。ICSP 标头上的 RESET 是 Arduino 的复位输入。

## A.3.4 编程参数

必须为每种 ATtiny 器件与所用编程器的组合确定要传递给 avrdude 的编程参数（也称为命令行选项或参数）。这些参数将在 Microchip Studio 中设置，调用 avrdude 时，Microchip Studio 会将它们传递给 avrdude。

### A.3.4.1 avrdude 文档

可在 download.savannah.gnu.org/releases/avrdude/ 上找到 avrdude 的 PDF 格式文档，其中包含有关使用 avrdude 的更多信息，并提供每个版本 avrdude 的 PDF 文件。名为 avrdude-doc-6.3.pdf 的文件是 avrdude 6.3 版本的文档，该版本在撰写时为当前版本。这是官方 avrdude 文档，可查阅以获取有关 avrdude 的信息。其中包含 avrdude 可识别的编程参数。

### A.3.4.2 avrdude 参数说明

此处解释了必须传递给不同编程器的 avrdude 的参数。本节只是一个概述，旨在更好地了解 avrdude 的工作原理。本书涵盖的三款业余爱好者编程器的特定参数如下。作为第一个示例，请参阅以下内容。

```
avrdude -p t85 -c usbasp -P usb -U flash:w:"file.hex"
```

上述代码行显示了如何从命令行调用 avrdude，以将程序从文件加载到 AVR 微控制器的 Flash 存储器中。虽然我们不会直接从命令行调用 avrdude，但 avrdude 是一个命令行程序，我们需要了解如何在 Microchip Studio 中设置它时使用它。

上述行中的第一个项目是 avrdude，它调用 avrdude 可执行程序——换句话说，它会调用或运行我们下载的名为 avrdude.exe 的 avrdude 程序。在调用 avrdude 之后的项目是从命令行传递给 avrdude 的命令行选项，只需在 avrdude 后输入即可。

第一个选项是 -p 开关，用于指定要编程的器件，后跟特定器件的代码。在此示例中，-p 后跟 t85，这是 ATtiny85 器件的代码。第 1 章第 1.3 节表 1.1 中 PDIP 封装 ATtiny 微控制器的器件代码显示在表 A.1 中。表 A.1 仅包含 avrdude 可编程的少量 AVR 器件。许多其他受支持的器件可以在 avrdude PDF 文档中找到。

### 表 A.1: avrdude 中 ATtiny 微控制器的器件代码

| 8 针 PDIP | | 20 针 PDIP | |
|---|---|---|---|
| ATtiny13 | t13 | ATtiny26 | t26 |
| ATtiny13A | t13 | ATtiny261A | t261 |
| | | ATtiny461 | t461 |
| ATtiny25 | t25 | ATtiny461A | t461 |
| ATtiny45 | t45 | ATtiny861 | t861 |
| ATtiny85 | t85 | ATtiny861A | t861 |
| | | | |
| **14 针 PDIP** | | ATtiny2313 | t2313 |
| ATtiny24 | t24 | ATtiny2313A | t2313 |
| ATtiny24A | t24 | ATtiny4313 | t4313 |
| ATtiny44 | t44 | | |
| ATtiny44A | t44 | **28 针 PDIP** | |
| ATtiny84 | t84 | ATtiny48 | t48 * |
| ATtiny84A | t84 | ATtiny88 | t88 |

在表 A.1 中，ATtiny48 器件标有星号，因为它未包含在 avrdude 文档的受支持器件列表中，并且 avrdude 6.3 版本不支持它。可以通过修改随 avrdude 附带的 avrdude.conf 文件来添加对 ATtiny48 的支持。可以使用任何文本或代码编辑器编辑此文本文件，并将来自 lists.nongnu.org/archive/html/avrdude-dev/2009-08/msg00005.html 的条目添加到其中。只需在文本编辑器中打开此文件并搜索“ATtiny88”，以便将上述条目放置在 ATtiny88 上方即可。如果您不放心编辑文件，或想要快速解决方案，请查找本书随附文件中的修改后的 avrdude.conf 文件。只需复制修改后的文件，替换我们安装 avrdude 的文件夹中当前存在的文件即可，如果您按照本附录中的说明操作，该文件夹位于 C:\avrdude-6.3-mingw32。

回到 avrdude 命令行参数示例，我们现在有 -c 开关，后跟编程器名称，如下面的粗体所示。

```
avrdude -p t85 -c usbasp -P usb -U flash:w:"file.hex"
```

-c 开关后必须跟一个编程器 ID。在上面的示例中，指定的编程器是 USBasp。表 A.2 显示了本附录中涵盖的三个编程器及其 avrdude 编程器 ID。

| 编程器 | ID |
| :--- | :--- |
| USBasp | usbasp |
| USBasp 克隆 | usbasp-clone |
| USBTinyISP | usbtiny |
| ArduinoISP | avrisp |

对于本书中所示的 USBasp，usbasp ID 可用。如果使用 USBasp 编程时遇到问题，可以尝试改用 usbasp-clone。如表 A.2 所示，USBTinyISP 的编程器 ID 是 usbtiny。当 Arduino Uno 加载了 ArduinoISP 草图后，它实际上已成为 ISP 编程器，因此必须与其使用 ID avrisp。avrdude 支持更多编程器，但如前所述，本附录仅涵盖三个编程器。

