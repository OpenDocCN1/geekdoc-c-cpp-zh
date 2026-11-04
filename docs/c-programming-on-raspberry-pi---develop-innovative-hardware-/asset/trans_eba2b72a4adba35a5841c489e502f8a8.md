
模块：

| GPIO 引脚 | 信号 | 名称 |
| --- | --- | --- |
| 10 | MOSI | SPI0 |
| 9 | MISO | SPI0 |
| 11 | SCLK | SPI0 |
| 8 | CE0 | SPI0 |
| 7 | CE1 | SPI0 |
| 19 | MISO | SPI1 |
| 20 | MOSI | SPI1 |
| 21 | SCLK | SPI1 |
| 18 | CE0 | SPI1 |
| 17 | CE1 | SPI1 |
| 16 | CE2 | SPI1 |

SPI0 有两个片选使能引脚：CE0 和 CE1。SPI1 有三个：CE0、CE1 和 CE2。默认情况下，SPI1 未启用，Raspberry Pi 允许你使用带片选引脚 CE0 和 CE1 的 SPI0。SPI1 可通过在 /boot/config.txt 中配置的 dt overlay 启用。例如：

```
dtoverlay=spi1-3cs
```

重启并使用以下命令检查 SPI 线路：

```
ls /dev/spidev*
```

## 8.3 • 项目 1 – 端口扩展器

### 描述：

本节给出了一个简单项目，用于展示如何在程序中使用 SPI 功能。该项目与第 7.3 节给出的端口扩展器项目 1 非常相似。在该项目中使用了 I2C 兼容芯片 MCP23017。在本项目中，使用 SPI 总线兼容的端口扩展器芯片 MCP23S17 为 Raspberry Pi 提供额外的 16 个 I/O 端口。MCP23S17 的操作与 MCP23017 的操作完全相同，区别在于 MCP23S17 使用 SPI 总线。在本项目中，一个 LED 连接到 MCP23S17 的端口引脚 GPA0，并且该 LED 每秒闪烁一次 ON 和 OFF。一个 470 欧姆限流电阻与 LED 串联使用。

### 目标：

本项目旨在展示如何在基于 Raspberry Pi 的项目中使用 SPI 总线。

### 框图：

该项目的框图与图 7.2 相同，但 MCP23017 芯片替换为 MCP23S17。

### MCP23S17

MCP23S17 是一款 28 引脚芯片，具有以下特性。引脚配置如图 8.2 所示，与 MCP23017 的引脚配置相同，但使用 SPI 引脚而非 I2C 引脚：

- 16 个双向 I/O 端口。
- 在 I2C 总线上最高 1.7MHz 操作。
- 中断能力。
- 外部复位输入。
- 低待机电流。
- +1.8 至 +5.5V 操作。
- 3 个地址引脚，因此 SPI 总线上最多可使用 8 个设备。
- 28 引脚 DIL 封装。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_241_0.png)

引脚说明见表 8.1。

| 引脚 | 描述 |
|---|---|
| GPA0-GPA7 | 端口 A 引脚 |
| GPB0-GPB7 | 端口 B 引脚 |
| VDD | 电源 |
| VSS | 地 |
| SI | SPI MOSI 数据引脚 |
| SCK | SPI 时钟引脚 |
| SO | SPI MISO 数据引脚 |
| CS | SPI SSEL 片选使能引脚 |
| A0-A2 | I2C 地址引脚 |
| RESET | 复位引脚 |
| INTA | 中断引脚 |
| INTB | 中断引脚 |

表 8.1 MCP23S17 引脚说明

MCP23S17 是一个 SPI 从设备。从机地址包含四个高固定位（0100）和三个用户定义的硬件地址位（引脚 A2、A1 和 A0），读/写位填满控制字节。这些地址位由控制寄存器 IOCON.HAEN 使能/禁用。默认情况下，用户地址位在上电时被禁用（即 IOCON.HAEN = 0），且 A2 = A1 = A0 = 0，芯片使用 0x40 寻址。因此，我们可以在 SPI0 上使用两个 MCP23S17 芯片，将一个 CS 位连接到 CE0，另一个连接到 CE1，并用 0x40 寻址两个芯片。通过将 HAEN 位设置为 1，我们可以在基于多个 MCP23S17 的应用（例如多于 2 个）中，通过相应连接 A2、A1 和 A0 来更改设备地址。可以连接十六个这样的芯片（8 个连接到 CE0，8 个连接到 CE1），对应 16x16 = 256 个 I/O 端口。图 8.3 和 8.4 显示了寻址格式。即使禁用，地址引脚也应进行外部偏置。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_242_0.png)

图 8.3 MCP23S17 控制字节格式

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_243_0.png)

*ACK 由 MCP23017 提供。
图 8.4 MCP23S17 寻址寄存器

与 MCP23017 一样，MCP23S17 芯片有 8 个内部寄存器，可配置其操作。通过配置位 IOCON.BANK，该器件可以工作在 16 位模式或两个 8 位模式。上电时，该位被清零，默认选择双 8 位模式。

端口引脚的 I/O 方向由寄存器 IODIRA（地址 0x00）和 IODIRB（地址 0x01）控制。在这些寄存器中将某位清零为 0，会使相应的端口引脚成为输出。类似地，在这些寄存器中将某位置 1，会使相应的端口引脚成为输入。GPIOA 和 GPIOB 寄存器地址分别为 0x12 和 0x13。如图 8.5 所示。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_243_1.png)

图 8.5 配置 I/O 端口

有关 MCP23S17 芯片的更多信息，可从以下网站上的 Microchip Inc 数据手册获取：
http://ww1.microchip.com/downloads/en/DeviceDoc/20001952C.pdf

### 电路图：

图 8.6 显示了该项目的电路图。SPI0 引脚 GPIO 10、GPIO 11 和 GPIO 8 用于 SPI 接口。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_244_0.png)

图 8.6 项目电路图

### 程序清单：

### wiringPi

wiringPi 包含 MCP23S17 芯片库，使芯片编程非常容易。必须在程序开头包含头文件 `<mcp23s17.h>`。必须使用以下函数初始化 SPI 总线：

```
mcp23s17Setup(Base, CE, address)
```

Base 是用于标识端口引脚的索引，且必须大于 64。CE 是所使用的片选使能引脚（0 表示 CE0，即我们使用 GPIO 8；1 表示 CE1，即我们使用 GPIO 7），address 是芯片地址（本项目为 0）。然后可以使用 pinMode 和 digitalWrite 函数来配置和访问端口引脚。例如，如果 Base = 100，则 `digitalWrite(100, 1)` 会将 GPA0 设置为逻辑 1，`digitalWrite(101, 1)` 会将 GPA1 设置为逻辑 1，依此类推。

图 8.7 显示了程序清单（程序：SPILED.c）。注意，在本项目中，SPI 总线初始化如下：

```
mcp23s17Setup(Base, CE, 0);
```

其中 Base = 100，CE = 0。

引脚 GPA0（索引 = 100）配置为输出，并形成一个 while 循环。在该循环内，该端口先被设置为逻辑 1，然后设置为逻辑 0，每个输出之间有一秒延迟。

```c
/*--------------------------------------------------------------
                 MCP23S17 SPI LED FLASH
                 ======================

In this program an LED is connected to MCP23S17 chip which is a SPI
based chip. The program flashes the LED every second

Author: Dogan Ibrahim
File  : SPILED.c
Date  : December 2020
--------------------------------------------------------------*/
#include <mcp23s17.h>
#include <wiringPi.h>

#define CE 0
#define Base 100

//
// Start of MAIN program
//
int main(void)
{
        wiringPiSetupGpio();
        mcp23s17Setup(Base, CE, 0);              // Use CE0
        pinMode(Base, OUTPUT);                   // LED output

        while(1)
        {
                digitalWrite(Base, LOW);        // LED OFF
                delay(1000);                     // 1 second
                digitalWrite(Base, HIGH);        // LED ON
                delay(1000);                     // 1 second
        }
}
```

图 8.7 程序：SPILED.c

你可以通过输入以下命令来编译并运行该程序：

```bash
gcc -o SPILED SPILED.c -lwiringPi -lwiringPiDev
sudo ./SPILED
```

### 修改后的程序：

图 8.7 给出的程序使用了内置的 MCP23S17 函数。我们也可以通过直接调用 SPI 函数，从基本原理出发对 MCP23S17 进行编程。了解这一点很有用，因为我们可以使用这些原理对任何其他基于 SPI 总线的芯片进行编程。

必须在程序开头包含头文件 `<wiringPiSPI.h>`。wiringPi 库支持以下 SPI 函数：

- **wiringPiSPISetup**：此函数初始化 SPI 总线。该函数有两个参数：第一个是 SPI 通道号，第二个是 SPI 速度。Raspberry Pi 4 有两个 SPI 通道：0 和 1。SPI 速度是 500,000 到 32,000,000 Hz 范围内的整数。该函数返回一个句柄，用于引用已初始化的 SPI 通道。如果无法初始化 SPI 通道，则返回 -1。
- **wiringPiSPIDataRW**：此函数在所选 SPI 总线上执行同时写/读事务。缓冲区中的数据会被总线返回的数据覆盖。该函数有三个参数：第一个是通道号，第二个是指向数据的指针。第三个参数是数据长度。

MCP23S17 芯片的编程如下（注意，并非所有 SPI 设备都需要设备地址）：

- 发送设备地址（本项目为 0x40）。
- 发送寄存器地址。
- 发送寄存器数据。

首先，我们必须将 I/O 方向寄存器 IODIRA 编程为 0，以使 PORT A 引脚为输出。该寄存器的地址为 0x0。然后，我们应编程 PORT A 的第 0 位（引脚 GPIOA），LED 连接在该引脚上。寄存器 GPIOA 的地址是 0x12。

图 8.8 显示了程序清单（程序：**SPILED2.c**）。程序开头定义了设备和寄存器地址。**channel** 设置为 0，因为 MCP23S17 的 CS 连接到 Raspberry Pi 的引脚 CE0。在主程序中，调用函数 **wiringPiSPISetup** 来设置通道号和 SPI 总线上的速度。该函数返回一个 **handle**，用于其他 SPI 函数调用。

程序中使用了两个函数：**configure** 设置寄存器 IODIRA，使 PORT A 引脚为输出。函数 **send** 向 MCP23S17 的寄存器 GPIOA 发送一个字节（0 或 1），从而按需打开或关闭 LED。你可以通过输入以下命令来编译并运行该程序：

```bash
gcc -o SPILED SPILED2.c -lwiringPi
sudo ./SPILED
```

