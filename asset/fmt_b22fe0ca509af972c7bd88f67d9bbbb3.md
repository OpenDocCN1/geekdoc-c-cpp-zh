
`Adafruit_NeoPixel(unsigned int numberOfPixels, byte pinNumber, byte flags)`

其中

`numberOfPixels` 是控制的 NeoPixel 数量
`pinNumber` 是连接到灯串中第一个 NeoPixel 的 Arduino 引脚
`flags` 指定颜色顺序和通信速率。这些取决于所使用的 NeoPixel 类型。它们的定义如下：

- `NEO_GRB` = 先绿后红
- `NEO_RGB` = 红后蓝
- `NEO_KHZ400` = 400 千赫兹
- `NEO_KHZ800` = 800 千赫兹

示例 HT8-1.
```cpp
Adafruit_NeoPixel myPixels = Adafruit_NeoPixel(5, 6, NEO_RGB + NEO_KHZ800);
```

### 其他方法

更新整个 NeoPixel 灯串为草图中的值。在调用此方法之前，任何 NeoPixel 都不会显示颜色或亮度设置。

```cpp
void show();
```

示例 HT8-2.
```cpp
myPixels.show();
```

初始化 NeoPixels。此方法通常在 `setup()` 中调用。

```cpp
void begin();
```

Arduino™ C 编程：16 课，从 setup() 到机器人

### Arduino 输出

在调用此方法之前，任何 NeoPixel 都都不会显示颜色或亮度设置。

```cpp
void show();
```

### 设置特定的 Arduino 引脚

```cpp
void setPin(byte pin);
```

其中

`numberOfPixels` 是控制的 NeoPixel 数量

`pinNumber` 是连接到灯串中第一个 NeoPixel 的 Arduino 引脚

`flags` 指定了颜色顺序和通信速率。这些取决于所使用的 NeoPixel 类型。它们的定义如下：

- `NEO_GRB` = 先绿后红
- `NEO_RGB` = 红后蓝
- `NEO_KHZ400` = 400 千赫兹
- `NEO_KHZ800` = 800 千赫兹

示例 HT8-1.
```cpp
Adafruit_NeoPixel myPixels = Adafruit_NeoPixel(5, 6, NEO_RGB + NEO_KHZ800);
```

### 其他方法

更新整个 NeoPixel 灯串为草图中的值。在调用此方法之前，任何 NeoPixel 都都不会显示颜色或亮度设置。

```cpp
void show();
```

示例 HT8-2.
```cpp
myPixels.show();
```

初始化 NeoPixels。此方法通常在 `setup()` 中调用。

```cpp
void begin();
```

Arduino™ C 编程：16 课，从 setup() 到机器人

### 设置特定的 Arduino 引脚

```cpp
void setPin(byte pin);
```

虽然你可以手动创建并解码 32 位颜色，但不需要。提供了这些方法。

示例 HT8-6:
```cpp
unsigned long myColor;
myColor = 0x0FFFF;
```
```cpp
// 将第 5 个 LED 设置为青色
myPixels.setPixelColor(4, myColor);
myPixels.show();
```

将独立的红、绿、蓝颜色转换为封装的 32 位 RGB 颜色。

```cpp
unsigned long Color(byte red, byte green, byte blue);
```

其中

`packedColor` 是 4 字节整数。三个字节包含了显示在 NeoPixel 上的红、绿、蓝数量。

`red` 是一个 0 到 255 的数字，指定了最终颜色中的红色。

`green` 是一个 0 到 255 的数字，指定了最终颜色中的绿色。

`blue` 是一个 0 到 255 的数字，指定了最终颜色中的蓝色。

返回一个无符号长型整数，包含封装在 32 位颜色格式中的红、绿、蓝数量。

示例 HT8-7.
```cpp
unsigned long myPackedColor;
```
```cpp
// 品红色的颜色值
byte red = 255;
byte green = 0;
byte blue = 255;
myPackedColor = myPixels.Color(red, green, blue);
```

此方法通常在 `setup()` 中调用。

### 设置 Arduino 引脚

```cpp
void setPin(byte pin);
```
