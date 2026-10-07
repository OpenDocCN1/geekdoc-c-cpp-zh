

注意，这是一个反相缓冲器，但你通常可以忽略它，并在软件中通过反转来修正，即将 1 读取为低电平，将 0 读取为高电平。R1 的作用是确保 5V 信号不存在，而 R2 限制 FET 中的电流到约 0.3mA。在大多数情况下，你应该尝试简单的分分压器，只有在它无效时才改用活动缓冲器。

## 我们能测量多快？

要找出使用 micro-bit 多快可以进行测量的最简单方法是使用忙等待（busy wait）进行脉冲宽度测量。在 P0 上施加方波，我们可以测量脉冲高电平的时间：

```cpp
#include "MicroBit.h"

MicroBit uBit;
int main()
{
  int i;
  uBit.init();
  while (1)
  {
    while (i == 1) uBit.io.P0.getDigitalValue();
    while (i == 0) uBit.io.P0.getDigitalValue();
    for (i = 0; i < 1000; i++) {
      if (i == 0) uBit.io.P0.getDigitalValue()) break;
    }
    uBit.serial.printf("%d\n\r", i);
  }
}
```

初看起来这可能有点奇怪。内部的 `while` 循环负责引导我们到达波形的正确点。我们首先循环直到电平变低，然后循环直到它再次变高，最后测量它在再次变低之前持续了多长时间。你可能认为我们只需要等待它变高，然后测量它的低电平持续多久，但这样忽略了这种可能性：当我们第一次测量时，信号可能正处于高电平期的中间。

该程序的第二个新方面是我们使用 `printf` 来获取信息。这是一个与串口驱动程序相关的打印函数。它基于标准 C 语言的 `printf` 函数，但只支持有限的数据类型。你只能使用 `%c, %d, %s, %x 和 %X`。

在这种情况下，我们使用默认的 USB 串口接口从 micro:bit 获取信息。这对于调试也很有用。要查看数据，你需要连接串口终端——例如 PuTTY。默认配置为：
波特率 = 115200
数据位 = 8 位
校验 = 无
停止位 = 1 位

你面临唯一的问题是找到正确的串口进行连接，它通常是列出的唯一 USB COM 端口。如果你找不到 COM 串口端口，你可能需要安装 mbed 串口驱动：
https://os.mbed.com/docs/mbed-os/v5.14/tutorials/windows-serial-driver.html

网页显示不应在 Windows 10 上使用，但在实践中，它已被证明对于 V1 microbit 是必要的，一旦安装，它就可以与 V2 micro:bit 工作。

如果你用不同的脉冲宽度运行此程序，结果非常规律：在图表中，循环计数位于 y 轴，脉冲时间位于 x 轴。微秒为单位的时间 $t$ 与循环计数 $n$ 的关系方程为：

![](img/23976341c9281123e7b181beea6e9dbd_52_0.png)

V1 t = 4.88 n + 3.38
V2 t = 0.85*n + 3.69

这可以低到约 10µs 或稍低。

```cpp
如果你想直接以微秒记录时间，而不是使用循环计数，你可以使用：
#include "MicroBit.h"
```

```cpp
MicroBit uBit;
int main()
{
    uBit.init();
    uint64_t t;

    volatile int i;

    while (1)
    {
        while (1 == uBit.P0.getDigitalValue());
        while (0 == uBit.P0.getDigitalValue());
        t = system_timer_current_time_us();
        for (i = 0; i < 1000; i++) {
            if (0 == uBit.P0.getDigitalValue())
                break;
        }
        t = system_timer_current_time_us() - t;
        uBit.serial.printf("%d,%d\n\r", i, (int)t);
    }
}
```

这种准确度约为 10µs。
在任何情况下，如果你尝试测量小于有效下限的脉冲宽度，你将得到像应用了更长脉冲的结果。原因很简单，micro:bit 会错过第一次跳变到零，但会检测到第二次、第三次或后续跳变。这相当于里叶变换或通用信号处理中常见的混叠效应（aliasing effect）。

## 中断

人们普遍认为，实时编程和中断是结合在一起的，如果你没有使用中断，你可能在做错。事实上，如果你正在使用中断，你可能也在做错。有些组织同意这种观点，认为中断是危险的，应该被完全禁止，这包括实时软件。

在 microbit 的情况下，我们有一套事件系统，如果你深入研究，它是可用的。
对于 GPIO 线而言，你可以使用四种设置之一来确定事件如何发生。最用的是边触发设置，当 GPIO 线从高到低或从低到高转换时触发事件。

```cpp
int eventOn(int eventType)
```

其中 eventType 是以下之一：

| 常量 | 描述 |
| :--- | :--- |
| MICROBIT_PIN_EVENT_ON | 当事件注册时，按上升沿或下降沿触发 |
| MICROBIT_PIN_ON_PULSE | 当引脚为高或低时触发 |
| MICROBIT_PIN_EVENT_TOUCH | 触摸引脚时触发 |
| MICROBIT_PIN_EVENT_NONE | 禁用该引脚的事件 |

程序的第二个新方面是我们使用 `printf` 获取信息。这是一个与串口驱动相关的打印函数。它模仿标准 C `printf` 函数，但只支持有限的数据类型。你只能使用 `%c, %d, %s, %x 和 %X`。

在这种情况下，我们使用默认的 USB 串口接口从 micro:bit 获取信息。这对于调试也很有用。要查看数据，你需要连接串口终端——例如 PuTTY。默认配置为：
波特率 = 115200
数据位 = 8 位
校验 = 无
停止位 = 1 位

这种准确度约为 10µs。
在任何情况下，如果你尝试测量小于有效下限的脉冲宽度，你将得到像应用了更长脉冲的结果。原因很简单，micro:bit 会错过第一次跳变到零，但会检测到第二次、第三次或后续跳变。这相当于里叶变换或通用信号处理中常见的混叠效应。

## 中断

人们普遍认为，实时编程和中断是结合在一起的，如果你没有使用中断，你可能在做错。事实上，如果你正在使用中断，你可能也在做错。有些组织同意这种观点，认为中断是危险的，应该被完全禁止，这包括实时软件。

在 microbit 的情况下，我们有一套事件系统，如果你深入研究，它是可用的。
对于 GPIO 线而言，你可以使用四种设置之一来确定事件如何发生。最用的是边触发设置，当 GPIO 线从高到低或从低到高转换时触发事件。

```cpp
int eventOn(int eventType)
```

其中 eventType 是以下之一：

| 常量 | 描述 |
| :--- | :--- |
| MICROBIT_PIN_EVENT_ON | 当事件注册时，按上升沿或下降沿触发 |
| MICROBIT_PIN_ON_PULSE | 当引脚为高或低时触发 |
| MICROBIT_PIN_EVENT_TOUCH | 触摸引脚时触发 |
| MICROBIT_PIN_EVENT_NONE | 禁用该引脚的事件 |

程序的第二个新方面是我们使用 `printf` 获取信息。这是一个与串口驱动相关的打印函数。它模仿标准 C `printf` 函数，但只支持有限的数据类型。你只能使用 `%c, %d, %s, %x 和 %X`。

（注：OCR 文本在末尾有一些重复/乱码部分。我将根据提供的文本块进行清晰重构。）

*自我纠正：提供的 OCR 文本在后面的页面（54-56）存在大量的重叠和重复。我将按照提供的内容流进行清理。）*

[content]
注意，这是一个反相缓冲器，但你通常可以忽略它，并在软件中通过反转来修正，即将 1 读取为低电平，将 0 读取为高电平。R1 的作用是确保 5V 信号不存在，而 R2 限制 FET 中的电流到约 0.3mA。在大多数情况下，你应该尝试简单的分压器，只有在它无效时才改用活动缓冲器。

## 我们能测量多快？

要找出使用 micro-bit 多快可以进行测量的最简单方法是使用忙等待（busy wait）进行脉冲宽度测量。在 P0 上施加方波，我们可以测量脉冲高电平的时间：

```cpp
#include "MicroBit.h"

MicroBit uBit;
int main()
{
  int i;
  uBit.init();
  while (1)
  {
    while (i == 1) uBit.io.P0.getDigitalValue();
    while (i == 0) uBit.io.P0.getDigitalValue();
    for (i = 0; i < 1000; i++) {
      if (i == 0) uBit.io.P0.getDigitalValue())
        break;
    }
    uBit.serial.printf("%d\n\r", i);
  }
}
```

初看起来这可能有点奇怪。内部的 `while` 循环负责引导我们到达波形的正确点。我们首先循环直到电平变低，然后循环直到它再次变高，最后测量它在再次变低之前持续了多长时间。你可能认为我们只需要等待它变高，然后测量它的低电平持续多久，但这样忽略了这种可能性：当我们第一次测量时，信号可能正处于高电平期的中间。

程序的第二个新方面是我们使用 `printf` 来获取信息。这是一个与串口驱动程序相关的打印函数。它基于标准 C 语言 `printf` 函数，但只支持有限的数据类型。你只能使用 `%c, %d, %s, %x 和 %X`。

在这种情况下，我们使用默认的 USB 串口接口从 micro:bit 获取信息。这对于调试也很有用。要查看数据，你需要连接串口终端——例如 PuTTY。默认配置为：
波特率 = 115200
数据位 = 8 位
校验 = 无
停止位 = 1 位

你面临唯一的问题是找到正确的串口进行连接，它通常是列出的唯一 USB COM 端口。如果你找不到 COM 串口端口，你可能需要安装 mbed 串口驱动：
https://os.mbed.com/docs/mbed-os/v5.14/tutorials/windows-serial-driver.html

网页显示不应在 Windows 10 上使用，但在实践中，它已被证明对于 V1 microbit 是必要的，一旦安装，它就可以与 V2 micro:bit 工作。

如果你用不同的脉冲宽度运行此程序，结果非常规律：在图表中，循环计数位于 y 轴，脉冲时间位于 x 轴。微秒为单位的时间 $t$ 与循环计数 $n$ 的关系方程为：

![](img/23976341c9281123e7b181beea6e9dbd_52_0.png)

V1 t = 4.88 n + 3.38
V2 t = 0.85*n + 3.69

这可以低到约 10µs 或稍低。

```cpp
如果你想直接以微秒记录时间，而不是使用循环计数，你可以使用：
#include "MicroBit.h"
```

```cpp
MicroBit uBit;
int main()
{
    uBit.init();
    uint64_t t;

    volatile int i;

    while (1)
    {
        while (1 == uBit.P0.getDigitalValue());
        while (0 == uBit.P0.getDigitalValue());
        t = system_timer_current_time_us();
        for (i = 0; i < 1000; i++) {
            if (0 == uBit.P0.getDigitalValue())
                break;
        }
        t = system_timer_current_time_us() - t;
        uBit.serial.printf("%d,%d\n\r", i, (int)t);
    }
}
```

这种准确度约为 10µs。
在任何情况下，如果你尝试测量小于有效下限的脉冲宽度，你将得到像应用了更长脉冲的结果。原因很简单，micro:bit 会错过第一次跳变到零，但会检测到第二次、第三次或后续跳变。这相当于里叶变换或通用信号处理中常见的混叠效应。

