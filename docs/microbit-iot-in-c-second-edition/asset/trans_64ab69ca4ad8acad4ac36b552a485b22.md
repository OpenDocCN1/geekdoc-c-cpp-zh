
其中 x 表示不确定，b9 根据数据第九位的值为 0 或 1。剩余的 9 位将在接下来的九个时钟脉冲响应中返回，你必须传输三个字节才能获取所有 10 位数据。这使得以 8 位为块读取数据变得非常混乱。

数据表手册建议了一种不同的处理方法，可以将数据整齐地封装在三个字节中。它建议的方法是发送单个字节：

00000001

从机会同时传输随机数据，这些数据会被忽略。最后的 1 被视为起始位。如果你现在传输第二个字节，其中最高有效位表示单端模式或差分模式，后跟一个三位地址，其余位设为零，那么从机将返回空空位和转换结果的高两个位。现在你只需要获取最终的 8 位数据进行读取即可：

| MCU 发送数据 | | | | | | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| n (与时钟下降沿对齐) | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | | | | |
| MCU 接收数据 (与时钟上升沿对齐) | ? | ? | ? | ? | ? | ? | ? | ? | D2 | D1 | D0 | X | X | X | X |
| X = "忽略" | | | | | | | | | 87 | 86 | 85 | 84 | 83 | 82 | 81

![](img/23976341c9281123e7b181beea6e9dbd_172_0.png)

你可以采用数据手册描述的第一种方法，但这种方法得到的两个字节包含数据，且所有低位都处于正确的位置。

利用这些信息，我们可以编写读取特定通道的指令。例如，要读取通道 0，我们首先发送一个设置为 0x01 的字节作为起始位，并忽略从机的传输。我们发送 0x80 来选择单端模式，通道 0 保留从机返回的高两个位。最后，我们发送一个零字节以便从从机获取低位。对于 microbit V1，使用之前提供的 SPITransfer 函数如下：

```c
uint8_t buf[] = {0x01, 0x00, 0x00};
uint8_t readBuf[3];
CS.setDigitalValue(0);
SPITransfer(buf, 3, readBuf, 3);
CS.setDigitalValue(1);
```

注意 CS 线在整个事务期间保持低电平。

对于 microbit V2，SPITransfer 的调用已改为：
pi.transfer(buf, 3, readBuf, 3);
uBit.sleep(1);

sleep 是保持 CS 线足够长时间的一种粗略方法。更好的解决方案是使用回调函数——参见之前的

为了从 readBuf 中提取数据，我们需要进行一些位操作：
data=((int)readBuf[1])<<8|(int)readBuf[2];

表达式的第一部分从从机发送的第一个字节中提取低三位，由于这些是最高有效位，它们被向左移动八位。然后将剩余位与它们进行 OR 运算，以得到完整的 10 位结果。假设 V_REF 为 3.3V，转换为电压：
int volts=data*330/1023;

注意，我们通过处理 volts*100 避免了浮点数运算。

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
