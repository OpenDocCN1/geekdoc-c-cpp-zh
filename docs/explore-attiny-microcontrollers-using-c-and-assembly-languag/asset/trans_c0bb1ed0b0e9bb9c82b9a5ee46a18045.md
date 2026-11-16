

wait_ms_macro:
    subi    R16, 1
    sbci    R17, 0
    sbci    R18, 0
    sbci    R19, 0
    mov     R20, R16
    or      R20, R17
    or      R20, R18
    or      R20, R19
    breq    SREG_Z, wait_ms_macro
    ret     ; 4 clock cycles, but is effectively 3 clock cycles

在上述代码中，循环之外的唯一指令是 RET 指令。该指令在 PC 宽度小于 22 位的 AVR CPU 上执行需要 4 个时钟周期。BRBC 通常消耗 2 个时钟周期，但在最后一次执行时仅消耗 1 个时钟周期。因此，我们从循环外消耗的时钟周期中借用 1 个时钟周期，使得 BRBC 最后一次执行也有效地消耗 2 个时钟周期。出于这个原因，我们从 RET 中减去 1 个时钟周期，使其有效地消耗 3 个时钟周期，而非 4 个。将这 3 个时钟周期加上宏主体中累计的 27 个时钟周期，得到 wait_ms_macro 循环外总共消耗 30 个时钟周期。在之前的项目代码中，延迟子程序循环外仅消耗了 10 个时钟周期。由于我们没有简化计算延迟子程序循环次数的公式，可以直接将计算中的 10 个周期替换为 30，如下面的代码所示。

```
ldi    R16, low (((((F_CPU * (@0) / 1000) - 30) / 10))
```

由于循环外的时钟周期正好为 30，是 10 的倍数，因此无需保留之前添加到代码中的 NOP 指令。这些 NOP 指令之前被添加，目的是使循环外的时钟周期总和达到 10。

由于上述计算中的某个值发生了变化，我们需要重新计算时间延迟宏和子程序可工作的最小 CPU 频率。我们使用下面的公式，与之前使用的相同。

![](img/83ef13a6c66cc7882b2f357e97f451dc_256_0.png)

已知 t_ms 的最小值为 1ms。C_T 的最小值是在延迟子程序中执行一遍时取得。该值现在为 40 个时钟周期，由子程序循环外的 30 个周期加上循环内 1 次迭代的 10 个周期组成。将这些值代入公式，得到如下结果。

f_{CPU} = \frac{10000(40+1)}{1}
= 410000

计算结果为 410kHz，该值用于宏顶部用于测试 F_CPU 限制的代码中，如下所示。

```
...
.elif (F_CPU < 410000)
    .error "F_CPU too low for M_WAIT_MS macro. Minimum 410kHz"
.elif (@0 < 1)
    .error "Time delay too low for M_WAIT_MS macro. Minimum 1ms"
...
```

回顾下面重复的 main.asm，可以看到 wait_ms_macro.inc 在使用宏的代码顶部被包含。这使得宏在 main.asm 文件中可用。尽管 F_CPU 在 wait_ms_macro.inc 中被使用，但它是在包含 wait_ms_macro.inc 之后定义的。之所以这不会导致错误，是因为汇编器是多遍汇编器。这意味着在第一遍遍历文件时，汇编器会构建符号表。这样，当它再次遍历源代码时，就知道 F_CPU 了。这通常称为前向引用。

```
wait_ms_macro.asm : main.asm

.include "wait_ms_macro.inc"
.equ    F_CPU    = 1000000

start:
    sbi     DDRB, DDB4        ; Set pin PB4 as output

loop:
    sbi     PORTB, PORTB4    ; Set LED pin high
    mWAIT_MS 200             ; LED on delay
    cbi     PORTB, PORTB4    ; Clear LED pin low
    mWAIT_MS 500             ; LED off delay
    rjmp    loop

.include "wait_ms_macro.asm"
```

由于我们的 M_WAIT_MS 宏调用了 wait_ms_macro 子程序，因此包含该子程序的文件必须在使用 M_WAIT_MS 宏的文件底部被包含。

当宏在程序中被使用时，宏会在使用它的代码位置被展开。宏展开意味着构成宏的代码会被实际粘贴到宏被使用的位置。下面的代码展示了之前代码中使用的宏是如何被展开的。

```
00000000 sbi DDRB, DDB4 ; Set pin PB4 as output
loop:
00000001 sbi PORTB, PORTB4 ; Set LED pin high
M_WAIT_MS 200 ; LED on delay
00000002 push R16
00000003 push R17
00000004 push R18
00000005 push R19
00000006 push R20
00000007 ldi R16, 0x1D
00000008 ldi R17, 0x4E
00000009 ldi R18, 0x00
0000000A ldi R19, 0x00
0000000B rcall wait_ms_macro
0000000C pop R20
0000000D pop R19
0000000E pop R18
0000000F pop R17
00000010 pop R16
00000011 cbi PORTB, PORTB4 ; Clear LED pin low
M_WAIT_MS 500 ; LED off delay
00000012 push R16
00000013 push R17
00000014 push R18
00000015 push R19
00000016 push R20
00000017 ldi R16, 0x4D
00000018 ldi R17, 0xC3
00000019 ldi R18, 0x00
0000001A ldi R19, 0x00
0000001B rcall wait_ms_macro
0000001C pop R20
0000001D pop R19
0000001E pop R18
0000001F pop R17
00000020 pop R16
00000021 rjmp loop
```

如上述清单所示，宏在被使用的两个位置被展开。宏中的代码基本上被粘贴到宏被使用的两个位置。这段代码包括所用寄存器的压栈和出栈、用于将延迟计数值加载到寄存器中的 LDI 指令，以及对 wait_ms_macro 子程序的调用。每次使用宏时，完整的宏代码都会替换到其位置。wait_ms_macro 子程序只有一个实例，由两个展开的宏调用。wait_ms_macro 子程序的代码如下清单所示。通过调用 wait_ms_macro，而不是将此代码直接包含在宏中，我们节省了一些内存空间。如果将 wait_ms_macro 代码放在宏中，而不是作为子程序调用，那么每次使用它时都会被完全展开。这将占用额外的内存。

```
wait_ms_macro:
00000022 subi R16, 1
00000023 sbci R17, 0
00000024 sbci R18, 0
00000025 sbci R19, 0
00000026 mov R20, R16
00000027 or R20, R17
00000028 or R20, R18
00000029 or R20, R19
0000002A breq SREG_Z, wait_ms_macro
0000002B ret
```

之所以不能将 PUSH 和 POP 指令放入 wait_ms_macro 子程序，是因为被压栈的寄存器必须在宏中加载值，否则我们就只是又一个固定时间子程序。这意味着这些寄存器在宏中被修改，因此必须在修改前压栈。

乍一看，似乎可以将 POP 指令放入子程序，而不是留在宏中，但这不可能。实际情况是，寄存器首先被压栈，然后通过加载要传递给子程序的值来修改。在随后调用子程序时，子程序的返回地址会自动压栈。如果我们随后在从子程序返回之前尝试弹出寄存器，我们实际上会先弹出子程序的返回地址，因为它是最后压栈的内容。当子程序返回并自动从栈中弹出其返回地址时，实际上会弹出最初压栈的前两个寄存器的值。显然，这会导致子程序返回到错误的地址，从而导致程序故障。

最后请注意，M_WAIT_MS 宏为 10 的倍数的值生成周期精确的延迟。这可以再次使用 Microchip Studio 中的模拟器进行检查。

## 10.3 从 C 代码调用汇编子程序

从 C 代码程序调用汇编语言子程序很容易。从 C 代码调用子程序时，最重要的信息是用于向子程序传递值的寄存器和用于从子程序返回值的寄存器。即使对于同一微控制器，不同 C 编译器的寄存器用法也可能不同。此信息可在名为 Atmel AT1886: Mixing Assembly and C with AVRGCC 的应用笔记中找到，适用于 avr-gcc 编译器，可从以下网址获取：ww1.microchip.com/downloads/en/Appnotes/doc4255.pdf

在下一节中将要展示的示例中，汇编语言子程序从 C 代码被调用并传递了一个 32 位值。在再下一节中，从 C 代码调用的汇编语言子程序返回一个值。

### 10.3.1 向汇编子程序传递值（从 C）

以下子程序代码取自本章 10.2.4.2 节的 wait_ms_macro_asm 项目。对代码进行了一些修改，以便 C 程序能够调用汇编语言子程序。该子程序是我们放入宏中的代码，用于生成可变的毫秒级时间延迟。在修改后的代码中，该子程序称为 wait_ms，因为这个名称简短且具有描述性。不要将此子程序与之前同名的子程序混淆。该项目包含三个文件。在 Microchip Studio 中创建一个名为 wait_ms.c 的新 GCC C 可执行项目。将项目中 main.c 的代码替换为以下代码。

```
wait_ms_c : main.c

#define F_CPU 12000000

#include <avr/io.h>
#include "wait_ms.h"

int main(void)
{
    DDRB |= (1 << DDB4);    // Set up pin PB4 as an output

    while (1)
    {
        PORTB |= (1 << PORTB4);    // Set pin high (LED on)
        wait_ms(WAIT_MS_TIME(200));    // LED on delay
        PORTB &= ~(1 << PORTB4);    // Set pin low (LED off)
        wait_ms(WAIT_MS_TIME(1000));    // LED off delay
    }
}
```

