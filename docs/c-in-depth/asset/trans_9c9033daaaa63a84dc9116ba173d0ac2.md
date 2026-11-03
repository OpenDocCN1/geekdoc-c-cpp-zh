

```c
printf("4.Delete a record\n");
printf("5.Display all records\n");
printf("6.Exit\n");
}
```

## 6.9.2 无参数但有返回值的函数

这类函数不接收任何参数，但可以返回一个值。

```c
int func(void);
main()
{
    int r;
    .......
    r=func();
    .......
}
int func(void)
{
    ........
    ........
    return (expression);
}
```

下一个程序使用了这种类型的函数。

```c
/*P6.12 Program that returns the sum of squares of all odd numbers from 1 to 25*/
#include<stdio.h>
int func(void);
main()
{
    printf("%d\n",func());
}
int func(void)
{
    int num,s=0;
    for(num=1;num<=25;num++)
    {
        if(num%2!=0)
            s+=num*num;
    }
    return s;
}
```

输出：

2925

## 6.9.3 有参数但无返回值的函数

这类函数带有参数；因此，调用函数可以向被调用函数发送数据，但被调用函数不返回任何值。这些函数可以写成：

```c
void func(int,int);
main()
{
    func(a,b);
    ...
}
void func(int c,int d)
{
    statements
}
```

这里的`a`和`b`是实际参数，用于发送值；`c`和`d`是形式参数，用于接收来自实际参数的值。

```c
/*P6.13 Program to find the type and area of a triangle.*/
#include<stdio.h>
#include<math.h>
void type(float a,float b,float c);
void area(float a,float b,float c);
main()
{
    float a,b,c;
    printf("Enter the sides of triangle : ");
    scanf("%f%f%f",&a,&b,&c);
    if(a<b+c && b<c+a && c<a+b)
    {
        type(a,b,c);
        area(a,b,c);
    }
    else
        printf("No triangle possible with these sides\n");
}
void type(float a,float b,float c)
{
    if((a*a)+(b*b)==(c*c)||(b*b)+(c*c)==(a*a)||(c*c)+(a*a)==(b*b))
        printf("The triangle is right angled triangle\n");
    if(a==b && b==c)
        printf("The triangle is equilateral\n");
    else if(a==b || b==c || c==a)
        printf("The triangle is isosceles\n");
    else
        printf("The triangle is scalene\n");
}
void area(float a,float b,float c)
{
    float s, area;
    s=(a+b+c)/2;
    area=sqrt(s*(s-a)*(s-b)*(s-c));
    printf("The area of triangle = %f\n",area);
}
```

## 6.9.4 有参数且有返回值的函数

这类函数带有参数，因此调用函数可以向被调用函数发送数据。它们也可以使用`return`语句向调用函数返回一个值。这个函数可以写成：

```c
int func(int,int);
main()
{
    int r;
    ........
    r=func(a,b);
    ........
    func(c,d);
}
int func(int a,int b )
{
    ........
    ........
    return (expression);
}
```

这里的`return`语句将表达式的值返回给调用函数。我们之前编写的`sum()`、`multiply()`和`max()`函数就是这类函数的例子。让我们再看一个示例程序：

```c
/*P6.14 Program to find the sum of digits of any number*/
#include<stdio.h>
int sum(int n);
main()
{
    int num;
    printf("Enter the number : ");
    scanf("%d",&num);
    printf("Sum of digits of %d is %d\n",num,sum(num));
}
int sum(int n)
{
    int i,sum=0,rem;
    while(n>0)
    {
        rem=n%10;        /*rem takes the value of last digit*/
        sum+=rem;
        n/=10;           /*skips the last digit of number*/
    }
    return (sum);
}
```

在描述不同类型的函数时，为简单起见，我们假设参数和返回值都是`int`类型。这些值可以是任何数据类型。

## 6.10 关于函数声明的更多内容

放置函数声明的关键点是它必须在函数调用之前。通常，所有函数声明都写在`main()`函数之前。这样，函数声明对所有函数都是可见的。也可以只在调用该函数的那些函数内部进行声明。注意，如果函数定义出现在函数调用之前，则不需要声明。

如果函数返回`int`或`char`类型的值，则不必声明该函数，因为默认情况下每个函数都会返回一个`int`值。编译器假设任何在定义中未指定返回类型的函数都会返回`int`值。但如果函数返回的是`int`以外的值，例如`float`、`double`、指针、数组、结构体等，则必须在函数调用之前声明它。

函数的声明有两个主要用途。第一，它告诉编译器函数的返回类型。第二，它指定了函数的参数类型和数量。因此，它可以用来检查函数定义和函数调用中参数数量和类型是否匹配。我们已经看到，声明`int`或`char`类型的函数是可选的，但最好声明所有函数，因为这样可以检查函数调用中参数的数量和类型。通过这种方式，我们可以防止由于函数调用中参数数量和类型错误而可能出现的bug。

## 6.11 无参数函数的声明

如果函数没有参数，那么可以将括号留空，也可以在括号内写入`void`。但最好写上`void`，因为当括号为空时，编译器会假定没有关于参数的信息。可能没有参数，也可能有任意数量的参数。因此，编译器将无法检查函数调用中参数类型和数量的任何不匹配。

类似地，如果函数不返回任何值，可以将返回类型指定为`void`。这将避免在表达式中意外使用该函数。例如：

```c
/*P6.15 Program to understand declaration of functions with no arguments*/
#include<stdio.h>
void func1();
void func2(void);
main()
{
    func1(1.3,'a'); /*will not generate any error*/
    func2(1.3,'a'); /*will generate error*/
}
void func1()
{
    printf("\nFunction1\n");
}
void func2(void )
{
    printf("\nFunction2\n");
}
```

这里我们看到，`func1()`可以用错误数量和类型的参数调用，并且不会显示任何编译错误，因此这可能是一个难以发现的bug。而用任何参数调用函数`func2()`则是不可能的。

## 6.12 如果没有函数声明

如果实际参数多于形式参数，那么多余的实际参数会被忽略。如果实际参数少于形式参数，那么多余的形式参数会接收到垃圾值。

```c
func(int a, int b,int c)
{
    ........
    ........
}
```

```c
func(1, 2, 3, 4, 5);        /*Actual arguments more than formal*/
```

这里最后两个参数被忽略。`a = 1`，`b = 2`，`c = 3`。

```c
func(1, 2);                 /*Actual arguments less than formal*/
```

这里第三个参数接收到一个垃圾值。`a = 1`，`b = 2`，`c = 垃圾值`。

如果对应的实际参数和形式参数之间存在类型不匹配，那么编译器会尝试将实际参数的类型转换为形式参数的类型，如果转换合法的话；否则，一个垃圾值会被传递给形式参数。

## 6.13 函数参数的求值顺序

当一个函数被调用且带有多个参数时，参数的求值顺序是未指定的。这种求值顺序在像`multiply(m, n)`或`multiply(m+n, n)`这样的函数调用中并不重要。但如果我们有一个像这样的函数调用：

```c
int m = 3, k;
k = multiply(m, m++);
```

现在，如果第一个参数先被求值，`k`的值将是9；如果第二个参数先被求值，`k`的值将是12。但由于在C中参数的求值顺序未指定，且取决于编译器，因此在不同编译器上的结果可能会不同。类似地，如果我们写：

```c
int i = 10;
printf("%d %d %d", --i, i++, i);
```

这里的结果也是不可预测的。因此，最好避免使用这些可能在不同编译器上产生不同结果的参数表达式。

## 6.14 main() 函数

每个C程序的执行总是从`main()`函数开始。每个函数都在`main()`中直接或间接地被调用，当所有函数完成其操作后，控制权返回到`main()`。一个程序中只能有一个`main()`函数。

`main()`函数是一个用户自定义函数，但其名称、参数的数量和类型在语言中是预定义的。操作系统调用`main()`函数，而`main()`向操作系统返回一个整数值。如果返回值为零，则表示函数已成功终止；任何非零的返回值都表示出错。如果在`main()`中没有指定返回值，则会自动返回一个垃圾值。调用带整数参数的`exit()`函数

