
`w_{10}(t=1) = W_{10}(t=0) + \eta(t=0)(x_{1,1}-W_{10}(t=0)) = 0.24`

`w_{20}(t=1) = W_{20}(t=0) + \eta(t=0)(x_{1,2}-W_{20}(t=0)) = 0.20`

`w_{30}(t=1) = W_{30}(t=0) + \eta(t=0)(x_{1,3}-W_{30}(t=0)) = 0.96.`

其中 `\eta(t=0) = 0.6`。考虑到第一个输入向量 `$x_1$`，更新后的权重矩阵为：

```
W(t=1,1) = \begin{pmatrix} 0.08 & 0.92 \\ 0.24 & 0.76 \\ 0.20 & 0.28 \\ 0.96 & 0.12 \end{pmatrix}
```

因此：

```
$$\mathbf{w}_0(t=1) = \begin{pmatrix} 0.08 \\ 0.24 \\ 0.20 \\ 0.96 \end{pmatrix}, \mathbf{w}_1(t=1) = \begin{pmatrix} 0.92 \\ 0.76 \\ 0.28 \\ 0.12 \end{pmatrix}$$
```

对于第三个输入向量 `$x_2$`，我们找到：

```
||w_0(t=1) - x_2||^2 = 1.8656, \quad ||w_1(t=1) - x_2||^2 = 0.6768.
```

因此，权重 `w_1(t=1,1)` 最接近输入向量 `x_2`，即 `j^*=1`（胜出神经元）。因此，我们更新权重矩阵 `W(t,1)` 中的列 `$w_0(t=1,2)$`，并保持列`$w_0(t=1,1)$` 不变。这意味着：

```
W(t=1,2) = \begin{pmatrix} 0.08 & 0.968 \\ 0.24 & 0.304 \\ 0.20 & 0.112 \\ 0.96 & 0.048 \end{pmatrix} \Rightarrow \mathbf{w}_0(t=1,2) = \begin{pmatrix} 0.08 \\ 0.24 \\ 0.20 \\ 0.96 \end{pmatrix}, \mathbf{w}_1(t=1,2) = \begin{pmatrix} 0.968 \\ 0.304 \\ 0.112 \\ 0.048 \end{pmatrix}
```

对于第四个输入向量 `x_3`，我们找到：

```
||w_0(t=1,2) - x_3||^2 = 0.7056, \quad ||w_1(t=1,2) - x_3||^2 = 2.7244.
```

向量 `w_0(t=1,2)` 最接近输入向量 `x_3`，即 `j^*=0`（胜出神经元）。因此，我们更新权重矩阵 `W` 中的列 `$w_0(t=1,2)$`，并保持列`$w_1(t=1,2)$` 不变。所有四个输入向量都已考虑在内。我们找到：

```
W(t=1) = \begin{pmatrix} 0.032 & 0.968 \\ 0.096 & 0.304 \\ 0.680 & 0.112 \\ 0.984 & 0.048 \end{pmatrix} \Rightarrow \mathbf{w}_0(t=1) = \begin{pmatrix} 0.032 \\ 0.096 \\ 0.680 \\ 0.984 \end{pmatrix}, \mathbf{w}_1(t=1) = \begin{pmatrix} 0.968 \\ 0.304 \\ 0.112 \\ 0.048 \end{pmatrix}
```

这是一个 epoch（一次迭代，一次步）。现在将学习率降低为：

$$\eta(t=1) = \frac{1}{1.05}\eta(t=0).$$

对每个输入向量 `x_0, x_1, x_2` 和 `x_3` 重复这些步骤。在第二个 epoch（第二次迭代）后，权重矩阵为：

```
W(t=2) = \begin{pmatrix} 0.016 & 0.980 \\ 0.047 & 0.360 \\ 0.630 & 0.055 \\ 0.999 & 0.024 \end{pmatrix}
```

迭代 100 个 epoch，发现权重矩阵收敛于：

```
W(t=100) \approx \begin{pmatrix} 0.0 & 1.0 \\ 0.0 & 0.5 \\ 1.0 & 0.0 \end{pmatrix}
```

## 13.4 KOHONEN 网络

零列是向量 `x_1` 和 `x_3` 的算术平均值，第一列是向量 `x_0` 和 `x_2` 的算术平均值。在 C++ 程序中，我们可以选择不同数量的权重向量。`t=0` 时的权重向量使用随机数生成器选择1、2、3、4和5。输入向量的数量也可以更改。`int m = 4` 是输入向量的数量。

```cpp
// Haus.cpp
#include <iostream>
#include <cstdlib> // srand, rand
#include <ctime>
using namespace std;
double euclidean(double *vec1,double *vec2,int n)
{
    double dist = 0.0;
    for(int i=0; i<n;i++) dist += (vec1[i]-vec2[i])*(vec1[i]-vec2[i]);
    return dist;
}
double distance(int i,int jstar)
{
    return double(i!=jstar);
    // 如果 i!=jstar返回1.0，如果 i==jstar返回0.0
double h(double d) { return 1.0-d; }
void train(double **W,int cols,double *vec,double rate)
{
    int i,j;
    int win = 0;
    double windist = euclidean(W[0],vec,n);
    for(i=0;i<cols;i++)
    if(euclidean(W[i],vec) < windist) win = i, windist = euclidean(W[i],vec);
    for(i=0;i<cols;i++)
    for(j=0;j<n;j++) W[i][j] += rate*h(distance(i,win))*(vec[j]-W[i][j]);
}
int main(void)
{
    int i, j;
    int T = 10000; // 迭代次数
    double eta = 0.6; // 学习率
    const int m = 4;
    int cols;
```
```cpp
// 训练向量
double x0[m] = {1.0,0.0,0.0,0.0}; double x1[m] = {0.0,0.0,0.0,1.0};
double x2[m] = {1.0,0.0,0.0,0.0}; double x3[m] = {0.0,0.0,1.0,0.0};
cout << "Enter number of columns for weight matrix: "; cin >> cols;
double** W = new double*[cols];
for(i=0;i<cols;i++) W[i] = new double[m];
for(i=0;i<cols;i++)
for(j=0;j<m;j++) W[i][j] = rand()/(double)(RAND_MAX);
for(i=0;i<T;i++)
{
    train(W,cols,x0,eta); train(W,cols,x1,eta);
    train(W,cols,x2,eta); train(W,cols,x3,eta);
    eta /= 1.05; // 学习率降低
}
for(i=0;i<cols;i++)
{
    cout << "W" << i << " = [";
    for(j=0;j<m;j++) cout << W[i][j] << (j==m-1 ? "" : ", ");
    cout << "]" << endl;
}
for(i=0;i<cols;i++) delete[] W[i];
delete[] W;
return 0;
```
```

## 13.4 旅行销员问题

旅行销员问题可能是所有网络和组合优化中最著名的问题。旅行销员从他的家基地 0 号节点出发，希望恰好访问由节点 1,...,n-1 表示的若干城市中的每一个，并返回家中，以最低的旅行成本完成。我们将该问题的任何解决方案称为城市巡游（tour）。如果有 `n` 个城市，就有 `n!` 种可能的巡游，但其中一些是相同的。旅行销员问题是一个通用的核心模型，捕捉了大多数路由问题的组合本质，事实上，大多数其他路由问题都是它的扩展。

人们可以将旅行销员问题描述为一种嵌入的（有向）网络流结构（Ahuja 等人 [2]）。

我们使用 Kohonen 算法解决旅行销员问题。城市的位置给出：

```
x[0] = 10.1, y[0] = 20.2, x[1] = 4.0, y[1] = 7.0
x[2] = 0.1, y[2] = 2.0, x[3] = 0.5, y[3] = 10.7
x[4] = 10.5, y[4] = 0.6, x[5] = 8.0, y[5] = 10.0
x[6] = 12.0, y[6] = 16.0, x[7] = 18.0, y[7] = 8.0.
```

距离由欧几得范数给出。程序 `kohonen.cpp` 的输出为旅行销员问题提供了以下解决方案：

```
0 → 3 → 5 → 1 → 2 → 4 → 7 → 6 → 0.
```

显然，路径 0 → 6 → 7 → 4 → 2 → 1 → 5 → 3 → 0 也是一个解决方案。

# 第 13 章 神经网络

```cpp
// kohonen.cpp
```
```cpp
#include <iostream>
#include <cmath>    // 用于 fabs, exp
#include <cstdlib>
#include <ctime>
#include <iomanip>   // 用于 setprecision
using namespace std;
// 找到数组 d 中具有最小数值的索引
int minimum(double* d, int M)
{
    int m = 0;
    double r = d[0];
    for(int j=1;j<M;j++) if(d[j] < r) { r = d[j]; m = j; }
    return m;
}
// 神经元的横向作用
double map(double a,double b,double c,double s)
{
    double result;
    result = exp(-(fabs(a-c)+fabs(b-d))/(2.0*s*s));
    return result;
}
int main(void)
{
    int N = 8; // 城市数量
    double* x = new double[N]; double* y = new double[N];
    // 城市的坐标
    x[0] = 10.1; x[1] = 4; x[2] = 0.1; x[3] = 0.5;
    x[4] = 10.5; x[5] = 5.0; x[6] = 12.0; x[7] = 18.0;
    y[0] = 20.2; y[1] = 7.0; y[2] = 2.0; y[3] = 10.7;
    y[4] = 0.6; y[5] = 10.0; y[6] = 16.0; y[7] = 8.0;
    int M = 3;
    // 神经元数量
    double* u = new double[M]; double* v = new double[M];
    const double PI = 3.14159;
    // t = 0 时的神经元模式
    for(int j=0;j<M;j++) {
        double k = j; double K = M;
        u[j] = 10.0+10.0*sin(2.0*PI*k/K); // 神经元模式
        v[j] = 10.0+10.0*cos(2.0*PI*k/K); // 神经元模式
    }
    double* dist = new double[M];
    double* delW1 = new double[M]; double* delW2 = new double[M];
    double eta0 = 0.8; // t = 0 时的学习率
```
## 13.4. KOHEN 神经网络

`long T = 15000; // 迭代次数`

`srand((unsigned long) time(NULL)); // 随机数种子`

// 迭代开始
for(long cnt=0;cnt<T;cnt++)
{
    int nrand = rand() % N;
    for(int j=0;j<M;j++) { 
        dist[j] = fabs(u[j]-x[nrand])+fabs(v[j]-y[nrand]);
        int imin = minimum(dist,M);
        double c = cnt; double it = T; double s;
        s = eta0*(1.0-c/(it+10000.0));
        for(int j=0;j<M;j++)
            delW1[j] = 1.0*map(u[j],v[j],u[imin],v[imin],s)*(x[nrand]-u[j]);
            delW2[j] = 1.0*map(u[j],v[j],u[imin],v[imin],s)*(y[nrand]-v[j]);
    }
    for(int j=0;j<M;j++) { u[j] += delW1[j]; v[j] += delW2[j]; }
    // 迭代结束
    cout << endl << endl;
    for(int j=0;j<M;j++) // 显示输出
    {
        cout << "u" << j << " = " << setprecision(3) << u[j] << " ";
        cout << "v" << j << " = " << setprecision(3) << v[j] << endl;
    }
    delete x; delete y; delete u;
    delete delW1; delete delW2; delete dist;
    return 0;
}
