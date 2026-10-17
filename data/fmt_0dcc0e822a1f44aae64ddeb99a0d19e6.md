
$N_{i,k}(x) := \begin{cases} 1 & x_i \le x < x_{i+1} \\ 0 & k=1 \end{cases}$

```

以及

```

$N_{i,k}(x) := \frac{x-x_i}{x_{i+1}-x_i}N_{i,k-1}(x) + \frac{x_{i+k}-x}{x_{i+k}-x_{i+1}}N_{i+1,k-1}(x) \quad \text{if } k>1$

```

其中 $i=0, 1, \dots, m-k$。B 函数的属性为：

- *单位划分*：$\sum_{i=0}^m N_{i,k}(x)=1$。
- 正性：$N_{i,k}(x) \ge 0$。
- 局部支撑：当 $x \notin [x_i, x_{i+1}]$ 时，$N_{i,k}(x)=0$。
- $C^{k-2}$ 连续性：如果节点 $\{x_i\}$ 两两不相同，则 $N_{i,k}(x)$ 是 $(k-2)$ 阶连续可微的。

使用 B 函数来指定语言术语，并选择节点互不相同（周期性模型）。$k$（B 函数的阶）的选择决定了用于建模语言术语的模糊集的以下因素。因此，对于 $k=1$，我们得到矩形；对于 $k=2$，得到三角形；对于 $k=3$，得到二次曲线形（Hardy and Steele [106]）。

语言术语定义在 $[x_0, x_m]$ 上，即模糊控制器输入变量 $x$ 的论域。它们被称为*真实术语*。为了对所有 $x \in [x_0, x_m]$ 保持单位划分，应该在 $[x_0, x_m]$ 的两端添加更多的 B 函数。它们被称为*边缘 B 函数*，用于定义虚拟的语言术语。在 2 阶的情况下，左端不需要边缘 B 函数，而 3 阶或 4 阶，右端需要两个边缘 B 函数。

## 18.5. 模糊规则系统

我们将核心规则定义为使用真实语言术语的语言规则。如果前提中出现虚拟语言术语，则需要额外的规则来描述这些情况下的控制动作，以维持论域 $x$ 两端的输出连续性。

由于这些规则涉及由每个变量论域边缘相邻隶属函数定义的虚拟语言术语，它们被称为边缘规则。每个边缘规则的输出值选取与最近的核心规则的输出值相同，即在其前提中使用直接相邻的语言术语的规则。

由于多入多输出规则库通常被分为若干个多入单输出规则库，我们只考虑多入单输出的情况。在以下条件下：

- 周期性 B 样条基函数作为输入的隶属函数。
- 模糊单点作为输出的隶属函数。
- “乘积”作为模糊交与。
- “质心”作为去模糊方法。
- 在每个输入变量的两端添加虚拟语言术语。
- 通过复制最近邻域的输出值来扩展虚拟语言术语的规则库。

此类模糊控制器的输出计算等同于通用 B 样条超曲。考虑一个具有 $n$ 个输入 $x_1, x_2, \dots, x_n$ 的多入单输出系统，前提中具有 $n$ 个合取项的规则形式如下：

```

$Rule(i_1, \dots, i_n) : if(x_1 = N^1_{i_1,k_1}) \& \& (x_n = N^n_{i_n,k_n}) \text{then } y = Y_{i_1,i_2,\dots,i_n}$

```

其中

- $x_j$ 是第 $j$ 个输入 $(j=1, \dots, n)$。
- $k_j$ 是用于 $z_j$ 的 B 样条基函数的阶。
- $N^j_{i,kj}$ 是由 B 样条基函数定义的 $x_j$ 的第 $i$ 个语言术语。
- $i_j = 0, \dots, m_j$ 代表第 $j$ 个输入如何模糊划分。
- $Y_{i_1,i_2,\dots,i_n}$ 是 $Rule(i_1, \dots, i_n)$ 的控制顶点（Deor 点）。

那么多入单输出模糊控制器的输出 $y$ 等于：

```

$y = \sum_{i_1=0}^{m_1} \dots \sum_{i_n=0}^{m_n} (Y_{i_1,i_2,\dots,i_n}) = \sum_{i_1=0}^{m_1} \dots \sum_{i_n=0}^{m_n} \prod_{j=1}^n \mathcal{N}_{i_j,k_j}(x_j)$

```

这被称为通用 B 样条超曲。它具有以下属性：

- 阶为 $k_1, k_2, \dots, k_n$ 的 B 函数用于指定变量 $x_1, x_2, \dots, x_n$ 的语言术语，可以保证输出对于输入变量 $x_j$ 是 $(k_j-2)$ 阶连续可微的。
- 如果输入空间划分得当，插值可以达到给定的精度。

### 18.5.5 应用

让我们看一个近似推理示例。考虑以下分析语言的规则：

IF many THEN Java
IF more than n THEN C
AND many THEN Java

我们再次使用离散模糊集来实现这个模糊推理。

```cpp
// language.cpp

#include <iostream>

#include "Fuzzy.h"

using namespace std;

template <class T>

T min(const T& x1, const T& x2, const T& x3, const T& x4)

{

    T min = x1;

    if(min > x2) min = x2;

    if(min > x3) min = x3;

    if(min > x4) min = x4;

    return min;

}

int main(void) 

{

    const int pMin = 0; const int pMax = 10;

    const int ncr = 200;

    Fuzzy fuzzy(ncr, pMin, pMax);

    fuzzy.greaterThan(5);

    Fuzzy someManyBrackets(ncr, pMin, pMax);

    someManyBrackets = someManyBrackets.edge(somewhat);

    Fuzzy fuzzy(ncr, pMin, pMax);

    Fuzzy slightlyManyExtends(ncr, pMin, pMax);

    slightlyManyExtends = slightlyManyExtends.edge(slightly);

    double n, bracket, extend;

    cout << "Enter no " >> n;

    cout << "Enter no { " >> bracket;

    cout << "Enter no " >> begin;

    cout << "Enter no " >> extend;

    double java = slightlyManyExtends(extend);

    double cpp = min(fuzzy(n), someManyBrackets(bracket)); 

    cout << "Confidence that program is Java: " << java << endl;

    cout << "Confidence that program is C++ : " << cpp << endl;

    return 0;

}
```

针对程序元素 bracket、begin 和 extend 的出现频率（任意比例）运行程序。以下是测试运行的输出：

```
Enter no of : 10

Enter no { : 10

Enter no of : 0

Enter no of : 0

Confidence that program is Java: 0

Confidence that program is C++ : 0.93307

Enter no of : 20

Enter no { : 15

Enter no of : 5

Enter no of : 10

Confidence that program is Java: 1

Confidence that program is C++ : 0
```

## 18.6 模糊 C 均

这种聚类技术（Lin 等 [153]）的目标是将向量空间 $\mathbb{R}^k$ 中一个由 $n$ 个向量组成的给定数据集分组：

```

$X=\{\mathbf{x}_0, \mathbf{x}_1, \dots, \mathbf{x}_{n-1}\}$

```

分为 $c$ 个类，使得同一组的数据尽可能相似，不同组的数据尽可能不相似。模糊 C means 通过最小化目标函数来实现这种分类：

```

$J(U,V)=\sum_{i=0}^{n-1}\sum_{j=0}^{c-1}(\mu_{ij})^m\|\mathbf{x}_i-\mathbf{v}_j\|^2$

```

其中 $\mu_{ij}$ 代表数据 $\mathbf{x}_i$ 对类中心 $\mathbf{v}_j$ 的隶属度。量 $\mu_{ij}$ 满足以下条件：

```

$\mu_{ij} \in [0,1] \text{ for } i=0,1,\dots,n-1, \ j=0,1,\dots,c-1$

```

以及

```

$\sum_{j=0}^{c-1}\mu_{ij}=1, \text{ for } i=0,1,\dots,n-1$.

```

此外，$|\mathbf{x}_i-\mathbf{v}_j|$ 是 $\mathbf{x}_i$ 与 $\mathbf{v}_j$ 之间的欧几距离。参数 $m$ 用于控制数据隶属的模糊程度，$m > 1$。指数 $m$ 的最优选择没有理论依据，通常选择值为 2.0。$n \times c$ 矩阵 $U=(\mu_{ij})$ 称为模糊划分矩阵，$V=\{\mathbf{v}_0,\dots,\mathbf{v}_c\}$ 是一组类中心（显然也是 $\mathbb{R}^k$ 中的向量）。模糊 C-means 聚类算法尝试根据给定的标准将集合 $X$ 的有限元素划分为 $c$ 个模糊簇。因此，模糊 C-means 聚类需要预假设类的数量。模糊 C-means 聚类算法如下：

- 1) 初始化隶属矩阵 $U=(\mu_{ij})$ 为随机值使得

# 18.6. 模糊 C-means 聚类 627

2) 计算模糊中心 $v_j$

```

$$\mathbf{v}_j = \frac{\sum_{i=0}^{n-1} (\mu_{ij})^m \mathbf{x}_i}{\sum_{i=0}^{n-1} (\mu_{ij})^m}$$

```

对于 $j = 0, 1, \dots, c-1$。

3) 计算新的距离

```

$d_{ij} = ||\mathbf{x}_i - \mathbf{v}_j||$

```

对于 $i = 0, 1, \dots, n-1$ 和 $j = 0, 1, \dots, c-1$。

4) 更新模糊隶度矩阵 $U = (\mu_{ij})$：如果 $d_{ij} \neq 0$，则

```

$$\mu_{ij} = \frac{1}{\sum_{l=0}^{c-1} (d_{ij}/d_{il})^{2/(m-1)}}$$

```

否则

```

$$\mu_{ij} = 1.$$

```

5) 重复步骤 2) 到 4) 直到达到最小 $J$ 值。

在 C++ 程序中，我们考虑 $\mathbb{R}^3$ 中的四个向量，$m=2$ 以及两个聚类，即 $c=2$。我们进行 20 次迭代。在每个时间步计算 $J(U, V)$ 并因此获得收敛准则被留作了一个练习题。

```cpp
// clustering.cpp
```

```cpp
#include <iostream>
#include <cmath> // 用于 sqrt
using namespace std;

double distance(double* w1, double* w2, int k)
{
    double r = 0.0;
    for(int i=0;i<k; i++) r += (w1[i]-w2[i])*(w1[i]-w2[i]);
    return sqrt(r);
}

int main(void)
{
    int n = 4; // 向量数量
    int k = 3; // 向量长度
double** X = new double[n];
    for(int i=0;i<n; i++) X[i] = new double[k];
    X[0][0] = 1.0; X[0][1] = 1.0; X[0][2] = 0.0;
    X[1][0] = 0.0; X[1][1] = 1.0; X[1][2] = 1.0;
    X[2][0] = 1.2; X[2][1] = 0.9; X[2][2] = 0.1;
```

```cpp
X[3][0] = 0.1; X[3][1] = 1.1; X[3][2] = 0.95;
```

```cpp
int c = 2; // 聚类数量
double** V = new double*[c];
for(int i=0;i<c;i++) { V[i] = new double[k]; }
```

```cpp
double** U = new double*[n];
for(int i=0;i<n;i++) { U[i] = new double[c]; }
U[0][0] = 0.1; U[0][1] = 0.9; U[1][0] = 0.4; U[1][1] = 0.6;
U[2][0] = 0.5; U[2][1] = 0.5; U[3][0] = 0.7; U[3][1] = 0.3;
```

```cpp
double** D = new double*[n]; // 距离
for(int i=0;i<n;i++) { D[i] = new double[c]; }
```

```cpp
// 计算模糊中心
int count = 0;
while(count < 50) {
  for(int j=0;j<c;j++) {
    for(int l=0;l<k;l++) {
      double t1 = 0.0; double t2 = 0.0;
      for(int i=0;i<n;i++) {
        t1 += U[i][j]*U[i][j]*X[i][l]; t2 += U[i][j]*U[i][j]*V[j][l];
      }
      V[j][l] = t1/t2;
    } // 循环 l 
  } // 循环 j结束
  for(int i=0;i<n;i++) {
    for(int j=0;j<c;j++) { 
      D[i][j] = distance(X[i],V[j],k); 
    };
    for(int j=0;j<k;j++) {
      double t3 = 0.0;
      if(D[i][j]==0.0) U[i][j] = 1.0;
      else for(int p=0;p<c;p++) { 
        t3 += D[i][j]*D[i][j]/(D[i][p]*D[i][p]); 
      }
      U[i][j] = 1.0/t3;
    }
  }
  count++;
} // while 结束
```cpp
for(int i=0;i<n;i++) {
  for(int j=0;j<c;j++)
    cout << "U[" << i << "][" << j << "] = " << U[i][j] << endl;
  for(int j=0;j<k;j++)
    cout << "V[" << j << "][" << i << "] = " << V[j] << endl;
  cout << endl;
}
// 释放内存
```cpp
for(int i=0; i<n; i++) { delete X[i]; }
for(int i=0; i<c; i++) { delete V[i]; }
for(int i=0; i<n; i++) { delete U[i]; }
for(int i=0; i<n; i++) { delete D[i]; }
return 0;
```
