
Answer: d.

2.（多选题）考虑以下语句：

```c
y = a * x * x + b * x + c;
```

下面哪一个或哪些对前述语句的变体包含冗余的括号？

- a) y = (a * x * x + b * x + c);
- b) y = a * (x * x) + (b * x) + c;
- c) y = (a * x * x) + (b * x) + c;
- d) All of the above.

Answer: d.

## 2.6 决策：相等与关系运算符

可执行语句要么执行诸如计算、输入和输出之类的操作，要么，如你即将看到的，进行决策。例如，一个程序可能会判断一个人在考试中的成绩是否大于或等于60，以便决定是否打印消息“Congratulations! You passed.”

一个条件是一个表达式，可以为 *true*（即条件满足）或 *false*（即条件不满足）。本节介绍 `if` 语句，它允许程序基于条件的值做出决策。如果条件为 *true*，则 `if` 语句体中的语句执行；否则，不执行。

### 相等与关系运算符

条件使用以下相等和关系运算符形成：

| 代数相等或关系运算符 | C 相等或关系运算符 | C 条件示例 | C 条件含义 |
|---|---|---|---|
| *关系运算符* | | | |
| > | > | x > y | x is greater than y |
| < | < | x < y | x is less than y |
| ≥ | >= | x >= y | x is greater than or equal to y |
| ≤ | <= | x <= y | x is less than or equal to y |
| *相等运算符* | | | |
| = | == | x == y | x is equal to y |
| ≠ | != | x != y | x is not equal to y |

关系运算符 <、<=、> 和 >= 具有相同的优先级并从左到右结合。相等运算符 == 和 != 具有相同的优先级，其优先级低于关系运算符，也从左到右结合。在 C 中，条件实际上可以是任何生成零（*false*）或非零（*true*）值的表达式。

### 将相等运算符 == 与赋值运算符混淆

![](img/43d318ad505997c339a3ea78d716d162_125_0.png)

将 == 与赋值运算符 (=) 混淆是常见的编程错误。为了避免这种混淆，将相等运算符读作“double equals”并将赋值运算符读作“gets”或“is assigned the value of.”。正如你将看到的，混淆这些运算符可能会导致难以找到的逻辑错误，而不是编译错误。

### 演示 if 语句

图 2.5 使用六个 if 语句比较用户输入的两个数字。对于每个条件为 *true* 的 if 语句，对应的 printf 执行。程序和三个示例执行输出显示在图中。

```c
// fig02_05.c
// Using if statements, relational
// operators, and equality operators.
#include <stdio.h>

// function main begins program execution
int main(void) {
    printf("Enter two integers, and I will tell you\n");
    printf("the relationships they satisfy: ");

    int number1 = 0; // first number to be read from user
    int number2 = 0; // second number to be read from user

    scanf("%d %d", &number1, &number2); // read two integers

    if (number1 == number2) {
        printf("%d is equal to %d\n", number1, number2);
    } // end if

    if (number1 != number2) {
        printf("%d is not equal to %d\n", number1, number2);
    } // end if

    if (number1 < number2) {
        printf("%d is less than %d\n", number1, number2);
    } // end if

    if (number1 > number2) {
        printf("%d is greater than %d\n", number1, number2);
    } // end if

    if (number1 <= number2) {
        printf("%d is less than or equal to %d\n", number1, number2);
    } // end if

    if (number1 >= number2) {
        printf("%d is greater than or equal to %d\n", number1, number2);
    } // end if
} // end function main
```

图 2.5 | 使用 if 语句、关系运算符和相等运算符。（第 1 部分，共 2 部分。）

```text
Enter two integers, and I will tell you
the relationships they satisfy: 3 7
3 is not equal to 7
3 is less than 7
3 is less than or equal to 7

Enter two integers, and I will tell you
the relationships they satisfy: 22 12
22 is not equal to 12
22 is greater than 12
22 is greater than or equal to 12

Enter two integers, and I will tell you
the relationships they satisfy: 7 7
7 is equal to 7
7 is less than or equal to 7
7 is greater than or equal to 7
```

图 2.5 | 使用 if 语句、关系运算符和相等运算符。（第 2 部分，共 2 部分。）

程序使用 scanf（第 14 行）将两个整数读入 int 变量 number1 和 number2。第一个 %d 将值转换为存储在变量 number1 中。第二个将值转换为存储在变量 number2 中。

### 比较数字

第 16–18 行的 if 语句

```c
if (number1 == number2) {
    printf("%d is equal to %d\n", number1, number2);
} // end if
```

比较 number1 和 number2 的值是否相等。如果值相等，第 17 行显示一行文本，表明数字相等。对于从第 20、24、28、32 和 36 行开始的 if 语句中的每个 true 条件，对应的正文语句显示一行文本。对每个 if 语句的主体进行缩进，并在每个 if 语句上方和下方放置空行，可增强程序的可读性。

2. 使用大括号界定 if 语句的主体对于单语句主体是可选的，但始终使用这些大括号被认为是良好的实践。在第 3 章中，我们将解释这些问题。

### 到目前为止介绍的运算符

下表按从最高到最低的优先级列出了到目前为止介绍的运算符：

| 运算符 | 结合性 |
|---|---|
| () | left-to-right |
| * / % | left-to-right |
| + - | left-to-right |
| < <= > >= | left-to-right |
| == != | left-to-right |
| = | right-to-left |

赋值运算符 (=) 从右到左结合。在编写包含许多运算符的表达式时，请参考运算符优先级图表。确认表达式中的运算符按正确的顺序应用。如果您不确定复杂表达式中求值的顺序，请使用括号对表达式进行分组或将语句分解为几个更简单的语句。

### 关键字

我们在本章示例中使用的一些词，例如 int、if 和 void，是语言的关键字或保留字，对编译器具有特殊含义。下表包含 C 关键字。不要将它们用作标识符。

| 关键字 |
|---|
| auto do goto signed unsigned |
| break double if sizeof void |
| case else int static volatile |
| char enum long struct while |
| const extern register switch |
| continue float return typedef |
| default for short union |
| C99 标准中添加的关键字 |
| _Bool _Complex _Imaginary inline restrict |
| C11 标准中添加的关键字 |
| _Alignas _Alignof _Atomic _Generic _Noreturn _Static_assert _Thread_local |

### 自检

1.（多选题）以下哪项陈述是错误的？

- a) 一个条件是一个表达式，可以为 true 或 false。
- b) 一个条件可以是任何生成零（true）或非零（false）值的表达式。
- c) if 语句基于条件的值做出决策。如果条件为 true，则 if 语句体中的语句执行；否则，不执行。
- d) 您使用相等运算符和关系运算符形成条件。

Answer: b) is false. Actually, in C, a condition may be any expression that generates a zero (false) or nonzero (true) value.

2.（多选题）以下哪项陈述是错误的？

```c
if (number1 == number2) {
    printf("%d is equal to %d\n", number1, number2);
} // end if
```

- a) 以下 if 语句在 number1 等于 number2 时执行其主体：
- b) 如果您不确定复杂表达式的求值顺序，请使用括号对表达式进行分组或将语句分解为更简单的语句。
- c) 可以在 if 语句的主体中放置任意数量的语句。使用大括号界定 if 语句的主体是必需的。
- d) C 的某些运算符，例如赋值运算符（=），是从右到左结合而不是从左到右结合。

Answer: c) is false. Actually, using braces to delimit the body of an if statement is optional when the body contains only one statement. Nevertheless, always using these braces helps avoid errors.

## 2.7 安全的 C 编程

我们在前言中提到了 SEI CERT C 编码标准，并指出我们将遵循某些指南，以帮助您避免打开系统攻击的编程实践。

### 避免单参数 printf

其中一条指南是避免使用单个字符串参数的 printf。³ printf 的第一个参数是格式字符串，printf 会检查其转换说明符。然后它用后续参数的值替换每个转换说明符。它会尝试这样做，无论是否有后续参数可用。

在后面的章节中，您将学习如何从用户输入字符串。虽然第一个 printf 参数通常是字符串字面量，但它可能是一个包含用户输入字符串的变量。在这种情况下，攻击者可以构造一个用户输入的格式字符串，其转换说明符的数量多于额外的 printf 参数的数量。这种利用已被攻击者用来读取他们无法访问的内存。⁴

3. 有关更多信息，请参阅 CERT 规则 FIO30-C (https://wiki.sei.cmu.edu/confluence/display/c/FIO30-C,+Exclude+user+input+from+format+strings)。第 6 章的安全 C 编程部分解释了此 CERT 指南所指的用户输入的概念。

4. “Format String Attack,” Format String Software Attack | OWASP Foundation. Accessed July 22, 2020, https://owasp.org/www-community/attacks/Format_string_attack.
