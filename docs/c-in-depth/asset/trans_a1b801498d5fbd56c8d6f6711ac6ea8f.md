


**输出：**

```
Number = 1
Number = 2
I understand the use of break
Out of for loop
```

这是一个简单的程序，虽然用处不大，但说明了 break 语句的使用。如果没有 break 语句，这个循环会执行 5 次。但在这里当 n 的值等于 3 时，遇到 break，循环被终止。

现在我们来看一个检查数字是否为素数的程序。素数是指只能被 1 和自身整除的数。数 n 为素数当且仅当 n/2、n/3、n/4...√n 的余数都为非零，或者说 n 不能被 2 到 √n 之间的任何数整除。

```c
/*P5.27 Program to find whether a number is prime or not*/
#include<stdio.h>
#include<math.h>
main()
{
    int i,num,flag=1;
    printf("Enter a number : ");
    scanf("%d",&num);

    for(i=2;i<=sqrt(num);i++)
    {
        if (num%i==0)
        {
            printf("%d is not prime\n",num);
            flag=0;
            break;
        }
    }
    if(flag==1)
        printf("%d is prime\n",num);
}
```

`sqrt()` 是一个返回数字平方根的库函数，使用此函数时我们必须包含头文件 `math.h`。for 循环的范围是从 2 到 √n，如果该数能被此范围内的任何数整除，则该数不是素数，也就没有必要检查其他数的可整除性，因此控制流通过 break 语句从循环中转移出来。控制流从循环中退出有两种情况：在循环完全执行后，当循环条件变为假时退出，或由于 break 语句而退出。如果控制流在循环完全执行后退出，则 flag 的值为 1，该数是素数。

### 5.5 continue 语句

continue 语句用于当我们想要跳过循环的某些语句后进入循环的下一轮迭代时。这个 continue 语句可以简单地写成：

```c
continue;
```

它通常与条件一起使用。当遇到 continue 语句时，当前迭代的剩余语句都会被跳过。

**输出：**

```
Number = 1
Number = 2
I understand the use of continue
Number = 4
Number = 5
Out of for loop
```

```c
/*P5.29 Program to find the sum and average of 10 positive integers*/
#include<stdio.h>
main()
{
    int i=1,n,sum=0;
    float avg;
    printf("Enter 10 positive numbers : \n");
    while(i<=10)
    {
        printf("Enter number %d : ",i);
        scanf("%d", &n);
        if(n<0)
        {
            printf("Enter only positive numbers\n");
            continue;
        }
        sum+=n;
        i++;
    }
    avg=sum/10.0;
    printf("Sum = %d Avg = %f\n",sum,avg);
}
```

在此程序中，如果输入任何负数，则会显示一条消息并且控制流转移到循环开始处。

### 5.6 goto 语句

这是一个无条件控制语句，用于将控制流转移到程序的另一部分。

goto 语句可以这样使用：

```c
goto label;
------
------
label:
statement;
------
------
```

这里 label 是任何有效的 C 标识符，其后跟一个冒号。每当遇到语句 `goto label;` 时，控制就会转移到标签之后的语句。

```c
/*P5.30 Program to print whether the number is even or odd*/
#include<stdio.h>
main()
{
    int n;
    printf("Enter the number : ");
    scanf("%d", &n);
    if(n%2==0)
        goto even;
    else
        goto odd;

even:
    printf("Number is even");
    goto end;

odd:
    printf("Number is odd");
    goto end;

end:
    printf("\n");
}
```

```
Enter the number : 14
Number is even
```

标签可以放在任何位置。如果标签在 goto 之后，则控制流向前转移，这称为前向跳转或前向 goto；如果标签在 goto 之前，则控制流向后转移，这称为后向跳转或后向 goto。在前向 goto 中，goto 和标签之间的语句不会被执行，而在后向 goto 中，goto 和标签之间的语句会重复执行。一个以上的 goto 可以与同一个标签关联，但我们不能在多个位置使用相同的标签。

使用 goto 语句只能在函数内部转移控制。 （函数概念将在后续章节介绍）

任何标签后面都应该有一个语句。如果标签位于程序末尾，后面没有要编写的语句，我们可以在标签后写空语句（单个分号），因为程序不能以标签结束。

应该避免使用 `goto`，因为很难理解控制流被转移到哪里。有时它会导致“意大利面条”代码，这种代码难以理解，调试和维护也非常困难。我们完全可以在不使用 goto 的情况下完成所有工作，并且在结构化编程中不鼓励使用 goto。

尽管不推荐使用 goto，但在一种情况下 goto 实际上可以使代码更简单、更易读。这种情况出现在我们需要从深层嵌套循环中退出时。

```c
for( ............)
{
    while(...........)
    {
        for( ............)
        {
            if( ............)
                goto stop;
        }
    }
}
stop:
```

如前所述，我们完全可以在不使用 goto 的情况下编写任何代码，因此这里也有另一种退出深层嵌套循环的方法。

```c
flag=0;
for(..............)
{
    while(...........)
    {
        for( ............)
        {
            if( ............)
            {
                flag=1;
                break; /*out of innermost loop*/
            }
        }
        if( flag == 1 )
            break; /*out of while loop*/
    }
    if( flag == 1 )
        break; /* out of outer for loop*/
}
```

我们可以看到在嵌套循环的情况下，使用 goto 的代码更易读，如果不使用它则必须执行许多测试。

### 5.7 switch 语句

这是一个多向条件控制语句。有时程序中需要从多个备选方案中做出选择。为此我们使用 switch 语句。可以这样写：

```c
switch(expression)
{
  case constant1:
    statement
    ........
  case constant2:
    statement
    ........
    ..........
    ..........
  case constantN:
    statement
    ........
  default :
    statement
    ........
}
```

这里 switch、case 和 default 是关键字。switch 关键字后面的 "expression" 可以是产生整数值的任何 C 表达式。它可以是任何整数或字符变量的值，也可以是返回整数的函数调用，或产生整数的算术、逻辑、关系、按位表达式。它也可以是任何整数或字符常量。由于字符会被转换为其 ASCII 值，所以我们也可以在此表达式中使用字符。数据类型 long int 和 short int 也允许。

case 关键字后面的常量应为整数或字符类型。它们可以是常量或常量表达式。这些常量必须彼此不同。

我们不能使用浮点或字符串常量。单个 case 中不允许多个常量；每个 case 后面只能跟一个常量。

每个 case 后面可以跟任意数量的语句。case 下也可能没有任何语句。如果 case 后面跟多个语句，则没有必要将它们用一对大括号括起来，但这样做也不是错误。case 下的语句可以是任何有效的 C 语句，如 if else、while、for 甚至另一个 switch 语句。将一个 switch 语句写在另一个内部称为 switch 嵌套。现在我们来看一些编写 switch 表达式和 case 常量的有效和无效方式。

`int a, b, c; char d, e; float f;`

**有效：**

- `switch(a)`
- `switch(a>b)`
- `switch(d+e-3)`
- `switch(a>b && b>c)`
- `switch(func(a, b))`

**无效：**

- `switch(f)`
- `switch(a+4.5)`

**有效：**

- `case 4:`
- `case 'a':`
- `case 2+4:`
- `case 'a'>'b':`

**无效：**

- `case "second":`
- `case 2.3:`
- `case a:`
- `case a>b:`
- `case a+2:`
- `case 2, 4, 5:`
- `case 2 4 : 4 : 5 :`

现在让我们看看 switch 语句是如何工作的。首先计算 switch 表达式，然后
