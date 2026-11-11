

![](img/57c0d966bb33c67a5a188e6bf39e4e02_149_0.png)

**图 4.19：** 执行打印“星期几”的代码

```c
#include<stdio.h>
void main()
{
    int day;
    printf("Enter the day number\n");
    scanf("%d",&day);
    /*switch over the value of variable "day"*/
        switch(day)
        {
        case 1: printf("Sunday\n");
            break;
        case 2: printf("Monday\n");
            break;
        case 3: printf("Tuesday\n");
            break;
        case 4: printf("Wednesday\n");
            break;
        case 5: printf("Thursday\n");
            break;
        case 6: printf("Friday\n");
            break;
        case 7: printf("Saturday\n");
            break;
        default: printf("Invalid Day Number\n");
        }
}
```

### 输出

```text
Enter the day number
2
Monday
```

> **为什么我们要在 switch 块内每个 case 的末尾编写 break 语句？**
>
> 当某个 case 被满足时，switch 并不会被视为已关闭。这意味着，即使某个 case 中的所有语句都已执行完毕，执行控制也不会离开 switch 块。如果缺少 break 语句，执行流会贯穿到满足表达式的 case 之后写入的所有 case 语句。因此，我们在每个 case 块内显式编写 break 语句，以避免执行流发生贯穿。例如，在上面的程序中，如果我们不编写 break 语句，并将变量 day 的值设为 4，那么执行流会从 case 4 开始贯穿每个 case 块，并产生以下输出：
>
> ```text
> Wednesday
> Thursday
> Friday
> Saturday
> Invalid Day
> ```
>
> 因此，为了生成期望的输出，需要在每个 case 块内编写 break 语句。

## 4.6 三元运算符/条件运算符

条件运算符是 if-else 语句的替代方案。该运算符也称为三元运算符，它作用于三个操作数，如下面的语法所示：

```c
condition ? expression1 : expression2;
```

该运算符首先计算条件，如果条件为“真”，则三元运算的结果与“表达式 1”返回的结果相同。如果条件为“假”，则三元运算的结果与“表达式 2”返回的结果相同。

作为示例，为了理解三元运算符的工作方式，让我们考虑下面给出的 if-else 语句，它将两个数 x 和 y 中的最小值存入变量 res。

```c
if (x < y)
{
    res = x;
}
else
{
    res = y;
}
```

这意味着，如果条件 x < y 为“真”，则变量 res 被设置为变量 x 的值；如果条件 x < y 为“假”，则变量 res 的值被设置为变量 y，如图 4.20 所示。作为给定 if-else 语句的替代方案，我们也可以使用三元运算符来初始化变量 res 的值，如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_151_0.png)

**图 4.20：** 求两个数 x 和 y 的最小值

```c
res = (x < y) ? x : y;
```

下面给出使用三元运算符求两个数 x 和 y 最小值的完整源代码。

```c
#include<stdio.h>
void main()
{
int x,y,res;
printf("Enter the two numbers\n");
scanf("%d %d",&x,&y);
res = (x < y) ? x : y;
printf("Minimum is %d\n",res);
}
```

### 输出

```text
Enter the two numbers
10 30
Minimum is 10
```

### 注意

#### 条件运算符的嵌套

可以嵌套条件运算符。例如，考虑一种情况：我们需要使用条件运算符求三个数 a、b 和 c 中的最大值。在这种情况下，我们可以如下嵌套条件运算符：

```c
res = a >= b && a >= c ? a : b >= a && b >= c ? b : c;
```

该语句等价于如下所示的 else if 阶梯：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_152_0.png)

else-if 阶梯中的条件与第 4.4 节示例中的条件非常相似。因此，变量 res 将存储三个变量中的最大值。下面给出完整程序，它使用条件运算符的嵌套而不是 else-if 阶梯来求三个数中的最大值。

```c
#include<stdio.h>
void main()
{
    int res,a,b,c;
    printf("Enter 3 nos\n");
    scanf("%d %d %d",&a,&b,&c);
    res = a >= b && a >= c ? a : b >= a && b >= c ? b : c;
    printf("Greatest number is %d\n",res);
}
```

### 输出

```text
Enter 3 nos
10 55 22
Greatest number is 55
```

你也可以通过改变条件运算符的嵌套方式，以不同方式编写相同条件。例如，以下语句也会将 a、b 和 c 中的最大值存入变量 res。

```c
res = a >= b ? (a >= c ? a : c) : (b >= c ? b : c);
```

虽然该语句完成同样的工作，唯一区别在于，此语句在内部转换为**嵌套 if-else 块**，而不是 else if 阶梯。首先测试主条件 a>=b，如果该条件为真，则执行以下部分：

```c
a >= c ? a : c
```

然而，如果主条件 a>=b 为假，则执行该语句的以下部分：

```c
b >= c ? b : c
```

该语句的工作方式如下图所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_153_0.png)

下面给出完整源代码，它使用这种方法通过嵌套条件运算符来求三个数中的最大值。

```c
#include<stdio.h>
void main()
{
    int res,a,b,c;
    printf("Enter 3 nos\n");
    scanf("%d %d %d",&a,&b,&c);
    res = a >= b ? (a >= c ? a : c) : (b >= c ? b : c);
    printf("Greatest number is %d\n",res);
}
```

### 输出

```text
Enter 3 nos
10 55 22
Greatest number is 55
```

## 4.7 goto 语句

goto 语句用于在程序中实现无条件跳转。当遇到 goto 语句时，程序正常的顺序执行会中断，执行控制权转移到由 goto 语句中指定的标签所标识的语句。

下面给出 goto 语句的语法：

```c
goto <label>;
```

标签是程序中唯一的名称，它被赋予某条语句，以便使用 goto 语句将执行控制权转移到该语句。必须使用冒号 (:) 运算符将该语句的唯一名称作为该语句的前缀写在程序中，如下所示：

```c
label: Statement;
```

下面给出修改后的程序，它通过接受用户输入的日期编号来打印星期几。如所见，代码使用 else-if 阶梯根据整型变量 day 的值打印星期几。在开头，我们编写了以下 if 结构，用于检查用户输入的日期编号是否无效：

```c
if(day <= 0 || day > 7)
{
    printf("Invalid Day Number\n");
    goto END;
}
```

这意味着，如果变量 day 的值不在 1 到 7（含两端）之间，那么我们在计算机屏幕上打印一条消息“Invalid Day Number”。此外，if 块内出现的以下 goto 语句会将控制权转移到程序中标记为 END 的语句。

```c
goto END;
```

因此，goto 语句将控制权转移到程序的最后一条语句，即：

```c
END: printf("End of the program\n");
```

从而跳过整个 else if 阶梯，并避免任何不必要的操作，因为用户输入了无效的日期编号。

```c
#include<stdio.h>
void main()
{
int day;
printf("Enter the day number\n");
scanf("%d",&day);
    if(day<=0 || day>7)
    {
    printf("Invalid Day Number\n");
    goto END;
    }
    if(day==1)
    {
    printf("Sunday\n");
    }
    else if(day==2)
    {
    printf("Monday\n");
    }
    else if(day==3)
    {
    printf("Tuesday\n");
    }
    else if(day==4)
    {
    printf("Wednesday\n");
    }
    else if(day==5)
    {
    printf("Thursday\n");
    }
    else if(day==6)
    {
    printf("Friday\n");
    }
    else
    {
    printf("Saturday\n");
    }
    END: printf("End of the program\n");
}
```

### 输出

```text
Enter the day number
2
Monday
End of the program
```

### 输出（情况：无效日期编号）

```text
Enter the day number
```

