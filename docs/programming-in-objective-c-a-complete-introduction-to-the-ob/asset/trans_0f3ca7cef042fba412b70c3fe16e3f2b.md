
剩余的值被设置为 0。请注意，在这种情况下，需要内层的大括号来强制进行正确的初始化。如果没有它们，将会初始化前两行和第三行的前两个元素。（你可以亲自验证一下是否确实如此。）

## Functions

`NSLog` 例程程序是一个你在每个程序中都使用过的函数示例。事实上，每个程序都使用过一个名为 `main` 的函数。让我们回到你写的第一个程序（程序 2.1），它在终端上显示了“Programming is fun.”这一短语：

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[])
{
    AutoreleasePool *pool = [[AutoreleasePool alloc] init];

    NSLog("@Programming is fun.");
    [pool drain];
    return 0;
}
```

这个名为 `printMessage` 的函数产生相同的输出：

```c
void printMessage(void)
{
    NSLog("@Programming is fun.");
}
```

- 谁可以调用它
- 它返回值的类型
- 它的名称
- 它告诉编译器的参数个数和类型

`printMessage` 函数定义的第一行告诉编译器，`printMessage` 是函数的名称，并且它没有返回值（关键字 `void` 的首次使用）。与方法不同，你不需要将函数的返回类型放在括号内。事实上，如果你这样做这样做，将会得到编译器错误信息。

在告诉编译器 `printMessage` 不返回结果后，`void` 关键字的第二次使用表示它不接受任何参数。

记住，`main` 是 Objective-C 系统中一个特殊识别的名称，它始终指示程序开始执行的地方。总会有一个 `main`。因此，你可以向前面的代码添加一个 `main` 函数，以得到一个完整的程序，如程序 13.3 所示。

## Program 13.3

```c
#import <Foundation/Foundation.h>

void printMessage(void)
{
    NSLog("@Programming is fun.");
}

int main (int argc, char *argv[])
{
    AutoreleasePool *pool = [[AutoreleasePool alloc] init];

    printMessage();
    [pool drain];
    return 0;
}
```

## Program 13.3 Output

Programming is fun.

程序 13.3 包含两个函数：`printMessage` 和 `main`。如前所述，调用函数的思想并不新。由于 `printMessage` 接受参数，你只需通过列出它的名称后跟一对开闭括号来调用它。

## Arguments and Local Variables

在第 5 章“程序循环”中，你编写了计算三角形数的程序。在这里，你定义了一个函数来生成三角形数并调用它，恰好命名为 `calculateTriangularNumber`。作为函数的参数，你指定了要计算哪一个三角形数。该函数计算所需的数字并显示结果。程序 13.4 显示了完成任务的函数以及尝试它的 `main` 例程。

## Program 13.4

```c
#import <Foundation/Foundation.h>
```

```c
// 计算第 n 个三角形数的函数
void calculateTriangularNumber(int n)
{
    int i, triangularNumber = 0;

    for (i = 1; i <= n; ++i)
        triangularNumber += i;

    NSLog(@"Triangular number %d is %d", n, triangularNumber);
}
```

## Chapter 13 Underlying Language Features

```c
int main (int argc, char *argv[])
{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];

  calculateTriangularNumber (10);
  calculateTriangularNumber (20);
  calculateTriangularNumber (50);

    [pool drain];
  return 0;
}
```

## Program 13.4 Output

Triangular number 10 is 55
Triangular number 20 is 210
Triangular number 50 is 1275

`calculateTriangularNumber` 函数的第一行是：
`void calculateTriangularNumber(int n)`

它告诉编译器 `calculateTriangularNumber` 是一个不返回值的函数（关键字 `void`），并且它接受一个名为 `n` 的单参数，该参数类型为 `int`。注意，你不能将参数类型放在括号内，就像你在编写方法时习惯这样做的那样。

左大括号表示函数定义的开始。由于你想计算第 n 个三角形数，你必须设置一个变量来存储计算过程中三角形数的值。你还需要一个变量作为你的循环索引。变量 `TriangularNumber` 和 `i` 是为了这些目的定义的，并声明为 `int` 类型。你定义和初始化这些变量的方式与你在之前的程序在 `main` 例程中定义和初始化变量的方式相同。

局部变量的行为与在方法中的相同：如果给函数内部的变量赋了一个初始值，那么每次调用函数时，该初始值都会赋值给该变量。

在函数内部定义的变量（如方法中所示）被称为**自动局部变量**（automatic local variables），因为它们在每次调用函数时都会自动被“创建”，并且它们的值对于函数是局部的。

**静态变量**使用 `static` 关键字声明，它们在函数调用之间保留其值，并具有 0 的默认初始值。

局部变量的值只能由定义该变量的函数访问。它的值无法从函数外部直接访问。

回到我们的程序示例，在定义局部变量后，函数计算三角形数并在终端显示结果。右大括号随后定义了函数的结束。

## Functions 257

在 `main` 例程内部，值 10 作为参数传递给第一次调用 `calculateTriangularNumber` 的地方。执行直接跳转到该函数，值 10 变为函数内部形式参数 `n` 的值。

下一次调用 `calculateTriangularNumber` 时，传递了参数 20。在之前描述的类似过程中，该值变为函数内部 `n` 的值。该函数随后计算第 20 个三角形数的值并显示答案。

## Returning Function Results

与方法一样，函数可以返回一个值。使用 `return` 语句返回的值类型必须与为函数声明的返回类型一致。如下所示的函数声明：

```c
float km_to_mph (float km_speed)
```

开始了函数 `km_to_mph` 的定义，它接受一个名为 `km_speed` 的 `float` 类型参数。

同样，

```c
int gcd (int u, int v)
```

定义了一个带有整数 `u` 和 `v` 的函数 `gcd` 并返回一个整数。让我们把程序 5.7 中使用的公约数算法重写为函数形式。

## Program 13.5

```c
#import <Foundation/Foundation.h>

// 此函数找到两个数字的
// 公约数并返回结果
int gcd (int u, int v) {
    int temp;
    while ( v != 0 ) {
        temp = u % v;
        u = v;
        v = temp;
    }
    return u;
}

main () {
    NSAutoreleasePool * pool = [[AutoreleasePool alloc] init];
    int result;

    result = gcd (150, 35);
    NSLog(@"The gcd of 150 and 35 is %i", result);

    result = gcd (1026, 405);
    NSLog(@"The gcd of 1026 and 405 is %i", result);

    result = gcd (83, 240);
    NSLog(@"The gcd of 83 and 240 is %i", result);

    [pool drain];
    return 0;
}
```

## Program 13.5 Output

The gcd of 150 and 35 is 5
The gcd of 1026 and 405 is 27
The gcd of 83 and 240 is 1

## Declaring Return Types and Argument Types

我们之前提到过，Objective-C 编译器假设函数返回一个 `int` 类型的值。更具体地说，每当调用一个函数时，除非发生了以下两种情况之一，否则编译器假设该函数返回一个 `int` 类型的值：

