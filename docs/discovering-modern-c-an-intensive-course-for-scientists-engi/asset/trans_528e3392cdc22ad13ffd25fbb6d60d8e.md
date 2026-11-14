

在 using 声明中，新名称位于左侧，而 typedef 将其放在右侧。对于数组声明，新类型名称不是 typedef 中最右侧的部分，且类型被分成两部分：

```cpp
typedef double da1[10];
```

与之相反，在 using 声明中，类型保持为一个整体：

```cpp
using da2 = double[10];
```

对于函数（指针）类型，差异更加明显——希望你在类型定义中永远不需要它。§4.4.2 中的 std::function 是一个更灵活的替代方案。例如，声明一个带有 float 和 int 参数并返回 float 的函数，读作

```cpp
typedef float float_fun1(float, int);
```

与之相对

```cpp
using float_fun2 = float (float, int);
```

在所有这些示例中，using 声明清楚地将新类型名称与定义分开。

此外，using 声明允许我们定义模板别名。这些是带有类型参数的定义：假设我们有一个用于任意阶数和可参数化值类型的模板类：

```cpp
template <unsigned Order, typename Value>
class tensor { ... };
```

现在我们想为一阶和二阶张量分别引入类型名称 vector 和 matrix。这无法通过 typedef 实现，但可以通过 using 的模板别名轻松实现：

```cpp
template <typename Value>
using vector = tensor<1, Value>;
```

```cpp
template <typename Value>
using matrix = tensor<2, Value>;
```

当我们将以下几行的输出：

```cpp
std::cout << "type of vector<float> is "
<< typeid(vector<float>).name() << '\n';
std::cout << "type of matrix<float> is "
<< typeid(matrix<float>).name() << '\n';
```

交给名称去修饰器，我们将看到

```
type of vector<float> is tensor<1u, float>
type of matrix<float> is tensor<2u, float>
```

总而言之，如果你有 typedef 经验，你会欣赏 C++11 带来的新机遇；如果你是类型定义领域的新手，你应该立即开始使用 using。

## 3.5 关于模板的一点理论：概念

> "亲爱的朋友，灰色皆是理论，生命之树常青。"<sup>8</sup>
> —Johann Wolfgang von Goethe

在前面的章节中，你可能会产生这样的印象：模板参数可以被任何类型替代。事实上，这并不完全正确。模板类和函数的程序员对可以对模板参数执行的操作做出了假设。

因此，了解哪些参数类型是可接受的非常重要。例如，我们已经看到 `accumulable` 可以用 `int` 或 `double` 实例化。没有加法的类型（如第 74 页的求解器类）不能用于 `accumulable`。从一组求解器中应该累积什么？函数 `accumulate` 的模板参数 `T` 的所有要求可以总结如下：

- `T` 是可拷贝构造的：当 `b` 的类型为 `T` 时，`T a(b);` 可编译。
- `T` 是可加赋的：当 `a` 和 `b` 的类型为 `T` 时，`a += b;` 可编译。
- `T` 可以从 `int` 构造：`T a(0);` 可编译。

这样一组类型要求称为 _概念_。包含概念 `C` 的所有要求并可能有额外要求的概念 `C` 称为 `C` 的 _细化_。满足概念 `C` 的所有要求的类型 `T` 称为 `C` 的 _模型_。例如，可加赋类型包括 `int`、`float`、`double`，甚至 `string`。

模板函数或类的完整定义应包含所需概念的列表，就像标准模板库中的函数所做的那样；见 `http://www.sgi.com/tech/stl/`。

今天，这些要求仅作为文档。未来的 C++ 标准很可能将概念作为核心语言特性支持。主要由 Andrew Sutton 编写的技术规范 "C++ Extensions for Concepts" [46] 正在进行中，可能会成为 C++17 的一部分。

## 3.6 模板特化

一方面，能够为许多参数类型使用相同的实现是一大优势。然而，对于某些参数类型，我们可能知道更高效的实现，这可以通过 C++ 中的 _模板特化_ 实现。原则上，我们甚至可以为某些类型实现完全不同的行为，代价是造成极大的混乱。因此，特化将更高效，但行为相同。C++ 提供了巨大的灵活性，我们作为程序员有责任负责任地使用这种灵活性，并保持自身的一致性。

### 3.6.1 为单一类型特化类

=> c++11/vector_template.cpp

在接下来的内容中，我们想将 Listing 3.3.1 中的 vector 示例特化为 bool。我们的目标是通过将 8 个 bool 值打包到一个字节中来节省内存。让我们从类定义开始：

```cpp
template <>
class vector<bool>
{
    // ...
};
```

虽然我们的特化类不再是类型参数化的，但我们仍然需要 template 关键字和空三角括号。名称 vector 之前已被声明为类模板，我们需要这个看似多余的模板表示法来表明以下定义是主模板的特化。因此，在主模板之前定义或声明模板特化是错误的。在特化中，必须在尖括号中为每个模板参数提供一个类型。这些值本身可以是参数（或其表达式）。例如，如果我们针对三个参数中的一个进行特化，另外两个仍然声明为模板参数：

```cpp
template <typename T1, typename T3>
class some_container<T1, int, T3>
{
    // ...
};
```

回到我们的布尔向量类：我们的主模板为空向量和包含 n 个元素的向量定义了构造函数。为保持一致性，我们也应该定义相同的构造函数。对于非空向量，当位数不能被 8 整除时，我们需要向上取整数据大小：

```cpp
template <>
class vector<bool>
{
public:
    explicit vector(int size)
        : my_size(size), data(new unsigned char[(my_size + 7) / 8])
    {
    }
    vector() : my_size(0) {}
private:
    int my_size;
    std::unique_ptr<unsigned char[]> data;
};
```

你可能已经注意到，默认构造函数与主模板中的相同。不幸的是，该方法不会“继承”到特化中。每当我们编写特化时，都必须从头开始定义所有内容或使用一个共同基类。9

我们可以自由地从主模板中省略成员函数或变量，但为保持一致性，我们只有出于充分理由，甚至非常充分的理由时才应这样做。例如，我们可能会省略 operator+，因为 bool 没有加法。常量访问运算符通过移位和位掩码实现：

```cpp
template <> class vector<bool>
{
    bool operator[](int i) const
    { return (data[i / 8] >> i % 8) & 1; }
};
```

可变访问更棘手，因为我们无法引用单个位。诀窍是返回一个 Proxy，它为单个位提供读写操作：

```cpp
template <> class vector<bool>
{
    vector_bool_proxy operator[](int i)
    { return {data[i / 8], i % 8}; }
    vector_bool_proxy operator[](int i) const
    { return {data[i / 8], i % 8}; }
};
```

返回语句使用花括号列表来调用两参数构造函数。让我们现在实现我们的代理，以管理 vector<bool> 中的特定位。显然，该类需要对包含字节的引用以及该字节内的位置。为了简化进一步操作，我们创建一个掩码，该掩码在问题位置有一个位，在所有其他位置有零位：

```cpp
class vector_bool_proxy
{
public:
    vector_bool_proxy(unsigned char& byte, int p)
        : byte(byte), mask(1 << p) {}

private:
    unsigned char& byte;
    unsigned char mask;
};
```

读取访问通过转换为 bool 来实现，我们只需对引用的字节进行掩码：

```cpp
class vector_bool_proxy
{
    operator bool() const { return byte & mask; }
};
```

只有当字节中的考虑位为 1 时，按位与才会产生非零值，该值在从 unsigned char 到 bool 的转换中被评估为 true。
设置位通过 bool 的赋值运算符实现：

```cpp
class vector_bool_proxy
{
```

