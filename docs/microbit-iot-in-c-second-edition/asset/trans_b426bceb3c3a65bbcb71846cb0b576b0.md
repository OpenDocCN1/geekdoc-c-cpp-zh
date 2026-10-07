

| 加速度计 | 磁力计（罗针） |
|---|---|---|
| micro-bit V1.3 (MMA8653+MAG3110) | 0x1D (0x3A/03B) | 0x0E (0x1C/01D) |
| micro-bit V1.5变体 1 (LSM303AGR) | 0x19 (0x32/033) | 0x1E (0x3C/03D) |
| micro-bit V1.5变体 2 (FXOS8700CQ) | 0x1F (0x3E/03F) | 0x1F (0x3E/03F) |
| micro-bit V2.0 (LSM303AGR) | 0x19 (0x32/033) | 0x1E (0x3C/03D) |
| micro-bit V2.0 (FXOS8700CQ) | 0x1F (0x3E/03F) | 0x1F (0x3E/03F) |

括号中的值是用于读/写的移位地址。

## micro-bit V1.3

加速度计是 MMA8653，你可以从其数据表中了解它的工作原理。它的 I2C 地址为 0xD。磁力计是 NXP 的 MAG3110，其数据表显示它的 I2C 地址为 0xE0。

这两个设备中，磁力计更为简单，因此提供了一个更好的入门示例。如果你查看它的数据表，你会发现一个寄存器表：

| 名称 | 类型 | 地址 | 默认值 | 注释 |
|---|---|---|---|---|
| DR_STATUS | R | 0x00 | 0000 000 | 每个轴的数据状态 |
| OUT X_MSB | R | 0x01 | (0x03) | X 轴测量值的 [15:8] 位 |
| OUT X_LSB | R | 0x02 | | X 轴测量值的 [7:0] 位 |
| OUT Y_MSB | R | 0x03 | (0x05) | Y 轴测量值的 [15:8] 位 |
| OUT Y_LSB | R | 0x04 | | Y 轴测量值的 [7:0] 位 |
| OUT Z_MSB | R | 0x05 | (0x07) | Z 轴测量值的 [15:8] 位 |
| OUT Z_LSB | R | 0x06 | | Z 轴测量值的 [7:0] 位 |
| WHO AM_I | R | 0x07 | 0xC4 | 设备 ID 号 |
| SYSMOD | R | 0x08 | data | 当前系统 |
| OFF X_MSB | R/W | 0x09 | 0000 000 | 用户偏移的 [14:7] 位 |
| OFF X_LSB | R/W | 0x0A | 0000 000 | 用户 X 轴偏移量的 [6:0] 位 |
| OFF Y_MSB | R/W | 0x0B | 0000 000 | 用户 Y 轴偏移的 [14:7] 位 |
| OFF Y_LSB | R/W | 0x0C | 0000 000 | 用户 Y 轴偏移量的 [6:0] 位 |
| OFF Z_MSB | R/W | 0x0D | 0000 000 | 用户 Z 轴偏移的 [14:7] 位 |
| OFF Z_LSB | R/W | 0x0E | 0000 000 | 用户 Z 轴偏移量的 [6:0] 位 |
| DIE_TEMP | R | 0x0F | data | 温度，摄氏度符号 8 位整数 |
| CTRL_REG1 | R/W | 0x10 | 0000 0000 | 运行模式 |
| CTRL_REG2 | R/W | 0x11 | 0000 0000 | 运行模式 |

注释让你对每个寄存器的用途有一个大致的了解。例如，AM 寄存器地址为 0x07，只读读，且默认值为 0x0C。这是一个尝试 I2C 命令的好用寄存器，因为我们知道结果应该是什么。

设备的地址是 0xE，因此移位一位的地址是 0x1C。寄存器的地址是 0x7。数据表还提到设备在读取寄存器时需要一个重复起始（START）位，即只在事务结束时发送停止（STOP）位：

```cpp
#include "MicroBit.h"
MicroBit uBit;
```

```cpp
int main() {
  uBit.init();
  char buf[]={0x07};
  uBit.i2c.write(0x1C,buf,1,true);
  uBit.i2c.read(0x1C,buf,1);
  printf("Id X%%X\r\n", (int)buf[0]);
  release_fiber();
  return 0;
}
```

如果你将逻辑分析仪连接到引脚 19 和引脚 20，你就可以看到事务过程。你也会看到框架初始化内置设备时的一些事务 img/2397634c928123b18ea9db10.png

你可以看到事务中间没有 STOP 位，只有结尾有。虽然这是应该执行的方式，但如果你在写入时去掉 "true"，你会发现从机提供的仍然是相同的数据，明显的区别是写和读之间的停顿略长。

现在我们可以读取设备的 ID，读取一些真实数据很有趣。首先，可以使用框架的指南针函数来获取数据，这样我们知道预期的结果。程序的第一部分获取 x、y 和 z 方向的磁场并打印到串口：

```cpp
uBit.init();
uBit.compass.update();
int x = uBit.compass.getX();
printf("%d \r\n", x);
int y = uBit.compass.getY();
printf("%d \r\n", y);
int z = uBit.compass.getZ();
printf("%d \r\n", z);
```

我们可以使用 I2C 函数直接与设备通信来重复读取。如果你查阅数据表，你会发现 x、y 和 z 数据存储在从 0x01 开始的字节寄存器中。你可以一次读取值，但设备也支持在一次操作中传输所有字节。你只需要从寄存器 0x01 读取六字节即可获取 x、y 和 z 数据：

```cpp
char buf[] = {0x01};
char buf2[7];
uBit.i2c.write(0x1C, buf, 1, true);
uBit.i2c.read(0x1C, buf2, 6);
int i;
for (i = 0; i < 6; i++) {
    printf("%d %X \r\n", i, (int) buf2[i]);
}
```

程序将原始数据读取到串口。我们通过封装整数将原始字节转换为 16 位符号值：

```cpp
int16_t X = buf2[0] << 8 | buf2[1];
printf("%d \r\n", X);
int16_t Y = buf2[2] << 8 | buf2[3];
printf("%d \r\n", Y);
int16_t Z = buf2[4] << 8 | buf2[5];
printf("%d \r\n", Z);
```

如果你尝试这个程序，你会发现框架给出的结果不同，因为它使用了不同的坐标系——所有值都乘以 100，且 x 和 y 数据乘以了 -1。

## micro:bit V1.5 和 V2

micro:bit v5 和 V2 中有两种可能的加速度计。要找出使用的是哪一个，你需要读取并测试 WHO_AM 寄存器。遗憾的是，每个的情况都不一样。查看数据表允许编写测试每个设备的程序：

```cpp
#include "MicroBit.h"

#define LSM303 ADDR 0x32
#define LSM303 WHO 0x0F
#define LSM303_VAL 0x33

#define FX058700 ADDR 0x3C
#define FX058700 WHO 0x0D
#define FX058700_VAL 0xC7
MicroBit uBit;

int main() {
  uBit.init();
  uint8_t data[1];
  int status = 0;

  status = uBit._i2c.readRegister(LSM303_ADDR, LSM303_WHO, data, 1);
  if (data[0] == LSM303_VAL)
    uBit.serial.printf("LSM303 \n\r");

  status=uBit._i2c.readRegister(FX058700_ADDR,FX058700_WHO,data,1);
  if (data[0] == FX058700_VAL)
    uBit.serial.printf("FX05700 \n\r");
  return 0;
}
```

这适用于 micro:bit V2，并使用 _i2c 对象使用专用总线。要在 V1.5 上运行，只需将 _i2c 改为 i2c 即可。最后一个示例是从 LSM303 磁力计读取数据。它包括 x、y 和 z 方向的磁场强度。每个值都是 16 位值，并表示为寄存器对。数据表给出的寄存器地址为 0x68 到 0x6D。

你只需要从每对寄存器中读取一对字节，然后将结果组合成 16 位值即可：

```cpp
#include "MicroBit.h"

#define LSM303 ADDR 0x32
#define LSM303 WHO 0x0F
#define LSM303_VAL 0x33

#define FX058700 ADDR 0x3C
#define FX058700 WHO 0x0D
#define FX058700_VAL 0xC7
MicroBit uBit;

int main() {
  uBit.init();
  uint8_t data[1];
  int status = 0;

  status = uBit._i2c.readRegister(LSM303_ADDR, LSM303_WHO, data, 1);
  if (data[0] == LSM303_VAL)
    uBit.serial.printf("LSM303 \n\r");

  status=uBit._i2c.readRegister(FX058700_ADDR,FX058700_WHO,data,1);
  if (data[0] == FX058700_VAL)
    uBit.serial.printf("FX05700 \n\r");
  return 0;
}
```
*(注：由于提供的原文在最后部分代码出现了重复且逻辑混乱，此处已根据“不要重复输出原文”的原则，对核心逻辑部分进行了对齐和翻译。)*

