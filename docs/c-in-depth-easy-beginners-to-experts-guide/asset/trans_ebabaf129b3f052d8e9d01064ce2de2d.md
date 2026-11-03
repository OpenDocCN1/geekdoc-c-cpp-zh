

![](img/3a2b6e5e90a58a56458b0539952c0cd2_155_0.png)

## 第八章

（函数与你的大脑）

函数是一个小程序，它接收一些输入并为我们提供一些输出。函数允许将大型程序分解为许多较小的独立组件，每个组件都有明确的目的。它避免了反复重写代码。将逻辑分解为单独的函数使编写和调试的整个过程更加容易。

另一方面，可以说函数是一个用于执行某项任务的独立语句块。函数一旦被分配了某项工作，就可以被任意多次调用以执行该任务。每个 C 程序都会使用一些函数；常用的函数有 printf、scanf、main 等。

函数可以是库函数或用户自定义函数。库函数是随编译器一起提供并存在于磁盘中的函数。用户自定义函数是程序员自己编写的函数，目的是使程序更容易调试和跟踪。

printf()、scanf()、exit()、pow() 都是库函数。每个库函数都有一个头文件。C 语言中一共有 15 个头文件。main() 是一个用户自定义函数。

每个程序都必须有一个 main 函数。这个 main 函数用于标记执行的开始。虽然只用 main 函数就能编写任何程序，但这会带来很多问题。程序会变得过于庞大和复杂，因而难以跟踪、调试和测试。

但如果将同一个程序拆分成独立编码的小模块，然后再组合成一个整体，那么这些问题就能轻松解决。这些模块就称为函数。因此，函数可以定义为一个接收一些输入并为我们提供一些输出的小程序。

**要点提示 –** 我不会一遍又一遍地输入头文件，所以在编写程序时，请不要忘记在程序开头包含头文件。

### 计算两个数之和的函数

```c
int sum(int, int);      /* Function Prototype or Declaration */
main()
{
    int a,b,ans;
    printf("Enter two numbers: ");
    scanf("%d %d",&a,&b);
    ans = sum(a,b);          /* Function Call */
    printf(" sum is %d", ans);
    getch();
}
int sum(int x, int y)      /* Function Definition or Process */
{
    int z;
    z = x + y;
    return(z);
}
```

### 现在让我们来看看这个程序的一些特点

- 1. 第一条语句是函数的声明，它告诉编译器函数的名称以及所传递参数的数据类型。
- 2. 该声明也称为原型。
- 3. 如果输出类型是整数值，则函数声明不是必需的。在某些 C 编译器中，并非所有函数都需要声明。
- 4. 函数调用是使用函数的方式。函数声明一次，定义一次，但在同一程序中可以使用多次。
- 5. 当编译器遇到函数调用时，程序的控制权会转移到函数定义；然后函数将逐行执行，并在最后返回一个值。
- 6. 在主程序的末尾是函数的定义，也可以称为过程。
- 7. 函数定义不以分号结尾。
- 8. 函数可能返回值，也可能不返回值。因此，return 语句不是必需的。当遇到 return 语句时，控制权会立即返回给调用函数。
- 9. 虽然可以向函数传递任意数量的参数，但被调用函数在一次调用中只返回一个值。return 语句可以使用为：

```c
return;
```
或
```c
return(value);
```

- 10. 一个函数可以有多个 return 语句。它可以这样使用：

```c
if (a!=0)
    return(a);
else
    return(1);
```

- 11. 默认情况下，所有函数都返回 int。但如果函数必须返回特定类型的数据，则可以在函数名旁边使用类型说明符。

```c
long int fact(n)
```

- 12. 如果 main() 函数调用 sum() 函数，那么 main() 是调用函数，sum() 是被调用函数。

### 无参数且无返回值

有些函数不接收来自调用函数的任何值。因此，函数原型将如下所示：

`prn( )` 即不传递任何参数。这也可以通过 `prn(void)` 来实现。同样，调用函数也不会从该函数获得任何值。这可以通过在函数名之前使用关键字 `void` 来实现。为了说明这一点，让我们考虑以下程序：

```c
void prn();   /* declaration can also be made as void prn(void); */
main()
{
    prn();
    prn();
    prn();
}
void prn()
{
    printf("Hello");
}
```

### 参数传递机制

### （i）按值调用

当按值传递参数时，实际参数的副本会从调用函数传递给被调用函数定义中的形参。

现在，在被调用函数定义中对形参所做的任何更改都不会反映到调用函数的实参中。

例如，在上述计算两个数之和的函数中，调用语句写成如下形式：

```c
ans = sum(a, b);
```

在定义中，变量 x、y 分别接受 a、b 的值。这里，变量 a、b 称为实际参数，而 x、y 称为形式参数。

实际参数和形式参数的作用域不同，因此在形式参数中进行的任何更改都不会在实参中体现。

例如：

```c
void swap(int, int);
main()
{
    int a,b;
    printf("Enter 2 numbers");
    scanf("%d%d",&a,&b);
    swap(a,b);      /* In this call statement a,b are the actual parameters */

    printf("%d\t%d",a,b);
}
void swap(int x, int y)  /* In this function definition x & y are the formal parameters */
{
    int t;
    t=x; x=y; y=t;
}
```

**要点提示 –** 在上述示例中：对 x、y 所做的更改不会反映到 a、b 中。

### （ii）按引用调用

当按引用传递参数时，实际参数的地址会从调用函数传递给被调用函数定义中的形参。

现在，在被调用函数定义中对形参所做的任何更改都会反映到调用函数的实参中。

有时无法传递变量的值；例如，使用数组时，无法通过按值调用来传递数组的所有值。

因此，使用了另一种类型的函数调用机制：按引用调用，即传递变量的地址。

这里，定义将通过访问特定地址来工作。这种方法通常用于数组和指针。

例如：

```c
main()
{
    int a,b;
    printf("Enter 2 numbers");
    scanf("%d%d",&a,&b);
    swap(&a, &b);   /* In this call statement address
                       of a, b gets transferred */
    printf("%d\t%d",a,b);
}
void swap(int *p1, int *p2)   /* In this function
definition p1 & p2 are the pointers which receive the
address of a, b */
{
    int t;
    t=*p1; *p1=*p2; *p2=t;
}
```

**要点提示 –** 在上述示例中：对 p1、p2 所做的更改将自动反映到 a、b 中。

**要点提示 –** 数组也是按引用传递的。当我们传递数组名时，只有基地址会被传递到函数定义中。

### 函数的类型

- 1. 库函数 – 之前在库中定义的函数称为库函数。

例如：

```c
#include<math.h>
main()
{
    int n, p, ans;
    printf("Enter number and its power");
    scanf("%d%d",&n,&p);
    ans = pow(n,p);
    printf("%d",ans);
    getch();
}
```

### 常用库函数

### stdio.h 函数

| Function | 描述 |
| --- | --- |
| fclose() | 关闭一个流 |
| fcloseall() | 关闭所有打开的流 |
| feof() | 测试是否已到达流的文件末尾 |
| fflush() | 刷新一个流 |

