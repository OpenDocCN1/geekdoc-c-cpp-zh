
`for` 循环按固定次数迭代，由三部分组成，例如初始化、条件表达式和后表达式。`for` 循环的语法如下：

```c
for(initialization,conditional_expression,post_expression)
    simple or compound statement
```

在正文中，`for` 循环由三部分组成：初始化、`conditional_expression` 和 `post_expression`；随后是简单语句或复合语句。初始化部分用一个值初始化变量。初始化只执行一次，之后是 `conditional_expression`。如果 `conditional_expression` 评估结果为假，则执行 `for` 循环后面的语句。如果 `conditional_expression` 评估结果为真，则执行 `for` 的循环体。`post_expression` 用于增加或减少控制 `for` 循环的计数器变量。`for` 循环持续执行直到 `conditional_expression` 评估结果为假。简单语句或复合语句代表 `for` 循环的循环体。

注意，当使用简单语句构建循环时，循环体不用大括号表示。列表 12 显示了带有简单语句的 `for` 循环：

- 列表 12：使用复合语句的 for 循环

输出:

前十个偶数如下：

2

4

6

8

10

12

14

16

18

20

在列表 12 中，通过 `for` 循环显示了前 10 个偶数。变量初始化为 2，并在每次迭代时增加 2，以便在每次迭代时显示偶数。当 `i` 的值超过 20 时，评估变为假，循环终止。

当一个 `for` 循环包含另一个循环时，它被称为嵌套循环。在嵌套 `for` 循环中，执行从外层循环开始，控制传递给内层循环。内层循环继续执行，直到内层 `for` 循环评估为真。当内层循环完成后，流传递给外层循环继续下一次迭代，并再次执行内层循环。这意味着对于外层循环的每次迭代，内层循环都会完全执行。列表 13 显示了嵌套循环的示例：

- 列表 13：嵌套 for 循环

```c
#include<stdio.h>
#include<conio.h>
int main() {
    int x,y,sum;
    clrscr();
    for(x=1;x<=20;x++) {
        for(y=1;y<2;y++) {
            sum=x+y;
            printf("x: %d\n",x);
            printf("y: %d\n",y);
        }
        printf("Sum: %d\n", sum);
    }
    getch();
    return 0;
}
```

输出 # 输出:

x: 1

y: 1

Sum: 1

y: 2

Sum: 3

y: 1

Sum: 3

x: 2

y: 2

Sum: 4

在列表 13 中，执行从外层 `for` 循环开始，其中 `x` 变量初始化为 1。现在，执行进入内层 `for` 循环，`y` 变量设置为 1。打印两个数字（x 和 y）的和。

内层 `for` 循环继续执行直到条件 `y<=2` 变为假。这样，内层循环执行了两次，`y` 变量的值从 1 变为 2。当内层循环完成后，执行转到外层循环，`x` 变量设置为 2。这次，内层循环再次执行，该循环后的语句也执行了两次。这样，外层循环和内层 `for` 循环在代码中被执行。

- 1. 你在 C 中如何执行循环？给出 C 语言中循环构造的语法。比较相同的部分。(VTU, 2003年7/8月)

- 2. 用通用语法解释任意三种形式的语句。(VTU, 2008年7/8月)

![](img/655987774ce63b710f1a1b263f2c84e0_330_0.png)

在学习迭代语句后，让我们探索跳转语句。

## 12.4 使用跳转语句

跳转语句是将控制从程序的某部分到另一部分的语句。C 支持的跳转语句如下：

- `break` 语句

- `continue` 语句

- `goto` 语句

让我们在后续章节中解释这些跳转语句。

### 使用 break 语句

`break` 用于用于打破循环或 `switch` 语句。打破循环意味着终止循环。列表 14 显示了使用 `break` 语句的示例：

- 列表 14：使用 break 语句

```c
#include<stdio.h>
#include<conio.h>
int main()
{
    int i=0;
    clrscr();
    while("true")
    {
        i+=2;
        if(i>10)
            break;
        printf("%d\n",i);
    }
    getch();
    return 0;
}
```

输出:

2

4

6

8

10

在列表 14 中，`i` 变量初始化为 0，`while` 循环显示 2 到 10 的数字。如果它大于 10，`break` 语句终止循环。

- 1. 解释 'C' 中 `break` 语句的使用。(VTU, 2007年7/8月)

- 2. 用示例解释 `continue` 语句以及 `break` 语句的重要性。(VTU, 2009年1/2月)

### 使用 continue 语句

`break` 语句打破整个循环，但 `continue` 语句打破迭代。换句话说，`continue` 语句带有下一个条件进入循环。列表 15 显示了使用 `continue` 语句的示例：

- 列表 15：使用 continue 语句

```c
#include<stdio.h>
#include<conio.h>
int main()
{
    int i;
    clrscr();
    for(i=2;i<=20;i+=2)
    {
        if(i==6 || i==14)
            continue;
        printf("%d\n",i);
    }
    getch();
    return 0;
}
```

输出:

2

4

8

10

12

16

18

20

在列表 15 中，显示了 10 个偶数，排除了 6 和 14。这是通过 `if` 条件内的 `continue` 语句实现的，当 `i` 变量变为 6 或 14 时执行该语句。

- 1. 解释循环中 `break` 和 `continue` 语句的使用。用示例辅助你的解释。(VTU, 2005年7/8月)

- 2. `break` 和 `continue` 语句之间有什么区别？每个给出一个示例。(VTU, 2008年1/2月)

- 3. 关于以下内容写笔记：

   i `break` 语句

   ii `continue` 语句

ii `continue` 语句 (VTU, 2008年7/8月)

### 使用 goto 语句

`goto` 语句用于从程序的某个部分转移到另一部分。该语句使用用户定义的标签来指定程序中的 `goto` 语句。使用 `goto` 语句的语法如下：

```c
goto label_name;
...
label_name:statement;
```

在上述语法中，`<label_name>` 指定了控制转移的目标语句的用户定义标签。该标签后面应跟一个冒号，且目标语句必须位于标签之前。

# 314 第12章

## 列表 16：使用 goto 语句

```c
#include <stdio.h>
#include <conio.h>
int main() {
    int arr[5],j,k;
    clrscr();
    printf("\A grade\n");
    printf("Enter the marks of any five students\n");
    for(j=0;j<5;j++) {
        scanf("%d",&arr[j]);
    }
    printf("Student grades are\n");
    for(k=0;k<5;k++) {
        if(arr[k]<40) {
            printf("Fail\n");
            continue;
        } else if(arr[k]>=70 && arr[k]<=90) {
            printf("A grade\n");
        } else if(arr[k]>=40 && arr[k]<70) {
            printf("C grade\n");
        } else {
            printf("B grade\n");
        }
    }
    getch();
    return 0;
}
```

输出：

Enter the marks of any five students

92

75

65

86

23

Student grades are

A grade

B grade

C grade

B grade

Fail

在列表 16 中，五名学生的成绩是基于运行时输入的数的。如果输入的分数小于 40，程序的控制权将传递给 `goto` 语句 `[lbl]`。`goto` 语句之后的语句将被执行，并显示 `Fail`。`goto` 语句内部的 `continue` 语句将控制权传回给 `if` 语句以评估其他分数。如果输入的分数大于 90，则显示 `A grade`；而如果输入的分数大于 70 且小于 90，则显示 `B grade`。如果输入的分数在 40 到 70 之间，则显示 `C grade`。

极不建议使用 `goto` 语句，因为它通过创建许多不同的执行路径，会使程序的调试变得困难。这种具有复杂控制结构的程序被称为“面条代码”（spaghetti）。

![](img/655987774ce63b710f1a1b263f2c84e0_334_0.png)

- 1. 列出 C语言中不同的控制语句。用示例解释其中任意一个。(VTU, July/August 2004)

- 2. 给出 C 中 3 类型循环的语法。解释每个循环的工作原理。为每种循环提供一个示例。(VTU, Jan./Feb. 2006)

- 3. 结合示例解释控制语句 (VTU, July/August 2006)

通过这个主题，我们结束了本章，让我们总结一下要点。

## 总结

在本章中，你学习了各种控制结构。本章从探索控制结构的语法开始，其中我们解释了简单语句和复合语句的区别。接下来，你学习了条件语句，例如 `if else` 和 `switch`。你还学习了如何创建嵌套 `if` 语句、`switch` 语句和 `if-else` 阶梯。接下来，我们解释了迭代语句：`while` 循环、`do-while` 循环和 `for` 循环。在本章结束时，你学习了跳转语句：`break`、`continue` 和 `goto`。

## 快速复习

- Q1. 写一个程序，接收并相乘 10 个实数（浮点数）。答。

```c
#include <stdio.h>
#include <conio.h>
int main(){
  int i;
  float a,pro=1;
  clrscr();
  /* 输入和计算段 */
  printf("Give the input:-\n");
  for(i=1;i<=10;i++){
    printf("No.%d:-",i);
    scanf("%f",&a);
    pro*=a;
  }
  /* 输出段 */
  printf("The product is %f\n",pro);
  getch();
  return 0;
}
```

# 316 第12章

输出：

Give the input:-

No.1:-1.1

No.2:-2.2

No.3:-3.3

No.4:-4.4

No.5:-5.5

No.6:-6.6

No.7:-7.7

No.8:-8.8

No.9:-9.9

No.10:-10.10

The product is 864208600000

Q2. 写一个程序打印 4 的第 n 项乘法表。

输出：

Give the value of n:-10

1*4=4

2*4=8

3*4=12

4*4=16

5*4=20

6*4=24

7*4=28

8*4=32

9*4=36

10*4=40

Q3. 写一个程序读取两个浮点数并测试它们在小数点后两位是否相同。

```c
/* 验证两个数在小数点后两位相等的程序 */
#include<string.h>
#include<stdio.h>
#include<math.h>
#include<conio.h>
int main()
```

```c
{
float a,b;
int c,d;
clrscr();
/* 输入段 */
printf("%f%f numbers:-\n");
scanf("%f%d",&a,&b); //（注：原文代码中此处可能有误，翻译保留原样）

...（此处省略部分未翻译逻辑代码）...
```

Q4. 写一个程序，提示用户输入一个数字并生成到该数字的斐波那数列。注意在斐波那数列中，前两个值都是 1，随后的每个值都是之前值的和。答。

输出：

The nth term is 34

# 318 第12章

Q5. 写一个程序要求用户输入整数并打印因数。答。

...（代码）

Q6. 写一个程序使用 `for` 循环计算 n 个数的和（n 由用户提供）。答。

...（代码）

Q7. 写一个程序判断一个数字是否为质数。答。

...（代码）

# 320 第12章

Q8. 将以下 `do` 循环重写为 `while` 循环。

...（代码）

Q9. 写一个 C 程序给出以下输出。

...（代码）

Q10. 写一个程序接收数组 `X[100]` 的输入数据。然后计算和并打印输入的 `X` 中大于平均值和小于平均值的数。答。

# 控制结构

```c

/* 评估数组中元素的程序 */

#include<stdio.h>

#include<conio.h>

/* 主程序开始 */

void main()

{

    int x[100];

    int n,i,sum=0,less=0,more=0;

    float avg;

    clrscr();

    /* 输入段 */

    printf("\ngive the number of input:-");

    scanf("%d",&n);

    for(i=1;i<=n;i++)

    {

        printf("\nkno. %d ",i);

        scanf("%d",&x[i]);

    }

    /* 计算 */

    sum+=x[i];

    avg=sum/n;

    for(i=1;i<=n;i++)

    {

        if(x[i]>=avg) more++;

        else less++;

    }

    printf("\nsum of the elements is %d",sum);

    printf("\naverage of the elements is %f",avg);

    printf("\nelements greater than average is %d",more);

    printf("\nelements less than average is %d",less);

    getch();

}

```

# 322 ► 第12章

```c

i++;

if(i<=10)

goto again;

getch();

return 0;

```

输出:
1 2 3 4 5 6 7 8 9 10

Q12. 假设初始 `x=5, y=0, z=0`，执行以下代码段后，`z` 的值是多少？

```c

if (x == 0 || x && y)

    if (!y)

        z = 1;

    else

        z = 2;

else

    z = 3;

```

A. 0 B. 1 C. 2 D. 3 (VTU, 2009年1/2月)

答：D. 3

Q13. 下列哪一个 'C' 语句从程序中的一个点无条件地跳转到另一个点？(VTU, 2009年1/2月)

A. `if` B. `goto` C. `switch` D. `else`

答：A. `if`

Q14. 没有测试条件的循环被称为 ______ 循环。

- A. 有限的 B. 无限的 C 控制的 D 均都不是
(VTU, 2009年1/2月)

答：B. 无限

Q15. 下列哪种结构是退出控制循环？

- A. `while` B. `do..while` C. `for` D 均都不是
(VTU, 2009年1/2月)

答：A. `while`

Q16. 下述代码段的输出是什么？

```c

x = 4;

do:

    printf("%d\n", x);

while (x -- >= 0);

```

A. 错误 B. 4321 C. 43210 D. 43210-1 (VTU, 2009年1/2月)

答：D. 43210-1

Q17. 给定三角形的三条边，编写一个 C 程序将三角形分类为等边三角形、等腰三角形和不等边三角形。(VTU, 2003年1/2月)

答：

```c

#include<stdio.h>

#include<conio.h>

main()

{

    int p,q,r;

    clrscr();

    printf("\n 输入三角形三条边的值");

    scanf("%d %d %d", &p, &q, &r);

    if ((p==r) && (q==r) && (p==q))

    {

        printf("\n 给定的三角形是等边三角形");

    } else if ((p==r)&&(q==r) && (p==q))

    {

        printf("\n 给定的三角形是等腰三角形");

    } else

    {
