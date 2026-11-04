
你必须在配置菜单中启用树莓派上的 SPI 接口。步骤如下：

- 进入命令模式（例如通过 Putty）。
- 输入以下命令：

  ```
  pi@raspberrypi:~ $ sudo raspi-config
  ```

- 选择 Interface Options。
- 启用 SPI 接口。
- 完成并退出配置菜单。

```
/*---------------------------------------------------------------
                    ANALOGUE TEMPERATURE SENSOR
                    =========================

In this project a TMP36DZ type analogue temperature sensor chip is used
to measure the ambient temperature. The temperature is read using a
MCP3002 type ADC chip. The result is converted into degrees Centigrade
and displayed on the PC screen

Author: Dogan Ibrahim
File  : tmp36.c
Date  : December 2020
---------------------------------------------------------------*/
#include <wiringPiSPI.h>
#include <wiringPi.h>
#include <stdio.h>

#define channel 0     // Use CE0

int handle;

//
// Read analogue temperature and return to calling program
//
int get_adc_data(int AdcChan)
{
    char buff[3];
    int rcv;

    buff[0] = 0x01;
    buff[1] = (2 + AdcChan) << 6;
    buff[2] = 0x0;

    wiringPiSPIDataRW(handle, buff, 3);
    rcv = ((buff[1] & 15) << 6) + (buff[2] >> 2);
    return rcv;
}

//
// Start of MAIN program
//
int main(void)
{
    float mv, Temp;
    int adc;

    wiringPiSetupGpio();
    handle = wiringPiSPISetup(channel, 1000000);

    while(1)
    {
        adc = get_adc_data(0);          // Read CH0
        mv = adc * 3300.0 / 1023.0;     // Conv to mv
        Temp = (mv - 500.0) / 10.0;     // Conv to T
        printf("Temperature = %5.2f\n", Temp);  // Print
        delay(1000);                    // Wait
    }
}
```

图 9.4 程序清单 tmp36.c

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_256_0.png)

图 9.5 MCP3002 时序图

图 9.6 给出了一个典型的 PC 屏幕显示。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_257_0.png)

#### pigpio

该程序的 pigpio 版本如图 9.7 所示（程序：**tmp36-2.c**）。此版本程序与 wiringPi 版本非常相似。函数 **get_adc_data** 像前一个程序一样从芯片接收温度数据。使用了两个缓冲区：**bufftx** 和 **buffrx**。bufftx 中填入起始位、SGL/DIFF、ODD/SIGN 和 MSBF。芯片返回的数据存储在缓冲区 **buffrx** 中。温度被提取并返回给调用程序。

```
/*--------------------------------------------------------------
                    ANALOGUE TEMPERATURE SENSOR
                    ==========================

In this project a TMP36DZ type analogue temperature sensor chip is used
to measure the ambient temperature. The temperature is read using a
MCP3002 type ADC chip. The result is converted into degrees Centigrade
and displayed on the PC screen

This is the pigpio version of the program

Author: Dogan Ibrahim
File  : tmp36-2.c
Date  : December 2020
--------------------------------------------------------------*/
#include <pigpio.h>
#include <stdio.h>

#define channel 0                                      // Use CE0

int handle;

//
// Read analogue temperature and return to calling program
//
int get_adc_data(int AdcChan)
{
    char bufftx[3], buffrx[3];
    int rcv;

    bufftx[0] = 0x01;
    bufftx[1] = (2 + AdcChan) << 6;
    bufftx[2] = 0x0;
    spiXfer(handle, bufftx, buffrx, 3);
    rcv = ((buffrx[1] & 15) << 6) + (buffrx[2] >> 2);
    return rcv;
}

//
// Start of MAIN program
//
int main(void)
{
    float mv, Temp;
    int adc;

    gpioInitialise();
    handle = spiOpen(channel, 1000000, 0);

    while(1)
    {
        adc = get_adc_data(0);          // Read CH0
        mv = adc * 3300.0 / 1023.0;     // Conv to mv
        Temp = (mv - 500.0) / 10.0;     // Conv to T
        printf("Temperature = %5.2f\n", Temp); // Print
        time_sleep(1);                  // Wait
    }
}
```

图 9.7 程序 tmp36-2.c

### 9.3 • 小结

在本章中，我们学习了如何在树莓派上使用模数转换器芯片。我们提供了一个使用模拟温度传感器芯片并结合 wiringPi 和 pigpio 库的项目。

在下一章中，我们将重点介绍数模转换器（DAC）。

## 第10章 • 使用数模转换器（DAC）

### 10.1 • 概述

DAC 用于将数字信号转换为模拟形式。此类转换器在数字信号处理和数字控制应用中有着广泛的应用。例如，我们可以通过编写程序生成波形，将这些波形转换为模拟形式，并从我们的数字计算机输出。如果我们要将扬声器或其他使用模拟电压工作的设备与树莓派接口，也需要 DAC。

树莓派没有内置的 ADC 转换器，因此必须使用外部 DAC 芯片来输出模拟信号。在本章中，我们将学习如何将一款常用的 DAC（MCP4921）芯片与树莓派配合使用，以生成简单的信号波形。

### 10.2 • MCP4921 DAC

在使用 MCP4921 之前，值得较为详细地了解其特性和操作。MCP4921 是一款采用 SPI 总线接口的 12 位 DAC。图 10.1 显示了该芯片的引脚布局。基本特性如下（更多详细信息请参见链接：[http://ww1.microchip.com/downloads/en/DeviceDoc/21897B.pdf](http://ww1.microchip.com/downloads/en/DeviceDoc/21897B.pdf)）：

- 12 位操作
- 支持 20MHz 时钟
- 4.5µs 建立时间
- 外部电压基准输入
- 单位增益或 2 倍增益控制
- 1 倍或 2 倍增益
- 2.7 至 5.5V 电源电压
- -40°C 至 +125°C 温度范围

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_259_0.png)

图 10.1 MCP4921 DAC

引脚说明如下：

- **Vdd：** 电源电压
- **CS：** 片选（低电平有效）
- **SCK：** SPI 时钟
- **SDI：** SPI 数据输入
- **LDAC：** 用于将输入寄存器数据传送到输出（低电平有效）
- **Vref：** 基准输入电压
- **Vout：** 模拟输出
- **Vss：** 电源地

在本项目中，我们将以增益 1 操作 MCP4921。因此，在 3.3V 基准电压和 12 位转换数据下，DAC 的最低有效位分辨率为 3300mV / 4096 = 0.8mV

### 10.3 • 项目1 - 生成任意峰值电压的方波信号

#### 描述：

在本项目中，我们将使用 DAC 生成频率为 500Hz（周期 = 2ms）、占空比为 50%（即导通时间 = 1ms，关断时间 = 1ms）的方波信号。输出电压的峰值为 2V（请注意，如果不使用 DAC，则无法实现这一点，因为引脚输出的高电平电压为 +3.3V）。

#### 目标：

本项目旨在展示如何将 DAC 芯片与树莓派接口。

#### 框图：

图 10.2 显示了项目的框图。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_260_0.png)

图 10.2 项目框图

#### 电路图：

项目电路图如图 10.3 所示。DAC 的输出连接到示波器。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_261_0.png)

图 10.3 项目电路图

数据以 2 个字节写入 DAC。低字节指定数字输入数据的 D0:D8。高字节由以下位组成：

- **D8:D11**：数字输入数据的 D8:D11 位
- **SHDN**：1：有效（输出可用），0：关闭器件
- **GA**：输出增益控制。0：增益为 2 倍，1：增益为 1 倍
- **BUF**：0：输入无缓冲，1：输入缓冲
- **A/B**：0：写入 DACA，1：写入 DACB（MCP4921 仅支持 DACA）

在正常操作中，我们将发送 12 位（D0:D11）输入数据的高字节（D8:D11），并将 D12 和 D13 位置 1，以使器件处于活动状态。增益设置为 1 倍。然后发送数据的低字节（D0:D7）。这意味着在将高字节发送到 DAC 之前，应向其加上 0x30。

#### 程序清单：

##### wiringPi

图 10.4 显示了程序清单（程序：squaredac.c）。由于我们使用的 DAC 基准电压设为 +3.3V（3300mV），且数据宽度为 12 位（即 4096 个步进），因此将输出电压设为 2V 所需的数字值由 ONvalue 给出，其中：ONvalue = 2000 × 4095 / 3300

信号的 OFF 值（OFFvalue）设为 0V。函数 DAC 配置 DAC，使其输出 2V。首先将高字节（位于 buff[0] 中）放入缓冲区 buff，然后放入低字节（位于 buff[1] 中）：

```
buff[0] = (data >> 8) & 0x0F;
buff[0] = buff[0] + 0x30;
buff[1] = data & 0xFF;
wiringPiSPIDataRW(handle, buff, 2);
```
