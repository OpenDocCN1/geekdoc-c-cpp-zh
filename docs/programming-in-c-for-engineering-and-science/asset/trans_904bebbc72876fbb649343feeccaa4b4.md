

header 和文档文件，以及由编译实现文件生成的对象文件的访问权限，以便将其内容链接到我们的程序中。实现文件中的细节可以保持“隐藏”，使我们能够使用库而无需关心这些细节。例如，我们在每个程序中都使用了 iostream 库提供的输入/输出操作，而无需关心其实现细节。

## 6.4.5.2 库促进程序维护

程序和库的单独编译使得可以更改库的实现文件并仅重新编译它，而无需更改或重新编译使用该库的程序或其他库。例如，如果库 Heat 的实现文件中的函数 celsiusToFahrenheit() 被更改，则只需重新编译实现文件即可。使用此函数的程序无需重新编译，因为 celsiusToFahrenheit() 的原型未发生变化，只有其定义发生了变化。只需将程序重新链接到库 Heat 的新对象文件即可。

相比之下，如果头文件中的接口被更改，则库的实现文件以及所有在 #include 指令中命名该头文件的程序和其他库都必须重新编译并重新链接。

## 6.4.5.3 库支持独立编码

库通过允许将相关项分组到独立单元中来促进软件设计的模块化，这在大型软件项目中尤其有用。一旦在项目中识别并对所需的对象和操作进行分类，就可以设计库来容纳各种对象类型的项，并为这些库构建头文件。

在此之后，项目的工作可以分给不同的程序员组，分别负责构建各种库的实现文件，以及负责在软件项目中使用库的程序的其他组。将工作划分为可管理的“块”并可并行编码，可以加快整个项目的完成速度。此外，由于一个部分的工作独立于另一部分的工作进行，因此出错的可能性更小。

## 6.4.5.4 库简化测试

单独的库可以由不同的程序员团队独立开发和测试（使用驱动程序）。这意味着每个库可以比单个非常大的程序更彻底（并且更快速）地进行测试。

## 6.4.5.5 库扩展编程语言

库提供可供任何程序（或其他库）使用的项——函数、常量等。程序员不必每次需要这些项时都“重新发明轮子”。

## 6.5 数值方法简介

科学和工程中的问题和数学模型，以及许多其他领域，都涉及求解常微分代数方程、微分方程、方程组等。在许多情况下，使用可由计算机程序实现的数值方法来寻找解。以下是数值方法常规使用的一些主要问题类型：

- 1. 对于少数代数方程，公式（例如二次方程的二次公式）给出精确根，但对于大多数方程，使用数值方法来寻找近似根。
- 2. 许多问题的解，如求曲线下的面积、计算某些事件的概率、计算力所做的功，需要对积分进行求值。对于某些问题，可以使用积分微积分的方法，但对于其他问题，使用数值技术来寻找近似值。
- 3. 微分方程在许多应用中起着重要作用，并且已经开发出各种有效且高效的数值方法来获得解。
- 4. 曲线拟合是指分析成对的数据值以确定这些对中的项目是否由某个代数方程相关。例如，第 9.4 节编程问题 10 中描述的最小二乘法就是将一条直线拟合到一组点的方法。
- 5. 数值方法通常用于找到同时满足多个未知数的线性方程组的解。这样的线性系统将在我们考虑矩阵时稍后描述。

在本节中，描述了前三类中的一些数值方法。

## 6.5.1 求解方程——二分法

在许多应用中，有必要找到函数的零点或根，即求解形式为 f(x) = 0 的方程。对于某些函数，可能很难甚至不可能精确找到此解。示例包括函数

```
f(v) = 50·10⁻⁹ (e⁴⁰ᵛ − 1) + v − 20
```

这可能出现在确定电气电路中直流工作点的问题中，或形式为

```
f(x) = x tan x − a
```

的函数。

一种简单的数值方法，用于寻找方程 f(x) = 0 的近似解是二分法。（编程问题描述了另一种常用的方法，称为牛顿-拉夫森法。）在二分法中，我们从区间 [a, b] 开始，其中函数值 f(a) 和 f(b) 在端点处符号相反。如果 f 在此区间内连续——即 y = f(x) 的图像在此区间内没有断裂——则 f 的图像必须在 x = a 和 x = b 之间至少一次穿过 x 轴，因此在 a 和 b 之间必须至少有一个方程 f(x) = 0 的解。为了定位其中一个解，我们首先将区间 [a, b] 二分并确定 f 在哪一半变号，从而定位包含方程解的更小的子区间。我们对该子区间进行二分并确定 f 在其哪一半变号；这给出包含解的更小的子区间。

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_193_0.png)

重复此过程会产生一系列子区间，每个子区间都包含方程的解，并且长度是前一个区间的一半。注意，在每一步，长度为 L 的子区间的中点与精确解的距离在 L / 2 以内：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_193_1.png)

示例 6.11 中的程序使用二分法来寻找近似解

f(x) = x³ + x − 5 = 0

它生成对解的连续近似值，在获得长度保证用户输入的指定精度的区间时终止。

## 示例 6.11 二分法

```
/* Program finds an approximate solution of the equation f(x) = 0
in a given interval, using the bisection method.

Input:  desired accuracy of approximation, endpoints of an interval
        containing a solution
Output: prompts to the user and the approximate solution
---------------------------------------------------------------*/

#include <iostream>
using namespace std;

double f(double x);

int main()
{
    cout << "\nThis program uses the bisection method to find an\n"
         << "approximate solution to the equation f(x) = 0.\n";

    double desiredAccuracy;      // the accuracy desired

    cout << "\nEnter the accuracy desired (e.g. .001): ";
    cin >> desiredAccuracy;

    double left, right;          // get interval containing a solution

    do
    {
        cout << "Enter endpoints of an interval containing a solution: ";
        cin >> left >> right;
    }
    while (f(left) * f(right) >= 0.0);

    double width = right - left,  // the interval width
           midPt,                // the midpoint of the interval
           fMid;                 // value of f() at midpoint

    while (width/2.0 > desiredAccuracy)
    {
        midPt = (left + right) / 2.0;
        fMid = f(midPt);

        if (f(left) * fMid < 0.0 )  // solution is in left half
            right = midPt;
        else                        // solution is in right half
            left = midPt;

        width /= 2.0;               // split the interval
    }
```
