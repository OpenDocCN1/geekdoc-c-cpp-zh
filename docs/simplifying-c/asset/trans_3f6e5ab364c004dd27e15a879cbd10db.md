
# 当循环

当循环（while loop）是一种先测型循环，用于无法预先确定语句需要执行次数的场景。当循环的语法如下：

```
while (测试条件)
   动作块;
```

上述语法中提到的测试条件是一个关系表达式或一个正常量。当且仅当测试条件求值为真时，当循环的动作块才会被执行。图 6 展示了当循环的逻辑流程：

![](img/5d422ba7108ffdf64376be51eaf0c459_151_0.png)

▲ **图 6：当循环的逻辑流程**

由于测试条件是在入口处进行检查的，因此当循环被视为入口控制循环。如果测试条件在第一次就被求值为假，那么循环的动作块将完全不会被执行。程序 6 展示了如何使用当循环来计算两个正数的最大公约数。

## 程序 6

```c
/* 使用当循环计算两个正数最大公约数的程序 */

#include <stdio.h>

/* 主函数开始 */
main()
{
   /* 声明变量 */
   int i_num1, i_num2, i_remainder, i_temp;
   /* 输入数据 */
   printf("Enter the first number: ");
   scanf("%d", &i_num1);

   printf("Enter the second number: ");
   scanf("%d", &i_num2);
   /* 检查两个数是否都为正数且大于 0 */
   if((i_num1 > 0) && (i_num2 > 0))
   {
      /* 必要时交换数值 */
      if(i_num2 > i_num1)
      {
         i_temp = i_num2;
         i_num2 = i_num1;
         i_num1 = i_temp;
      }

      /* 查找最大公约数 */
      i_remainder = i_num1 % i_num2;
      printf("The greatest common divisor of %d and %d is ", i_num1, i_num2);
      while(i_remainder)
      {
         i_num1 = i_num2;
         i_num2 = i_remainder;
         i_remainder = i_num1 % i_num2;
      }

      /* 打印最大公约数 */
      printf("%d\n", i_num2);
   }
   else
   {
      printf("One or Both of the entered number is zero or negative\n");
   }
   return;
} /* 主函数结束 */
```

**输出 1：**

Enter the first number: 25
Enter the second number: 20
The greatest common divisor of 25 and 20 is 5

**输出 2：**

Enter the first number: 44
Enter the second number: 0
One or Both of the entered number is zero or negative

从程序 6 中可以观察到，当循环是一个事件控制循环。这里终止循环的事件是 `i_remainder == 0`。在程序 6 中，如果表达式 `i_remainder = i_num1 % i_num2;` 的初始求值结果为 0，则当循环根本不会执行。输出 1 给出了正确的最大公约数，而输出 2 指示了一个错误状态。

让我们来看一个当循环的另一个例子。程序 7 展示了如何使用当循环计算大于 0 的正数的阶乘。

## 程序 7

```c
/* 使用当循环计算大于 0 的正数阶乘的程序 */
#include <stdio.h>

/* 主函数开始 */
main()
{
    /* 声明变量 */
    long l_factorial = 1;
    int i_number, i_ctr = 1;

    /* 输入数据 */
    printf ("Enter a number: ");
    scanf ("%d", &i_number);

    /* 检查数是否大于 0 */
    if(i_number > 0)
    {
        /* 计算阶乘 */
        while(1)
        {
            l_factorial = l_factorial * i_ctr;
            /* 检查计数器是否等于该数 */
            if(i_ctr == i_number)
                break;
            i_ctr++;
        }
        printf("Factorial of %d is %ld\n", i_number, l_factorial);
    }
    else
        printf("The number entered is zero or negative\n");

    return;
} /* 主函数结束 */
```

**输出 1：**

Enter a number: 4
Factorial of 4 is 24

**输出 2：**

Enter a number: -10
The number entered is zero or negative

在程序 7 中可以看到，当循环使用常量作为测试条件。使用常数值 1 的测试条件始终求值为真，因此这里的当循环变成了一个无限循环。为了终止循环，我们使用了事件 `i_ctr == i_number`。如果该条件求值为真，循环即终止。输出 1 给出了正确的阶乘值，而输出 2 指示了一个错误状态。

> 初学者程序员必须谨慎，因为他们通常犯的一个错误是用分号终止当语句。在这种情况下，编译器可能会也可能不会报错。

C 语言提供的最后一种重复结构是 do...while 循环。下一节将讨论 do...while 结构的使用。

# Do...While 循环

do...while 语句是一种后测型循环，其动作块至少会执行一次。测试条件总是在退出循环时进行检查。因此，它也被称为出口控制循环。do...while 循环的语法如下：

```
do
  动作块;
while (测试条件);
```

图 7 展示了 do...while 循环的逻辑流程：

![](img/5d422ba7108ffdf64376be51eaf0c459_154_0.png)

▲ **图 7：Do...While 循环的逻辑流程**

do...while 语句的动作块在大多数情况下是一个复合语句。如果在动作块内只使用单条语句，可能会导致无限循环。例如，请看下面给出的代码片段：

```c
do                          or          do
  printf("Hello\n");                    printf("Hello\n");
while (1);                      while (i_ctr <= 10);
```

在上述两种情况下，由于没有停止标准，循环将无限地执行下去。程序 8 展示了如何使用 do...while 循环来判断输入的数是否为质数：

## 程序 8

```c
/* 使用 do...while 循环判断输入的正数是否为质数的程序 */

#include <stdio.h>
#include <math.h>

/* 主函数开始 */
main()
{
  /* 声明变量 */
  int i_number, i_divisor = 3;
  double d_limit;

  /* 输入数据 */
  printf("Enter a number: ");
  scanf("%d", &i_number);

  /* 检查数是否大于 0 */
  if(i_number > 0)
  {
    /* switch 结构开始 */
    switch(i_number)
    {
      /* 识别特殊情况 */
      case 1:
        printf("Number %d is special number\n", i_number);
        break;
      case 2:
      case 3:
        printf("Number %d is a prime number\n", i_number);
        break;
      /* 检查数是否为质数 */
      default:
        d_limit = sqrt(i_number);

        /* 检查数是否能被 2 整除 */
        if(i_number % 2 == 0)
        {
          printf("Number %d is not prime\n", i_number);
          break;
        }

        /* 检查数是否能被 3、5 等其他数字整除 */
        /* do...while 循环开始 */
        do
        {
          if(i_number % i_divisor == 0)
          {
            printf("Number %d is not prime\n", i_number);
            break;
          }
          else
            i_divisor += 2;
        }
        while(i_divisor <= (int)d_limit);
        /* do...while 循环结束 */

        if(i_divisor > (int)d_limit)
          printf("Number %d is prime number\n", i_number);
    }
    /* switch 结构结束 */
  }
  else
    printf("The number entered is zero or negative\n");
  return;
} /* 主函数结束 */
```

**输出 1：**

Enter a number: 1
Number 1 is special number

**输出 2：**

Enter a number: 2
Number 2 is a prime number

**输出 3：**

Enter a number: 17
Number 17 is prime number

**输出 4：**

Enter a number: 121
Number 121 is not prime number

**输出 5：**

Enter a number: -10
The number entered is zero or negative

在程序 8 中，我们结合了 if 和 if-else 决策结构以及 do...while 循环。请注意，程序中使用的 do...while 循环有两个退出点：第一个是测试条件 `i_number % i_divisor == 0`，第二个是测试条件 `i_divisor <= (int)d_limit`。在任一情况下，控制流都会先进入循环，然后立即转向循环后的下一条语句。请注意，要在 Linux/Unix 环境中执行上述程序，我们需要使用命令 `gcc prog7_8.c -lm`。这里的参数 `-lm` 指的是链接程序中引用的 math.h 文件。

for、while 和 do...while 这三种循环结构可以互换使用。并没有规定生成计数器控制循环必须使用 for 循环。同样，也不是说 while 或 do...while 循环只能用于生成事件控制循环。用户可以根据其便利性使用这些循环结构中的任意一种来设计计数器控制循环或事件控制循环。下一节将讨论嵌套循环的概念。

## 7.3 | 嵌套循环

我们在本书第 6 章中已经学习了嵌套的概念，当时讨论的是嵌套的决策结构。嵌套循环一词指的是在一个循环内使用另一个循环。嵌套循环通常在外部循环的动作块中的某一条语句本身也是一个循环时创建。因此，我们现在有了两个循环，即外部循环和内部循环。图 8 展示了嵌套 for 循环的一个示例：

