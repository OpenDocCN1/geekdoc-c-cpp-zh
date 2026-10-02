
| 寄存器 | 名称 | 分类 |
| :--- | :--- | :--- |
| `AX` (0-15) | 加法寄存器 | 通用寄存器 |
| `BH` (8-B) / `BL` (7-D) | | |
| `BX` (0-15) | 基址寄存器 | 通用寄存器 |
| `CH` (8-B) / `CL` (7-D) | | |
| `CX` (0-15) | 计数寄存器 | 通用寄存器 |
| `DH` (8-B) / `DL` (7-D) | | |
| `DX` (0-15) | 数据寄存器 | 通用寄存器 |
| `SI` (0-15) | 源索引 | 偏移寄存器 |
| `DI` (0-15) | 目的索引 | 偏移寄存器 |
| `IP` (0-15) | 指令指针 | 偏移寄存器 |
| `BP` (0-15) | 基址指针 | 偏移寄存器 |
| `SP` (0-15) | 栈指针 | 偏移寄存器 |
| `ES` (0-15) | 附加段 | 段寄存器 |
| `SS` (0-15) | 栈段 | 段寄存器 |
| `CS` (0-15) | 代码段 | 段寄存器 |
| `DS` (0-15) | 数据段 | 段寄存器 |
| `FLAGS` (0-15) | 标志寄存器 | 标志寄存器 |

图 9.7 | 8086 微处理器可用寄存器及其分类

如图 9.7 所示，8086 微处理器中的可用寄存器分类为：

1. 通用寄存器
2. 偏移寄存器
3. 段寄存器
4. 标志寄存器

## 9.45 结构与联合体

通用寄存器，即加法寄存器、基址寄存器、计数寄存器和数据寄存器是 16 位寄存器，分别称为 `AX`、`BX`、`CX` 和 `DX`。也可以单独访问这些寄存器的低字节和高字节。这些寄存器的低字节和高字节分别称为 `AL`、`AH`、`BL`、`BH`、`CL`、`CH`、`DL` 和 `DH`。其他寄存器可以整体访问，即一次处理所有 16 位。在 Turbo C 3.0/5 中，头文件 `dos.h` 中定义了一个联合体 `REGS`，它有助于在 `int86` 和 `intdos` 函数之间传递信息。

关于预定义类型联合体 `REGS` 的重要点如下：

1. 类型联合体 `REGS` 在头文件 `dos.h` 中定义为：

```c
union REGS
{
    struct WORDREGS x;
    struct BYTEREGS h;
}
```

类型 `struct WORDREGS` 和 `struct BYTEREGS` 在头文件 `dos.h` 中也定义为：

```c
struct WORDREGS
{
    unsigned int ax, bx, cx, dx;
    unsigned int si, di, cflag, flags;
}

struct BYTEREGS
{
    unsigned char al, ah, bl, bh;
    unsigned char cl, ch, dl, dh;
}
```

2. 类型联合体 `REGS` 的对象可以声明为：`union REGS identifier_names;`，例如 `union REGS inregs, outregs.`。

3. 对象的 16 位成员通过成员 `x` 提供，而 8 位成员（即 `ax`、`ah`、`bl`、`bh` 等）通过已声明的联合体类型 `REGS` 对象的成员访问。例如，如果定义对象 `inregs` 为联合体类型 `REGS`。则 16 位成员 `bx` 通过 `inregs.x.bx` 访问，而其高位和低位（即 `bh` 和 `bl`）分别通过 `inregs.h.bh` 和 `inregs.h.bl` 访问。

4. 中断服务程序的输入可以通过设置已声明联合体类型 `REGS` 对象特定成员的值，并按地址/引用传递给函数 `int86` 和 `intdos` 来提供。声明联合体类型 `REGS` 对象成员的值如下：

```c
inregs.x.ax = 1; // 设置成员 ax 的值为 1
inregs.h.ch = 2; // 设置成员 ch 的值为 2
```

## 9.9.2 中断编程

中断编程的示例位于程序 9-31 到 9-36。详细的中断列表见附录 D 以供参考。详尽的中断列表可能达数千页，此类列表超出了本书的范围。

## 9.46 结构与联合体

### 程序 9-31 | 一个 gotoxy 函数的用法和实现的程序

| 行 | Prog 9-31a.c | Prog 9-31b.c |
| :--- | :--- | :--- |
| 1 | 使用库函数 //在特定位置打印文本 | 使用中断编程 //使用中断实现函数 |
| 2 | `#include <stdio.h>` | `#include <stdio.h>` |
| 3 | `#include <conio.h>` | `#include <conio.h>` |
| 4 | | `#include <dos.h>` |
| 5 | | `void mygotoxy(int` |
| | | 输出窗口 (Turbo C 3.0) |
| | | 输入要打印文本的行和列: Hello |
| 说明 | - 程序调用 BIOS 函数将光标置于所需的行和列 | |
| | - 关联的中断号为十六进制 `0x10`（即十进制 16） | |
| | - 该中断下有很多服务，包括定位光标、更改光标大小、在屏幕上绘图等 | |
| | - 这些例程具有关联的服务号。调用中断前将服务号放在 `AH` 寄存器中 | |
| | - 参见附录 D 以获取 BIOS 服务的详细描述 | |
| | - 函数调用 `int86(0x10, &inregs, &outregs);` 也可以写为 `int86(16, &inregs, &outregs);` | |
| | - 通常，中断按十六进制编号，因此首选调用函数的方法 | |
| | - 所有使用 Turbo C 3.0 编译器使用中断的 DOS 程序在 32 位环境（即 Windows）中产生 32 位程序，而中断仅适用于 16 位程序 | |

### 程序 9-32 | 一个 getche 函数的用法和实现的程序

| 行 | Prog 9-32a.c | Prog 9-32b.c |
| :--- | :--- | :--- |
| 1 | 使用库函数 //使用函数读取字符 | 使用中断编程 //使用中断实现 getche |
| 2 | `#include <stdio.h>` | `#include <stdio.h>` |
| 3 | `#include <conio.h>` | `#include <conio.h>` |
| 4 | `main()` | `#include <dos.h>` |
| 5 | `{` | `char mygetche();` |
| 6 | `char ch;` | `main()` |
| 7 | `clrscr();` | `{ char ch;` |
| 8 | `printf("The character is:\t");` | `clrscr();` |
| 9 | `ch = getche();` | `printf("The character is:\t");` |
| 10 | `printf("\nThe character you entered is %c.", ch);` | `ch = mygetche();` |
| 11 | `}` | `printf("\nThe character you entered is %c.", ch);` |
| | | `}` |
| | | `char mygetche()` |
| | | `{` |
| | | `union REGS inregs, outregs;` |
| | | `inregs.h.ah = 1;` |
| | | `intdos(&inregs, &outregs);` |
| | | `return outregs.h.al;` |
| | | `}` |
| | | 输出窗口 (Turbo C 3.0) |
| | | 输入字符: H |
| | | 输入的是 H |
| 说明 | - 程序调用从标准输入读取字符的 DOS 例程 | |
| | - DOS 例程分组在中断号 `0x21` 下（即十进制 33） | |
| | - 该中断下有很多可用服务，如读取字符、写入屏幕、写入打印机、获取机器名、创建目录、重命名目录、删除文件等 | |
| | - 这些服务具有关联的服务号。调用中断前将服务号放在 `AH` 寄存器中 | |
| | - 参见附录 D 获取 DOS 服务的详细描述 | |
| | - 函数调用 `intdos(&inregs, &outregs);` 也可以写为 `int86(0x21, &inregs, &outregs);` | |

### 程序 9-33 | 一个 putch 函数的用法和实现的程序

| 行 | Prog 9-33a.c | Prog 9-33b.c |
| :--- | :--- | :--- |
| | 使用库函数 | 使用中断编程 |
| 7 | `clrscr();` | `{` |
| 8 | `printf("The character is:\t");` | `char ch;` |
| 9 | `putch('A');` | `clrscr();` |
| 10 | | `printf("The character is:\t");` |
| 11 | | `myputch();` |
| 12 | | `myputch();` |
| 13 | | `{ union REGS inregs, outregs;` |
| 14 | | `inregs.h.ah = 2;` |
| 15 | | `inregs.h.dl = 'A';` |
| 16 | | `intdos(&inregs, &outregs);` |
| 17 | | `}` |
| 18 | | |
| 19 | | |
| | 输出窗口 (Turbo C 3.0) | |
| | The character is: A | |
| 说明 | * 程序调用一个 DOS 例程来实现 `putch` 函数的功能 | |
| | * 在屏幕上写入字符的例程服务号为 2 | |
| | * 调用中断前，通过将 2 赋值给 `inregs.h.ah` 将服务号放在 `AH` 寄存器中 | |
| | * 参见附录 D 查看字符放在 `DL` 寄存器中 | |
| | * 在给定代码中，通过将 `'A'` 赋值给 `inregs.h.dl` 将 `'A'` 放在 `DL` 寄存器中 | |

### 程序 9-34 | 一个 puts 函数的用法和实现的程序

| 行 | Prog 9-34.c | 输出窗口 (Turbo C 3.0) |
| :--- | :--- | :--- |
| | 使用库函数 | Interrupt Programming |
| 1 | `//通过中断编程在屏幕上打印字符串` | |
| 2 | `#include <stdio.h>` | |
| 3 | `#include <conio.h>` | |
| 4 | `#include <dos.h>` | |
| 5 | `main()` | |
| 6 | `{` | |
| 7 | `union REGS inregs, outregs;` | |
| 8 | `char *ch = "Interrupt Programming";` | |
| 9 | `clrscr();` | |
| 10 | `inregs.h.ah = 9;` | |
| 11 | `inregs.x.dx = (unsigned int)ch;` | |
| 12 | `intdos(&inregs, &outregs);` | |
| 13 | `}` | |

### Prog 9-35.c | 使用中断程序获取机器名

```c
//使用中断程序获取机器名
#include <stdio.h>
#include <conio.h>
#include <alloc.h>
#include <dos.h>

char *machinename();

main()
{
    clrscr();
    printf("The name of the machine is %s", machinename());
}

char *machinename()
{
    union REGS inregs, outregs;
    char *ch = (char *)malloc(16);
    inregs.h.ah = 0x5E;
    inregs.x.dx = (unsigned int)ch;
    intdos(&inregs, &outregs);
    return ch;
}
```

| 行号 | Prog 9-35.c | 输出窗口 (Turbo C 3.0) |
| :--- | :--- | :--- |
| | | The name of the machine is COMP2 |

备注：

- 获取机器的 DOS 例程服务号是 `5E`
- 因此，通过给 `inregs.h.ah` 赋值，将十六进制值 `5E` 放入 `AH` 寄存器
- 服务例程还期望一个 16 字节缓冲区（即字符数组）的基础地址，机器名将存放在其中，并将地址赋值给 `DX` 寄存器
- 除了函数调用 `intdos(&inregs, &outregs)`，也可以使用函数 `int86(0x21, &inregs, &outregs)`

### Prog 9-36.c | 使用中断程序进行鼠标编程

```c
//使用中断程序进行鼠标编程
#include <stdio.h>
#include <conio.h>
#include <dos.h>

union REGS inregs, outregs;

initmouse();
showmouseptr();

main()
{
    clrscr();
    printf("Developing the mouse support\n");
    initmouse();
    getch();
}

initmouse()
{
    inregs.x.ax = 0;
    int86(0x33, &inregs, &outregs);
    if (outregs.x.ax == 0)
        printf("Mouse not supported by the system");
    else
        showmouseptr();
}

showmouseptr()
{
    inregs.x.ax = 1;
    int86(0x33, &inregs, &outregs);
}
```

| 行号 | Prog 9-36.c | 输出窗口 (Turbo C 3.0) |
| :--- | :--- | :--- |
| | | 正在开发鼠标支持 |

备注：

- 开发鼠标支持的中断号为 `0x33`
- 程序仅实现了两个服务，即初始化鼠标支持和显示鼠标指针
- 参考附录 D 并实现其他服务来读取鼠标的位置和按钮状态，定义水平和垂直光标、范围，改变光标的形状等

## 9.10 枚举

在 C 语言中，枚举提供了创建用户定义类型的另一种方式。枚举类型设计用于具有有限值集的对象。例如，考虑一个我们希望变量持有布尔值的应用程序。我们可以创建一个包含 `FALSE` 和 `TRUE` 的枚举类型 `BOOL`。值 `FALSE` 和 `TRUE` 被称为枚举常量。`BOOL` 类型的变量可以取 `FALSE` 或 `TRUE`（即布尔值）。注意，`FALSE` 和 `TRUE` 不是字符串，而是整数常量。编译器在内部将整数值与 `FALSE` 和 `TRUE` 名称关联起来。因此，任何适用于整数常量变量的操作都可以应用于任何 `BOOL` 类型的变量。整数值由名称表示，枚举类型有助于使程序更具可读性。关于枚举的要点如下：

1. **枚举类型的定义**：枚举定义的通用形式为：`[storage_class][type_qualifier] enum [tag-name] {enumeration-list}[identifier=initializer, ...];`

关于枚举类型定义的要点如下：

- i. 方括号括起的术语是可选的，在枚举类型的定义中可能不会出现。加粗的术语是枚举定义的必要部分。
- ii. 枚举由关键字 `enum` 组成，随后是可选的标识符名称和花括号内用逗号分隔的枚举成员列表。枚举列表中出现的所有枚举成员组成一个枚举集。
- iii. 枚举成员是一个可以持有整数值的标识符，也称为枚举常量。可以选择给枚举成员分配一个整数值，例如在枚举类型定义 `enum BOOL {true=1, false=0};` 中，整数 `1` 和 `0` 分别赋值给值 `true` 和 `false`。
- iv. 枚举列表中的枚举成员名称必须是唯一的。
- v. 枚举列表中赋值给枚举成员的值不需要是唯一的，例如，在枚举定义 `enum COLORS {red=2, green=1, yellow=3};` 是完全有效的。
- vi. 每个枚举成员都有一个作用域，从其在枚举列表中出现之后开始。由于作用域规则，枚举定义 `enum COLORS {red=2, green=1, yellow=3}` 是合法的。
- vii. 枚举列表中的枚举成员从在枚举列表中出现后开始其作用域。每个枚举成员具有一个值。默认情况下，第一个枚举成员被赋予值 `0`，后续成员依次加 1。
- viii. 枚举定义可以选择性地带有存储类和类型限定符。
- ix. 枚举定义以分号结束。

声明枚举对象有两种方式：

a. 在枚举类型定义时：枚举对象的声明见表 9.7。

**表 9.7 | 在枚举类型定义期间声明**

| 代码示例 |
| :--- |
| `enum {off, on} s1, s2;` |
| `enum {off, on} s1 = off, s2 = on;` |
| `enum {off, on} s1 = on, s2 = off;` |
| `enum {off, on} s1 = on, s2 = on;` |

b. 在枚举定义后的独立语句中：枚举对象的声明方式如下。枚举对象的声明见表 9.8。

**表 9.8 | 在枚举类型定义后声明**

| 代码示例 |
| :--- |
| `enum {off, on}; s1 = off;` |
| `enum {off, on}; s1 = on;` |
| `enum {off, on}; s1 = off, s2 = off;` |
| `enum {off, on}; s1 = off, s2 = on;` |
| `enum {off, on}; s1 = on, s2 = off;` |
| `enum {off, on}; s1 = on, s2 = on;` |
