
**初始化**  循环的这一部分最先执行。这一部分的语句只执行一次。该语句涉及一个循环控制变量。

**测试表达式**  TestExpr 表示一个测试表达式，它必须为真，循环才能继续执行。

**语句**  stmt 是单条语句或语句块。

**更新**  这里包含的语句在每次通过循环时、在测试循环条件之前执行。该语句也涉及一个循环控制变量。

C 允许将循环控制变量的更新写在循环体内部。for 循环的示例如下：

```c
int main(void)
{
    int i;
    for(i = 0; i < 10; i++)
        printf("%d", i);
    return 0;
}
```

上述 for 循环的操作如下：

- 1. 将 i 设为 0。
- 2. 如果 i 小于 10，执行循环体，即 `printf`，然后转到步骤 3；否则，转到 for 循环之后的下一条指令并继续。
- 3. 递增 i。
- 4. 转到步骤 2。

下图解释了上述程序中使用的 for 循环里由分号分隔并控制循环操作的三个表达式。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_242_0.png)

该循环将产生以下输出：

```text
0123456789
```

注意，从 0 到 9“运行循环”会执行循环体 10 次。for 结构的流程图如图 10.11 所示。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_242_1.png)

图 10.11 for 结构流程图

需要注意的是，前面循环的所有四个部分都存在于 for 循环中，尽管它们被压缩到一行中。一般来说，for 循环可以写成等价的 while 循环，反之亦然。

## 有界循环与无界循环的等价性

现在我们应该能够理解，for 和 while 控制流语句都密切相关。然而，要完全理解这一点，需要解释 for 结构的三个“部分”并不总是初始化、条件和修改。

一般来说，for 循环可以写成等价的 while 循环，反之亦然。for 循环

```c
for(initialization; TestExpr; updating)
{
    stmt;
}
```

等价于以下 while 结构：

```c
initialization;
while (TestExpr)
{
    stmt;
    updating;
}
```

以下示例说明了一个打印 1、2、3、4、5 的 for 循环。

在两种情况下，测试表达式都应产生一个布尔值，即真或假，因为需要真值来确定循环是否应继续执行。

让我们用一个打印 1、2、3、4 和 5 的示例来说明“while”和“for”循环结构之间的相似之处。上述问题的算法如下：

- 1. 开始
- 2. C ← 1
- 3. 打印 C
- 4. C ← C+1
- 5. 如果 C<=5，则转到步骤 3
- 6. 停止

该问题对应的 C 程序可以使用 while 或 for 结构。下面展示了两个版本，一个使用 for 结构，另一个使用 while 结构，以及它们的等价关系：

```c
// for version
#include <stdio.h>
int main(void)
{
    int c;  // Initialization
    for(c=1; c<=5; c++)  // TestExpr, Updating
    {
        printf("%d", c);
    }
    return 0;
}

// while version
#include <stdio.h>
int main(void)
{
    int c;
    c=1;  // Initialization
    while(c<=5)  // TestExpr
    {
        printf("%d", c);
        c++;  // Updating
    }
    return 0;
}
```

为了测试对 while 和 for 循环的理解，将实现一种循环到另一种循环的转换。假设下面说明中给出的一个 while 循环需要转换为构造良好的 for 循环。

```c
float C = 2.0;
char chr = 'F';
while(C > 0.01) {
    printf("%f \n",C);
    C /= 10;
}
```

为了便于转换，请注意循环的四个部分。

```c
float C = 2.0;          /* initialization */
char chr = 'F';
while(C > 0.01) {       /* test expression */
    printf("%f \n",C);  /* body of the loop */
    C /= 10;            /* updating */
}
```

给定这些信息，就可以转换为 for 循环。for 循环为

```c
float C;
char chr = 'F';

for(C = 2.0; C > 0.01; C /= 10)
{
    printf("%f \n",C);
}
```

在这种情况下有一个小技巧。尽管声明并初始化了两个变量，但 while 循环中只使用了一个。因此，在 for 循环中只初始化那个特定变量 C。

现在，考虑将以下 for 循环转换为相应的 while 循环。

```c
int index;
int Total;
for(Total = 0, index = 0; index < 10; index += 1)
{
    if(index > 5)
        Total += index;
    else if(index < 5)
        Total -= index;
}
```

再次注意循环的四个部分，转换如下：

```c
int index = 0;
int Total = 0;
while(index < 10)
{
    if(index > 5) Total += index;
    else if(index < 5)
        Total -= index;
    index += 1;
}
```

必须强调，在 for 结构中，条件是在执行循环体中包含的语句和更新之前测试的；循环体可能从未执行或测试。

使用 for 循环生成迭代的事件顺序如下。

- 1. 计算*初始化*表达式。
- 2. 如果*测试表达式*的值为假，则终止循环，即转到步骤 6；否则转到步骤 3。
- 3. 执行语句或语句块。
- 4. 计算*更新*表达式。
- 5. 转到步骤 2。
- 6. 执行下一条语句。

绘制了 for 结构的执行周期以帮助理解该概念。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_243_0.png)

```c
int main()
{
    int counter = 2, number, max;
    printf("Enter an integer number\n");
    scanf("%d", &max);
    while(counter <= 10)
    {
        printf("Enter an integer number\n");
        scanf("%d", &number);
        if(number > max)
            max = number;
        counter++;
    }
    printf("The maximum number is %d\n", max);
    return 0;
}
```

for 语句后不能有分号，否则会导致不同的输出。考虑以下程序。

```c
#include <stdio.h>
int main()
{
    int c;
    for(c=1; c<=5; c++);
        printf("%d", c);
    return 0;
}
```

printf 语句前的分号意味着循环只递增 c 的值。这个 for 循环中没有包含可执行语句，即语句块中没有语句。输出将是 6，因为循环一直持续到 c=5。当 c 的值为 6 时，测试表达式求值为假，循环终止。

### for 循环的一些变体

从语法角度来看，for 语句中不必同时存在初始化、测试表达式和更新这三个表达式，但分号必须存在。然而，应清楚理解省略的标准和后果。

任何初始化语句都可以用在 for 循环的第一部分。多个初始化应使用逗号运算符分隔。

### 示例

- 24. 打印数列 1+2+3+4+... 前 n 项的和。

程序 1

```c
#include <stdio.h>
int main()
{
    int c, s=0, n;
    printf("\n Enter the No. of terms");
    scanf("%d", &n);
    for(c=1; c<=n; c++)
        s+=c;
    printf("\n Sum is %d", s);
    return 0;
}
```

程序 2 等价于程序 1

```c
#include <stdio.h>
int main()
{
    int c=1, s, n;
    printf("\n Enter the No. of terms");
    scanf("%d", &n);
    for(s=0; c<=n; c++)
        s+=c;
    printf("\n Sum is %d", s);
    return 0;
}
```

程序 3

```c
#include <stdio.h>
int main()
{
    int c, s, n;
    printf("\n Enter the No. of terms");
    scanf("%d", &n);
    for(c=1, s=0; c<=n; c++)
        s+=c;
    printf("\n Sum is %d", s);
    return 0;
}
```

- 如果不需要初始化，或者初始化在 for 循环之前完成，则可以通过只给出一个分号来跳过初始化语句。这使用前面的程序来说明。

```c
#include <stdio.h>
int main()
{
    int c=1, s=0, n;
    printf("\n Enter the No. of terms");
    scanf("%d", &n);
    for(; c<=n; c++)
        s+=c;
    printf("\n Sum is %d", s);
    return 0;
}
```

