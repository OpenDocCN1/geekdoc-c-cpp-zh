
```
PIN 5 to Gnd
PIN 6 to Vdd
PIN 7 to CHIPINO PIN SS (A5)
PIN 8 to NC
PIN 9 to Gnd
PIN 10 to Switch/Resistor Connection
PIN 11 to NC
PIN 12 to NC
PIN 13 to NC
PIN 14 to NC
PIN 15 to NC
PIN 16 to LED1 Anode
PIN 17 to LED2 Anode
PIN 18 to 5v

Switch connected to ground and 10k resistor, 10k resistor to 5v.
LED1 and LED2 each Cathode to ground through 1k ohm resistor.

*/
```

SimpleC 的头文件接下来使用引号包含，因为该文件与我们的主 C 文件位于同一目录中。

```
#include "simplec1.1.h"
```

代码的主循环接下来开始，并使用 SimpleC 库中的两个初始化函数。init_micro 函数建立 I/O 设置，然后 spi_init 函数为使用硬件 SPI 端口创建必要的设置。

```
void
main(void)
{
init_micro();
spi_init();
}
```

专门用于 MCP23S08 的第一个函数通过控制 IODIR 寄存器来将引脚设置为其正确输入/输出状态。此标签 IODIR 在 simplec1.1.h 文件中定义。设置与 PIC 类似，其中 1 为输入，0 为输出。因此 MCP23S08 上的 8 个引脚被设置为使 GP0 引脚为输入，其余为输出。

```
WR_MCP23S08 (IODIR, 0x01);    // Setup pins
```

代码的连续循环包含在 while 循环中。第一步是创建本地 8 位变量 y 并将其预设为 1。

```
while (1==1)
{
    char y = 1;
```

SimpleC 库中的 RD_MCP23S08 函数用于测试开关的状态。它实际上读取所有引脚的状态，因此我们必须使用二进制 AND 函数来仅查看 GP0 位。之后 y 变量将包含开关的状态。

```
y = RD_MCP23S08 (GPIO); // Read switch
y = y & 0x01;           // Mask all but bit 7
```

我们测试 y 变量以查看其是否为零，表示开关被按下。如果开关被按下，我们使用 WR_MCP23S08 函数写入在 simplec1.1.h 文件中定义的锁存寄存器 OLAT。我们将 GP6 位设置为 1 以点亮该 LED，如果开关被按下。如果 y 变量为 1 表示开关空闲，则 OLAT 寄存器被设置为使 GP7 位为 1 并点亮另一个 LED。

```
if (y==0)
    {WR_MCP23S08 (OLAT, 0x40);}  // If switch idle light LED
else
    {WR_MCP23S08 (OLAT, 0x80);}  // If switch pressed LED off
```

我们使用 SimpleC 库中的 pause 函数延迟 10 毫秒，然后循环回到 while 循环的开头。

```
    pause(10);
} //End While
```

最后我们用主循环的大括号结束这个简短程序。

```
} //End Main
```

## 项目 3 – 来自 MCP23S08 的输出

这个项目只是前一个项目的变体，因为它只驱动 MCP23S08 的输出。我们在前一个项目中是基于开关状态来做的。这个项目使用相同的 LED 连接，用 LED 作为指示器创建一个快速的二位二进制计数器。

### 硬件

硬件只是前一个项目的简化版本。你可以使用之前的面包板设置，因此这是对 SPI 示例的快速补充。MCP23S08 可以直接驱动 LED，因为每个引脚都有较高的输出电流驱动。这可能很有用，因为 LED 可以被驱动继电器线圈的晶体管取代。

![](img/910b145bee7ca8076318eafbe6d13997_149_0.png)

图 8-5：SPI 项目 3 电路图

![](img/910b145bee7ca8076318eafbe6d13997_150_0.png)

图 8-6A：SPI 项目 3 面包板

![](img/910b145bee7ca8076318eafbe6d13997_150_1.png)

图 8-6B：带 CHIPINO 模块的 SPI 项目 3

### 软件

软件也与前一个项目非常相似。软件只使用 WR_MCP23S08 函数而不使用 RD 函数。这使程序更短，并显示 SimpleC 如何使向项目添加输出变得容易。

```
/******************
PIC16F886 SPI - MCP23S08 I/O expander
The program controls two LEDs connected to the MCP23S08 GP6 and GP7 pin.
It binary counts from zero to three on the LEDs.

Connections
MCP23S08
```

```
PIN 1 to CHIPINO PIN 4 (SCK/RC3)
PIN 2 to CHIPINO PIN 2 (SDO/RC5)
PIN 3 to CHIPINO PIN 3 (SDI/RC4)
PIN 4 to Gnd
PIN 5 to Gnd
PIN 6 to Vdd
PIN 7 to CHIPINO PIN SS (A5)
PIN 8 to NC
PIN 9 to Gnd
PIN 10 to NC
PIN 11 to NC
PIN 12 to NC
PIN 13 to NC
PIN 14 to NC
PIN 15 to NC
PIN 16 to LED1 Anode
PIN 17 to LED2 Anode
PIN 18 to 5v

LED1 and LED2 each Cathode to ground through 1k ohm resistor.
*/

#include "simplec1.h"

void
main(void)
{
init_micro();
spi_init();
WR_MCP23S08 (IODIR, 0x00);    // Setup pins as outputs
while (1==1)
{
    for(char x = 0; x<4; x++)
    {
        WR_MCP23S08 (OLAT, x*64);    // Turn on LEDs
        pause(1000);
    }
} //End While
} //End Main
```

### 工作原理

该程序不需要太多来自前一个项目的解释。头文件非常相似，但描述和连接不同。

```
/***********************
PIC16F886 SPI - MCP23S08 I/O expander
The program controls two LEDs connected to the MCP23S08 GP6 and GP7 pin.
It binary counts from zero to three on the LEDs.

Connections
MCP23S08
PIN 1 to CHIPINO PIN 4 (SCK/RC3)
PIN 2 to CHIPINO PIN 2 (SDO/RC5)
PIN 3 to CHIPINO PIN 3 (SDI/RC4)
PIN 4 to Gnd
PIN 5 to Gnd
PIN 6 to Vdd
PIN 7 to CHIPINO PIN SS (A5)
PIN 8 to NC
PIN 9 to Gnd
PIN 10 to NC
PIN 11 to NC
PIN 12 to NC
PIN 13 to NC
PIN 14 to NC
PIN 15 to NC
PIN 16 to LED1 Anode
PIN 17 to LED2 Anode
PIN 18 to 5v

LED1 and LED2 each Cathode to ground through 1k ohm resistor.
*/

添加 SimpleC 包含文件，然后是此项目的主循环和初始化函数。

```
#include "simplec1.1.h"

void
main(void)
{
init_micro();
spi_init();
}
```

WR_MCP23S08 函数用于通过向 IODIR 寄存器写入全零来将所有引脚设置为输出。

```
WR_MCP23S08 (IODIR, 0x00);  // Setup pins as outputs
```

while 循环包含一个 for 循环，循环计数 4 次。每次循环将变量 x 增加一。然后该变量乘以 64 以将位移至 MCP23S08 的 GP6 和 GP7 引脚。WR_MCP23S08 函数可以在写入值到 OLAT 寄存器之前在其参数部分处理数学运算。添加一秒延迟以创建一个一秒二进制计数器。

```
while (1==1)
{
    for(char x = 0; x<4; x++)
    {
        WR_MCP23S08 (OLAT, x*64);    // Turn on LEDs
        pause(1000);
    }
} //End While
} //End Main
```

### 后续步骤

这些项目展示了 SimpleC 如何使使用硬件 SPI 外设变得容易。我将经常使用它，我经常想在许多项目中使用 MCP23S08 及其 16 I/O 兄弟 MCP23S16，但真的不想阅读数据手册并处理所有寄存器，而我可以用更大的 PIC 来获得更多 I/O。但现在我花时间为 MCP23S08 创建了一个函数，我将更多地使用它们。

作为下一步，你可以扩展项目以控制 MCP23S08 上的更多 I/O 并创建一串 LED 或多个开关。这可以通过对这些项目的少量修改轻松实现。现在如果你真的想更进一步，那么也许可以为每个设备连接 EEPROM 并使用单独的片选 (CS) 控制线。这将要求你修改 SimpleC 文件，但应该不会太困难。然后你可以从 PIC 控制多个 SPI 设备。

## 第 9 章 – SimpleC 脉宽调制

在本章中，我将向你展示 SimpleC 如何使使用硬件 PWM 外设变得极其容易。你可以在一行命令中设置频率和占空比。由于 SimpleC 是为固定的 16MHz 振荡器编写的，我能够在 SimpleC PWM 函数内完成所有计算并预设所有寄存器。因此，SimpleC 用户唯一需要做的就是决定频率和占空比。如果你想了解外设内部工作原理的更多细节，我在我的第二卷书籍中涵盖了这一点，并展示了用于计算寄存器设置的公式。在这里，我们将走简单路线并使用 SimpleC。

这个项目将使用 5 KHz 频率信号驱动两个 PWM 输出。微控制器将使用模拟引脚读取电位器，然后相应地调整 PWM1 的占空比。该项目还将以与 PWM1 相同的频率驱动 PWM2 引脚，但在 PWM2 上为恒定的 50% 占空比信号。输出将驱动 LED 以提供视觉反馈。我还在示波器上捕获了信号以显示信号（图 9-3）。

### 硬件

该项目的硬件非常简单易建。图 9-1 中的原理图显示了连接。PWM 1 在 CHIPINO 引脚 5 (C2) 上，PWM 2 在 CHIPINO 引脚 6 (C1) 上，并连接了 LED。电位器在其滑动端引脚上产生 V+ 和 V- 之间的可变电压，该电压介于 5V 和地之间。模拟引脚 AN0 将监测电位器。CHIPINO 具有 16 MHz 晶体，可驱动微控制器和内部 PWM 信号。
