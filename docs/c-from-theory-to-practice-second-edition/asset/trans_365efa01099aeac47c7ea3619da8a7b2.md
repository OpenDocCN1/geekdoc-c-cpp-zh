
## 练习

### C.5.15 以下程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int a = 10, b = !a;

    a = b ? 50 : 200;
    printf("Val = %d\n", a);
    return 0;
}
```

答案：语句 a = b ? 50 : 200; 等价于：a = (b != 0) ? 50 : 200; 由于 b 为 0，a 变为 200，程序显示：Val = 200。

### C.5.16 编写一个程序读取学生的成绩并仅在输入成绩在 [5,10] 范围内时将其存储到变量中。否则，变量应设为 -1。使用条件运算符。

```c
#include <stdio.h>
int main(void)
{
    float i, grd;

    printf("Enter grade: ");
    scanf("%f", &grd);

    i = (grd >= 5 && grd <= 10) ? grd : -1;
    printf("%f\n", i);
    return 0;
}
```

### C.5.17 编写一个程序读取一个整数并显示一条消息以指示它是正数还是负数。如果它为 0，程序应显示 Zero。使用条件运算符。

```c
#include <stdio.h>
int main(void)
{
    int num;

    printf("Enter number: ");
    scanf("%d", &num);

    num > 0 ? printf("Pos\n") : (num < 0) ? printf("Neg\n") : printf("Zero\n");
    return 0;
}
```

注释：或者，我们可以写：

```
printf("%s\n", num > 0 ? "Pos" : num < 0 ? "Neg" : "Zero");
```

### C.5.18 以下程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int a = -10;
    if(((a < 0) ? -a : a) <= 10)
        printf("One %d\n", -a);
    else
        printf("Two %d\n", -a);
    return 0;
}
```

答案：由于 a 为 -10，条件表达式的结果为 -a，即 10。请注意，a 的值不会改变，它仍然等于 -10。因此，由于 if 条件为真，程序显示：One 10

### C.5.19 以下程序读取三个产品的价格并显示最高价格。使用条件运算符替换 if-else 语句并使用单个 printf() 显示最高价格。

```c
#include <stdio.h>
int main(void)
{
    float i, j, k;
    printf("Enter prices: ");
    scanf("%f%f%f", &i, &j, &k);
    if(i >= j && i >= k)
        printf("Max = %f\n", i);
    else if(j > i && j > k)
        printf("Max = %f\n", j);
    else
        printf("Max = %f\n", k);
    return 0;
}
```

答案：printf("Max = %f\n", (i >= j && i >= k) ? i : (j > i && j > k) ? j : k); 要显示最低价格，将 > 改为 <。

### C.5.20 编写一个程序读取学生的成绩并使用条件运算符根据以下分级显示相应的消息：

- a. 如果成绩在 [7.5–10] 范围内，程序输出：A
- b. 如果成绩在 [5–7.5) 范围内，程序输出：B

就风格而言，编写 switch 语句有几种方法。最流行的方法是将语句放在 case 标签下方，并将 break 语句放在语句内部或与语句对齐。我们更倾向于将每个 break 与 case 标签对齐，并在每个 case 与前一个 break 之间留出一个空格。

表达式必须是整数变量或括号中的表达式，并且所有 constant_1、constant_2、...、constant_n 的值必须是不同的整数常量表达式（例如，30 是一个常量表达式，30+40 也是）。case 的顺序无关紧要。当执行 switch 语句时，表达式的值会与每个 case 常量进行比较。如果找到匹配项，则执行相应 case 的语句组，并且不会测试剩余的 case。如果没有找到匹配项且存在 default case，则会执行其语句组。break 语句终止 switch 的执行，程序继续执行 switch 之后的下一条语句。我们将在第 6 章中更详细地讨论 break 语句。switch 语句可以嵌套，并且 case 或 default 子句与包含的 switch 相关联。

例如，以下程序读取一个整数，如果它是 1，则输出 One；如果它是 2，则输出 Two；否则输出 Other。在任何情况下，break 语句都会终止 switch，程序输出 End。

~~~c
#include <stdio.h>
int main(void)
{
    int a;

    printf("Enter number: ");
    scanf("%d", &a);

    switch(a)
    {
        case 1:
            printf("One\n");
            break;

        case 2:
            printf("Two\n");
            break;

        default:
            printf("Other\n");
            break;
    }
    printf("End\n");
    return 0;
}
~~~

请注意，default case 是可选的；它也可以出现在 case 列表中的任何位置，并且如果没有匹配项则会被执行。如果存在，我们建议始终将其放在最后以使其清晰。如果缺少且没有匹配的 case，则不执行任何操作。

让我们为 default case 做一个括号。通常，它用于报告“不可能”的条件。有一次，我选择输出消息 Panic: Wish you weren't here 影射 Pink Floyd 的经典歌曲。正如你可能猜到的，这个错误情况在测试阶段从未出现过。你能想象它什么时候出现吗？在

```
case 3:
    printf("Three\n");
    break;
default:
    printf("Other\n");
    break;
}
printf("End\n");
return 0;
}
```

由于 a 为 1，第一个 case 输出 One。然而，由于没有 break，switch 语句不会终止，执行会落到下一个 case，直到遇到 break。因此，程序输出 Two 和 Three。break 语句终止 switch，程序显示 End。如果那个 break 缺失，程序也会输出 Other。最后一个 break 可以省略，因为右大括号 }  anyway 会终止 switch。我们更倾向于保留它，不仅为了保持统一的风格，而且作为一种安全保护，以防某天在那里添加另一个 case。

![](img/b8da5dcf9ba7f1fad5213c453d095246_115_0.png)

> 通常，缺少 break 是潜在错误的原因。如果你故意省略它，请添加注释明确说明，这样阅读你代码的人，甚至一段时间后的你也不会感到困惑。

如果我们想在多个 case 中执行相同的语句块，可以将它们合并在一起。例如：

```
case constant_1:
case constant_2:
case constant_3:
/* block of statements that will be executed if the value of the expression matches any of constant_1 or constant_2 or constant_3. */
break;
```

在另一个例子中，以下程序读取一个表示月份的整数（1 表示一月，12 表示十二月）并显示该月份所属的季节。

```c
#include <stdio.h>
int main(void)
{
    int month;

    printf("Enter month [1-12]: ");
    scanf("%d", &month);

    switch(month)
    {
        case 12:
        case 1:
        case 2:
            printf("Winter\n"); /* If the input value is 1, 2 or 12, the program outputs Winter. */
            break;

        case 3:
        case 4:
        case 5:
            printf("Spring\n");
            break;

        case 6:
        case 7:
        case 8:
            printf("Summer\n");
            break;

        case 9:
        case 10:
        case 11:
            printf("Autumn\n");
            break;

        default:
            printf("Error: Wrong month\n");
            break;
    }
    return 0;
}
```

## switch 与 if

switch 语句的主要缺点是我们只能进行相等性测试，即测试表达式的值是否与某个 case 常量匹配。相比之下，我们可以使用 if 来测试任何类型的条件。此外，case 常量仅限于整数，表达式也必须是整数变量或表达式。字符被视为小整数，因此可以使用，但浮点数和字符串不允许。另一方面，在某些情况下，用 switch 语句代替级联的 if-else-if 语句可能会使程序更易读。例如，switch 语句的典型用途是处理命令菜单中的用户选择。

## 练习

### C.5.21 编写一个程序模拟物理计算器。程序应读取算术运算的符号和两个整数并显示算术运算的结果。

```c
#include <stdio.h>
int main(void)
```
