
```cpp
using namespace std;

template<class T> // 模板前缀

T abs(T value)      // 头部行

{

    T absnum; // 变量声明
    if (value < 0)
        absnum = -value;
    else
        absnum = value;
    return absnum;

}

int main() {
    int num1 = -4;
    float num2 = -4.23f;
    double num3 = -4.23456;
    cout << "The absolute value of " << num1 << endl;
    cout << " is " << abs(num1) << endl;
    cout << "The absolute value of " << num2 << endl;
    cout << " is " << abs(num2) << endl;
    cout << "The absolute value of " << num3 << endl;
    return 0;
}
```

在 `main()` 中进行的第一次调用 `abs(0)` 中，传递了一个整数值作为参数。在这种情况下，编译器用 `int` 数据类型替换函数模板中的 `T` 数据类型，创建了以下函数：

```cpp
int abs(int value) // 头部行
{
    int absnum; // 变量声明
    if (value < 0)
        absnum = -value;
    else
        absnum = value;
    return absnum;
}
```

# 第 6 章
311
## 函数和参数声明

同样，在第二次和第三次函数调用中，编译器创建了两个函数：一个是将数据类型 `T` 替换为关键字 `float` 的函数，另一个是将类型 `T` 替换为关键字 `double` 的函数。这是程序 6.4 的输出：

```
The absolute value of -4 is 4
The absolute value of -4.23 is 4.23
The absolute value of -4.23456 is 4.23456
```

使用函数模板的价值在于，定义了一个函数来创建不同的函数，每个函数都使用相同的逻辑和操作，但作用于不同的类型。

最后，程序 6.3 和 6.4 均使用单个占位符类型定义模板，但也可以定义包含多个数据类型的函数模板。例如，模板前缀

```cpp
template <class DTYPE1, class DTYPE2, class DTYPE3>
```

可以用于创建一个需要三个不同类型的函数。与之前一样，在函数模板的头和体中，数据类型 `DTYPE1`、`DTYPE2` 和 `DTYPE3` 的使用方式与任何内置数据类型（如 `int`、`float` 和 `double`）相同。此外，如之前所述，名称 `DTYPE1`、`DTYPE2` 和 `DTYPE3` 可以是任何非关键字标识符。
惯例，使用字母 `T` 后跟零或多个数字，例如 `T`、`T1`、`T2`、`T3` 等。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_330_0.png)

# 练习题 6.1

- 1. （练习）对于以下函数头，确定必须传递给函数的值的数量、类型和顺序（序列）：
  a. `void factorial(int n)`
  b. `void volts(int res, double induct, double cap)`
  c. `void power(int type, double induct, double cap)`
  d. `double flag(char type, double current, double time)`
  e. `void total(double amount, double c, char d, double e)`
  f. `void flag(int a, int b)`
  g. `getVal(int a, int b)`

- 2. （练习）编写一个名为 `checked()` 的函数，接受三个参数。第一个参数接受一个整数，第二个和第三个参数接受 `double`。注意：错误通常不在于函数的功能，而在于接收的数据。

# 312 使用函数的模块化

- 3. （练习）a. 写一个名为 `findAbs()` 的函数，接受一个双精度数，计算其绝对值并显示。如果数字为负，则显示该数。

- 4. （练习）a. 写一个名为 `mult()` 的函数，接受两个浮点数，将它们相乘并显示结果。

- 5. （练习）a. 写一个名为 `sqrt()` 的函数，计算传递给它的平方并显示结果。该函数能够处理带小数点的数字。

- 6. （练习）a. 写一个名为 `powFun()` 的函数，将整数进行整数幂并显示结果。正整数作为第二个值，使用长整数类型存储结果以确保有足够的空间。

- 7. （数值）a. 写一个 C++ 程序，计算并显示用户输入数字的小数。例如，如果输入 256.879，则应显示 0.879（提示：使用 `int` 转换）。

- 8. （数值）a. 写一个 C++ 程序，接受一个整数并判断该整数是偶数还是奇数（提示：使用 `%` 运算符）。

- 9. （练习）a. 写一个函数，生成 1 到 10 的数字、平方及其立方方的表格。该函数产生的显示与练习 5.11 相同。

- 10. （修改）a. 修改练习 9a 中的函数，接受表格的起始值、要显示的值以及值之间的增量。如果没有发送增量，函数应使用默认值 1。将你的函数命名为 `selTab(6,5,2)`；它应该产生一个五行的表格，第一行从数字 6 开始，后续每个数字递增 2。

11. (数值题) 可以构造一个无参数的实用函数，用于返回一个 $\pi$ 的值，其精度可达到你的计算机允许的最大小数位数。该值通过通过取 1.0 的反正弦（即 $\pi/2$）并将其结果乘以 2 来得到。在 C++ 中，所需的表达式是 $2.0 * asin(1.0)$；`asin()` 函数由标准 C++ 数学库提供。（记住在你的预处理器指令中包含 `cmath`）。使用此表达式，编写一个名为 $pi()$ 的 C++ 函数来计算并显示 $\pi$ 的值。（在下一节中，你将看到如何将此值返回给调用者函数。）

12. (练习题) a. 编写一个函数模板 `display()`，当函数被调用时，返回传递给它的单个参数的值。

- 将练习 12a 中创建的函数模板包含在一个完整的 C++ 程序中，该程序调用该函数三次：一次使用字符参数，一次使用整数参数，一次使用双精度参数。

13. (数值题) a. 编写一个名为 `hole()` 的函数模板，当函数被调用时，返回传递给它的任何参数的值。

- 将练习 13a 中创建的函数模板包含在一个完整的 C++ 程序中，该程序调用该函数三次：一次使用字符参数，一次使用整数参数，一次使用双精度参数。

14. (数值题) a. 编写一个名为 `maximum()` 的函数模板，当函数被调用时，返回传递给函数的三个参数的最大值。假设所有三个参数都是相同的数据类型。

- 将练习 14a 中创建的函数模板包含在一个完整的 C++ 程序中，该程序先用三个整数调用该函数，然后用双精度数调用它。

15. (数值题) a. 编写一个名为 `square()` 的函数模板，当函数被调用时，计算并返回传递给函数的单个参数的平方。

- 将练习 15a 中创建的函数模板包含在一个完整的 C++ 程序中。

## 6.2 返回单个值

使用上一节解释的向函数传递数据的方法，被调用的函数只接收调用时参数中所包含值的副本。（如果不清楚，请复习图 6.3。）当一个值传递给被调用的函数时，传递的过程被称为**按值传递**（passed by value），这是 C++ 的一个显著优势。调用函数无法直接访问调用函数的参数所使用的变量，它不会无意中更改这些变量之一存储的值。

接收按值传递参数的函数可以按照自己的方式发送它想要的值，并直接向调用函数返回一个、且仅一个“合法”的值（见图 6.6）。在本节中，你将看到如何将此值返回给调用函数。正如你所预料的，考虑到 C++ 的灵活性，有一种返回多于一个值的方法，但那是下一节的主题。

函数可以接收多个值

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_333_0.png)

与调用函数一样，直接返回一个值需要正确处理调用函数和被调用函数之间的接口。从返回事务的一侧来看，被调用的函数必须提供以下项目：

- 返回值的数据类型
- 实际的返回值

返回值的函数必须在头头中指定要返回的值的数据类型。记得函数头头包含了函数名和参数列表。例如，之前编写的 `findMax()` 函数确定了传递给它的两个数字的最大值。为了方便起见，再次列出 `findMax()` 的代码：

```cpp
void findMax(int x, int y)
// 函数体开始
int maxnum; // 变量声明
if (x > y)
    maxnum = x;
else
    maxnum = y;
cout << "最大值是 " << maxnum << endl;
return; // 函数体结束
```

# 第 6 章 317

## 返回单个值

# 程序 6.5

```cpp
#include <iostream>
using namespace std;
int findMax(int, int); // 函数原型
int main() {
    int firstnumber, secnum, max;
    cout << "\nenter a number: ";
    cin >> firstnumber;
    cout << "nGreat! Please enter a second number: ";
    cin >> secnum;
    max = findMax(firstnumber, secnum); // 在此处调用函数
    cout << "\nThe两个数的最大值是 " << max << endl;
    return 0;
}
int findMax(int x, int y) { // 函数体开始
    int maxnum; // 变量声明
    if (x >= y) // 寻找最大数
        maxnum = x;
    else
        maxnum = y;
    return maxnum; // 返回语句
}
```

在回顾程序 6.5 时，请注意本节引入的项目。首先，`findMax()` 的原型是一个以分号结尾的语句，正如所有声明一样；它通知 `main()` 以及任何后续使用 `findMax()` 的函数 `findMax()` 返回的数据类型。其次，`main()` 中使用赋值语句将 `findMax()` 用的返回值存储在变量 `max` 中。在程序 6.5 中，`max` 在 `main()` 的变量中正确声明为整数，以便与返回值的数据类型匹配。

第三和第四项涉及 `findMax()` 函数的编码：`findMax()` 的第一行声明该函数返回一个整数值，并且返回语句的计算结果为匹配的数据类型。因此，`findMax()` 在内部

# 318 使用函数的模块化

一致地向 `main()` 返回一个整数值，且 `main()` 已收到可以接收并使用返回的整数。
在编写函数时，请务必记住这四项。另一个例子，请看你是否能在程序 6.6 中识别出这四项。

# 程序 6.6

```cpp
#include <iostream>
using namespace std;
double tempvert(double); // 函数原型
int main()
{
    const int CONVERTS = 4; // 要进行的转换次数
    int count;
    double fahr;
    for(count = 1; count <= CONVERTS; count++)
    {
        cout << "\nEnter Fahrenheit temperature: ";
        cin >> fahr;
        cout << "对应的摄氏度度是 " << tempvert(fahr) << endl;
    }
    return 0;
}
```

```cpp
// 将华氏转换为摄氏
double tempvert(double intTemp)
{
    return (5.0/9.0) * (intTemp - 32.0);
}
```

在回顾程序 6.6 时，首先分析 `tempvert()` 函数。该函数的定义从函数头开始，以返回语句后的右大括号结束。该函数被声明为 `double`，意味着函数返回语句中的表达式必须计算为双精度数，而它确实是这样。由于函数头不是语句而是定义函数的代码开头，因此它不以分号结尾。

在接收端，`main()` 拥有 `tempvert()` 函数的原型，该原型与 `tempvert()` 的函数定义一致。`main()` 中没有声明任何变量来存储

# 第 6 章 返回单个值

来自 `tempvert()` 的返回值，因为该返回值被立即传递给 `cout` 进行显示。

最后，声明的用途之一（如第 2 章所学）是通知计算机为数据预留的内部存储空间。`tempvert()` 的原型执行了这项任务，并通知编译器返回值所需的存储类型。由于 `main()` 总是程序中的第一个函数，你必须为 `main()` 调用的所有函数以及后续函数包含函数原型。

# 内联函数¹¹

调用函数会给计算机带来一定的开销。这种开销由以下步骤组成：

- 1. 将值放入函数可以访问的预留内存区域（栈）中
- 2. 将控制权交给函数
- 3. 为任何返回值提供预留的内存位置（再次使用栈来实现此目的）
- 4. 返回到调用程序中的正确点

当函数被调用多次时，支付这种开销是合理的，因为可以大幅缩小程序体积。与其在每次需要时都编写相同的代码，不如只写一次，并在需要时调用。
然而，对于调用次数不频繁的小函数，传递和返回值的开销可能并不值得。通过将代码行分组在一个公共函数名下，并让编译器在调用函数时将这些代码放入程序中，**内联函数**提供了这种能力。

# 320 使用函数的模块化

# 程序 6.7

```cpp
#include <iostream>
using namespace std;
inline double tempvert(double inTemp) // 一个内联函数
{
    return (5.0/9.0) * (inTemp - 32.0);
}
int main() {
    const int CONVERTS = 4; // 要进行的转换次数
    int count;
    double fahr;
    for(count = 1; count <= CONVERTS; count++) {
        cout << "*输入华氏度温度: ";
        cin >> fahr;
        cout << "对应的摄氏度度是 " << tempvert(fahr) << endl;
    }
    return 0;
}
```
