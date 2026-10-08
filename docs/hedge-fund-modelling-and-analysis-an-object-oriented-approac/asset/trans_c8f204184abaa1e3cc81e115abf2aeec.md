

```cpp
Matrix& Matrix::operator=(const Matrix& a)
{
    rows = a.rows;
    cols = a.cols;
    p = new DBL*[a.rows];

    for (UINT r=0; r<a.rows; r++)
    {
        p[r] = new DBL[a.cols];
    }

    // 从 Matrix a拷贝值
    for (UINT r=0; r<a.rows; r++)
    {
        for (UINT c=0; c<a.cols; c++)
        {
            p[r][c] = a.p[r][c];
        }
    }

    return *this;
}

// 重载运算符 ()
// 注意：索引从 1 开始，而不是 0 开始
double& Matrix::operator()(const int r, const int c)
{
    if (p != NULL && r >= 0 && r <= rows && c > 0 && c <= cols)
    {
        return p[r-1][c-1];
    }
    else
    {
        cout << "\n下标越界!\n";
    }
}

// 重载运算符 *
Matrix* operator*(const Matrix& a, const Matrix& b)
{
    // 检查维度是否匹配
    if (a.cols == b.rows)
    {
        Matrix res(a.rows, b.cols);

        for (UINT r=0; r<a.rows; r++)
        {
            for (UINT c_res=0; c_res<b.cols; c_res++)
            {
                for (UINT c=0; c<a.cols; c++)
                {
                    res.p[r][c_res] += a.p[r][c] * b.p[c][c_res];
                }
            }
        }
        return res;
    }
    else 
    {
        cout << "\n矩阵维度不匹配! \n";
    }
    // 返回一个空矩阵
    // (不应该发生，但为了安全起见)
    return Matrix();
}

// 矩阵乘以双精度浮点数 (*)
Matrix operator*(const Matrix& a, const Dbl b)
{
    Matrix res = a;
    res.Multiply(b);
    return res;
}

// 双精度浮点数乘以矩阵 (*)
Matrix operator*(const Dbl b, const Matrix& a)
{
    Matrix res = a;
    res.Multiply(b);
    return res;
}

// 打印矩阵
void Matrix::Print() const
{
    if (p != NULL) {
        printf(" ");
        for (UINT r=0; r<rows; r++) {
            if (r > 0) {
                printf(" ");
            }
            for (UINT c=0; c<cols-1; c++) {
                printf("%.3f ", p[r][c]);
            }
            if (r < rows-1)
            {
                printf("%.3f", p[r][cols-1]);
            }
            else {
                printf("%.3f\n", p[r][cols-1]);
            }
        }
    } else {
        // 矩阵为空
        printf("*\n");
    }
}
```

我们在 `Matrix` 类中使用了指针，并在这里简要讨论了它们的实现，但请注意，对指针的完整解释超出了本书的范畴。

指针是一个对象，其值通过地址引用存储在内存其他地方（即“指向”）另一个值。指针引用内存中的一个位置，而获取存储在该位置的值的值被称为解引用指针。指向数据的指针可以显著提高诸如遍历矩阵等重复操作的性能。在时间上上，拷贝和解引用指针通常比拷贝和访问指针所指向的数据要便宜得多。每当程序需要动态分配内存时，C++ 均提供了 `new` 和 `delete` 运算符。动态内存使用 `new` 运算符分配，并返回指向新分配的内存块开头的指针，例如：

```cpp
double *ptr; 或
ptr = new double[5];
```

在第二种情况下，系统动态为 `double` 类型的元素分配空间，并返回指向序列第一个元素的指针，该指针赋值给 `ptr`（一个指针）。因此，`ptr` 现在指向一个具有五个 `double` 类型元素空间的有效内存块。在源码 6.3 中，我们如下声明了一个指针 `ptr`：

```cpp
DBL** p;
```

这实际上是一个双级指针。由于我们正在处理二维数组，所以我们使用了双级指针。本质上，我们在说：`DBL**` 是指向 `DBL*` 的指针，而 `DBL*` 是指向 `DBL` 的指针，告诉我们要处理多少个指针。因此，我们可以访问数组的行，例如：

```cpp
p = new DBL*[rows];
```

通过以下代码访问列：

```cpp
p[r] = new double[cols];
```

然而，计算机内存是有限的资源，可能会被耗尽。因此，无法保证所有使用 `new` 运算符分配内存的请求都能获得系统授予。在大多数情况下，动态分配的内存只需要程序运行中的特定时期；一旦不再需要，就可以释放它，以便内存供其他请求使用。这就是 `delete` 运算符的目的，例如：

```cpp
delete ptr;
delete[] ptr;
```

第一条语句释放使用 `new` 分配的单个元素的内存，第二条语句释放使用括号 `[]` 分配的数组的内存。在源码 6.3 中，我们在析构函数中显式删除了所有分配的内存。

注意源码 6.3，我们首次引入了拷贝构造函数和赋值运算符。拷贝构造函数是类的一种特殊构造函数，用于创建现有实例的拷贝。在源码 6.3 中，我们将拷贝构造函数声明为：

```cpp
Matrix(const Matrix& a);
```

如果你不显式声明拷贝构造函数，编译器会隐式地为你提供一个。隐式拷贝构造函数对源对象进行成员级的拷贝。默认提供的拷贝构造函数在许多情况下是足够的，但如果对象包含原始指针，这会导致对象的析构。赋值运算符允许我们使用 `=` 将一个实例赋值给另一个。例如：

```cpp
AClass m1, m2;
m1 = m2; // 将 m2 赋值给 m1
```

在源码 6.3 中，我们将赋值运算符声明为：

```cpp
Matrix& operator=(const Matrix& a);
```

如果你不显式声明赋值构造函数，编译器会隐式地提供一个。隐式赋值运算符对源对象的每个成员进行赋值。默认提供的赋值运算符在许多情况下是足够的，但如果对象包含原始指针，这会导致对象的析构。通常情况下，每当你创建自己的拷贝构造函数时，也需要编写一个赋值运算符。注意赋值运算符的返回类型应该是引用，即：

```cpp
AClass& AClass::operator=(const AClass& other)
{
    a = other.a;
    b = other.b;
    c = other.c;
    return *this;
}
```

在这种情况下，我们只是返回对象的引用，即：

```cpp
return *this;
```

如果你尝试在一个返回类型为 `Type` 而不是 `Type&` 的函数上返回 `this`，编译器将尝试拷贝对象并立即调用析构函数，这通常不是想要的行为。因此，源码 6.3 中的返回类型应该是引用 (&)。

在源码 6.3 中，我们引入了 `Matrix` 类的多个友元，以便我们执行相关的矩阵操作 (*)，即矩阵乘以矩阵以及标量乘法。即：

```cpp
friend Matrix operator*(const Matrix& a, const Matrix& b);
friend Matrix operator*(const Matrix& a, const DBL& b);
friend Matrix operator*(const DBL b, const Matrix& a);
```

我们在第 1 章中曾遇到过友元；友元可以访问声明其友元的类的私有和保护成员。友元允许类具有更好的封装，因为它授予了原本必须公开的实现部分的访问。这种封装的增加是以类之间紧密耦合为代价的。

## 均方差优化

马科维的工作最终导致了均方差组合优化的开发⁵，这是一种在给定组合风险水平下实现预期收益率的方法。给定目标收益率 r*，均方差优化问题可以如下求解：

```
min \frac{1}{2}w^T\Sigma w
```

受限于条件：

```
w^TR = r*
\sum_{i=1}^N w_i = 1
```

一个组合是前沿组合，如果它在给定的预期收益下最小化差，即前沿组合解决了以下优化问题：

```
min \frac{1}{2}w^T\Sigma w
```

受限于条件：

```
w^TR = r*
w^T\1 = 1
```

> 这种技术被称为二次规划 (QP)，涉及对多个变量的二次函数进行优化（最小化或最大化），受限于这些变量的线性约束。在这种情况下，组合方差是权重 w_i 的二次函数。

