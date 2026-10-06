

# goto 语句下的标签定义

goto label2;
label2:

# goto 语句的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_80_0.png)

# goto 在编程中的用法

**goto** 会使程序的可读性降低、容易出错且难以查找错误。由于从函数的一个部分到另一个部分的无条件控制转移，在某一点，程序员无法判断程序是如何到达你代码中的某个特定位置的。因此，大多数程序员都避免使用 **goto**。

**重要提示：** 你应该尽可能避免使用 **goto**。尝试用 **if...else, switch...case** 和**循环语句**的组合来替换 goto 语句。

考虑下方的 **goto** 示例，以演示在何时以及为什么你应该避免使用 **goto**。

```c
#include <stdio.h>

int main()
{
    int i=1;
    start:
    goto print;
    print:
    printf("%sd ", i);
    goto next;
    increment:
    i++;
    goto print;
    next:
    if(i < 10)
        goto increment;
    else
        goto exit;
    printf("I cannot execute.");
    exit:
    return 0;
}
```

上面的程序很难阅读且难以发现错误（如果有的话）。因此，在这种情况下，你必须避免使用 goto。

好的，包括我在内的许多程序员都讨论过 goto 的不可靠性。然而，goto 在很多情况下是有用的，例如：

- 跳出深层嵌套循环。
- 从其他地方将控制权转移到任何嵌套循环层。

**注意：** 你可以使用 goto 和 if...else 的组合来构建任何循环。

# C 语言中的 switch 语句

C 语言中的 switch 语句是 if-else-if 阶梯语句的替代方案，它允许我们对名为 switch 变量的单个变量的不同可能值执行多个操作。在这里，我们可以为单个变量的不同值在多个 case 中定义各种语句。

switch 语句测试变量的值并将其与多个 case 进行比较。当找到匹配的 case 时，将执行与该特定 case 相关的语句块。

switch 块中的每个 case 都有不同的名称/数字，称为标识符。用户提供的值将与 switch 块中的所有 case 进行比较，直到找到匹配。

如果找到匹配的 case，则执行默认（default）语句，控制将离开 switch 块。

# C 语言 switch 语句的规则

1. switch 表达式必须是整数或字符类型。
2. case 值必须是整数或字符常量。
3. case 值只能在 switch 语句内部使用。
4. switch case 中的 break 语句不是必须的。它是可选的。如果在 case 中没有找到 break 语句，则匹配 case 之后的所有 case 都将执行。这在 C switch 语句中被称为“穿透”（fall through）状态。
5. Case 值必须是常量且唯一的。
6. Case 标签必须以冒号（:）结尾。
7. 只能有一个 default 标签。
8. 每个 case 中必须存在一个 break 关键字。
9. 我们可以嵌套多个 switch 语句。

让我们通过示例来尝试理解它。假设有以下变量：

```c
int x,y,z;
char a,b;
float f;
```

# 使用控制语句和循环

| 有效 switch | 无效 switch | 有效 Case | 无效 Case |
| :--- | :--- | :--- | :--- |
| switch(x) | switch(f) | case 3; | case 2.5; |
| switch(x>y) | switch(x+2.5) | case 'a'; | case x; |
| switch(a+b-2) | | case 1+2; | case x+2; |
| switch(func(x,y)) | | case 'x'>'y'; | case 1,2,3; |

# C 语言 switch 语句的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_83_0.png)

C 语言 switch 语句的语法如下：

```c
switch(expression){
    case value1:
        // 要执行的代码;
        break; // 可选
    case value2:
        // 要执行的代码;
        break; // 可选
        ....
    default:
        // 如果所有 cases 都不匹配时执行的代码;
}
```

# switch case 语句的功能

首先，求值 switch 语句指定的整数表达式。然后将该值与不同 case 给出的常量值逐一匹配。如果找到匹配项，则执行该 case 中指定的所有语句，以及该 case 之后的所有 case，包括 default 语句。任何两个 case 不可以有相似的值。如果匹配的 case 包含 break 语句，则之后的所有 case 都将被跳过，控制将离开 switch。否则，匹配 case 之后的所有 case 都将执行。

让我们来看一个 C 语言 switch 语句的简单示例。

# Switch case 示例 1:

```c
#include<stdio.h>
int main(){
    int number=0;
    printf("enter a number:");
    scanf("%d",&number);
    switch(number){
        case 10:
            printf("number is equal to 10");
            break;
        case 50:
            printf("number is equal to 50");
            break;
        case 100:
            printf("number is equal to 100");
            break;
        default:
            printf("number is not equal to 10, 50 or 100");
    }
    return 0;
}
```
输出：
enter a number:10
number is equal to 10

# Switch case 示例 2:

```c
#include<stdio.h>
int main(){
    int x=10;
    int y=5;
    switch(x>y){
        case 1:
            printf("hi");
            break;
        case 0:
            printf("bye");
            break;
    }
    return 0;
}
```
输出：
hi

# C switch 语句穿透

C switch 语句穿透意味着如果不使用 break 语句，匹配 之后的所有 case 都将执行。让我们尝试下面的示例。

```c
#include<stdio.h>
int main(){
    int number=0;
    printf("enter a number:");
    scanf("%d",&number);
    switch(number){
        case 10:
            printf("number is equal to 10");
        case 50:
            printf("number is equal to 50");
        case 100:
            printf("number is equal to 100");
        default:
            printf("number is not equal to 10, 50 or 100");
    }
    return 0;
}
```
输出：
enter a number:10
number is equal to 10
number is equal to 50
number is equal to 100

# 嵌套 switch case

我们可以在 switch 内部使用任意数量的 switch 语句。考虑以下示例：

```c
#include <stdio.h>
int main () {
  int i = 10;
  int j = 20;

  switch(i) {
    case 10:
      printf("the value of i evaluated in outer switch: %d\n",i);
    case 20:
      switch(j) {
        case 20:
          printf("The value of j evaluated in nested switch: %d\n",j);
      }
  }

  printf("Exact value of i is : %d\n", i);
  printf("Exact value of j is : %d\n", j);

  return 0;
}
```
输出：
the value of i evaluated in outer switch: 10
The value of j evaluated in nested switch: 20
Exact value of i is : 10
Exact value of j is : 20

# 循环语句

# 简介

计算机是执行重复任务的最合适机器，可以不知疲倦地执行成千上万次。每种编程语言都通过某些形式的语句来完成此类重复任务。重复执行一组语句的过程被称为循环。语句根据条件执行多次。但如果给定的逻辑使得重复可以任意次数进行，而没有固定条件来停止这些语句，那么这种类型的循环被称为无限循环。

循环语句允许我们多次执行一个语句或一组语句。在 C 编程语言中，有三种循环：while、do-while 和 for。

# 为什么要使用循环？

当你需要多次执行一段代码块时，你需要在 C 语言中使用循环概念。

# 循环语句的优点

- 减少代码长度。
- 占用较少的内存空间。
- 减轻开发者的负担。
- 缩短了执行程序的耗时过程。

