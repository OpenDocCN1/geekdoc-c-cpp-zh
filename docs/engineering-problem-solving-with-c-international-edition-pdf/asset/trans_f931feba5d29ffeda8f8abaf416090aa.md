

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_0.png)

### 图 6.14 曲线下的面积。

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_1.png)

### 图 6.15 等间距点。

如果用直线段连接曲线上的点，我们就形成一组梯形，它们的总面积近似于曲线下的面积。曲线上的点越密集，区间内的梯形就越多，因此对积分的近似就越准确。在图 6.16 中，我们使用曲线上的五个点来生成四个梯形，这四个梯形面积之和即为函数在 a 和 b 之间积分的近似值。

梯形的面积等于底乘以两个高（或两边）之和再乘以一半：

Area = 1/2 * base * (height₁ + height₂).

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_2.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_3.png)

### 图 6.16 四个梯形。

因此，第一个梯形 $A_1$ 的面积是通过点对 $(x_1, y_1)$ 和 $(x_2, y_2)$ 计算得出的：

$A_1 = 1/2 * (x_2 - x_1) * (y_1 + y_2)$.

在本例中，由于曲线上的点沿 x 轴等间距分布，每个梯形的底都是相同的值。我们可以分别计算各个梯形的面积，如下：

- A1 = 1/2 * base * ($y_1$ + $y_2$),
- A2 = 1/2 * base * ($y_2$ + $y_3$),
- A3 = 1/2 * base * ($y_3$ + $y_4$),
- A4 = 1/2 * base * ($y_4$ + $y_5$).

因此，a 和 b 之间的总面积可以由四个梯形的面积之和近似得到：

$$\int_a^b f(x) dx \approx \frac{base}{2} ((y_1 + y_2) + (y_2 + y_3) + (y_3 + y_4) + (y_4 + y_5))$$
$$\approx \frac{base}{2} (y_1 + 2y_2 + 2y_3 + 2y_4 + y_5).$$

一般来说，如果将曲线下的面积分为底相等的 $N$ 个梯形，则面积可以由以下方程近似：

$$\int_a^b f(x) dx \approx \frac{base}{2} \left( y_1 + 2 \sum_{k=2}^N y_k + y_{N+1} \right).$$

该方程称为梯形法则。

使用这种数值技术计算积分时，我们需要记住，曲线上的数据点可能来自不同的来源。如果我们有曲线的方程，C++ 程序可以计算我们用作梯形高度的数据点；在这种情况下，我们可以随意选择数据点是尽可能接近还是尽可能分开。另一种可能性是，这些点是实验收集的数据；在这种情况下，我们有一组表示梯形底值的 x 坐标和表示梯形高度的 y 坐标。我们仍然可以使用梯形面积来估计积分，但不能选择更接近或更远的数据点，因为我们没有可供求值的函数；我们只有可用的数据。如果由数据点确定的梯形底不相等，我们必须分别计算各个梯形的面积，而不是使用假设底相等的方程。

我们将现在展示一个 C++ 程序，用于确定以下方程在两个指定点之间积分的估计值：

$y = f(x)$
$= 4e^{-x}.$

```cpp
/*-------------------------------- Program chapter6_12 ----------------------------------*/
/*                                                                                       */
/*   Program chapter6_12                                                                 */
/*                                                                                       */
/*   This program estimates the area under a given curve                                 */
/*   using trapezoids with equal bases.                                                  */
/*---------------------------------------------------------------------------------------*/
#include<iostream>    //Required for cin, cout
#include<cmath>       //Required for exp()
using namespace std;

// Function prototypes.
double integrate(double a, double b, int n);
double f(double x);

int main()
{
   // Declare objects
   int num_trapezoids;
   double a, b, area;

   // Get input from user.
   cout << "Enter the interval endpoints, a and b\n";
   cin >> a >> b;
   cout << "Enter the number of trapezoids\n";
   cin >> num_trapezoids;

   // Estimate area under the curve of 4e^-x
   area = integrate(a, b, num_trapezoids);

   // Print result.
   cout << "Using " << num_trapezoids
        << " trapezoids, the estimated area is "
        << area << endl;

   return 0;
}
```

```cpp
double integrate(double a, double b, int n)
{
   // Declare objects.
   double sum(0), x, base, area;

   base = (b-a)/n;
   for(int k=2; k<=n; k++)
   {
      x = a + base*(k-1);
      sum = sum + f(x);
   }
   area = 0.5*base*(f(a) + 2*sum + f(b));
   return area;
}
```

```cpp
double f(double x)
{
    return(4*exp(-x));
}
/*-------------------------------------------------------------*/
```

以下是前面程序的一些示例运行：

```
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
5
Using 5 trapezoids, the estimated area is 2.536905
--------------------------------------------------------------
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
50
Using 50 trapezoids, the estimated area is 2.528567
--------------------------------------------------------------
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
100
Using 100 trapezoids, the estimated area is 2.528503
```

如果使用微积分对指定函数在区间 [0, 1] 上进行积分，精确到七位小数的理论答案是 2.528482。

## 摘要

大多数 C++ 程序都能从同时使用库函数和程序员定义的函数中受益。函数使我们能够重用软件并在解决方案中采用抽象，从而缩短开发时间并提高软件质量。开发了大量示例来说明如何使用带返回值的程序员定义函数来解决问题，包括递归函数的示例。还介绍了具体应用，以说明如何生成随机数（整数或浮点值）以及如何实现增量搜索技术和牛顿 - 拉夫逊方法来识别多项式的实根，以及使用梯形法则进行数值积分。

## 关键术语

| 抽象 | 计算机仿真 |
|---|---|
| 访问器方法 | 自定义头文件 |
| 地址运算符 | 封装 |
| 自动存储类 | 外部存储类 |
| 重心 | 函数参数 |
| 参数强制转换 | 形式参数 |
| 复合材料 | 函数 |

- 函数参数
- 函数体
- 函数头
- 函数原型
- 全局作用域
- 增量搜索
- 库函数
- 局部作用域
- 模块化
- 模块
- 模块图
- 矩
- 修改器方法
- 牛顿 - 拉夫逊方法
- 数值积分
- 参数声明
- 按引用传递
- 按值传递
- 公共接口
- 程序员定义的函数
- 随机数
- 随机数种子
- 寄存器类
- 可靠性
- 可重用性
- 根
- 作用域
- 仿真
- 稳定系统
- 静态存储类
- 存储类
- 结构图
- 系统
- 梯形法则

## C++ 语句摘要

### 函数定义：

```
return_type function_name(parameter types)
{
    declarations:
    statements:
}
```

### 方法定义：

```
return_type class_name::function_name(parameter types)
{
    declarations:
    statements:
}
```

### 返回语句：

void 函数：

```
return;
```

### 带返回值的函数：

```
return ( a + b)/2;
```

### 函数原型：

```
double sinc(double x);
double sinc(double);
void check_roots(double left, double right, double a0,
                 double a1, double a2, double a3);
```

