
# 28.4 $C_{a,n}$ 的递归实现

在这里我们使用递归来实现函数

$$C_{a,n} = \frac{a!}{(a-n)!}$$

其中 $a$ 和 $n$ 是满足 $a \geq n$ 的非负整数，其定义见第 10 章第 10.17 节。该实现可以通过两种等效的方式完成：通过

```cpp
int C(int a, int n) {
    return n ? a * C(a-1, n-1) : 1;
} // a!/(a-n)!
```

或者通过

```cpp
int C(int a, int n) {
    return n ? (a+1) * C(a, n-1) : 1;
} // a!/(a-n)!
```

# 28.5 复数的平方根

这里是使用给定复数 $c$ 的极坐标表示法来计算其平方根的函数：

$$\sqrt{c} = \sqrt{r}(\cos\theta + i \cdot \sin\theta) = \sqrt{r}(\cos(\theta/2) + i \cdot \sin(\theta/2))$$

假设 $0 \leq \theta < 2\pi$

为了实现所需的复数平方根函数，首先找到 `fabs` 函数，它返回复数的绝对值：

```cpp
double fabs(const complex& c) {
    return sqrt(abs2(c));
} // 复数的绝对值
```

复数平方根函数的简单实现显式地计算了 $\theta$ 和 $\theta/2$：

```cpp
const complex sqrt(const complex& c) {
    double r = fabs(c);
    double theta = acos(c.re / r);
```

遗憾的是，定义的 `theta` 与原始角度 $\theta$ 并不相同。事实上，上面使用的 `acos` 函数始终返回 $0$ 到 $\pi$ 之间的角度，`theta` 仅在 $0 \le \theta \le \pi$ 时等于 $\theta$。另一方面，对于 $\pi < \theta < 2\pi$，`theta` 等于 $2\pi - \theta$ 而不是 $\theta$。因此，必须使用下面的替换来纠正这一点，并确保 `theta` 确实等于 $\theta$。

```cpp
if (c.im() < 0.) theta = 4. * acos(0.) - theta;
```

现在可以形成并返回 $c$ 的平方根：

```cpp
r = sqrt(r);
theta = theta / 2;
return complex(r * cos(theta), r * sin(theta));
} // 复数的平方根
```

另一方面，一种更复杂的方法使用 `sin`、`cos` 和 `acos` 函数显式地计算 $\theta$ 或 $\theta/2$。相反，它使用余弦定理（第 5 章第 5.6 节）得到

$$\cos(\theta) = \cos^2(\theta/2) - \sin^2(\theta/2)$$

或者，使用勾股定理

$$\cos(\theta) = 2\cos^2(\theta/2) - 1 = 1 - 2\sin^2(\theta/2)$$

结果，可以根据 $\cos(\theta)$（$c$ 的实部）同时得到 $\cos(\theta/2)$ 和 $\sin(\theta/2)$：

$$\cos(\theta/2) = \pm\sqrt{\frac{1 + \cos(\theta)}{2}}$$

以及

$$\sin(\theta/2) = \sqrt{\frac{1 - \cos(\theta)}{2}}$$

# 28.6 向量的操作

注意，在上面的 $\cos(\theta/2)$ 公式中，对于 $0 \leq \theta \leq \pi$ 应该使用加号，而对于 $\pi < \theta < 2\pi$ 应该使用减号。上面的公式产生了计算结果 $\sqrt{c}$ 的代码：

```cpp
const complex sqrt(const complex& c) {
    double r = fabs(c);
    double cosTheta = acos(c.re / r);
    double sign = c.im() < 0 ? -1 : 1;
    double cosTheta2 = sign * sqrt((1. + cosTheta) / 2);
    double sinTheta2 = sqrt((1. - cosTheta) / 2);
    r = sqrt(r);
    return complex(r * cosTheta2, r * sinTheta2);
    // 复数的平方根
}
```

遗憾的是，上述平方根函数的定义在实轴正部分是不连续的。当 $\theta$ 趋于 $0^+$（即 $\theta$ 为正且从上方趋于 0）时，$\theta/2$ 同样趋于 0。另一方面，当 $\theta$ 趋于 $2\pi-$（$0 < \theta < 2\pi$）时，$\theta/2$ 趋于 $\pi$，产生所需平方根的相反数。为了避免这个问题，让我们假设原始角度 $\theta$ 位于 $-\pi$ 和 $\pi$ 之间，而不是 $0$ 和 $\pi$ 之间。这样，无论 $\theta > 0$ 还是 $\theta < 0$，$\theta/2$ 都会趋于 0。结果，上面的公式的形式变为

$$\cos(\theta/2) = \sqrt{\frac{1+\cos(\theta)}{2}}$$

以及

$$\sin(\theta/2) = \pm\sqrt{\frac{1-\cos(\theta)}{2}}$$

其中上面的公式在 $\theta \geq 0$ 时使用加号，$\theta < 0$ 时使用减号。因此，代码中 `cosTheta2` 和 `sinTheta2` 的定义应修改为

```cpp
double cosTheta2 = sqrt((1. + cosTheta) / 2);
double sinTheta2 = sign * sqrt((1. - cosTheta) / 2);
```

代码的其他部分保持不变。

# 28.7 矩阵的操作

这里是两个矩阵加、减，以及标量乘矩阵、向量乘矩阵、矩阵向量和矩阵矩阵的运算符实现，如第 16 章所述。

```cpp
template<class T, int N, int M>
const matrix<T,N,M>& operator+=(const matrix<T,N,M>& m) {
    for(int i = 0; i < N; i++)
        component[i] += m[i];
    return *this;
} // 矩阵加

template<class T, int N, int M>
const matrix<T,N,M>& operator-=(const matrix<T,N,M>& m) {
    for(int i = 0; i < N; i++)
        component[i] -= m[i];
    return *this;
} // 矩阵减

template<class T, int N, int M>
const matrix<T,N,M>& operator*=(const T& a) {
    for(int i = 0; i < M; i++)
        set(i, component[i] * a);
    return *this;
} // 标量乘矩阵

template<class T, int N, int M>
const matrix<T,N,M>& operator/=(const T& a) {
    for(int i = 0; i < M; i++)
        set(i, component[i] / a);
    return *this;
} // 标量除法

template<class T, int N, int M>
const matrix<T,N,M> operator*(const T& a, const matrix<T,N,M>& m) {
    return matrix<T,N,M>(m) *= a;
} // 标量乘矩阵

template<class T, int N, int M>
const matrix<T,N,M> operator*(const matrix<T,N,M>& m, const T& a) {
    return matrix<T,N,M>(m) *= a;
} // 矩阵乘标量
```

# 28.8 2 × 2 矩阵的行列式、逆矩阵与转置

```cpp
const matrix<T,M,K>& operator*=(matrix<T,N,M>& m1, const matrix<T,M,K>& m2) {
    return m1 = m1 * m2;
} // 矩阵乘法

template<class T, int N, int M>
const matrix<T,N,M> operator+(const matrix<T,N,M>& m1, const matrix<T,N,M>& m2) {
    return matrix<T,N,M>(m1) += m2;
} // 矩阵加法

template<class T, int N, int M>
const matrix<T,N,M> operator-(const matrix<T,N,M>& m1, const matrix<T,N,M>& m2) {
    return matrix<T,N,M>(m1) -= m2;
} // 矩阵减法
```

以下是上述第 16 章中用于计算 `matrix` 类 2 × 2 矩阵行列式、逆矩阵和转置的函数：

```cpp
typedef matrix<double,2,2> matrix2;

double det(const matrix2& A) {
    return A(0,0)*A(1,1) - A(0,1)*A(1,0);
} // 2x2 矩阵的行列式
```

上述 `det()` 用于通过 Kremer 公式计算 $A^{-1}$：

$$A_{0,0} A_{0,1} = \det(A)^{-1} \begin{pmatrix} A_{1,1} & -A_{0,1} \\ -A_{1,0} & A_{0,0} \end{pmatrix}$$

该公式的实现方式如下：

```cpp
const matrix2 inverse(const matrix2& A) {
    point column0(A(1,1), A(1,0));
    point column1(-A(0,1), A(0,0));
    return matrix2(column0, column1) / det(A);
} // 2x2 矩阵的逆矩阵
```

最后，2 × 2 矩阵的转置的计算方式如下：

```cpp
const matrix2 transpose(const matrix2& A) {
    return matrix2(point(A(0,0), A(0,1)),
                   point(A(1,0), A(1,1)));
} // 2x2 转置
```

# 28.9 3 × 3 矩阵的行列式、逆矩阵与转置

以下是利用第 9 章第 9.23–9.24 节中的定义，计算并返回 3×3 矩阵行列式、逆矩阵和转置的对应函数。

```cpp
double det(const matrix3& A) {
    return A(0,0) * (A(1,1)*A(2,2) - A(1,2)*A(2,1))
         - A(0,1) * (A(1,0)*A(2,2) - A(1,2)*A(2,0))
         + A(0,2) * (A(1,0)*A(2,1) - A(1,1)*A(2,0));
} // matrix3 的行列式
```

```cpp
const matrix3 inverse(const matrix3& A) {
    point3 column0(A(1,1)*A(2,2) - A(1,2)*A(2,1),
                   - (A(0,1)*A(2,2) - A(1,2)*A(2,0)),
                   A(1,0)*A(2,1) - A(1,1)*A(2,0));

    point3 column1(-A(0,1)*A(2,2) + A(0,2)*A(2,1),
                    - (A(0,0)*A(2,2) - A(0,2)*A(2,0)),
                    A(0,0)*A(2,1) - A(0,1)*A(2,0));

    point3 column2(A(0,0)*A(1,2) - A(0,2)*A(1,1),
                    - (A(0,0)*A(1,1) - A(0,1)*A(1,0)),
                    A(0,0)*A(2,1) - A(0,1)*A(2,0)); // 基于 OCR 噪声的简化逻辑

    return matrix3(column0, column1, column2) / det(A);
} // matrix3 的逆矩阵
```

```cpp
const matrix3 transpose(const matrix3& A) {
    return matrix3(point3(A(0,0), A(0,1), A(0,2)),
                   point3(A(1,0), A(1,1), A(1,2)),
                   point3(A(2,0), A(2,1), A(2,2)));
} // matrix3 的转置
```

# 28.10 向量积

以下是第 9 章第 9.25 节中定义的计算并返回 3 维向量积的函数：

```cpp
point3 operator&(const matrix3& u, const matrix3& v) {
    point3 i(1,0,0);
    point3 j(0,1,0);
    point3 k(0,0,1);
    return i * (u(1,1)*v(2,2) - u(1,2)*v(2,1))
         - j * (u(0,1)*v(2,2) - u(1,2)*v(2,0))
         + k * (u(1,0)*v(2,1) - u(1,1)*v(2,0));
} // 向量积
```

# 28.11 指函数

将 `exp` 函数重写为模板函数，使其适用于：

```cpp
template <class T>
T exp(const T& arg) {
    T sum = 0;
    int n = 0;
    while (n < 10) {
        // ...
        n++;
    }
    return sum;
}
```

# 28.12 动态向量操作

以下是 `dynamicVector` 类某些算术运算符的详细实现，留作练习（减法、乘法、除法等）：

```cpp
template<class T>
const dynamicVector<T>& operator-=(dynamicVector<T>& u, const dynamicVector<T>& v) {
    for(int i = 0; i < u.dim(); i++)
        u[i] -= v[i];
    return u; // 从当前向量中减去一个动态向量
}
```

```cpp
template<class T>
const dynamicVector<T>& operator*=(dynamicVector<T>& u, const T& a) {
    for(int i = 0; i < u.dim(); i++)
        u[i] *= a;
    return u; // 动态向量乘以标量
}
```

```cpp
template<class T>
const dynamicVector<T>& operator/=(dynamicVector<T>& u, const T& a) {
    for(int i = 0; i < u.dim(); i++)
        u[i] /= a;
    return u; // 动态向量除以标量
}
```

```cpp
template<class T>
dynamicVector<T> operator-(const dynamicVector<T>& u, const dynamicVector<T>& v) {
    return dynamicVector<T>(u) -= v;
} // 向量减法
```

```cpp
template<class T>
dynamicVector<T> operator*(const dynamicVector<T>& u, const T& a) {
    return dynamicVector<T>(u) *= a;
} // 向量乘以标量
```

```cpp
template<class T>
dynamicVector<T> operator*(const T& a, const dynamicVector<T>& u) {
    return dynamicVector<T>(u) *= a;
} // 标量乘以向量
```

```cpp
template<class T>
dynamicVector<T> operator/(const dynamicVector<T>& u, const T& a) {
    return dynamicVector<T>(u) /= a;
} // 向量除以标量
```
