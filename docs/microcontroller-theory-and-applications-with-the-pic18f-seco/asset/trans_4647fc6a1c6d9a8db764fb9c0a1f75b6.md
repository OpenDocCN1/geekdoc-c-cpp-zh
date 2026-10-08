
## 10.1 数字 I/O 接口
（基于上下文推测，原文此处缺失章节标题，但根据内容属于数字接口部分，若严格依据OCR文本，则从图片开始）

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_307_0.png)

**图 10.14** 例 10.10 的插图

**例 10.10** 如图 10.14 所示，四个 LED 连接到 PIC18F4321 的 PORTC 的第 0-3 位。编写一个 C 程序，通过轮询 TMR3IF 标志位，基于 Timer3 提供的延时时间闪烁（开启或关闭）这些 LED。使用 Timer3 提供的最大延时，以及 1:4 的 TMR3 预分频器。使用 1MHz 的默认时钟。

### 解决方案

程序需要执行以下操作：

1.  配置 PORTC 为输出模式，输出 0 以关闭 LED。
2.  配置 T3CON 为 16 位操作模式，预分频比为 1:4，然后关闭 Timer3。
3.  将 TMR3H:TMR3L 初始化为 0:0。
4.  将 TMR3IF 清零。
5.  启动 Timer3，然后在 'while' 循环中等待 TMR3IF 变为高电平。
6.  一旦 Timer3 计数到 0xFFFF（提供最大延时时间）并溢出至 0x0000，TMR3IF 变为 1。
7.  停止 Timer3。
8.  重新将 TMR3H:TMR3L 初始化为 0:0，以备下一轮。
9.  反转 PORTC，使得在循环的第一轮中，四个 LED 全部开启。
10. 将 TMR3IF 清零。
11. 过程继续。

以下 C 代码可实现上述功能：

```c
#include <p18f4321.h>
void main (void)
{
    TRISC  = 0x00;                   // PortC is output
    PORTC = 0x00;
    T3CON = 0xA0;                   // Timer3 OFF with prescaler of 4
                                    // TMR3H initialized to 0
    TMR3H = 0x00;
    TMR3L = 0x00;
                                    // TMR3L initialized to 0
    PIR2bits.TMR3IF = 0;
                                    // Clear TMR3IF to 0
    while(1)
    {
        T3CONbits.TMR3ON = 1;       // Turn on TMR3
        while(PIR2bits.TMR3IF == 0);
                                    // Wait for TMR3IF to be 1
        T3CONbits.TMR3ON = 0;       // Stop TMR3
        TMR3H = 0x00;
                                    // Re-initialize TMR3H to 0
        TMR3L = 0x00;
                                    // Re-initialize TMR3L to 0
        PORTC = ~PORTC;
                                    // Invert PORTC output
        PIR2bits.TMR3IF = 0;
                                    // Clear TMR3IF to 0
    }
}
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_308_0.png)

**图 10.15** 例 10.11 的插图

**例 10.11** 如图 10.15 所示，四个 LED 连接到 PIC18F4321 的 PORTC 的第 0-3 位。使用 1MHz 的默认时钟。编写一个 C 程序执行以下操作：

1.  关闭所有 LED。
2.  使用由中断驱动的 Timer0 提供的延时时间开启 LED0。使用最大延时时间，预分频值为 1:4。
3.  使用由中断驱动的 Timer1 提供的延时时间开启 LED1。使用最大延时时间，预分频值为 1:4。
4.  使用由中断驱动的 Timer2 提供的延时时间开启 LED2。PR2 使用最大值，预分频值为 1:4，后分频值为 1:16。
5.  使用由中断驱动的 Timer3 提供的延时时间开启 LED3。使用最大延时时间，预分频值为 1:4。
6.  重复该过程。

### 解决方案

C 程序如下所示：

```c
#include <p18f4321.h>
void TMR0_ISR (void);
void TMR1_ISR (void);
void TMR2_ISR (void);
void TMR3_ISR (void);

#pragma interrupt check_int
void check_int(void)
{
    // Check which interrupt flag is triggered
    if (INTCONbits.TMR0IF == 1)
        TMR0_ISR ();
    if (PIR1bits.TMR1IF == 1)
        TMR1_ISR ();
    if (PIR1bits.TMR2IF == 1)
        TMR2_ISR ();
    if (PIR1bits.TMR3IF == 1)
        TMR3_ISR ();
}

#pragma code TMR_Int = 0x08 // At interrupt, code jumps here
void TMR_Int (void)
{
    _asm
        GOTO check_int
    _endasm
}
#pragma code // End of code

void main (void)
{
    TRISC = 0x00; // PortC is output
    PORTC = 0x00; // All LEDs OFF
    T0CON = 0x21; // Timer0 OFF, 8-bit with prescaler of 4
    TMR0L = 0x00; // Value placed in lower 8 bits of TMR0
    INTCONbits.TMR0IF = 0; // Clear TMR0 interrupt flag
    INTCONbits.TMR0IE = 1; // Enable TMR0 interrupt
    T1CON = 0xA0; // Timer1 OFF, 16-bit with prescaler of 4
    TMR1H = 0x00; // TMR1H = 0
    TMR1L = 0x00; // TMR1L = 0
    PIR1bits.TMR1IF = 0; // Clear TMR1 interrupt flag
    PIE1bits.TMR1IE = 1; // Enable TMR1 interrupt
    T2CON = 0x79; // Timer2 OFF, prescaler of 4 and postscaler of 16
    TMR2 = 0x00; // Value placed in Timer2
    PR2 = 0xFF; // Timer2 to compare with
    PIR1bits.TMR2IF = 0; // Clear TMR2 interrupt flag
    PIE1bits.TMR2IE = 1; // Enable TMR2 interrupt
    T3CON = 0xA0; // Timer3 OFF, 16-bit with prescaler of 4
    TMR3H = 0x00; // TMR3H = 0;
    TMR3L = 0x00; // TMR3L = 0;
    PIR2bits.TMR3IF = 0; // Clear TMR3 interrupt flag
    PIE2bits.TMR3IE = 1; // Enable TMR3 interrupt
    INTCONbits.GIE = 1; // Enable global interrupts
    INTCONbits.PEIE = 1; // Enable peripheral interrupts
    T0CONbits.TMR0ON = 1;    // Turn on TMR0
    while(1);
    // Do nothing while timers are counting
}

void TMR0_ISR(void)
{
    T0CONbits.TMR0ON = 0;    // Turn off TMR0
    PORTC = 0x01;            // Light ON LED connected to PORTC bit 0
    TMR0H = 0x00;            // TMR0H = 0
    TMR0L = 0x00;            // TMR0L = 0
    INTCONbits.TMR0IF = 0;   // Clear TMR0 interrupt flag
    T1CONbits.TMR1ON = 1;    // Turn on TMR1
}

void TMR1_ISR(void)
{
    T1CONbits.TMR1ON = 0;    // Turn off TMR1
    PORTC = 0x02;            // Light LED connected to PORTC bit 1
    TMR1H = 0x00;            // TMR1H = 0
    TMR1L = 0x00;            // TMR1L = 0
    PIR1bits.TMR1IF = 0;     // Clear TMR1 interrupt flag
    T2CONbits.TMR2ON = 1;    // Turn on TMR2
}

void TMR2_ISR(void)
{
    T2CONbits.TMR2ON = 0;    // Turn off TMR2
    PORTC = 0x04;            // Light LED connected to PORTC bit 2
    TMR2 = 0x00;             // Value placed in Timer2
    PIR1bits.TMR2IF = 0;     // Clear TMR2 interrupt flag
    T3CONbits.TMR3ON = 1;    // Turn on TMR3
}

void TMR3_ISR(void)
{
    T3CONbits.TMR3ON = 0;    // Turn off TMR3
    PORTC = 0x08;            // Light LED connected to PORTC bit 3
    TMR3H = 0x00;            // TMR3H = 0
    TMR3L = 0x00;            // TMR3L = 0;
    PIR2bits.TMR3IF = 0;     // Clear TMR3 interrupt flag
    T0CONbits.TMR0ON = 1;    // Turn on TMR0
}
```

## 10.2 模拟接口

模拟接口作为片上功能集成在微控制器中。该接口通常包括片上 A/D（模数）和 D/A（数模）转换器。这便于将温度、流量和压力等模拟信号与微控制器进行接口连接。如第 1 章所述，A/D 和 D/A 转换器（也称为 ADC 和 DAC）广泛用于执行数据采集和控制。ADC（也称为 A/D 转换器）将模拟电压转换为二进制数。另一方面，DAC（也称为 D/A 转换器）将二进制数转换为模拟电压或电流。在本讨论中，“ADC”或“A/D 转换器”与“DAC”或“D/A 转换器”将互换使用。

单独的 A/D 和 D/A 转换器芯片在商业上是可获得的。这些芯片通常用于基于微处理器的应用。PIC18F4321 包含一个片上 A/D。然而，如果需要数模转换，则需要接口连接一个外部 D/A 芯片。

### 10.2.1 PIC18F 片上 ADC（A/D 转换器）

PIC18F 片上 ADC 提供 8 位或 10 位的输出。典型的 ADC 特性包括分辨率、参考电压、ADC 通道、采集时间和 ADC 时钟。我们下面将简要描述它们。

**分辨率** 分辨率是 ADC 最重要的特性之一。分辨率规定了 ADC 转换模拟电压的精度。例如，如果一个模拟电压（也称为稍后将讨论的“参考电压”）在 0 到 5 伏直流之间，那么 8 位 ADC 将输入电压转换为 8 位二进制数，并能以高达 19 mV 的精度进行测量（$5/2^{8} = 5/256 = 19\ \text{mV}$）。这意味着 8 位 ADC 无法区分 1 mV 和 18 mV 之间的差异。另一方面，10 位 ADC 可以将 0 到 5V 直流的模拟电压转换为 10 位二进制数，精度为 4.8 mV（$5/2^{10} = 5/1024 = 4.8\ \text{mV}$）。因此，10 位 ADC 提供了更高的分辨率。

PIC18F 片上 ADC 为 8 位或 10 位，可通过编程选择。

**参考电压** 参考电压规定了模拟输入电压的最小值和最大值。PIC18F4321 中包含两个参考电压输入端，Vref+（PIC18F4321 的第 5 引脚）和 Vref-（PIC18F4321 的第 4 引脚）。Vref+ 连接到最大电压，而 Vref- 连接到最小电压。PIC18F4321 将差分电压 (Vref+ - Vref-) 转换为 8 位或 10 位数。Vref+ 和 Vref- 的值通过在 PIC18F 中编程一个寄存器来选择（稍后讨论）。Vref+ 和 Vref- 的常见值是 +5VDC 和 0V。当通过编程选择 8 位 ADC 时，5V 将转换为十进制数 255（FFH），0V 转换为 0。

**ADC 通道** ADC 硬件模块通过多路复用器连接到几个通道。多路复用器允许将多个模拟输入连接到 ADC 进行转换。每个通道都可以连接一个将被 ADC 转换为二进制的模拟电压。可以通过编程选择其中一个通道，多路复用器将选定的通道连接到 ADC 模块。PIC18F 包含 13 个通道（AN0 至 AN12）。

**采集时间** 当选择一个 ADC 通道时，该通道的电压用于对内部电容器充电。电容器完全充电到选定通道的电压需要一定的时间。这个充电时间称为“采集时间”。PIC18F ADC 的采集时间可由用户编程设定。一旦达到采集时间，PIC18F 断开选定通道与源之间的连接，然后开始转换。采集时间取决于源阻抗和 Vdd（漏极电压）等因素。

**ADC 时钟** 用于执行转换的 ADC 时钟称为 ADC 时钟周期 ($T_{AD}$)。这与转换一个位所需的时间相同。

PIC18F4321 包含一个片上模数转换器 (ADC) 模块，具有 13 个通道（AN0-AN12）。模拟输入可以选定作为这些通道之一的输入

