
使用变量来跟踪动物的位置（即位置编号为 1–70）。让每只动物从位置 1（即“起跑门”）开始。如果动物滑到第 1 格的左侧，则将其移回第 1 格。

通过生成范围在 1 ≤ *i* ≤10 的随机整数 *i* 来产生前面表格中的百分比。对于乌龟，当 1 ≤ *i* ≤5 时执行“快走”，当 6 ≤ *i* ≤7 时执行“滑倒”，当 8 ≤ *i* ≤10 时执行“慢走”。使用类似的技术来移动兔子。比赛开始时显示

```
BANG !!!!!
AND THEY’RE OFF !!!!!
```

对于每个时钟滴答（即每次循环重复），显示一个包含 70 个位置的行，在乌龟的位置显示字母 T，在兔子的位置显示字母 H。偶尔，参赛者会落在同一个格上。在这种情况下，乌龟会咬兔子，你的程序应该从该位置开始显示 OUCH!!!。除了 T、H 或 OUCH!!!（在平局的情况下）之外的所有位置都应为空白。

显示每一行后，测试是否有动物到达或超过第 70 格。如果是，则显示获胜者并终止模拟。如果乌龟获胜，显示 TORTOISE WINS!!! YAY!!!。如果兔子获胜，显示 Hare wins. Yuch.。如果两只动物在同一时钟滴答中同时获胜，你可以选择偏袒乌龟（“弱者”），也可以选择显示 It’s a tie.。如果两者都没赢，则再次执行循环以模拟下一个时钟滴答。

| 动物 | 移动类型 | 时间百分比 | 实际移动 |
|---|---|---:|---|
| 乌龟 | 快走 | 50% | 向右 3 格 |
|  | 滑倒 | 20% | 向左 6 格 |
|  | 慢走 | 30% | 向右 1 格 |
| 兔子 | 睡觉 | 20% | 不移动 |
|  | 大跳 | 20% | 向右 9 格 |
|  | 大滑 | 10% | 向左 12 格 |
|  | 小跳 | 30% | 向右 1 格 |
|  | 小滑 | 20% | 向左 2 格 |

图 8.18 | 乌龟和兔子的移动规则。

### 8.13（这段代码做了什么？）

这个程序做了什么？

```cpp
// Ex. 8.13: ex08_13.cpp
// What does this program do?
#include <iostream>
using namespace std;

void mystery1( char *, const char * ); // prototype

int main()
{
    char string1[ 80 ];
    char string2[ 80 ];

    cout << "Enter two strings: ";
    cin >> string1 >> string2;
    mystery1( string1, string2 );
    cout << string1 << endl;
} // end main

// What does this function do?
void mystery1( char *s1, const char *s2 )
{
    while ( *s1 != '\0' )
        ++s1;

    for ( ; *s1 = *s2; ++s1, ++s2 )
        ; // empty statement
} // end function mystery1
```

### 8.14（这段代码做了什么？）

这个程序做了什么？

```cpp
// Ex. 8.14: ex08_14.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery2( const char * ); // prototype

int main()
{
    char string1[ 80 ];

    cout << "Enter a string: ";
    cin >> string1;
    cout << mystery2( string1 ) << endl;
} // end main

// What does this function do?
int mystery2( const char *s )
{
    unsigned int x;

    for ( x = 0; *s != '\0'; ++s )
        ++x;

    return x;
} // end function mystery2
```

## 专题：构建你自己的计算机

在接下来的几个问题中，我们暂时离开高级语言编程的世界。我们“拆开”一台计算机，看看它的内部结构。我们介绍机器语言编程，并编写几个机器语言程序。为了使这成为一次特别有价值的体验，我们随后构建一台计算机（使用基于软件的模拟），你可以在其上执行你的机器语言程序！

### 8.15（机器语言编程）

让我们创建一台名为 Simpletron 的计算机。顾名思义，它是一台简单的机器，但正如我们很快会看到的，它也是一台功能强大的机器。Simpletron 运行用它能直接理解的唯一语言编写的程序，即 Simpletron 机器语言，简称 SML。

Simpletron 包含一个*累加器*——一个“特殊寄存器”，在 Simpletron 使用这些信息进行计算或以各种方式检查之前，信息被放入其中。Simpletron 中的所有信息都以*字*为单位处理。一个字是一个带符号的四位十进制数，例如 +3364、-1293、+0007、-0001 等。Simpletron 配备了一个容量为 100 个字的内存，这些字通过其位置编号 00、01、…、99 来引用。

在运行 SML 程序之前，我们必须*加载*，即把程序放入内存。每个 SML 程序的第一条指令（或语句）总是放在位置 00。模拟器将从该位置开始执行。

用 SML 编写的每条指令占据 Simpletron 内存的一个字；因此，指令是带符号的四位十进制数。假设 SML 指令的符号总是正号，但数据字的符号可以是正号或负号。Simpletron 内存中的每个位置可能包含一条指令、一个程序使用的数据值，或者一个未使用（因此未定义）的内存区域。每条 SML 指令的前两位是*操作码*，它指定要执行的操作。SML 操作码如图 8.19 所示。

| 操作码 | 含义 |
|---|---|
| *输入/输出操作* | |
| `const int read = 10;` | 从键盘读取一个字到内存中的特定位置。 |
| `const int write = 11;` | 将内存中特定位置的一个字写到屏幕。 |
| *加载和存储操作* | |
| `const int load = 20;` | 将内存中特定位置的一个字加载到累加器中。 |
| `const int store = 21;` | 将累加器中的一个字存储到内存中的特定位置。 |
| *算术操作* | |
| `const int add = 30;` | 将内存中特定位置的一个字与累加器中的字相加（结果留在累加器中）。 |
| `const int subtract = 31;` | 从累加器中的字减去内存中特定位置的一个字（结果留在累加器中）。 |
| `const int divide = 32;` | 将累加器中的字除以内存中特定位置的一个字（结果留在累加器中）。 |
| `const int multiply = 33;` | 将内存中特定位置的一个字乘以累加器中的字（结果留在累加器中）。 |
| *控制转移操作* | |
| `const int branch = 40;` | 转移到内存中的特定位置。 |
| `const int branchnneg = 41;` | 如果累加器为负，则转移到内存中的特定位置。 |
| `const int branchzero = 42;` | 如果累加器为零，则转移到内存中的特定位置。 |
| `const int halt = 43;` | 停止——程序已完成其任务。 |

**图 8.19** | Simpletron 机器语言（SML）操作码。

- a) 使用哨兵控制循环读取正数并计算和显示它们的总和。当输入负数时终止输入。

- b) 使用计数器控制循环读取七个数字，有些是正数，有些是负数，并计算和显示它们的平均值。

- c) 读取一系列数字，并确定和显示最大的数字。读取的第一个数字表示应处理多少个数字。

### 8.16（计算机模拟器）

起初这可能看起来令人难以置信，但在本问题中，你将构建自己的计算机。不，你不会把组件焊接在一起。相反，你将使用基于软件模拟的强大技术来创建 Simpletron 的软件模型。你的 Simpletron 模拟器将把你正在使用的计算机变成一台 Simpletron，而且你实际上将能够运行、测试和调试你在练习 8.15 中编写的 SML 程序。

当你运行你的 Simpletron 模拟器时，它应该首先显示

```
*** Welcome to Simpletron! ***
*** Please enter your program one instruction ***
*** (or data word) at a time. I will type the ***
*** location number and a question mark (?). ***
*** You type the word for that location. ***
*** Type the sentinel -99999 to stop entering ***
*** your program. ***
```

你的程序应该使用一个单下标、包含 100 个元素的内置数组来模拟 Simpletron 的内存。现在假设模拟器正在运行，让我们查看输入练习 8.15 中第二个示例程序时的对话框：

```
00 ? +1009
01 ? +1010
02 ? +2009
03 ? +3110
04 ? +4107
05 ? +1109
06 ? +4300
07 ? +1110
08 ? +4300
09 ? +0000
10 ? +0000
11 ? -99999

*** Program loading completed ***
*** Program execution begins ***
```

上述对话框中每个 ? 右侧的数字表示用户输入的 SML 程序指令。

SML 程序现在已被放置（或加载）到内置数组内存中。现在 Simpletron 执行你的 SML 程序。执行从位置 00 的指令开始，并且像 C++ 一样顺序继续，除非通过控制转移被引导到程序的另一部分。

使用变量 accumulator 来表示累加器寄存器。使用变量 instructionCounter 来跟踪内存中包含正在执行的指令的位置。使用变量 operationCode 来指示当前正在执行的操作（即指令字的左边两位）。使用变量 operand 来指示当前指令操作的内存位置。因此，operand 是当前正在执行的指令的最右边两位。不要直接从内存执行指令。相反，将下一条要执行的指令从内存传送到一个名为 instructionRegister 的变量。然后“取出”左边两位并放入 operationCode，再“取出”右边两位并放入 operand。当 Simpletron 开始执行时，所有特殊寄存器都被初始化为零。

