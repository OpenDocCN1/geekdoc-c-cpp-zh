
注意，在 V1 版本中，USBTX 和 USBRX 提供了用于连接 USB 端口的 GPIO 引脚，而在 V2 版本中则是 MICROBIT_PIN_UART_TX 和 MICROBIT_PIN_UART_RX。

在本章的剩余部分，我们将使用 uBit serial 属性，因为这是最常用的工作方式。MicroBitSerial 对象的构造函数接受要使用的引脚（Tx 和 Rx）作为参数 `tx` 和 `rx`：

```
MicroBitSerial(PinName tx, PinName rx);
```

由 uBit 对象创建的默认 MicroBitSerial 对象通过构造函数设置为 USB 引脚。还有一个版本的构造函数允许你设置大小：

```
MicroBitSerial( PinName tx, PinName rx, uint8_t rxBufferSize)
```

以及一个可以分别设置 Tx 和 Rx 缓冲区大小的版本：

```
MicroBitSerial( PinName tx, rx,
uint8_t rxBufferSize,
uint8_t txBufferSize)
```

目前你可以大部分忽略缓冲区大小，直接使用默认值即可。

一旦你拥有了 MicroBitSerial 对象，可以使用以下方法设置波特率：
`baud( int baudrate)`

对于 V1：
`setBaudrate( int baudrate)`

对于 V2：
这是目前你使用高级级 micro:bit 框架可以更改的唯一设置。目前没有简单的方法可以更改 V2 串口的配置，但你可以使用从 mbed 框架深处继承的方法修改 V1 串口配置：
`void SerialBase::format(int bits, Parity parity, int stop_bits)`

其中 Parity 的类型定义如下：

```
enum Parity {
None = 0,
Odd,
Even,
Forced1,
Forced0
};
```

例如，为了设置两个停止位，你可能会使用（仅限 V1）：

```
uBit.init();
uBit.serial.format(8,mbed::RawSerial::None,2);
uBit.serial.baud(115200);
uBit.serial.send("A\r\n");
```

`format` 的唯一问题是，无法保证它不会与框架的其他部分以意想不到的方式发生交互，尽管它看起来并没有。

如果你想通过 MicroBit 对象与 USB 连接以外的任何设备进行通信，最后的配置函数非常重要：

```
int redirect(PinName tx, PinName rx)
```

这会将 Tx 和 Rx 引脚更改为你指定的任何引脚。

其余的配置似乎也会转移到新引脚。例如，若要在边缘连接器的物理引脚 1 上发送内容并在引脚 2 上接收，在 V1 上你会使用：

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

在 V2 上则是：

```cpp
#include "MicroBit.h"
MicroBit uBit;

int main() {
{
uBit.init();
uBit.serial.setBaudrate(115200);
uBit.serial.redirect(uBit.io.P1 , uBit.io.P2);
uBit.serial.send("A\r\n");
}
```

如果你将逻辑分析仪连接到 P1，你将看到字母 A 的串口数据，随后是一个回车符和一个换行符。

# 发送数据

我们已经使用了 `send` 函数但还没有真正讨论过它，发送数据并不是使用串口的困难部分。有一组 `send` 函数，它们在允许发送的内容上有所不同：

- `int sendChar(char c)`
- `int send(ManagedString s)`
- `int send(ManagedString s, MicroBitSerialMode)`
- `int send(uint8_t *buffer, int bufferLen)`
- `int send(uint8_t *buffer, int bufferLen, MicroBitSerialMode mode)`

你可以看到你可以发送单个字符、ManagedString 或字节缓冲区，这通常已经足够了。此外，还有一个 `put` 方法允许你发送字符，但由于你有 `sendChar`，所以它并不真正需要。你也不 `puts`，因为 `send` 会自动将标准的 C 字符串转换为托管字符串。

唯一看起来有用的继承方法是：
`send_break()`

它发送一个比字符时间更长的低电平。这仅适用于 V1，用于需要空位信号来重置或执行特殊操作且无法作为字符代码发送的设备。

最后，串口驱动中还有一个 `printf` 函数。它基于标准的 C `printf` 函数，但只支持有限的数据类型。你可以使用 `%c`, `%d`, `%s`, `%x` 和 `%X`。

在接收数据时，模式参数更为重要，但在发送数据时它也有影响。

共有三种模式：

- **ASY**：字符被发送到缓冲区，函数立即返回。
- **SYNC_SPINWAIT**：字符被发送到缓冲区，程序进行自旋（等待）。
- **SYNC_SLEEP**：字符被发送到缓冲区，程序进入睡眠。

# 读取数据

在接收数据时，模式参数更为重要，但在发送数据时它也有影响。（等等，我重复了，我将直接提供最终输出）。
