

## 756 数值方法

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_775_0.png)

**图 14.2** 第二次判断左半部分或右半部分包含根的示意图

在通过判断左半部分或右半部分包含根来确定函数的根后，将区间再次替换为左半或右半区间。此过程一直持续，直到箭头指向根达到预先指定的精度。每一步都将区间减半，因此在 $n$ 次迭代后，包含根的区间大小为 $(b-a)/2^n$。如果你需要找到在容差 $\delta$ 以内的根（即 $|x - \text{root}| < \delta$），则所需的迭代次数 $n$ 可以根据方程确定：

$\frac{b-a}{2^n} < \delta$

例如，在前一节示例中的初始搜索区间为 $(b-a) = 0.1$。如果要求的根的精度为 $\delta = 10^{-5}$，则：

$\frac{0.1}{2^n} < 10^{-5}$

或者

$2^n > 10^4$

该方程可以如下解出 $n$：

$n > \log(10^4) / \log(2)$

因此，计算表明，通过第 13 次应用区间平分程序即可达到该精度。该方法中被省略的唯一元素是计算机如何确定区间的哪一半包含轴交点。

## 第 14 章

## 二分法

为此，考虑函数在左侧的取值 $f_1 = f(x_1)$ 与函数在中点处的取值 $f_2 = f(x_2)$ 的乘积，所示：

| 如果 | 那么 |
|---|---|
| $f_1f_2 > 0.0$ | $f_1$ 和 $f_2$ 均为正或同为负。在任何情况下，$x_1$ 和 $x_2$ 之间都没有交点，区间内没有根。 |
| $f_1f_2 < 0.0$ | $f(x)$ 在 $x_1$ 和 $x_2$ 之间符号改变。在这种情况下，在 $x_1$ 和 $x_2$ 限定的区间内有一个根。 |

程序 14.1 使用此过程计算方程的根。在检查此程序时，请注意以下特征：

- 在第一次之后的每次迭代中，只有一次函数评估。在每次迭代中重新评估 $f(x_1), f(x_2)$ 是低效的，因为其中两个值已经已知。如果函数极其复杂，这种冗余计算将是一个严重问题。不必要的函数评估会浪费大量时间。
- 程序包含了几个针对潜在问题的检查，并附有诊断消息（如迭代次数过多、区间内无根等），尽管程序员可能认为这些情况很罕见。程序中包含的检查越多，编写代码仅需几分钟，就能节省数小时的调试时间。
- 成功的标准基于区间的大小。因此，即使函数在某点处接近于 0，$x$ 的变化也非常微小，继续迭代也不会实质性地提高根的精度。

## 程序 14.1

```cpp
#include <iostream>
#include <cmath>
using namespace std;

void bisection(double, double, double, int); // 函数声明
double f(double); // 函数声明

int main() {
    int imax; // 最大迭代次数
    double a, b; // 原始区间的左端和右端
    double epsilon; // 收敛标准

    // 获取输入数据
    cout << "Enter the limits of the original interval, a and b: ";
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_776_0.png)

## 758 数值方法

```cpp
cin >> a >> b;
cout << "Enter the convergence criteria: ";
cin >> epsilon;
cout << "Enter the maximum number of iterations allowed: ";
cin >> imax;
```

```cpp
bisection(a, b, epsilon, imax);
```

```cpp
return 0;
```

```cpp
// 一个寻找函数根的二分函数
// 已知区间 a < x 包含 f(x) 的根。
// 通过找到根位于区间的哪一半，然后将原始区间
// 替换为该半区间，逐步改进根的估计值。
```

```cpp
void bisection(double a, double b, double epsilon, int imax)
{
    int i; // 当前迭代计数器
    double x1, x2, x3; // 当前区间的左、右、中点
    double f1, f2, f3; // 在这些点上的函数值
    double width; // 原始区间宽度 = (b - a)
    double curwidth; // 当前区间的宽度 = (x3 - x1)
```

```cpp
// 输出传递的输入数据
cout << "\nOriginal search interval is from "
cout << a << " to " << b << endl;
cout << "The convergence criterion is: interval * " << epsilon << endl;
cout << "The maximum number of iterations allowed is * " << imax << endl;
```

```cpp
// 计算根
x1 = a;
x3 = b;
f1 = f(x1);
f3 = f(x3);
width = (b - a);
```

```cpp
// 验证区间内是否存在根
if (f1 * f3 > 0.0)
    cout << "\nNo root in the original interval exists" << endl;
else
{
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_777_0.png)

## 第 14 章

## 二分法

```cpp
for (i = 1; i <= imax; i++)
{
  // 找到根位于区间的哪一半
  x2 = (x1 + x3) / 2;
  f2 = f(x2);
  if (f1 * f2 <= 0.0)
  {
    curwidth = (x2 - x1) / 2;
    f3 = f2;
    x3 = x2;
  }
  else // 根在右半
  {
    curwidth = (x3 - x2) / 2;
    f1 = f2;
    x1 = x2;
  }
  if (curwidth < epsilon)
  {
    cout << "\nroot at x = " << x2 << " was found "
    cout << "in " << i << " iterations";
    cout << "\nThe value of the function is " << f2 << endl;
    return;
  }
}
cout << "\nAfter " << imax << " iterations, no root was found" << endl;
return;
```

```cpp
// 计算 f(x) 的函数
double f(double x)
{
  const double PI = asin(1.0); // pi
  return exp(-x) - sin(x);
}
```

程序14.1 的示例运行结果：

+   Enter the limits of the original interval, a and b: .4 .5
+   Enter the convergence criteria: .00001
+   Enter the maximum number of iterations allowed: 25

## 760 数值方法

原始搜索区间从 0.4 到 0.5
收敛标准为：区间 * 1e-05
允许的最大迭代次数为 25

在 x = 0.43567 处找到根，经过 13 次迭代
函数值为 1.2259e-05

尽管程序 14.1 用于计算方程的根，通过更改返回语句中的计算部分，该程序可以用于任何函数。

最后的注释：程序 14.1 中使用的二分法是一种所谓的蛮力方法，意味着它缺乏技巧。尽管它说明了基本的 C++ 技术，但有更强大、更聪明的数值程序。这些技术将在 14.3 节中进行解释。

## 练习 14.2

- 1. （练习）使用二分法寻找方程的根。首先，构造如下形式的表格：

| 步骤 | x₁ | x₂ | x₃ | f(x₁) | f(x₂) | f(x₃) | 左侧交叉 | 右侧交叉 |
|---|---|---|---|---|---|---|---|
| 0 | a | ½(a + b) | b | | | | | |
| 1 | | | | | | | | |
| | | | | | | | | |
| | | | | | | | | |

接下来，使用二分法和手持计算器获得以下方程的五位有效数字根：
- f(x) = x² + 2x - 1（使用 a = 2.8 和 b = 3.1。精确答案 = 3.0）
- g(x) = ½sin(x)(e⁻ˣ + eˣ)（这是椭圆齿方程，x 为弧度。a = 1 和 b = 4）
- E(x) = √(R² - x²) - tan(x)（这是箱中粒子的量子能量方程。使用 R = 10，a = 4.0 和 b = 4.7）

预测找到练习 1a 到 1c 中指定精度答案所需的步数。

- 2. （修改）修改程序 14.1，以显示练习 1 中每个函数的指示表格。

- 3. （修改）修改程序 14.1，为练习 1 中使用的每个函数产生与练习 1 要求类似的表格。

