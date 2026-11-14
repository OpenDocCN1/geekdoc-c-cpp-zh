

const T& operator[](int i) const { check_index(i); return data[i]; }
T& operator[](int i) { check_index(i); return data[i]; }
// ...
};

我们当然可以提供一个用于添加此类向量的运算符：

## 清单 5-4：朴素加法运算符

![](img/5682e787fc967e93d7e33e8bac5f58a0_487_0.png)

```
template <typename T>
inline vector<T> operator+(const vector<T>& x, const vector<T>& y)
{
    x.check_size(size(y));
    vector<T> sum(size(x));
    for (int i = 0; i < size(x); ++i)
        sum[i] = x[i] + y[i];
    return sum;
}
```

一个简短的测试程序检查一切是否正常工作：

![](img/5682e787fc967e93d7e33e8bac5f58a0_487_1.png)

```
vector<float> x = {1.0, 1.0, 2.0, -3.0},
        y = {1.7, 1.7, 4.0, -6.0},
        z = {4.1, 4.1, 2.6, 11.0},
        w(4);

cout << "x = " << x << std::endl;
cout << "y = " << y << std::endl;
cout << "z = " << z << std::endl;

w = x + y + z;
cout << "w = x + y + z = " << w << endl;
```

如果按预期工作，它有什么问题？从软件工程角度来看：没有问题。从性能角度来看：问题很多。

以下列表显示在执行语句时，operator+的哪一行执行了哪个操作：

- 1. 为 `x` 和 `y` 的加法创建一个临时变量 `sum`（第 5 行）。
- 2. 执行一个循环，读取 `x` 和 `y`，按元素相加，并将结果写入 `sum`（第 6+7 行）。
- 3. 在返回语句中将 `sum` 复制到一个临时变量，例如 `t_xy`（第 8 行）。
- 4. 当 `sum` 超出作用域时，使用析构函数删除它（第 9 行）。
- 5. 为 `t_xy` 和 `z` 的加法创建一个临时变量 `sum`（第 5 行）。
- 6. 执行一个循环，读取 `t_xy` 和 `z`，按元素相加，并将结果写入 `sum`（第 6+7 行）。
- 7. 在返回语句中将 `sum` 复制到一个临时变量，例如 `t_xyz`（第 8 行）。
- 8. 删除 `sum`（第 9 行）。
- 9. 删除 `t_xy`（第二次加法后）。
- 10. 执行一个循环，读取 `t_xyz` 并写入 `w`（在赋值中）。
- 11. 删除 `t_xyz`（赋值后）。

诚然，这是最坏情况；然而，这只发生在非常老的编译器上。现代编译器通过静态代码分析执行更多优化并优化返回值（§2.3.5.3），从而避免将副本复制到临时变量 `t_xy` 和 `t_xyz`。优化后的版本仍然执行：

- 1. 为 `x` 和 `y` 的加法创建一个临时变量 `sum`（为区分，我们称其为 `sum_xy`）（第 5 行）。
- 2. 执行一个循环，读取 `x` 和 `y`，按元素相加，并将结果写入 `sum`（第 6+7 行）。
- 3. 为 `sum_xy` 和 `z` 的加法创建一个临时变量 `sum`（为区分，`sum_xyz`）（第 5 行）。
- 4. 执行一个循环，读取 `sum_xy` 和 `z`，相加，并将结果写入 `sum_xyz`（第 6+7 行）。
- 5. 删除 `sum_xy`（第二次加法后）。
- 6. 将数据从 `sum_xyz` 移动到 `w`（在赋值中）。
- 7. 删除 `sum_xyz`（赋值后）。

我们对维度为 n 的向量执行了多少操作？

- 2n 次加法；
- 4n 次读取；
- 2n 次写入；
- 2 次内存分配；以及
- 2 次内存释放。

相比之下，如果我们可以编写一个单循环或内联函数：

单击此处查看代码图像

```
template <typename T>
void inline add3(const vector<T>& x, const vector<T>& y,
                 const vector<T>& z, vector<T>& sum)
{
    x.check_size(size(y));
    x.check_size(size(z));
    x.check_size(size(sum));
    for (int i = 0; i < size(x); ++i)
        sum[i] = x[i] + y[i] + z[i];
}
```

此函数执行：

- 2n 次加法；
- 3n 次读取；以及
- n 次写入。

此函数的调用：

```
add3(x, y, z, w);
```

这当然不如运算符表示法优雅。它也更容易出错：我们需要查看文档以了解第一个或最后一个参数是否包含结果。使用运算符时，语义是明确的。

在高性能软件中，程序员倾向于为每个重要操作实现硬编码版本，而不是从较小的表达式自由组合它们。原因显而易见；我们的运算符实现额外执行了：

- n 次读取；
- n 次写入；
- 2 次内存分配；以及
- 2 次内存释放。

好消息是我们没有执行额外的算术运算。坏消息是上述操作更昂贵。在现代计算机上，将大量数据从内存传输或传输到内存所需的时间远多于执行定点或浮点算术运算。

不幸的是，科学应用中的向量往往相当长，通常大于平台的缓存，并且向量必须非常频繁地从主内存传输到主内存。在图 5-1 中，我们象征性地描绘了内存层次结构。顶部的芯片代表处理器，其下方的蓝色芯片代表 L1 缓存，磁盘代表 L2，软盘代表主内存，磁带代表虚拟内存。层次结构由靠近处理器的小型快速内存和大型慢速内存组成。当从慢速内存读取一个数据项时（在第二个（蓝色）磁带中标记，副本保存在每个更快的内存中（第二个软盘，第一个磁盘，第一个蓝色 L1 缓存芯片）。

对于较短的向量，数据可能驻留在 L1 或 L2 缓存中，数据传输不那么关键。但随后，分配和释放会成为严重的减速因素。

![](img/5682e787fc967e93d7e33e8bac5f58a0_491_0.png)

图 5-1：内存层次结构

## 5.3.2 表达式模板类

表达式模板（ET）的目的是保留原始运算符表示法，而不引入由临时变量造成的开销。该技术由 Todd Veldhuizen 和 Daveed Vandevoorde 独立发现。

=> c++11/expression_template_example.cpp

为了避免在优雅性和性能之间做选择，我们引入一个新类，表示两个向量的和（在新类中引用）。加法不再返回向量，而是返回这个新类的对象：

单击此处查看代码图像

```
template <typename T>
class vector_sum
{
public:
    vector_sum(const vector<T>& v1, const vector<T>& v2)
        : vl{v1}, v2{v2} {}
private:
    const vector<T>& vl, &v2;
};
```

```
template <typename T>
vector_sum<T> operator+(const vector<T>& x, const vector<T>& y)
{
    return {x, y};
}
```

现在我们可以写 x + y，但还不能写 w = x + y。问题不仅在于赋值尚未定义；我们还没有为 vector_sum 提供足够的功能来在赋值中执行有用的操作。因此，我们首先扩展 vector_sum，使其看起来像一个向量本身：

单击此处查看代码图像

```
template <typename T>
class vector_sum
{
public:
    // ...
    friend int size(const vector_sum& x) { return size(x.vl); }

    T operator[](int i) const { return vl[i] + v2[i]; }
private:
    const vector<T>& vl, &v2;
};
```

这个类中有趣的函数是括号运算符：当访问第 i 个条目时，我们即时计算操作数的第 i 个条目的和。

在括号运算符中计算按元素求和的缺点是，当条目被多次访问时会重复计算。例如，在矩阵向量乘法中会发生这种情况，如：A * (x+y)。因此，对于某些操作，预先计算向量和而不是在访问运算符中按元素计算可能更有益。

要计算 w = x + y，我们还需要为 vector_sum 提供一个赋值运算符：

单击此处查看代码图像

```
template <typename T> class vector_sum; // forward declaration
template <typename T>
class vector
{
    // ...
    vector& operator=(const vector_sum<T>& that)
    {
        check_size(size(that));
        for (int i = 0; i < my_size; ++i)
            data[i] = that[i];
        return *this;
    }
};
```

赋值遍历当前对象的数据和参数 that 的数据。由于后者是 vector_sum，表达式 that[i] 计算按元素求和，这里是 x[i] + y[i]。因此，与清单 5-4 中朴素实现所执行的相反，w = x + y 的评估现在：

- 只有一个循环；
- 没有临时向量；
- 没有额外的内存分配和释放；以及
- 没有额外的数据读取和写入。

实际上，执行的操作与循环中的相同：

单击此处查看代码图像

```
for (int i = 0; i < size(w); ++i)
w[i] = x[i] + y[i];
```

创建 vector_sum 对象的成本可以忽略不计。该对象将保留在堆栈上，不需要内存分配。即使是创建对象的这点小努力，通常也会被大多数具有体面静态代码分析的编译器优化掉。

当我们添加三个向量时会发生什么？清单 5-4 中的朴素实现返回一个向量，该向量可以添加到另一个向量。我们的方法返回一个 vector_sum，而我们没有针对
