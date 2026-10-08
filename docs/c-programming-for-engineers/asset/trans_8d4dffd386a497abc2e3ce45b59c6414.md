

## 第 15 章 Arduino  C 语言

要使用数字输出，你首先需要使用 `pinMode()` 函数将引脚配置为 `OUTPUT`（输出）。例如：

```
pinMode(13, OUTPUT); // 设置引脚 13 为输出
digitalWrite(13, HIGH); // 打开引脚 13 (5V)
digitalWrite(13, LOW); // 关闭引脚 13 (0V)
```

数字输出通常用于控制：

- LED：控制视觉指示器
- 继电器：控制电机或灯光等大功率设备
- 蜂鸣器/扬声器：产生简单的音调或音效
- 移位寄存器：扩展数字输出数量
- 晶体管/MOSFET：驱动大电流设备

需要注意的事点：

- **不要让引脚过载**：每个 Arduino 板的每个引脚都有最大电流额（通常约为 40mA）。过载引脚可能导致运行不稳定或损坏 Arduino。详细信息请参考开发板文档。
- **更大电流**：为了控制电流大于单个引脚所提供的设备（例如高功率 LED、大电机），请使用晶体管、MOSFET 或驱动器。这些组件会放大 Arduino 的信号并有效处理更大的电流。
- **感性负载**：电机或电磁铁等设备在关闭时不仅需要大电流，还会产生 EMF（电磁力）。使用续流二极管（也称为自由二极管）来吸收这些电压尖峰。
- **模拟引脚也可以**：在某些 Arduino 板上，某些模拟输入引脚（如 A0、A1 等）也可以作为数字输出。

## 数字输入

数字输入意味着引脚处于高电压还是低电压。高电压或低电压通常相对于微控制器电源电压（Vcc）的一半。如果引脚电压高于 Vcc/2，则该引脚被视为高电平。

引脚的状态通过使用 `digitalRead()` 函数确定。该函数接受一个参数，要读取的引脚数量（0-13 或 A0-A5），并将引脚状态作为 1（HIGH）或 0（LOW）返回。

引脚的数字状态取决于它是否被设置为输出。然而，当你读取设置为输出的引脚状态时，你读取的只是定义的输出状态。

```
int pinState; // 定义变量以存储引脚状态
pinState = digitalRead(2); // 读取引脚 2 的状态
```

## 15.3 Arduino 与普通 C 语言

当引脚被设置为输入时，它的电压取决于连接的电路，而不是取决于微控制器。如果电路断开（例如通过开关），引脚的状态将变得不确定，这被称为“浮空”（floating）。为了防止这种不确定性，在输入引脚上连接了上拉电阻或下拉电阻。该电阻将输入引脚连接到高电压或地，确保当开关打开时，引脚被拉伸到 HIGH 或 LOW。

## 15.3.3 Arduino 标准 I/O 库

在 Arduino 中，你可以使用标准输入/(I/O）函数通过 PC 上的串口进行通信。Arduino IDE 提供了一个内置的串口监视器（Serial Monitor），用于从板发送和接收数据。你也可以在 PC 上使用 PuTTY 等终端模拟器应用程序与 Arduino 板通信。

标准 I/O 的主要函数有：

- `Serial.begin(baud,rate)`：此函数以指定的波特率初始化串口通信。例如，`Serial.begin(9600);` 将波特率设置为每秒 9600 位。
- `Serial.print(data)`：此函数将指定的数据发送到串口。数据可以是数字、字符串或任何可以转换为字符串的数据类型。
- `Serial.print(x, 3); // 打印浮点数 x，保留3位有效数字
- `Serial.println(data)`：此函数与 `Serial.print()` 类似，但它会在输出末尾添加一个换行符（`'\n'`）。
- `Serial.available()`：此函数返回串口中可读取的字节数（字符数）。
- `Serial.read()`：此函数从串口读取单个字节（字符）。如果没有可用数据，则返回 -1。
- `Serial.readBytes(buffer, length)`：此函数从串口读取最多 `length` 个字节并将其存储在提供的 `buffer` 数组中。
- `Serial.readBytesUntil(terminator, buffer, length)`：此函数从串口读取，直到遇到指定的终止字符 `terminator`，或者读取了 `length` 个字节。字节存储在 `buffer` 数组中。

![](img/33fb6b7acbb6df48a3c9564e97117da6_246_0.png)

## 第 15 章 Arduino C 语言

这是一个关于如何使用这些函数的示例：

```
// Arduino 代码
void setup() {
  Serial.begin(9600); // 以 9600 波特率初始化串口
}

void loop() {
  if (Serial.available() > 0) { // 检查是否有可用数据
  char input = Serial.read(); // 从串口读取单个字节
  Serial.print("You entered: ");
  Serial.println(input); // 打印输入字符并换行
  }
}
```

然后，在 Arduino IDE 串口监视器中，你可以在输入框中输入字符并……（等等，文本在此结束）。

实际上，查看提供的 OCR 文本，文本突然中断了。让我根据提供的块进行重新处理。

[content]
## 第 15 章 Arduino C 语言

要使用数字输出，你首先需要使用 `pinMode()` 函数将引脚配置为 `OUTPUT`（输出）。例如：

```
pinMode(13, OUTPUT); // 设置引脚 13 为输出
digitalWrite(13, HIGH); // 打开引脚 13 (5V)
digitalWrite(13, LOW); // 关闭引脚 13 (0V)
```

数字输出通常用于控制：

- LED：控制视觉指示器
- 继电器：控制电机或灯光等大功率设备
- 蜂鸣器/扬声器：产生简单的音调或音效
- 移位寄存器：扩展数字输出数量
- 晶体管/MOSFET：驱动大电流设备

需要注意的事点：

- **不要让引脚过载**：每个 Arduino 板的每个引脚都有最大电流额（通常约为 40mA）。过载引脚可能导致运行不稳定或损坏 Arduino。详细信息请参考开发板文档。
- **更大电流**：为了控制电流大于单个引脚所提供的设备（例如高功率 LED、大电机），请使用晶体管、MOSFET 或驱动器。这些组件会放大 Arduino 的信号并有效处理更大的电流。
- **感性负载**：电机或电磁铁等设备在关闭时不仅需要大电流，还会产生 EMF（电磁力）。使用续流二极管（也称为自由二极管）来吸收这些电压尖峰。
- **模拟引脚也可以**：在某些 Arduino 板上，某些模拟输入引脚（如 A0、A1 等）也可以作为数字输出。

## 数字输入

数字输入意味着引脚处于高电压还是低电压。高电压或低电压通常相对于微控制器电源电压（Vcc）的一半。如果引脚电压高于 Vcc/2，则该引脚被视为高电平。

引脚的状态通过使用 `digitalRead()` 函数确定。该函数接受一个参数，要读取的引脚数量（0-13 或 A0-A5），并将引脚状态作为 1（HIGH）或 0（LOW）返回。

引脚的数字状态取决于它是否被设置为输出。然而，当你读取设置为输出的引脚状态时，你读取的只是定义的输出状态。

```
int pinState; // 定义变量以存储引脚状态
pinState = digitalRead(2); // 读取引脚 2 的状态
```

## 15.3 Arduino 与普通 C 语言

当引脚被设置为输入时，它的电压取决于连接的电路，而不是取决于微控制器。如果电路断开（例如通过开关），引脚的状态将变得不确定，这被称为“浮空”。为了防止这种不确定性，在输入引脚上连接了上拉电阻或下拉电阻。该电阻将输入引脚连接到高电压或地，确保当开关打开时，引脚被拉伸到 HIGH 或 LOW。

## 15.3.3 Arduino 标准 I/O 库

在 Arduino 中，你可以使用标准输入/(I/O）函数通过 PC 上的串口进行通信。Arduino IDE 提供了一个内置的串口监视器（Serial Monitor），用于从板发送和接收数据。你也可以在 PC 上使用 PuTTY 等终端模拟器应用程序与 Arduino 板通信。

标准 I/O 的主要函数有：

- `Serial.begin(baud,rate)`：此函数以指定的波特率初始化串口通信。例如，`Serial.begin(9600);` 将波特率设置为每秒 9600 位。
- `Serial.print(data)`：此函数将指定的数据发送到串口。数据可以是数字、字符串或任何可以转换为字符串的数据类型。
- `Serial.print(x, 3); // 打印浮点数 x，保留3位有效数字
- `Serial.println(data)`：此函数与 `Serial.print()` 类似，但它会在输出末尾添加一个换行符（`'\n'`）。
- `Serial.available()`：此函数返回串口中可读取的字节数（字符数）。
- `Serial.read()`：此函数从串口读取单个字节（字符）。如果没有可用数据，则返回 -1。
- `Serial.readBytes(buffer, length)`：此函数从串口读取最多 `length` 个字节并将其存储在提供的 `buffer` 数组中。
- `Serial.readBytesUntil(terminator, buffer, length)`：此函数从串口读取，直到遇到指定的终止字符 `terminator`，或者读取了 `length` 个字节。字节存储在 `buffer` 数组中。

![](img/33fb6b7acbb6df48a3c9564e97117da6_246_0.png)

## 第 15 章 Arduino C 语言

这是一个关于如何使用这些函数的示例：

```
// Arduino 代码
void setup() {
  Serial.begin(9600); // 以 9600 波特率初始化串口
}

void loop() {
  if (Serial.available() > 0) { // 检查是否有可用数据
  char input = Serial.read(); // 从串口读取单个字节
  Serial.print("You entered: ");
  Serial.println(input); // 打印输入字符并换行
  }
}
```

## 15.3 Arduino 与普通 C 语言
（此处根据 OCR 文本合并逻辑，内容重复）

## String 对象

构造字符串对象的格式如下：

```
String(val)
String(val, base)
String(val, decimalPlaces)
```

其中

- val：格式化为 String 的变量。允许的数据类型：string, char, byte, int, long, unsigned int, unsigned long, float, double
- base：（可选）格式整数值的进制。
- decimalPlaces：仅当 val 为 float 或 double 时有效。

以下是在 Arduino 中声明和使用 String 的示例：

```
// 使用常量 String
stringOne = "Hello String";
// 将常量转换为 String 对象
stringTwo = String("This is a string");
// 拼接字符串
StringThree = String(stringTwo + " more");
// 使用常量整数
StringFour = String(13);
// 使用整数和进制
stringFive = String(analogRead(0), DEC);
// 使用整数和进制（十六进制）
stringSix = String(45, HEX);
// 使用整数和进制（二进制）
stringSeven = String(255, BIN);
// 使用长整型
stringEight = String(millis(), DEC);
// 使用浮点数和小位数
stringNine = String(5.698, 3);
```

## 15.3.4 Arduino String 类型

String 类型是面向对象的。选择 String 的几个理由：

- **String 方法**：String 类型提供了内置方法，简化了字符串操作。
- **变长字符串**：与字符数组不同，String 的长度可以改变。
- **库兼容性**：许多 Arduino 库接受并返回 String 对象。

然而，需要注意的是 String 类型使用动态分配，这会导致内存碎片，特别是在 RAM 内存有限的板上。

## String 方法

在 Arduino 编程中，它们看起来相似，但存在关键区别。函数是执行特定任务的独立代码块。它们有自己的作用域，只能访问自己的变量。而方法是与对象或类的实例化相关联的。它们可以访问并与所属对象的数据和状态进行交互。其他区别：

作用域：函数有自己的作用域，只能访问自己的变量。方法可以访问所属对象的数据。

