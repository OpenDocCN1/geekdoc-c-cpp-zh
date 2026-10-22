

```
if (ch == SPACE)      // leave the space
    putchar(ch);      // character unchanged
else
    putchar(ch + 1);  // change other characters
ch = getchar();      // get next character
}
putchar(ch);          // print the newline

return 0;
}
```

（如果你的编译器抱怨由于转换可能导致数据丢失，请不要担心。第 8 章“字符输入/输出和输入验证”将在介绍 EOF 时解释所有内容。）

这里有一个示例运行：

```
CALL ME HAL.
DBMM NF IBM/
```

将此循环与第 7.1 节中的循环进行比较。第 7.1 节使用 scanf() 返回的状态而不是输入项的值来确定何时终止循环。而第 7.2 节则使用输入项本身的值来决定何时终止循环。这种差异导致了略有不同的循环结构，在循环之前有一个读语句，在每个循环的末尾有一个读语句。然而，C 灵活的语法使你能够通过将读取和测试合并为一个表达式来模拟第 7.1 节。例如，你可以把如下形式的循环

```
ch = getchar();          /* read a character          */
while (ch != '\n')       /* while not end of line      */
{
    ...                     /* process character          */
    ch = getchar();         /* get next character         */
}
```

替换为如下形式：

```
while ((ch = getchar()) != '\n')
{
    ...                     /* process character          */
}
```

关键行是

```
while ((ch = getchar()) != '\n')
```

它展示了 C 编程中一个典型的风格——在一个表达式中组合两个动作。C 的自由格式功能可以帮助使该行的各个组成部分更清晰：

```
while (
    (ch = getchar())      // assign a value to ch
        != '\n')          // compare ch to \n
```

这些动作是为 ch 分配一个值并将该值与换行符进行比较。ch = getchar() 周围的括号使其成为 != 运算符的左操作数。为了评估这个表达式，计算机必须首先调用 getchar() 函数，然后将其返回值赋给 ch。因为赋值表达式的值是左成员的值，所以 ch = getchar() 的值只是 ch 的新值。因此，在读取 ch 之后，测试条件就简化为 ch != '\n'（即 ch 不是换行符）。

这种特定的习惯用法在 C 编程中非常常见，所以你应该熟悉它。你也应该确保记住使用括号正确地分组子表达式。

所有括号都是必要的。假设你错误地使用了这样的方式：

```
while (ch = getchar() != '\n')
```

!= 运算符的优先级高于 =，因此首先被评估的表达式是 getchar() != '\n'。因为这是一个关系表达式，其值是 1 或 0（真或假）。然后这个值被赋给 ch。省略括号意味着 ch 被赋值为 0 或 1 而不是 getchar() 的返回值；这不是期望的结果。

语句

```
putchar(ch + 1);   /* change other characters */
```

再次说明字符实际上是以整数存储的。在表达式 ch + 1 中，ch 会被扩展为类型 int 以进行计算，并且 resulting int 被传递给 putchar()，putchar() 接受 int 参数但只使用最后的字节来确定要显示哪个字符。

## ctype.h 字符函数族

注意，第 7.2 节的输出显示句号被转换成了斜杠；这是因为斜杠字符的 ASCII 码比句号字符大一。但如果程序的目的是只转换字母，那么最好让所有非字母字符，而不是仅空格，保持不变。逻辑运算符将在本章后面讨论，提供了一种测试字符是否不是空格、不是逗号等的方法，但列出所有可能性会相当繁琐。幸运的是，C 有一套用于分析字符的标准函数；ctype.h 头文件包含其原型。这些函数接受一个字符作为参数，如果字符属于特定类别则返回非零（真），否则返回零（假）。例如，isalpha() 函数如果其参数是字母则返回非零值。第 7.3 节通过使用此函数对第 7.2 节进行了概括；它还结合了我们刚刚讨论的缩短的循环结构。

如果你担心你的能源管理，你可能想准备一个计算能源成本的程序。第 7.4 节中的程序就是朝着这个方向迈出的第一步。

## 第 7.4 节 electric.c 程序

```
// electric.c -- calculates electric bill
#include <stdio.h>
#define RATE1 0.13230      // rate for first 360 kwh
#define RATE2 0.15040      // rate for next 108 kwh
#define RATE3 0.30025      // rate for next 252 kwh
#define RATE4 0.34025      // rate for over 720 kwh
#define BREAK1 360.0       // first breakpoint for rates
#define BREAK2 468.0       // second breakpoint for rates
#define BREAK3 720.0       // third breakpoint for rates
#define BASE1  (RATE1 * BREAK1)
// cost for 360 kwh
#define BASE2  (BASE1 + (RATE2 * (BREAK2 - BREAK1)))
// cost for 468 kwh
#define BASE3  (BASE1 + BASE2 + (RATE3 *(BREAK3 - BREAK2)))
//cost for 720 kwh
int main(void)
{
    double kwh;            // kilowatt-hours used
    double bill;           // charges

    printf("Please enter the kwh used.\n");
    scanf("%lf", &kwh);    // %lf for type double
    if (kwh <= BREAK1)
        bill = RATE1 * kwh;
    else if (kwh <= BREAK2)  // kwh between 360 and 468
        bill = BASE1 + (RATE2 * (kwh - BREAK1));
    else if (kwh <= BREAK3)  // kwh between 468 and 720
        bill = BASE2 + (RATE3 * (kwh - BREAK2));
    else                     // kwh above 680
        bill = BASE3 + (RATE4 * (kwh - BREAK3));
    printf("The charge for %.1f kwh is $%.2f.\n", kwh, bill);

    return 0;
}
```

以下是一些示例输出：

```
Please enter the kwh used.
580
The charge for 580.0 kwh is $97.50.
```

第 7.4 节使用符号常量表示费率，以便将常量集中在一个地方。如果电力公司更改其费率（这是可能的），将费率放在一个地方使其易于更新。列表还以符号形式表达了费率的断点。它们也可能发生变化。BASE1 和 BASE2 是以费率和断点表示的。然后，如果费率或断点发生变化，基数将自动更新。你可能还记得预处理器不做计算。在程序中出现 BASE1 时，它将被替换为 0.13230 * 360.0。别担心；编译器会将此表达式计算为其数值（47.628），因此最终的程序代码使用 47.628 而不是计算。

程序的流程很直接。程序根据 kwh 的值选择其中一个公式之一。你应该特别注意，程序只能在 kwh 大于或等于 360 时才能到达第一个 else。因此，else if (kwh <= BREAK2) 行实际上等同于要求 kwh 在 360 到 482 之间，正如程序注释所指出的。同样，最后的 else 只能在 kwh 超过 720 时到达。最后，请注意 BASE1、BASE2 和 BASE3 分别代表前 360、468 和 720 千瓦时的总费用。因此，你只需要加上超出这些数量的电力的额外费用。

实际上，else if 是你已经知道的一种变体。例如，程序的核心只是另一种写法

```
if (kwh <= BREAK1)
    bill = RATE1 * kwh;
else
    if (kwh <= BREAK2)  // kwh between 360 and 468
        bill = BASE1 + (RATE2 * (kwh - BREAK1));
    else
        if (kwh <= BREAK3)  // kwh between 468 and 720
            bill = BASE2 + (RATE3 * (kwh - BREAK2));
        else                // kwh above 680
            bill = BASE3 + (RATE4 * (kwh - BREAK3));
```

也就是说，程序由一个 if else 语句组成，其 else 部分的语句是另一个 if else 语句。第二个 if else 语句被说成嵌套在第一个语句中，第三个嵌套在第二个语句中。请记住整个 if else 结构被视为一个语句，这就是为什么我们不需要用大括号括起嵌套的 if else 语句。然而，使用大括号会更清晰地说明这种特定格式的意图。

这两种形式是完全等价的。唯一的区别在于空格和换行符的位置，而编译器会忽略这些差异。尽管如此，第一种形式更好，因为它更清楚地表明你正在进行四种选择。这种形式使你更容易浏览程序并了解选择是什么。保存嵌套的缩进形式以备需要时使用——例如，当你必须测试两个不同的量时。一种这样的情况的例子是在夏季对超过 720 千瓦时的用电量收取 10% 的附加费。

