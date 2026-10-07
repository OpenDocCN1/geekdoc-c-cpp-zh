
要使用 Hold（保持）主模式读取温度，你只需发送 0xE3 并读取三个字节：

```cpp
#include "MicroBit.h"
MicroBit uBit;

int main() {
    uBit.init();
    uint8_t buf[3] = {0};
    uBit.i2c.readRegister(0x80, 0xE3, buf, 3);
    uint8_t msb=buf[0];
    uint8_t lsb=buf[1];
    uint8_t check=buf[2];
    uBit.serial.printf("msb %d\n lsb %d\n checksum %d\n\r",
    msb, lsb, check);

    return 0;
}
```

缓冲区被解包到三个具有更有意义名称变量中：
msb - 高位字节；lsb - 低位字节；check - 校验和。

你应该看到类似这里的内容：

- msb 97
- lsb 232
- checksum 217

温度在 20°C 左右。

逻辑分析仪揭示了发生了什么。首先，我们发送标准的地址帧并写入 0xE3。然后经过一个短脉冲，发送了读取地址帧，设备将时钟线拉低（下方迹线）：

![](img/23976341c9281123e7b181beea6e9dbd_113_0.png)

时钟线被设备保持低位超过 42ms，期间它在准备数据。随后它被释放并发送了三个数据帧：

| +500us | | +600us | | +700us | | +800us |
|---|---|---|---|---|---|
| | 0x62 + ACK | | 0x7C + ACK | | 0x09 + NAK | |

此响应位于逻辑分析仪轨迹的非常靠下的位置，请继续向下滚动直到找到它。

虽然时钟拉伸（clock stretching）是最简单的方法，但它在某些从主组合上可能不起作用。

最后，我们必须找到如何使用无 Hold 模式或轮询方法来读取数据。这有时很有用，尽管在 micro:bit 上并非如此。在这种情况下，我们不能使用读取字节数据命令，因为数据尚未准备好读取，且主设备不会强制等待。我们必须使用两步法：发送命令并读取数据：

```cpp
char buf[4] = {0xF3};
uBit.i2c.write(0x80, buf, 1);
while (uBit.i2c.read(0x80, buf, 3) == MICROBIT_I2C_ERROR){};
```

理论上，这会不断轮询直到数据返回。在实践中，它并不有效。原因是硬件在检测到 NAK 时会重置 I2C 总线并重试。框架试图通过重置 I2C 总线并重试来补偿这一点。结果是数据丢失。

简而言之，你不能 micro:bit 上使用轮询。

# 处理数据

我们的下一个任务实际上并不与使用 I2C 总线的问题直接相关，但它是非常典型的下一步。设备返回三个字节的数据，但这些数据与温度的关系并不简单。

如果你阅读数据手册，会发现温度数据是当前通过组合高位和低位字节并将低两个位清零得到的 14 位值。低两个位用作状态位 - 位 0 目前未使用，如果数据是温度测量则位 1 为 0，如果是湿度测量则为 1。

为了合并两个字节，我们使用：

```cpp
unsigned int data6=((unsigned int) msb << 8) |
(lsb & 0xFC);
```

这清零了低两个位，将 msb 左移八位并将两者进行 OR 操作。结果是一个低两位为零的温度值。

现在我们有了原始温度值，但仍需转换为单位。数据手册给出的温度（°C）公式为：
-46.8 + 175.72 * data16 / 2^16

唯一的问题是计算 2^16。你可以通过表达式 `1<<x` 计算 2^16。这得到：

```cpp
float temp = (float)(-46.8 + (175.72 * data16)/(1<<16));
```

由于 2^16 是一个常量（65536），使用以下方法效率更高：

```cpp
float temp = (float)(-46.8 +(175.72 * data16)/(65536);
```

注意浮点运算的使用。micro:bit 处理器没有硬件浮点单元，框架带有软件实现。浮点运算很慢，通常将其转换为比例整数运算。在这种情况下使用浮点很方便，但有一个障碍：`printf` 函数不支持浮点。有一个支持的版本，但需要导入。

总的来说，使用比例整数更容易 - 在这种情况下将温度乘以 100，利用除以 2^16 等于右移：

```cpp
int temp= -4685 + ((17572*data16)>>16);
```

现在我们要做的的是以正确的比例值打印温度：

```cpp
printf("Temperature %d.%d C \n", temp/100, temp%100);
```

最终程序：
```cpp
#include "MicroBit.h"
MicroBit uBit;

int main() {
	uBit.init();
	uint8_t buf[3] = {0};
	uBit.i2c.readRegister(0x80, 0xE3, buf, 3);
	uint8_t msb = buf[0];
	uint8_t lsb = buf[1];
	uint8_t check = buf[2];

	unsigned int data16 = ((unsigned int)msb << 8) | ((unsigned int)lsb & 0xFC);
	int temp = -4685 + ((17572 * data16) >> 16);
	uBit.serial.printf("Temperature %d.%d C \n", temp / 100, temp % 100);

	return 0;
}
```

# 读取湿度

I2C 和特定设备的优点在于它变得更容易。一旦学会了如何处理一个设备，这种技能就可以通用，设备的其他方面通常是类似的。

读取湿度可以使用相同的程序，只需要更改命令和最终百分比湿度的公式。读取三个数据字节所需的命令是 0xE5，将16 位值转换为百分比湿度（RH）的公式为：

```cpp
-600 + 12500 * data16 / 2^16
```

如果我们处理 RH*100，这可以通过整数运算实现。

将所有内容整合并重用之前程序中的变量，我们得到：

```cpp
uBit.i2c.readRegister(0x80, 0xE5, 3);
msb = buf[0];
lsb = buf[1];
check = buf[2];
uBit.serial.printf("\nmsb %d \nlsb %d \nchecksum %d \n\r", msb, lsb, check);
data16 = ((unsigned int)msb << 8) | (unsigned int) (lsb & 0xFC);
int hum = -600 + (12500 * data16) >> 16;
uBit.serial.printf("Humidity %d %% %d \n", hum / 100, hum % 100);
```

程序中唯一特殊的部分是使用 `%%` 打印单个字符 - 这是必要的，因为 `%%` 在 `printf` 中有特殊含义。

# 校验和计算

虽然计算校验和或循环冗余校验（CRC，用于检测原始数据的意外变化并非 I2C 特有），但它是另一项常见任务。数据手册解释了用于 CRC 的多项式：

X^8+X^3+X^4+X+1

一旦获取了这些信息，你就可以通过写二进制数来计算除数，在多项式中对应 X 幂的每个位置写 1，即第 8 位、第5 位、第4 位和第 1 位。因此除数为 0x031。

接下来的操作对于所有 CRC 来说大致相同。首先，将用于计算校验和的数据与校验和值一起放在低位部分：

```cpp
uint32_t data32 = ((uint32_t)msb << 16) |
(uint32_t) lsb << 8)|(uint32_t) check;
```

现在 32 位变量中有了三个字节，即 24 位。

接下来，调整除数，使其最高非零位与最高位对齐。一旦数据和除数对齐，你就可以遍历高位。对于每一位，检查它是否为 1 - 进行异或运算：

```cpp
uint32_t divisor = 0x031 << 15;
for (int i = 0; i < 16; i++){
    if(data32 & (uint32_t)1<<(23 - i))data32 ^= divisor;
    divisor >>= 1;
}
```

循环结束后，如果没有错误，data32 应为 0。

一个带有优化的计算校验和完整函数：

```cpp
uint8_t crcCheck(uint8_t msb, uint8_t lsb, uint8_t check){
    uint32_t data32=((uint32_t)msb << 16) |
    ((uint32_t)lsb << 8)|((uint32_t) check;
    uint32_t divisor = 0x031 << 15;
    for (int i = 0; i < 16; i++){
        if(data32 & (uint32_t)1<<(23 - i))data32 ^= divisor;
        divisor >>= 1;
    }
    return (uint8_t)data32;
}
```

除非 I2C 总线过载或受到大量噪声影响，否则很少出现 CRC 错误。

