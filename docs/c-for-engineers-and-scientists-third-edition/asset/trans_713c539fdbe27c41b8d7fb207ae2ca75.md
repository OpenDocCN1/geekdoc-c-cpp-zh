

# 第 6 章 317

返回单个值

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
（注：程序 6.7 的 OCR 文本包含若干错误，例如用 `CONST` 代替 `const int` 以及 `tempvert(fahrn)`，这些已修正。）

使用内联函数的优点是执行速度。因为函数在每次调用时都会复制并包含，所以不会浪费时间。然而，缺点是程序体积增大。内联函数应仅用于被频繁调的小函数。

# 340

# 第 6 章 321

返回单个值

![img/2a849fc7bc04aa2669e22b_340_0.png]

# 练习题 6.2

1. （修改）重写程序 6.5，使 `findMax` 接受双精度参数并返回双精度值。使 `main()` 传递双精度值并接受 `findMax()` 返回的值。

2. （练习）对于以下函数头，确定应传递给函数的值的个数、类型和顺序，以及函数的返回类型：
- int factorial(int n)
- double volts(int induct, double cap)
- double power(int induct, double cap)
- char flag(char type, float time)
- float total(float amount, float rate)
- float roi(int a, int b, char c, char d, float e, float f)
- void getVal(int item, int iter, char def, char delim)

3. （练习）为以下编写函数头：
- 名为 `check()` 的函数具有三个参数。第一个参数接受整数，第二个和第三个参数接受双精度数。函数不返回值。
- 名为 `findAbs()` 的函数接受传递的双精度数，并返回其绝对值。
- 名为 `mult()` 的函数接受浮点数作为参数，将它们相乘并返回结果。
- 名为 `sqrtIT()` 的函数计算并返回传递的整数值的平方。
- 名为 `powfun()` 的函数接受传递的整数（作为参数），并以整数形式返回结果。
- 生成 1 到 10 数字及其平方、立方方的函数。立方方命名传递给函数，函数不返回值。

4. （通用数学）编写一个函数 `rightTriangle()`，接受直角形的两边长度作为参数 a 和 b。该子程序应确定并返回三角形的斜边 c。
b. 将练习 4a 中的函数包含在一个运行程序中。该函数应正确调用 `rightTriangle()` 并显示函数值。

5. （通用数学）编写一个 C++ 函数 `findAbs()`，它接受传递的双精度数，计算其绝对值，并将绝对值返回给调用函数。

