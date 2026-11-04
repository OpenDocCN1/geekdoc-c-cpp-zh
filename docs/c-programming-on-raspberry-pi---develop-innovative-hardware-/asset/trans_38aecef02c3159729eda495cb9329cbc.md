

```c
serClose(handle);
}
```

图 11.9 程序 RPISerial2.c

## 11.4 • 小结

在本章中，我们学习了如何使用树莓派的串行通信端口。
文中给出了一个树莓派与 Arduino UNO 通信的示例项目。

在下一章中，我们将重点讨论 wiringPi 和 pigpio 库的其他各种有用且重要的函数。

## 第 12 章 • wiringPi 的其他有用函数

### 12.1 • 概述

在上一章中，我们学习了如何将串行设备连接到树莓派，并使用 wiringPi 和 pigpio 库对串行端口进行编程。wiringPi 库还包含一些非常非常有用的附加函数。在本章中，我们将通过简单的项目来了解如何使用这些函数。

### 12.2 • 项目 1 – 使用外部中断 – 事件计数器

#### 描述：

外部中断是所有微控制器非常重要的特性，因为它们使处理器能够快速响应外部事件。当外部中断发生时，处理器会停止当前正在执行的工作，跳转到中断服务程序（ISR）来处理该中断。中断处理完成后，控制权返回主程序。

这是一个事件计数器项目，其中 GPIO 2 引脚用作事件输入。如果引脚从高电平变为低电平，则视为发生一次事件。当事件发生时，计数器加一，并将总计数显示在 PC 监视器上。在本项目中，使用一个按钮来模拟 GPIO 2 上发生的事件。

#### 电路图：

图 12.1 显示了项目的电路图。一个按钮连接到 GPIO 2。按钮状态为逻辑 1，按下按钮时为 0。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_281_0.png)

图 12.1 项目电路图

#### 程序清单：

wiringPi 库提供了以下函数来处理 GPIO 引脚上的外部中断：

```c
wiringPiISR (int pin, int edgeType, void (*function)(void));
```

这里，pin 是用于外部中断的引脚。edgeType 指定在引脚上如何识别中断。有效选项为：**INT_EDGE_FALLING**、**INT_EDGE_RISING**、**INT_EDGE_BOTH** 和 **INT_EDGE_SETUP**。每当检测到外部中断时，将调用指定的函数。如果在处理当前中断期间又发生了另一个中断，新的中断将被保存，并在当前中断处理完成后得到处理。ISR 可以完全访问程序中的所有全局变量、文件句柄等。

图 12.2 显示了程序清单（程序：**EventInt.c**）。在主程序内部，调用了函数 **wiringPiISR**，并在引脚 **Button** 上以下降沿检测方式初始化外部中断。ISR 函数名为 **MyISR**。在该例程中，变量 count 加一，并将 **flag** 置为 1。**flag** 变量在主程序循环中用于检测是否发生了中断。通过等待 **Button** 释放并在 **Button** 操作后引入短暂延迟，将接触抖动降至最低。

程序的示例输出如图 12.3 所示。

```c
/*--------------------------------------------------------------
                 EXTERNAL INTERRUPT EVENT COUNTER
                 ===============================

This is an external interrupt event counter program. A button is
connected to GPIO 2 and the state of the button is at 0. When the
button is pressed GPIO 2 goes from 1 to 0 and generates an external
interrupt. Inside the ISR a counter is incremented and the total
count is displayed on the PC screen

Author: Dogan Ibrahim
File  : EventInt.c
Date  : December 2020
--------------------------------------------------------------*/
#include <wiringPi.h>
#include <stdio.h>

#define Button 2                              // Button at GPIO 2
int count, flag;                              // Init count

//
// This is the interrupt service routine. The value of count is
// incremented by one in this routine
//
void MyISR()
{
        count++;                              // Increment count
        flag = 1;                             // Set flag
}
```

//
// 主程序开始
//
int main(void)
{
    wiringPiSetupGpio();
    count = 0;
    flag = 0;
    pullUpDnControl(Button, PUD_UP);
    wiringPiISR(Button, INT_EDGE_FALLING, &MyISR);

    while(1)
    {
        if(flag == 1)
        {
            flag = 0;
            printf("count = %d\n", count);
            while(digitalRead(Button) == 0);
            delay(20);
        }
    }
}
```

图 12.2 程序 EventInt.c

```
pi@raspberrypi:~$ gcc -o Event EventInt.c -lwiringPi
pi@raspberrypi:~$ sudo ./Event
count = 1
count = 2
count = 3
count = 4
count = 5
count = 6
count = 7
count = 8
count = 9
```

图 12.3 程序示例输出

#### 修改后的程序：

图 12.1 中的电路图可以通过移除上拉电阻并在软件中上拉引脚来简化。wiringPi 函数 pullUpDnControl 用于在软件中将 I/O 引脚上拉/下拉。该函数的第一个参数是引脚名称。第二个参数指定上拉（PUD_UP）或下拉（PUD_DOWN）。修改后的电路图和程序清单（程序：EventInt2.c）分别如图 12.4 和图 12.5 所示。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_284_0.png)

图 12.4 修改后的电路图

```c
/*---------------------------------------------------------------
                    EXTERNAL INTERRUPT EVENT COUNTER
                    ================================

This is an external interrupt event counter program. A button is
connected to GPIO 2 and the state of the button is at 0. When the
button is pressed GPIO 2 goes from 1 to 0 and generates an external
interrupt. Inside the ISR a counter is incremented and the total
count is displayed on the PC screen

In this version of the program software pull-up is used

Author: Dogan Ibrahim
File  : EventInt2.c
Date  : December 2020
---------------------------------------------------------------*/
#include <wiringPi.h>
#include <stdio.h>

#define Button 2                              // Button at GPIO 2
int count, flag;                              // Init count

//
// This is the interrupt service routine. The value of count is
// incremented by one in this routine.
//
void MyISR()
{
        count++;                              // Increment count
        flag = 1;                             // Set flag
}

//
// Start of MAIN program
//
```

```c
//
int main(void)
{
        wiringPiSetupGpio();
        count = 0;
        flag = 0;

        pullUpDnControl(Button, PUD_UP);        // Software pull-up
        wiringPiISR(Button, INT_EDGE_FALLING, &MyISR);

        while(1)
        {
                if(flag == 1)
                {
                        flag = 0;
                        printf("count = %d\n", count);
                        while(digitalRead(Button) == 0);
                        delay(20);
                }
        }
}
```

图 12.5 程序 EventInt2.c

### 12.3 • 项目 2 – 使用音调库 – 生成 1kHz 信号

#### 描述：

wiringPi 的音调库可用于在树莓派的任何引脚上生成软件控制的方波信号，最大频率为 5kHz（5000Hz）。生成音调的频率不是非常精确，可用于在压电发声器（或无源蜂鸣器）上生成音调。

在本项目中，我们将在一个无源蜂鸣器上生成 1kHz 的音调。

#### 框图：

图 12.6 显示了项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_285_0.png)

图 12.6 项目框图

#### 电路图：

项目的电路图如图 12.7 所示。一个无源蜂鸣器连接到 GPIO 2 引脚。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_286_0.png)

#### 程序清单：

除了 **<wiringPi.h>** 之外，程序开头还必须包含头文件 **<softTone.h>**。提供了以下函数：

**softToneCreate**：此函数创建一个由软件控制的音调引脚。必须将引脚号指定为该函数的参数。

**softToneWrite (int pin, int freq)**：此函数以指定频率生成音调。函数的第一个参数是引脚号。第二个参数是频率，单位 Hz。注意，音调会持续播放，直到频率设置为 0。

程序除了使用 **wiringPi** 库进行编译外，还必须使用 **lpthread** 库进行编译。

图 12.8 显示了程序清单（程序：**tone1.c**）。该程序非常简单，因为它调用了 wiringPi 函数来生成 1kHz 信号。程序可以按如下方式编译和运行：

```
gcc -o tone1 tone1.c -lwiringPi -lpthread
sudo ./tone1
```

