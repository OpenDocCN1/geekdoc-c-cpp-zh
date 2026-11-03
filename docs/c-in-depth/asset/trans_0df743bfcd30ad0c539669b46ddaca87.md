
```c
printf("Maximum of %d and %d is : %d\n",a,b,max(a,b));
}
max(int x,int y)
{
    if(x>y)
        return x;
    else
        return y;
}
```

## 6.7 return 语句

`return` 语句用于在函数中将值返回给调用函数。它也可以用于从被调用函数立即退出并返回调用函数，而不返回任何值。

该语句可以出现在函数体内的任何位置。它有两种使用方式——

- `return;`
- `return ( expression );`

这里 `return` 是关键字。`return` 语句的第一种形式用于终止函数而不返回任何值。在这种情况下只写 `return` 关键字。下面的程序使用了这种形式的 `return` 语句。

```c
/*P6.7 Program to understand the use of return statement*/
#include<stdio.h>
void funct(int age,float ht);
main()
{
    int age;
    float ht;
    printf("Enter age and height: ");
    scanf("%d %f", &age, &ht);
    funct(age,ht);
}
void funct(int age,float ht)
{
    if(age>25)
    {
        printf("Age should be less than 25\n");
        return;
    }
    if(ht<5)
    {
        printf("Height should be more than 5\n");
        return;
    }
    printf("Selected\n");
}
```

`return` 语句的第二种形式用于终止函数并向调用函数返回一个值。程序 P6.3 和 P6.6 使用了 `return` 语句的第二种形式。`return` 语句返回的值可以是任何常量、变量、表达式，甚至是任何其他函数调用（该调用返回一个值）。例如，在程序 P6.3 中，我们可以直接写 `return (x+y)`，而不必先取一个变量再返回它。同样，在程序 P6.6 中，我们可以直接写 `return ( x>y ? x : y )`。

其他一些有效 `return` 语句的示例包括——

- `return 1;`
- `return x++;`
- `return ( x*y*z );`
- `return ( 3 * sum(a, b) );`

将返回值括在圆括号中是可选的。

我们可以在一个函数中使用多个 `return` 语句，但一旦遇到第一个 `return` 语句，函数就会终止，其后的所有语句都不会执行。

下一个函数比较两个日期（d1/m1/y1 和 d2/m2/y2），如果第一个日期较小则返回 1，如果第二个日期较小则返回 -1，如果两个日期相同则返回 0。在这个函数中，我们使用了 7 个 `return` 语句。

```c
int cmpdate( int d1, int m1, int y1, int d2, int m2, int y2)
{
    if(y1<y2)
        return 1;
    if(y1>y2)
        return -1;
    if(m1<m2)
        return 1;
    if(m1>m2)
        return -1;
    if(d1<d2)
        return 1;
    if(d1>d2)
        return -1;
    return 0;
}
```

下一个程序使用一个函数来求一个数的阶乘。

```c
/*P6.8 Program to find out the factorial of a number*/
#include<stdio.h>
long int factorial(int n);
main()
{
    int num;
    printf("Enter a number : ");
    scanf("%d",&num);
    if(num<0)
        printf("No factorial of negative number\n");
    else
        printf("Factorial of %d is %ld\n",num,factorial(num));
}
long int factorial(int n)
{
    int i;
    long int fact=1;
    if(n==0)
        return 1;
    for(i=n;i>1;i--)
        fact*=i;
    return fact;
}
```

一个函数只能返回一个值。如果我们想返回多个值，就必须使用后续章节讨论的另一种技术。试图使用逗号返回多个值是不正确的。

```c
return 1, 2, 3;
```

这里该表达式使用了逗号运算符，因此只会返回最右侧的值。

如果函数不返回任何值，则应将其声明为 `void`。所有不是 `void` 类型的函数都会返回一个值。如果函数不是 `void` 类型，且没有通过 `return` 语句返回值，则会自动返回一个垃圾值。

如果返回值的类型不是函数定义中指定的类型，那么在转换合法的情况下，会将其转换为该类型。

## 6.8 函数参数

调用函数向被调用函数发送一些值以进行通信；这些值称为参数（arguments 或 parameters）。

**实际参数：** 在函数调用中写出的参数称为实际参数，因为这些值是实际发送给被调用函数的值。实际参数可以写成变量、常量、表达式或任何返回值的函数调用。例如——

```c
func(x)
func(a*b, c*d+k)
func(22, 43)
func(1, 2, sum(a, b))
```

**形式参数：** 在函数定义中写出的参数名称称为形式参数或哑参数，因为它们仅用于保存调用函数发送的值。

```c
/*P6.9 Program to understand formal and actual arguments*/
#include<stdio.h>
main()
{
    int m=6,n=3;
    printf("%d\t",multiply(m,n));
    printf("%d\t",multiply(15,4));
    printf("%d\t",multiply(m+n,m-n));
    printf("%d\n",multiply(6,sum(m,n)));
}
multiply(int x,int y)
{
    int p;
    p=x*y;
    return p;
}
sum(int x, int y)
{
    return x+y;
}
```

**输出：**

```c
18 60 27 54
```

在这个程序中，函数 `multiply()` 被调用了 4 次。变量 `x` 和 `y` 是 `multiply()` 的形式参数。第一次调用该函数时，实际参数是变量 `m` 和 `n`，因此形式参数 `x` 和 `y` 分别用 `m` 和 `n` 的值初始化，并返回 `p=18`。第二次调用函数时，实际参数为 15 和 4，因此这次 `x` 和 `y` 分别初始化为 15 和 4，于是返回 `p=60`。同样，第三次 `x` 和 `y` 分别初始化为 `m+n=9` 和 `m-n=3`，于是返回 `p=27`。在第四次调用中，第一个参数是常量值（6），而第二个参数是函数调用。因此这次 `x` 被初始化为 6，`y` 被初始化为函数 `sum()` 返回的值，即 9。于是这次返回 `p=54`。

形式参数和实际参数的名称可以相同，也可以不同，因为它们写在不同的函数中。

```c
/*P6.10 Program to understand formal and actual arguments*/
#include<stdio.h>
main()
{
    int a=6,b=3;
    func(a,b);
    func(15,4);
    func(a+b,a-b);
}
func(int a,int b)
{
    printf("a = %d    b = %d\n",a,b);
}
```

**输出：**

```c
a = 6   b = 3
a = 15  b = 4
a = 9   b = 3
```

在上面的程序中，我们可以看到 `main()` 内 `a` 和 `b` 的值是 6 和 3，而 `func()` 内的 `a` 和 `b` 则用每次调用时发送的实际参数值初始化。在函数内对形式参数所做的任何更改都不会影响实际参数。

## 6.9 函数的类型

根据参数和返回值，函数可以分为四类。

1. 无参数且无返回值的函数。
2. 无参数但有返回值的函数。
3. 有参数但无返回值的函数。
4. 有参数且有返回值的函数。

### 6.9.1 无参数且无返回值的函数

无参数且无返回值的函数写法如下——

```c
void func(void);
main()
{
    ........
    func();
    ........
}
void func(void)
{
    ........
    statement;
    ........
}
```

在上面的示例中，函数 `func()` 由 `main()` 调用，函数定义写在 `main()` 函数之后。由于函数 `func()` 没有参数，`main()` 不能向 `func()` 发送任何数据；又因为它没有 `return` 语句，所以该函数不能向 `main()` 返回任何值。调用函数和被调用函数之间没有通信。由于没有返回值，这类函数不能用作表达式中的操作数。P6.2 中的函数 `drawline()` 就是这类函数的一个示例。让我们再看一个示例程序——

```c
/*P6.11 Program that uses a function with no arguments and no return values*/
#include<stdio.h>
void dispmenu(void);
main()
{
    int choice;
    dispmenu();
    printf("Enter your choice :");
    scanf("%d",&choice);
}
void dispmenu(void)
{
    printf("1.Create database\n");
    printf("2.Insert new record\n");
    printf("3.Modify a record\n");
}
```
