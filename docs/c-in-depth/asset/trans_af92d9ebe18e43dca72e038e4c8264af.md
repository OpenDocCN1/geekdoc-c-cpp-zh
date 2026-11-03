

该表达式的值会逐一与每个 `case` 常量比较。如果表达式的值与某个 `case` 常量匹配，则执行该 `case` 下的所有语句；如果没有 `case` 常量与表达式的值匹配，则执行 `default` 下的语句块。`default` 是可选的，如果不存在且没有任何 `case` 匹配，则不执行任何操作。这些 `case` 和 `default` 可以按任意顺序出现。

```c
/*P5.31 Program to understand the switch control statement*/
#include<stdio.h>
main()
{
    int choice;
    printf("Enter your choice : ");
    scanf("%d",&choice);
    switch(choice)
    {
        case 1:
            printf("First\n");
        case 2:
            printf("Second\n");
        case 3:
            printf("Third\n");
        default:
            printf("Wrong choice\n");
    }
}
```

输出：
Enter your choice : 2
Second
Third
Wrong choice

这里 `choice` 的值与第二个 `case` 匹配，因此 `case 2` 之后的所有语句会按顺序执行。除了 `case 2` 的语句之外，`case 3` 和 `default` 的语句也会被执行。这就是所谓的 `case` 穿透（falling through）。

如果我们不想让控制流从匹配的 `case` 继续向下穿透执行之后所有 `case` 的语句，可以使用 `break` 语句。如果 `switch` 中遇到 `break` 语句，则 `break` 之后的所有语句都不会执行，控制流会跳出整个 `switch`。下面用 `break` 重写上面的程序。

```c
/*P5.32 Program to understand the switch with break statement*/
#include<stdio.h>
main()
{
    int choice;
    printf("Enter your choice : ");
    scanf("%d",&choice);
    switch(choice)
    {
        case 1:
printf("First\n");
break;
case 2:
printf("Second\n");
break;
case 3:
printf("Third\n");
break;
default:
printf("Wrong choice\n");
}
/*End of main()*/
```

输出：
Enter your choice : 2
Second

并不是说，只要 `switch` 中使用了 `break`，每个 `case` 语句后面都必须有 `break`。某些 `case` 可以使用 `break`，另一些可以不使用。因此，`switch` 中的 `break` 是可选的，是否使用取决于程序的需求和逻辑。`continue` 语句不能用于 `switch` 中。

![](img/a76c706396af8b310f291a5313a27079_101_0.png)

最后一个 `case`（或位于最后的 `default`）后面在逻辑上不需要 `break`，但这样做是一种良好的编程习惯，因为将来我们可能需要在末尾添加新的 `case`。

```c
/*P5.33 Program to perform arithmetic calculations on integers*/
#include<stdio.h>
main()
{
char op;
int a,b;
printf("Enter number operator and another number : ");
scanf("%d %c %d",&a,&op,&b);
switch(op)
{
case '+':
printf("Result = %d\n",a+b);
break;
case '-':
printf("Result = %d\n",a-b);
break;
case '*':
printf("Result = %d\n",a*b);
break;
case '/':
printf("Result = %d\n",a/b);
break;
case '%':
printf("Result = %d\n",a%b);
break;
default:
printf("Enter valid operator\n");
}/*End of switch*/
}/*End of main()*/
```

输出：
Enter number operator and another number : 2+5
Result = 7

在这个程序中，合法的乘法运算符只有 `'*'`。如果我们希望 `'x'` 和 `'X'` 也作为合法的乘法运算符，可以像下面这样修改上面的 `switch` 语句。

```c
switch(op)
{
...............
...............
case '-':
result = a-b;
break;
case 'x':
case 'X':
case '*':
result = a*b;
break;
...............
...............
}
```

## 控制语句

```c
break;
case '/':
....................
....................
}/*End of switch*/
```

这里我们添加了两个没有语句的 `case`。由于 `case 'x'` 和 `case 'X'` 后面没有 `break`，在这两种情况下都会执行 `case '*'` 的语句。

```c
#include<stdio.h>
main( )
{
char ch;
printf("Enter an alphabet : ");
scanf("%c", &ch);
switch(ch)
{
case 'a':
case 'e':
case 'i':
case 'o':
case 'u':
printf("Alphabet is a vowel\n");
break;
default:
printf("Alphabet is a consonant\n");
}
}
```

在这个程序中，如果有人输入大写元音，它会被当作辅音处理。解决这个问题的一种方法是再添加 5 个大写元音的 `case`。但我们也可以不添加任何 `case`，用另一种方式解决。我们之前学过，`switch` 表达式可以是返回 `int` 或 `char` 的函数调用。所以把 `switch` 表达式改为 `tolower(ch)`，问题就解决了。`tolower()` 是一个把大写字母转换为小写字母的库函数，使用它时需要包含头文件 `ctype.h`。

`switch` 语句在菜单驱动程序中非常重要。下面我们编写一个菜单驱动的（模拟）程序，它的结构类似数据库应用。虽然这个程序本身不执行任何实际功能，但它展示了菜单驱动程序的结构。

```c
#include<stdio.h>
main( )
{
int choice;
while(1)
{
printf("1.Create database\n");
printf("2.Insert new record\n");
printf("3.Modify a record\n");
printf("4.Delete a record\n");
printf("5.Display all records\n");
printf("6.Exit\n");
printf("Enter your choice : ");
scanf("%d",&choice);
switch(choice)
{
case 1:
    printf("Database created.....\n\n");
    break;
case 2:
    printf("Record inserted.....\n\n");
    break;
case 3:
    printf("Record modified.....\n\n");
    break;
case 4:
    printf("Record deleted.....\n\n");
    break;
case 5:
    printf("Records displayed.....\n\n");
    break;
case 6:
    exit(1);
default:
    printf("Wrong choice\n");
}/*End of switch*/
/*End of while*/
/*End of main*/
```

这里我们把 `switch` 放在一个无限循环中。函数 `exit()` 用于终止程序。每次循环执行时，都会显示所有选项并提示输入选择。程序会根据选择执行相应操作。如果输入选项 6，程序就会退出。在实际程序中，我们会把完整代码写在各个 `case` 中，而不仅仅是简单的 `printf` 语句。

## 5.8 一些附加问题

### 问题 1

编写一个程序，判断输入的日期是否有效。假设 1850 年到 2050 年之间的日期是有效的。

```c
/*P5.36 Program to check whether a date is valid or not.*/
#include<stdio.h>
main()
{
    int d,m,y;
    int flag=1,isLeap=0;
    printf("Enter date (dd/mm/yyyy) : ");
    scanf("%d/%d/%d",&d,&m,&y);
    if(y%4==0 && y%100!=0 || y%400==0)
        isLeap=1;
    if(y<1850 || y>=2050)
flag=0;
else if(m<1 || m>12)
    flag=0;
else if(d<1)
    flag=0;
else if(m==2)      /*check for number of days in February*/
{
    if(d>28)
        flag=0;
    if(d==29 && isLeap)
        flag=1;
}
else if(m==4 || m==6 || m==9 || m==11)/*check days in april, june, sept, nov*/
{
    if(d>30)
        flag=0;
}
else if(d>31)
    flag=0;

if(flag==0)
    printf("Not a valid date\n");
else
    printf("Valid Date \n");
}/*End of main() */
```

### 问题 2

编写一个程序，计算两个日期在年、月、日上的差值。假设输入的日期都在有效范围内，并且第一个日期早于第二个日期。

```c
/*P5.37 Program to get difference of two dates in years, months, days*/
#include<stdio.h>
main( )
{
    int d1,d2,d,m1,m2,y1,y2;
    printf("Enter first date (dd/mm/yyyy) : ");
    scanf("%d/%d/%d",&d1,&m1,&y1);
    printf("Enter second date (dd/mm/yyyy) : ");
    scanf("%d/%d/%d",&d2,&m2,&y2);
    if(d2<d1)
    {
        if(m2==3)
        {
            if(y2%4==0 && y2%100!=0 || y2%400==0)  /*check for leap*/
                d2=d2+29;
            else
                d2=d2+28;
        }
        else if(m2==5 || m2==7|| m2==10|| m2==12)
            d2=d2+30;
        else
            d2=d2+31;
        m2=m2-1;
    }
    if (m2<m1)
    {
        y2=y2-1;
        m2=m2+12;
    }
    y=y2-y1;
    m=m2-m1;
    d=d2-d1;
    printf("Difference of the two dates is : ");
    printf("%d years %d months %d days\n",y,m,d);
}/*End of main()*/
```

这里我们是用第二个日期减去第一个日期，因此可以通过如下方式得到年、月、日的差值：

`y = y2 - y1;`      `m = m2 - m1;`      `d = d2 - d1;`

我们假设第二个日期晚于第一个日期，因此 `y2` 始终大于或等于 `y1`，`y` 也始终为正。

但 `m2` 可能小于 `m1`，此时 `m` 会为负；如果 `d2` 小于 `d1`，那么 `d` 也会为负。所以在计算 `y`、`m` 和 `d` 之前，应确保 `m2` 大于或等于 `m1`，且 `d2` 大于或等于 `d1`。

如果 `d2` 小于 `d1`，就从 `m2` 借一个月，并把该月的天数加到 `d2` 上。由于各月的天数不同，加到 `d2` 上的天数取决于借来的月份。我们总是借 `m2` 之前的那一个月。例如，如果 `m2 = 5`（五月），就从 `m2` 借四月，因此给 `d2` 加上 30。

`d2 = d2+30;`          `m2 = m2-1;`

如果 `m2 = 3`（三月），就从 `m2` 借二月，因此给 `d2` 加上 28 或 29（若是闰年）。

`d2 = d2+28;`      `m2 = m2-1;`

在程序中，这是通过嵌套的 `if else` 语句实现的。

如果 `m2` 小于 `m1`，就从 `y2` 借 1 年（12 个月）加到 `m2` 上。这样 `m2` 就会大于 `m1`。

`m2 = m2+12;`      `y2 = y2-1;`

### 问题 3

编写一个程序，使用俄罗斯农夫乘法计算两个数的乘积。俄罗斯农夫乘法通过乘以 2、除以 2 和加法来计算任意两个正数的乘积。这里将第一个数反复除以 2（整数除法），并将第二个数反复乘以 2，直到第一个数变为 1。假设我们要计算 19 乘以 25，可以像下面这样把除以 2 和乘以 2 的结果分别写在两列中：

