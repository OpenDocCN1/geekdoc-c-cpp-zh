
```
#include <p18f4321.h>
#pragma config OSC = INTIO2 // Select internal oscillator
#pragma config WDT = OFF // Watch Dog Timer OFF
#pragma config LVP = OFF // Low Voltage Programming OFF
#pragma config BOR = OFF // Brown Out Reset OFF
```

请注意，上述内容适用于所有 PIC18F 汇编和 C 程序，包括轮询和中断驱动的 CCP、轮询和中断驱动的 SPI 以及 FC。

## 11.1.4 PIC18F4321 比较模式

在比较模式下，16 位 `CCPRx`（`CCP1` 为 `CCPR1H:CCPR1L` 或 `CCP2` 为 `CCPR2H:CCPR2L`）寄存器值不断与 `TMR1` 或 `TMR3` 寄存器中的值进行比较。当发生匹配时，PIC18F4321 的 `CCPx` 引脚可以：

- 驱动为高电平
- 驱动为低电平
- 翻转（从高到低或从低到高；取反）
- 保持不变

引脚上的操作基于 `CCPxCON` 寄存器中的模式选择位（`CCPxM3:CCPxM0`）的值（图 11.1）。一旦发生匹配，`CCPx` 标志位 `CCPxIF` 将被置为一。用户必须通过清除相应的 `TRIS` 位将 `CCPx` 引脚配置为输出。`Timer1` 或 `Timer3` 必须以定时器模式运行。

比较模式的典型应用包括在特定时延后激活事件（如开启或关闭泵）、生成具有特定占空比的脉冲串或波形。

编程 PIC18F4321 比较模式的步骤如下：

- 向 `CCPxCON`（图 11.1）加载适合比较模式的数据。将 `PORTC` 的 `CCPx` 引脚配置为输出。注意 `CCPx` 引脚与 `PORTC` 的某些位是复用的。
- 向 `CCPR1H:CCPR1L`（或 `CCPR2H:CCPR2L`）寄存器对加载适当的值。
- 通过将适当数据加载到 `T3CON` 寄存器中，在比较模式下选择 `Timer1`（或 `Timer3`）作为时钟源。`T1CON` 不用于选择比较模式的时钟源。相反，`T3CON` 用于选择 `Timer1` 或 `Timer3` 作为时钟源。
- 将 `Timer1H:Timer1L`（或 `Timer3H:Timer3L`）初始化为 0。
- 将 `PIR1` 中的 `CCP1IF`（或 `PIR2` 中的 `CCP2IF`）清零。
- 使用 `T1CON` 启动 `Timer1`（或使用 `T3CON` 启动 `Timer3`）。
- 在循环中等待，直到 `CCP1IF`（或 `CCP2IF`）为高电平。
- 一旦发生匹配（`CCP1IF` 或 `CCP2IF` 为高电平），使用 `T1CON` 停止 `timer1`（或使用 `T3CON` 停止 `Timer3`），编程的位值（高电平、低电平、翻转或不变）将被输出到 `CCPx` 引脚。

### 示例 11.2

假设为 PIC18F4321。

(a) 编写一个位于地址 `0x100` 的 PIC18F 汇编语言程序，在一毫秒时延后翻转 `CCP1` 引脚。使用 `Timer3` 和 `CCP1` 的比较模式。使用 8MHz 内部时钟。

(b) 编写一个 C 语言程序，在一毫秒时延后翻转 `CCP1` 引脚。使用 `Timer3` 和 `CCP1` 的比较模式。使用 8MHz 内部时钟。

### 解答

在 8-MHz 内部晶振下，`Fosc` = 8 MHz。由于 `Timer3` 使用 `Fosc`/4。定时器时钟频率 = `Fosc`/4 = 2 MHz。因此，`Timer3` 的时钟周期 = 0.5 微秒。计数值 = (1 ms)/(0.5 µsec) = `2000_10` = `0x07D0`。因此，对于 PIC18F4321 的比较模式，`CCPR1H:CCPR1L` 应加载 `0x07D0`。

(a) PIC18F 汇编语言程序如下：

```
INCLUDE <PIC18F4321.INC>
ORG 0x100
MOVLW 0x70 ; 8MHz internal clock
MOVWF OSCCON
MOVLW 0x02 ; Select compare mode, toggle CCP1 pin
MOVWF CCP1CON ; on match
BCF TRISC, CCP1 ; Configure CCP1 pin as output
MOVLW 0x40 ; Select TIMER3 as clock source for ; compare
MOVWF T3CON ; Select TIMER3 internal clock, 1:1 prescale ; TIMER3 OFF
MOVLW 0x07 ; Load CCP1H with 0x07
MOVWF CCPR1H
MOVLW 0xD0 ; Load CCP1L with 0xD0
MOVWF CCPR1L
CLRF TMR3H ; Initialize TMR3H to 0
CLRF TMR3L ; Initialize TMR3L to 0
BCF PIR1, CCP1IF ; Clear CCP1IF
BSF T3CON, TMR3ON ; Start Timer3
WAIT BTFSF PIR1, CCP1IF ; Wait in a loop until CCP1IF is 1. CCP1 pin
GOTO WAIT ; toggles when match occurs
BCF T3CON, TMR3ON ; Stop Timer3
HERE BRA HERE ; Halt
END
```

(b) C 语言程序如下：

```c
#include <p18f4321.h>
void main(void)
{
    OSCCON = 0x70;            // 8MHz internal clock
    CCP1CON=0x02;             // Select compare mode, toggle CCP1 pin
                              // on match
    TRISCbits.TRISC2=0;      // Configure CCP1 pin as output
    T3CON=0x40;               // Select TIMER3 as clock for compare,
                              // 1:1 prescale
    CCPR1H=0x07;              // Load CCPR1H with 0x07
    CCPR1L=0xD0;              // Load CCPR1L with 0xD0
    TMR3H=0;                  // Initialize TMR3H to 0
    TMR3L=0;                  // Initialize TMR3L to 0
    PIR1bits.CCP1IF=0;        // Clear CCP1IF
    T3CONbits.TMR3ON=1;      // Start Timer3

    while(PIR1bits.CCP1IF==0); // Wait in a loop until CCP1IF is 1

    T3CONbits.TMR3ON=0;      // Stop Timer3

    while(1);                // Halt
}
```

### 示例 11.3

编写一个 C 程序，在 PIC18F4321 的 `CCP1` 引脚上生成一个周期为 100 ms、占空比为 75% 的波形。使用比较模式、`Timer3` 和 1 MHz 晶振。

### 解答

在 1-MHz OSC 下，频率 = `Fosc`/4 = 0.25MHz

周期 = 1/0.25MHz = 4 微秒，波形周期为 100 毫秒

在一个周期内有 75% 的时间为高电平，波形将在 75 ms 内为高电平，25 ms 内为低电平。

因此，在 1:1 分频器下，计数值 = (75milliseconds)/(4 microseconds) = 18,750 (十进制) 或 `0x493E`。因此，应加载 `0x493E` 到 `CCPR1H:CCPR1L`，以便在一个周期内有 75% 的时间为高电平。

另外，在一个周期内有 25% 的时间为低电平，且在 1:1 分频器下，计数值 = (25milliseconds)/(4 microseconds) = 6250 (十进制) 或 `0x186A`。因此，应加载 `0x186A` 到 `CCPR1H:CCPR1L`，以便在一个周期内有 25% 的时间为低电平。

C 程序如下：

```c
void main(void)
{
    CCP1CON=0x02;             // Select compare mode, toggle CCP1 pin on match
    TRISCbits.TRISC2=0;      // Configure CCP1 pin as output
    T3CON=0x40;               // Select TIMER3 as clock for compare, 1:1 prescale
    while(1)
    {
        //~LOW:
```

`CCPR1H=0x18; // Load CCPR1H`

`CCPR1L=0x6A; // Load CCPR1L`

`TMR3H=0; // Initialize TMR3H to 0`

`TMR3L=0; // Initialize TMR3L to 0`

`PIR1bits.CCP1IF=0; // Clear CCP1IF`

`T3CONbits.TMR3ON=1; // Start Timer3`

`while(PIR1bits.CCP1IF==0); // Wait in a loop until CCP1IF is 1`

`T3CONbits.TMR3ON=0; // Stop Timer3`

// HIGH:

`CCPR1H=0x49; // Load CCPR1H`

`CCPR1L=0x3E; // Load CCPR1L`

`TMR3H=0; // Initialize TMR3H to 0`

`TMR3L=0; // Initialize TMR3L to 0`

`PIR1bits.CCP1IF=0; // Clear CCP1IF`

`T3CONbits.TMR3ON=1; // Start Timer3`

`while(PIR1bits.CCP1IF==0); // Wait in a loop until CCP1IF is 1`

`T3CONbits.TMR3ON=0; // Stop Timer3`

## 11.1.5 PIC18F4321 PWM (脉宽调制) 模式

在脉宽调制（PWM）模式下，`CCPx`引脚可以被配置为输出，以生成具有指定频率和10位（8位整数部分和2位小数部分）占空比的周期性波形。PWM占空比通过向`CCPRxL`寄存器写入高八位（整数部分）以及`CCPxCON`寄存器的低两位（小数部分）（第5位和第4位）来指定。`Timer2`用于PWM模式。PWM周期通过向CCP模块中的8位`PR2`寄存器写入值来指定。

根据PIC18F4321数据手册，PWM周期可以使用以下公式计算：

```
PWM Period = [(PR2 + 1) x 4 x Tosc x (TMR2 Prescale Value)]
where Tosc = (1/Fosc), Fosc is the crystal frequency, TMR2 Prescale Value can be initialized as 1, 4, or 16 using the T2CON register.
Hence, PR2 = [(Fosc)/(4 x Fpwm x TMR2 Prescale Value)] - 1
Note that PWM frequency (Fpwm) is defined as 1/(PWM period).
```

以下方程用于计算以时间为单位的PWM占空比：

```
PWM Duty Cycle = ((CCPxL.CCPxCON <5:4>) x Tosc x (TMR2 Prescale Value)).
```

如前所述，占空比定义为脉冲在高电平期间占一个时钟周期的百分比。此外，`CCPRxL`中的高八位是占空比的十进制部分，而`CCPxCON`寄存器的第5位和第4位包含占空比的小数部分。例如，考虑一个25%的占空比。由于占空比是`PR2`寄存器值的一个分数，当`PR2`值为30时，占空比的十进制值为7.5（0.25 x 30）。因此，必须将8位二进制数00000111加载到`CCPRL`中，并且必须将2位二进制数10（十进制0.5）加载到`CCPxCON`寄存器中的`DCxB1`和`DCxB0`位（图11.1）。这将把占空比7.5分配给要在`CCPx`引脚生成的PWM波形。

`CCP1` PWM输出波形（使用`CCP1L:CCP1CON`寄存器指定的占空比）的生成方式如下：`CCPR1L`被复制到`CCPR1H`。`CCP1CON <5:4>` 中的两位在内部锁存，以提供10位占空比。同样，8位`TMR2`值与两位内部锁存值拼接以创建10位占空比。

在`TMR2`从0启动后，`CCP1`引脚变为高电平，指示周期开始。`CCP1H`和两位锁存值与`TMR2`和两位锁存值进行比较以匹配。一旦匹配发生，`CCP1`引脚变为低电平。此时，波形将以占空比指定的持续时间保持高电平。`TMR2`继续递增。一旦`TMR2`的内容与`PR2`匹配，`CCP1`引脚被驱动为高电平，并且`TMR2`被清零为0。这完成了一个周期，然后开始另一个周期。对于后续周期，相同的过程持续进行。这在图11.2中有所描绘。

当配置CCP模块进行PWM操作时，应遵循以下程序：

- 1. 应使用PWM周期初始化`PR2`寄存器。
- 2. 通过向`CCP1xL`寄存器写入8位整数值，并向`CCP1xCON`的第5、4位写入两位小数部分来加载PWM占空比（图11.1）。此外，通过编程`CCP1xCON`寄存器来禁用PWM模式。
- 3. 通过清除相应的`TRISCx`位将`CCP1x`引脚配置为输出。
- 4. 选择`Timer2`预分频值，然后通过对`T2CON`写入来启用`Timer2`。
- 5. 通过向`CCP1xCON`寄存器写入适当的数据来启用PWM模式。
- 6. 将`TMR2`寄存器初始化为0。
- 7. 通过向`T2CON`寄存器写入适当的数据来打开`Timer2`。
- 8. 将`PIR1`寄存器中的`TMR2IF`标志（图10.8）清零为0。
- 9. 在循环中等待`TMR2IF`标志变高。一旦`TMR2IF`变高，将在`CCP1x`引脚生成具有指定占空比的PWM波形。
- 10. 这将完成一个周期。

可以通过轮询`PIR1`寄存器中的`TMR2IF`（图10.8）来生成PWM波形。下面的PIC18F汇编语言指令序列和C代码将通过将`TMR2IF`清零为0，打开`TMR2`，然后在循环中等待`TMR2IF`位变高（指示周期完成）来轮询`PIR1`寄存器中的`TMR2IF`标志位：

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_338_0.png)

在PIC18F汇编中：

```
REPEAT: BCF             PIR1,TMR2IF   ; Clear TMR2IF flag to 0
BACK:   BSF             T2CON,TMR2ON  ; Turn Timer2 ON
        BTFS          PIR1,TMR2IF   ; wait until completion of a cycle
        GOTO    BACK
        GOTO    REPEAT              ; Repeat
```

在C中：

```
PIR1bits.TMR2IF=0;              // Clear TMR2IF flag to 0
T2CONbits.TMR2ON=1;             // Turn Timer2 ON
while(PIR1bits.TMR2IF==0);      // Wait until TMR2IF = 1
```

### 示例 11.4

- (a)

在地址`0x100`处编写一个PIC18F汇编语言程序，在PIC18F4321的`CCP1`引脚上生成4 KHz、50%占空比的PWM。假设4 MHz晶振。

- (b)

编写一个C语言程序，在PIC18F4321的`CCP1`引脚上生成4 KHz、50%占空比的PWM。假设4 MHz晶振。

### 解答

`PR2 = [(Fosc)/(4 x Fpwm x TMR2 Prescale Value)] - 1`

`PR2 = [(4 MHz)/(4 x 4 KHz x 1)] - 1` 假设预分频值为1

`PR2 = 249`。具有50%占空比 = 0.5 x 249 = 124.5。因此，`CCPRL`寄存器将加载124，而`CCP1CON`寄存器中的位`DC1B1:DC0B0`将加载10（二进制）。

- (a)

PIC18F汇编语言程序如下所示：
