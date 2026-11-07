
表达式中允许的算术运算有：

- `+` 加法
- `-` 减法
- `*` 乘法
- `/` 除法

栈应使用以下声明进行维护：

```c
struct stackNode {
    int data;
    struct stackNode *nextPtr;
};
typedef struct stackNode StackNode;
typedef StackNode *StackNodePtr;
```

程序应由 main 和另外六个函数组成，其函数原型如下：

| 函数原型 | 描述 |
|---|---|
| `int evaluatePostfixExpression(char *expr);` | 求值后缀表达式并返回其结果。 |
| `int calculate(int op1, int op2, char operator);` | 计算表达式 op1 operator op2 并返回其结果。 |
| `void push(StackNodePtr *topPtr, int value);` | 将值压入栈。 |
| `int pop(StackNodePtr *topPtr);` | 从栈中弹出一个值并返回该值。 |
| `bool isEmpty(StackNodePtr topPtr);` | 如果栈为空（即 topPtr 为 NULL），则返回 true；否则返回 false。 |
| `void printStack(StackNodePtr topPtr);` | 打印栈——此函数遍历实现栈的链表，但不修改它。 |

## 12.24（简单编程语言——编写简单程序）

在构建编译器之前，让我们讨论一种简单而强大的高级语言，它类似于 BASIC 编程语言的早期版本。我们称该语言为 Simple。每个 Simple 语句都由一个行号和一个 Simple 指令组成。行号必须按升序出现。每个指令都以以下 Simple 命令之一开头：rem、input、let、print、goto、if...goto 或 end，我们在下表中进行了描述。Simple 仅使用 +、-、* 和 / 运算符计算整数表达式。这些运算符的优先级与 C 中相同。圆括号可以改变表达式的求值顺序。练习 12.27 建议对 Simple 编译器进行增强。其中一些建议的增强，例如添加浮点功能，也需要对 Simpletron 虚拟机进行修改。

| 命令 | 示例语句 | 描述 |
|---|---|---|
| `rem` | `50 rem this is a remark` | `rem` 命令后的文本仅用于文档说明，会被忽略——不生成 SML 代码。 |
| `input` | `30 input x` | 显示问号以提示用户输入一个整数。从键盘读取该整数并将其存储在 x 中。 |
| `let` | `80 let u = 4 * (j - 7)` | 将 4 * (j - 7) 的值赋给 u。等号右侧可以出现任意复杂的中缀表达式。 |
| `print` | `10 print w` | 显示单个整数变量 w 的值。 |
| `goto` | `70 goto 45` | 将程序控制转移到第 45 行。 |
| `if...goto` | `35 if i == z goto 80` | 比较 i 和 z 是否相等，如果条件为真则将控制转移到第 80 行；否则继续执行下一条语句。 |
| `end` | `99 end` | 终止程序执行。 |

### Additional Simple Language Rules

Simple 还有以下语言规则：

- Simple 编译器**仅识别小写字母**——Simple 程序中的所有字符都应为小写。
- 变量名是一个字母。不允许使用多字符变量名，因此 Simple 程序应在 `rem` 语句中记录其变量。
- Simple **仅使用 int 变量**。
- Simple **没有变量声明**——仅在程序中提及变量名即声明该变量并将其初始化为零。
- Simple 的语法**不允许字符串操作**（读取字符串、写入字符串、比较字符串等）。
- Simple 使用**条件分支 `if...goto` 语句**和**无条件分支 `goto` 语句**来改变程序的控制流。如果 `if...goto` 语句中的条件为真，控制将转移到指定的行号。以下关系和相等运算符 `<`、`>`、 `<=`、 `>=`、 `==` 或 `!=` 在 `if...goto` 语句中有效。它们的优先级与 C 相同。

我们的编译器假设 Simple 程序输入正确。练习 12.27 要求你修改编译器以执行**语法错误检查**。

### Simple Program Examples

让我们考虑几个演示语言特性的 Simple 程序。第一个（图 12.5）从键盘读取两个整数，将值存储在变量 a 和 b 中，并计算并打印它们的和（存储在变量 c 中）。

```text
10 rem    input two integers, then determine and print their sum
15 rem
20 rem    input the two integers
30 input a
40 input b
45 rem
50 rem    add integers and store result in c
60 let c = a + b
65 rem
70 rem    print the result
80 print c
90 rem    terminate program execution
99 end
```

**Fig. 12.5** | 输入两个整数，然后确定并打印它们的和。

下一个程序（图 12.6）确定并打印两个整数中较大的一个。整数从键盘输入并存储在变量 s 和 t 中。if...goto 语句测试条件 s >= t。如果条件为真，控制将转移到第 90 行，该行显示 s。否则，程序显示 t，然后将控制转移到第 99 行的 end 语句，程序在此终止。

```text
10 rem    input two integers, then determine and print the larger one
20 input s
30 input t
32 rem
35 rem    test if s is greater than or equal to t
40 if s >= t goto 90
45 rem
50 rem    t is greater than s, so print t
60 print t
70 goto 99
75 rem
80 rem    s is greater than or equal to t, so print s
90 print s
99 end
```

**Fig. 12.6** | 输入两个整数，然后确定并打印较大者。

Simple 没有像 C 的 for、while 或 do...while 这样的重复语句。然而，你可以使用 if...goto 和 goto 语句模拟其中的每一个。图 12.7 使用哨兵控制循环计算几个整数的平方。每个整数从键盘输入并存储在变量 j 中。如果输入的值是哨兵 -9999，控制将转移到第 99 行，程序在此终止。否则，k 被赋值为 j 的平方，k 输出到屏幕，控制传递到第 20 行，在那里输入下一个整数。

```text
10 rem  calculate squares of integers until user enters -9999 sentinel to end
20 input j
23 rem
25 rem  test for sentinel value
30 if j == -9999 goto 99
33 rem
35 rem  calculate square of j and assign result to k
40 let k = j * j
50 print k
53 rem
55 rem  loop to get next j
60 goto 20
99 end
```

**Fig. 12.7** | 计算整数的平方，直到用户输入 -9999 结束。

### Write Your Own Simple Programs

使用图 12.5–12.7 的示例程序作为指南，编写 Simple 程序以完成以下各项：

- a) 输入三个整数，确定它们的平均值并打印结果。
- b) 使用哨兵控制循环输入 10 个整数并计算并打印它们的和。
- c) 使用计数器控制循环输入七个整数，一些为正数，一些为负数，并计算并打印它们的平均值。
- d) 输入一系列整数并确定并打印最大值。输入的第一个整数指示应处理的数字数量。
- e) 输入 10 个整数并打印最小值。
- f) 计算并打印从 2 到 30 的偶数之和。
- g) 计算并打印从 1 到 9 的奇数之积。

## 12.25（构建编译器；先决条件：完成练习 7.28、7.29、12.22、12.23 和 12.24）

现在我们已经介绍了 Simple 语言（练习 12.24），让我们讨论如何构建 Simple 编译器。以下图表总结了将 Simple 程序编译为 SML，然后在 Simpletron 模拟器中执行的流程：

![](img/43d318ad505997c339a3ea78d716d162_698_0.png)

编译器读取包含 Simple 程序的文件，**编译**它为 SML 代码，然后将 SML 一条指令一行写入文本文件。接下来，Simpletron 模拟器**加载** SML 文件到 Simpletron 的 100 元素内存数组中，执行程序并将结果输出到屏幕和文件。我们还将所有屏幕输出发送到文件以便轻松打印硬拷贝。

你在练习 7.29 中开发的 Simpletron 模拟器从键盘而不是文件获取输入。你必须修改 Simpletron 以从文件读取，以便它可以运行你的 Simple 编译器生成的程序。

编译器对 Simple 程序执行两次传递以将其转换为 SML：

- **第一次传递**构建符号表（下面详细讨论）。编译器将 Simple 程序的每个行号、变量名和常量存储在符号表中。每个都与其类型和最终 SML 代码中的位置一起存储。**第一次传递**还为每个 Simple 语句生成相应的 SML 指令（s）。如你所见，如果 Simple 程序包含转移控制到程序后面行的语句，**第一次传递**的结果是包含一些不完整指令的 SML 程序。
- **第二次传递**定位并**完成未完成的指令**并将 SML 程序输出到文件。编译器的**第一次传递**代码远大于其**第二次传递**代码。

### First Pass

编译器首先将 Simple 程序的第一个语句读入内存。编译器将该行分离为其各个标记（即语句的“片段”）以进行处理和编译。你可以使用函数 strtok 来执行此操作。请记住，每个语句都以行号后跟命令开头。随着编译器将语句的其余部分分解为标记，如果标记是行号、变量或常量，它将被放入符号表中。行号仅在它是语句中的第一个标记时才放入符号表中——你很快就会看到编译器对条件或无条件分支的目标行号的处理方式。

**symbolTable** 是**tableEntry 结构**的数组，表示程序中的每个**symbol**。程序中可以出现的符号数量没有限制。因此，**symbolTable** 可能很大。现在将 **symbolTable** 设为 200 元素数组。你可以在拥有一个工作的编译器后调整其大小。

tableEntry 结构声明如下：

```c
struct tableEntry {
    int symbol;
    char type; // 'C' (constant), 'L' (line number), 'V' (variable)
    int location; // 00 to 99
};
```

每个 tableEntry 包含三个成员：

- **symbol** 是一个整数，包含变量的 ASCII 表示（再次，变量名是单个字符）、行号或整数常量。
