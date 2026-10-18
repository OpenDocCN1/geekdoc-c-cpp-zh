
然而，文件开头并不总是放置下面这一行的最佳位置：

    using namespace std;

我们最终将使用的命名空间不止 std 一个。实际上，我们可能会在不同的函数定义中使用不同的命名空间。如果你将这条指令

    using namespace std;

放在函数定义体的起始花括号 { 内，那么该 using 指令只适用于这个函数定义。这样，你就可以在两个不同的函数定义中使用两个不同的命名空间，即使这两个函数定义位于同一个文件中，即使这两个命名空间中存在某些名称在两个命名空间中含义不同。

把 using 指令放到函数定义内部，类似于把变量声明放到函数定义内部。如果你在函数定义内部放置一个变量定义，该变量就是函数的局部变量；也就是说，变量声明的含义仅限于该函数定义。如果你把 using 指令放到函数定义内部，该 using 指令就是该函数定义的局部指令；换句话说，using 指令的含义仅限于该函数定义。

我们需要过一段时间才会在 using 指令中使用 std 以外的命名空间，但从现在开始就把这些 using 指令放在它们该放的位置，不失为一种良好的实践。在程序清单4.15中，我们重写了程序清单4.12中的程序，并把 using 指令放在它们应处的位置。程序清单4.15中的程序运行行为与程序清单4.12中的程序完全相同。在这个特定例子中，差别仅仅在于风格；但当你开始使用更多命名空间时，这种差别将影响程序的运行效果。

## 程序清单4.15 使用命名空间（第1部分，共2部分）

```
//Computes the area of a circle and the volume of a sphere.
//Uses the same radius for both calculations.
#include <iostream>
#include <cmath>

const double PI = 3.14159;

double area(double radius);
//Returns the area of a circle with the specified radius.

double volume(double radius);
//Returns the volume of a sphere with the specified radius.
```

（续）

## 程序清单4.15 使用命名空间（第2部分，共2部分）

```
13
14 int main( )
15 {
16     using namespace std;
17
18     double radiusOfBoth, areaOfCircle, volumeOfSphere;
19
20     cout << "Enter a radius to use for both a circle\n"
21         << "and a sphere (in inches): ";
22     cin >> radiusOfBoth;
23
24     areaOfCircle = area(radiusOfBoth);
25     volumeOfSphere = volume(radiusOfBoth);
26
27     cout << "Radius = " << radiusOfBoth << " inches\n"
28         << "Area of circle = " << areaOfCircle
29         << " square inches\n"
30         << "Volume of sphere = " << volumeOfSphere
31         << " cubic inches\n";
32
33     return 0;
34 }
35
36
37 double area(double radius)
38 {
39     using namespace std;
40
41     return (PI * pow(radius, 2));
42 }
43
44 double volume(double radius)
45 {
46     using namespace std;
47
48     return ((4.0/3.0) * PI * pow(radius, 3));
49 }
```

该程序的示例对话与程序清单4.12中程序的示例对话相同。

## 自测练习题

20. 如果在函数定义中使用变量，你应该在何处声明该变量？在函数定义中？在程序的主函数中？任何方便的地方都可以吗？

## 程序清单4.16 阶乘函数

### 函数声明

```
1    int factorial(int n);
2    //Returns factorial of n.
3    //The argument n should be nonnegative.
```

### 函数定义

```
1    int factorial(int n)
2    {
3        int product = 1;
4        while (n > 0)
5        {
6            product = n * product;
7            n--;
8        }
9
10       return product;
11   }
```

形参 n 被用作局部变量

factorial 的函数定义使用了两个局部变量：在函数体开始处声明的 product，以及形参 n。由于形参也是局部变量，我们可以改变它的值。在这个例子中，我们使用自减运算符 n-- 来改变形参 n 的值。（自减运算符已在第2章讨论过。）

每次执行循环体时，变量 product 的值会乘以 n 的值，然后通过 n-- 使 n 的值减一。如果以 3 作为实参调用 factorial 函数，那么第一次执行循环体时 product 的值为 3，第二次执行循环体时 product 的值为 3 * 2，第三次执行循环体时 product 的值为 3 * 2 * 1，然后 while 循环结束。因此，下面这条语句会把变量 x 设置为 6，也就是 3 * 2 * 1：

```
x = factorial(3);
```

注意，局部变量 product 在声明时被初始化为 1。（这种在声明变量时进行初始化的方式已在第2章介绍过。）很容易看出 1 是变量 product 的正确初值。要理解这就是 product 的正确初值，请注意：当 while 循环体第一次执行完毕后，我们希望 product 的值等于形参 n 的（原始）值；如果 product 初始化为 1，那么结果正是如此。

形参用作局部变量

这种做法是可行的，而且在许多编程语言中，你不得不这样做。幸运的是，C++ 提供了一种更优雅的解决方案。在 C++ 中，你可以直接对两个函数使用同一个函数名 ave，并用下面的函数定义来代替函数定义 ave3：

```
double ave(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```

## 程序清单4.17 重载函数名

```
//Illustrates overloading the function name ave.
#include <iostream>

double ave(double n1, double n2);
//Returns the average of the two numbers n1 and n2.

double ave(double n1, double n2, double n3);
//Returns the average of the three numbers n1, n2, and n3.

int main()
{
    using namespace std;
    cout << "The average of 2.0, 2.5, and 3.0 is "
         << ave(2.0, 2.5, 3.0) << endl;

    cout << "The average of 4.5 and 5.5 is "
         << ave(4.5, 5.5) << endl;

    return 0;
}

double ave(double n1, double n2)
{
    return ((n1 + n2)/2.0);
}

double ave(double n1, double n2, double n3)
{
    return ((n1 + n2 + n3)/3.0);
}
```

### 输出

```
The average of 2.0, 2.5, and 3.0 is 2.50000
The average of 4.5 and 5.5 is 5.00000
```

函数名 ave 现在有两个定义。这就是重载的一个例子。在这种情况下，我们重载了函数名 ave。在程序清单4.17中，我们将 ave 的这两个函数定义嵌入到一个完整的示例程序中。请务必注意，每个函数定义都有自己的函数声明。

重载是个很棒的想法。它让程序更易于阅读，也让你不必因为已经在某个函数定义中使用了最自然的名称，而绞尽脑汁为另一个函数另起新名。但是，当编译器遇到对某个具有两个或更多定义的函数名的调用时，它怎么知道该使用哪个函数定义呢？编译器无法读懂程序员的想法。为了判断应使用哪个函数定义，编译器会检查函数调用中实参的个数以及实参的类型。在程序清单4.17的程序中，对 ave 的一次调用有两个实参，另一次调用有三个实参。为了判断使用哪个定义，编译器只需计算函数调用中实参的个数：如果有两个实参，就使用第一个定义；如果有三个实参，就使用第二个定义。

确定适用哪个定义

每当你为同一个函数名给出两个或更多定义时，各种函数定义必须具有不同的参数规格；也就是说，任何两个具有相同函数名的函数定义，必须使用不同数量的形参，或者使用不同类型的形参（或者两者都不同）。注意，当你重载一个函数名时，两个不同定义的函数声明在形参上必须不同。你不能通过给出两个仅在返回值类型上不同的定义来重载一个函数名。

### 重载函数名

如果同一个函数名有两个或更多的函数定义，就称为重载。当你重载一个函数名时，这些函数定义必须具有不同数量的形参，或者某些形参的类型不同。当出现函数调用时，编译器会使用其形参数量和形参类型与函数调用中的实参相匹配的那个函数定义。

重载对你来说其实并不陌生。在第2章中，你已经见过除法运算符 / 的一种重载。如果两个操作数都是 int 类型，例如 13/2，那么返回值是整数除法的结果，此时为 6。另一方面，如果其中一个或两个操作数是 double 类型，那么返回值是普通除法的结果；例如，13/2.0 返回的值为 6.5。除法运算符 / 有两个定义，而这两个定义的区别并不在于操作数的数量不同，
