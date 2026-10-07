

```cpp
int16 t humidity = (byte1 << 8) | byte2;
int16 t temperature = (byte3 << 8) | byte4;
if (temperature & 0x8000)
    temperature = -(temperature % 0x7FFF);
uuBit.serial.printf("Checksum %X %X\n", byte5,
    (byte1 + byte2 + byte3 + byte4) & 0xFF);
uuBit.serial.printf("Humidity %d.%d\n",
    humidity / 10, abs(humidity % 10));
uuBit.serial.printf("Temperature %d.%d\n",
    temperature / 10, abs(temperature % 10));

char buff[10];
sprintf(buff, "%d%%d%%", humidity / 10, abs(humidity % 10));
uuBit.display.scroll(buff, 200);
sprintf(buff, "%hd.%dC", temperature / 10,
    abs(temperature % 10));
uuBit.display.scroll(buff, 200);
uuBit.sleep(2500);
```

显然，这段代码需要重构为一个函数，该函数接受设备连接的引脚并返回湿度和温度。
DHT11/22 是一种实用的设备，但在低成本温度测量方面，DS18D20 是一个非常受欢迎的选择，而且更准确。

# 总结

- DHT22 是一种廉成本温湿度传感器。
- 它使用一种自定义的单线总线，与标准的 1-Wire 总线不兼容。
- 它的异步协议易于实现所需的时序控制。
- 时序控制可能很简单，但除非关闭中断，否则很难在无错误的情况下完成单次读取。
- 使用了非常简单的校验和来检测错误。

# # 第9 章
# DS18B20 1-Wire 温度传感器

1-Wire 总线是一种专有的总线，非常容易使用，并且有很多可以连接到它的有用设备。在所有 1 线设备中，最流行的可能是 DS18B20 温度传感器——它很小、非常廉，，如果处理器支持 1-Wire 总线协议，它就非常容易使用，但 micro:bit 不支持。然而，该协议用 C 语言编写足够简单，且 micro:bit 的速度足够快，不需要额外设备即可工作。我们必须使用 C 语言；例如，Python 的速度不够快。

microbit 有内置温度传感器，但它测量的是 CPU 的温度，只能给你非常近似的空气温度。DS18B20 可以为你提供准确的温度，而且你可以拥有多个传感器。

# # 硬件

DS18B20 有多种格式，但最常见的格式看起来就像标准的 BJT（晶极管）——这在尝试寻找它时有时会带来问题。你也可以获得带有电缆的防水传感器形式的 DS18B20。无论封装如何，它都可以在 3.3V 或 5V 下工作。

![](img/23976341c9281123e7b181beea6e9dbd_136_0.png)

DS18B20 的基本规格如下：

- 测量范围从 -55°C 到 +125°C (-67°F 到 +257°F)
- 在 -10°C 到 +85°C 之间的精度为 ±0.5°C
- 温度计分辨率用户可选，为 9 到 12 位
- 在最长 750ms 内转换为 12 位数字字

它还可以从数据线供电，使得总线在物理上只有两根线——数据线和地——然而这种“寄生电源”模式很难可靠地工作，在初始设计中最好避免。在普通供电模式下，有三个连接：

![](img/23976341c9281123e7b181beea6e9dbd_137_0.png)

地需要连接到系统地，$V_{DD}$ 连接到 3.3V，DQ 连接到开集总线的上拉电阻。

![](img/23976341c9281123e7b181beea6e9dbd_137_1.png)

总总线上可以有多个设备，每个设备都有唯一的 64 位激光 ROM 代码，可以作为地址来选择活动设备。为了简单起见，最好从单个设备开始，避免枚举总线上设备的问题，尽管一旦你了解了这一切是如何运作的，这并不难实现。

然而，我们必须解决一个问题，即输入和输出之间快速切换的需求。在没有干预的情况下，输出和输入模式之间的切换是通过系统完成的，速度较慢，大约 80µs。在某些情况下这很重要，因为协议需要主站获取数据并从从机接收数据。例如，DHT22 温湿度传感器请求处理器向其写入测量值，然后在处理器不写入任何内容的情况下发回数据，这允许使用单根 GPIO 线。

在 DS18B20 的情况下，协议略有不同。主站将总线拉低，然后拉高，最后等待从机响应。从机随后拉低总线以表示存在。主站随后切换到输入模式并从从机读取数据。数据以 16 位块发送，其中温度，下一个 16 位是湿度，最后 8 位是 CRC。

温度以补码格式发送，最高位是符号位。每个位的分辨率为 0.0625°C。

![](img/23976341c9281123e7b181beea6e9dbd_138_0.png)

# # 初始化

通信的第一步是初始化总线。主站将线拉低至少 480µs，然后拉高并等待至少 70µs。从机通过拉低总线 60µs 到 240µs 来响应。主站随后读取总线以查看从机是否响应。

```cpp
bool init() {
    bool reset = false;
    for (int i = 0; i < 10; i++) {
        pinWrite(DATA_PIN, LOW);
        delayMicroseconds(480);
        pinWrite(DATA_PIN, HIGH);
        delayMicroseconds(70);
        if (digitalRead(DATA_PIN) == LOW) {
            reset = true;
            break;
        }
    }
    return reset;
}
```

一旦总线初始化，主站就可以开始从从机请求数据。每个位通过将总线拉低 60µs 然后释放为高电平来发送。主站在高电平期间读取总线。

```cpp
int16_t readData() {
    int16_t data = 0;
    for (int i = 0; i < 16; i++) {
        pinWrite(DATA_PIN, LOW);
        delayMicroseconds(60);
        pinWrite(DATA_PIN, HIGH);
        delayMicroseconds(10);
        if (digitalRead(DATA_PIN) == HIGH) {
            data |= (1 << i);
        }
    }
    return data;
}
```

这是通信协议的简化版本。在实际应用中，你将需要处理 CRC 检查和协议的其他细节。

