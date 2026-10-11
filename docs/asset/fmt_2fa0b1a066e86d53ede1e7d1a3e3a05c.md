
```c
ADCON1 = 0x0F; // 配置端口 A、B 和 E 为数字 I/O
TRISA bits. TRISA0 = 0; // PORTA 的 bit0 是输出
TRISBbits. TRISB1 = 0; // PORTB 的 bit1 是输出
TRISEbits. TRISE1 = 0; // PORTE 的 bit1 是输出
```

### 8.2.4 接口 LED（发光二极管）和七段显示器

PIC18F 可以吸收或提供足够的电流，使得 LED 和七段显示器无需像 `74HC244` 那样的缓冲器（电流放大器）即可连接到 PIC18F。LED 可以通过两种方式连接。图 8.12(a) 和 (b) 展示了这些配置。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_224_0.png)

图 8.12 LED 与 PIC18F 的接口

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_224_1.png)

图 8.13 七段显示器

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_224_2.png)

图 8.14 七段显示器配置

在图 8.12(a) 中，PIC18F 输出高电平以点亮 LED；输出‘低电平’以关闭 LED。在图 8.12(b) 中，PIC18F 输出低电平以点亮 LED；输出‘高电平’以关闭 LED。此外，当 LED 点亮时，典型的电流为 10 mA，LED 上的压降为 1.7V。因此，

R = (5 - 1.7) / 10 mA = (5 - 1.7) / 10 mA = 330

如第 3 章所述，七段显示器可用于显示例如 0 到 9 的十进制数。“七段”这一名称源于显示屏每个段都有一个 LED 这一事实，共有七个 LED。图 8.13 展示了一个典型的七段显示器。

图 8.14 展示了两种不同的七段显示器配置，即共阴极和共阳极。请注意，图 8.13 和 8.14 是为方便起见从第 3 章重绘的。在图 8.13 中，每个段包含一个 LED。通过打开或关闭相应的段，可以显示 0 到 9 的所有十进制数。例如，可以通过关闭段 g 中的 LED 并打开段 a 到 f 中的其他六个 LED 来显示零。七段显示器有两种类型：共阴极和共阳极。在共阴极配置中，微控制器可以编程为发送高电平以点亮段，发送低电平以关闭段。相反，在共阳极配置中，微控制器可以发送低电平以点亮段，发送高电平以关闭段。在两种配置中，都可以使用 R = 330 欧姆的电阻。

图 8.15 展示了 `PIC18F4321` 与共阴极七段显示器通过 `PORT C` 的典型接口。`PORT C` 的每一位通过一个 330 欧姆电阻连接到七段显示器的一个段。请注意，图中未显示这七个电阻。共阳极七段显示器也可以类似地连接到 `PIC18F4321`。

### 8.2.5 使用 PIC18F 汇编语言的编程 I/O 示例

本节包含使用 PIC18F 汇编语言的编程 I/O 示例。如前所述，为了使程序正常工作，在“`<include p18F4321.inc>`”语句之后，所有编程示例中应包含以下“config”语句：

```assembly
include <p18F4321.inc>
config OSC = INTIO2 ; 选择内部振荡器
config WDT = OFF ; 看门狗定时器关闭
config LVP = OFF ; 低电压编程关闭
config BOR = OFF ; 欠压复位关闭
```

请注意，在上述代码中，指令“`include`”将在汇编语言程序中引入文件“`p18F4321.inc`”。文件“`p18F4321.inc`”包含在 P18f 汇编语言程序中使用的标准库例程。上述语句“`include <p18F4321.inc>`”指示 MPLAB 汇编器将文件“`p18F4321.inc`”中的源代码包含到程序中。文件 `p18f4321.inc` 是 `PIC18F4321` 专用文件，主要包含用于访问 `PIC18F4321` 特殊功能寄存器（SFR）的变量的定义。例如，`PIC18F4321` 的 `PORTA` 被映射为数据内存地址为 `0xF80` 的特殊功能寄存器（SFR）。“`p18F4321`”文件包含此信息。这意味着用户可以在 C 程序中使用 `PORTA`。

编译器在编译过程中遇到程序中的 `PORTA` 时，会插入地址 `0xF80`。

上述中的 "`config`" 指令告知 MPLAB 汇编器在汇编之前执行特定操作。该指令可用于打开或关闭某些片上设备。例如，放置在 "`include`" 指令之后的语句 "`config WDT = OFF`" 将关闭看门狗定时器。

#### 示例 8.1

编写一个位于 `0x100` 的 PIC18F 汇编语言程序，根据图 8.16 中连接到 `Port C` bit 0 的开关输入，驱动连接到 `Port D` bit 0 的 LED。如果开关断开，则关闭 LED；如果开关闭合，则点亮 LED。

#### 解答

根据图 8.16，由于 LED 的阴极连接到 `Port C` 的 bit 0，`PIC18F4321` 输出‘0’将点亮 LED，输出‘1’将关闭它。PIC18F 吸收（针对低电平输出）足够的电流以打开或关闭 LED，无需 `74HC244` 等任何缓冲器；仅需要限流电阻 R = 330 欧姆。

PIC18F 汇编语言程序如下所示：

```assembly
INCLUDE       <P18F4321.INC>
ORG           0x100
BSF           TRISC, TRISCO  ; 将 Port C 的 bit 0 配置为输入
BCF           TRISD, TRISD0 ; 将 Port D 的 bit 0 配置为输出
START  MOVF    PORTC, W     ; 将 PORTC 输入到 WREG
        MOVF    W, PORTD     ; 将开关输入输出到 LED
        BRA     START        ; 重复
        END
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_226_0.png)

**图 8.15**

`PIC18F4321` 通过 `PORT C` 接口到共阴极七段显示器

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_226_1.png)

**图 8.16**

示例 8.1 的图

在上述中，由于开关和 LED 数据是对齐的（两者分别连接到各自端口的 bit 0），`MOVF PORTC, PORTD` 指令直接从 `PORTC` 的 bit 0 输入开关输入，并输出到 `PORTD` 的 bit 0。此外，使用 `BRA START` 的无限循环将使循环持续进行。这意味着，在上述程序执行一次后，只要按下开关，LED 就会自动打开和关闭。然而，如果在程序末尾放置 `SLEEP` 或 `FINISH BRA FINISH`，程序将在手动复位激活时执行一次。每次按下图 8.16 中的开关，都必须通过激活手动复位重新执行上述程序。

#### 示例 8.2

需要一个 `PIC18F4321` 微控制器，根据连接到 `Port D` 的 bit 6 和 bit 7 的两个开关输入，驱动连接到 `Port C` bit 7 的 LED。如果两个开关相等（均为高电平或低电平），则点亮 LED；否则关闭 LED。假设高电平点亮 LED，低电平关闭 LED。编写一个位于 `0x200` 的 PIC18F 汇编程序来实现此功能。

#### 解答

```assembly
INCLUDE <P18F4321.INC>
ORG     0x200
BCF     TRISC, TRISC7 ; 将 PORTC 的 bit 7 配置为输出
SETF    TRISD         ; 将 PORTD 配置为输入端口
BACK    MOVF    PORTD, W ; 将 PORTD 输入到 WREG
        ANDLW 0xC0    ; 保留 bit 6 和 7
BZ      LEDON         ; 如果两个开关都是低电平，点亮 LED
        SUBLW 0xC0    ; 如果两个开关都是高电平，点亮 LED
BZ      LEDON
BCF     PORTC, RC7 ; 关闭 LED
BRA     DOWN
LEDON   BSF     PORTC, RC7 ; 点亮 LED
DOWN    BRA     BACK
END
```

#### 示例 8.3

图 8.17 中所示的 `PIC18F4321` 微控制器需要通过连接到 `PORTA` bit 0 到 bit 3 的四个开关输入一个 BCD 数（0–9），然后将 BCD 数字输出到连接到 `PORTB` bit 0 到 bit 6 的共阳极七段显示器。编写一个位于地址 `0x70` 的 PIC18F 程序，通过将七段代码存储在从地址 `0x100` 开始的数据内存中来完成此任务。

#### 解答

为了找到显示器的适当值，可以从图 8.17 中获得包含每个 BCD 数字的七段代码的表格（也称为“查找表”），如下所示：

### 8.2.6 使用 C 语言的程序化 I/O 示例

g f e d c b a 十六进制：

| | g | f | e | d | c | b | a | 十六进制 |
|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0x40 |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 0x79 |
| 2 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0x24 |
| 3 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0x30 |
| 4 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0x19 |
| 5 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0x12 |
| 6 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0x03 |
| 7 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0x78 |
| 8 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0x00 |
| 9 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0x18 |

请注意，对于共阳极七段显示器，‘0’ 会点亮段，而 ‘1’ 会熄灭段。此外，假设 `PORTB` 的第 7 位为 ‘0’。上述表格必须使用 `MOVLW` 和 `MOVWF` 指令存储在数据存储器中，或者使用 MPLAB 汇编器指令 `DB` 配合 PIC18F 汇编语言指令 `TBLRD`（表格读取）以及适当的寻址模式来存储。

PIC18F 汇编语言程序如下所示：

```assembly
INCLUDE <P18F4321.INC>
ORG 0x70
MOVLW 0x40 ; Store 7-segment codes
MOVWF 0x100
MOVLW 0x79
MOVWF 0x101
MOVLW 0x24
MOVWF 0x102
MOVLW 0x30
MOVWF 0x103
MOVLW 0x19
MOVWF 0x104
MOVLW 0x12
MOVWF 0x105
MOVLW 0x03
MOVWF 0x106
MOVLW 0x78
MOVWF 0x107
MOVLW 0x00
MOVWF 0x108
MOVLW 0x18
MOVWF 0x109
MOVLW 0x0F ; Configure PORTA as input
MOVWF ADCON1
CLRF TRISB ; Configure PORTB as output
LFSR 0, 0x100 ; Initialize FSR0 with the starting
; address of lookup table
LOOP MOVF PORTA, W ; Input switch data to the WREG
ANDLW B'00001111' ; Mask the lower 4-bits
MOVF PLUSW0, PORTB ; Output BCD data to PORTB
BRA LOOP ; Loop
END
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_228_0.png)

**图 8.17** 示例 8.3 的电路图

在继续之前，以下将讨论典型 C 程序的基本特性总结：

#### 预处理器指令

C 预处理器指令是 C 编译器的一部分。预处理器的目的是执行与预处理器相关的特定命令。这些预处理器不是 C 语言的一部分。相反，它们是 C 编译器软件的一部分。每个预处理器指令都以符号 `#` 开头。

在编译 C 程序之前，C 编译器首先启动预处理器软件模块的执行。该模块随后遍历程序以查找“`#`”符号。如果找到符号“`#`”，预处理器模块执行由该命令指定的功能。然后 C 编译器可以开始编译程序。

典型的预处理器指令是“`#include`”、“`#define`”和“`#pragma config`”。“`#include`”预处理器指令将文本（命令、注释等）从另一个文档转移到程序中。例如，考虑

```c
#include <p18f4321.h>
```

在上面，扩展名 `.h` 表示头文件。注意，头文件包含在 C 程序中使用的标准库函数。上述语句指示编译器将文件 `p18f4321.h` 中的源代码包含到程序中。文件 `p18f4321.h` 是 `PIC18F4321` 专用的头文件，主要包含用于访问 `PIC18F4321` 的特殊功能寄存器（SFRs）的变量定义。例如，`PIC18F4321` 的 `PORTA` 被映射为具有数据存储器地址 `0xF80` 的特殊功能寄存器（SFR）。头文件包含此信息。这意味着用户可以在 C 程序中使用 `PORTA`。编译器在编译时遇到程序中的 `PORTA` 时，会插入地址 `0xF80`。

“`#define`”预处理器指令可用于声明常量。例如，考虑

```c
#define y 4
```

“`#define`”预处理器将 4 分配给 `y`。使用预处理器“`#define`”定义的常量是在程序编译之前执行的文本替换。

“`#pragma config`”预处理器指令告诉编译器在编译之前执行特定操作。该指令可用于打开或关闭某些片上设备。例如，放置在“`#include`”指令之后的语句“`#pragma config WDT = OFF`”将关闭看门狗定时器。

在本节中，包含了使用 C 语言的程序化 I/O 示例。如前所述，为了使 I/O 程序正常工作，在所有编程示例中，在“`#include <p18f4321.h>`”语句之后应包含以下“`#pragma config`”语句：

```c
#pragma config OSC = INTIO2 // Select internal oscillator
#pragma config WDT = OFF // Watch Dog Timer OFF
#pragma config LVP = OFF // Low Voltage Programming OFF
#pragma config BOR = OFF // Brown Out Reset OFF
```

#### main ( ) 函数

所有 C 程序必须包含一个“`main ( )`”函数，且该函数只能出现一次。关键字“`void`”可以可选地放在括号内，以明确没有参数。语句，

```c
main (void)
```

意味着函数调用不需要参数。“`void`”类型不为调用者提供结果值。因此，“`main ( )`”意味着它不返回值。由于“`main`”被归类为函数，所有代码都必须放在花括号内。

#### while (1)

在包括 `PIC18F` 在内的微控制器中，程序执行完成后，没有操作系统可以返回。因此，使用无限的“`while (1)`”循环来保持微控制器运行并防止其退出“`main( )`”。这将防止尝试在未定义的内存位置执行代码。注意，关键字“`while`”定义了一个迭代循环，该循环基于插入在 while 语句括号内的条件继续或中断。例如，以下“`while`”循环中花括号内的语句

```c
while ( x < 2)
{
Statements
}
```

只要变量‘`x`’小于 2 且循环条件为真，就会被执行。因此，在每次迭代之前，程序确定条件是“TRUE”（在 C 中由非零表示）还是“FALSE”（在 C 中由零表示）。这意味着“`while (1)`”中循环内的‘1’始终为 TRUE 条件。因此，循环将永远运行。因此，`while(1)` 是一个无限循环。

#### PIC18F 数据类型

C 的数据类型在第 4 章中讨论。本节将概述常见的 PIC18F 数据类型。PIC18F 的常见数据类型列举如下：

- 无符号字符（8 位）。由于 `PIC18F` 是 8 位微控制器，`PIC18F` 通常将其用于正变量（8 位正温度）。
- 有符号字符（8 位）：在 `PIC18F` 中，这被称为“`char`”，因为有符号字符是 `PIC18F` 中的默认数据类型。此数据类型可用于 8 位有符号温度。
- 无符号整数（16 位）：由于内存地址是无符号的（始终为正），此数据类型可用于 `PIC18F4321` 的程序内存地址。注意，`PIC18F4321` 的程序内存地址宽度为 13 位。
- 有符号整数（16 位）：由于 `PIC18F4321` 中的内存内容宽度为 16 位，此数据类型可用于在程序存储器中存储 16 位有符号数据。

#### C 中的函数

如第 4 章所述，C 中的函数类似于汇编中的子程序。因此，函数是一个执行特定任务的 C 代码块。

下面提供了一个典型的 C 函数示例。以下 C 函数不将结果返回给 main；在这种情况下可以使用保留字“`void`”。下面提供了 `PIC18F` 的 C18 C 编译器的简单示例：

```c
#include <p18f4321.h>
// Initializations
void CONVERT (void);
void main (void)
{
Statements
CONVERT (); // Function Call
} // end of main
void CONVERT ()
{ Body of the Function
}
```

#### C 中的数组
