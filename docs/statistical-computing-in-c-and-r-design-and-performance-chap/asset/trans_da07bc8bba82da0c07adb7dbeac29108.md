

# 伪随机数的生成

对于 $g = 1, ..., G$。选择整数系数 $c_1, ..., c_G$ 以通过以下方式在 $[0, 1]$ 区间产生数字：

```
$u_j = (c_1 \frac{x_{1j}}{m_1} + c_2 \frac{x_{2j}}{m_2} + ... + c_G \frac{x_{Gj}}{m_G}) \mod 1$
```

其中 $x \mod 1$ 为 $x$ 的小数部分。在 L'Ecuyer 和 Tezuka (1991) 以及 L'Ecuyer (1996) 详细说明的条件下，生成器的周期长度可以达到各个生成器周期的乘积。包含此类生成器良好参数选择的表格见于 L'Ecuyer (1999)。

Wichmann 和 Hill (1982) 提出了一种组合生成器的示例，在后文中将其简称为 WH 生成器。该算法使用了线性同余（因此是 $k=1$ 的多重递归）生成器：

```
$x_i = 17Lx_i \mod 30269$
$y_i = 172y_{i-1} \mod 30307$
$z_i = 170z_{i-1} \mod 30323$
```

得到的均匀随机偏差通过以下公式获得：

```
$u_i =(\frac{x_i}{30269} + \frac{y_i}{30307} + \frac{z_i}{30323}) \mod 1$
```

该生成器的周期超过 $2.8 \times 10^{13}$。我们为 WH 生成器实现的 C++ WH 类具有以下头文件：

## 列表 4.4 WH.h

```cpp
// WH.h
#ifndef "WH_H"
#define WH_H

class WH{
unsigned long a1, a2, a3;
unsigned long m1, m2, m3;

public:
WH();
~WH();
void rangen(unsigned long seed1, unsigned long seed2,
unsigned long seed3, int n, double* pu) const;
};
#endif
```

其方法定义给出：

## 列表 4.5 WH.cpp

```cpp
// WH.cpp
#include "WH.h"

WH::WH() {
a1 = 171; m1 = 30269; a2 = 172; m2 = 30307; a3 = 170; m3 = 30323;
}
void WH::rangen(unsigned long seed1, unsigned long seed2,
unsigned long seed3, int n, double* pu) const {
double temp = 0;
```

# 其他生成方法

```cpp
for(int i = 0; i < n; i++){
  seed1 = (a1*seed1)%m1;
  seed2 = (a2*seed2)%m2;
  seed3 = (a3*seed3)%m3;
  temp = ((double)seed1)/((double)m1)
    + ((double)seed2)/((double)m2)
    + ((double)seed3)/((double)m3);
  if(temp > 2.0) temp -= 2;
  if(temp < 1.0) temp -= 1;
  pu[i] = temp;
}
```

这里 $a1, a2, a3, m2$ 和 $m3$ 代表三个生成器的倍数和模。尽管它们在构造函数定义中被显式指定以产生 WH 生成器，但也可以其他选择作为另一个构造函数的输入以产生更通用的实现。操作类方法接收种子、样本大小和指向 double 的指针。指针附近的内存位置将由生成器填充随机偏差。

WH 生成器提供的周期长度比 4.4 节的 Fisher-Moore 生成器有了显著增加。尽管如此，对于许多在并行计算环境中需要极长随机数流的应用来说，它的周期仍然太短。生成器的一个来源可以使用 L'Ecuyer 等 (2001, 2002) 的 Rngstreams。该包的 C、C++、C# 和 Java 源代码可以从以下地址下载：

```
http://www.iuumontreal.ca/-lecuyer/myftp/streams
```

特别地，Rngstreams 的 C++ 实现提供了一个 OOP 框架，其中创建的对象具有关联的方法 `Rand301` 来产生均匀偏差。

Rngstreams 的“骨干”是 Merg32k3a。它是两个多重递归生成器的组合，产生：

```
$x_{1,n} = (1403580 \times x_{1,n-2} - 810728 \times x_{1,n-3}) \pmod{2^{32} - 209}, \quad (4.11)$
$x_{2,n} = (527612 \times x_{2,n-1} - 1370589 \times x_{2,n-3}) \pmod{2^{32} - 22853}, \quad (4.12)$
```

在第 $n$ 步递归时 $\tilde{x}_i = (x_{i,0}, x_{i,1}, ..., x_{i,2})^T$，对于 $i=1,2$。这两个状态通过以下方式组合产生均匀随机 $u_n$：

```
$z_n = (x_{1,n} \pmod{2^{32} - 209}), \quad \text{if } z_n > 0,$
$u_n = z_n / (2^{32} - 209), \quad \text{if } z_n = 0.$
```

在 (4.10) 中对应 $K=2, 3，$m_1 = 2^{32}-209, a_1=1403580, a_2=-810728, m_2=2^{32}-22853, a_3=527612, a_4=-1370589$。该生成器的周期约为 $2^{61}$，前提 $x_{1,0}, x_{1,1}, x_{1,2}$ 不为 0 且小于 $(2^{32}-209)$。且 $x_{2,0}, x_{2,1}, x_{2,2}$ 小于 $(2^{32}-22853)$ 而不全为零。Rngstreams 的初始状态使用 `SetSeed` 函数设置，该函数包含用户必须提供的六个整数种子：

```cpp
static bool SetSeed(unsigned long seed[])
```

静态分配允许在没有对象的情况下调用它。实际均匀分布通过 RngStream 类的 `RandU01` 方法获得。下面的列表 4.6 展示了这一过程。

# 伪随机数的生成

## 列表 4.6 rngStream.cpp

```cpp
//RngStream.cpp
#include <iostream>
#include "RngStream.h"

using std::cout; using std::endl;

int main(){
    unsigned long seed[6] = {1, 2, 3, 4, 5, 6};
    RngStream::SetSeed(seed);
    RngStream rngObj;
    cout << "Your random number is ";
    cout << rngObj.RandU01(0) << endl;
    return 0;
}
```

关键步骤是在程序开头包含头文件 `RngStream.h`。实例化 `RngStream` 对象并生成的随机数被打印到标准输出。该程序的编译和执行如下：

```
$ g++ -Wall rngStream.cpp rngStreamEx.cpp -o rngStreamEx
$ ./rngStreamEx
Your random number is 0.1```

# 4.6 非均匀生成

如介绍所示，均匀随机数的生成是从非均匀分布中产生伪样本的关键。最直接的方法是使用算法 4.1 实现的概率积分变换。可以使用解析形式完成的情况是指数分布，其概率密度函数为：

$$f(x) = \begin{cases} \lambda exp\{-\lambda x\}, & x>0; 0, & \text{其他}. \end{cases}$$

对应于 $f$ 的分布函数为 $F(x)=1-\exp\{-\lambda x\}$，$x>0$，其反函数（分位数函数）为 $F^{-1}(u)=-\ln(1-u)/\lambda$，其中 $u \in (0,1)$。下面的驱动程序使用该函数通过 WH 生成器从指数分布产生产生伪样本，算法 4.4-5。

## 列表 4.7 driverExp.cpp

```cpp
//driverExp.cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
#include "WH.h"

using std::cout; using std::cin; using std::endl;
```

# 非均匀生成

```cpp
double Finv(double u, double lambda){
  return (-log(1 - u)/lambda);
}
```

```cpp
int main(int argc, char* argv[]){
  double lambda; int n;

  cout << "Input the value for lambda:" << endl;
  cin >> lambda;

  unsigned long seed1, seed2, seed3;
  cout << "Choose a value for the sample size:" << endl;
  cin >> n;
  cout << "Choose a value for seed1:" << endl;
  cin >> seed1;
  cout << "Choose a value for seed2:" << endl;
  cin >> seed2;
  cout << "Choose a value for seed3:" << endl;
  cin >> seed3;

  WH* pwh = new(std::n) WH();
  if(pwh == 0){
    cout << "Memory allocation for WH failed" << endl;
    exit(1);
  }

  double* pu = new(std::n) double[n];
  if(pu == 0){
    cout << "Memory allocation for double pointer failed" << endl;
    exit(1);
  }

  pwh->rangen(seed1, seed2, seed3, n, pu);
  cout << "Your random numbers are " << endl;
  for(int i = 0; i < n; i++) {
    cout << Finv(pu[i], lambda) << " ";
  }
  cout << endl;
  delete pwh;
  delete []pu;
  return 0;
}
```

