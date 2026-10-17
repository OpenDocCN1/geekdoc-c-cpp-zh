
显然，如果你想要精度，`$V_{REF}$`（必须低于或等于 `$V_{DD}$`）应该由一个精确的低电压源设置。然而，在大多数应用中，`$V_{REF}$` 和 `$V_{DD}$` 简单地连接在一起，并使用常用的低质量电源电压作为参考。如果效果不好，你可以使用稳压二极管（Zener diode）作为参考，例如 `TL431`。

`MCP3000` 系列采用逐近近似法（successive approximation）。

其中 `x` 表示不确定，`b9` 根据数据第九位的值为 `0` 或 `1`。剩余的 `9` 位将在接下来的九个时钟脉冲响应中返回，你必须传输三个字节才能获取所有 `10` 位数据。这使得以 `8` 位为块读取数据变得非常混乱。

数据表手册建议了一种不同的处理方法，可以将数据整齐地封装在三个字节中。它建议的方法是发送单个字节：

`00000001`

从机会同时传输随机数据，这些数据会被忽略。最后的 `1` 被视为起始位。如果你现在传输第二个字节，其中最高有效位表示单端模式或差分模式，后跟一个三位地址，其余位设为零，那么从机将返回空空位和转换结果的高两个位。现在你只需要获取最终的 `8` 位数据进行读取即可：

| MCU 发送数据 | | | | | | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| n (与时钟下降沿对齐) | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | | | | |
| MCU 接收数据 (与时钟上升沿对齐) | ? | ? | ? | ? | ? | ? | ? | ? | D2 | D1 | D0 | X | X | X | X |
| X = "忽略" | | | | | | | | | 87 | 86 | 85 | 84 | 83 | 82 | 81

![](img/23976341c9281123e7b181beea6e9dbd_172_0.png)

你可以采用数据手册描述的第一种方法，但这种方法得到的两个字节包含数据，且所有低位都处于正确的位置。

利用这些信息，我们可以编写读取特定通道的指令。例如，要读取通道 `0`，我们首先发送一个设置为 `0x01` 的字节作为起始位，并忽略从机的传输。我们发送 `0x80` 来选择单端模式，通道 `0` 保留从机返回的高两个位。最后，我们发送一个零字节以便从从机获取低位。对于 `microbit V1`，使用之前提供的 `SPITransfer` 函数如下：

```c
uint8_t buf[] = {0x01, 0x00, 0x00};
uint8_t readBuf[3];
CS.setDigitalValue(0);
SPITransfer(buf, 3, readBuf, 3);
CS.setDigitalValue(1);
```

注意 `CS` 线在整个事务期间保持低电平。

对于 `microbit V2`，`SPITransfer` 的调用已改为：

`pi.transfer(buf, 3, readBuf, 3);`

`uBit.sleep(1);`

`sleep` 是保持 `CS` 线足够长时间的一种粗略方法。更好的解决方案是使用回调函数——参见之前的

为了从 `readBuf` 中提取数据，我们需要进行一些位操作：

`data=((int)readBuf[1])<<8|(int)readBuf[2];`

表达式的第一部分从从机发送的第一个字节中提取低三位，由于这些是最高有效位，它们被向左移动八位。然后将剩余位与它们进行 `OR` 运算，以得到完整的 `10` 位结果。假设 `V_REF` 为 `3.3V`，转换为电压：

`int volts=data*330/1023;`

注意，我们通过处理 `volts*100` 避免了浮点数运算。

在实际应用中，你还需要将电压转换为其他物理量，例如温度或光照。

完整的程序是：

```c
#include "MicroBit.h"

MicroBit uBit;

SPI spi(MOSI, MISO, SCK);

MicroBitPin CS(MICROBIT_ID_IO0_P16, MICROBIT PIN P16, PIN CAPABILITY_DIGITAL);
//SPITransfer 函数仅对 V1 需要
int SPITransfer(uint8_t *txBuffer, uint32_t txSize, uint8_t *rxBuffer, uint32_t rxSize)
{
CS.setDigitalValue(0);
uint32_t i;
for (i = 0; i < txSize; i++)
{
if (i < rxSize)
{
rxBuffer[i] = spi.write(txBuffer[i]);
} else
{
spi.write(txBuffer[i]);
}
}
CS.setDigitalValue(1);
return 0;
}
```

```c
int main()
{
    CS.setDigitalValue(1);
    spi.format(8, 0);
    spi.frequency(1000000);

    uint8_t buf[] = {0x01, 0x80, 0x00};
    uint8_t readBuf[3];
    CS.setDigitalValue(0);
    SPITransfer(buf, 3, readBuf, 3);// // V2 注释掉
    //spi.transfer(buf, 3, readBuf, 3); // V2 取消注释
    //uBit.sleep(1);//V2 取消注释
    CS.setDigitalValue(1);
    int data = ((int)readBuf[1] & 0x03) << 8 | (int)readBuf[2];
    int volts = data * 330 / 1023;
    uBit.serial.printf("data %d\n\r", volts);

    release_fiber();
    return 0;
}
```

## 一些封装函数

这些方法都可行，但如果能有一个函数读取指定通道的 A-D 转换就更好了，现在我们可以：

```c
int readADC(uint8_t chan)
{
    uint8_t buf[] = {0x01, (0x08 | chan) << 4, 0x00};
    uint8_t readBuf[3];
    CS.setDigitalValue(0);
    SPITransfer(buf, 3,readBuf, 3); // V2 注释掉

    //spi.transfer(buf, 3, readBuf, 3); // V2 取消注释
    //uBit.sleep(1);//V2 取消注释
    CS.setDigitalValue(1);
    int data = ((int)readBuf[1] & 0x03) << 8 | (int)readBuf[2];
    int volts = data * 330 / 1023;
    uBit.serial.printf("data %d\n\r", volts);

    release_fiber();
    return 0;
}
```

# 第 12 章

## 串口连接

串口是连接设备的最古老的方法之一，但它仍然非常有用。`micro:bit` 有单一的串口接口，但它可以被定向使用任何 `GPIO` 引脚作为 `Rx`（接收）和 `Tx`（发送）。驱动 `micro:bit` 的软件做了大量工作，使其基于的单任务环境更像多任务操作系统。它为处理串口接口提供的功能非常丰富，了解其工作原理非常重要，因为这些功能远超其作为基础的原始串口设施。

## 串口协议

串口协议非常简单——这可能是因为它发明于使用机电元件、电机等设备生成数据的时代。它的设计初衷是让早期的电打字机能够工作，因此你经常会看到与之相关的 `TTY` 等缩写。由于用于串口通信的电子设备被称为通用异步收发器，因此经常使用 `UART` 这个术语。

最早的标准是 `V24` 和 `RS232`。然而，请注意，早期的通信工作在 `±24` 和后来的 `±12V` 之间。今天串口通信工作在逻辑电平或 `TTL` 电平，范围为 `0` 到 `5V` 或 `0` 到 `3.3V`。电压差是一个我们将稍后讨论的问题。重要的是，无论电压如何，协议始终是相同的。

目前，如前所述，协议是简单的。线路在空闲时处于高电平并表示 `0`。当设备开始传输时，它会将线路拉低以产生一个起始位。该位的位宽决定了传输速度。起始位之后是可变数量的数据位、一个可选的校验位，最后是一个或两个停止位。

最初，起始位的目的是允许电机开始启动，并允许接收端执行任何定时处理。停止位同样是为了给线路留出回到空闲状态的时间。早期，该协议使用的速度非常慢——每秒 `300` 波特就被认为足够快了。今天协议大体相同，但不再需要多个停止位，且通信省去了这些步骤。传输速度也更高——`9600` 或 `115200`。

为了指定正在使用的协议，你经常会遇到简短形式——例如：`9600` 波特、`8` 位数据位、无校验、`1` 位停止位。

![](img/23976341c928123e7b181ea67db.png)

什么是波特？波特率指的是位时间。

| 波特 (Baud) | 位时间 (Bit Time) |
| :--- | :--- |
| 300 | ~3ms |
| 9600 | ~104µs |
| 115200 | ~8µs |

注意波特率并不等于数据发送速度，因为计算中包含了起始位以及可能的校验位。

## 硬件

一个简单的串口接口有一个发送引脚 `Tx` 和接收引脚 `Rx`。这意味着一个串口接口只需要两根线即可进行双向通信。通常，你将一个设备的 `Tx` 引脚连接另一个设备的 `Rx` 引脚，反之亦然。唯一的问题是，某些制造商根据引脚应该连接到哪里进行标记，而不是它们实际是什么，你必须将 `Rx` 连接到 `Tx`，将 `Tx` 连接到 `Rx`，这并没有太大帮助。如果你有任何疑问，通常需要用示波器、逻辑探针或表进行检查。

除了 `Tx` 和 `Rx` 引脚外，串口接口还有许多控制线。这些大部分是为了帮助旧式的打字机设计的，现在并不经常使用。例如，`RTS`（请求发送）是一条用于请求连接另一端设备发送数据的线路，`CTS`类允许发送）是一条表示可以发送数据的线路，此类此类。对于现代设备之间的许多连接，你可以忽略这些额外线路，只需发送和接收数据。如果你需要与实现复杂接口的设备建立接口，你将需要查找细节并手工编写程序来与其交互。在本章的其余部分，我们将使用 `Tx` 和 `Rx`，并忽略额外的状态和信号线。

`micro:bit` `CPU` 中的 `UART` 可以独立于硬件的其他部分工作。当 `CPU` 在处理其他事情时，它会接收和传输数据。通常，它连接到属于 `USB` 端口的引脚。这意味着，默认情况下，通过 `USB` 端口发送和接收串口数据，如果它连接到串口驱动程序，你就自动拥有了一个工作的串口连接（前提是速度设置正确）。串口设备可以连接到任何 `GPIO` 线，这一事实使其能够直接与其他设备通信，而无需涉及 `USB` 端口。你甚至可以与连接到 `GPIO` 线的设备通信，并将 `USB` 端口发生的情况回显。

`micro:bit` 在 `0V` 到 `3.3V` 之间实现串口通信，而基于 `PC` 的串口通常使用 `+13V` 到 `-13V`，所有符合 `RS232` 标准的端口都使用正负电压摆幅，这与 `micro:bit` 以及大多数其他微处理器完全不兼容。如果你使用通过 `USB` 端口连接串口设备的默认配置，则无需担心。然而，如果你想使用 `GPIO` 线，你就需要对电平转换进行处理。

要连接到 `microbit`，你需要一个工作在 `0V` 到 `3.3V` 之间的 `USB-TTL` 电平串口接口。市场上有很多种。你只需要将 `USB` 接口插入 `PC` 或设备，安装驱动程序并开始传输数据。如果你想使用 `USB` 串口，你需要在台式电脑上使用串口终端来连接到 `microbit`。对于 `Windows`，只需下载 `PuTTY` 即可。

`USB` 连接的默认值是 `115200` 波特、`8` 位、无校验、`1` 位停止位。如果你使用 `PC` 和 `PuTTY`，只需将 `PuTTY` 设置为 `115200`，它就能正常工作。

## 串口命令

似乎有很多与串口相关的命令。然而，它们仅分为三组：初始化、写入和读取。不幸的是，`microbit` 对串口对象的实现中有许多细微变化。

初始化命令控制端口的工作方式。它们都创建或操作 `MicroBitSerial` 实例，但如果你想创建自己的实例，不要使用 `uBit` 的实例。这会导致两个 `MicroBitSerial` 实例尝试控制硬件产生冲突。如果你想使用 `uBit` 提供的其他功能，简单的方法是创建一个全局 `uBit` 并按通常的方式初始化它。然后使用它的属性访问已创建的 `MicroBitSerial` 对象：

```cpp
#include "MicroBit.h"
MicroBit uBit;
int main() {
{
	uBit.init();
	uBit.serial.baud(115200);
	uBit.serial.send("A\r\n");
}
```

默认连接到 `USB` 串口，因此你应该在连接到端口的串口台中看到一个 `A`。注意对于 `V2`，波特率的名为 `setBaudrate`。

如果你不想使用 `uBit`，你需要将 `MicroBitSerial` 创建为全局对象。要创建一个与之前程序相同的程序，你可以使用：

```cpp
#include "MicroBit.h"
/* 为 V2 取消注释
#define setBaudrate
#define USBTX MICROBIT_PIN UART TX
#define USBRX MICROBIT_PIN UART_RX
*/
MicroBitSerial serial(USBTX, USBRX);

int main() {
{
	serial.baud(115200);
	serial.send("A\r\n");
	release_fiber();
}
```

注意，在 `V1` 版本中，`USBTX` 和 `USBRX` 提供了用于连接 `USB` 端口的 `GPIO` 引脚，而在 `V2` 版本中则是 `MICROBIT_PIN_UART_TX` 和 `MICROBIT_PIN_UART_RX`。

在本章的剩余部分，我们将使用 `uBit serial` 属性，因为这是最常用的工作方式。`MicroBitSerial` 对象的构造函数接受要使用的引脚（`Tx` 和 `Rx`）作为参数 `tx` 和 `rx`：

```
MicroBitSerial(PinName tx, PinName rx);
```

由 `uBit` 对象创建的默认 `MicroBitSerial` 对象通过构造函数设置为 `USB` 引脚。还有一个版本的构造函数允许你设置大小：

```
MicroBitSerial( PinName tx, PinName rx, uint8_t rxBufferSize)
```

以及一个可以分别设置 `Tx` 和 `Rx` 缓冲区大小的版本：

```
MicroBitSerial( PinName tx, rx,
uint8_t rxBufferSize,
uint8_t txBufferSize)
```

目前你可以大部分忽略缓冲区大小，直接使用默认值即可。

一旦你拥有了 `MicroBitSerial` 对象，可以使用以下方法设置波特率：

`baud( int baudrate)`

对于 `V1`：

`setBaudrate( int baudrate)`

对于 `V2`：

这是目前你使用高级级 `micro:bit` 框架可以更改的唯一设置。目前没有简单的方法可以更改 `V2` 串口的配置，但你可以使用从 `mbed` 框架深处继承的方法修改 `V1` 串口配置：

`void SerialBase::format(int bits, Parity parity, int stop_bits)`

其中 `Parity` 的类型定义如下：

```
enum Parity {
None = 0,
Odd,
Even,
Forced1,
Forced0
};
```

例如，为了设置两个停止位，你可能会使用（仅限 `V1`）：

```
uBit.init();
uBit.serial.format(8,mbed::RawSerial::None,2);
uBit.serial.baud(115200);
uBit.serial.send("A\r\n");
```

`format` 的唯一问题是，无法保证它不会与框架的其他部分以意想不到的方式发生交互，尽管它看起来并没有。

如果你想通过 `MicroBit` 对象与 `USB` 连接以外的任何设备进行通信，最后的配置函数非常重要：

```
int redirect(PinName tx, PinName rx)
```

这会将 `Tx` 和 `Rx` 引脚更改为你指定的任何引脚。

其余的配置似乎也会转移到新引脚。例如，若要在边缘连接器的物理引脚 `1` 上发送内容并在引脚 `2` 上接收，在 `V1` 上你会使用：

```cpp
#include "MicroBit.h"
MicroBit uBit;

int main() {
{
uBit.init();
uBit.serial.format(8,mbed::RawSerial::None,2);
uBit.serial.baud(115200);
uBit.serial.redirect(MICROBIT_PIN_P1, MICROBIT_PIN_P2);
uBit.serial.send("A\r\n");
}
```

在 `V2` 上则是：
