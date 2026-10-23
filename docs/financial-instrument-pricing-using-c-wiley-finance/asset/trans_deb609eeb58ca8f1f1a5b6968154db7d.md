

{
    sum += L(i,p)*U(p,j);
}

result(i,j) = sum;
}
}

return result;
}
```

```
// Compute Upper*Lower.
ublas::matrix<double> operator * (
    const ublas::triangular_matrix<double, ublas::upper>& U,
    const ublas::triangular_matrix<double, ublas::lower>& L)
{
    // Rough and Ready, but it works; it is a test of uBLAS::transpose.
    ublas::triangular_matrix<double, ublas::upper> Upper = trans(L);
    ublas::triangular_matrix<double, ublas::lower> Lower = trans(U);

    return Lower*Upper;
}
```

我们可以运行这段代码并看到在所有情况下结果都相同。最后，另一个测试是把原始矩阵从两个乘积中减去，然后取相应的最大范数：

// Look at matrix norms.
ublas::matrix<double> m1 = Corr - UD*LD;
ublas::matrix<double> m2 = Corr - LD*UD;
cout << "A - U*L max error: " << ublas::norm_inf(m1) << endl;
cout << "A - L*U max error: " << ublas::norm_inf(m2) << endl << endl;
```

这些值应该非常小。
一个使用示例是：

// Correlation matrix,
// This is the example in MC book page 145 where we use Cholesky
// decomposition.

unsigned D = 4;
u::matrix<double> Corr (D,D);
Corr(0,0) = Corr(1,1) = Corr(2,2) = Corr(3,3) = 1.0;

Corr(0,1) = Corr(1,0) = 0.5;
Corr(0,2) = Corr(2,0) = 0.2;
Corr(0,3) = Corr(3,0) = 0.01;

Corr(1,2) = Corr(2,1) = 0.01;
Corr(1,3) = Corr(3,1) = 0.30;

Corr(3,2) = Corr(2,3) = 0.30;
std::cout << "Original matrix: " << Corr << std::endl;

u::matrix<double> Backup(Corr);

u::triangular_matrix<double, u::lower> LD(D,D);
u::triangular_matrix<double, u::upper> UD(D,D);

InitLU(Corr, LD, UD);

// Recover original matrix in different ways
Corr = LD * UD;
std::cout << "LD*UD: " << Corr << std::endl;

Corr = UD * LD;
std::cout << "UD*LD: " << Corr << std::endl;

// Look at matrix norms
u::matrix<double> m1 = Backup - UD*LD;
std::cout << "A - U*L max error: " << u::norm_inf(m1) << std::endl;

u::matrix<double> m2 = Backup - LD*UD;
std::cout << "A - L*U max error: " << u::norm_inf(m2) << std::endl;

// Now test Cholesky directly
u::triangular_matrix<double, u::lower> L(D,D);
Cholesky(Backup, L);

u::matrix<double> Product  = L * trans(L);
std::cout << "Cholesky, L*trans(L): " << Product << std::endl;
std::cout << "A - L*trans(L) max error: "
          << u::norm_inf(Backup - Product) << std::endl;

Product  = trans(L)*L;
std::cout << "Cholesky, trans(L)*L: " << Product << std::endl;
std::cout << "A - trans(L)*L max error: "
          << u::norm_inf(Backup - Product) << std::endl;
```

Cholesky 分解也适用于具有复数系数的矩阵；然而，我们需要对代码进行修改（我们需要取转置矩阵元素的复共轭）：

```
template <typename T>
    void CholeskyComplex(const u::matrix<std::complex<T>>& A,
                        u::triangular_matrix<std::complex<T>, u::lower>& L)
{ // Cholesky decomposition

    std::complex<T> sum;
    unsigned N = A.size1();

for (unsigned j = 0; j < N; ++j) // Loop over columns
{
    sum = 0.0;
    for (unsigned k = 0; k < j; ++k)
    {
        // Modification for complex numbers, use conjugate
        sum += L(j, k)*std::conj(L(j, k));
    }
    L(j, j) = std::sqrt(A(j, j) - sum);

    for (unsigned i = j + 1; i < N; ++i) // Rows
    {
        sum = 0.0;
        for (unsigned k = 0; k < j; ++k)
        {
            // Modification for complex numbers
            sum += L(i, k)*std::conj(L(j, k));
        }
        L(i, j) = (A(i, j) - sum) / L(j, j);
    }
}
```

## 26.9.2 LU 分解

该算法将一般矩阵 A 分解为下三角矩阵 L 和上三角矩阵 U 的乘积。该算法在 Dahlquist 和 Björck（1974）以及 Isaacson 和 Keller（1966）中有所记载，例如。结合 uBLAS 的 C++ 代码以自由函数的形式给出：

// LU decomposition: A -> L*U
void InitLU(const ublas::matrix<double>& A,
            ublas::triangular_matrix<double, ublas::lower>& L,
            ublas::triangular_matrix<double, ublas::upper>& U)
{
    double sum;
    unsigned N = A.size1();

    // Common to make all diagonal elements == 1.0
    for (size_t k = 0; k < N; ++k)
    {
        L(k,k) = 1.0;
    }

    for (size_t j = 0; j < N; ++j)      // Loop over columns.
    {
        // U
        for (size_t i = 0; i <= j; ++i)     // Columns.
```
```cpp
{
    sum = 0.0;
    for (size_t k = 0; k < i; ++k)
    {
        sum += L(i,k)*U(k,j);
    }
    U(i,j) = A(i,j) - sum;
}
// L
for (size_t i = j+1; i < N; ++i)    // Rows.
{
    sum = 0.0;
    for (size_t k = 0; k < j; ++k)
    {
        sum += L(i,k)*U(k,j);
    }
    L(i,j) = (A(i,j) - sum) / U(j,j);
}
}
```

计算出矩阵 *L* 和 *U* 后，我们就可以分两步求解矩阵系统；首先分解矩阵 *A*，然后按顺序求解下三角和上三角系统：

$$Ax=b$$

$$(LU)x=b \text{ and } Ly=b \text{ and } Ux=y.$$

该序列步骤的代码为：

```
```cpp
// Solve Ax = b
ublas::vector<double> SolveLU(const ublas::vector<double>& b,
                              const ublas::triangular_matrix<double, ublas::lower>& L,
                              const ublas::triangular_matrix<double, ublas::upper>& U)
{
    size_t N = b.size();
    ublas::vector<double> result(N);

    double sum;

    // Forward sweep Ly = b
    result[0] = b[0] / L(0,0);
    for (size_t i = 1; i < N; ++i)
    {
        sum = 0.0;
        for (size_t k = 0; k < i; ++k)
        {
            sum += L(i,k)*result[k];
        }
        result[i] = (b[i] - sum) / L(i,i);
    }
```

```
// Backward sweep Ux = y
result[N-1] = result[N-1]/U(N-1, N-1);
for (size_t i = N-2; i >= 0 && i < N; --i)
{
    sum = 0.0;
    for (size_t k = i+1; k < N; ++k)
    {
        sum += U(i,k)*result[k];
    }
    result[i] = (result[i] - sum) / U(i,i);
}

return result;
}
```

一个简单的示例是：

```
unsigned N = 4;

// Input for Ax = b
ublas::matrix<double> A(N, N);
ublas::vector<double> b(N);
for (size_t i = 0; i < A.size1(); ++i)
{
    b[i] = 1.0;
    for (size_t j = 0; j < A.size2(); ++j)
    {
        A(i, j) = 0.0;
    }
    A(i,i) = 1.0;
}
std::cout << "Initial matrix A: " << A << std::endl;
cout << "Initial vector b: " << b << endl;

// Determine the L and U matrices.
ublas::triangular_matrix<double, ublas::lower> L(N,N); Init(L, 0.0);
ublas::triangular_matrix<double, ublas::upper> U(N,N); Init(U, 0.0);
InitLU(A, L, U);
cout << "Matrix L: " << L << endl;
cout << "Matrix U: " << U << endl;

// Solve 'Ax=b'.
ublas::vector<double> result = SolveLU(b, L, U);
cout << "Result vector Ax=b: " << result << endl;
```

## 26.9.3 QR 分解

该算法将矩阵 A 分解为酉矩阵 Q 和上三角矩阵 R 的乘积：

A = QR. (26.23)

输出为：

```
[3,3]((-0.512148,0.494524,0.702247),
    (0.384111,-0.599423,0.702247),
    (0.768221,0.629394,0.117041))

[3,3]((7.81025,2.4327,0.128037),
    (0,6.56369,-0.809221),
    (0,0,3.51123))
```

QR 后处理结果

```
Differences of A and Q*R: 2.22045e-16
Differences of trans(Q)*Q and identity I: 1.38778e-16
Differences of trans(Q)*A and R: 1.9984e-15
```

对于更大的矩阵，控制台输出难以阅读，我们可以然后使用我们在第 14 章中介绍的 Excel 驱动程序：

// Start Excel
using NumericMatrix = boost::numeric::ublas::matrix<double>;
ExcelDriver& excel = ExcelDriver::Instance();
excel.MakeVisible(true);            // Default is INVISIBLE!

std::string sheetName("Test Case Q Matrix");
long row = 4; long col = 2;
excel.AddMatrix<NumericMatrix>(Q, sheetName, row, col);

std::string sheetName2("Test Case R Matrix");
excel.AddMatrix<NumericMatrix>(R, sheetName2, row, col);
```

该选项不仅用于可视化目的，而且还允许我们将矩阵和向量数据导出到 Excel，以便在 VBA 或 C# 等中进一步处理。运行代码并可视化输出是有用的。

## 26.10 生成随机数

协方差矩阵（也称为离散矩阵或方差-协方差矩阵）是一个矩阵，其第 (i,j) 位置的元素是随机向量第 i 个和第 j 个元素的协方差。

多元正态分布 N(μ, Σ) 由其均值向量 μ 和协方差矩阵 Σ 指定。协方差矩阵可通过其对角线条目 σ_i² 和相关系数 ρ_ij 隐式指定，使用 ρ_ij = Σ_ij / σ_i σ_j 以矩阵形式：

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_850_0.png)

