

## A.4 计算累积双变量正态概率

最常用的多元正态计算是双变量情况，其中我们令 x 和 y 服从双变量正态分布，均值均为 0，方差均为 1，并假设两个变量的相关系数为 ρ。根据相关系数的定义 ρ ∈ [-1, 1]。累积概率分布

P(x < a, y < b) = N(a, b, ρ) = ∫_{-∞}^{a} ∫_{-∞}^{b} (1 / 2π√(1-ρ²)) exp(-1/2 * (x² - 2ρxy + y²) / (1-ρ²)) dxdy

该积分有多种近似方法。我们选取一种，在 (Hull, 1993, Ch 10) 中讨论，如 C++ 代码 A.3 所示。

如果存在超过两个相关变量，累积概率的计算就是一个非平凡问题。一种常用方法涉及对定积分进行蒙特卡洛估计。我们将考虑这一点，但首先需要考虑随机正态变量的模拟。

### 示例

计算 N(0) 和 N(0,0,0)

```
C++ program:
cout << " N(0) = " << N(0) << endl;
cout << " N(0,0,0) = " << N(0,0,0) << endl;
Output from C++ program:
N(0) = 0.5
N(0,0,0) = 0.25
```

```cpp
#include <cmath> // include the standard library mathematics functions
using namespace std; // which are in the standard namespace
#include <iostream>
double N(const double&); // define the univariate cumulative normal distribution as a separate function
#ifndef PI
const double PI=3.141592653589793238462643;
#endif
inline double f(const double& x, const double& y,
 const double& aprime, const double& bprime,
 const double& rho) {
 double r = aprime*(2*x-aprime) + bprime*(2*y-bprime) + 2*rho*(x-aprime)*(y-bprime);
 return exp(r);
};
inline double sgn(const double& x) // sign function
{ if (x>0.0) return 1.0;
 return -1.0;
};
double N(const double& a, const double& b, const double& rho) {
 if ( (a<=0.0) && (b<=0.0) && (rho<=0.0) ) {
 double aprime = a/sqrt(2.0*(1.0-rho*rho));
 double bprime = b/sqrt(2.0*(1.0-rho*rho));
 double A[]={0.3253030, 0.4211071, 0.1334425, 0.006374323};
 double B[]={0.13333764, 0.6243247, 1.3425378, 2.2626645 };
 double I[]={0.0,0.0,0.0,0.0};
 for (int i=0;i<4;++i) {
 for (int j=0; j<4; ++j) {
 sum += A[i]*A[j]* (f(B[i],B[j],aprime,bprime,rho);
 };
 };
 sum = sum * ( sqrt(1.0-rho*rho)/PI);
 return sum;
}
else if ( (a > 0.0) && (b <= 0.0) {
 if ( (a<=0.0) && (b<=0.0) && (rho>=0.0) ) {
 return N(a) - N(a, -b, -rho);
 }
 else if ( (a>=0.0) && (b<=0.0) && (rho>=0.0) ) {
 return N(b) - N(a, b, -rho);
 }
 else if ( (a>=0.0) && (b>=0.0) && (rho<=0.0) ) {
 return N(a) + N(b) - 1.0 + N(-a, -b, -rho);
 };
}
else if ( a * b > rho >= 0.0 ) {
 double delta = sqrt(a*a - 2*rho*a*b + b*b);
 double rho1 = ((rho * a - b) * sgn(a))/denum;
 double rho2 = ((rho * b - a) * sgn(b))/denum;
 double delta=(1.0-sgn(a)*sgn(b))/4.0;
 return N(a,0.0,rho) + N(b,0.0,rho) - delta;
}
else {
 cout << " unknown " << endl;
}
return -99.9; // should never get here, alternatively throw exception
};
```

### C++ 代码 A.3：累积双变量正态的近似

## A.5 模拟随机正态数

随机数生成是一个庞大的主题，Knuth (1997) 等资料对此有详细论述。生成的数字永远不能真正随机，只能是“伪”随机，它们将根据某些可重复的算法生成，在（大量）随机数生成之后，序列将开始重复。在复制开始前的迭代次数是衡量随机数生成器质量的指标。对于需要高质量随机数生成器的任何人，都应避免使用标准 C++ 库提供的 rand() 函数，但为了不深入讨论随机数生成问题，我们将此函数作为在区间 [0,1) 上生成均匀分布数的基础，如 C++ 代码 A.4 所示。

```cpp
#include <cstdlib>
using namespace std;
double random_uniform_0_1(void){
 return double(rand())/double(RAND_MAX); // this uses the C library random number generator.
};
```

### C++ 代码 A.4：来自均匀 [0,1) 分布的伪随机数

### 练习 A.1。

将此处的 random_uniform 函数替换为更高质量的替代方案，方法是查看您的计算平台上有哪些数值库可用，或从 mathlib 或 statlib 等地方下载高质量的随机数生成器。

这些均匀分布的随机变量被用作 Knuth (1997) 讨论的正态密度极点方法的基础，并按 C++ 代码 A.5 所示实现。

```cpp
#include <cmath>
#include <cstdlib>
using namespace std;
double random_uniform_0_1(void);
double random_normal(void){
 double U1, U2, V1, V2;
 double S=2;
 while (S>=1) {
  U1 = random_uniform_0_1();
  U2 = random_uniform_0_1();
  V1 = 2.0*U1-1.0;
  V2 = 2.0*U2-1.0;
  S = pow(V1,2)+pow(V2,2);
 };
 double X1=V1*sqrt((-2.0*log(S))/S);
 return X1;
};
```

### C++ 代码 A.5：来自正态 (0,1) 分布的伪随机数

### 示例

- 1. 生成 5 个 (0,1) 之间的随机均匀数
- 2. 生成 5 个 N(0,1) 随机数。

```
C++ program:
cout << " 5 random uniform numbers between 0 and 1: " << endl;
cout << " ";
for (int i=0;i<5;++i){ cout << " " << random_uniform_0_1(); }; cout << endl;
cout << " 5 random normal(0,1) numbers: " << endl;
cout << " ";
for (int i=0;i<5;++i){ cout << " " << random_normal(); }; cout << endl;
Output of C++ program:
5 random uniform numbers between 0 and 1:
0.840188 0.394383 0.783099 0.79844 0.911647
5 random normal(0,1) numbers:
-1.07224 0.925946 2.70202 1.36918 0.0187313
```

## A.6 一般多元分布的累积概率

超越双变量情况后，概率积分的计算更多地成为一般数值积分的练习。一种典型工具是蒙特卡洛积分，但这不是唯一的可能性。

## A.7 C++11 中的实现

C++ 语言的最新标准 C++11 包含一个用于生成随机数的库。参见 (Stroustrup, 1997a, 第 5.6.3 节)。

## A.8 参考文献

Tong (1990) 讨论了多元正态分布，是一个很好的参考。对于最终来源，请参见 Knuth (1997)。

## 附录 B

### C++ 概念

本章列出了各种 C/C++ 概念，并对每个概念进行了一些说明。

- accumulate() 对序列元素进行累加的函数。
- bool 布尔变量，取 true 和 false 两个值。出于历史原因，也可以使用零和一分别表示 false 和 true。
- class (C++ 关键字)。
- const (C++ 函数调用中变量的限定符)。
- double (基本类型)。高精度浮点数。
- exp(x) (C 函数)。定义在 <cmath> 中。返回自然指数 e 的给定幂 x，即 e^x。
- fabs
- float (基本类型)。精度有限的浮点数。
- for 循环
- 头文件
- if
- 索引（在向量和矩阵中）。要访问数组 A 中的第 i 个元素，请使用 A[i-1]。这是从其他语言转到 C 的人常见的陷阱。出于历史效率原因，C 中存在此特性。C 中的数组是使用指针实现的。索引是通过查找数组的第一个元素，然后添加指针来找到索引元素。第一个元素当然是通过向第一个元素添加零来找到的，因此第一个元素的索引为零。
- include
- inline (C++ 函数名的限定符)。向优化器提示，该函数最有效的实现方式是内联，即将函数的完整代码放入每个调用实例中。副作用是使函数局限于定义它的文件。
- int (基本类型)。有效位数有限的整数。
- log(x) (C 函数)。定义在 <cmath> 中。计算其参数的自然对数 ln(x)。
- long (基本类型)。可以容纳大数的整数。
- min_element() (C++ 函数)

