
```c
ADCON0bits.GO = 1; // Start A/D conversion
while(1);
// Wait for interrupt
}
#pragma interrupt convert
void convert (void)
{
    PIR1bits.ADIF = 0; // Clear ADIF to 0
    result = ADRESH;
    PORTC = result/51;
    PORTD = (result%51)/5;
    ADCON0bits.GO = 1; // Start A/D conversion again
}
```

### 10.2.2 使用C语言接口外部D/A（数模）转换器

如前所述，大多数微控制器（例如PIC18F4321）没有片上D/A转换器（有时也称为DAC）。因此，外部D/A转换芯片被接口到PIC18F4321以完成此功能。有些微控制器，如Intel/Analog Devices 8051，包含片上D/A转换器。为了说明将D/A转换器接口到PIC18F的基本概念，一个典型的D/A转换器，如Maxim MAX5102，被接口到PIC18F4321。

**例10.13** 假设图10.22的框图。编写一个C程序，通过PIC18F4321的PORTD输入八个开关，并将该字节输出到MAX5102 D/A转换器的D0-D7输入引脚。微控制器将向WR和A0引脚发送适当的信号，以便D/A转换器将输入字节转换为0V到5V之间的模拟电压，并与其OUTA引脚输出转换后的电压。使用1-MHz内部时钟。

解答

为图10.22的D/A转换器接口编写PIC18F C语言程序的步骤如下：

- 1. 将PORTB和PORTC配置为输出，PORTD配置为输入。
- 2. 通过PORTB的位1向D/A的A0引脚输出低电平，以选择OUTA。
- 3. 通过PORTB的位0向D/A的WR引脚输出低电平。
- 4. 通过PORTD输入开关，并输出到PORTC。
- 5. 通过PORTB的位0向D/A的WR引脚输出高电平，以锁存8位输入数据用于转换为模拟电压。由于程序将写入来自开关的一个字节数据，因此不需要延时。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_324_0.png)

C = 0.1 微法

**图10.22** 例10.13的图示

C语言程序如下所示：

```c
#include <p18f4321.h>
void main (void)
{
    TRISB=0x00;    // Configure PORTB as output
    TRISC=0x00;    // Configure PORTC as output
    TRISD=0xFF;    // Configure PORTD as input
    PORTBbits.RB1=0;    // Clear A0 to 0 to select OUTA
    PORTBbits.RB0=0;    // Output LOW on bit 0 of PORTB
    PORTC=PORTD;    // Input switches, output to PORTC
    PORTBbits.RB0=1;    // Latch data for conversion
    while(1);    // Halt
}
```

## 问题与练习

- 10.1 找出T0CON寄存器的内容，以使用外部时钟、1:16预分频器，并在负沿递增来将Timer0编程为8位模式。
- 10.2 用PIC18F汇编和C编写程序：
  - (a) 将Timer0初始化为8位定时器，以提供计数为100的时间延迟。假设4 MHz内部时钟，预分频器值为1:16。
  - (b) 使用4 MHz晶振，在PORTC的位0上生成周期为4 ms的方波。使用Timer0。
  - (c) 使用4 MHz晶振，在PORTD的位7上生成周期为4 ms的方波。使用Timer1。
  - (d) 在PR2值为200微秒的情况下，点亮连接在PORTC位0的LED。假设4-MHz晶振，TMR2预分频和后置分频为1:1。
  - (e) 使用Timer3在16位模式下生成PORTC引脚3上的方波，周期为4 ms，预分频器值为1:8。使用4 MHz晶振。
- 10.3 设计基于PIC18F4321的数字时钟。时钟将显示时、分、秒。编写一个C程序来实现此功能。使用1MHz内部时钟。
- 10.4 使用C18延迟函数"10KTCyX,"，编写一个C程序，使连接在PORTC bit0的LED在10秒后切换。使用4MHz内部时钟。
- 10.5 假设PIC18F4321，Fosc = 1 MHz。考虑以下C程序：

```c
#include <p18f4321.h>
void delay(void);
void main(void){
    TRISBbits.TRISB=0;
    while (1){
        PORTBbits.RB4^=1;
        delay();
    }
}
void delay() {
    T0CON=0x01;
    TMROH=0xc2;
    TMROL=0xF7;
    T0CONbits.TMR0ON=1;
    while(INTCONbits.TMOIF == 0)
    ;
    T0CONbits.TMR0ON = 0;
    INTCONbits.TMOIF = 0;
}
```

  - (a) 在RB4引脚上生成什么类型的信号？其频率是多少？
  - (b) 如果T0CON初始化为0x42，并且从程序中删除TMR0H = 0xC2，信号的频率是多少？
- 10.6 假设PIC18F4321，4MHz晶振。对于ADC转换，在ADCON2寄存器中计算预分频为4时的$T_{AD}$，以及预分频为2时的$T_{ACK}$，然后验证转换是否有效。
- 10.7 找出ADCON0、ADCON1和ADCON2寄存器的内容，以启动以下选择的ADC：
  - AN5作为模拟输入。
  - $V_{ref^{-}}=V_{dd}$，$V_{ref^{+}}=V_{ss}$
  - $F_{osc}/4$，$4T_{AD}$
  - 结果左对齐
  - ADC模块开启
- 10.8 编写一个PIC18F汇编语言程序，使用PIC18F ADC将连接在AN9的模拟信号（0-5V DC）转换为10位数字，将这个10位数字除以4，并将8位结果存储在ADRESL中。丢弃余数。使用1MHz内部时钟。
- 10.9 为基于PIC18F4321的系统设计并开发硬件和软件（图P10.9），该系统将测量、计算并显示正弦电压的均方根（RMS）值。系统要求：
  - (a) 对5V（零到峰值电压）、60-Hz正弦电压进行128次采样。
  - (b) 使用PIC18F4321的片上ADC及其转换完成中断信号对采样值进行数字化。
  - (c) 使用公式 RMS Value = $[\sqrt{\sum_{i=1}^{N}(X_n)^2}]/N$ 计算波形的RMS值，其中$X_n$是采样值，N是总采样数。在两个七段显示器上显示RMS值（一个用于整数部分，另一个用于小数部分）。
  
  设计所有必要的接口。使用1 MHz内部时钟。
  
  编写一个C语言程序来实现上述功能。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_327_0.png)

**图P10.9**

- 10.10 *电容表。* 考虑图P10.10的RC电路。电容器两端的电压为Vc (t) = k e^(-t/RC)。在一个时间常数RC中，此电压放电至k/e的值。对于特定的R值，电容器的值C = T/R，其中T是时间常数，可由PIC18F4321使用1 MHz内部时钟计数。设计PIC18F4321的硬件和软件，通过放大器使用脉冲为电容器充电至最高10V峰值电压。然后，PIC18F4321将停止给电容器充电，测量一个时间常数的放电时间，并计算电容器的值。
  - (a) 绘制硬件原理图。
  - (b) 编写一个C程序来实现上述功能。
- 10.11 设计一个基于PIC18F4321的系统，以测量2k电阻（图P10.11）吸收的功率。系统将输入2k电阻两端的电压(V)，使用PIC18F4321的片上A/D转换器将其转换为8位输入，然后使用V²/R计算功率。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_328_0.png)

图P10.10

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_328_1.png)

图P10.11

## 11 PIC18F CCP和串行I/O

在本章中，我们描述使用汇编和C语言编程PIC18F片上外设的基础知识。主题包括PIC18F CCP（捕获/比较/脉宽调制）和串行I/O模块。

### 11.1 PIC18F CCP（捕获/比较/脉宽调制（PWM）模块

CCP模块在PIC18F4321中作为片上功能实现，用于提供基于时间的脉冲信号的测量和控制。Timer1到Timer3用于此目的。CCP模块不使用Timer0。任何复位都会关闭CCP模块。

PIC18F4321包含两个CCP（捕获/比较/脉宽调制）模块，即CCP1和CCP2。PIC18F4321的CCP1模块被实现为具有增强PWM功能的标准CCP，以更好地控制直流电机。因此，PIC18F4321中的CCP1模块也称为ECCP（增强型CCP）。CCP2模块提供标准的捕获、比较和PWM功能。请注意，CCP1和CCP2是两个模块。因此，可以同时将CCP1设置为PWM，CCP2设置为捕获或比较（反之亦然），因为它们是独立的两个模块。可能无法使用同一个CCP模块（例如CCP1）同时进行捕获（或比较）和PWM。这是因为，虽然定时器可能不同（Timer1，Timer3），但其他逻辑功能是共享的。在接下来的讨论中，CCP1和CCP2模块将被称为CCPx。

CCP模块可以被编程为以下模式之一：

- 捕获模式（CCPx引脚通过编程配置为输入）
- 比较模式（CCPx引脚通过编程配置为输出）
- PWM模式（CCPx引脚通过编程配置为输出）

PIC18F捕获模式在检测到脉冲的第n个上升沿或下降沿时，将16位定时器（Timer1或Timer3）的内容写入16位寄存器（CCPRxH:CCPRxL，由CCPx模块提供）。捕获模式可用于测量两个事件之间经过的时间。典型事件包括检测连接到CCPx引脚的周期性波形的每个下降沿或每个上升沿。通过捕获两个连续的上升沿，然后减去它们的值，可以得到波形的周期。因此，捕获模式可用于测量传入周期性波形的周期。

PIC18F比较模式非常类似于秒表的计时功能。请注意，秒表加载了一个由用户确定的预设时间。开始秒表后，它从预设值倒数到0。PIC18F比较模式以类似的方式工作，只不过它是从0计数到预设值。PIC18F比较

