

# 第 14 章

## 割线法

# 程序 14.3

```cpp
#include <iostream>
#include <cmath>
using namespace std;

void secant(double, double, double, int); // 函数原型
double f(double); // 函数原型

int main()
{
    int imax; // 最大迭代次数
    double a, b; // 原区间的左右端点
    double epsilon; // 收敛标准

    // 获取输入数据
    cout << "Enter the limits of the original search interval, a and b: ";
    cin >> a >> b;
    cout << "Enter the convergence criteria: ";
    cin >> epsilon;
    cout << "Enter the maximum number of iterations allowed: ";
    cin >> imax;

    secant(a, b, epsilon, imax);

    return 0;
}

// 此函数实现了割线法，用于寻找
// 函数的根
void secant(double a, double b, double epsilon, int imax)
{
    int i; // 当前迭代计数器
    double x0, x1; // 当前区间的左右 x 值
    double f0, f1; // 在这些点处的函数值
    double dx0; // delta x0
    double dx1; // delta x1
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_790_0.png)

```cpp
// 输出传递的输入数据
cout << "\nThe original search interval is from " << a << " to " << b
 << "\nconvergence criterion is: interval < " << epsilon
 << "\nThe maximum number of iterations allowed is: " << imax << endl;
// 确定根
x0 = a;
f0 = f(x0);
dx0 = abs(b - a);
```

```cpp
// 迭代
for (i = 1; i <= imax; i++)
{
x1 = x0 + dx0;
f1 = f(x1);
if (abs(f1) < epsilon) // 找到根
{
cout << "\nRoot at x = " << x1 << " was found "
cout << "\nin " << i << " iterations" << endl;

cout << "\nThe value of the function is: " << f1 << endl;
return;
}
else // 下次迭代
dx1 = ( f1/(f0 - f1) ) * dx0;
x0 = x1;
dx0 = dx1;
f0 = f1;
}
```

```cpp
cout << "\nAfter " << imax << " iterations, no root was found "
 << "\nwithin the convergence criterion\n"
 << "The search for a root has failed due to excessive iterations\n"
 << "after the maximum number of: " << imax << " iterations" << endl;

return;
}
```

```cpp
// 计算 f(x) 的函数
double f(double x)
{
const double PI = 2*asin(1.0); // pi 的值

return (exp(-x) - sin(0.5 * PI * x));
}
```

程序 14.3 的示例运行如下：

```
Enter the limits of the original search interval, a and b: .4 .5
Enter the convergence criteria: .00001
Enter the maximum number of iterations allowed: 25
```

The original search interval is from 0.4 to 0.5
The convergence criterion is: interval < 1e-005
The maximum number of iterations allowed is: 25

A root at x = 0.443628 was found in 4 iterations
The value of the function is -9.01417e-008

尽管割线法可能是寻找根最流行的方法，但它确实存在发散问题。由于某种原因，可以在该方法的 C++ 代码中建立一个检查，检测连续区间是否开始变大而不是变小。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_792_0.png)

# 练习题 14.4

- 1.（练习）运行程序 14.3。
- 2.（练习）使用程序 14.3 寻找函数 f(x) = x^2 - 2x + 0.9 的根，初始假设为 x0 = 0.6 和 x1 = 0.9。
- 3.（练习）程序 14.3 中的割线函数（ ）被用于寻找函数 f(x) = x^2 - 2x + 0.9 的根。从初始假设 x0 = 0.6, x1 = 0.9 开始，每次迭代显示的 x0 和 x1 值如下：

| 步骤 | X0 | X1 - X0 |
|---|---|---|
| 0 | 0.600 | 0.300 |
| 1 | 0.900 | -0.180 |
| 2 | 0.720 | -0.057 |
| 3 | 0.663 | 0.022 |
| 4 | 0.685 | -0.001 |

仔细绘制 0.5 ≤ x ≤ 1.0 的函数，并使用之前的数字显示割线法如何得到函数的根。
- 4.（数值）使用程序 14.3 寻找函数 f(x) = x^2 - 2x - 3 的根。

# 14.5 数值积分引论

单变量函数的积分可以被视为微分的反——即原函数——或者是曲线下的面积。原函数通常在微积分课程中讨论。在本节中，我们关注的是更非分析性的视觉化方法，即将定积分解释为面积。函数 $f(x)$ 从 $a$ 到 $b$ 的积分

```
$I = \int_{a}^{b} f(x)dx
```

通过设计测量该区间函数图形面积的方案来评估积分的最有效方法是首先学习数值方法，以后通过更正式的原函数概念来加强理解。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_793_0.png)

阶段学习数值积分的另一个原因是它是稳定的过程。因为数值积分将面积表示为较小段的和，这可以有效地防止除零或相同数量数字引起的舍入误差问题。不幸的是，许多出现在工程或科学问题中的积分——得到答案的解析表达式——需要大量的训练和经验。必须学习许多“技巧”。另一方面，数值积分方法很少且易于理解和记忆。在许多其他程序中，你通过将有限范围内的函数替换为直线段开始。将区间 $[a, b]$ 分分为长度为 $\Delta x$ 的子区间。函数在每个子区间上被替换，然后通过面积近似函数。这种方法是积分的梯形近似，将在下一节描述。下一种近似是用抛物段替换函数，称为辛普森法则，并在第14.7节解释。

# 14.6 梯形法

通过假设有限范围内的函数可以用简单的函数替换来获得曲线面积的近似。函数的简单近似首先被考虑并被称为梯形法。函数 $f(x)$ 从 $a$ 到 $b$ 的曲线面积通过连接点 $f(a)$ 和 $f(b)$ 之间的直线来近似。面积面积是积分的近似和梯形的面积，其值为 $f$ 的平均值乘以区间宽度：

$I \approx \frac{1}{2} [f(a) + f(b)](b - a) = T_0$

这是一个面板的梯形法，标识为 $T_0$。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_794_0.png)

**通过单个梯形近似曲线面积**

为了提高曲线近似的精度，将区间对半，并在每个半部分用直线段近似函数。此示例中的面积由两个梯形的面积近似，如图14.9所示：

```
I = T_l = [\frac{\Delta x_l}{2}(f(a) + f_l)] + [\frac{\Delta x_r}{2}(f_l + f(b))] \quad \text{(OCR错误)}
```

或者

```
$T_l = \frac{\Delta x_l}{2}[f(a) + 2f_l + f(b)] \quad \text{(公式14.7)}$
```

其中

```
$\Delta x_l = \frac{(b - a)}{2}$
```

$f_l = f(a + \Delta x_l)$

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_795_0.png)

**图 14.9 双面板近似面积**

注意在相加梯形面积时，$f(a)$ 和 $f(b)$ 仅是第一个和最后一个梯形的边，而 $f_i$ 是两个梯形的边，因此“计算了两次”，这解释了公式14.7中的因子2。此外，双面板近似 $T_2$ 与单面板结果 $T_1$ 的关系所示：

$T_2 = \frac{1}{2} T_1 + \Delta x f_i, \quad (\text{公式14.8})$

为了增加精度，只需将区间细分为许多面板。$n$ 个面板的结论非常明确：

$I = T_n = \frac{1}{2} f(a) + \sum_{i=1}^{n-1} f_i + \frac{1}{2} f(b) \quad (\text{公式14.9})$

其中 $\Delta x_n = (b-a)/n$，且 $f_i$ 是在每个内部点的函数值：$f_i = f(a + i\Delta x_n)$

公式14.9中额外因子2的原因与双面板近似相同。公式14.9被称为梯形法。

## 梯形法方程的计算形式

公式14.9是在假设所有面板的宽度相同为 $\Delta x_n$ 时推导出的。然而，推导过程中不需要相等面板，该公式可以很容易地推广到宽度为 $\Delta x_i, i = 1, \dots, n-1$ 的不等区间划分。然而，由于稍后解释的原因，你将限制面板宽度相等且面板数量为2的幂，所示：

$n = 2^k$

面板数量为 $n$，计算阶数称为 $k$，相应的梯形法近似标记为 $T_k$。$T_0$ 是 $n=2^0=1$ 个面板的结果。$k=2$ 或 $2^k=4$ 个面板的情况如图14.10所示。在该图中，面板宽度为 $\Delta x_2 = (b-a)/2^2，$k=2$ 梯形法近似值为：

$T_2 = (\Delta x_2/2)[f(a) + 2f(a+\Delta x_2) + 2f(a+2\Delta x_2) + 2f(a+3\Delta x_2) + f(b)]$

