

- 并非每个 `case` 都必须包含 **break**。如果没有 **break**，控制流将 *穿透*（fall through）到后续的 `case`，直到遇到 break 为止。
- **switch** 语句可以有一个可选的 **default** 分支，它必须出现在 switch 的末尾。当所有 `case` 都不匹配时，可以使用 default 分支来执行相应任务。default 分支中不需要 **break**。

## 流程图

![](img/6e49c39a6ef9e32d938b03dc613e44f6_62_0.png)

## 示例

```c
#include <stdio.h>

int main ()
{
    /* 局部变量定义 */
    char grade = 'B';

    switch(grade)
    {
    case 'A' :
        printf("Excellent!\n" );
        break;
    case 'B' :
    case 'C' :
        printf("Well done\n" );
        break;
    case 'D' :
        printf("You passed\n" );
        break;
    case 'F' :
        printf("Better try again\n" );
        break;
    default :
        printf("Invalid grade\n" );
    }
    printf("Your grade is %c\n", grade );

    return 0;
}
```

当上面的代码被编译和执行时，它会产生以下结果：

```text
Well done

Your grade is B
```

## 嵌套 switch 语句

将一个 switch 作为外部 switch 语句序列的一部分是可能的。即使内部和外部 switch 的 case 常量包含相同的值，也不会产生冲突。

## 语法

**嵌套 switch** 语句的语法如下：

```c
switch(ch1) {
    case 'A':
        printf("This A is part of outer switch");
        switch(ch2) {
            case 'A':
                printf("This A is part of inner switch");
                break;
            case 'B': /* 分支代码 */
        }
        break;
    case 'B': /* 分支代码 */
}
```

## 示例

```c
#include <stdio.h>

int main ()
{
    /* 局部变量定义 */
    int a = 100;
    int b = 200;

    switch(a) {
        case 100:
            printf("This is part of outer switch\n", a );
            switch(b) {
                case 200:
                    printf("This is part of inner switch\n", a );
            }
    }
    printf("Exact value of a is : %d\n", a );
    printf("Exact value of b is : %d\n", b );

    return 0;
}
```

当上面的代码被编译和执行时，它会产生以下结果：

![](img/6e49c39a6ef9e32d938b03dc613e44f6_64_0.png)

This is part of outer switch
This is part of inner switch
Exact value of a is : 100
Exact value of b is : 200

## ? : 运算符

我们在前一章中已经介绍了**条件运算符 ? :**，它可以用来替代 **if...else** 语句。它的一般形式如下：

```
Exp1 ? Exp2 : Exp3;
```

其中 Exp1、Exp2 和 Exp3 是表达式。注意冒号的使用和位置。

? 表达式的值是这样确定的：

1. 对 Exp1 进行求值。如果它为真，则对 Exp2 求值，并使其成为整个 ? 表达式的值。
2. 如果 Exp1 为假，则对 Exp3 求值，并将其值作为表达式的值。

## 11. 循环

你可能会遇到需要多次执行一段代码的情况。通常情况下，语句是按顺序执行的：函数中的第一条语句先执行，接着是第二条，以此类推。

编程语言提供了各种控制结构，允许实现更复杂的执行路径。

循环语句允许我们多次执行一条语句或一组语句。下面是大多数编程语言中循环语句的一般形式：

![](img/6e49c39a6ef9e32d938b03dc613e44f6_66_0.png)

C 编程语言提供了以下类型的循环来处理循环需求。

| 循环类型 | 描述 |
|---|---|
| while 循环 | 当给定条件为真时，重复执行一条语句或一组语句。它在执行循环体之前测试条件。 |
| for 循环 | 多次执行一系列语句，并简化管理循环变量的代码。 |

这里需要重点注意的是，while 循环可能根本不会执行。当条件被测试且结果为假时，循环体将被跳过，while 循环之后的第一条语句将被执行。

```c
#include <stdio.h>

int main ()
{
    /* 局部变量定义 */
    int a = 10;

    /* while 循环执行 */
    while( a < 20 )
    {
        printf("value of a: %d\n", a);
        a++;
    }
}
```

4. 现在再次对条件进行求值。如果条件为真，则循环执行并重复此过程（循环体，然后增量步骤，然后再条件）。当条件变为假后，`for` 循环终止。

## 流程图

![](img/6e49c39a6ef9e32d938b03dc613e44f6_70_0.png)

## 示例

```c
#include <stdio.h>

int main ()
{
    /* for 循环执行 */
    for( int a = 10; a < 20; a = a + 1 )
    {
        printf("value of a: %d\n", a);
    }

    return 0;
}
```

当上面的代码被编译和执行时，它会产生以下结果：

```text
value of a: 10

value of a: 11

value of a: 12

value of a: 13

value of a: 14

value of a: 15

value of a: 16

value of a: 17

value of a: 18

value of a: 19
```

## do...while 循环

与 **for** 和 **while** 循环在循环顶部测试循环条件不同，C 编程中的 **do...while** 循环在循环底部检查其条件。

**do...while** 循环与 while 循环类似，不同之处在于它保证至少执行一次。

## 语法

C 编程语言中 **do...while** 循环的语法是：

```c
do
{
    statement(s);

}while( condition );
```

注意，条件表达式出现在循环的末尾，因此循环中的语句在条件被测试之前先执行一次。

如果条件为真，控制流跳回到 do，并再次执行循环中的语句。此过程重复，直到给定条件变为假。

![](img/6e49c39a6ef9e32d938b03dc613e44f6_72_0.png)

```c
#include <stdio.h>

int main ()
{
    /* 局部变量定义 */
    int a = 10;

    /* do 循环执行 */
    do
    {
    printf("value of a: %d\n", a);
    a = a + 1;
    }while( a < 20 );

    return 0;
}
```

当上面的代码被编译和执行时，它会产生以下结果：

```text
value of a: 10

value of a: 11

value of a: 12

value of a: 13

value of a: 14

value of a: 15

value of a: 16

value of a: 17

value of a: 18

value of a: 19
```

## 嵌套循环

C 编程允许在一个循环内部使用另一个循环。以下部分展示了一些示例来说明这个概念。

## 语法

C 中**嵌套 for 循环**语句的语法如下：

```c
for ( init; condition; increment )
{
    for ( init; condition; increment )
    {
        statement(s);
    }
    statement(s);
}
```

C 编程语言中**嵌套 while 循环**语句的语法如下：

```c
while(condition)
{
    while(condition)
    {
        statement(s);
    }
    statement(s);
}
```

C 编程语言中**嵌套 do...while 循环**语句的语法如下：

```c
do
{
    statement(s);
    do
    {
        statement(s);
    }while( condition );
}while( condition );
```

关于循环嵌套的最后一点说明是，你可以在任何其他类型的循环中放置任何类型的循环。例如，一个 `for` 循环可以放在 `while` 循环内，反之亦然。

## 示例

下面的程序使用嵌套的 for 循环来找出 2 到 100 之间的素数：

```c
#include <stdio.h>

int main ()
{
    /* 局部变量定义 */
    int i, j;

    for(i=2; i<100; i++) {
        for (j=2; j <= (i/j); j++)
            if(!(i%j)) break;          // 如果找到因子，则不是素数
        if(j > (i/j)) printf("%d is prime\n", i);
    }
    return 0;
}
```

当上面的代码被编译和执行时，它会产生以下结果：

```text
2 is prime

3 is prime

5 is prime

7 is prime

11 is prime

13 is prime

17 is prime

19 is prime

23 is prime

29 is prime

31 is prime

37 is prime

41 is prime

43 is prime

47 is prime

53 is prime

59 is prime

61 is prime

67 is prime

71 is prime

73 is prime

79 is prime

83 is prime

89 is prime

97 is prime
```

## 循环控制语句

循环控制语句会改变执行的正常顺序。当执行离开某个作用域时，该作用域中创建的所有自动对象都会被销毁。

C 支持以下控制语句。

