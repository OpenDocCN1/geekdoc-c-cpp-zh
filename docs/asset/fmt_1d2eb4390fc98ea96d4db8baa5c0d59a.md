
Lempel-Ziv 有限字符串的复杂度是从一个简单的自定界学习机器的角度评估的，该机器在扫描给定的 $n$ 位字符串 $S = s_1s_2\cdots s_n$ 时，每当发现一个以前遇过的子串，就会向内存中添加一个新单词。因此复杂度 $c(n)$ 的计算如下：假设给定字符串 $s_1s_2\cdots s_r$ 新插入了 $s_r$，即它不是通过简单复制到 $s_r$ 之前的程序得到的。到 $s_r$ 记为

$R := s_1s_2\cdots s_r$

其中 $o$ 表示 $s_r$ 是新插入的。为了检查 $R$ 的剩余部分即 $s_{r+1}s_{r+2}\cdots$ 是否可以通过简单复制重构，或者剩余 $R$ 使得 $Q \equiv s_{r+1}$ 并询问该项是否包含在 $Q$ 的词表中，这等于询问 $Q$ 是否包含在 $RQ\pi$ 的词表 $v(RQ)$ 中，其中 $RQ\pi$ 表示由 $R$ 和 $\pi$（拼接）组成的字符串，而 $\pi$ 意味着最后一个数字被删除了。这可以推广到 $Q$ 也包含两个（即 $Q = s_{r+1}s_{r+2}$）或更多元素的情况。我们假设 $s_{r+1}$ 可以从 $R$ 的词表中复制。

# 第 2 章 时间序列分析

为了获得一个与字符串长度无关的复杂度度量，我们使用归一化复杂度度量。对于非常长的字符串，对其进行归一化是有意义的。为了归一化，我们考虑区间 [0,1]。区间 [0,1] 中的有理数（无理数）表示其二进制分解的 0 1 字符串是非周期性的。对于几乎所有对应于数 $x \in [0, 1]$ 二进制表示的字符串，都是随机的且具有最大复杂度。当 $n \to \infty$ 时，复杂度趋向于相同的值：

```
\frac{n}{\log_2(n)}
```

对于二进制字母表。对于具有三进制字母表的字符串，我们有 $n/\log_3(n)$。该量被用于归一化复杂度 $c(n)$。因此，最大的归一化复杂度可以等于 1。

我们假设 Lempel 和 Ziv 编码所需的信息每个新词为一个单位。“010101..”，只有这样，随机字符串的复杂度才为 $n/\log_2(n)$。当然，人们可以自由选择单位来计算复杂度。通常单位是比特（bits）。在这种情况下，指定 $n$ 个词中的一个所需的信息约为 $\log_2(n)$。随机二进制字符串的平均 Lempel 和 Ziv 复杂度符号为 1 位/符号。这假设了香农熵，因此在完全混沌状态下，逻辑映射的符号 Lempel 和 Ziv 复杂度当 $n \to \infty$ 时等于 1。对数修正有几个来源，其中之一是在这种图中，Lempel 和 Ziv 复杂度仅对有限字符串定义，因此必须指定字符串长度。因此，在这种图中，长度为 $n$ 的交替二进制字符串

010101..

的 Lempel 和 Ziv 复杂度 $\ge \log_2(n)$，且不是有限的。

接下来，我们需要从一维映射中找到一个字符串。这是通过符号动力学实现的。要构造动力系统的符号动力学，划分的确定以及底层符号序列的排序规则至关重要。对于一维光滑映射，划分由所有临界组成。

```cpp
// Lempelviv.cpp
#include <iostream>
#include <cmath> // 用于 log
using namespace std;

unsigned int complexity(const unsigned int* S,unsigned int T)
```

## 2.8. 复杂度

```cpp
{
unsigned int c = 1, l = 1;
do{
  unsigned int kmax = 1;
  for(unsigned int i=0;i<l;i++) {
    unsigned int k = 0;
    while(S[i+k]==S[l+k]) {k++; if(l+k >= T-1) return (c); }
    if(k >= kmax) kmax = k+1;
  }
  ++c;
  l += kmax;
}
while (l < T)
return c;
}
```

```cpp
int main(void)
{
unsigned int T = 4000; // 字符串长度
unsigned int *S = new unsigned int[T];

// 来自逻辑映射的时间序列 -> 符号动力学
double x = 0.618; // 初始值
S[0] = 1; // 因为 x > 0.5

for(unsigned int t=1;t<T;t++){
  double x1 = x;
  x = 4.0*x1*(1.0-x1);
  if(x >= 0.5) S[t] = 1;
  else S[t] = 0;
}

unsigned int sumc = complexity(S,T);
cout << "sumc = " << sumc << endl;
double cnorm;
cnorm = sumc*log((double)T)/log(2.0)*((double)T);
cout << "cnorm = " << cnorm;
delete[] S;
return 0;
}
```

## 2.9 习题

(1) $\alpha = \sqrt{2}$。考虑映射

$x_j = (j+1)^2\alpha \quad \mod 1$

其中 $j = 0$

(2) 考虑二维映射

$x_{1,t+1} = 4x_{1,t}(1-x_{1,t}), \quad x_{2,t+1} = 4x_{1,t}x_{2,t}(1-x_{2,t})$。

这意味着序列受到逻辑映射解的调制。该二维映射的固定点为 $(0,0), (3/4,0), (3/4,2/3)$。通过计算 Lyupanov 指数和 Hurst 系数，研究由 $x_t$ ($t=0, 1, \dots$) 给出的时间序列。

(3) 变量序列是独立同分布的，如果每个随机变量与其他变量具有相同的概率分布且且相互独立。设随机变量 $\xi_t$ ($t=0, 1, \dots$) 为独立同分布随机变量序列，它们以等概率取值 $-1, 0, 1$。令 $x_t \in \{0, 1, 2, 3, 4, 5\}$ 为由下式定义的马尔可夫过程

$x_{t+1} = \begin{cases} x_t + \xi_t & \text{对于 } x_t \in \{1, 2, 3, 4\} \\ x_t & \text{对于 } x_t \in \{0, 5\} \end{cases}$

其中序列 $s_t$ ($t=0, 1, \dots$) 给出如下。考虑由 $f(y)$ 给出的立方映射 $f: [-1, 1] \to [-1, 1]$。

(ii) 求解线性差分方程

$y_{t+1} = \begin{cases} 4y^3 - 3y & \text{对于 } y \in [-1, -1/2) \\ 0 & \text{对于 } y \in [-1/2, 1/2) \\ 1 & \text{对于 } y \in [1/2, 1] \end{cases}$

选择 $y = 1/3$ 作为函数 $f$ 的初始值。找到相应的映射并计算 $\lim_{t \to \infty} P(x_t = 0|x_0 = j)$。

# 第3 章

## 平面上的自治系统

## 3.1 固定点的分类

在本章中，我们考虑平面上的自治常微分方程

$\frac{dx}{dt} = f_1(x,y), \quad \frac{dy}{dt} = f_2(x,y)$

其中 $f_1, f_2$ 是足够光滑的。点 $(x^*, y^*)$ 是固定点（平衡点），如果 $f_1(x^*, y^*) = 0$ 且 $f_2(x^*, y^*) = 0$。

为了分析固定点的稳定性，我们通常研究其雅比矩阵：

$J = \begin{pmatrix} \frac{\partial f_1}{\partial x} & \frac{\partial f_1}{\partial y} \\ \frac{\partial f_2}{\partial x} & \frac{\partial f_2}{\partial y} \end{pmatrix}_{(x^*, y^*)}$

通过计算雅比矩阵的特征值 $\lambda$ 来判断固定点的稳定性：

- 如果所有特征值的实部都小于 0，则该点是稳定的（吸引）。
- 如果至少有一个特征值的实部大于 0，则该点是不稳定的。
- 如果存在复数特征值且实部为 0，则该点可能是中心。

自治系统还可以表现出周期轨道（极限环）和混沌行为。在本章中我们将详细讨论这些现象。

### 3.1. 固定点的分类

特征方程如下：

```
$\lambda^2 - (a+d)\lambda + (ad-bc) = 0$.
```

当该方程有两个不同的根 $\lambda_1, \lambda_2$ 时，会产生线性无关的解的族。我们定义：

```
$p := a+d, \quad q := ad-bc$.
```

此时，特征方程的形式为：

```
$\lambda^2 - p\lambda + q = 0$.
```

设

下表列出了可能的情况。

| 情况 | 条件 | 结果 |
| :--- | :--- | :--- |
| (i) | $\lambda_1, \lambda_2$ 为实数、同号不等 $\Delta > 0, q > 0$ | 节点 (node) |
| (ii) | $\lambda_1 = \lambda_2$ (实数) $b \neq 0, c \neq 0$ $\Delta < 0, p \neq 0$ | 结点节点 (inflected node) |
| (iii) | $\lambda_1, \lambda_2$ 为复数，非实数部 $\Delta < 0, p \neq 0$ | 螺旋 (spiral) |
| (iv) | $\lambda_1 \neq 0, \lambda_2 = 0$ $q = 0$ | 平行 (parallel lines) |
| (v) | $\lambda_1, \lambda_2$ 为实数、异号 $q < 0$ | 鞍点 (saddle point) |
| (vi) | $\lambda_1, \lambda_2$ 为纯虚数 $q > 0, p = 0$ | 中心 (centre) |

在对固定点进行分类时，正如之前的示例，我们考虑了一个未证明的假设，即原方程的相轨迹与线性化方程在固定点附近的轨迹具有相同的性质。这对于螺旋、节点和鞍点通常是成立的，但对于中心则不然。

**示例。** 线性近似在原方程具有螺旋的地方产生了一个中心。相反，微分方程组

```
$\frac{du_1}{dt} = u_2, \quad \frac{du_2}{dt} = -u_1^3$
```

固定点 $(u_1^*, u_2^*) = (0, 0)$ 在原点有一个中心，但线性化方程组

```
$\frac{dv_1}{dt} = v_2, \quad \frac{dv_2}{dt} = 0$
```

并没有中心。

## 3.2 同宿轨道

具有同宿轨道的非谐振系统在非线性动力系统、特别是混沌系统的研究中起着特殊作用（Lichtenberg and Lieberman [152], Guckenheimer and Holmes [91]）。考虑一个一阶微分方程系统 $du_j/dt = f_j(\mathbf{u})$，其中 $j = 1, \dots, n$ ($n \ge 2$) 且 $f_j$ 是解析函数。

**定义。** 同宿轨道是一阶微分方程 $du_j/dt = f_j(\mathbf{u})$ 流的一种轨迹，它将一个鞍固定点连接到自身。因此，同宿轨道位于固定点的稳定流形和不稳定流形的交点上。

根据定义，这些轨道在 $t \to \infty$ 和 $t \to -\infty$ 时趋于同一个固定点。

**示例。** 考虑非谐振系统

```
$$\frac{d^2u}{dt^2} = \frac{u}{2} + u^2 + u^3 = 0$$
```

引入 $u_1$ 和 $u_2: du/dt$，我们得到平面上的自治系统：

```
$$\frac{du_1}{dt} = u_2, \quad \frac{du_2}{dt} = \frac{u_1}{2} - u_1^2 - u_2^2.$$
```

该系统的三个固定点由：

```
$(u_1^*, u_2^*) = (0,0), \quad (u_1^*, u_2^*) = (-\sqrt{3}+1)/2,0), \quad (u_1^*, u_2^*) = ((\sqrt{3}-1)/2,0).
```

半平面 $u_1 > 0$ 包含一个唯一的同宿轨道 $\Gamma(t) = (u_1(t), u_2(t))$，其显式给出为：

```
$u(t) = u_1(t) = \frac{2e^{\sqrt{2}t}}{(e^{\sqrt{2}t} + \frac{1}{2})^2 + 1}$.
```

固定点 (0,0) 是双点，另外两个固定点是椭点。对于固定点 (0,0)，函数矩阵的特征值是实数；对于另外两个固定点，特征值是纯虚数。

动力系统 $du_j/dt = f_j(\mathbf{u})$ 的异宿轨道是相空间中连接两个不同固定点的路径。

**示例。** 考虑平面上的单摆：

```
$$\frac{du_1}{dt} = u_2, \quad \frac{du_2}{dt} = -sin(u_1)$$
```

固定点为 $(\pi,0)$ 和 $(-\pi,0)$。

### 3.2. 同宿轨道

在 `Homoclinic.java` 程序中，我们应用李级数技术来计算给定微分方程的同宿轨道。

```java
// Homoclinic.java

import java.awt.*;
import java.awt.event.*;
import java.awt.Graphics.*;

public class Homoclinic extends Frame {
    public Homoclinic() {
        setSize(600,500);
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent event) {
                System.exit(0);
            }
        });
    }

    public void paint(Graphics g) {
        double t = 0.0001, u2 = 0.0;
        double u1 = -0.001, u2 = 0.001; // initial值
        double u1, u2;
        g.drawRect(40,40,500,40);
        g.drawLine(40,220,500,220); g.drawLine(40,40,400,400);
        while(count < 42) {
            u1 = u1; u2 = u1*(0.5-u1);
            u2 = u2+t*(0.5-u1)/2.0;
            int m1 = (int) Math.floor(150.0*u1+400.0);
            int n1 = (int) Math.floor(150.0*u2+220.0);
            int m2 = (int) Math.floor(150.0*u1+400.0);
            int n2 = (int) Math.floor(150.0*u2+220.0);
            g.drawLine(m1,n1,m2,n2);
            count += t;
        } // end while
    } // end point
}

public void main(String[] args) {
    Frame f = new Homoclinic(); f.setVisible(true);
}
```

## 3.3 单摆

单摆的方程给出为：

```
$$\frac{d^2u}{dt^2} + \omega^2 \sin(u) = 0, \quad \omega^2 := \frac{g}{L}$$
```

$L$ 是单摆长度，$g$ 是重力加速度，$u$ 是单摆相对于平衡位置的角位移，$\omega$ 是频率。引入量：

```
$$\tilde{u}(t) = u(t) \quad \tilde{t}(t) = \omega t$$
```

我们可以将单摆方程写成无量纲形式：

```
$$\frac{d^2\tilde{u}}{d\tilde{t}^2} + \sin(\tilde{u}) = 0.$$
```

后续省略波浪号。引入量 $u_1 = u$ 和 $u_2 = du/dt = du_1/dt$，得到一阶自治系统：

```
$$\frac{du_1}{dt} = u_2, \quad \frac{du_2}{dt} = -\sin(u_1).$$
```

因此我们有固定点 $(n\pi, 0), n \in \mathbb{Z}$。变分方程给出为：

```
$$\frac{dv_1}{dt} = v_2, \quad \frac{dv_2}{dt} = -\cos(u_1)v_1.$$
```

将固定点 $(n\pi, 0)$ 代入这些方程，找到：

```
$$\frac{dv_1}{dt} = v_2, \quad \frac{dv_2}{dt} = \begin{cases} -v_1 & \text{偶数} \\ v_1 & \text{奇数} \end{cases}$$
```

在第一情况下，特征值为：

```
$i \text{ 和 } -i$.
```

因此我们有一个中心。在第二情况下，特征值为：

```
$+1 \text{ 和 } -1$
```
