

其一般语法是：

```cpp
if(condition)
{
    Statements;
    Statements;
    ............;
}
else
{
    Statements;
    Statements;
    ............;
}
```

如果 if 中的条件为真，则 if 后面的块中的所有语句都会被执行，否则它们将被跳过并执行 else 部分。

```cpp
/*PROG 3.30 CHECKING THE NUMBER IS EVEN OR ODD USING IF–ELSE STATEMENT*/
#include<iostream.h>
void main( )
{
    int a;
    cout << "Enter any integer number \n";
    cin >> a;
    if(a%2 == 0)
        cout << "number is even\n";
    else
        cout << "number is odd\n";
}
```

```text
OUTPUT :
(First run)
Enter any integer number
40
number is even
(Second Run)
Enter any integer number
17
number is odd
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_100_0.png)

Figure 3.31. Output screen of first and second run of program.

### EXPLANATION :

% 的优先级高于 ==，因此 a%2 与 0 进行比较。如果为真，则该数字为偶数，否则数字不是偶数。仅当 if 部分为假时 else 部分才执行，反之亦然。在程序中，if 和 else 部分都只包含一个语句，因此不需要大括号，不过如果加上也不会有任何危害。条件也可以按以下方式书写：

```cpp
if(num%2!=0)
    printf("number is odd\n");
else
    printf("number is even\n");
```

```cpp
/*PROG 3.31 TO CALCULATE GROSS SALARY OF THE PERSON. GIVEN BASIC SALARY(BS) AS INPUT. IF BS IS >5000 DA=55% OF BS AND HRA=15% BS ELSE DA=45% OF BS AND HRA=10% OF BS*/

#include <iostream.h>
void main()
{
    float bs,gs,hra,da;
    cout<<"Enter your basic salary"<<endl;
    cin>>bs;
    if(bs<=5000)
    {
        da=(bs*45)/100;
        hra=(bs*10)/100;
    }
    else
    {
        da=(bs*55)/100;
        hra=(bs*15)/100;
    }
    gs=bs+da+hra;
    cout<<"Basic salary is="<<bs<<endl;
    cout<<"HRA is="<<hra<<endl;
    cout << "DA is=" << da << endl;
    cout << "Gross salary is=" << gs << endl;
}
```

```text
OUTPUT :
Enter your basic salary
8825
Basic salary is=8825
HRA is=1323.75
DA is=4853.75
Gross salary is=15002.5
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_101_0.png)

Figure 3.32. Output screen of program.

### EXPLANATION :

我们将基本工资输入到 bs 中。通过 if 条件我们检查基本工资 bs 是否为 5000。根据 if 条件为真或为假，hra 和 da 按照问题中指定的条件计算。

## 3. if-else 的嵌套

if-else 的嵌套意味着一个 if-else 或简单的 if 作为另一个 if-else 或简单 if 语句的一部分。if-else 的嵌套可能有各种语法，我们介绍其中几种：

### Syntax-1

```cpp
if(condition)
{
    if(condition)
    {
        Statements;
        Statements;
        Statements;
        .................
    }
    else
    {
        Statements;
        Statements;
        Statements;
    }
}
```

在上述情况下，第一个 if 没有 else 部分。

### Syntax-2

```cpp
if(condition)
{
    if(condition)
    {
        Statements;
        Statements;
        Statements;
    }
    else
    {
        Statements;
        Statements;
        Statements;
    }
}
else
{
    Statements;
    Statements;
    Statements;
}
```

### Syntax-3

```cpp
if(condition)
{
    if(condition)
    {
        Statements;
        Statements;
        Statements;
    }
    else
    {
        Statements;
        Statements;
        Statements;
    }
}
else
{
    if(condition)
    {
        Statements;
        Statements;
        Statements;
    }
    else
    {
        Statements;
        Statements;
        Statements;
    }
}
```

```cpp
/* PROG 3.32 TO CHECK WHETHER A YEAR IS LEAP YEAR OR NOT VER 1*/

#include <iostream.h>
void main()
{
    int year;
    cout << "Enter any year\n";
    cin >> year;
    if(year % 100 == 0)
    {
        if(year%400 == 0)
            cout<<"The given year is leap year\n";
        else
            cout<<"The given year is not a leap year\n";
    }
    else
    {
        if(year %4 == 0)
            cout<<"The given year is leap year\n";
        else
            cout<<"The given year is not a leap year\n";
    }
}
```

```text
OUTPUT :
(First Run)
Enter any year
2000
The given year is leap year
(Second run)
Enter any year
2007
The given year is not a leap year
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_104_0.png)
![](img/ad5299318df8d4d7c6df5eaa86590ea3_104_1.png)

Figure 3.33. Output screen of first and second run of program.

### EXPLANATION :

一年是闰年，如果它能被 100 和 400 整除，或者不能被 100 整除但能被 4 整除。最初如果 year %100 为零，内部的 if 检查 year %400 是否为零。如果是，则该年为闰年，否则该年不是闰年。如果外部的 if 失败，则执行其对应的 else 部分，在其中我们检查 year % 4 ==0，如果为真则该年为闰年，否则该年不是闰年。

```cpp
/*PROG 3.33 MAXIMUM OF THREE NUMBERS*/

#include <iostream.h>
void main()
{
    int x,y,z;
    cout << "Enter the three numbers\n";
    cin >> x >> y >> z;
    if((x == y) && (y == z))
        cout << "All three are equal\n";
    else if(x>y)
    {
        if(x>z)
            cout << "Maximum is=" << x << endl;
        else
            cout << "Maximum is=" << z << endl;
    }
    else
    {
        if(y>z)
            cout << "Maximum is=" << y << endl;
        else
            cout << "Maximum is=" << z << endl;
    }
}
```

```text
OUTPUT :
Enter the three numbers
34 765 234
Maximum is=765
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_105_0.png)

Figure 3.34. Output screen of program.

### EXPLANATION :

如果三个数字不相等，我们检查 a>b，如果为真意味着 a 大于 b，我们然后检查 a>c，如果是则 a 为最大，否则 c 为最大。如果 a>b 最初为假意味着 b 大于 a，我们然后检查 b>c，如果是则 b 为最大，否则 c 为最大。

## 4. else-if 阶梯

else-if 阶梯的一般语法如下所示：

```cpp
if (condition)
    Statements;
else if(condition)
    Statements;
else if(condition)
    Statements;
.................;
.................;
```

如果第一个 if 条件得到满足，则执行其所有相关语句，并且所有其他 else-if 都被跳过。仅当第一个 if 失败时，控制才会到达第一个 else-if。第二个、第三个和其他 else-if 也是如此，取决于你的程序需要。即在这个 else-if 阶梯中只有一个 if 条件会被满足。

```cpp
/*PROG 3.34 TO ARRANGE THREE NUMBERS IN ASCENDING ORDER*/

#include <iostream.h>
void main()
{
    int a,b,c,min,max,mid;
    cout<<"Enter the three number"<<endl;
    cin>>a>>b>>c;
    if(a>b && a>c)
        max=a;
    else if(b>a && b>c)
        max=b;
    else if(c>a && c>b)
        max=c;
    if(a<b && a<c)
        min=a;
    else if(b<a && b<c)
        min=b;
    else if(c<a && c<b)
        min=c;
    mid=(a+b+c)-(min+max);
    cout<<"Number in ascending order "<<min
        <<"\t"<<mid<<"\t"<<max<<endl;
}
```

```text
OUTPUT :
Enter the three number
34 57 90
Number in ascending order 34 57 90
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_107_0.png)

Figure 3.35. Output screen of program.

### EXPLANATION :

在变量 max 中我们存储了三个数中的最大值，在变量 min 中我们存储了三个数中的最小值。mid 是通过用 (min + max) 从 a、b、c 的和中减去得到的，即 (a + b + c)。

## 5. switch-case 语句

switch-case 语句可用于替换 else-if 阶梯结构。其一般语法如下：

```cpp
switch(expression)
{
    case choice1 :
        statements;
        break;
    case choice2 :
        statements;
        break;
    case choice3 :
        statements;
        break;
        ...........................;
        ...........................;
    default :
}
```

表达式可以是任何整数或字符类型，其结果仅为字符或整数。choice 1、choice 2 和 choice n 是我们将与表达式进行测试的可能值。如果从 choice 1 到 choice n 的值中没有一个与表达式的值匹配，则执行 default 分支。

### Some Points For switch-case Statements

- switch 语句是一个多分支语句。
- 如果有可能从多个选项中做出选择，这种结构化选择是有用的。

