

```c
void name()
{
    char empname[25];
    printf("Enter the employee name : ");
    scanf("%s", empname);
    printf("The employee name is %s", empname);
}
```

```
The program displays the following output
Enter the employee name : Rama
The employee name is Rama
```

在程序 2.2 中，main() 是调用函数，它调用函数 name()。函数 name() 不包含参数，因此没有参数声明。请注意，被调用函数（即 name）直接从输入终端（即键盘）接收其数据（即员工姓名），并在被调用函数本身中将 empname 的内容显示到输出终端（即屏幕）。由于没有内容需要返回，因此未使用 return 语句。函数的右花括号表示函数执行结束，从而将控制权返回给调用函数。关键字 void 用于函数 name() 之前，以指示没有返回值。

## 无参数且有返回值的函数

当函数没有参数时，它不会从调用函数接收任何数据，但可以进行一些处理，然后将结果返回给被调用函数。因此，调用函数和被调用函数之间存在数据传输。程序 2.3 有助于你更好地理解这些内容。

### 程序 2.3:

```c
/* Program to find the sum of even numbers within the limit. */
/* retnoarg.c */
#include<stdio.h>
int sum();
/* Function prototype */
void main()
{
    printf(" %d", sum());
}
int sum()
{
    int i, n, result = 0;
    printf("Enter the limit : ");
    scanf("%d", &n);
    printf("Sum of Even numbers within %d is ", n);
    for(i = 2 ; i <= n ; i += 2)
    {
        result += i;
    }
    return(result);
}
```

```
The program displays the following output
Enter the limit : 10
Sum of Even numbers within 10 is 30
```

在程序 2.3 中，main() 是调用函数，它调用函数 sum()。sum() 不包含参数，因此没有参数声明。请注意，被调用函数（即 sum()）直接在被调用函数（即 sum()）中从输入终端（即键盘）接收其数据（即计算偶数的上限）。该函数中使用了 return 语句，以返回在限制内计算的前 n 个偶数之和，结果从 main() 函数显示到标准输出设备（即屏幕）。请注意，在函数名 sum() 之前使用 int 而不是 void，因为它向被调用函数返回 int 类型的值。

## 有参数但无返回值的函数

当函数有参数时，它会从调用函数接收数据。main() 函数无法控制函数接收输入数据的方式。我们也可以让调用函数从输入终端读取数据并将其传递给被调用函数。这种方法似乎更好，因为调用函数可以在将数据传递给被调用函数之前检查数据的有效性。程序 2.4 有助于你更好地理解这些内容。

### 程序 2.4:

```c
/* Program to calculate simple interest. */
/* agnot.c */
#include<stdio.h>
void simple(float, float, int); /* Function prototype or declaring functions */
float principal, rate;
int year;
void main()
{
printf("Enter principal,rate of interest & no.of years \n");
scanf("%f %f %d", &principal, &rate, &year);
simple(principal, rate, year);
}
void simple(float principal, float rate, int year)
{
float simple_interest = 0.0;
simple_interest = ( principal * rate * year ) / 100;
printf("The simple interest is %.2f", simple_interest);
}
```

```
The program displays the following output
Enter principal,rate of interest & no.of years
5000 1.5 2
The simple interest is 150.00
```

在程序 2.4 中，main() 是调用函数，它调用函数 simple()。该函数接收三个参数（即 principal、rate 和 year）。前两个参数为浮点类型，第三个参数为整型。请注意，被调用函数（即 simple()）从调用函数（即 main()）接收其数据。由于没有内容需要返回，因此未使用 return 语句。函数的右花括号标志着函数结束，从而将控制权返回给调用函数。关键字 void 用于函数名 simple() 之前，以指示没有返回值。

## 有参数且有返回值的函数

当函数有参数时，它会从调用函数接收数据，进行一些处理，然后将结果返回给被调用函数。这样一来，main() 函数将对该函数拥有控制权。这种方法似乎更好，因为调用函数可以在将数据传递给被调用函数之前检查数据的有效性，并在将结果发送到标准输出设备（即屏幕）之前检查结果的有效性。请注意，当调用函数时，实际参数值的副本会被传递给被调用函数。程序 2.5 有助于你更好地理解这些内容。

### 程序 2.5:

```c
/* Program to find the sum of first N natural numbers. */
/* arg_ret.c */
#include<stdio.h>
int sum(int x); /* Function prototype */
void main()
{
int n;
printf("Enter the limit : ");
scanf("%d", &n);
printf("Sum of first %d natural numbers is %d", n, sum(n));
}
int sum(int x)
{
int i, result = 0;
for(i = 1; i <= x; i++)
result += i;
return(result);
}
```

在程序 2.5 中，main() 是调用函数，它调用函数 sum()。函数 sum() 接收一个参数。请注意，被调用函数（即 main()）从调用函数（即 main()）接收其数据。该函数中使用了 return 语句，以返回从标准输入设备输入的 n 个自然数之和，结果从 main() 函数显示到标准输出设备。请注意，在函数名 sum() 之前使用 int 而不是 void，因为它向被调用函数返回 int 类型的值。

## 调用函数时需注意的重要事项

- 函数名后必须加括号。
- 函数调用中的函数名与函数定义中的函数名必须相同。
- 实际参数和形式参数的类型、数量和顺序必须相同。
- 调用函数时，语句末尾必须使用分号。

## 2.2 向函数传递值

向函数传递参数通常有两种方式，即：

- 按值传递。
- 按引用传递。

在按值传递中，会创建变量的副本并将其作为参数传递给函数。在这种方法中，对函数参数所做的更改不会影响调用该函数的变量，因为更改仅在函数内部进行。在按引用传递中，每个参数的地址会被传递给函数。在这种方法中，对函数参数所做的更改会影响调用该函数的变量。

### 2.2.1 按值传递

传递变量实际值的过程称为按值传递。在这种情况下，调用函数中的值作为参数传递给被调用函数。当通过实际参数将值传递给函数时，实际参数的值会被复制到被调用函数中的变量，因此相应形式参数的值可以在函数内更改，但调用函数中实际参数的值不会更改。程序 2.6 有助于你更好地理解这些内容。

程序 2.6:

```c
/* Program to demonstrate call by value. */
/* call_val.c */
#include<stdio.h>
void add(int);
void main()
{
int x = 5;
printf("\n Value of x before calling the function is %d", x);
add(x);
printf("\n Value of x after calling the function is %d", x);
}
void add(int y)
{
y = y + 5;
printf("\n Value of x in the called function is %d", y);
}
```

