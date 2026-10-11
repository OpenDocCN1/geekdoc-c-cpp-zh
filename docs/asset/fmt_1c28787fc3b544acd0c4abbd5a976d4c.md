
```c
int x,y,z;
char a,b;
float f;
```

#### 使用控制语句和循环

| 有效 switch | 无效 switch | 有效 Case | 无效 Case |

| :--- | :--- | :--- | :--- |

| switch(x) | switch(f) | case 3; | case 2.5; |

| switch(x>y) | switch(x+2.5) | case 'a'; | case x; |

| switch(a+b-2) | | case 1+2; | case x+2; |

| switch(func(x,y)) | | case 'x'>'y'; | case 1,2,3; |

#### C 语言 switch 语句的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_83_0.png)

C 语言 `switch` 语句的语法如下：

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

#### switch case 语句的功能

首先，求值 `switch` 语句指定的整数表达式。然后将该值与不同 `case` 给出的常量值逐一匹配。如果找到匹配项，则执行该 `case` 中指定的所有语句，以及该 `case` 之后的所有 `case`，包括 `default` 语句。任何两个 `case` 不可以有相似的值。如果匹配的 `case` 包含 `break` 语句，则之后的所有 `case` 都将被跳过，控制将离开 `switch`。否则，匹配 `case` 之后的所有 `case` 都将执行。

让我们来看一个 C 语言 `switch` 语句的简单示例。

#### Switch case 示例 1:

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

#### Switch case 示例 2:

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

#### C switch 语句穿透

C `switch` 语句穿透意味着如果不使用 `break` 语句，匹配 之后的所有 `case` 都将执行。让我们尝试下面的示例。

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

#### 嵌套 switch case

我们可以在 `switch` 内部使用任意数量的 `switch` 语句。考虑以下示例：

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

## 循环语句

### 简介

计算机是执行重复任务的最合适机器，可以不知疲倦地执行成千上万次。每种编程语言都通过某些形式的语句来完成此类重复任务。重复执行一组语句的过程被称为循环。语句根据条件执行多次。但如果给定的逻辑使得重复可以任意次数进行，而没有固定条件来停止这些语句，那么这种类型的循环被称为无限循环。

循环语句允许我们多次执行一个语句或一组语句。在 C 编程语言中，有三种循环：`while`、`do-while` 和 `for`。

#### 为什么要使用循环？

当你需要多次执行一段代码块时，你需要在 C 语言中使用循环概念。

#### 循环语句的优点

- 减少代码长度。
- 占用较少的内存空间。
- 减轻开发者的负担。
- 缩短了执行程序的耗时过程。

![](img/967bcdbdba6f2e1f56642982e8b39e66_89_0.png)

#### 循环的类型

根据控制语句在程序中的位置，循环分为两类：

- 1. 入口控制循环
- 2. 出口控制循环

在入口控制循环中，在执行循环体之前会检查条件。它也被称为预检查循环。

在出口控制循环中，在执行循环体之后会检查条件。它也被称为后检查循环。

控制条件必须定义良好且明确。否则，循环将执行无限次。不停止执行语句次数的循环被称为无限循环。无限循环也称为“无尽循环（Endless loop）”。

#### 以下是无限循环的一些特征：

- 1. 没有指定终止条件。
- 2. 指定的条件永远不会满足。

指定的条件决定了是否执行循环体。“C”编程语言为我们提供了三种类型的循环语句（结构）：

- 1. `while` 循环
- 2. `do-while` 循环
- 3. `for` 循环

#### while 循环

循环是一种入口控制循环。在 `while` 循环中，在处理循环体之前会评估条件。如果条件为真，那么且只有那时才会执行循环体。在执行循环体之后，控制回到开头，检查条件是否为真；如果是，则执行相同的过程，直到条件变为假。一旦条件变为假，控制就会离开循环。

退出循环后，控制将跳转到紧随循环之后的语句。循环体可以包含多个语句。如果它只包含一个语句，则大括号不是强制的。尽管即使循环体中只有一个语句，使用大括号也是一种良好的习惯。

在 `while` 循环中，如果条件不为真，则循环体将不会执行，即使一次也不。这与稍后介绍的 `while` 循环不同。

#### while 循环是如何工作的？

- `while` 循环评估括号 `()` 内部的测试表达式。
- 如果测试表达式为真，则执行 `while` 循环体内的语句。然后，再次评估测试表达式。
- 该过程一直持续直到测试表达式被评估为假。
- 如果测试表达式为假，循环终止（结束）。

#### while 循环的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_91_0.png)

`while` 循环通过三个步骤完成：

- 变量初始化（例如 `int x = 0;`）
- 条件（例如 `while(x <= 10)`）
- 变量增或减（`x++` 或 `x--` 或 `x = x + 2`）

`while` 循环的语法如下：

```
变量初始化;
while(条件)
{
    语句;
    变量增或减;
}
```

`while` 循环的示例程序：

```c
#include<stdio.h>
#include<conio.h>
int main()
{
    int num=1; //初始化变量
    while(num<=10) //while循环条件
    {
        printf("%d\n",num);
        num++; //增加操作
    }
    return 0;
}
```

#### 输出：

上面的程序说明了 `while` 循环的使用。在上面的程序中，我们使用 `while` 循环打印了从 1 到 10 的系列数字。

```c
#include<stdio.h>
#include<conio.h>
int main() {
    int num=1; //初始化变量
    while(num<=10) //while循环条件
    {
        printf("%d\n",num);
        num++; //增加操作
    }
    return 0;
}
```

- 1. 我们初始化了一个名为 `num` 的变量，值为 1。我们将打印 1 到 10。因此，变量初始化值为 1。如果你想从 0 开始打印，请在初始化时赋值 0。
- 2. 在 `while` 循环中，我们提供了一个条件 `(num<=10)`，这意味着循环将执行体直到 `num` 的值变为 10。之后，循环将终止，控制将循环外部。
- 3. 在循环体中，我们有一个打印函数来打印数字，以及一个增加操作来在每次循环执行时增加值。`num` 的初始值为 1，执行后它将变为 2，在下一次执行期间，它将变为 3。这个过程将一直持续直到值变为 10，然后在控制台上打印该系列数字并终止循环。

`\n` 用于格式化，意味着值将在新行打印。

#### while 循环中的 break 语句

`break` 语句主要用于 `switch` 语句。它对于立即停止循环也非常有用。

我们考虑以下程序，它引入了 `break` 来退出 `while` 循环

```c
#include <stdio.h>
int main()
{
    int num = 5;
    while (num > 0)
    {
        if (num == 3)
            break;
        printf("%d\n", num);
        num--;
    }
}
```

**输出：5 4**

#### while 循环中的 continue 语句

当你想要跳到下一次迭代但留在循环中时，你应该使用 `continue` 语句。

**示例：**

```c
#include <stdio.h>
int main() {
    int nb = 7;
    while (nb > 0)
    {
        nb--;
        if (nb == 5)
            continue;
        printf("%d\n", nb);
    }
}
```

输出：6 4 3 2 1 0（跳过了 5）

#### do-while 循环

正如我们在 `while` 循环看到的，只有当条件为真时才执行体。在某些情况下，即使条件为假，我们也必须至少执行一次循环体。这种操作可以通过使用 `do-while` 循环来实现。

`do-while` 循环与 `while` 循环相似，不同之处是在体之后总是检查条件。

#### do-while 的语法：

```
do
{
    循环体内的语句
}
while (条件);
```

#### do-while 循环的流程图

![](img/967bcdbdba6f2e1f56642982e8b39e66_94_0.png)

#### do-while 循环的示例程序：

```c
#include<stdio.h>
#include<conio.h>
int main()
{
    int num=1;
    do
    {
        printf("%d\n",num*2);
        num++;
    } while(num<=10);
    return 0;
}
```

输出：2 4 6 8 10 12 14 16 18 20

#### 使用控制语句与循环

```c
i++;
{
    printf("do you want to continue with the table of %d \n enter any non-zero value to continue.",n+1);
    scanf("%d",&choice);
}
if(choice == 0)
{
    break;
}
n++;
}while(1);
```

输出：

2 X 1 = 2    2 X 2 = 4    2 X 3 = 6    2 X 4 = 8    2 X 5 = 10

2 X 6 = 12   2 X 7 = 14   2 X 8 = 16

2 X 9 = 18   2 X 10 = 20

你想继续查看 3 的乘法表吗，请输入任意非 0 

的值以继续。11

3 X 1 = 3    3 X 2 = 6    3 X 3 = 9    3 X 4 = 12

3 X 5 = 15   3 X 6 = 18   3 X 7 = 21

3 X 8 = 24   3 X 9 = 27   3 X 10 = 30

你想继续查看 4 的乘法表吗，请输入任意非 0 

的值以继续。0

#### while 循环与 do 循环的区别

| WHILE | DO-WHILE |

| --- | --- |

| 先检查条件，后执行语句(s)。 | 先执行语句(s)，后检查条件。 |

| 可能会执行 0 次，如果条件为假。 | 至少执行一次语句(s)。 |

| while 末尾没有分号。 | do-while 末尾有分号。 |

| 如果是单条语句，不需要括号。 | 总是需要括号。 |

#### for 循环

| 变量在循环执行前初始化。 | 变量可以在循环外或初始化。 |

| while 循环是进入控制的。 | do-while 循环是退出控制的。 |

| while(condition){ 语句(s); } | do { 语句(s); }while(condition); |

| for 循环是 'C' 语言中更高效的结构。 | |

for 循环流程图

![](img/967bdba6f5e64298.png)

`for` 循环的通用语法结构如下：

for ( 初始值; 条件; 递增或递减 ) {

  语句;

}

#### for 循环是如何工作的？

- 初始化语句只执行一次。
- 然后评估测试表达式。如果测试表达式为假，循环终止。
- 然而，如果测试表达式为真，执行循环体内的语句(s)，并更新表达式。
- 再次评估测试表达式。

这个过程一直持续直到测试表达式为假。此时，循环终止。

以下程序演示了简单 `for` 循环的使用：

```c
#include<stdio.h>
int main()
{
    int number;
    for(number=1;number<=10;number++){for 循环打印 1-10
    {
        printf("%d\n",number);
    }
    return 0;
}
```

输出：

1 2 3 4 5 6 7 8 9 10

上面的程序使用 `for` 循环打印 1-10 的序列。

```c
#include<stdio.h>
int main()
{
    int number;
    for(number=1;number<=10;number++)
    {
        printf("%d\n",number)
    }
    return 0;
}
```

1. 我们声明了一个 `int` 类型的变量。
2. 在 `for` 循环的初始化部分，我们给 `number` 赋值为 1。
3. 在条件部分，我们指定了条件，然后是递增部分。
