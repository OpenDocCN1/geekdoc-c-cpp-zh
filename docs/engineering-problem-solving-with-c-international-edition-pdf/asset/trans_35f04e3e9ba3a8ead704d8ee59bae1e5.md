

请注意，此函数原型需要两个形式参数。因为友元函数不是成员函数，所以没有调用对象。相反，我们必须在函数原型和函数头中将两个操作数都作为形式参数包含在内。以下代码段说明了此函数的用法：

```
Pixel p1, p2(100, 200, 100), p3(10, 20, 30);
p1 = p2 + p3; // Valid.
p1 = p2 + 100; // Valid.
p1 = 100 + p2; // Valid!
```

第三个赋值语句

```
p1 = 100 + p2; // Valid!
```

现在是一个有效语句。整数 100 为 + 函数提供第一个参数，p2 提供第二个参数。由于函数期望 Pixel 对象作为参数，因此使用构造函数将整数 100 提升为 Pixel 对象 (100,100,100)，函数调用成功。该函数的定义如下：

```
/* ........................................................ */
/* Addition (+) operator as friend function. */
/* File name: Pixel.cpp */
/* ........................................................ */
Pixel operator+(Pixel p1, Pixel p2)
{
    Pixel temp;
    temp.red = p1.red + p2.red;
    temp.green = p1.green + p2.green;
    temp.blue = p1.blue + p2.blue;
    return temp;
}
/* ........................................................ */
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_518_0.png)

请注意，关键字 friend 未包含在函数定义中。friend 状态只能在类声明中授予。将此函数定义与成员函数定义进行比较。由于此函数不是成员函数，因此没有调用对象，成员函数定义中对 red、green 和 blue 的引用已在友元函数定义中替换为对 p1.red、p1.green 和 p1.blue 的引用。

## 练习！

假设以下函数原型已添加到 Pixel 类声明中。为每个函数编写函数定义。

- 1. friend Pixel operator*(Pixel p1, Pixel p2);
- 2. friend Pixel operator/(Pixel p1, Pixel p2);
- 3. friend Pixel operator-(Pixel p1, Pixel p2);

## << 运算符

我们的 Pixel 类声明包含一个重载 << 运算符的函数。该函数的原型如下：

```
friend ostream& operator<<(ostream& out, const Pixel& p);
```

此函数定义为带有两个形式参数的友元函数，并且函数返回 ostream 引用。返回 ostream 引用支持链式调用。因此，我们可以在单个输出语句中输出多个表达式，如以下语句所示：

```
cout << p1 << ', ' << p2 << endl;
```

<< 运算符不能定义为 pixel 类的成员函数，因为函数的第一个参数必须是 ostream 引用。但是，该函数需要访问 Pixel 参数的私有数据成员，因此我们将其声明为 Pixel 类的友元函数。为了效率，我们选择将第二个形式参数设为 const 引用传递，而不是值传递。这允许传递引用，但防止修改引用所指向的参数。函数定义如下：

```
/*
 * Output << operator.
 *
 * File name: Pixel.cpp
 *
 */
ostream& operator<<(ostream& out, const Pixel& p)
{
    out << p.red << ',';
    out << p.green << ',';
    out << p.blue;
    return out;
}
/* ---------------------------------------------------------- */
```

函数必须返回 ostream 引用，因此需要语句 return out;。

我们的函数输出 Pixel p 的 red、green 和 blue 值，以空格分隔。我们可以按以下方式使用该函数：

```
Pixel p1, p2(100, 200, 100);
cout << "P1: " << p1 << " P2: " << p2 << endl;
...
```

屏幕上打印的输出为

```
P1: 0 0 0 P2: 100 200 100
```

我们也可以使用我们的 << 函数将输出发送到文件。请回顾，ofstream 类派生自 ostream 类。因此，所有 ostream 操作也可以应用于 ofstream 对象。以下代码段使用我们的 << 函数向文件 pixel.dat 写入数据。

```
...
Pixel p1, p2(255);
ofstream outfile("pixel.dat");
outfile << "P1: " << p1 << " P2: " << p2 << endl;
...
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_519_0.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_519_1.png)

写入文件 pixel.dat 的输出为

```
P1: 0 0 0 P2: 255 255 255
```

请注意，我们的 << 函数在 Pixel 值之后不输出换行符。这允许我们在同一行上输出多个 Pixel 值，并且与为内置数据类型定义的输出运算符的性能一致。

## >> 运算符

我们的 Pixel 类声明包含一个重载 >> 运算符的函数。该函数的原型如下：

```
friend istream& operator>>(istream& in, Pixel& p);
```

此函数定义为带有两个形式参数的友元函数，并且函数返回 istream 引用。>> 运算符不能定义为 Pixel 类的成员函数，因为第一个参数必须是 istream 引用。但是，该函数需要访问 pixel 参数的私有数据成员，因此我们已将该函数声明为 Pixel 类的友元函数。

由于该函数定义用于输入 Pixel 值，因此函数必须修改由形式参数 p 引用的对象。因此，此形式参数必须是引用传递。函数定义如下：

```
/*
 * Input (>>) operator.
 * File name: Pixel.cpp
 */
istream& operator>>(istream& in, Pixel& p)
{
    in >> p.red >> p.green >> p.blue;
    return in;
}
/*----------------------------------------------------------*/
```

此函数必须返回 istream 引用。

重载 >> 运算符与重载 << 运算符类似，只不过输入时遇到错误的潜在可能性更大。该函数尝试输入三个整数值，以分配给 p 的 red、green 和 blue 数据成员。该函数在输入流中查找三个由空格分隔的整数值。输入流中的任何意外字符（例如逗号或冒号）都会使 istream 进入失败状态。

如果我们的 Pixel 类要求输入特定格式，则我们的 >> 函数需要检查所需格式。如果未遇到所需格式，则函数需要将 istream 置于失败状态。为举例说明，假设输入 Pixel 值的格式要求整数值用冒号分隔，如下所示：

```
100:150:100
```

我们的函数可以修改为检查此格式，如果格式不正确，则将 istream 置于失败状态：

```
/*
 * Input (>>) operator.
 *
 * Expected Pixel format is 100;150;100
 *
 * File name: Pixel.cpp
 *
 */
istream& operator>>(istream& in, Pixel& p)
{
    // Declare local objects.
    char ch;

    // Input integer value for red data member.
    in >> p.red;

    // Input colon. If colon not encountered.
    // set error state and return.
    in >> ch;
    if(ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for green data member.
    in >> p.green;

    // Input colon. If colon not encountered.
    // set error state and return.
    in >> ch;
    if(ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for blue data member.
    in >> p.blue;

    return in;
}
/*--------------------------------------------------------------*/
```

在此函数定义中，函数 `setstate()` 用于将 `istream` 置于失败状态。函数 `setstate()` 是 `istream` 类的成员函数。在语句

```
in.setstate(ios::failbit);
```

由 `in` 引用的 `istream` 对象调用 `setstate` 函数，并将 `failbit` 设置为 true。

使用 Pixel 类时的另一个潜在错误是将大于 255 的值赋给一个或多个数据成员。潜在溢出错误的处理将在下一节中讨论。

## 验证对象

请回顾，我们将像素定义为 red、green 和 blue 三元组，其中三元组中的每个值范围为 0 到 255。Pixel 类包含三个类型为 unsigned int 的数据成员（red、green 和 blue）。数据类型 unsigned int 防止出现负值，但不能防止值超过最大值 255。请考虑使用 Pixel 类的以下示例：

```
/* Program chapter10_2 ---------------------------------------*/
/* Driver program for testing Pixel class */
#include "Pixel.h" //Required for Pixel
#include <iostream> //Required for cout
using namespace std;
int main()
{
    //Test constructors
    Pixel defaultP;
    Pixel grayP(100);
    Pixel redP(255, 0, 0);
    //Test output operator
    cout << "Default pixel: " << defaultP << endl;
    cout << "Gray pixel: " << grayP << endl;
    cout << "Red pixel: " << redP << endl;
    //Test arithmetic operators
    defaultP = grayP + redP;
    cout << "After addition, defaultP: " << defaultP << endl;
    return 0;
}
```

该程序的示例运行如下：

```
Ingbers-MacBook-Pro:Programs jaingber$ g++ main.cpp Pixel.cpp
Ingbers-MacBook-Pro:Programs jaingber$ ./a.out
Default pixel: 0 0 0
Gray pixel: 100 100 100
Red pixel: 255 0 0
After addition. defaultP: 355 100 100
```

我们可以看到 defaultP 的 red 值已超过最大值 255。如果 Pixel 对象的任何数据成员超过最大值，则在使用 Pixel 类修改图像时可能会出现意外结果。为处理此情况，我们将遵循前一节中讨论的 istream 类模型。Pixel

