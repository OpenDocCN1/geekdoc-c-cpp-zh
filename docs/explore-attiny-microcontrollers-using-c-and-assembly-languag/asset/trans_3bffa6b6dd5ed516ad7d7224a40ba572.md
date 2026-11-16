
led_pinb_toggle_c : main.c

//#define F_CPU 1000000UL // 1MHz default clock for ATtiny25/45/85
#define F_CPU 1200000UL // 1.2MHz default clock for ATtiny13(A)
#include <avr/io.h>
#include <util/delay.h>

int main(void)
{
    DDRB = 0x0F;        // Set up pins PB0 to PB4 as output pins

    while(1) {
        _delay_ms(1000);  // LED on/off delay time
        PINB = 0x0F;      // Toggle LEDs on pins PB0 to PB4
    }
}

## 8.2.5 将 I/O 引脚配置为输入

当开关连接到微控制器引脚且该引脚配置为输入时，可以读取开关的状态来判断其是断开还是闭合。下一页的图 8.6 电路用于演示如何读取开关的状态。如果你有硬件，请在面包板上搭建电路。虽然图中显示电路使用了 debugWIRE，但拥有爱好者编程器的读者可以将其以 ISP/SPI 模式连接。使用 PB3 和 PB4 引脚分别连接开关和 LED，可将其他引脚留给 ISP/SPI 编程器。如果使用 Atmel-ICE，请继续以 debugWIRE 模式使用它。

图 8.6 电路中的开关 SW1 直接将 PB3 连接到 GND。在这种配置下，通常需要一个从 PB3 连接到 +5V 的上拉电阻，如图中灰显的电阻 R2 所示，以便当开关断开时引脚上的逻辑电平为逻辑 1。当开关闭合时，引脚连接到 GND，在引脚上呈现逻辑 0。上拉电阻可防止开关闭合时 +5V 被短路到 GND，同时允许开关断开和闭合时两种逻辑电平出现在引脚上。

由于 AVR 微控制器的每个引脚上都有内部上拉电阻，并且可以单独启用或禁用，因此我们不需要在引脚 PB3 上放置外部电阻。使用外部上拉电阻的唯一原因是需要更强的上拉电阻，即更低的上拉电阻值，例如 4k7 或 10k。ATtiny13(A) 和 ATtiny25/45/85 数据手册显示，内部上拉电阻相当弱且公差较大，规格为 20KΩ 至 50KΩ。这些内部上拉电阻值可在数据手册的电气特性部分找到。

![](img/83ef13a6c66cc7882b2f357e97f451dc_177_0.png)

在 Microchip Studio 中创建 read_switch_asm 汇编器项目，并将以下清单中的代码输入到 main.asm 中。该程序的作用是：如果开关闭合则点亮 LED，如果开关断开则熄灭 LED。由于电路中使用了上拉电阻，逻辑是反向的。开关闭合时读取 0，断开时读取 1。

```
read_switch.asm : main.asm

sbi   DDRB, DDB4        ; LED connected to PB4
cbi   DDRB, DDB3        ; Switch connected to PB3
sbi   PORTB, PORTB3     ; Enable pull-up on PB3

loop:
sbic  PINB, PINB3       ; Skip if switch closed
cbi   PORTB, PORTB4     ; Switch LED off
sbis  PINB, PINB3       ; Skip if switch open
sbi   PORTB, PORTB4     ; Switch LED on
rjmp  loop
```

在程序开头，使用 SBI 指令将引脚 PB4 设置为输出引脚，这与 LED 闪烁程序中所做的一样。CBI 用于清除 DDRB 寄存器中的一位，将引脚 PB3 设置为输入引脚，如代码清单中的第二条指令所示。虽然引脚默认为输入，但这条指令表明我们明确希望将此引脚用作输入，不过我们也可以省略这条指令，代码仍然可以工作。因为 PB3 已设置为输入引脚，所以使用 SBI 指令设置 PORTB 寄存器中的位 PORTB3 可启用引脚 PB3 上的内部上拉电阻。请回顾本章 8.2.1.8 节中的图 8.4，以查看控制 I/O 端口的寄存器和位，或参考所使用 ATtiny 器件的 AVR 数据手册。

在程序的主循环中，使用两条指令来测试引脚 PB3 上开关的状态，即 SBIC 和 SBIS。这两条指令都测试 PINB 寄存器中位 PINB3 的逻辑状态，如代码所示。位 PINB3 包含引脚 PB3 的逻辑状态，因为 PB3 已设置为输入引脚。图 8.7 的流程图显示了代码的功能。以下是对 SBIC 和 SBIS 用法的说明。

SBIC（如果 I/O 寄存器中的位被清除则跳过）指令：如果连接开关的引脚 PB3 处于逻辑电平 0（开关闭合），则跳过下一条指令。当开关断开时，由于启用了内部上拉电阻，PB3 处于逻辑电平 1。在这种情况下，下一条指令是 CBI 指令，用于关闭 LED，因此不会被跳过。这意味着当开关断开时，SBIC 后面的 CBI 指令会被执行，LED 被关闭。

SBIS（如果 I/O 寄存器中的位被置位则跳过）指令：如果 PB3 上施加了逻辑电平 1（开关断开），则跳过下一条指令。当开关断开时，由于上拉电阻，PB3 上施加了逻辑电平 1，导致下一条指令被跳过。如果开关闭合，PB3 上施加了逻辑电平 0，此时 SBIS 指令不跳过下一条指令。下一条指令（SBI）将 LED 点亮。

从程序中省略 SBIC 指令，在物理硬件上全速运行程序时似乎不会有什么区别。无论开关是断开还是闭合，LED 都会在循环顶部被关闭。当开关断开时，LED 永远不会被点亮。当开关闭合时，LED 会在循环顶部被关闭，并在循环底部被点亮。因为当开关闭合时 LED 关闭的时间非常短，然后随即点亮，所以在眼睛看来它似乎是持续点亮的。

使用硬件调试器和物理硬件，或 Microchip Studio 中的模拟器来启动程序并中断。使用调试器单步执行程序，以确保你理解 SBIC 和 SBIS 指令如何根据开关的状态进行决策。在单步执行代码时，闭合和断开开关。在开关闭合的情况下测试代码时，请记住在单步执行代码时保持开关闭合。

![](img/83ef13a6c66cc7882b2f357e97f451dc_179_0.png)

```
sbi DDRB, DDB4
cbi DDRB, DDB3
sbi PORTB, PORTB3
loop:
sbic PINB, PINB3
cbi PORTB, PORTB4
sbis PINB, PINB3
sbi PORTB, PORTB4
rjmp loop
```

图 8.7：read_switch_asm 项目的流程图

如果你使用的是模拟器，则需要通过更改 PINB 寄存器中相应位的状态来模拟开关的闭合和断开。为此，启动调试器，使用顶部菜单中的 Debug ▶ Windows ▶ I/O 打开 I/O 窗口，然后在 I/O 窗口中单击 I/O PORT (PORTB) 以显示 I/O 端口寄存器。在 I/O 窗口底部，单击 PINB 寄存器中的位 3 以更改其状态，这模拟了开关状态的改变。请记住，位编号从 0 开始而不是 1，因此位 3 是从右数的第四位。LED 的状态可以在 PORTB 寄存器的位 4（从右数的第五位）中查看。请注意，在 PINB 寄存器中，当位 3 为高电平时开关断开，当为低电平时开关闭合。这种反向逻辑可能有点令人困惑。在单步执行代码时，请务必仔细思考正在发生的事情。

以下清单中展示了与 read_switch_asm 项目功能等效的 C 程序，即 read_switch_c 项目的代码清单。这个程序基本上是不言自明的。前三条指令设置了 LED 引脚、开关引脚和内部上拉电阻，与汇编语言程序一样。在 if() 语句中，测试 PINB 寄存器中的位 PINB3 以查看开关是闭合还是断开。然后使用按位 AND 和 OR 运算符来关闭或打开 LED。

```
read_switch.c : main.c

#include <avr/io.h>

int main(void)
{
    DDRB  |= (1 << DDB4);    // Set PB4 pin as output for LED
    DDRB  &=~(1 << DDB3);    // Set PB3 pin as input for switch
    PORTB |= (1 << PORTB3);  // Enable pull-up on PB3 pin

    while (1) {
        if (PINB & (1 << PINB3)) {   // If pin is high, switch is open
            PORTB &=~(1 << PORTB4);  // Switch LED off
        } else {
            PORTB |= (1 << PORTB4);  // Switch LED on
        }
    }
}
```

以下清单中将原始 read_switch_asm 代码与反汇编的 read_switch_c 代码并列展示。在反汇编代码中，寄存器地址已替换为寄存器名称，指令地址已替换为标签，以便于阅读。

值得注意的是，反汇编代码比手写的汇编语言程序多一条指令。反汇编代码没有使用两条位测试和跳过指令，而是使用一条 SBIS 指令，并在其下方放置一条 RJMP 指令。因此，如果开关闭合，将发生跳转到 led_on 标签的操作，在该标签处 LED 被
