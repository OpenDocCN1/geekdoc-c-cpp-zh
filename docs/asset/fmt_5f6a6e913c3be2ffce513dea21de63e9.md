
$$f_r(x) := \begin{cases} \frac{1-r}{r} & \text{对于 } x \in [0, r) \\ \frac{2r}{1-2r}x + \frac{1-3r}{1-2r} & \text{对于 } x \in [r, r/2) \\ \frac{2r}{1-2r}(1-x) + \frac{1-3r}{1-2r} & \text{对于 } x \in [1/2, 1-r] \\ \frac{1-r}{r}(1-x) & \text{对于 } x \in [1-r, 1] \end{cases}$$

其中参数范围为 $r \in (0, 1/2)$。为了精确找到不变密度，我们控制 Frobenius-Perron 积分方程。Frobenius-Perron 积分方程给出

$$\rho_r(x) = \int_0^1 \rho_r(y)\delta(x-f_r(y))dy.$$

我们应用狄拉克函数的恒等式 $(c \neq 0)$，其中对 $n$ 求和遍历所有重数为 1 的零，$g'(y_n)$ 表示在 $y_n$ 处的导数。

其他分段线性映射，例如锯齿形映射，已被 van Wyk 和 Steeb [259] 研究过。映射 $f : \mathbb{R} \to \mathbb{R}$ 为：

$$f(x;a,b,c) = \begin{cases} x+b-c, & \text{如果 } x \leq (a-1)/a \\ (1-ab)x+ab-c, & \text{如果 } (a-1)/a < x < 1 \\ x-c, & \text{如果 } 1 \leq x \end{cases}$$

![](img/e89136779f66a50f0bd7e926e5daf1d2_41_0.png)

# 第1章 非线性与混沌映射

```cpp
double lambda = log(fabs(y))((double) T); // 李普诺夫指数
cout << "lambda" << " " << lambda << endl;
// 方法
double eps = 0.001; double xeps, xeps1 = 0.3; xeps = x-eps;
// x 和 xeps 是邻近的点
double sum = 0.0;
T = 1000;
double distance;
for(int t=0;t<T;t++)
{
    l1 = x; xeps1 = xeps;
    x = 4.0*xeps1*(1.0-xeps);
    double distance = fabs(x-xeps);
    sum += log(distance/eps);
    xeps = x-eps;
}
lambda = sum/((double) T);
cout << "lambda" << " " << lambda << endl;
return 0;
```

在接下来的 C++ 程序中，我们使用 Symbolic++ 的 `VeryLong` 和 `Derive` 类来寻找李普诺夫指数的近似值。`Derive` 类提供了导数。因此通过精确微分得到变分方程

```cpp
// Liapunov2.cpp
// 逻辑映射与变分方程的迭代

#include <iostream>
#include <cmath>                // 用于 fabs, log
#include "verylong.h"
#include "rational.h"
#include "derive.h"
using namespace std;

int main()
{
    int T = 100;                    // 迭代次数
    double x = 1.0/3.0;               // 初始值
    double x1; double y = 1.0;
    Derive<double> Ci(1.0);             // 常数 1.0
    Derive<double> C4(4.0);             // 常数 4.0
    Derive<double> X;
    cout << "t = " << t << " << " <<x = " << x << " " << endl;
    for(int t=1;t<=T;t++) x1 = x; x = 4.0*x1*(1.0-x1);
    X.set(x1); Derive<double> Y = C4*X*(C1-X); y = df(Y);
    cout << "t = " << t << " << " <<x = " << x << " "
    cout << "y = " << y << endl << endl;
}
```

## 1.1 一维映射

```cpp
}
double lambda = log(fabs(y))((double) T);
cout << "approximate value for lambda = " << lambda << endl;
int M = G;
Rational<VeryLong> u; Rational<VeryLong> u("1/3"), v(1);
Rational<VeryLong> K1("1"), K2("4");
DeriveRational<VeryLong> D = D1(K1); // 常数 1
DeriveRational<VeryLong> V = D4(K2); // 常数 4
DeriveRational<VeryLong> U > U;
cout << "j = 0 u = " << u << " " <<v = " " << endl;
for(int j=1;j<=M; j++) {
    u1 = u; u = K2*u1*(K1-u1);
    u.set(Rational<VeryLong>(u1));
    DeriveRational<VeryLong> V = D4*U*(D1-U);
    v = df(V)*y;
    cout << "j = " << j << " " 
    cout << "u = " << u << " " << "v = " << v << endl;
}
lambda = log(fabs(double(y))((double) M));
cout << "approximate value for lambda = " << lambda << endl;
return 0;
```

**示例。** 正弦映射 $f: [0,1] \to [0,1]$ 定义为 $f(x) := \sin(\pi x)$。该映射可以写为差分方程

> $x_{t+1} = \sin(\pi x_t)$

其中 $t=0, 1, 2, \dots$ 且 $x_0 \in [0, 1]$。正弦方程的变分方程给出

> $y_{t+1} = \frac{df}{dx}(x=x_t)y_t = \pi \cos(\pi x_t)y_t$。

为了找到正弦映射的李普诺夫指数，我们在 C++ 程序 `Liapunov.cpp` 中替换以下行

```cpp
x = 4.0*x1*(1.0-x1); xeps = 4.0*x1*(1.0-x1)
```

```cpp
x = sin(x1)
```

在该语句前面添加 `const double pi = 3.14159;`。对于 $T = 5000$，得到 $\lambda = 0.689$。这显示了混沌行为。

### 1.1.5 相关函数

考虑一维差分方程 $f : [0,1] \to [0,1]$

$x_{t+1} = \sin(\pi x_t)$

其中 $t=0, 1, 2, \dots$。**时间平均** 定义为

$\langle x \rangle := \lim_{T\to\infty} \frac{1}{T} \sum_{t=0}^{T-1} x_t$。

**相关函数** 定义为

$C(\tau) = \lim_{T\to\infty} \frac{1}{T} \sum_{t=0}^{T-\tau-1} (x_t - \langle x \rangle)(x_{t+\tau} - \langle x \rangle)$

其中 $\tau=0, 1, 2, \dots$。**示例。** 对于逻辑映射 $f(x)=4x(1-x)$，

$C(\tau) = \begin{cases} 1/8 & \text{for } \tau = 0 \\ 0 & \text{otherwise} \end{cases}$ 初始值。C++ 程序 `autocorrelation.` 计算平均值

```cpp
// autocorrelation.cpp

#include <iostream>
using namespace std;

double average(double* x) {
 {
 sum = 0.0;
    for(int t=0;0<T;t++) {
        sum += x[t];
    }
    return sum/T;
}

void

orr(double* x, double& C, int T, double av) {
    double sum = 0.0;
    int diff = T-1;
    for(int t=0;t<diff;t++) {
        sum += (x[t]-av)*(x[t+1]-av);
    }
    C = sum/diff;
}

int main(void) {
    int T = 4096;
    double* x = new double[T];
    x[0] = 1.0/3.0; // 初始值
    for(int t=0;t<T-1;t++) {
        x[t+1] = 4.0*x[t]*(1.0-x[t]);
    }
    double av = average(x, T);
    cout << "average value = " << av << endl;
    int length = 11;
    double* C = new double[length];
    autocorr(x, C, T, av);
    for(int tau=0;tau<length;tau++)
        cout << "C[" << tau << "] = " << C[tau] << endl;
    delete[] x;
    delete[] C;
    return 0;
}
```

输出与上述精确解吻合良好。对于平均值我们得到 0.497383，对比 0.5；对于 $C(0)$ 我们得到 0.125707，对比 0.125。将 C++ 程序应用于映射 $f(x)=3x(1-x)$。

### 1.1.6 萨尔科斯基定理

Sarkovskii 定理（Sarkovskii [216], Stefan [247], Yorke [54]）告诉我们，如果一个连续映射 $f: \mathbb{R} \to \mathbb{R}$ 具有周期为 $k$ 的轨道，且在萨尔科斯基序中 $k < \ell$，则 $f$ 具有周期为 $\ell$ 的轨道。萨尔科斯基序可以写为：

- $3, 5, 7, 9, \dots$
- $2\cdot3, 2\cdot5, 2\cdot7, \dots$
- $2^2, 2^2\cdot3, 2^2\cdot5, \dots$
- $2^3, 2^3\cdot3, 2^3\cdot5, \dots$
- $\dots, 2^n, \dots, 2^2, 1$

萨尔科斯基定理的逆定理是：对于每个自然数 $n>1$，存在一个一维连续函数，具有周期为 $2n+1$ 的周期，但不具有为 $2n-1$ 的周期。

## 1.1 一维映射

### 1.1.7 离散一维傅里叶变换

离散傅里叶变换是连续傅里叶变换的近似。当有一组函数样本值 $x(t)$ 分布在等间隔的时间点（编号为 $t=0,1,...,T-1$）时，就会使用离散变换。离散傅里叶变换将给定的函数值集合映射到一组均匀间距的正弦波，其频率编号为 $k=0,1,...,T-1$，振幅由下式给出：

```
$$\hat{x}(k)=\frac{1}{T-1}\sum_{t=0}^{T-1}x(t)\exp\left(-i2\pi k\frac{t}{T}\right)
```

该方程可以写为：

```
$$\hat{x}(k)=\frac{1}{T-1}\sum_{t=0}^{T-1}x(t)\cos\left(2\pi k\frac{t}{T}\right)-i\frac{1}{T-1}\sum_{t=0}^{T-1}x(t)\sin\left(2\pi k\frac{t}{T}\right)
```

逆离散傅里叶变换给出于：

```
$$x(t)=\frac{1}{T-1}\sum_{k=0}^{T-1}\hat{x}(k)\exp\left(i2\pi k\frac{t}{T}\right)
```

为了找到逆傅里叶变换，我们利用以下事实：

```
$$\sum_{k=0}^{T-1}\exp\left(i2\pi k\frac{(n-m)}{T}\right)=T\delta_{nm}
```

其中 $\delta_{nm}$ 表示 Kronecker 符号。

在我们考虑的第一个 C++ 程序 (`Fourier.cpp`) 中，考虑时间 $x(t)=\cos(2\pi t/T)$，其中 $T=8$ 且 $t=0,1,2,...,T-1$。我们找到离散傅里叶变换 $\hat{x}(k)$ $(k=0,1,...,T-1)$。

```
$$\hat{x}(k)=\frac{1}{8}\sum_{t=0}^{7}\cos\left(\frac{2\pi t}{8}\right)e^{-i2\pi kt/8}
```

使用恒式 $\cos(2\pi t/8)=(e^{i2\pi t/8}+e^{-i2\pi t/8})/2$ 我们得到：

```
$$\hat{x}(k)=\frac{1}{16}\sum_{t=0}^{7}(e^{i2\pi t(1-k)/8}+e^{-i2\pi t(1+k)/8})
```

因此，

```
$$\hat{x}(k)=\begin{cases}\frac{1}{2}&for\ k=1\\\frac{1}{2}&for\ k=7\\0&otherwise\end{cases}$$
```

## 第 1 章. 非线性与混沌映射

// fourier.cpp

```cpp
#include <iostream>
#include <cmath>    // for cos, sin
using namespace std;

int main(void)
{
    const double pi = 3.14159;
    int T = 8;
    double* x = new double[T];
    for(int t=0;t<T;t++) x[t] = cos(2.0*pi*t/((double) T));
    double* rex = new double[T]; double imx = new double[T];
    for(int k=0;k<T;k++) { double cossum = 0.0, sinsum = 0.0;
        for(int t=0;t<T;t++) {
            cossum += x[t]*cos(2.0*pi*k/((double) T));
            sinsum += x[t]*sin(2.0*pi*k/((double) T));
        }
        rex[k] = cossum/((double) T); imx[k] = -sinsum/((double) T);
    }
    // display the output
    for(int k=0;k<T;k++) {
        cout << "rex[" << k << "] = " << rex[k] << " ";
        cout << "imx[" << k << "] = " << imx[k] << endl;
    }
    return 0;
}
```

在下一个 C++ 程序 (`fourier.cpp`) 中，我们考虑逻辑映射 $4x_t(1-x_t)$，其中 $t=0,1,2,...$ 且 $x \in [0, 1]$。我们假设有一组来自逻辑映射的 $T$ 个样本，即 $x_0, x_1, ..., x_{T-1}$。// fourier.cpp
