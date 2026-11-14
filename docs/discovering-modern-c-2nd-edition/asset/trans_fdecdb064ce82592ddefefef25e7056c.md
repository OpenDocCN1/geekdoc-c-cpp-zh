

它更易读，也更强大。对于简单的定义，这只是顺序问题：

```
typedef double value_type;
```

与之相对：

```
using value_type = double;
```

在 `using` 声明中，新名称位于左侧，而 `typedef` 将其放在右侧。在声明数组时，新类型名称不是 `typedef` 的最右侧部分，类型被分成了两部分：

```
typedef double da1[10];
```

相比之下，在 `using` 声明中，类型保持完整：

```
using da2 = double[10];
```

对于函数指针，差异更加明显——希望你在类型定义中永远不需要它们。§4.4.7 中的 `std::function` 是一个更灵活的替代方案。例如，声明一个带有 `float` 和 `int` 参数并返回 `float` 的函数，读起来如下：

```
typedef float (*float_fn1)(float, int);
```

与之相对：

```
using float_fun2 = float(*)(float, int);
```

在所有示例中，`using` 声明都清晰地将新类型名称与定义分开。

此外，`using` 声明允许我们定义 *模板别名*。这些是带有类型参数的定义。假设我们有一个用于任意阶和可参数化值类型的张量模板类：

点击此处查看代码图片

```
template <unsigned Order, typename Value>
class tensor { ... };
```

现在我们想分别为一阶和二阶张量引入 `vector` 和 `matrix` 类型。这无法通过 `typedef` 实现，但可以通过 `using` 的模板别名轻松实现：

点击此处查看代码图片

```
template <typename Value>
using vector = tensor<1, Value>;

template <typename Value>
using matrix = tensor<2, Value>;
```

当我们打印以下行的输出时：

点击此处查看代码图片

```
std::cout << "The type of vector<float> is "
          << typeid(vector<float>).name() << ".\n";
std::cout << "The type of matrix<float> is "
          << typeid(matrix<float>).name() << ".\n";
```

在名称去修饰器中，我们将看到：

点击此处查看代码图片

```
The type of vector<float> is tensor<1u, float>.
The type of matrix<float> is tensor<2u, float>.
```

总而言之，如果你有 typedef 经验，你会欣赏 C++11 带来的新机遇；如果你是类型定义的新手，应该立即开始使用 using。

## 3.5 模板特化

一方面，为许多参数类型使用相同的实现是一大优势。然而，对于某些参数类型，我们可能知道更高效的实现，这可以通过 C++ 中的模板特化来实现。原则上，我们甚至可以为某些类型实现完全不同的行为，但代价是造成极大的混淆。因此，特化应当更高效，但行为应保持一致。C++ 提供了巨大的灵活性，作为程序员，我们有责任合理使用这种灵活性，并保持自身的一致性。

### 3.5.1 为单一类型特化类

=> c++11/vector_template.cpp

接下来，我们想将清单 3–1 中的 vector 示例为 bool 进行特化。我们的目标是将 8 个 bool 值打包到一个字节中以节省内存。让我们从类定义开始：

```
template <>
class vector<bool>
{
    // ...
};
```

尽管我们的特化类不再是类型参数化的，但我们仍然需要 template 关键字和空的尖括号。名称 vector 之前已被声明为类模板，我们需要这个看似多余的模板表示法来表明以下定义是主模板的特化。因此，在主模板之前定义或声明模板特化是错误的。在特化中，我们必须在尖括号内为每个模板参数提供一个类型。这些值可以是参数本身（或其表达式）。例如，如果我们为三个参数中的一个进行特化，另外两个仍然声明为模板参数：

点击此处查看代码图片

```
template <typename T1, typename T3>
class some_container<T1, int, T3>
{
    // ...
};
```

回到我们的布尔向量类：我们的主模板为空向量和包含 n 个元素的向量定义了构造函数。为保持一致性，我们也应该定义相同的内容。

对于非空向量，当位数不能被 8 整除时，我们需要向上取整数据大小：

点击此处查看代码图片

```
template <>
class vector<bool>
{
public:
    explicit vector(int size)
        : my_size(size), data{new unsigned char[(my_size + 7) / 8]}
    {
    }

    vector() : my_size(0) {}
private:
    int my_size;
    std::unique_ptr<unsigned char[]> data;
};
```

你可能已经注意到，默认构造函数与主模板中的相同。不幸的是，该方法不会“继承”到特化中。每当我们编写特化时，都必须从头开始定义一切，或者使用一个公共基类。9

9. 作者试图克服这种冗长 [20]。

我们可以自由地从主模板中省略成员函数或变量，但为保持一致性，我们只有出于充分理由，甚至非常充分的理由时才应这样做。例如，我们可能会省略 operator+，因为 bool 没有加法运算。常量访问运算符通过移位和位掩码实现：

点击此处查看代码图片

```
template <> class vector<bool>
{
bool operator[](int i) const
{ return (data[i / 8] >> i % 8) & 1; }
};
```

可变访问更棘手，因为我们无法引用单个位。诀窍是返回一个 Proxy——一种占位符设计模式，为其他东西提供接口。我们的 vector_bool_proxy 应为向量中的单个位提供 bool 接口：

点击此处查看代码图片

```
template <> class vector<bool>
{
vector_bool_proxy operator[](int i)
{ return {data[i / 8], i % 8}; }
};
```

返回语句使用带花括号的列表来调用两参数构造函数。现在让我们实现我们的代理来管理 `vector<bool>` 中的特定位。显然，该类需要对包含字节的引用以及该字节内的位置。为了简化后续操作，我们创建一个掩码，在问题位置上有 1 位，在所有其他位置上有 0 位：

点击此处查看代码图片

```
class vector_bool_proxy
{
public:
    vector_bool_proxy(unsigned char& byte, int p)
        : byte(byte), mask(static_cast<unsigned char>(1 << p))
    {}

private:
    unsigned char& byte;
    unsigned char mask;
};
```

请注意，`1 << p` 的结果是 `int`，如果没有强制转换，将其存储到 `mask` 将是收窄转换。读取访问通过简单地对引用的字节进行掩码并转换为 `bool` 来实现：

点击此处查看代码图片

```
class vector_bool_proxy
{
    operator bool() const { return byte & mask; }
};
```

只有当 `byte` 中考虑的位为 1 时，按位与才会产生非零值，该值在从 `unsigned char` 到 `bool` 的隐式转换中被评估为 `true`。设置位通过 `bool` 的赋值运算符来实现：

点击此处查看代码图片

```
class vector_bool_proxy
{
    vector_bool_proxy& operator=(bool b)
    {
        if (b)
            byte |= mask;
        else
            byte &= ~mask;
        return *this;
    }
};
```

当我们区分配置的值时，赋值更容易实现。当参数为 `true` 时，我们应用与掩码的或运算，以便考虑位置上的位被打开。所有其他位置保持不变，因为与 0 进行或运算没有影响（0 是按位或的单位元）。相反，当参数为 `false` 时，我们首先反转掩码，并将其与字节引用进行与运算。然后，反转掩码在活动位置上的 0 位将位关闭，而在所有其他位置上，与 1 位进行与运算保留了这些位值。

通过为 `bool` 特化 `vector`，我们只使用大约八分之一的内存。尽管如此，我们的特化与主模板（大部分）保持一致：我们可以以相同的方式创建向量并读写它们。精确地说，压缩向量与主模板并不完全相同，例如，当我们获取元素引用或涉及类型推导时。然而，我们尽可能使特化与通用版本相似，在大多数情况下我们不会意识到差异，并且它的工作方式相同。

### 3.5.2 特化和重载函数

在本节中，我们讨论并评估函数模板特化的优缺点。

#### 3.5.2.1 将函数特化为特定类型

函数可以像类一样进行特化。不幸的是，它们不参与重载决策，且不太具体的重载优先于更具体的模板特化；参见 [64]。出于这个原因，Sutter 和 Alexandrescu 在 [66, Item 66] 中给出了以下建议：

> 建议
> 不要使用函数模板特化！

要为上述特定类型或类型元组提供特殊实现，我们可以简单地使用重载。这效果更好，甚至更简单，例如：

![](img/5682e787fc967e93d7e33e8bac5f58a0_267_0.png)

