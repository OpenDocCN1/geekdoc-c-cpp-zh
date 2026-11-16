

RJMP 到此中断的中断处理程序或 ISR 放在此原点更改下方，以便其在内存中位于地址 0x0006。在此代码中，没有其他中断的中断向量表条目，因此绝不能启用其他中断。使用此布局，可以从项目中删除虚拟中断处理程序代码，因为它从未被使用。

## 主程序代码

中断向量表之后，我们有以下代码。

```
main:
    sbi   DDRB, DDB4        ; Pin PB4 as output pin
    ldi   r16, (1 << WGM01)  ; CTC mode for timer
    out   TCCR0A, r16
    ldi   r16, 0x7F         ; Output compare value
    out   OCR0A, r16
    ldi   r16, (1 << OCIE0A) ; Enable T0A compare match interrupt
    sts   TIMSK0, r16
    sei                     ; Set global interrupt enable bit
    ldi   r16, (1 << CS02) | (1 << CS00) ; Prescaler CLK/1024 and start timer
    out   TCCR0B, r16
loop:
    rjmp loop
```

在此代码中，引脚 PB4 使用 SBI 指令设置为输出引脚。之后，定时器 0 的设置方式与之前轮询定时器的项目相同。定时器首先置于 CTC 模式，然后将比较值加载到 OCR0A。随后是上面以粗体显示的新代码，用于启用定时器 0 比较匹配 A 中断和全局中断使能位。位 OCIE0A 在 TIMSK0 寄存器中被置位，以启用定时器/计数器比较匹配 A 中断。随后是 SEI（设置全局中断使能位）指令，它在状态寄存器中设置 I 位。请返回第 6 章第 6.5 节中的图 6.8 以查看状态寄存器。在状态寄存器中，最左边的第一位，即位号 7，是全局中断使能位，或 I 位。一旦该位被置位，任何已启用的单独中断（例如定时器/计数器 0 比较匹配 A 中断）在被触发时都将工作。最后，定时器像之前一样通过选择系统时钟除以 1024 来启动。程序执行随后进入无限循环。

## 中断服务例程代码

最后，我们有定时器 0 比较匹配 A 中断的中断服务例程代码，如下面的代码片段所示。此 ISR 中的代码仅使用 PINB 寄存器切换连接到引脚 PB4 的 LED。此项目与轮询项目的区别在于，现在定时器中断和 ISR 处理一切。

```
; Timer 0 compare match A interrupt service routine or handler
ISR_tim0_compa:
    sbi PINB, PINB4 ; Toggle LED
    reti
```

由于主程序执行在无限循环中什么也不做，只有 ISR 可以切换 LED。当定时器计数器寄存器 TCNT0 与输出比较寄存器 OCR0A 之间出现比较匹配时，将触发定时器/计数器比较匹配 A 中断。程序执行跳转到中断向量表中该中断的向量位置，该位置在 ATtiny13(A) 上为地址 0x0006。在此位置处是跳转到 ISR_tim0_compa 中断服务例程的 RJMP 指令。在此 ISR 中，PINB 寄存器中的 PINB4 位被置位，从而切换 LED。ISR 在执行 RETI 指令后返回主循环。务必始终使用 RETI 而不是 RET 从 ISR 返回。

## 运行定时器中断代码

使用调试器/编程器或使用 Microchip Studio 中的模拟器运行代码。单步执行代码并注意，地址 0 处的第一条 RJMP 指令跳转到 main 标签。在单步执行 SEI 指令之前，请确保处理器状态窗口已打开。查看处理器状态窗口顶部附近的状态寄存器 I 标志。它最初被清除或为 0。在单步执行 SEI 指令后，它变为实心红色，表明它刚刚改变了状态并且现在已被置位。在 ISR_tim0_compa ISR 底部的 RETI 指令上设置断点。现在使用 F5 键盘键运行代码。当代码执行在断点处停止时，注意状态寄存器中的 I 标志现在已被清除。单步执行 RETI 指令并注意 I 标志自动被置位并再次变为实心红色。请记住，如果处理器状态窗口中的项目状态刚刚改变，它们会变为红色。例如，状态寄存器中的位如果仍然置位但未从最近的单步执行中改变，则会变为蓝色。打开 I/O 窗口并单击 I/O 端口 (PORTB) 项目，以便在 I/O 窗口底部显示端口 B 寄存器。使用 F5 键盘键在断点仍位于 RETI 指令上的情况下运行代码，将导致执行在引脚 PB4 被切换后停止。可以在 I/O 窗口底部的 PORTB 寄存器中看到每次中断时对应于引脚 PB4 的位都在切换。

## 10.5.3.2 ATtiny25/45/85 定时器中断项目

由于 ATtiny13(A) 和 ATtiny25/45/85 之间的中断向量表不同，因此包含了下一个项目，它与前一个项目相同，但已调整为适用于 ATtiny25/45/85。在 Microchip Studio 中为 ATtiny25、ATtiny45 或 ATtiny85 创建 timer0_interrupt_asm 项目。将以下清单中的代码输入到项目的 main.c 文件中。

```
timer0_interrupt.asm : main.asm

.org 0
rjmp main ; 0 - Reset vector
rjmp ISR_unused ; 1 - External interrupt 0 vector
rjmp ISR_unused ; 2 - Pin change interrupt 0 vector
rjmp ISR_unused ; 3 - Timer 1 compare match A interrupt vector
rjmp ISR_unused ; 4 - Timer 0 overflow interrupt vector
rjmp ISR_unused ; 5 - Timer 0 overflow interrupt vector
rjmp ISR_unused ; 6 - EEPROM ready interrupt vector
rjmp ISR_unused ; 7 - Analog comparator interrupt vector
rjmp ISR_unused ; 8 - ADC conversion complete interrupt vector
rjmp ISR_unused ; 9 - Timer 1 compare match B interrupt vector
rjmp ISR_tim0_compA ; A - Timer 0 compare match A interrupt vector
rjmp ISR_tim0_compB ; B - Timer 0 compare match B interrupt vector
rjmp ISR_unused ; C - Watchdog timer timeout interrupt vector
rjmp ISR_unused ; D - USI start interrupt vector
rjmp ISR_unused ; E - USI overflow interrupt vector

main:
sbi DDRB, DDB4 ; Pin PB4 as output pin
ldi r16, (1 << WGM01) ; CTC mode for timer
out TCCR0A, r16
ldi r16, 0x7F ; Output compare value
out OCR0A, r16
ldi r16, (1 << OCIE0A) ; Enable T0A compare match interrupt
out TIMSK, r16
sei ; Set global interrupt enable bit
ldi r16, (1 << CS02) | (1 << CS00) ; Prescaler CLK/1024 and start timer
out TCCR0B, r16

loop:
rjmp loop

; Timer 0 compare match A interrupt service routine or handler
ISR_tim0_compA:
sbi PINB, PINB4 ; Toggle LED
reti

; Dummy interrupt handler to catch all unused interrupts
ISR_unused:
nop
rjmp ISR_unused
```

与前一个项目相比，上述程序中第一个也是最明显的变化是更大的中断向量表。ATtiny25/45/85 设备比 ATtiny13(A) 设备具有更多的片上外设，这些额外的外设具有中断功能。这意味着需要为这些额外的中断源提供额外的中断向量。除了拥有更大的中断向量表之外，定时器 0 比较匹配 A 中断向量位于不同的位置。此中断向量在 ATtiny13(A) 上位于地址 0x0006，但在 ATtiny25/45/85 上位于地址 0x000A。事实上，在比较两个 ATtiny 设备系列时，只有前三个中断向量（包括复位向量）位于相同的地址。程序其余部分与 ATtiny13(A) 相同，只是 TIMSK 寄存器在 ATtiny13(A) 上称为 TIMSK0，在 ATtiny25/45/85 上称为 TIMSK。

## 10.5.3.3 通用定时器中断项目

由于 ATtiny 头文件为中断向量地址定义了名称，因此可以更改前面的项目，使其同时适用于 ATtiny13(A) 和 ATtiny25/45/85。在 Microchip Studio 中创建 timer0_uni_int.asm 汇编语言项目，并将以下代码添加到 main.asm。此代码可在 ATtiny13(A) 和 ATtiny25/45/85 设备上运行，无需更改任何内容。

```
timer0_uni_int.asm : main.asm

.lfndef TIMSK
.equ TIMSK = TIMSK0
.endif

.org 0
rjmp main ; Reset vector

.org OCA0addr
rjmp ISR_tim0_compA ; Timer 0 compare match A interrupt vector

main:
sbi DDRB, DDB4 ; Pin PB4 as output pin
ldi r16, (1 << WGM01) ; CTC mode for timer
out TCCR0A, r16
ldi r16, 0x7F ; Output compare value
out OCR0A, r16
ldi r16, (1 << OCIE0A) ; Enable T0A compare match interrupt
out TIMSK, r16
sei ; Set global interrupt enable bit
ldi r16, (1 << CS02) | (1 << CS00) ; Prescaler CLK/1024 and start timer
out TCCR0B, r16

loop:
rjmp loop

; Timer 0 compare match A interrupt service routine or handler
ISR_tim0_compA:
sbi PINB, PINB4 ; Toggle LED
reti
```

