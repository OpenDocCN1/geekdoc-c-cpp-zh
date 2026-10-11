
```assembly
INCLUDE       <PIC18F4321.INC>
ORG           0x100
MOVLW         0x60                ; 4MHz internal clock
MOVWF         OSCCON
MOVLW         D'249'              ; Initialize PR2 register
MOVWF         PR2
MOVLW         D'124'              ; Initialize CCPRL
MOVWF         CCPRL
MOVLW         0x20                ; CCP1 OFF,
MOVWF         CCP1CON             ; DC1B1:DC0B0=10
BCF           TRISC.CCP1          ; Configure CCP1 pin as output
CLRF          T2CON               ; 1:1 prescale, Timer2 OFF, no postscale
MOVLW         0x2C                ; PWM mode
MOVWF         CCP1CON
CLRF          TMR2                ; Clear Timer2 to 0
BACK:     BCF           PIR1,TMR2IF       ; Clear TMR2IF to 0
BSF           T2CON,TMR2ON        ; Turn Timer2 ON
WAIT:     BTFS          PIR1,TMR2IF       ; Wait until TMR2IF is HIGH
GOTO          WAIT
BRA           BACK
END
```

在上面的程序中，`TMR2`的值在每个时钟周期与周期寄存器`PR2`进行比较。当两个值匹配时，比较器生成一个匹配信号作为定时器输出。该信号还在下一个周期将`TMR2`的值复位为`0x00`。在上面的程序中，最后一条指令`BRA BACK`分支到标签处，将`PIR1`中的`TMR2IF`标志清零为`0`。由于`TMR2`在每次匹配后会自动清零，因此程序无需返回将`TMR2`清零。

- (b)

C语言程序如下所示：

```c
#include<p18f4321.h>
void main(void)
{
    OSCTCON =0x60; // 4MHz internal clock
    PR2=249; // Initialize PR2 register
    CCPRL=124; // Initialize CCPRL
    CCP1CON=0x20; // CCP1 OFF, DC1B1:DC0B0=10
    TRISCBits.TRISC2=0; // Configure CCP1 pin as output
    T2CON =0; // 1:1 prescale, Timer2 OFF, no postscale
    CCP1CON=0x2C; // PWM mode
    TMR2=0; // Clear Timer2 to 0

    while(1)
    {
        PIR1bits.TMR2IF=0; // Clear TMR2IF to 0
        T2CONbits.TMR2ON=1; // Turn Timer2 ON
        while(PIR1bits.TMR2IF==0); // Wait until TMR2IF is HIGH
    }
}
```

## 11.2 直流电机控制

如前所述，PWM信号的占空比与PWM提供的平均电压和功率成正比。由于这一特性，PWM模式可用于调光LED和控制无刷直流电机的速度等应用。这意味着随着PWM占空比的增加，LED会更亮。同样，随着PWM占空比的增加，直流电机的速度也会增加。另一方面，随着PWM占空比降低，LED会变暗，而电机的转速也会变慢。

在早期，电压调节器电路被用于控制直流电机的速度。但是，电压调节器会消耗大量功率。因此，使用处于PWM模式的`PIC18F`来控制直流电机的速度。在这种方案中，通过开和关施加到电机的驱动电压，功率耗散显著减少。

有时，希望改变直流电机的旋转方向。这可以通过软件反转电机方向，并将称为H桥（H-Bridge）的设备连接到`PIC18F`的I/O端口来实现。注意，另一方面，电机的速度可以使用PWM模式并通过将直流电机连接到`PIC18F4321`的`CCP1`引脚来控制。使用`PIC18F4321`的PWM模式进行直流电机控制的基本概念将在示例11.5中进行说明。

### PIC18F 的 CCP 和串行 I/O

像 `PIC18F4321` 这样的微控制器无法输出控制典型直流电机所需的大电流和电压。因此，需要驱动器（如 `CNY17F` 光耦）来放大 `PIC18F` 输出提供的电流和电压，并为直流电机提供适当的电平。使用 PWM 信号的许多有用应用之一就是它能够控制电机等设备。

在脉冲宽度调制（PWM）模式下，`CCPx` 引脚可配置为输出来生成具有指定频率和 10 位占空比的周期性波形。`TMR2` 用于 PWM 模式。PWM 周期是通过向 CCP 模块中称为 `PR2` 的 8 位内部寄存器写入值来指定的。请注意，可以使用定时器生成 PWM 波形。但是，使用 CCP 模块生成 PWM 波形更为简单。

## 例 11.5

希望通过使用连接到 `PORTB` 位 0 的电位器（图 11.3 (a)）动态改变脉冲宽度来改变直流电机的速度。请注意，PWM 占空比由电位器控制。`PIC18F4321` 将通过其片上 A/D 转换器将电位器电压作为八位输入，在 `CCP1` 引脚上生成 800 Hz 的 PWM 波形，然后随着电位器电压的变化改变电机的速度。使用 4 MHz 晶振和 `TMR2` 预分频值 16。忽略占空比的小数部分。请注意，可以使用图 11.3 (b) 中的电路代替光耦 `CNY17F`。

使用中断驱动的 ADC：

- (a) 编写 `PIC18F` 汇编语言程序以实现此功能。
- (b) 编写 C 语言程序以实现此功能。

### 解决方案

```
PR2 = [ (Fosc)/(4 x Fpwm x TMR2 Prescale Value) ] - 1
      = [(4 MHz)/(4 x 800 x 16)] - 1
      = 77.125
```

因此，`PR2` 约为 77。

将电位器电压转换为 8 位二进制数后，`ADRESH` 将包含转换后的数据。请注意，8 位 `ADRESH` 寄存器可容纳的最大值为 255。`ADRESH` 的内容可以移动到 `CCP1L` 中，以表示占空比的十进制部分。为了使占空比在 0 到 77 的范围内，`ADRESH` 的内容必须除以 3（255/77 约为 3）。这将确保占空比的十进制部分在 0 和 77 之间。电位器上的电压越高，`ADRESH/3` 的值就越高。这将生成占空比更高的 PWM 波形，从而使电机运行得更快。

下方的 `PIC18F` 汇编语言程序提供了此实现：

### (a)

```assembly
INCLUDE <PIC18F4321.INC>
ORGR      0x000
GOTO      MAIN
ORGR      0x0008    ; Program will go to CHECK_INT
                    ; at interrupt
GOTO      ADIF_ISR  ; Go to Interrupt Service Routine
ORGR      0x70      ; Start of the main program

MAIN
    MOVW    0x60
    MOVWF   OSCCON                ; Setting the internal clock to 4MHz
    MOVW    0x10
    MOVWF   STKPTR                ; Initialize STKPTR
                                  ; since interrupt is used
    MOVW    0x00
    MOVWF   TRISC                 ; Make PORTC output
    MOVW    0x02
    MOVWF   T2CON                 ; Configure Timer2 with prescale 16 and
                                  ; no postscale
    CLR     TMR2
    BCF     PIR1,TMR2IF           ; Clears Timer2 flag
    MOVW    0x31                  ; Use AN12 as ADC
    MOVWF   ADCON0
    MOVW    0x00
    MOVWF   ADCON1                ; Enable pins for analog input
    MOVW    0x08
    MOVWF   ADCON2                ; 2 TAD and Fosc/2, Left justified
    MOVW    0x0C
    MOVWF   CCP1CON               ; Select PWM mode
    MOVW    D'77'                 ; Set period of PWM signal
    MOVWF   PR2

START   BSF     ADCON0,GO         ; Start the ADC
WAIT    BRA     WAIT              ; Wait for ADC to interrupt
        BRA     START             ; Start ADC again

        ORG     0x200             ; start of the Service routine
ADIF_ISR  MOVFF   ADRESH, 0x20    ; Move value in ADRESH to 0x200
                                  ; Divide by 3 using repeated addition
        MOVW    0x03              ; Move 3 into the WREG
        CLRF    0x21              ; Clear value in 0x21

DIVIDE  CPFSGT  0x20              ; Compare the value to 3 skip if greater than
        BRA     FINISHED          ; Division is done
        INC     0x21, F           ; Increment 0x21
        SUBWF   0x20              ; Subtract 3 from 0x20
        BRA     DIVIDE            ; Subtract again

FINISHED MOVFF   0x21, CCP1L     ; Move final value into CCP1L
        BCF     PIR1,TMR2IF       ; Clear Timer2 flag
        BSF     T2CON,TMR2ON      ; Turn on Timer2

AGAIN   BTFSS   PIR1,TMR2IF       ; Wait until cycle is over
        BRA     AGAIN
        RETFIE                    ; Return to start ADC again
        END
```

### (b) 下方的 C 程序提供了此实现：

```c
#include <p18f4321.h> 
void ADINT_ISR(void); 
#pragma interrupt check_int 
void check_int(void) 
{ 
    ADINT_ISR();
}

#pragma code ADC_INT=0x08 // At interrupt, code jumps here

void ADC_Int (void)
{
    __asm
        GOTO check_int
    __endasm
}

#pragma code          // End of Code

void main ()
{
    OSCCON=0x60;         // 4 MHz
    PIE1bits.ADIE = 1;   // enable ADC interrupt
    PIR1bits.ADIF = 0;   // clear ADC interrupt flag
    INTCONbits.PEIE = 1;  // enable peripheral interrupt
    INTCONbits.GIE = 1;  // enable global interrupt
    TRISC=0;             // CCP1 output
    T2CON=0x02;          // Configure Timer2 with prescale 16
    PIR1bits.TMR2IF=0;   // Clear Timer2 interrupt flag

    ADCON0=0x31;    // AN12
    ADCON1=0x00;    // Enable analog pins
    ADCON2=0x08;    // 2 TAD and Fosc/2, Left justified-8-bit in ADRESH
    CCP1CON=0x0C;    // PWM enable
    PR2=77;
    TMR2 = 0;
    ADCON0bits.GO = 1;

    while (1);          // Wait for interrupt
}

void ADINT_ISR (void)
{
    PIR1bits.ADF = 0;
    CCP1L=ADRESH/3;
    PIR1bits.TMR2IF=0;        // Clear Timer2 interrupt
    T2CONbits.TMR2ON=1;

    while(PIR1bits.TMR2IF==0);
    ADCON0bits.GO=1;
}
```

**图 11.3(a)** 例 11.5 的电路图

**图 11.3(b)** 用于替代光耦的电路

## 11.3 串行接口

在许多情况下，希望将一个微控制器的二进制数据传送到另一个微控制器。在这种情况下，可以使用并行或串行传输技术来传输数据。在并行传输中，二进制数据的每一位都通过单独的线路传输。这意味着 8 位数据将通过八条线路传输。并行数据传输适用于短距离。对于位于数百英尺处的两个系统之间的数据传输，它并不具有成本效益。因此，通常使用串行传输在位于长距离的两个系统（如两台计算机）之间进行通信。

对于长距离，可以使用电话线进行数据传输。可以使用称为“调制解调器”（modem）的外围设备来实现此目的。请注意，modem 是调制器/解调器（modulator/demodulator）的缩写。发送端的调制解调器将发送数字设备（如微控制器）上的二进制数据转换为（调制为）音频信号，而接收端的另一个调制解调器则将这些音频信号转换（解调）为接收数字设备（如另一个微控制器）可用的二进制数据。

在串行传输中，仅使用一条线路逐位传输完整的二进制数据。因此，发送设备（如微控制器）必须使用并行输入串行输出移位寄存器将并行数据转换为串行位串。接收设备（如另一个微控制器）必须使用串行输入并行输出移位寄存器将数据从串行转换为并行。数据通常从最低有效位开始发送。为了区分各种位，使用时钟信号。串行数据传输可分为两种类型：同步和异步。我们将简要描述它们。

### 11.3.1 同步串行数据传输

同步串行数据传输的基本特征是基于时钟信号传输或接收数据。在确定特定的数据传输速率（通常称为“波特率”，即每秒位数）后，发送设备

在每个时钟脉冲上发送一个数据位。为了正确解释数据，接收设备必须知道每个数据单元的起始和结束位置。因此，在同步串行数据传输中，接收方必须知道要传输的数据单元数量。此外，接收方必须与数据边界保持同步。通常，使用一个或两个 SYNC 字符（一串位）来指示每个同步数据流的开始。数据单元通常包含诸如奇偶校验位之类的错误检测位。在某些传输中，最低有效位被用作奇偶校验位。发送设备在寻找数据时通常处于“搜索”模式。一旦根据所使用的 SYNC 字符数量匹配到一个或多个 SYNC 字符，接收方就开始解释数据。在同步串行传输中，发送设备需要向接收设备连续发送数据。然而，如果数据尚未准备好传输，发送方将使用 SYNC 字符进行填充，直到数据可用为止。

如前所述，在同步串行传输中，接收方必须知道所使用的 SYNC 字符数量以及要传输的数据单元数量。一旦接收方匹配到 SYNC 字符，它会接收指定数量的数据单元，然后进入“搜索”模式以匹配下一组数据的 SYNC 模式。

### 11.3.2 异步串行数据传输
