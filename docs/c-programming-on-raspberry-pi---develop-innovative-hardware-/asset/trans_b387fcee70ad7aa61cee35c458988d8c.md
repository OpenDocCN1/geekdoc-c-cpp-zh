
while(1)
{
    freq = rand() % 91;        // Between 0-90
    freq = freq + 10;          // Between 10-100
    duty = freq / 2;           // Duty cycle
    softPwmCreate(Buzzer, 0, freq); // Frequency
    softPwmWrite(Buzzer, duty);     // Duty cycle
    delay(250);                // 250ms delay
}

图 5.37 程序 RandomBuzzer.c

在本项目中，PWM 波形的占空比设置为 50%，频率在 100 Hz 和 1 kHz 之间变化。随机数用于生成 10 到 100 之间的随机数。这些数字用于设置 PWM 波形的频率。每次输出之间使用 250 ms 的延迟。请注意，当值为 10 时，PWM 波形的周期为 10 x 100µs = 1 ms（1 kHz）。当值为 100 时，周期为 100 x 100µs = 10 ms（100 Hz）。在本程序中，使用 GPIO 编号。

## pigpio

项目的 pigpio 程序如图 5.38 所示（程序：RandomBuzzer2.c）。在本程序中，PWM 频率与前一个程序一样在 100 Hz 和 1 kHz 之间变化。占空比设置为 50%。

/*-----------------------------------------------------------
                        RANDOM BUZZER
                        ===========
In this program a passive buzzer is connected to the Raspberry Pi
and random numbers are generated between 100 and 1000 to correspond
to frequencies. PWM waveforms are generated with these frequencies
and sent to the buzzer.

This is the pigpio version of the program

Author: Dogan Ibrahim
File  : RandomBuzzer2.c
Date  : December 2020
-----------------------------------------------------------*/

#include <pigpio.h>
#include <stdlib.h>

#define Buzzer 2

//
// Configure LED port as output
//

void Configure()
{
    gpioSetMode(Buzzer, PI_OUTPUT);     // Buzzer output
    gpioWrite(Buzzer, 0);               // Buzzer OFF
}

//
// Start of MAIN program. Generate PWM waveforms with 100 Hz to
// 1000 Hz and send to the buzzer
//
int main(void)
{
    int freq;

    gpioInitialise();
    Configure();

    while(1)
    {
        freq = rand() % 901;            // 0 - 900
        freq = 100 + freq;              // 100 - 1000
        gpioPWM(Buzzer, 128);           // Duty = 50%
        gpioSetPWMfrequency(Buzzer, freq);
        time_sleep(0.25);
    }
}

图 5.38 程序 RandomBuzzer2.c

## Suggestion:

在图 5.37 和图 5.38 中，仅频率是随机变化的。修改程序以改变占空比并观察差异。

## 5.10 • 项目 9 – 显示温度和相对湿度

### Description:

### 描述：

在本项目中，使用 DHT11 温度和相对湿度传感器芯片获取环境温度和相对湿度。读数每 5 秒在屏幕上显示一次。

### Aim:

### 目标：

本项目旨在展示如何使用 C 语言在树莓派上编程常用的 DHT11 相对湿度和温度传感器芯片。

### Block diagram:

### 框图：

图 5.39 显示了项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_159_0.png)

图 5.39 项目的框图

### Circuit diagram:

### 电路图：

在本项目中，使用 DHT11 相对湿度和温度传感器芯片。标准的 DHT11 是一个 4 引脚数字输出器件（如图 5.40 所示，仅使用 3 个引脚），具有 +V、GND 和 Data 引脚。Data 引脚必须通过 10K 电阻上拉至 +V。芯片使用电容式湿度传感器和热敏电阻来测量环境温度。芯片大约每秒提供一次数据输出。DHT11 的基本特性如下：

- 3 至 5V 工作。
- 2.5mA 电流消耗（转换期间）。
- 温度读数范围为 0-50°C，精度为 ±2°C。
- 湿度读数范围为 20-80%，精度为 5%。
- 兼容面包板，引脚间距为 0.1 英寸。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_159_1.png)

图 5.40 标准 DHT11 芯片

在本示例中，使用了来自 Elektor 的内置 10K 上拉电阻的 DHT11 模块。这是一个 3 引脚器件，其引脚布局如图 5.41 所示。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_160_0.png)

图 5.42 显示了项目的电路图。DHT11 的数据输出连接到树莓派的 GPIO 2 引脚（wiringPi 引脚 8）。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_160_1.png)

### Using the DHT11

### 使用 DHT11

DHT11 传感器芯片通过单个数据引脚工作。通过向芯片施加精确的时序脉冲来提取数据。从芯片接收 5 字节（40 位）数据，2 字节湿度数据（1 字节整数，1 字节小数），2 字节温度数据（1 字节整数，1 字节小数），1 字节校验和数据。

提取温度和湿度的方法如下（此处 MCU 为树莓派）：

- 芯片上电后，应等待一秒钟让芯片稳定下来。
- MCU 将数据引脚设置为低电平，最短 18 毫秒。
- MCU 将数据引脚设置为高电平并等待 40 微秒。
- DHT11 将数据引脚拉低 80 微秒。
- DHT11 将数据引脚设置为高电平 80 微秒（图 5.43）。
- 现在，DHT11 与 MCU 之间开始数据传输。
- 低电平数据以 50 微秒的低电平后跟 26-28 微秒的高电平来识别
- 高电平数据以 50 微秒的低电平后跟 70 微秒的高电平来识别（图 5.44）
- 数据传输在接收到 40 位数据后结束。前两个字节（字节 0 和 1）表示湿度数据。接下来两个字节（字节 2 和 3）为温度数据。最后一个字节（字节 4）为校验和数据，由数据字节 0、1、2 和 3 相加然后与 0xFF 进行逻辑与运算得到。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_161_0.png)

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_161_1.png)

### Program listing:

### 程序清单：

### wiringPi

### wiringPi

项目的程序清单如图 5.45 所示（程序：**dht11.c**）。程序使用 GPIO 编号，而不是 wiringPi 编号。

/*----------------------------------------------------
                         DHT11 TEMPERATURE AND HUMIDITY
                         =============================

In this program a DHT11 sensor chip is connected to the Raspberry Pi.
The program reads and displays the temperature and the humidity
every 5 seconds on the PC screen

Author: Dogan Ibrahim
File  : dht11.c
Date  : December 2020
-----------------------------------------------------*/
#include <wiringPi.h>

#include <stdio.h>

#define DHT_PIN 2

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

//
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
        res = res + WaitEdge(1);

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

        // Check the Checksum
        if((indx >= 40) && (data[4] ==
            ((data[0]+data[1]+data[2]+data[3]) & 0xFF))
        {
            *T = data[2];              // T = data[2].data[3]
            *H = data[0];              // H = data[0].data[1]
        }
}

// Start of MAIN program
int main(void)
{
    int Temp, Hum;

    wiringPiSetupGpio();
    delay(1000);

    while(1)
    {
        Read_DHT11(&Temp, &Hum);
        printf("T=%d C  H=%d %%\n", Temp, Hum);
        delay(5000);          // 5s delay
    }
}

图 5.45 程序 dht11.c

函数 Read_DHT11 从 DHT11 芯片读取温度和湿度。在该函数的开始处，整数数组 data 初始化为 5 个元素。该数组用于存储温度、湿度和校验和数据。该数组被清零为 0，引脚
