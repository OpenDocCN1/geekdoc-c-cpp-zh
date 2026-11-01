
```
i2c_write(data);
i2c_stop();
pause(11);
}
```

下一个函数由前面的构建模块组合而成，用于创建一个自定义函数，该函数从特定地址的EEPROM读取数据。

```
// *******************************************
// I2C_EEIN function to read from an 8-bit address Microchip
// EEPROM part (i.e. 24LC01) with 8 byte address (2k bit max)
// *******************************************
unsigned char I2C_EEIN(unsigned char address)
{
    unsigned char data;

    i2c_start();
    i2c_write(0xA0);
    i2c_write(address);
    i2c_repStart();
    i2c_write(0xA1);
    data=i2c_read(0);
    i2c_stop();
    return(data);
}
```

之前的所有函数都将成为SimpleC库的一部分。本项目的主代码循环是这一切汇集之处。首先调用init_micro()函数，然后设置B端口用于驱动LED指示灯。

```
// *******************************************
// Main Program Loop
// *******************************************

void main(void)
{
    init_micro(); // Initialize I/O
    i2c_init();      // Initialize i2c
    PORTB=0x00;      // All LEDs off
    TRISB=0x00;      // All PORTB outputs
```

创建了一个变量“cnt”用作计数器，以便在while循环中向EEPROM发送10个数据值。正在存储的值也会以二进制形式显示在四个LED上。

```
unsigned char cnt=0;    // Create variable and initialize to zero

while(cnt<=10)  /* write 10 numbers to eeprom */
{
    PORTB=cnt;          // The cnt value will display on the LEDs
    I2C_EOUT(cnt,10-cnt);  // Store 9 at address 1, 8 at address 2, ...
    cnt=cnt+1;          // Increment cnt variable
```

```
pause(255);      // Delay 255 milliseconds
}

cnt=0;
```

同样的变量“cnt”也被用作计数器，以便在while循环中从EEPROM读取10个数据值。读取的值将以二进制形式显示在LED上。

```
while(cnt<=10)
{
PORTB = I2C_EEIN(cnt); // Display data read from EEPROM on LEDs in binary
pause(1000);           // Delay for 1 second to read LEDs
cnt=cnt + 1;           // Increment cnt variable
}
```

所创建的所有这些函数都用于运行这个仅约16行代码的主循环。将所有函数放入一个库文件，正是SimpleC让C编程变得更简单的方式。

## 后续步骤

这个项目有很多可以更改的选项。您可以更改存储的数据，但根据您选择的数据，用四个LED以二进制形式读取可能会很困难。一个很好的改进是用LCD显示屏替换LED，这样会更容易理解。我使用LED是为了让硬件部分保持简单。说到简单，SimpleC会让为这个项目添加LCD变得非常容易。本书的最后一个项目将展示如何使用SimpleC库完成同样的项目，所以还等什么呢？让我们开始创建SimpleC库，让嵌入式C编程对初学者来说更加容易。

现在很明显，这只是我个人的观点，即单个库文件更容易让初学者理解，而我的这个系列书籍正是为这一读者群而写的。我相信会有更多有经验的程序员或学者给我各种理由来证明我是错的，而且很可能会在亚马逊上留下负面评论，但我仍然坚持我的信念：SimpleC仅仅是帮助更多初学者学习嵌入式C编程的垫脚石。如果我错了，SimpleC文件是开源的，任何用户都可以将其拆分为单独的.c和.h文件，以优化程序存储空间的使用。我甚至在完成这本书之前就修改了它。我最初从1.0版本开始，但在分发了一些测试版之后，我发现需要进行一些小的修改，因此我发布了1.1版本，也就是本书中使用的版本。

## SimpleC软件说明

SimpleC库由两个文件组成：simplec1.1.h和simplec1.1.c。数字1.1是版本级别，因此未来当我添加新函数时，版本号将从1.1增加到1.2、1.3，依此类推。这些文件已开源，可以在本书的软件下载和chipino.cc下载页面中找到，因此向此库添加内容可以成为一个社区项目，任何人都可以改进其功能。

在本节中，我想简要介绍每个函数的工作原理，以便您在使用库或需要针对特定应用进行修改时可以参考本章。稍后，我会为那些想要修改这些函数的人深入讲解每个函数的实际代码。

*注意：所有SimpleC函数都是区分大小写的，这意味着如果它们在simplec.c文件中以小写形式编写，那么您也需要在程序中使用小写形式。某些特定函数是以大写形式编写的，请务必注意这一点。*

## 初始化和时间延迟

SimpleC库中的第一组函数处理微控制器初始化、时基和基本I/O控制。配置设置和部分I/O定义位于simplec1.1.h文件中，我将在稍后介绍。其余的初始化由这些函数负责，下面我来总结一下。

### high(pin)

将指定的引脚（pin）置为高电平。该引脚会自动被设置为输出模式。pin可以是常量（0-13）或包含0-13数字的变量。

示例：

```
while()
{
  high(5); // Make pin5 (C2) an output and set it high (~5 volts)
}
```

或

```
#define led 8 // Define Pin 8 (RB0) as connected to LED

while()
{
  high(led);  //Make LED pin an output and set it high (~5 volts)
}
```

### low(pin)

将指定的引脚（pin）置为低电平。该引脚会自动被设置为输出模式。pin可以是常量（0-13）或包含0-13数字的变量。

示例：

```
while()
{
  low(5); // Make pin5 (C2) an output and set it low (~0 volts)
}
```

或

```
#define led 8 // Define Pin 8 (RB0) as connected to LED

while()
{
  low(led);  //Make LED pin an output and set it low (~0 volts)
}
```

### input(pin)

将指定的*pin*设为输入，并返回该引脚的状态。该函数前必须有接收状态的变量。*pin*可以是常量（0–13）或包含0–13数字的变量。

**示例：**

```
while()
{
char var = input(8);  // Store a 1 (high) or 0 (low) in the variable per pin 8 level
}
```

### pulseout(pin,period)

pulseout在指定的*pin*上生成指定*period*的脉冲。通过先将引脚置高、延时、再置低来生成脉冲。*pin*自动被设为输出。*pin*和*period*可以是常量（0–13）或包含0–13数字的变量。

pulseout的分辨率为10微秒增量。因此，*period*值为25时会产生250微秒长的脉冲。

```
while()
{
pulseout(5,100); // Send a pulse 1000 microseconds long (1 msec) on pin5
}
```

### adcin(pin)

adcin函数将模拟引脚上感测到的电压转换为0到255（8位分辨率）的数字值。参数*pin*指定要感测和转换的模拟引脚。SimpleC支持编号为0到4的5个模拟引脚。这与Microchip PIC的AN0至AN4引脚相对应。该函数实际用于一个等式中，将结果存入变量。电压范围可为0v至5v，但绝不能超过此范围。

示例

```
while()
{
char var = adcin(1)    // Convert voltage on AN1 pin and store in variable var
}
```

## LCD字符模块控制

2x16 LCD是一种常见的显示微控制器消息的方式。使用SimpleC库中的函数可以简化2x16 LCD的设置和控制。

### lcd_init()

lcd_init函数为PORTB（引脚8-13）控制的2x16 LCD字符模块建立连接。LCD的DB0-DB3引脚分别连接到B0至B3（引脚8-11）。RS引脚连接到B4（引脚12），EN引脚连接到B5（引脚13）。

在使用任何LCD命令之前，必须先调用lcd_init()。最好将其放在程序顶部。

示例：

```
void
main(void)
{
init_micro();    // Initialize I/O
lcd_init();      // Initialize LCD Display
lcd_clear();     // Clear LCD screen

while (1==1)
{
lcd_goto(0);            // Select first line
lcd_text("Simple C Make");  // Display Hello World
lcd_goto(0x40);         // Select second line
lcd_text("Programming Easy");// Display message between quotes
pause(1000);            // Delay for 1 second to read display
}
}
```

### lcd_clear()

lcd_clear函数将清除2x16 LCD字符模块的屏幕。光标也会位于显示器的左上角，通常称为零位置。

lcd_clear()函数通常放在程序顶部开始处，但也可以在程序中的任何位置使用，在写入新消息之前清除屏幕。

示例：

```
void
```

