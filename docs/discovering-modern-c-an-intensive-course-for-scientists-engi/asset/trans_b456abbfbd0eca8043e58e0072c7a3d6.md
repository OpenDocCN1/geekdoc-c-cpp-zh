

public:
 // ...
 friend int size(const vector_sum& x) { return size(x.v1); };
 T operator[](int i) const { return v1[i] + v2[i]; }
 private:
 const vector<T>& v1, &v2;
 };

这个类中最有趣的函数是括号运算符：当访问第 i 个元素时，我们即时计算操作数的第 i 个元素之和。

在括号运算符中计算逐元素求和的缺点是，当元素被多次访问时会出现重复计算。例如，在矩阵向量乘法中计算 A * (x+y) 时就会发生这种情况。因此，对于某些操作，提前求出向量和而不是在访问运算符中逐元素计算可能更有益。

为了求出 w = x + y，我们还需要为 vector_sum 提供一个赋值运算符：

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

该赋值运算符遍历当前对象的数据以及参数 that 的数据。由于后者是 vector_sum，表达式 that[i] 计算一个逐元素求和，即 x[i] + y[i]。因此，与 Listing 5-4 中朴素实现所执行的操作相比，w = x + y 的求值现在具有：

- 只有一个循环；
- 没有临时向量；
- 没有额外的内存分配和释放；以及
- 没有额外的数据读写。

实际上，执行的操作与以下循环相同：

```
for (int i = 0; i < size(w); ++i)
 w[i] = x[i] + y[i];
```

创建 vector_sum 对象的开销可以忽略不计。该对象将保留在栈上，不需要内存分配。即使是创建对象所需的这点小开销，通常也会被大多数具有体面静态代码分析能力的编译器优化掉。

当我们相加三个向量时会发生什么？Listing 5-4 中朴素的实现返回一个向量，该向量可以与另一个向量相加。我们的方法返回一个 vector_sum，但我们没有为 vector_sum 和 vector 提供加法。因此，我们需要另一个表达式模板类和相应的操作：

```
template <typename T>
class vector_sum3
{
public:
    vector_sum3(const vector<T>& v1, const vector<T>& v2,
                const vector<T>& v3)
        : v1(v1), v2(v2), v3(v3)
    { ... }

    T operator[](int i) const { return v1[i] + v2[i] + v3[i]; }

private:
    const vector<T>& v1, &v2, &v3;
};

template <typename T>
vector_sum3<T> inline operator+(const vector_sum<T>& x,
                                const vector<T>& y)
{
    return {x.v1, x.v2, y};
}
```

此外，vector_sum 必须将我们的新加法运算符声明为友元以访问其私有成员，而 vector 需要为 vector_sum3 提供赋值运算。这变得越来越令人烦恼。另外，如果我们先执行第二个加法会怎样：w = x + (y + z)？那么我们需要另一个加法运算符。如果某些向量与标量相乘会怎样，例如 w = x + dot(x, y) * y + 4.3 * z，而这个标量积也通过 ET 实现？我们的实现工作将陷入组合爆炸，我们需要一个更灵活的解决方案，我们将在下一节中介绍。

## 5.3.3 泛型表达式模板

到目前为止，我们从一个特定的类（vector）开始，逐步泛化实现。虽然这有助于我们理解机制，但我们现在直接转向适用于任意向量类型及其视图的通用版本：

```
template <typename V1, typename V2>
inline vector_sum<V1, V2> operator+(const V1& x, const V2& y)
{
    return {x, y};
}
```

我们现在需要一个带有任意参数的表达式类：

```
template <typename V1, typename V2>
class vector_sum
{
public:
    vector_sum(const V1& v1, const V2& v2) : v1(v1), v2(v2) {}
    ??? operator[](int i) const { return v1[i] + v2[i]; }

private:
    const V1& v1;
    const V2& v2;
};
```

这相当直接。唯一的问题是 operator[] 应该返回什么类型。为此，我们必须在每个类中定义 value_type（外部类型特征会更灵活，但我们希望在这里尽可能简单）。在 vector_sum 中，我们可以取第一个参数的 value_type，而该类型本身可以从另一个类中获取。只要整个应用程序中的标量类型相同，这是一个可接受的解决方案。然而，我们在 3.10 节中看到，如果不注意结果类型，混合参数可能会产生完全荒谬的结果。为了应对混合运算，我们取参数的 value types 的 common_type_t：

```
template <typename V1, typename V2>
class vector_sum
{
    // ...
    using value_type = std::common_type_t<typename V1::value_type,
                                          typename V2::value_type>;

    value_type operator[](int i) const { return v1[i] + v2[i]; }
};
```

如果我们的 vector_sum 类不需要显式声明 value_type，可以在 C++14 中使用 decltype(auto) 作为返回类型，并将类型推断完全交给编译器。相比之下，当模板用 vector_sum 本身实例化时，后置返回类型不起作用，因为这会产生对自身的依赖。

为了将不同种类的表达式赋值给向量类，我们还应该泛化赋值运算符：

```
template <typename T>
class vector
{
public:
    template <typename Src>
    vector& operator=(const Src& that)
    {
        check_size(size(that));
        for (int i = 0; i < my_size; ++i)
        data[i] = that[i];
        return *this;
    }
};
```

这个赋值运算符接受每种类型，除了 vector<T>，我们需要为其提供专用的拷贝赋值运算符。为了避免代码冗余，我们可以实现一个执行实际拷贝的方法，并从通用赋值和拷贝赋值中调用它。

## 表达式模板的优势：

尽管 C++ 中运算符重载的可用性产生了记号上更简洁的代码，但科学界拒绝放弃使用 Fortran 编程或直接在 C/C++ 中实现循环。原因是传统的运算符实现开销太大。由于创建临时变量以及复制向量和矩阵对象的开销，C++ 无法与用 Fortran 编写的程序的性能竞争。随着泛型和表达式模板的引入，这一问题已得到解决。现在我们可以以记号上方便的方式编写极其高效的科学程序。

## 5.4 元调优：编写你自己的编译器优化

编译器技术在进步，提供的优化技术也越来越多。理想情况下，我们都以最简单、最易读的方式编写软件，编译器从中生成最优的可执行文件。我们只需要一个更新、更好的编译器，程序就会越来越快。不幸的是，这并不总是真的有效。

除了像复制消除（§2.3.5.3）这样的通用优化之外，编译器还提供像循环展开（Loop Unrolling）这样的数值优化技术：循环被转换，使得多次迭代在一次中完成。这减少了循环控制的开销，并增加了并发执行的潜力。许多编译器仅将此技术应用于内层循环，而展开多个循环通常能带来更好的性能。多次迭代计算从引入额外临时变量中受益，而这反过来可能需要用户类型或操作中不可用的语义信息。

某些编译器特别针对特定操作进行了调优——尤其是用于基准测试的操作，更具体地说，是用于对世界500台最快计算机进行排名的 LINPACK 基准测试（www.top500.org）。例如，它们可以使用模式匹配来识别标准稠密矩阵乘法中典型的三重嵌套循环，并将此代码替换为高度调优的汇编实现，其速度可以快一个或多个数量级。这些程序使用七个或九个循环，配合平台相关的块大小，以榨取每个缓存级别的最后一点性能，转置子矩阵，在多个线程上运行，进行精巧的寄存器编排，等等。5

5. 有时人们可能会产生这样的印象：高性能计算（HPC）社区认为，以接近峰值性能乘以稠密矩阵可以解决世界上的所有问题，或者至少可以证明，只要足够努力，一切都可以以接近峰值性能来计算。出于嫉妒，超级计算机中心越来越多的人意识到，他们的机器不仅仅运行稠密矩阵操作，而且现实世界的应用在大多数情况下受限于内存带宽和延迟。

