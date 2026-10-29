

# 程序 6.14

```
#include <iostream>
using namespace std;
void teststat();  // 函数原型
int main()
{
    int count;          // count 是一个局部自动变量
    for(count = 1; count <= 3; count++)
        teststat();
    return 0;
}

void teststat()
{
    static int num = 0;  // num 是一个局部静态变量
    cout << "The value of the static variable num is now "
         << num << endl;
    num++;
    return;
}
```

这是程序 6.14 产生的输出：

```
The value of the static variable num is now 0
The value of the static variable num is now 1
The value of the static variable num is now 2
```

正如这个输出所示，静态变量 num 仅被设置为 0 一次。然后 teststat() 函数在将控制权返回给 main() 之前递增这个变量。当离开 teststat() 函数时 num 所拥有的值会被保留，并在下次调用该函数时显示出来。

与自动变量不同——自动变量可以用常量或同时使用常量和先前已初始化变量的表达式来初始化——静态变量只能使用常量或常量表达式（如 3.2 + 8.0）来初始化。此外，与自动变量不同，当没有给出显式初始化时，所有静态变量都会被设置为 0。因此，程序 6.14 中将 num 初始化为 0 并不是必需的。

局部变量可用的剩余存储类别 register 不像 auto 或 static 变量那样被广泛使用。以下是 register 变量声明的示例：

```
register int time;
register double diffren;
register float coupon;
```

register 变量与 auto 变量具有相同的持续时间；也就是说，局部 register 变量在声明它的函数被进入时创建，在函数执行完毕时销毁。register 变量与 auto 变量之间唯一的区别在于变量存储的位置。

除 register 变量外，所有变量（局部和全局）的存储空间都保留在计算机的内存中。大多数计算机在 CPU 中还有少量称为寄存器的高速存储区域，也可以用于变量存储。由于寄存器位于 CPU 中，它们比计算机内存中的常规存储区域访问速度更快。此外，引用寄存器的计算机指令通常比引用内存位置的指令占用更少的空间，因为可访问的寄存器数量少于内存位置的数量。当编译器在程序编译期间用寄存器位置替代变量时，指令所需的空间比寻址具有数百万个位置的内存要少。

除了减小编译后 C++ 程序的大小之外，如果你的计算机支持这种数据类型，使用 register 变量还可以提高程序的执行速度。如果你的编译器不支持 register 变量，或者声明的 register 变量超过了计算机的寄存器容量，那么用 register 存储类别声明的变量会自动转换为 auto。然而，打算在不同类型的计算机上运行的应用程序不应使用 register 变量。使用 register 存储类别的唯一限制是，不能使用地址运算符 & 获取 register 变量的地址。当你意识到寄存器没有标准内存地址时，这个概念就更容易理解了。

## 全局变量存储类别

全局变量是通过函数外部的定义语句创建的。就其本质而言，这些外部定义的变量不会随着函数的调用而出现和消失。全局变量一旦创建，就会一直存在，直到声明它的程序运行完毕。因此，全局变量不能声明为在程序运行期间被创建和销毁的 auto 或 register 变量。全局变量可以用 static 或 extern 存储类别声明（但不能同时使用两者）。以下是包含这两种类别描述的声明语句示例：

```
extern int sum;
extern double volts;
static double current;
```

static 和 extern 存储类别只影响全局变量的作用域，而不影响其生命周期。与静态局部变量一样，所有全局变量在编译时都被初始化为 0。extern 存储类别的目的是将全局变量的作用域扩展到其正常边界之外。要理解这个概念，首先要注意到目前为止编写的所有程序都包含在一个文件中。因此，当你保存或检索程序时，只需要给计算机一个程序名称即可。然而，C++ 并不要求这样做。

大型程序通常由存储在多个文件中的许多函数组成。例如，图 6.13 显示了存储在第一个文件中的三个函数 main()、func1() 和 func2()，以及存储在第二个文件中的两个函数 func3() 和 func4()。

## 第 6 章

## 变量存储类别

![](img/202cface8244f523c2641baa2e00d7dd_300_0.png)

## 图 6.13  程序可以扩展到多个文件

对于图 6.13 中显示的文件，在 file1 中声明的全局变量 volts、current 和 power 只能被该文件中的函数 main()、func1() 和 func2() 使用。在 file2 中声明的单个全局变量 factor 只能被 file2 中的函数 func3() 和 func4() 使用。

虽然变量 volts 已在 file1 中创建，但你可能希望在 file2 中使用它。要做到这一点，你需要在 file2 中放置声明语句 extern int volts;，如图 6.14 所示。将此语句放在 file2 的顶部会将 volts 的作用域扩展到 file2 中，以便 func3() 和 func4() 都可以使用它。extern 指定只是声明一个在另一个文件中定义的全局变量。因此，在 func4() 中放置语句 extern double current; 会将这个在 file1 中创建的全局变量的作用域扩展到 func4() 中。此外，在 file2 中创建的全局变量 factor 的作用域通过放置在 func1() 之前的声明语句 extern double factor; 扩展到 func1() 和 func2() 中。请注意，factor 对 main() 不可用。

## 信息要点

## 存储类别

auto 和 register 类型的变量始终是局部变量。只有非静态全局变量才能使用 extern 关键字声明。这样做会将变量的作用域扩展到另一个文件或函数中。

将全局变量设为 static 会使该变量对其声明所在文件保持私有。因此，static 变量不能使用 extern 关键字。除 static 变量外，所有变量在每次进入其作用域时都会被初始化；static 变量仅在定义时初始化一次。

改变它们的值。因此，全局静态变量随后不能通过使用 extern 声明语句扩展到第二个文件。尝试这样做会导致编译错误。

## 练习 6.5

- 1. （练习）a. 列出可用于局部变量的存储类别。
- b. 列出可用于全局变量的存储类别。

- 2. （练习）描述局部 auto 变量和局部 static 变量之间的区别。

- 3. （练习）以下函数之间有什么区别？

```
void init1()
{
    static int yrs = 1;

    cout << "The value of yrs is " << yrs << endl;
    yrs = yrs + 2;

    return;
}
```

```
void init2()
{
    static int yrs;

    yrs = 1;
    cout << "The value of yrs is " << yrs << endl;
    yrs = yrs + 2;

    return;
}
```

- 4. **（练习）**
  - a. 描述全局 `static` 变量和全局 `extern` 变量之间的区别。
  - b. 如果一个变量用 `extern` 存储类别声明，程序中某处还必须存在什么其他声明语句？

- 5. **（练习）** 声明语句 `static double years;` 可用于创建局部或全局静态变量。什么决定了变量 `years` 的作用域？

- 6. **（练习）** 对于图 6.15 中显示的函数和变量声明，放置一个 `extern` 声明以实现以下每一项：
  - a. 将全局变量 `choice` 的作用域扩展到 `file2` 中。
  - b. 仅将全局变量 `flag` 的作用域扩展到 `average()` 函数中。
  - c. 将全局变量 `date` 的作用域扩展到 `average()` 和 `variance()` 中。
  - d. 仅将全局变量 `date` 的作用域扩展到 `roi()` 中。
  - e. 仅将全局变量 `coupon` 的作用域扩展到 `roi()` 中。
  - f. 将全局变量 `bondtype` 的作用域扩展到 `file1` 中。
  - g. 将全局变量 `maturity` 的作用域扩展到 `watts()` 和 `thrust()` 中。

![](img/202cface8244f523c2641baa2e00d7dd_303_0.png)

