
## 10.10 电容表
考虑图P10.10的RC电路。电容器两端的电压为`Vc(t) = k e^(-t/RC)`。在一个时间常数`RC`中，此电压放电至`k/e`的值。对于特定的`R`值，电容器的值`C = T/R`，其中`T`是时间常数，可由`PIC18F4321`使用1 MHz内部时钟计数。设计`PIC18F4321`的硬件和软件，通过放大器使用脉冲为电容器充电至最高10V峰值电压。然后，`PIC18F4321`将停止给电容器充电，测量一个时间常数的放电时间，并计算电容器的值。

### (a) 绘制硬件原理图。

### (b) 编写一个C程序来实现上述功能。

## 10.11 设计一个基于PIC18F4321的系统，以测量2k电阻（图P10.11）吸收的功率。系统将输入2k电阻两端的电压(V)，使用`PIC18F4321`的片上A/D转换器将其转换为8位输入，然后使用`V²/R`计算功率。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_328_0.png)

图P10.10

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_328_1.png)

图P10.11

# 11 PIC18F CCP和串行I/O

在本章中，我们描述使用汇编和C语言编程`PIC18F`片上外设的基础知识。主题包括`PIC18F` `CCP`（捕获/比较/脉宽调制）和串行I/O模块。

## 11.1 PIC18F CCP（捕获/比较/脉宽调制（PWM）模块

`CCP`模块在`PIC18F4321`中作为片上功能实现，用于提供基于时间的脉冲信号的测量和控制。`Timer1`到`Timer3`用于此目的。`CCP`模块不使用`Timer0`。任何复位都会关闭`CCP`模块。

`PIC18F4321`包含两个`CCP`（捕获/比较/脉宽调制）模块，即`CCP1`和`CCP2`。`PIC18F4321`的`CCP1`模块被实现为具有增强PWM功能的标准`CCP`，以更好地控制直流电机。因此，`PIC18F4321`中的`CCP1`模块也称为`ECCP`（增强型`CCP`）。`CCP2`模块提供标准的捕获、比较和PWM功能。请注意，`CCP1`和`CCP2`是两个模块。因此，可以同时将`CCP1`设置为PWM，`CCP2`设置为捕获或比较（反之亦然），因为它们是独立的两个模块。可能无法使用同一个`CCP`模块（例如`CCP1`）同时进行捕获（或比较）和PWM。这是因为，虽然定时器可能不同（`Timer1`，`Timer3`），但其他逻辑功能是共享的。在接下来的讨论中，`CCP1`和`CCP2`模块将被称为`CCPx`。

`CCP`模块可以被编程为以下模式之一：

- 捕获模式（`CCPx`引脚通过编程配置为输入）
- 比较模式（`CCPx`引脚通过编程配置为输出）
- PWM模式（`CCPx`引脚通过编程配置为输出）

`PIC18F`捕获模式在检测到脉冲的第n个上升沿或下降沿时，将16位定时器（`Timer1`或`Timer3`）的内容写入16位寄存器（`CCPRxH:CCPRxL`，由`CCPx`模块提供）。捕获模式可用于测量两个事件之间经过的时间。典型事件包括检测连接到`CCPx`引脚的周期性波形的每个下降沿或每个上升沿。通过捕获两个连续的上升沿，然后减去它们的值，可以得到波形的周期。因此，捕获模式可用于测量传入周期性波形的周期。

`PIC18F`比较模式非常类似于秒表的计时功能。请注意，秒表加载了一个由用户确定的预设时间。开始秒表后，它从预设值倒数到0。`PIC18F`比较模式以类似的方式工作，只不过它是从0计数到预设值。`PIC18F`比较

比较模式（Compare mode）可用于在指定时间量之后，开启或关闭连接到 `CCPx` 引脚的设备。这可以通过在指定的定时器值（`Timer1` 或 `Timer3`）与 16 位寄存器值（`CCPRxH:CCPRxL`）匹配时，立即输出一个信号（例如，通过编程 `CCPxCON` 寄存器输出高电平或低电平）来实现。因此，利用比较模式，可以将 `PIC18F` 编程为在特定的时间延迟后在 `CCPx` 引脚上输出信号。例如，在化工厂中，可以利用比较模式在储罐注水 50 秒后关闭水泵。

`PIC18F` 的脉宽调制（PWM）模式可用于在 `CCPx` 引脚上生成具有用户指定频率和占空比的方波。请注意，占空比定义为脉冲在一个时钟周期内处于高电平时间的百分比。此外，随着 PWM 信号占空比的增加，PWM 提供的平均电压和功率也会增加。由于这一特性，PWM 模式可用于调光 LED 和控制无刷直流电动机转速等应用。这意味着，随着 PWM 占空比的增加，LED 会更亮，电动机转速也会提高；反之，当 PWM 占空比较低时，LED 会变暗，电动机转速也会降低。

轮询 I/O 和中断 I/O 都可以用于 `CCP` 模块。本节将提供使用轮询 I/O 的 `CCP1` 模块示例。请注意，在捕获和比较模式的轮询 I/O 中，`PIR1` 寄存器中的 `CCPxIF` 标志位在等待循环中被监控，而在 PWM 模式下，`T2CON` 寄存器中的 `TMR2IF` 标志位在等待循环中被检查。

### 11.1.1 CCP 寄存器

每个 `CCP` 模块都配有一个 8 位控制寄存器（`CCPxCON`），如图 11.1 所示。`CCPxCON`（x = 1 或 2）可用于选择三种模式之一，即比较模式、捕获模式或 PWM 模式。

每个 `CCP` 模块还包含一个 16 位数据寄存器（`CCPRx`）。该 16 位数据寄存器由两个 8 位寄存器组成：`CCPRxL`（低字节）和 `CCPRxH`（高字节）。该 16 位数据寄存器可用作 16 位捕获寄存器、16 位比较寄存器或 8 位 PWM 寄存器（`CCPRxL`，保存占空比的 8 位小数部分）。

### 11.1.2 CCP 模块及相关定时器

`CCP` 模块根据所选模式使用定时器 1、2 或 3。在捕获和比较模式下，`Timer1` 和 `Timer3` 可供模块使用，而在 PWM 模式下，`Timer2` 可供模块使用。特定定时器分配给模块的方式由 `T3CON` 寄存器中的 Timer to CCP 使能位决定（图 10.11）。表 11.1 总结了 `CCP1` 模块中各模式的定时器分配情况。

### 11.1.3 PIC18F4321 捕获模式

在捕获模式下，当相应的 `CCPx` 引脚上发生事件（例如每个上升沿或下降沿）时，`CCPRxH:CCPRxL` 寄存器对会捕获 `TMR1` 或 `TMR3` 寄存器的 16 位值。该事件由模式选择位 `CCPxM3:CCPxM0`（`CCPxCON` 的 3-0 位，图 11.1）选择。当捕获发生时，`CCPx` 中断标志位（例如 `PIR1` 寄存器中的 `CCP1IF`，图 10.8）被置为 1；必须在软件中将其清零。如果在读取 `CCPRx` 寄存器值之前发生另一次捕获，旧的捕获值将被新的捕获值覆盖；因此，应保存旧的捕获值。

#### 表 11.1 PIC18F4321 CCP1 模块的定时器分配

| 所选 CCP 模式 | 定时器 |
| :--- | :--- |
| 捕获模式 | `Timer1` 或 `Timer3` |
| 比较模式 | `Timer1` 或 `Timer3` |
| PWM 模式 | `Timer2` |

在捕获模式下，应通过将相应的 `TRISx` 方向位置位，将 `PIC18F4321` 的 `CCPx` 引脚配置为输入。此外，与捕获模式一起使用的定时器（`Timer1` 或 `Timer3`）必须运行在定时器模式。每个 `CCP` 模块使用的定时器（`Timer1` 或 `Timer3`）通过 `T3CON` 寄存器（图 10.11）选择。

综上所述，可以使用以下步骤将 `PIC18F4321` 编程为捕获模式，以确定波形的周期（假设使用 `CCP1`；`CCP2` 的过程类似）：

- 1. 将适当的数据加载到 `CCP1CON` 寄存器（图 11.1）中，以配置捕获模式。
- 2. 使用 `TRISC` 寄存器将 `CCP1` 配置为输入引脚。请注意，`CCP1` 引脚与 `RC2` 引脚复用。
- 3. 通过将适当的数据加载到 `T3CON` 寄存器（图 10.11）中，为捕获模式选择 `Timer1` 或 `Timer3`。`T1CON` 不用于选择 `Timer1`。相反，仅使用 `T3CON` 来选择 `Timer1` 或 `Timer3`。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_331_0.png)

bit 7-6 **未实现**：读值为 '0'

bit 5-4 **`DCxB1:DCxB0`**：`CCP` 模块 x 的 PWM 占空位 1 和位 0

- 捕获模式：未使用。
- 比较模式：未使用。
- PWM 模式：这些位是 10 位 PWM 占空比的低两位（位 1 和位 0）。占空比的高 8 位（`DCx9:DCx2`）位于 `CCPRxL` 中。

bit 3-0 **`CCPxM3:CCPxM0`**：`CCPx` 模块模式选择位

- 0000 = 禁用捕获/比较/PWM（复位 `CCP` 模块）
- 0001 = 保留
- 0010 = 比较模式，匹配时切换输出（`CCPxIF` 位被置位）
- 0011 = 保留
- 0100 = 捕获模式，每个下降沿
- 0101 = 捕获模式，每个上升沿
- 0110 = 捕获模式，每第 4 个上升沿
- 0111 = 捕获模式，每第 16 个上升沿
- 1000 = 比较模式：初始化 `CCP` 引脚为低电平；比较匹配时，强制 `CCP` 引脚为高电平（`CCPxIF` 位被置位）
- 1001 = 比较模式：初始化 `CCP` 引脚为高电平；比较匹配时，强制 `CCP` 引脚为低电平（`CCPxIF` 位被置位）
- 1010 = 比较模式：比较匹配时产生软件中断（`CCPxIF` 位被置位，`CCP` 引脚反映 I/O 状态）
- 1011 = 比较模式：触发特殊事件，复位定时器，`CCPx` 匹配时启动 A/D 转换（`CCPxIF` 位被置位）
- 11xx = PWM 模式

#### 图 11.1 CCPxCON 寄存器

- 4. 捕获后清除 `CCP1IF` 标志：对于 `CCP1` 清除 `CCP1IF` 位（图 10.8 中的 `PIR1` 寄存器），或对于 `CCP2` 清除 `CCP2IF` 位（图 10.12 中的 `PIR2` 寄存器），以便可以进行下一次捕获。
- 5. 将 `CCPR1H` 和 `CCPR1L` 清零。
- 6. 检查 `PIR1` 中的 `CCP1IF` 标志，并在循环中等待直到 `CCP1IF` 为 1 以检测第一个上升沿。一旦检测到第一个上升沿，使用 `T1CON` 启动 `Timer1`（或使用 `T3CON` 启动 `Timer3`）。
- 7. 将 `CCPR1H` 和 `CCPR1L` 保存到数据存储器中，例如 `REGX` 和 `REGY`。
- 8. 将 `CCP1IF` 清零。
- 9. 检查 `PIR1` 中的 `CCP1IF` 标志，并在循环中等待直到 `CCP1IF` 为 1 以检测第二个上升沿。一旦检测到第二个上升沿，停止 `Timer1`（或 `Timer3`）。
- 10. 通过清除 `CCP1CON` 寄存器禁用捕获。
- 11. 执行 16 位减法：[`CCPR1H:CCPR1L`] - [`REGX:REGY`]，并将结果存储在 [`REGX:REGY`] 中。
- 12. 寄存器对 [`REGX:REGY`] 中的 16 位结果将包含输入波形的周期，以时钟周期数表示。

捕获模式的典型应用包括：

- 通过捕获脉冲的后续前导（上升）或后沿（下降）沿来测量未知周期信号的脉冲宽度。
- 通过捕获两个后续的上升沿或下降沿来测量信号的周期。
- 测量占空比。请注意，占空比定义为 `$(t_1/T) \times 100$`，其中 `t_1` 是信号在一个周期 `T` 内处于高电平的时间分数。

#### 例 11.1 假设使用 PIC18F4321。

- (a) 编写一段 `PIC18F` 汇编语言程序，位于地址 `0x200`，用于测量连接到 `CCP1` 引脚的输入周期波形的周期（以时钟周期数表示）。将结果存储在寄存器 `0x21`（高字节）和 `0x20`（低字节）中。使用 `Timer3` 和 `CCP1` 的捕获模式。
- (b) 编写一段 C 语言程序，用于测量连接到 `CCP1` 引脚的输入周期波形的周期（以时钟周期数表示）。使用 `Timer3` 和 `CCP1` 的捕获模式。

##### 解答

- (a) `PIC18F` 汇编语言程序如下所示：

```asm
INCLUDE <PIC18F4321.INC>
        ORG     0x200
        MOVFW B'00000101'       ; 选择上升沿捕获模式
        MOVWF CCP1CON
        BSF     TRISC, CCP1     ; 将 CCP1 引脚配置为输入
        MOVFW B'01000000'       ; 选择 TIMER3 作为捕获时钟源
        MOVWF T3CON             ; 选择 TIMER3 内部时钟，1:1 预分频
                                ; TIMER3 关闭
        CLRF  CCPRIH            ; 将 CCPRIH 清零
        CLRF  CCPRIL            ; 将 CCPRIL 清零
        BCF   PIR1, CCP1IF      ; 清除 CCP1IF
```

##### 示例 11.1

等待 `CCP1` 的第一个上升沿。

```
WAIT  BTSS  PIR1, CCP1IF ; Wait for the first rising edge
GOTO WAIT
BSF T3CON, TMR3ON ; Turn Timer3 ON
MOVFF CCPR1L, 0x20 ; Save CCPR1L in 0x20 at 1st rising edge
MOVFF CCPR1H, 0x21 ; Save CCPR1H in 0x21 at 1st rising edge
BCF PIR1, CCP1IF ; Clear CCP1IF
WAIT1 BTSS PIR1, CCP1IF ; Wait for next rising edge
GOTO WAIT1
BCF T3CON, TMR3ON ; Turn OFF Timer3
CLRF CCP1CON ; Disable capture
MOVF 0x20, W ; Move 1st Low byte to WREG
SUBWF CCPR1L, F ; Subtract WREG from 2nd low byte
; Result in 0x20
MOVF 0x21, W ; Move 1st HIGH byte to WREG
SUBWFB CCPR1H, F ; Subtract WREG with borrow
; from 2nd high byte, result in 0x21
SLEEP ; Halt
END
```

(b)

```c
#include <pic18f4321.h>
void main(void)
{
  unsigned char FIRST_CCPR1L, FIRST_CCPR1H, HIGH_BYTE, LOW_BYTE;
  CCP1CON = 0x05; // Select capture mode rising edge
  TRISCbits.TRISC2 = 1; // Configure RC2/CCP1/PIO pin as input
  T3CON = 0x40; // Select TIMER3 as clock source for capture
  CCPR1H = 0x00; // Clear CCPR1H to 0
  CCPR1L = 0x00; // Clear CCPR1L to 0
  PIR1bits.CCP1IF = 0; // Clear CCP1IF

  while (PIR1bits.CCP1IF == 0); // Wait for the first rising edge
  T3CONbits.TMR3ON = 1; // Turn Timer3 ON
  FIRST_CCPR1L = CCPR1L; // Save CCPR1L in FIRST_CCPR1L at 1st rising edge
  FIRST_CCPR1H = CCPR1H; // Save CCPR1H in FIRST_ at 1st rising edge
  PIR1bits.CCP1IF = 0; // Clear CCP1IF

  while (PIR1bits.CCP1IF == 0); // Wait for next rising edge
  T3CONbits.TMR3ON = 0; // Turn OFF Timer3
  CCP1CON = 0x00; // Disable capture
  LOW_BYTE = CCPR1L - FIRST_CCPR1L; // Low byte of result
  HIGH_BYTE = CCPR1H - FIRST_CCPR1H; // High byte of result

  while(1); // Halt
}
```

如前所述，为了在实验室中实现 `PIC18F` 汇编程序中的 I/O 程序，例如示例 11.1(a)，应在 `PIC18F` 汇编语言程序中在 `"#include <p18f4321.inc>"` 语句之后，使用汇编器指令 `"config"` 插入以下配置命令，如下所示：

```
include <p18f4321.inc>
config OSC = INTIO2 ; Select internal oscillator
config WDT = OFF ; Watch Dog Timer OFF
config LVP = OFF ; Low Voltage Programming OFF
config BOR = OFF ; Brown Out Reset OFF
```

同样地，为了在实验室中使用 C 语言实现 I/O 程序，例如示例 11.1(b)，应在 C 程序中在 `#include <p18f4321.h>` 之后使用指令 `"#pragma config"` 插入以下配置命令，如下所示：
