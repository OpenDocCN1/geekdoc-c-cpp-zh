
复数的一个基本属性是

$e^{i\theta} = \cos \theta + i \sin \theta$

因此，复数的极坐标表示的一种替代形式为

$r e^{i\theta}$

现在考虑两个复数

$z = r_1 e^{i\theta_1}$

$w = r_2 e^{i\theta_2}$

指数的常见性质给出

$z \cdot w = (r_1 e^{i\theta_1})(r_2 e^{i\theta_2}) = r_1 r_2 e^{i(\theta_1 + \theta_2)}$

这与前面展示的两个复数乘积的几何表示一致。同样，我们可以利用极坐标表示和指数的性质来说明，两个复数的商对应于这样一个向量：其大小是两个复数向量大小之商，其倾角是两个复数向量倾角之差：

$z / w = (r_1 e^{i\theta_1}) / (r_2 e^{i\theta_2}) = (r_1 / r_2) e^{i(\theta_1 - \theta_2)}$

C++ 的复数类中定义了这些基本的复数算术运算，并用通常的算术运算符 +、-、* 和 / 表示；+ 和 - 也可以用作一元运算符。此外，还定义了赋值运算符 =，以及赋值简写 +=、-=、*= 和 /=，以及逻辑运算 == 和 !=。

输入和输出运算符 << 和 >> 也针对三种复数类型进行了重载。复数值以 (a, b) 形式输出，其中 a 是实部，b 是虚部。如果虚部为 0，则可以以 a 或 (a) 形式输入；否则以 (a, b) 形式输入。

除了这些运算，C++ 还为其复数类定义了几个函数。下表描述了其中一些比较常用的函数。在下表中，z 表示复数 a + bi。

## 复数函数

|  |  |
|---|---|
| z 的实部 | real(z) 返回 z 的实部 |
|  | z.real(a) 将 a 赋给 z 的实部 |
| z 的虚部 | imag(z) 返回 z 的虚部 |
|  | z.imag(b) 将 b 赋给 z 的虚部 |

6 对于复数，<、>、≤ 和 ≥ 未定义。

|  |  |
|---|---|
| z 的相角：θ | arg(z) |
| z 的范数：a² + b² | norm(z) |
| z 的绝对值（或模）： | abs(z) |
| \|z\| = √a² + b² |  |
| z 的共轭：z̄ = a − bi | conj(z) |
| 幂：zʳ，其中 r 为实数 | pow(z, r) |
| 平方根 | sqrt(z) |
| 三角函数 | cos(z), sin(z), tan(z), |
| 双曲函数 | cosh(z), sinh(z), tanh(z), |
| 指数函数：eᶻ | exp(z) |
| 对数——自然对数、以 10 为底的对数 | log(z), log10(z) |

## 7.5.3 示例：求解二次方程

在 5.4 节中，我们考虑了求解二次方程的问题，使用 if 语句检查是否存在实根，若不存在则显示一条消息。示例 7.2 中的程序是示例 5.4 中程序的变体，它可以求出任意二次方程的根——这些根可能是复数。

### 示例 7.2 二次方程求解器——复数根

```
/* This program solves quadratic equations using the quadratic formula.

    Input: the three coefficients of a quadratic equation
    Output: the complex roots of the equation
-------------------------------------------------------------------*/

#include <iostream>      // cout, cin, <<, >>
#include <complex>       // complex types
using namespace std;

int main()
{
    complex<double> a, b, c;
    cout << "Enter the coefficients of a quadratic equation: ";
    cin >> a >> b >> c;

    complex<double> discriminant = b*b - 4.0*a*c,
                    root1, root2;
    root1 = (-b + sqrt(discriminant)) / (2.0*a);
    root2 = (-b - sqrt(discriminant)) / (2.0*a);
    cout << "Roots are " << root1 << " and " << root2 << endl;
}
```

### 示例运行：

输入二次方程的系数：1 4 3
根为 (-1,0) 和 (-3,0)

输入二次方程的系数：2 0 -8
根为 (2,0) 和 (-2,0)

输入二次方程的系数：2 0 8
根为 (0,2) 和 (-0,-2)

输入二次方程的系数：1 2 3
根为 (-1,1.41421) 和 (-1,-1.41421)

输入二次方程的系数：(1,2) (3,4), (5,6)
根为 (-0.22822,0.63589) 和 (-1.97178,-0.23589)

## 7.5.4 应用：交流电路

下面的交流电路包含一个电容器、一个电感器和一个电阻器，三者串联：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_253_0.png)

电阻器的阻抗 Z_R 就是电阻 R（单位为欧姆），但对于电感器和电容器，阻抗是频率的函数。电感器的阻抗 Z_L 是由下式给出的复数值：

```
Z_L = ω L i
```

其中 ω 是交流电源的频率（单位为弧度/秒），L 是自感（单位为亨利）。对于电容器，阻抗为

```
Z_C = -i / (ω C)
```

其中 C 是电容（单位为法拉）。总阻抗 Z 由下式给出：

```
Z = Z_R + Z_L + Z_C
```

电流 I（单位为安培）为

```
I = V / Z
```

示例 7.3 中的程序输入电阻、电感、电容、交流电源频率和电压，然后利用前面的公式计算电流并输出。

### 示例 7.3 交流电路中的电流

```
/* This program computes the current in an a-c circuit containing a capacitor, an inductor, and a resistor in series.

Input: resistance, inductance, capacitance, frequency, voltage
Output: current
*/

#include <iostream>  // cin, cout, <<, >>
#include <complex>  // complex<double> type
#include <iomanip>  // format output
using namespace std;

int main()
{
  const complex<double> i = complex<double>(0, 1);
  double R,  // resistance (ohms)
  L,  // inductance (henrys)
  C,  // capacitance (farads)
  omega;  // frequency (radians per second)
  complex<double> V,  // voltage (volts)
  Z,  // total impedance
  I;  // current (amperes)
  cout << "\nEnter resistance (ohms), inductance (henrys),\n and capacitance (farads): ";
  cin >> R >> L >> C;
  cout << "\nEnter frequency (radians/second): ";
  cin >> omega;
  cout << "\nEnter voltage as a complex number in the form (x, y): ";
  cin >> V;
  // Calculate resistance using complex arithmetic
  Z = R + omega * L * i - i / (omega * C);
  // Calculate and display current using complex arithmetic
  I = V / Z;
  cout << fixed << setprecision(2)
       << "\nCurrent = " << real(I) << " + " << imag(I) << "I"
       << "\nwith magnitude = " << abs(I) << endl;
}
```

### 示例运行：

输入电阻（欧姆）、电感（亨利）、
和电容（法拉）：5000 .03 .02

输入频率（弧度/秒）：377

以 (x, y) 形式输入复数电压：(60000, 134)

电流 = 12.00 + -0.00I
模 = 12.00

## 7.6 随机数模拟：核反应堆的屏蔽

术语 **模拟** 是指对动态过程进行建模，并利用该模型研究该过程的行为。某些 *确定性* 过程的行为可以用一个方程或一组方程来建模。例如，涉及指数增长或衰减的过程通常用形如 $A(t) = A_0 e^{kt}$ 的方程来建模，其中 $A(t)$ 是时刻 $t$ 时某种物质 $A$ 的现有量，$A_0$ 是该物质的初始量，$k$ 是速率常数。然而，在许多问题中，所研究的过程可以用 *随机性* 来建模；例如，布朗运动、飞机到达机场、机器生产的次品数量等。模拟此类过程的计算机程序使用随机数生成器，将随机性引入执行过程中产生的值。

## 7.6.1 随机数生成器——RandomInt 类

**随机数生成器**是一个函数，它从某个固定范围内以*随机*方式选取一个数，并使得由这些数构成的序列在给定范围内趋于均匀分布。虽然不可能开发出产生真正随机数的算法，但有些方法可以产生满足大多数用途的*伪随机数*序列。这些算法大多具有两个性质：

- 1. 需要一个称为*种子*的初始值来开始生成随机数。不同的种子会产生不同的随机数序列。
- 2. 生成的每个随机数都用于计算下一个随机数。

虽然 C++ 没有提供随机数生成器，但其母语言 C 提供了这一功能。可以用它来构造 RandomInt 类，用于那些值为伪随机整数的数据对象。（有关此类的更多信息，请参见教材网站。）⁷

> ⁷ 这个 RandomInt 类由加尔文学院的 Joel Adams 教授开发，他是教材《C++: An Introduction to Computing, 3/e》（Pearson Education Inc., 2003）的合著者之一。
