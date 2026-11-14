

不幸的是，该类型特性在多个编译器中实现较晚。例如，g++ 4.9 和 clang 3.4 不提供它，而 g++ 5.1 和 clang 3.5 提供。

这种旧式复制函数仅应在与 C 交互时使用。在纯 C++ 程序中，最好依赖 STL 复制：

```
copy(&a, &x + 1, &y);
```

无论我们的类的内存布局如何，这都适用，且当类型允许时，复制的实现内部会使用移动。

C++14 添加了一些模板别名，例如

```
conditional_t<B, T, F>
```

作为以下内容的快捷方式：

```
typename conditional<B, T, F>::type
```

同样，enable_if_t 是 enable_if 类型的缩写。

## 4.4 实用工具

C++11 添加了新库，使现代编程风格更加轻松和优雅。例如，我们可以更轻松地返回多个结果，更灵活地引用函数和函数对象，并创建引用容器。

### 4.4.1 元组

当函数计算多个结果时，它们过去通常作为可变引用参数传递。假设我们实现一个带主元的 LU 分解，接受矩阵 A 并返回分解后的矩阵 LU 和置换向量 p：

```
void lu(const matrix& A, matrix& LU, vector& p) { ... }
```

我们也可以将 LU 或 p 作为函数结果返回，并通过引用传递另一个对象。这种混合方法更加令人困惑。

=> c++11/tuple_move_test.cpp

为了在不实现新类的情况下返回多个结果，我们可以将它们捆绑到一个元组中。元组（来自 <tuple>）与容器的区别在于允许不同类型。与大多数容器不同，对象的数量必须在编译时已知。使用元组，我们可以一次返回 LU 分解的两个结果：

```
tuple<matrix, vector> lu(const matrix& A)
{
    matrix LU(A);
    vector p(n);
    // ... some computations
    return tuple<matrix, vector>(LU, p);
}
```

返回语句可以借助辅助函数 make_tuple 简化，该函数能推导类型参数：

```
tuple<matrix, vector> lu(const matrix& A)
{
    ...
    return make_tuple(LU, p);
}
```

make_tuple 在与 auto 变量结合使用时尤其方便：

```
auto t = make_tuple(LU, p, 7.3, 9, LU*p, 2.0+9.0i);
```

调用我们的函数 lu 的调用者可能会使用函数 get 从元组中提取矩阵和向量：

```
tuple<matrix, vector> t = lu(A);
matrix LU = get<0>(t);
vector p = get<1>(t);
```

在此，所有类型也可以推导：

```
auto t = lu(A);
auto LU = get<0>(t);
auto p = get<1>(t);
```

函数 get 接受两个参数：一个元组和其中的位置。后者是编译时参数。否则，结果的类型将无法得知。如果索引过大，错误将在编译期间检测到：

```
auto t = lu(A);
auto am_i_stupid = get<2>(t); // Error during compilation
```

在 C++14 中，如果类型无歧义，元组条目也可以按类型访问：

```
auto t = lu(A);
auto LU = get<matrix>(t);
auto p = get<vector>(t);
```

这样我们就不再需要记住元组中的内部顺序了。或者，我们可以使用函数 tie 来分离元组中的条目。这通常更优雅。

在这种情况下，我们必须事先声明兼容的变量：

```
matrix LU;
vector p;
tie(LU, p) = lu(A);
```

tie 乍一看相当神秘，但其实现出人意料地简单：它创建一个带有函数参数引用的对象。将元组赋给该对象会执行每个元组成员到相应引用的赋值。

使用 tie 的实现比使用 get 的实现具有性能优势。当我们将函数 lu 的结果直接传递给 tie 时，它仍然是右值（没有名称），我们可以移动条目。使用中间变量时，它变成左值（有名称），条目必须被复制。为了避免复制，我们也可以显式移动元组条目：

```
auto t = lu(A);
auto LU = get<0>(move(t));
auto p = get<1>(move(t));
```

在此，我们踩得相当危险。原则上，对象在应用 move 后被视为已过期。只要析构函数不会崩溃，它可以处于任何状态。在我们的示例中，在对 t 应用 move 后我们又读取了 t。在这种情况下这是正确的。move 将 t 转换为右值，我们可以随意处理其数据。但我们没有。当 lu 被创建时，我们只获取元组条目 0 的数据而不触碰条目 1。相反，在创建 p 时，我们只从 t 的条目 1 窃取数据而不访问条目 0 中已过期的数据。因此，这两个操作移动的是完全不相交的数据。尽管如此，对同一数据项多次使用 move 非常危险，必须仔细分析（就像我们所做的那样）。

在讨论了调用方的高效数据处理后，我们应该再看一下函数 lu。结果矩阵和向量在从函数返回时会被复制到元组中。在返回语句中，移动函数中的所有数据是安全的，因为这些数据无论如何都会被销毁。以下是修订后的函数片段：

```
tuple<matrix, vector> lu(const matrix& A)
{
    ...
    return make_tuple(move(LU), move(p));
}
```

既然我们已经避免了所有复制，返回元组的实现与使用可变引用的代码一样高效，至少在结果用于初始化变量时是这样。当结果被赋值给现有变量时，我们仍然有分配和释放内存的开销。

C++ 中的另一个异构类是 pair。它在 C++03 中就已存在，并且至今仍然存在。pair 等同于带有两个参数的元组。两者之间存在转换，因此 pair 和两参数元组可以相互交换甚至混合。本节中的示例都可以使用 pair 实现。我们可以写 t.first 而不是 get<0>(t)（以及 t.second 对应 get<1>(t)）。

=> c++11/boost_fusion_example.cpp

### 进一步阅读：

库 Boost::Fusion 旨在将元编程与经典（运行时）编程融合。使用此库，我们可以编写遍历元组的代码。以下程序实现了一个通用函数对象 printer，它针对元组 t 的每个条目被调用：

```cpp
struct printer
{
    template <typename T>
    void operator()(const T& x) const
    {
        std::cout << "Entry is " << x << std::endl;
    }
int main ()
{
    auto t = std::make_tuple( 7u, "Hallo", std::string("Hl"),
                              std::complex<float>(3, 7));
    boost::fusion::for_each(t, printer{});
}
```

该库还提供了更强大的功能来遍历和转换异构类型容器（boost::fusion::for_each 在我们看来远比 std::for_each 有用）。尤其是当编译时和运行时的功能以非平凡方式交互时。Boost Fusion 是必不可少的。

元编程领域中功能最全面的库是 Boost 元编程库（MPL）[22]。该库实现了大部分 STL 算法（§4.1），并提供了类似的数据类型：例如，vector 和 map 被实现为编译时容器。尤其是，当编译时和运行时的功能以非平凡方式交互时，MPL 与 Boost Fusion 的组合极其强大。撰写本书时的一个新库是 Hana [11]，它以更函数式的方法处理编译时和运行时计算。它在很大程度上依赖 C++14 特性，从而产生显著更紧凑的程序。

### 4.4.2 function

=> c++11/function_example.cpp

<functional> 中的 function 类模板是泛化函数指针。函数类型规范作为模板参数传递，如下所示：

```cpp
double add(double x, double y)
{
    return x + y;
}
int main ()
{
    using bin_fun = function<double(double, double)>;
    bin_fun f = &add;
    cout << "f(6, 3) = " << f(6, 3) << endl;
}
```

function 包装器可以持有具有相同返回类型和相同参数类型列表的不同种类的函数实体。6 我们甚至可以构建兼容函数对象的容器：

```cpp
vector<bin_fun> functions;
functions.push_back(&add);
```

6. 因此，它们可能具有不同的签名，因为不要求相同的函数名称。相比之下，签名的相等性并不强制要求相同的返回类型。

