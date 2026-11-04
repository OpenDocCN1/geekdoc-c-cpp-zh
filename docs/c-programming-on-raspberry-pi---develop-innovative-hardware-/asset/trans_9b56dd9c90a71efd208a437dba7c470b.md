
```c
//
// Connections between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10

//
// Start of MAIN program
//
int main(void)
{
    int lcd;
    char CurrentDate[16], CurrentTime[12];
    struct tm* timeinfo;
    time_t timer;

    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    lcdClear(lcd);

    while(1)
    {
        time(&timer);
        timeinfo = localtime(&timer);

        strftime(CurrentDate, 16, "%d-%b-%Y", timeinfo);
        strftime(CurrentTime, 12, "%H:%M:%S", timeinfo);

        lcdPosition(lcd, 0, 0);
        lcdPuts(lcd, CurrentDate);

        lcdPosition(lcd, 0, 1);
        lcdPuts(lcd, CurrentTime);
        delay(1000);
    }
}
```

图6.9 程序 LCDDateTime.c

## 6.8 项目6——显示温度和湿度

### 描述：

本项目使用一个 DHT11 温度和湿度传感器芯片。环境温度和湿度分别显示在 LCD 的顶行和底行。

### 目标：

本项目旨在展示如何将温度和湿度数据显示在 LCD 上。

### 框图：

图6.10展示了该项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_194_0.png)

图6.10 项目框图

### 电路图：

该项目的电路图如图6.11所示。LCD 与树莓派的连接方式与上一个项目相同。DHT11 传感器连接到 GPIO 9。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_194_1.png)

图6.11 项目电路图

### 程序清单：

### wiringPi

图6.12展示了程序清单（程序：LCDTH.c）。该程序使用 GPIO 引脚编号。读取温度和湿度的程序部分与图5.45相同。此外，数据会显示在 LCD 上。

```c
/*-----------------------------------------------------------
                    DISPLAY TEMPERATURE AND HUMIDITY ON LCD
                    ================================

In this program a DHT11 sensor chip and an LCD are connected to the
Raspberry Pi. The program displays the temperature and humidity on
the LCD

Author: Dogan Ibrahim
File  : LCDTH.c
Date  : December 2020
-----------------------------------------------------------*/

#include <wiringPi.h>
#include <stdio.h>
#include <lcd.h>

//
// Connections between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10

//
// DHT11 data pin (GPIO 9)
//
#define DHT_PIN 9

//
// This function waits for an edge change. If there is no edge
// change in 255 microseconds then the function returns 1, otherwise
// it returns 0
//
int WaitEdge(int mode)
{
    int counter = 0;
    while(digitalRead(DHT_PIN) == mode)
    {
        counter++;
        delayMicroseconds(1);
        if(counter == 255)return 1;
    }
    return 0;
}

// This function reads the temperature and humidity from DHT11
// and returns the readings to the calling program
//
void Read_DHT11(int *T, int *H)
{
    char res, i, state, counter, indx = 0;
    int data[5];

    for(i = 0; i < 5; i++)data[i] = 0;
    pinMode(DHT_PIN, OUTPUT);
    digitalWrite(DHT_PIN, LOW);
    delay(18);
    digitalWrite(DHT_PIN, HIGH);
    delayMicroseconds(40);
    pinMode(DHT_PIN, INPUT);

    res = WaitEdge(0);
    res = res * WaitEdge(1);

    i = 0;
    while(i < 80 && res == 0)
    {
        counter = 0;
        if(WaitEdge(0) == 1)break;
        while(digitalRead(DHT_PIN) == HIGH)
        {
            counter++;
            delayMicroseconds(1);
            if(counter == 255)break;
        }

        data[indx/8] <<= 1;
        if(counter > 28)data[indx/8] |= 1;
        indx++;
        i++;
    }
    //
    // Check the Checksum
    //
    if((indx >= 40) && (data[4] ==
       ((data[0] + data[1] + data[2] + data[3]) & 0xFF)))
    {
        *T = data[2];                // T = data[2].data[3]
        *H = data[0];                // H = data[0].data[1]
    }
}

//
// Start of MAIN program
//
int main(void)
{
    int Temp, Hum, lcd;

    wiringPiSetupGpio();
    delay(1000);
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);

    while(1)
    {
        Read_DHT11(&Temp, &Hum);
        lcdClear(lcd);
        lcdPosition(lcd, 0, 0);          // row 0, col 0
        lcdPrintf(lcd, "T = %d C", Temp);
        lcdPosition(lcd, 0, 1);          // row 1, col 0
        lcdPrintf(lcd, "H = %d %%", Hum);
        delay(5000);                     // 5s delay
    }
}
```

图6.12 程序 LCDTH.c

数据按以下格式显示：

**T = 22 C**

**H = 58 %**

## 6.9 小结

本章中，我们学习了如何在树莓派上使用 LCD，同时使用 wiringPi 库和 C 语言进行编程。

下一章的关键主题是 I2C（或 I²C）接口及相应库。

# 第7章 • I2C总线接口

## 7.1 概述

I2C（或 I²C）总线常用于基于微控制器的项目。本章将介绍该总线在树莓派上的使用。目的是让读者熟悉 I2C 总线库函数，并展示如何在实际项目中使用它们。在了解项目细节之前，值得先看一下 I2C 总线的基本原理。

## 7.2 I2C总线

I2C 总线是与传感器和执行器等外部设备通信时最常用的微控制器通信协议之一。I2C 总线是单主多从总线，可工作在标准模式：100 Kbit/s、全速模式：400 Kbit/s、快速模式：1 Mbit/s 和高速模式：3.2 Mbit/s。该总线由两根开漏线组成，并通过电阻上拉：

- **SDA**：数据线
- **SCL**：时钟线

图7.1展示了一个主设备和三个从设备的 I2C 总线结构。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_199_0.png)

图7.1 一个主设备和三个从设备的 I2C 总线

由于 I2C 总线仅基于两根线，因此必须有办法在同一总线上寻址单个从设备。为此，协议规定每个从设备为给定总线提供一个唯一的从地址。该地址通常为7位宽。当总线空闲时，两根线均为高电平。总线上的所有通信都由主设备发起并完成，主设备首先发送 START 位，并通过发送 STOP 位完成一次事务。这会提醒所有从设备总线上有数据即将到来。在起始位之后，发送7位唯一从地址。总线上的每个从设备都有一个地址，这确保在任意时刻只有被寻址的从设备在总线上通信，以避免冲突。最后发送的位是读/写位。如果该位为0，主设备希望向总线写入（例如写入从设备的寄存器）。如果为1，主设备希望从总线读取（例如从从设备的寄存器读取）。数据在总线上发送时最高位（MSB）在前。每个字节之后都有一个确认（ACK）位，该位允许接收方向发送方表明该字节已成功接收，从而继续发送下一个字节。ACK 位在第9个时钟脉冲发送。

I2C 总线上的通信过程如下：

- 主设备在总线上发送它想要通信的从设备地址。
- 最低位（LSB）是 R/W 位，用于确定数据传输方向，即从主设备到从设备（R/W = 0），或从从设备到主设备（R/W = 1）。
- 发送所需字节，每个字节之间插入 ACK 位，直到出现停止条件。

根据所用从设备类型，某些事务可能需要单独的事务。例如，从兼容 I2C 的存储设备读取数据的步骤如下：

- 主设备以写模式（R/W = 0）启动事务，在总线上发送从设备地址。
- 然后以两个字节发送要读取的存储位置（假设为64Kbit存储器）。
- 主设备发送 STOP 条件以结束事务
- 主设备以读模式（R/W = 1）启动新事务，在总线上发送从设备地址
- 主设备从存储器读取数据。如果以顺序格式读取存储器，则会读取多个字节。
- 主设备在总线上设置停止条件

在使用任何 I2C 设备之前，我们必须在树莓派配置中启用 I2C。步骤如下：

- 启动配置工具
- 向下移动到**接口选项**并按 **Enter**
- 选择 **I2C** 并按 **Enter** 以启用它

```bash
pi@raspberrypi:~ $ sudo raspi-config
```

在使用树莓派的 I2C 引脚之前，我们必须确保连接到树莓派的 I2C 设备能被树莓派 I2C 总线识别。搭建电路并在命令行输入以下命令，确保显示所连接设备的 I2C 地址：

```bash
pi@raspberrypi:~ $ sudo i2cdetect -y 1
```

