
The value of e to the power of y is 7.389056

### Q14. 写一个 C 程序在不使用算术运算符的情况下计算两个数的和。

Ans. 你可以使用复合赋值运算符在不使用算术运算符的情况下计算两个数的和。使用复合赋值运算符计算两个数的和的程序为：

```c
#include <stdio.h>
void main() {
    int a=20;
    int b=20;
    int c;
    c += b;
    printf("%d", c);
    getch();
}
```

Output: 40

### Q15. 这两个语句之间的区别是什么？

```c
#include <stdio.h>
#include "stdio.h"
```

Ans. 前述语句都使用了`stdio.h`文件。第一条语句使用角括号头文件，第二条语句使用双引号头文件。两者的区别在于，当头文件被包含在角括号中时，文件只会在标准指令中搜索。当头文件被包含在双引号中时，文件会首先在指定的目录中搜索，然后在标准目录中搜索。

### Q16. 下面 C 程序的输出是什么？

```c
#include <stdio.h>
void main() {
float a=5.2;
if(a==5.2)
printf("Equal\n");
else if(a<5.2)
printf("Less than\n");
else
printf("Greater than\n");
getch();
}
```

Ans. Less than

### Q17. 下面 C 程序的输出是什么？

```c
#include <stdio.h>
void main() {
    printf("%d",sizeof(5.2));
    getch();
}
```

Ans. 8

# 在 C语言中操作运算符和表达式

iii. `$x^5+10x^4+8x^3+4x+2$

iv. `$(4x+3)(2y+2z+4)$`

| a |

|---|


| b | `(b-a)` |

答：

- i. `$(a*b)/(a*x);`

- ii. `$(2*x)+(3/y))/(x-6);`

- iii. `$(pow(x,5)+(10*pow(x,4))+(8*pow(x,3))+(4*x)+2);`

- iv. `$(a+3)*(2y)+(2*z)+4;`

- v. `$a^{(b-2)}$;`

Q19. 求出每个以下表达式的结果。

`int i=4, j=2, k=6, a=2;`

- i. `$k=i+1$;`

- ii. `$j=i/k$;`

- iii. `$i=i/3$;`

- iv. `$m=i+(j=2+k);$`

- v. `$a=1*j/2$;`

答。 i. 36 ii. 0 iii. 0 iv. 12 (VTU, Jan/ Feb 2007)

Q20. 写一个程序，使用级数求 (sin) x 的和。

`$\sin(x) = x - \frac{x^3}{3!} + \dots$` 直到 N 项。

同时使用库函数打印和(sin x)。 (VTU, July/ August 2003)

答答。

```c
#include <stdio.h>
#include <math.h>
main () {
    double x, r, m, sin, term;
    int n, p;
    printf("\n enter the value of x: ");
    scanf("%f", &x);
    printf("\n enter the number of terms: ");
    scanf("%d", &n);
    x=x*(3.14/180);
    sin=0;
    for(p=1; p<=n; p+=1) {
        term=pow(x,p)/p;
        sin=sin+term;
    }
    printf("\n Sin series=%f\n", sin);
    printf("\n Sin series by fun=%f\n", r);
    r=sin;
    printf("\n calculated result=%f\n", r);
}
```

Q21. 写一个 C 程序计算 cos (x) = `$1 - \frac{x^2}{2!} + \frac{x^4}{4!} \dots$` 直到 15 项，并列出从 `$0^{\circ}$` 到 `$180^{\circ}$` 以 `$10^{\circ}$` 为步长的值。

答。

```c
#include <stdio.h>
#include <math.h>
main () {
    double x, sum, s=-1, fact, i;
    int term, q;
    printf("Enter the number of term");
    scanf("%d", &term);
    printf("Give the value of x");
    scanf("%f", &x);
    x=x*(3.142/180);
    cos(x);
    for(i=2; i<term; i=i+2) {
      fact=1;
      for(q=1; q<i; q++) {
        fact=fact*q;
      }
      sum=cos(x)+pow(x,i)/fact* s;
      s=s*(-1);
    }
    printf("Value of cos is %1f", sum, cos);
}
```

Q22. 将以下数学表达式转换为 'C' 表达式。

- i. `$x^{1/2} + x^{2/3} + x^{3/4} + x^{5/2} + x^{7/2}$`

- ii. `$\frac{a+b}{c}$`

- iii. `$\sqrt{x}$`

- iv. `$\sqrt{e^x + y}$`

- v. `$\sqrt{x\sin{y}}$`

- vi. `$\frac{\sin45^{\circ}\cos30^{\circ}}}{\alpha+\beta}$`

答。(VTU, July/ August 2005)

- i. `pow(x,1/2) + pow(x,2/3) + pow(x,3/4) + pow(x,5/2) + pow(x,7/2)`

- ii. `(a+b)/c`

- iii. `sqrt(x)`

- iv. `sqrt(exp(x) + y)`

- v. `sqrt(x*sin(y))`

- vi. `(sin(45)*cos(30))/(alpha+beta)`

# 12 控制结构

目标：

- 12.1 探索控制结构的语法

- 12.2 条件语句

- 12.3 循环语句

- 12.4 跳转语句

在编程语言中，程序不仅仅是指令的线性序列。例如，你需要创建重复代码或进行决策。C语言提供了控制结构，也称为控制流。控制结构决定了在不同情况下执行什么。控制结构分为：

- **条件语句**：指定执行一组语句。控制结构包括 `if-else` 和 `switch`。

- **循环语句**：满足条件执行一个或多个语句。控制结构包括 `while`、`do-while` 和 `for` 循环。

- **跳转语句**：将控制从程序的某部分转移到另一部分。跳转语句包括 `goto`、`break` 和 `continue`。

在本章中，你学习各种控制结构。章节从控制结构的语法开始。接下来，你学习 `if-else` 和 `switch` 等条件语句。然后解释 `while` 循环、`do-while` 循环和 `for` 循环。在本章最后学习 `break` 和 `continue` 等跳转语句。

### 12.1 探索控制结构的语法

通常情况下，控制结构的语法涉及复合语句或块，用分号（`;`）分隔并使用大括号 `{}` 分组。注意简单语句和复合语句的区别。简单语句是以分号（`;)`结尾的简单指令。而复合语句则是使用大括号 `{}` 分组的多个指令或语句。以下是复合语句的语法：

```c
{
statement 1;
statement 2;
statement 3;
}
```

C语言中的复合语句示例：

```c
{
printf("First statement");
printf("Second statement");
printf("Third statement");
}
```

应该注意，在简单语句的情况下不需要使用 `{}` 大括号。

## 12.2 条件语句

条件语句是一种控制结构，允许你在程序中选择一个或多个执行路径。在评估给定的条件表达式后，如果条件表达式为真，则执行相应的代码块；否则，跳过该代码块。C支持的条件语句列表如下：

- `if` 语句

- `if-else` 语句

- 嵌套 `if` 语句

- `if-else` 链

- `switch` 语句

- 嵌套 `switch` 语句

现在详细探索并创建这些语句。

#### 使用 if语句

`if`语句执行简单或复合语句，取决于表达式真还是假。使用`if`语句的语法是：

```c
if(conditional expression)
statement;
```

或者

```c
if(conditional expression)
{
statement 1;
statement 2;
statement 3;
}
```

在上述语法中，当`if`语句中给出的条件表达式为真时，执行简单或复合语句（语句块）。否则，程序控制传递到下一个语句。如果条件表达式为假，C编译器什么都不做。注意括号内的条件表达式必须被求值为真（非零值）或假（零值）。此外，复合语句必须用大括号括起来。以下是在`if`语句中使用条件表达式的示例：

```c
if(a>b)          /* 非零值返回真。 */
if(0)            /* 零值返回假。 */
if(i<=0)         /* 如果i<=0为真，否则为假。 */
if(i = 0)        /* 因为表达式值为零，为假。 */
```

以下代码片段显示了`if`语句配合简单语句的示例：

```c
if (a>b)
i = i + 1;      /* 语句1*/
j = j + 1;      /* 语句2*/
}
```

在前面的代码片段中，条件表达式 `a>b`为真，执行标记为1和2的语句。

以下代码片段显示了`if`语句配合复合语句的示例：

```c
if (a>b) {
i = i + 1;      /* 语句1*/
j = j + 1;      /* 语句2*/
}
```

在前面的代码片段中，条件表达式 `a>b`为真，标记为1和2的语句都将被执行。

列表1显示了使用`if`语句的示例：

列表1：使用`if`语句

```c
#include <stdio.h>
#include <conio.h>
int main() {
    int age;
    clrscr();
    printf("Enter your age\n");
    scanf("%d",&age);
    if(age<18)
        printf("You are not eligible to give vote\n");
    else
        printf("You are eligible to give vote\n");
    getch();
    return 0;
}
```

# 第 12 章

17

你没有投票资格

在列表 1 中，你需要在运行时输入年龄。如果输入的年龄小于 18 ，则会显示“你没有投票资格”的消息；如果输入的年龄大于 18 ，则会显示“你有投票资格”的消息。

- *使用 if-else 语句*

`if-else` 语句在 `if` 语句中提供的条件表达式为真时，执行一个简单或复合语句。当条件表达式为假时，它执行另一个简单或复合语句，然后执行 `else` 语句。

以下是 `if-else` 语句的语法：

```
if (conditional expression)
    简单或复合语句 1
else
    简单或复合语句 2
```

在前面的代码中，当 `if` 子句中指定的条件表达式为真时，执行简单或复合语句 1；否则，执行简单或复合语句 2。

下面的代码片段展示了 `if-else` 语句的使用示例：

```
if (a<b)
    printf(" big number is %d", a);    /* 语句 1*/
else
    printf(" big number is %d", b);    /* 语句 2*/
```

在前面的代码片段中，如果变量中存储的值大于变量 `b` 中存储的值，则执行标记为 1 的语句；否则，执行标记为 2 的语句。

列表 2 显示了 `if-else` 语句的使用：

- *列表 2：使用 if-else 语句*

```
#include<stdio.h>
#include<conio.h>
int main() {
    int age;
    clrscr();
    printf("Enter your age\n");
    scanf("%d",&age);
    if(age<18)
        printf("you are not eligible to give vote\n");
    else
        printf("you are eligible to give vote\n");
    getch();
    return 0;
}
```

输入你的年龄

你有投票资格

你需要在运行时输入年龄。如果输入的年龄小于 18，则会显示“你没有投票资格”的消息；否则，会显示“你有投票资格”的消息。

# 创建嵌套 if 语句

嵌套 `if` 语句是指一个语句中包含另一个 `if` 语句。当外部 `if` 语句被求值为真时，程序的控制权会移动到内部 `if` 语句。使用以下语法来创建嵌套 `if`：

```
if(conditional expression1)
    /* 当条件表达式1 为真时执行的语句 1 */
    if(conditional expression2)
        /* 当条件表达式2 为真时执行的语句 2 */
```

在前面的语法中，首先执行条件表达式1，当它求值为真时，执行语句 1，并且程序的控制权传递到内部的 `if` 语句。当内部 `if` 语句的条件表达式2 为真时，执行语句 2。列表 3 显示了嵌套 `if` 的示例：

- 列表 3：创建嵌套 if 语句

```
#include<stdio.h>
#include<conio.h>
int main()
{
    int num;
    clrscr();
    printf("Enter a number greater than 0\n");
    scanf("%d",&num);
    if(num>0)
    {
        if(num>50)
        {
            if(num>100)
            {
                printf("The number is greater than 500\n");
            }
            printf("The number is greater than 100\n");
        }
        printf("The number is greater than 50\n");
    }
    printf("The number is greater than 0\n");
    }
    getch();
    return 0;
}
```

输出：

nEnter a number greater than 0

400

The number is greater than 100

The number is greater than 50

The number is greater than 0

在列表 3 中，`num` 是一个整数变量，由你在运行时初始化。这里使用了四次 `if` 语句，它们彼此嵌套在一起。第一个 `if` 语句检查 `num` 变量的输入值是否大于 0，然后第二个语句检查 `num` 变量的值是否大于 50。当第二个语句结果为真时，第三个 `if` 语句检查 `num` 变量是否大于 100。当第三个 `if` 语句结果为真时，第四个 `if` 语句检查 `num` 变量是否大于 500。在 `if` 的每一层级上，都会通过 `printf()` 函数显示相应的消息。在案例中，我们在运行时输入了数字 400，所以显示了相应的消息。

- *使用 if-else 阶梯*

当按顺序使用多个 `if-else` 语句时，它被称为 `if-else` 阶梯。

使用 `if-else` 阶梯的语法为：

```
if (conditional expression 1)
简单或复合语句    /* s1*/
else if (conditional expression 2)
简单或复合语句    /* s2*/
else if (conditional expression 3)
简单或复合语句    /* s3*/
...
else if (conditional expression n)
简单或复合语句    /* sn*/
```

如果条件表达式 1 为真，则执行标记为 `s1` 的语句。如果条件表达式 1 为假且条件表达式 2 为真，则执行标记为 `s2` 的语句。这个过程一直持续到条件表达式 n，其中 n 是一个正实数。你应该注意，根据条件表达式的不同，`s1`、`s2`、`s3` 中只有一个会被执行。

列表 4 显示了一个 `if-else` 阶梯的示例：
