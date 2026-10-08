

![](img/2d1ac831a270b8b08f8b8ec2205913dc_225_0.png)

**图 6.1** 10 只对冲基金的年化平均值和标准差

![](img/2d1ac831a270b8b08f8b8ec2205913dc_225_1.png)

**图 6.2** 10 只对冲基金的风险-收益散点图

配置各种资产以获得平均组合收益，并随后通过多元化降低整体风险。从技术角度来说，对于一个由 $N$ $(\ge 2)$ 个风险资产组成的组合，$i = 1, \dots$，组合预期收益率 $r_p$ 由下公式给出：

```
$$r_p = \sum_{i=1}^{N} w_i \tilde{r}_i \quad (6.1)
```

其中 $\tilde{r}_i$ 是与每个风险资产 $i$ 相关的平均收益率，$w_i$ 是投资在每个风险资产 $i$ 中的单个持仓（或权重）。假设组合是全额投资的，因此每个资产的总持仓始终等于 100%，即权重必须满足以下条件：

```
$$\sum_{i=1}^{N} w_i = 1\quad (6.2)
```

组合方差 $\sigma_p^2$ 由下公式给出：

```
$$\sigma_p^2 = \sum_{i=1}^{N} \sum_{j=1}^{N} w_i w_j \sigma_i \sigma_j \rho_{ij}\quad (6.3)
```

其中 $w_i$ 和 $w_j$ 是权重$\sigma_i$ 和 $\sigma_j$ 是标准差，$\rho_{ij}$ 是资产 $i$ 和 $j$ 收益之间的相关性。注意，对于任意一对随机变量 $X_i$ 和 $X_j$，相关性 $\rho_{ij}$ 可以写为：

```
$$\rho_{ij} = \frac{\sigma_{ij}}{\sigma_i \sigma_j}\quad (6.4)
```

其中 $\sigma_{ij} = \text{cov}(X_i, X_j)$。

因此，组合方差可以写为：

```
$$\sigma_p^2 = \sum_{i=1}^{N} \sum_{j=1}^{N} w_i w_j \sigma_{ij}\quad (6.5)
```

其中，正式地 $\sigma_{ij} = \text{cov}(\tilde{r}_i, \tilde{r}_j)$ 且 $\sigma_p^2 = \text{cov}(\tilde{r}_p, \tilde{r}_p)$。

组合平均收益和方差也可以转换为紧凑的矩阵表示。也就是说，我们可以写组合收益：

```
$$r_p = \sum_{i=1}^{N} w_i \tilde{r}_i = \mathbf{w}^T \mathbf{R}\quad (6.6)
```

其中 $\mathbf{w}^T$ 是矩阵 $\mathbf{w}$ 的*转置*矩阵，它包含了所有单个资产权重 $w_i$，$\mathbf{R}$ 是资产 $i$ 的平均收益向量。$\mathbf{w}, \mathbf{w}^T$ 和 $\mathbf{R}$ 给出：

```
$$\mathbf{w} = \begin{bmatrix} w_1 \\ w_2 \\ w_3 \\ \vdots \\ w_N \end{bmatrix}\quad (6.7)
```

```
$w^T = (w_1 \quad w_2 \quad w_3 \quad \dots \quad w_N) \quad (6.8)$
```

```
$R = \begin{pmatrix} \tilde{r}_1 \\ \tilde{r}_2 \\ \tilde{r}_3 \\ \cdot \\ \vdots \\ \tilde{r}_N \end{pmatrix} \quad (6.9)$
```

尽管 $w^T$ 和 $R$ 是向量，但它们也可以被视为 $(n \times 1)$ 或 $(1 \times n)$ 矩阵。矩阵形式的*组合方差*可以写为：

```
$$\sigma_p^2 = \sum_{i=1}^N \sum_{j=1}^N w_i w_j \sigma_{ij} = w^T \Sigma w \quad (6.10)
```

其中 $\Sigma$ 是单个资产 $i$ 和 $j$ 的*方差-协方差矩阵*，给出：

```
$$\Sigma = \begin{pmatrix} \sigma_1^2 & cov_{12} & cov_{13} & \cdot & cov_{1n} \\ cov_{21} & \sigma_2^2 & cov_{23} & \cdot & \cdot \\ cov_{31} & cov_{32} & \sigma_3^2 & \cdot & \cdot \\ \vdots & \vdots & \vdots & \cdot & \cdot \\ cov_{n1} & \cdot & \cdot & \cdot & \sigma_N^2 \end{pmatrix} \quad (6.11)
```

源码 6.2 显示了 PRet() 和 PVar() 成员函数和方法的实现。

```
SOURCE 6.2: THE PRet() AND PVar() MEMBER FUNCTION AND METHOD IMPLEMENTATIONS

// Optimise.h
#pragma once

#include "Matrix.h"
#include "Stats.h```

```cpp
class Optimise: public Stats
{
    public:
        Optimise() {}
        virtual ~Optimise() {}

    // 成员函数声明
    Matrix PRet(const V2DDV& v); // PRet()
    Matrix PVar(const V2DDV& v); // PVar()
    private:
        // 成员变量声明
    Matrix m_matrix; // Matrix 类的实例
};

// Optimise.cpp
#include "Optimise.h"

Matrix Optimise::PRet(const V2DDV& v)
{
    UINT n = v[0].size()-1;

    // WT 和 R 矩阵
    Matrix WT = Matrix(1, n);
    Matrix R = Matrix(n, 1);

    // 转置权重
    for (UINT i=1; i<=n++)
        WT(1, i) = 1 / n; // 等权重

    // 平均收益率
    double r = Mean(v, 1);

    // R 矩阵
    for (UINT i=1; i<=n++)
        R(i, 1) = r[i-1];

    return WT * R;
}

Matrix Optimise::PVar(const V2DDV& v)
{
    UINT n = v[0].size()-1;

    // w, WT 和 VCV 矩阵
    Matrix w = Matrix(n, 1);
    Matrix WT = Matrix(1, n);
    Matrix VCV = Matrix(n, n);

    // 初始组合权重
    for (UINT i=1; i<=n++)
        w(i, 1) = 1 / n; // 等权重

    // 转置权重
    for (UINT i=1; i<=n++)
        WT(1, i) = 1 / n; // 等权重

    // 协方差矩阵
    double cov = Cov(v);

    // VCV 矩阵
    int k = 0; // 协方差偏移
    for (UINT i=1; i<=n++)
    {
        for (UINT j=1; j<=n++)
        {
            VCV(i, j) = cov[j+k-1];
            if(i == j)
                VCV(i, j) *= n; // 年化方差
        }
        k+=n;
    }

    return WT * VCV * w;
}

// ...
// main.cpp
// ...
// 创建类实例
Matrix thfs;
Optimise optimise;

// 声明调用 GetData()
V2DDV data = thfs.GetData("./data/10_hedge_funds.dat");

// 声明调用 PRet() 和 PVar() 成员函数
Matrix pret = optimise.PRet(data);
Matrix pvar = optimise.PVar(data);

// 输出结果
cout << "\n Port. Ret() = ";
pret.Print();
cout << " Port. Var() = ";
pvar.Print();

// ...
```

源码 6.2 显示对冲基金的年收益和方差分别为 8.52% 和 10.75%。在源码 6.2 中，我们假设了一个等权重组合，并将 `double` 转换了 $n$（见图 6.3）。注意我们将 VCV 矩阵对角线上的每个对冲基金方差乘以了 $n$，即 $VCV(i, j) *= n;$（见图 6.4）。

在源码 6.2 中，我们包含了一个新的 Matrix 类来处理所有矩阵计算。源码 6.3 显示了 Matrix 类的 Matrix.h 和 Matrix.cpp 文件。

# 源码 6.3: Matrix.h AND Matrix.cpp FILES Matrix CLASS

```cpp
// Matrix.h
#pragma once
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_231_0.png)

**图 6.3** $W$ 和 $W^T$ 的等权重

![](img/2d1ac831a270b8b08f8b8ec2205913dc_231_1.png)

**图 6.4** 年化的 VCV 矩阵

```cpp
#include <Utils.h>
#include <cstdlib>
#include <stdio.h>
#include <math.h>

class Matrix
{
public:
    Matrix(); // 默认构造函数
    Matrix(int row_count, int column_count); // 构造函数
    ~Matrix(); // 析构函数

    double& operator(int r, int c); // 重载运算符

    void Print() const; // 打印矩阵

    friend Matrix operator*(const Matrix& a, const Matrix& b); // 矩阵乘矩阵 (*)
    friend Matrix operator*(const Matrix& a, double b); // 矩阵乘浮点数 (*)
    friend Matrix operator*(double b, const Matrix& a); // 浮点数乘矩阵 (*)

    Matrix(const Matrix& a); // 拷贝构造函数
    Matrix& operator=(const Matrix& a); // 赋值运算符

private:
    int rows; // 矩阵行
    int cols; // 矩阵列
    double** p; // 指向 double 矩阵的双指针
};
``````cpp
// Matrix.cpp
#include "Matrix.h"
#include <iostream>
using std::cout;

// 默认构造函数
// 创建一个空的 Matrix 对象
Matrix::Matrix() : p(NULL), rows(0), cols(0)
{}

// 构造函数
// 创建具有特定行和列的空 Matrix 对象
Matrix::Matrix(int row_count, int column_count)
{
    p = NULL; // 空指针
    if (row_count > 0 && column_count > 0)
    {
        rows = row_count;
        cols = column_count;
    }

    p = new double*[rows];

    for (UINT r=0; r<rows; r++)
    {
        p[r] = new double[cols];

        // 初始化为零
        for (UINT c=0; c<cols; c++)
        {
            p[r][c] = 0;
        }
    }
}

// 析构函数
Matrix::~Matrix()
{
    // 删除堆上分配的所有内存
    for (UINT r=0; r<rows; r++)
    {
        delete p[r];
    }
    delete p;
    p = NULL; // 空指针
}

// 拷贝构造函数
Matrix::Matrix(const Matrix& a)
{
    rows = a.rows;
    cols = a.cols;

    p = new double*[a.rows];

    for (int r=0; r <a.rows; r++)
    {
        p[r] = new double[a.cols];

        // 从矩阵 a 拷贝值
        for (UINT c=0; c<a.cols; c++)
        {
            p[r][c] = a.p[r][c];
        }
    }
}
```

