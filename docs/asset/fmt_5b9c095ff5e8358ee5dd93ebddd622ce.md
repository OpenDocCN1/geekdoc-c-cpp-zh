
注意，需要使用类型转换运算符将整数 `rand()` 转换为双精度值，以便除法结果为双精度类型。

本节之前介绍的程序可以很容易修改以生成并打印浮点值。此类修改的示例值集如下：

- 输入正种子值：
82
输入限制 a 和 b (a<b):
-5
随机数：
3.64335 -1.51118 2.9090 2.21546 -4.37439 -4.23527
0.709869 -3.41159 -4.86308 -0.958863

> 修改生成整数的程序，使其能够在用户指定的范围内生成 10 个随机浮点值。然后，使用不同的种子值，从以下每个范围范围生成几组数字：
- 1. 0.0 到 1.0
- 2. 0.1 到 1.0
- 3. -5.0 到 -4.5
- 4. -5.1 到 5.1

## 6.6 解决问题应用：仪的可靠性

如果某设备将被用在一旦故障会导致危险的情况下，或者用在难以进入的环境中，那么分析该设备的可靠性就尤为重要。

分析仪表可靠性的方程可以从统计学和概率的研究中得出，其中可靠性是组件正常工作的时间比例。因此，如果一个组件的可靠性为 0.8，那么它在 80% 的时间内会正常工作。如果已知单个组件的可靠性，也可以确定组件组合的可靠性。考虑图 6.5 中的图。在串联设计中，为了使信息从点 a 流向点 b，所有三个组件必须正常工作。在并行设计中，只需三个组件中的某一个正常工作，信息即可从点 a 流向点 b。如果我们知道单个组件的可靠性

![](img/4456642232e4f4a18bd7dfe37701766d_277_0.png)

**图 6.5** 串联和并行配置。

如果我们知道单个组件的可靠性，就可以以两种方法确定特定组件组合的可靠性：可以使用概率和统计学的定理和结果计算分析可靠性，也可以开发计算机模拟来给出可靠性的估计值。

考虑图 6.5(a) 中的串联配置。如果 r 是组件的可靠性，且所有三个组件具有相同的可靠性，那么可以证明串联配置的可靠性为 $r^3$。因此，如果每个组件的可靠性为 0.8，这意味着组件在 80% 的时间内正常工作，那么串联配置的分析可靠性为 $0.8^3$，或 0.512。这意味着，该串联配置应该在 51.2% 的时间内正常工作。

考虑图 6.5(b) 中的并行配置。三个组件中至少有一个组件必须正常工作，信息才能从点 a 流向点 b。如果我们知道单个组件的可靠性，就可以以两种方法确定特定组件组合的可靠性：可以使用概率和统计学的定理和结果计算分析可靠性，也可以开发计算机模拟来给出可靠性的估计值。

### 3. 手算示例

在手工示例中，我们使用组件可靠性 0.8 并进行三次试验。由于每次试验需要三个随机数，假设生成的前九个随机数如下。 这些值是使用 `_rand_float` 函数、种子为 6,666 且在 0 到 1 之间的数值生成的。

第一组三个随机值是：

| 0.9397775 | 0.0422243 | 0.9292037 |

第二组三个随机值是：

| 0.817733 | 0.211689 | 0.99909 |

第三组三个随机值是：

| 0.0377037 | 0.103508 | 0.4072722 |

从每组三个随机数中，我们可以确定串联配置是否能够正常工作，或者并行配置是否能够正常工作。对于第一组和第二组三个随机数，其中两个值大于 0.8，因此只有并行配置能够正常工作。对于第三组随机数，两种配置均正常工作。因此，分析结果和三次试验的仿真结果如下：

```
Analytical Reliability:

Series: 0.512 Parallel: 0.992

Simulation for 3 Trials

Series: 0.333333 Parallel: 1
```

随着试验次数的增加，仿真结果应趋于分析结果。如果更改随机种子，三次试验的仿真结果也会发生变化。

### 4. 算法开发

我们首先开发分解大纲，将解决方案分解为一系列步骤。

#### 分解大纲

- 1. 读取可靠性、试验次数和随机种子。
- 2. 计算分析可靠性。
- 3. 计算仿真可靠性。
- 4. 打印可靠性比较。

步骤 1 涉及提示用户输入必要信息。步骤 2 使用之前的公式计算分析可靠性。由于计算过程简单，我们在 `main` 函数中完成这些计算。步骤 3 涉及一个循环来生成随机数，并判断每次试验的配置是否正常工作。步骤 4 打印计算结果。该解决方案在 6.1 图中所示。伪代码的细化如下：

```
main:

  read component reliability, number of trials,

  and random number seed

  compute analytical reliabilities

  set series_success to zero

  set parallel_success to zero

  set k to 0

  while k <= number of trials

    generate three numbers between 0 and 1

    if each number <= component reliability,

      increment series_success by 1

    if any number <= component reliability,

      increment parallel_success by 1

    increment k by 1

  print analytical reliabilities

  print simulation reliabilities
```

伪代码步骤足够转换为 C++。我们在程序中包含了 `rand_float()` 函数：

```cpp
/*
 * Program6_7
 * 本程序估计串联和并行的配置可靠性。
 */
```

```cpp
#include <iostream> // 用于 cin, cout.
#include <cstdlib> // 用于 rand(), rand()
#include <cmath> // 用于 pow().
using namespace std;
```

```cpp
// 函数原型
double rand_float(double a, double b);
```

```cpp
int main()
{
  // 声明对象
  unsigned int seed;
  int n;
  double component_reliability, a_series, a_parallel;
  int series_success(0), parallel_success(0);
  double num1, num2, num3;
  // 获取仿真信息。
```

# 6. 函数模块化编程

```cpp
cout << "Enter component reliability: \n";
cin >> component_reliability;
cout << "Enter number of trials: \n";
cin >> n;
cout << "Enter unsigned seed: \n";
cin >> seed;
// 计算分析可靠性。
a_series = pow(component_reliability, 3);
a_parallel = 1 - pow(1 - component_reliability, 3);
// 确定仿真可靠性。
for (int k = 0; k < n; k++) {
  num1 = rand_float(0, 1);
  num2 = rand_float(0, 1);
  num3 = rand_float(0, 1);
  if (num1 <= component_reliability && num2 <= component_reliability && num3 <= component_reliability) {
    series_success++;
  }
  if (num1 <= component_reliability || num2 <= component_reliability || num3 <= component_reliability) {
    parallel_success++;
  }
}
// 打印结果。
cout << "Analytical Reliability \n";
cout << "Series: " << a_series << "\n";
cout << "Parallel: " << a_parallel << "\n";
cout << "Simulation Reliability " << n << " trials \n";
cout << "Series: " << (double)series_success / n << "\n";
cout << "Parallel: " << (double)parallel_success / n << "\n";
```

```cpp
double rand_float(double a, double b)
{
    return ((double)rand() / RAND_MAX) * (b - a) + a;
}
```

## 5. 测试

如果我们使用手工示例的数据，将得到如下交互，且输出匹配匹配：

```
Enter component reliability: 0.8
Enter number of trials: 3
Enter unsigned seed: 6666
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation for 3 trials
Series: 0.333333 Parallel: 1
```

以下是两次仿真结果，证明了随着试验次数的增加，仿真结果如何趋于分析结果：

```
Enter component reliability: 0.8
Enter number of trials: 100
Enter unsigned seed: 123
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation Reliability, 100 trials
Series: 0.54 Parallel: 0.97
```

```
Enter component reliability: 0.8
Enter number of trials: 1000
Enter unsigned seed: 3535
Analytical Reliability
Series: 0.512 Parallel: 0.992
Simulation Reliability, 1000 trials
Series: 0.514 Parallel: 0.995
```

# 修改

这些问题与本节开发的程序有关，该程序比较了分析可靠性和仿真可靠性。

- 1. 使用此程序计算 10、100、1000 和 10000 次试验的仿真结果比较，假设组件可靠性为 0.85。
- 2. 使用此程序计算使用五种不同随机种子的1000次试验仿真结果比较。假设组件可靠性为 0.75。
- 3. 需要什么样的组件可靠性才能使串联可靠达到0.7？ 提示：使用分析公式。 使用此程序验证你的答案。
- 4. 需要什么样的组件可靠性才能使并行可靠达到0.9？在这种使用可靠性方程并不容易。如果你的计算器无法找到多项式方程的根，请反复尝试程序直到接近所需的可靠性。
- 5. 执行必要的代数运算，证明当每个组件的 $r_c$ 相同时，方程 $R = 1 - \prod_{c=0}^{3} (1 - r_c)$ 简化为 $3r - 3r^2 + r^3$。

## 第 6.7节 定义类方法

在 `Point` 类声明中声明的重载构造函数和运算符都是 `Point` 类的方法或成员函数。回顾第 2 章的内容，方法定义了可以在类上执行的操作。我们目前对 `Point` 类的定义的操作非常有限。应用程序可以使用两种构造方法中的一种来声明和初始化 `Point` 对象，但应用程序无法访问 `Point` 对象的属性。因此，一旦 `Point` 对象被初始化，它的值就无法被修改，应用程序无法访问私有属性的值。在本节中，我们将定义一组访问器方法 `accessor methods` 和一组变器方法 `mutator methods`，以为我们的自定义数据类型 `Point` 提供更好的公共接口。

### 公共接口

**封装** `encapsulation` 一个设计良好的数据类型的公共接口提供了一组完整且最小的公共方法集，并通过封装隐藏数据类型的实现。封装要求对类属性的直接访问限制在类内的成员函数和友函数中。`friend` 关键字将在第 10 章中讨论。封装和良好的公共接口允许数据类型进行高效的维护和扩展。我们在 `Point` 类中使用了 `private` 关键字来限制对属性的访问。因此，通过当前的公共接口，应用程序无法访问或修改 `Point` 对象的值。考虑所示的测试程序：

```cpp
#include <iostream>
#include "Point.h"
using namespace std;
int main()
{
    Point pl;
    cout << pl.xCoord << endl;
    return 0;
}
```

该程序尝试打印 `Point` 对象 `pl` 的私有数据成员 `xCoord` 的值。`pl.xCoord` 的语法是正确的，在这种情况下编译器会生成错误信息，因为 `xCoord` 是一个私有属性。在 Mac Pro 上使用 `g++` 编译器编译此程序时生成的错误信息所示：

![](img/4456642232e4f4a18bd7dfe37e70176d_284_0.png)

```
Ingbers-Macbook-Pro:Programs jaingber5 g++ main.cpp Point.cpp
Point.h:7: 'int main()'
Point.h:9: error: double::xCoord is private
main.cpp:7: error: within this context
```

良好的公共接口需要一组完整的公共方法来支持类的私有属性。我们的 `Point` 类有两个私有属性，我们将向公共接口中添加另外四个方法：两个访问器方法和两个变器方法。扩展后的类声明所示所示：

```cpp
/* /
 * Point class Chapter6_7 */
 * Filename: Point.h */
class Point
{
    // 类型声明语句
    // 数据成员。
    private:
    double xCoord, yCoord; //类属性
    public:
    // 类方法的声明语句
    // Point 类的构造函数
    Point(); //默认构造函数
    Point(double x, double y); //参数化构造函数
    // 重载运算符
    double operator -(const Point& rhs) const;
    bool operator ==(const Point& rhs) const;
    // 访问器方法
    double getX() const { return xCoord; }
    double getY() const { return yCoord; }
    // 变器方法
    void setX(double newX);
    void setY(double newY);
};
```

### 访问器方法

访问器方法是带有空参数列表的返回值的成员函数。访问器方法的唯一目的是返回属性的值。因为访问器方法是短小简单的方法，它们可以定义在类声明中。目前的惯例是将这些方法命名为 `getAttribute()`。我们注意到访问器方法定义中的 `const` 修饰符很重要。访问器方法旨在为属性提供只读访问，而 `const` 修饰符的使用强制了这一点。在 `const` 方法中尝试修改私有属性的任何都将导致编译错误，正如我们的测试程序所示。为了说明访问器方法的使用，我们将修改测试程序使用访问器方法 `getX()` 来打印点的 x 坐标值。

```cpp
#include <iostream>
#include "Point.h"
using namespace std;
int main() {
  Point p1(2.3, -7.1);
  cout << p1.getX() << endl;
  return 0;
}
```
