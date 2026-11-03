
- (b) 可以有多个声明。
- (c) 变量不能在声明时初始化。
- (d) 声明中必须始终指定关键字 extern。
- (e) 声明也可以放在函数内部。

考虑以下程序：

```
#include<stdio.h>
int x=8;
main()
{
    ......
}
func1()
{
    ......
}
func2()
{
    .........
}
```

在这个程序中，变量 x 对所有函数都是可用的，因为外部变量从其定义点开始一直到程序结束都是活跃的。现在，如果我们像这样改变变量 x 的定义位置——

```
#include<stdio.h>
main()
{
    ......
}
func1()
{
    ......
}
int x=8;
func2()
{
    .........
}
```

现在 x 在 main() 和 func1() 之后定义，因此这两个函数不能使用它，它只能用于函数 func2()。假如我们想在函数 main() 中使用这个变量，那么可以在该函数中放置一个声明，如下所示：

```
#include<stdio.h>
main()
{
    extern int x;
    ......
}
func1()
{
    ......
}
int x=8;
func2( )
{
..........
}
```

现在 x 将对函数 func2( ) 和 main( ) 可用。

到目前为止，我们都是把程序写在一个文件中。当程序很大时，它会被写在不同的文件中，这些文件被分别编译，之后链接在一起形成可执行程序。现在我们来考虑一个多文件程序，它写在三个文件中，即 first.c、second.c 和 third.c。

![](img/a76c706396af8b310f291a5313a27079_456_0.png)

在 first.c 文件中，定义并初始化了一个外部变量 x。该变量既可以在 main( ) 和 func1( ) 中使用，但其他文件无法访问它。假如 second.c 文件想要访问这个变量，那么我们可以在这个文件中放置声明，如下所示：

![](img/a76c706396af8b310f291a5313a27079_456_1.png)

现在，这个变量可以在文件 first.c 和 second.c 中被访问和修改，对它所做的一切更改在两个文件中都是可见的。如果 second.c 文件中只有一个函数需要这个变量，那么 extern 声明可以放在该函数内部。因此，使用 extern 关键字声明外部变量可以用来扩展该变量的作用域。

假设我们的程序由许多文件组成，并且在文件 first.c 中定义了许多可能也被其他文件需要的变量。我们可以在每个需要它的文件中为每个变量放置一个 extern 声明。另一种更好、更实用的方法是将所有 extern 声明集中放到一个头文件中，然后在需要访问这些变量的文件中包含该头文件。

## 14.2.3 静态（static）

静态变量有两种类型：

- (1) 局部静态变量
- (2) 全局静态变量

### 14.2.3.1 局部静态变量

局部静态变量的作用域与自动变量相同，即只能在定义它的函数或块内部使用。静态变量的生命周期比自动变量更长。静态变量在编译时创建，并在程序结束时才消亡。它不会在每次控制进入函数/块时被创建和销毁。因此，静态变量只被创建一次，其值在函数调用之间得以保留。如果它被初始化了，那么初始化值只在创建时放入一次，而不会在每次调用函数时都进行初始化。

静态变量只能用常量或常量表达式初始化。与自动变量不同，我们不能使用先前已初始化变量的值来初始化静态变量。如果静态变量没有被显式初始化，那么默认情况下它的初始值为零。

```c
int x = 8;
int y = x; /*Valid*/
static int z = x; /*Invalid, initializer should be constant*/
```

让我们用一个程序来理解局部静态变量的用法。该程序与 P14.2 类似，但这里 x 和 y 被声明为静态变量。

```c
/*P14.5 Program to understand the use of local static variables*/
#include<stdio.h>
main()
{
func();
func();
func();
}
func()
{
static int x=2,y=5;
printf("x=%d,y=%d\n",x,y);
x++; y++;
}
```

**输出：**
x = 2, y = 5
x = 3, y = 6
x = 4, y = 7

注意，初始化的效果只在第一次调用时体现。在后续调用中不执行初始化，变量 x 和 y 中保存的是上一次函数调用留下的值。下一个程序也说明了局部静态变量的用法。

```c
/*P14.6 Program to understand the use of local static variable */
#include<stdio.h>
main()
{
    int n,i;
    printf("Enter a number :");
    scanf("%d",&n);
    for(i=1;i<=10;i++)
        func(n);
    printf("\n");
}
func(int n)
{
    static int step; /* Automatically initialized to 0 */
    step=step+n;
    printf("%d\t",step);
}
```

**输出：**
输入数字：4
4   8   12   16   20   24   28   32   36   40

下一个程序使用递归函数求一个数的各位数字之和。函数 sumd() 内部的变量 sum 应声明为 static。

```c
/*P14.7 Program to find out the sum of digits of a number recursively*/
#include<stdio.h>
int sumd(int num);
main()
{
    int num;
    printf("Enter a number : ");
    scanf("%d",&num);
    printf("Sum of digits of %d is %d\n",num,sumd(num));
}
int sumd(int num)
{
    static int sum=0;
    if(num>0)
    {
        sum=sum+(num%10);
        sumd(num/10);
    }
    return sum;
}
```

### 14.2.3.2 全局静态变量

如果局部变量被声明为 static，那么它在整个程序运行期间都保持存活。对于全局变量而言，static 限定符不是用来延长生命周期的，因为全局变量的生命周期已经与程序的生命周期相同。这里，static 限定符用于信息隐藏。如果外部变量被定义为 static，那么程序中的其他文件就无法使用它。因此，我们可以通过将外部变量声明为 static，使其成为某个文件私有的变量。

```
first.c
int x = 8;
static int y =10;
main()
{
.......
}
func1()
{
..........
}
```

```
second.c
extern int x;
func2()
{
..........
}
func3()
{
..........
}
```

```
third.c
func4()
{
..........
}
func5()
{
..........
}
```

这里，变量 y 被定义为静态外部变量，因此它只能在文件 first.c 中使用。我们不能通过在其他文件中为它放置 extern 声明来使用它。

## 14.2.4 寄存器存储类

register 存储类只能应用于局部变量。寄存器变量的作用域、生命周期和初始值与自动变量相同。两者之间唯一的区别在于它们存储的位置。自动变量存储在内存中，而寄存器变量存储在 CPU 寄存器中。寄存器是处理器中的小型存储单元。存储在寄存器中的变量比存储在内存中的变量访问速度快得多。因此，对于频繁使用的变量，可以赋予 register 存储类以加快处理速度。例如，用作循环计数器的变量可以声明为寄存器变量，因为它们经常被使用。

```c
/*P14.8 Program to understand the use of register variable*/
#include<stdio.h>
main()
{
    register int i;
    for(i=0;i<20000;i++)
    printf("%d\n",i);
}
```

寄存器变量没有内存地址，因此我们不能对它们使用地址运算符（&）。处理器中的寄存器数量有限，因此我们只能将少数几个变量声明为 register。如果许多变量都被声明为 register，而 CPU 寄存器又不可用，则编译器会将它们视为自动变量。

CPU 寄存器通常为 16 位，因此我们只能为 int、char 或指针类型指定 register 存储类。如果声明为 register 变量的类型不是这些类型，编译器会将其视为自动变量。

register 存储类说明符可以应用于函数的形参，而其他三种存储类说明符不能这样使用。
