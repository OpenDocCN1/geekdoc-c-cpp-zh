

## 黑盒视角

从黑盒视角来看 show_n_char()，输入是要显示的字符和要跳过的空格数，结果动作是将该字符打印指定次数。输入通过参数传递给函数。这些信息足以告诉你在 main() 中如何使用该函数，同时也为编写该函数提供了设计规范。

ch、num 和 count 是 show_n_char() 函数私有的局部变量，这是黑盒方法的一个基本方面。如果你在 main() 中使用相同名称的变量，它们将是独立的变量。也就是说，如果 main() 中有一个 count 变量，更改它的值不会改变 show_n_char() 中 count 的值，反之亦然。黑盒内部发生的事情对调用函数是隐藏的。

## 使用 return 从函数返回值

你已经看到了如何将信息从调用函数传递给被调用函数。要向相反方向传递信息，可以使用函数返回值。为了回顾其工作原理，我们将构造一个返回两个参数中较小值的函数。我们将这个函数命名为 imin()，因为它专为处理 int 值而设计。我们还将创建一个简单的 main()，其唯一目的是检查 imin() 是否正常工作。像这样用于测试函数的程序有时称为驱动程序。驱动程序会“试驾”函数。如果函数表现良好，它就可以安装到更重要的程序中。程序清单 9.3 展示了该驱动程序和最小值函数。

### 程序清单 9.3 lesser.c 程序

```
/* lesser.c -- finds the lesser of two evils */
#include <stdio.h>
int imin(int, int);

int main(void)
{
    int evil1, evil2;

    printf("Enter a pair of integers (q to quit):\n");
    while (scanf("%d %d", &evil1, &evil2) == 2)
    {
        printf("The lesser of %d and %d is %d.\n", evil1, evil2, imin(evil1,evil2));
        printf("Enter a pair of integers (q to quit):\n");
    }
    printf("Bye.\n");

    return 0;
}
```

```
int imin(int n,int m)
{
    int min;

    if (n < m)
        min = n;
    else
        min = m;

    return min;
}
```

回想一下，scanf() 返回成功读取的项数，因此输入不是两个整数将导致 while 循环终止。下面是一个示例运行：

```
Enter a pair of integers (q to quit):
509 333
The lesser of 509 and 333 is 333.
Enter a pair of integers (q to quit):
-9393 6
The lesser of -9393 and 6 is -9393.
Enter a pair of integers (q to quit):
q
Bye.
```

关键字 return 使后续表达式的值成为函数的返回值。在本例中，函数返回赋给 min 的值。由于 min 是 int 类型，因此 imin() 函数也是 int 类型。

变量 min 是 imin() 私有的，但 min 的值通过 return 传递回调用函数。如下一条语句的效果是将 min 的值赋给 lesser：

```
lesser = imin(n,m);
```

你能改写成下面这样吗？

```
imin(n,m);
lesser = min;
```

不能，因为调用函数根本不知道 min 的存在。请记住，imin() 的变量是 imin() 的局部变量。函数调用 imin(evil1,evil2) 将一组变量的值复制给另一组变量。

返回值不仅可以赋给变量，还可以用作表达式的一部分。例如：

```
answer = 2 * imin(z, zstar) + 25;
printf("%d\n", imin(-32 + answer, LIMIT));
```

返回值可以由任何表达式提供，而不只是变量。例如，你可以将程序缩短为：

```
/* minimum value function, second version */
imin(int n,int m)
{
    return (n < m) ? n : m;
}
```

条件表达式的计算结果为 n 或 m，选其中较小者，然后该值返回给调用函数。如果你为了清晰或风格，喜欢将返回值括在括号中，也是可以的，尽管括号并非必需。

如果函数返回的类型与声明的类型不同会怎样？

```
int what_if(int n)
{
    double z = 100.0 / (double) n;
    return z; // what happens?
}
```

那么实际返回值就是你把指定的返回值赋给声明返回类型的变量后得到的值。因此，在这个例子中，最终效果与将 z 的值赋给一个 int 变量然后返回该值相同。例如，假设我们有以下函数调用：

```
result = what_if(64);
```

那么 z 被赋值为 1.5625。但 return 语句返回的是 int 值 1。

使用 return 还有另一个作用：它会终止函数并将控制权返回给调用函数中的下一条语句。即使 return 语句不是函数中的最后一条语句，也会发生这种情况。因此，你可以这样编写 imin()：

```
/* minimum value function, third version */
imin(int n,int m)
{
    if (n < m)
        return n;
    else
        return m;
}
```

许多（但不是所有）C 语言实践者认为，最好只在函数末尾使用一次 return，以便更容易让人跟踪函数的控制流。然而，在像这样短小的函数中使用多个 return 也并非大错。无论如何，对用户来说，三个版本都是一样的，因为所有版本接受相同的输入并产生相同的输出，只是内部实现不同。即使这个版本也能同样工作：

```
/* minimum value function, fourth version */
imin(int n, int m)
```

## 问题所在

让我们看一些涉及 imax()（imin() 的近亲）的例子。程序清单 9.4 展示了一个以老式方式声明 imax() 然后错误使用它的程序。

### 程序清单 9.4 misuse.c 程序

```
/* misuse.c -- uses a function incorrectly */
#include <stdio.h>
int imax();      /* old-style declaration */

int main(void)
{
    printf("The maximum of %d and %d is %d.\n", 3, 5, imax(3));
    printf("The maximum of %d and %d is %d.\n", 3, 5, imax(3.0, 5.0));
    return 0;
}

int imax(n, m)
int n, m;
{
    return (n > m ? n : m);
}
```

第一次调用 printf() 时省略了 imax() 的一个参数，第二次调用则使用了浮点参数而不是整数。尽管存在这些错误，程序仍然可以编译和运行。

以下是使用 Xcode 4.6 的示例输出：

```
The maximum of 3 and 5 is 1606416656.
The maximum of 3 and 5 is 3886.
```

使用 gcc 运行的示例产生了 1359379472 和 1359377160 这些值。这两个编译器都工作正常；它们只是程序未使用函数原型的受害者。

发生了什么？具体机制可能因系统而异，但在 PC 或 VAX 上是这样的：调用函数将其参数放入一个称为栈的临时存储区域，被调用函数从栈中读取这些参数。这两个过程并不相互协调。调用函数根据调用中的实际参数决定传递哪种类型，而被调用函数则根据其形式参数的类型读取值。因此，调用 imax(3) 将一个整数放到栈上。当 imax() 函数开始执行时，它从栈上读取两个整数。实际上只放了一个整数，所以读取的第二个值是当时恰好位于栈上的某个值。

示例第二次使用 imax() 时，将 float 值传递给 imax()。这会在栈上放置两个 double 值。（回想一下，float 作为参数传递时会被提升为 double。）在我们的系统上，这是两个 64 位的值，所以栈上放置了 128 位数据。当 imax() 从栈上读取两个 int 时，它读取栈上前 64 位，因为在我们的系统上每个 int 是 32 位。这些位恰好对应两个整数值，其中较大的是 3886。

## ANSI C 的解决方案

ANSI C 标准针对参数不匹配问题的解决方案是允许函数声明也声明变量类型。结果就是函数原型——一种声明，它说明返回类型、参数数量以及这些参数的类型。为了表明 imax() 需要两个 int 参数，你可以使用以下任一原型声明它：

```
int imax(int, int);
int imax(int a, int b);
```

第一种形式使用逗号分隔的类型列表。第二种形式在类型后加上变量名。请记住，变量名是占位名，不必与函数定义中使用的名称一致。

有了这些信息，编译器就可以检查函数调用是否与原型匹配。参数数量是否正确？类型是否正确？如果存在类型不匹配并且两种类型都是数字，编译器会将实际参数的值转换为与形式参数相同的类型。例如，imax(3.0, 5.0) 会变成 imax(3, 5)。我们已经修改了程序清单 9.4 以使用函数原型，结果如程序清单 9.5 所示。

### 程序清单 9.5 proto.c 程序

```
/* proto.c -- uses a function prototype */
#include <stdio.h>
int imax(int, int);      /* prototype */
int main(void)
{
    printf("The maximum of %d and %d is %d.\n", 3, 5, imax(3));
    printf("The maximum of %d and %d is %d.\n", 3, 5, imax(3.0, 5.0));
    return 0;
}

int imax(int n, int m)
{
    return (n > m ? n : m);
}
```

