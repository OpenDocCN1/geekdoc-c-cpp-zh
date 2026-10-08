

### (b) 使用 C 语言：

在此示例中，LM339 比较器通过 C 语言和外部中断与 PIC18F4321 进行接口连接。外部中断允许微控制器由 PIC18F4321 外部的源（例如比较器）触发中断。与之前的中断示例一样，代码以 `#pragma` 命令开始，该命令将把代码片段放置在内存的特定位置；当中断被触发时，微控制器将自动跳转到内存位置 `0x000008`，最终到达 `COMP_ISR`。

在主程序中，PORTD 被配置为输出，PORTB 被配置为数字输入。启用外部中断标志和全局中断使能。然后主程序在一个无限 'while' 循环中等待，该循环将 LED 关闭，直到比较器输出为高电平并中断微控制器。识别中断后，代码将自动跳转到地址 `0x000008`，然后通过 `Int_Output` 处的代码跳转到 `COMP_ISR` 处的服务例程。在服务例程中，代码将继续从 PORTB 获取开关数据，并通过 PORTD 将数据输出到 LED。只要比较器输出保持高电平，就会继续执行此操作。当 Vx 低于 Vy 时，比较器将输出 0，代码将返回到无限 'while' 循环并关闭 LED。以下是使用 C 语言的 PIC18F 程序：

```c
#include <PIC18F4321.h>
void COMP_ISR(void);
#pragma code COMP_Int=0x08 //At interrupt code jumps here
void COMP_Int(void)
{
_asm                // Using assembly language
GOTO COMP_ISR
_endasm
}
#pragma code
void main()
{
TRISD=0x00;                     // PORTD is output
ADCON1=0x0F;                   // Configure RB1 and INT0 as digital input
INTCONbits.INT0IE=1;           // Enable external interrupt
INTCONbits.INT0IF=0;          // Clear the external interrupt flag
INTCONbits.GIE=1;             // Enable global interrupts
PORTD=0;                      // Turn off LED;
while(1){  // wait in an infinite loop for the interrupt to occur
PORTD=0;                      // LED is off
}
}
# pragma interrupt COMP_ISR
void COMP_ISR(void) //start of the Comparator interrupt service routine
{
INTCONbits.INT0IF=0;          // Clear external interrupt flag
while(PORTBbits.RB0==1){ // Check if comparator is high
PORTD = PORTB;              // Move PORTB into PORTD
}
}
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_256_0.png)

**图 9.11** 示例 9.3 的图

## 示例 9.3

在图 9.11 中，如果 Vx > Vy，PIC18F4321 通过 INT0 被中断。另一方面，断开开关将通过 INT1 中断微控制器。请注意，在 PIC18F4321 中，INT0 的优先级高于 INT1。

### (a) 在地址 0x100 处使用 PIC18F 汇编语言编写主程序，执行以下操作：

- 将 STKPTR 初始化为 0x12
- 将 PORTB 配置为中断输入。
- 清除 INTCON 寄存器中的 INT0IF 和 INTCON3 寄存器中的 INT1IF 的中断标志位
- 将 PORTD（位 0、1）配置为 LED 的输出
- 通过清除 INTCON3 寄存器中的 INT1IP 位将 INT1 设置为低优先级中断
- 通过设置 RCON 寄存器中的 IPEN 位启用优先级中断
- 通过设置 INTCON 寄存器中的 GIEH 和 GIEL 位启用全局高优先级和低优先级中断
- 关闭 PORTD 上的两个 LED。
- 在无限循环中等待，并等待一个或两个中断发生。
- 关闭 PORTD 上的两个 LED（PORTD 位 0 上的比较器 LED 和 PORTD 位 1 上的开关 LED）
- 在无限循环中等待一个或两个中断发生。

此外，在地址 0x200 处使用 PIC18F 汇编语言编写高优先级中断（INT0）的服务例程，执行以下操作：

- 清除 INT0 的中断标志（INT0IF）
- 检查比较器输出是否仍为 1。如果是，则打开 PORTD 位 0 上的 LED。

最后，在地址 0x300 处使用 PIC18F 汇编语言编写低优先级中断（INT1）的服务例程，执行以下操作：

- 清除 INT1 的中断标志（INT1IF）
- 打开 PORTD 位 1 上的 LED

### (b) 在图 9.11 中，如果 Vx > Vy，PIC18F4321 通过 INT0 被中断。另一方面，断开开关将通过 INT1 中断微控制器。请注意，在 PIC18F4321 中，INT0 的优先级高于 INT1。使用 C 语言编写主程序，执行以下操作：

- 将 PORTB 配置为中断输入。
- 清除 INTCON 寄存器中的 INT0IF 和 INTCON3 寄存器中的 INT1IF 的中断标志位
- 将 PORTD（位 0、1）配置为 LED 的输出
- 通过清除 INTCON3 寄存器中的 INT1IP 位将 INT1 设置为低优先级中断
- 通过设置 RCON 寄存器中的 IPEN 位启用优先级中断
- 通过设置 INTCON 寄存器中的 GIEH 和 GIEL 位启用全局高优先级和低优先级中断
- 关闭 PORTD 上的两个 LED。
- 在无限循环中等待，并等待一个或两个中断发生

此外，使用 C 语言编写高优先级中断（INT0）的服务例程，该例程将检查比较器输出是否仍为 1。如果是，则打开 PORTD 位 0 上的 LED。如果比较器输出为 0，则返回。

最后，使用 C 语言编写低优先级中断（INT1）的服务例程，执行以下操作：

- 清除 INT1 的中断标志
- 检查开关是否仍为 1。如果是，则打开 PORTD 位 1 上的 LED；如果开关输入为 0，则返回。

# 解决方案

此示例将演示 PIC18F4321 微控制器的中断优先级方案。通过中断优先级，用户可以选择将中断声明为低优先级或高优先级中断。如果在任何时刻低优先级和高优先级中断同时发生，微控制器将始终处理高优先级中断。在上述示例中，比较器被设置为高优先级，开关被设置为低优先级，因此如果两个中断同时触发，则只有与比较器相关联的 LED 会被打开。

请注意，外部中断 INT0 只能作为高优先级中断。在实现单个中断时，中断服务例程编写在地址 0x08。另一方面，当启用优先级中断时，高优先级中断的服务例程编写在地址 0x08，而低优先级中断的服务例程编写在地址 0x018。

为了启用第二个外部中断 INT1，配置寄存器 INTCON3。此外，必须启用 INT1IE，并且必须将 INT1IF 清除为 0。此外，INTCON3 寄存器中用于设置 INT1 优先级的 INT1IP 位必须清除为 0 以设置为低优先级。接下来，RCON 寄存器中用于启用 PIC18F4321 中断优先级功能的 IPEN 位必须设置为 1。最后，INTCON 寄存器中的 GIEH 和 GIEL 位必须设置为 1，以启用全局高优先级和低优先级中断。

### (a) PIC18F 汇编语言程序：

```asm
INCLUDE <P18F4321.INC>
; RESET
                ORG             0       ; Reset vector
                BRA           MAIN      ; Jump to main program
; HIGH PRIORITY INTERRUPT ADDRESS VECTOR
                ORG             0x0008  ; High priority interrupt
                BRA           HIGH_INT_ISR
                                        ; Jump to service routine for the
                                        ; comparator
; LOW PRIORITY INTERRUPT ADDRESS VECTOR
                ORG             0x0018  ; Low priority interrupt
                BRA           LOW_INT_ISR
                                        ; Jump to service routine for the
                                        ; comparator
                ORG             0x0100
                ; MAIN PROGRAM
MAIN            MOVWF        0x12      ; Initialize STKPTR to 0x12
                MOVWF        STKPTR
                CLRF         TRISD     ; PORTD is output
                MOVLW        0x0F      ; Configure ADCON1 to set up
                MOVWF        ADCON1    ; INT0 and INT1 as digital inputs
                BSF          INTCON, INT0IE  ; Enable the external interrupt INT0
                BSF          INTCON3, INT1IE ; Enable the external interrupt INT1
                BCF          INTCON, INT0IF  ; Clear the INT0IF flag
                BCF          INTCON3, INT1IF ; Clear the INT1IF flag
                BCF          INTCON3, INT1IP   ; Configure INT1 as low priority
                BSF          RCON, IPEN      ; Enable priority interrupt
```

