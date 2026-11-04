
| GPIO 引脚 | wiringPi 引脚 | 物理引脚 |
|---|---|---|
| 11（MSB） | 14 | 23 |
| 9 | 13 | 21 |
| 10 | 12 | 19 |
| 22 | 3 | 15 |
| 27 | 2 | 13 |
| 17 | 0 | 11 |
| 3 | 9 | 5 |
| 2（LSB） | 8 | 3 |
| 14 | 15 | 8（按钮） |

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_129_0.png)

图 5.14 项目框图

## 电路图：

项目电路图如图 5.15 所示。8 个 LED 通过 470 欧姆限流电阻连接到 GPIO 端口。请注意，按钮可以通过两种不同方式连接到 GPIO 端口。在图 5.16 中，按钮输出为逻辑 1，按下按钮时变为逻辑 0。在图 5.17 中，按钮输出为逻辑 0，按下按钮时变为逻辑 1。本示例使用第二种方法。因此，GPIO 引脚通常为逻辑 0，按下按钮时变为逻辑 1。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_0.png)

图 5.15 项目电路图

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_1.png)

图 5.16 按钮常态为逻辑 1

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_2.png)

图 5.17 按钮常态为逻辑 0

## 程序清单：

### wiringPi

项目程序清单如图 5.18 所示（程序：**UpDown.c**）。

```
/*---------------------------------------------
BINARY UP/DOWN COUNTER
======================
In this program 8 LEDs are connected to GPIO ports through current
limiting resistors. Additionally, a button is used. The program counts
up/down in binary every 500ms. By default it counts up. When the
button is pressed it counts down as long as the button is kept pressed

Author: Dogan Ibrahim
File : UpDown.c
Date : December 2020
-------------------------------------------------------------*/

#include <wiringPi.h>
#include <stdlib.h>

#define OFF LOW
#define ON HIGH
#define Button 15        // GPIO 14
#define UP 0
#define DOWN 1

int LEDs[] = {14, 13, 12, 3, 2, 0, 9, 8};     // GPIO 11,9,10,22,27,17,3,2

//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
    char k;
    for(k = 0; k < 8; k++)
    {
        pinMode(LEDs[k], OUTPUT);
        digitalWrite(LEDs[k], OFF);
    }
    pinMode(Button, INPUT);
}

//
// Display data on ports
//
void Display(unsigned int No, unsigned int L)
{
    unsigned int j, i, m, p, r;
    m = L - 1;
    for(i = 0; i < L; i++)
    {
        j = 1;
        for(p = 0; p <= m; p++) j *= 2*j;           // Power of 2
        r = No & j;
        if(r > 0) r = 1;
        digitalWrite(LEDs[i], r);
        m--;
    }
}

//
// Start of MAIN program. When the button is not pressed, increment
// count. When the button is pressed, count down from the last value
//
int main(void)
{
        char j, count = 0;
        char Button_State;

        wiringPiSetup();
        Configure();

        while(1)
        {
                Display(count, 8);
                Button_State = digitalRead(Button);

                if(Button_State == UP)
                {
                        if(count == 255)
                                count = 0;
                        else
                                count++;
                }
                else if(Button_State == DOWN)
                {
                        if(count == 0)
                                count = 255;
                        else
                                count--;
                }
                delay(500);
        }
}
```

图 5.18 程序 UpDown.c

程序开始时，建立一个名为 LEDs 的数组，用于存储项目中使用的 LED 的端口号。名称 **Button** 分配给 GPIO 端口 14，名称 **UP** 和 **DOWN** 分别分配给 0 和 1。全局变量 **count** 初始化为零。然后，将连接 LED 的 GPIO 端口配置为输出端口，并将连接 **Button** 的 GPIO 端口配置为输入端口。在主程序中，调用函数 **Display**，并将 **count** 作为参数传入。然后读取 **Button** 的状态：如果 **Button** 未被按下（**Button_State** 等于 **UP**），则执行向上计数。另一方面，如果 **Button** 被按下（**Button_State** 等于 **DOWN**），则执行向下计数。注意，变量 **count** 在计数结束时复位。也就是说，在向上计数期间，当计数达到 255 时，在下一个周期复位为 0。类似地，在向下计数期间，当计数达到 0 时，在下一个周期复位为 255。你可以通过修改以下两条语句，在此程序中使用 GPIO 编号：

```
~~~
int LEDs[] = {11, 9, 10, 22, 27, 17, 3, 2};

and

wiringPiSetupGpio()
~~~
```

### pigpio

项目的 pigpio 程序如图 5.19 所示（程序：UpDown2.c）。该程序与 wiringPi 版本相同，只有少量小修改。

```
~~~c
/*----------------------------------------------------------------------
                    BINARY UP/DOWN COUNTER
                    =======================
In this program 8 LEDs are connected to GPIO ports through current
limiting resistors. Additionally, a button is used. The program counts
up/down in binary every 500ms. By default it counts up. When the
button is pressed it counts down as long as the button is kept pressed

In this version of the program the pigpio library is used

Author: Dogan Ibrahim
File : UpDown2.c
Date : December 2020
----------------------------------------------------------------------*/

#include <pigpio.h>
#include <stdio.h>

#define OFF 0
#define ON 1
#define Button 14
#define UP 0
#define DOWN 1

int LEDs[] = {11, 9, 10, 22, 27, 17, 3, 2};
~~~
//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
    char k;
    for(k = 0; k < 8; k++)
    {
        gpioSetMode(LEDs[k], PI_OUTPUT);
        gpioWrite(LEDs[k], OFF);
    }
    gpioSetMode(Button, PI_INPUT);
}

//
// Display data on ports
//
void Display(unsigned int No, unsigned int L)
{
    unsigned int j, i, m, p, r;
    m = L - 1;
    for(i = 0; i < L; i++)
    {
        j = 1;
        for(p = 0; p < m; p++)j = 2*j;
// Power of 2
        r = No & j;
        if(r > 0) r = 1;
        gpioWrite(LEDs[i], r);
        m--;
    }
}

//
// Start of MAIN program. When the button is not pressed,increment
// count. When the button is pressed, count down from the last value
//
int main(void)
{
    char j, count = 0;
    char Button_State;

    gpioInitialise();
    Configure();

while(1)
{
        Display(count, 8);
        Button_State = gpioRead(Button);

        if(Button_State == UP)
        {
                if(count == 255)
                        count = 0;
                else
                        count++;
        }
        else if(Button_State == DOWN)
        {
                if(count == 0)
                        count = 255;
                else
                        count--;
        }
        time_sleep(0.5);
}
```

图 5.19 程序 UpDown2.c

## 5.6 • 项目 5 – LED 骰子

### 描述：

这是一个基于 LED 和按钮开关的简单骰子项目。LED 的排列方式模拟真实骰子各面的外观。按下按钮开关时，会生成一个 1 到 6 之间的随机数并显示在 LED 上。通常所有 LED 均熄灭，表示系统已准备好生成新的骰子点数。3 秒后，LED 再次熄灭。

### 目标：

本项目旨在展示如何设计一个基于 LED 的骰子。

### 框图：

图 5.20 展示了项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_136_0.png)

图 5.20 项目框图

如图 5.21 所示，LED 的排列方式使其点亮时能够像真实骰子一样表示数字。项目的工作过程如下：通常所有 LED 均熄灭，表示系统已准备好生成新的骰子点数。按下开关会生成一个 1 到 6 之间的随机骰子点数，并在 LED 上显示 3 秒。3 秒后，LED 再次熄灭。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_136_1.png)

图 5.21 LED 骰子

### 电路图：

项目电路图如图 5.22 所示。7 个 LED 通过 470 欧姆限流电阻连接到 GPIO 引脚 9、10、22、27、17、3 和 2。连接如下：

| LED | GPIO 引脚 | wiringPi 引脚 | 物理引脚 |
|---|---|---|---|
| D1 | 9 | 13 | 21 |
| D2 | 10 | 12 | 19 |
| D3 | 22 | 3 | 15 |
| D4 | 27 | 2 | 13 |
| D5 | 17 | 0 | 11 |
| D6 | 3 | 9 | 5 |
| D7 | 2 | 8 | 3 |

按钮开关通过 10K 下拉电阻连接到 GPIO 引脚 14，因此按钮输出为逻辑 0，按下按钮时变为逻辑 1。
