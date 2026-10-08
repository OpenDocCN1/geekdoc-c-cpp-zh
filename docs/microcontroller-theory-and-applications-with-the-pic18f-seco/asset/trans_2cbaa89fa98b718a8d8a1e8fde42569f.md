

# 8.2.6 使用 C 语言的程序化 I/O 示例

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

请注意，对于共阳极七段显示器，‘0’ 会点亮段，而 ‘1’ 会熄灭段。此外，假设 PORTB 的第 7 位为 ‘0’。上述表格必须使用 MOVLW 和 MOVWF 指令存储在数据存储器中，或者使用 MPLAB 汇编器指令 DB 配合 PIC18F 汇编语言指令 TBLRD（表格读取）以及适当的寻址模式来存储。

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

### 预处理器指令

C 预处理器指令是 C 编译器的一部分。预处理器的目的是执行与预处理器相关的特定命令。这些预处理器不是 C 语言的一部分。相反，它们是 C 编译器软件的一部分。每个预处理器指令都以符号 # 开头。

在编译 C 程序之前，C 编译器首先启动预处理器软件模块的执行。该模块随后遍历程序以查找“#”符号。如果找到符号“#”，预处理器模块执行由该命令指定的功能。然后 C 编译器可以开始编译程序。

典型的预处理器指令是“#include”、“#define”和“#pragma config”。“#include”预处理器指令将文本（命令、注释等）从另一个文档转移到程序中。例如，考虑

```c
#include <p18f4321.h>
```

在上面，扩展名 .h 表示头文件。注意，头文件包含在 C 程序中使用的标准库函数。上述语句指示编译器将文件 p18f4321.h 中的源代码包含到程序中。文件 p18f4321.h 是 PIC18F4321 专用的头文件，主要包含用于访问 PIC18F4321 的特殊功能寄存器（SFRs）的变量定义。例如，PIC18F4321 的 PORTA 被映射为具有数据存储器地址 0xF80 的特殊功能寄存器（SFR）。头文件包含此信息。这意味着用户可以在 C 程序中使用 PORTA。编译器在编译时遇到程序中的 PORTA 时，会插入地址 0xF80。

“#define”预处理器指令可用于声明常量。例如，考虑

```c
#define y 4
```

“#define”预处理器将 4 分配给 y。使用预处理器“#define”定义的常量是在程序编译之前执行的文本替换。

“#pragma config”预处理器指令告诉编译器在编译之前执行特定操作。该指令可用于打开或关闭某些片上设备。例如，放置在“#include”指令之后的语句“#pragma config WDT = OFF”将关闭看门狗定时器。

在本节中，包含了使用 C 语言的程序化 I/O 示例。如前所述，为了使 I/O 程序正常工作，在所有编程示例中，在“#include <p18f4321.h>”语句之后应包含以下“#pragma config”语句：

```c
#pragma config OSC = INTIO2 // Select internal oscillator
#pragma config WDT = OFF // Watch Dog Timer OFF
#pragma config LVP = OFF // Low Voltage Programming OFF
#pragma config BOR = OFF // Brown Out Reset OFF
```

### main ( ) 函数

所有 C 程序必须包含一个“main ( )”函数，且该函数只能出现一次。关键字“void”可以可选地放在括号内，以明确没有参数。语句，

```c
main (void)
```

意味着函数调用不需要参数。“void”类型不为调用者提供结果值。因此，“main ( )”意味着它不返回值。由于“main”被归类为函数，所有代码都必须放在花括号内。

### while (1)

在包括 PIC18F 在内的微控制器中，程序执行完成后，没有操作系统可以返回。因此，使用无限的“while (1)”循环来保持微控制器运行并防止其退出“main( )”。这将防止尝试在未定义的内存位置执行代码。注意，关键字“while”定义了一个迭代循环，该循环基于插入在 while 语句括号内的条件继续或中断。例如，以下“while”循环中花括号内的语句

```c
while ( x < 2)
{
Statements
}
```

只要变量‘x’小于 2 且循环条件为真，就会被执行。因此，在每次迭代之前，程序确定条件是“TRUE”（在 C 中由非零表示）还是“FALSE”（在 C 中由零表示）。这意味着“while (1)”中循环内的‘1’始终为 TRUE 条件。因此，循环将永远运行。因此，while(1) 是一个无限循环。

### PIC18F 数据类型

C 的数据类型在第 4 章中讨论。本节将概述常见的 PIC18F 数据类型。PIC18F 的常见数据类型列举如下：

- 无符号字符（8 位）。由于 PIC18F 是 8 位微控制器，PIC18F 通常将其用于正变量（8 位正温度）。
- 有符号字符（8 位）：在 PIC18F 中，这被称为“char”，因为有符号字符是 PIC18F 中的默认数据类型。此数据类型可用于 8 位有符号温度。
- 无符号整数（16 位）：由于内存地址是无符号的（始终为正），此数据类型可用于 PIC18F4321 的程序内存地址。注意，PIC18F4321 的程序内存地址宽度为 13 位。
- 有符号整数（16 位）：由于 PIC18F4321 中的内存内容宽度为 16 位，此数据类型可用于在程序存储器中存储 16 位有符号数据。

### C 中的函数

如第 4 章所述，C 中的函数类似于汇编中的子程序。因此，函数是一个执行特定任务的 C 代码块。

下面提供了一个典型的 C 函数示例。以下 C 函数不将结果返回给 main；在这种情况下可以使用保留字“void”。下面提供了 PIC18F 的 C18 C 编译器的简单示例：

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

### C 中的数组

如第 4 章所述，数组包含存储在连续内存位置下的具有共同名称的一组相同类型的数据元素。相同类型的数据元素意味着数据元素可以是，例如，字符（char）元素或整数（int）元素。

可以使用 PIC18F 的 C18 编译器创建共阳极七段显示器的 BCD 码数组，如下所示：

```c
#include <pic18f4321.h>
void main ()
{
unsigned char code [10] = {0x40, 0x79, 0x24, 0x30, 0x19, 0x12, 0x03, 0x78,
0x00, 0x18};
// ...
}
```

在上述程序中，数组名称为“code”，方括号内为 10（元素总数），每个元素都列在花括号内。例如，

