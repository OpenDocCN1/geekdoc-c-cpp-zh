

当 `expr` 很长时，第一条语句可能会相当冗长，我们添加到其中的所有内容都需要在这条语句中添加两次。并且每次修改时，我们都必须注意两个表达式仍然相同。

=> c++14/value_range_vector.cpp

在自动 `return` 类型中，限定符的保留也很重要。作为示例，我们引入了一个对向量的视图，用于测试值是否在给定范围内。

该视图将使用 `operator[]` 访问被视向量的一个元素，并在范围测试后以完全相同的限定符返回它。显然这是 `decltype(auto)` 的工作。我们对该视图的示例实现仅包含一个构造函数和访问运算符：

```cpp
template <typename Vector>
class value_range_vector
{
    using value_type = typename Vector::value_type;
    using size_type = typename Vector::size_type;
    public:
        value_range_vector(Vector& vref, value_type minv,
        value_type maxv)
        : vref(vref), minv(minv), maxv(maxv)
        {
        }

        decltype(auto) operator[](size_type i)
        {
            decltype(auto) value = vref[i];
            if (value < minv) throw too_small{};
            if (value > maxv) throw too_large{};
            return value;
        }

    private:
        Vector&
            vref;
        value_type minv, maxv;
};
```

我们的访问运算符在返回之前会缓存来自 `vref` 的元素以进行范围检查。临时变量的类型和 `return` 类型都使用 `decltype(auto)` 推导。为了查看向量元素是否以正确类型返回，我们可以将其中一个存储在 `decltype(auto)` 变量中并检查其类型：

```cpp
int main()
{
    using Vec = vector<double>;
    Vec v = {2.3, 8.1, 9.2};

    value_range_vector<Vec> w{v, 1.0, 10.0};
    decltype(auto) val = w[1];
}
```

val 的类型是 double&，正如我们所期望的那样。示例中三次使用了 decltype(auto)：在视图实现中两次，在测试中一次。如果我们只将其中一个替换为 auto，val 的类型将变为 double。

## 3.4.4 推导的类模板参数

虽然自C++早期起函数模板参数就可以被推导，但直到C++14之前，类始终需要被完全实例化，例如：

```cpp
tuple<int, float, string> t1(3, 3.2f, "text"s);
```

这里我们用一个int、一个float和一个字符串字面量实例化了一个tuple（如果没有后缀s，它将是const char*）。尽管如此，我们仍必须用这些类型实例化tuple——这不言而喻。现在我们可以将类型推导交给编译器：

```cpp
tuple t2(3, 3.2f, "text"s);
```

t2的类型也是tuple<int, float, string>。如果我们的类模板参数从构造函数中清晰明了，也可以被推导：

```cpp
template <typename Value>
struct vec
{
    vec(std::initializer_list<Value> values)
    : s(values.size()), d(new Value[s])
    {
        std::copy(begin(values), end(values), d);
    } // ...
};

vec v = {2.3, 3.4, 4.5, 5.6};
```

上面的构造函数参数将被实例化为initializer_list<double>，因此类模板参数很明确。有时类与构造函数参数之间的关系并不那么明显：

```cpp
template <typename Value>
struct vec
{
    template <typename Iter>
    vec(Iter beg, Iter end)
    : s(distance(beg, end)), d(new Value[s])
    {
        copy(beg, end, d);
    }
};
```

```cpp
int array[] = {3, 4, 5, 6};
vec w(begin(array), end(array));
```

这里我们遍历一个int数组，但构造函数的参数不是int，而是迭代器类型。在这种情况下，我们必须通过推导指南来帮助编译器：

```cpp
template <class Iter>
vec(Iter beg, Iter end)
-> vec<typename std::iterator_traits<Iter>::value_type>;
```

推导指南是从构造函数签名到所需实例化类型的映射。后者可以是类型表达式，如我们的情况。类模板iterator_traits是一个类型特征，提供关于常见迭代器类型（如普通指针）的信息。这里我们关心的是迭代器所指向的value_type。因此，我们的推导指南表明，每当使用基于迭代器的构造函数时，就用迭代器的value_type实例化`vec`类。有时根本没有可用的类型信息：

- 8. 我们将在第5.2.1节更全面地讨论类型特征。

```cpp
template <typename Value>
struct vec
{
    vec(unsigned s) : s(s), d(new Value[s]) {}
};

vec x(3);
```

然后我们可以提供一个默认类型。可以作为类参数：

```cpp
template <typename Value = double>
struct vec;
```

或者作为推导指南：

```cpp
vec(unsigned s) -> vec<double>;
```

## **C++17** 3.4.5 推导多种类型

=> c++17/structured_bindings.cpp

有时我们在函数中计算多个结果，并可以将它们作为`pair`、`tuple`或用户定义的类一起返回。在第4.4.2节的示例中，我们将说明访问和/或复制`tuple`单个组件的各种可能性。我们希望预先展示这些示例，并展示C++17提供的一种机会，即在不先存储捆绑结果的情况下使用类型推导。它被称为*结构化绑定*，允许我们在推导返回类型的同时，将实用程序或用户定义类的成员绑定到新变量。在我们的示例中，我们有一个用于LU分解的函数，它返回一个矩阵和一个向量：

```cpp
auto lu(const matrix& A)
{
    // ... some computations
    return tuple<matrix, vector>(LU, p);
}
```

现在我们可以在应用程序中立即将返回的对象拆分为（分解后的）矩阵和（置换）向量：

```cpp
auto [LU, p] = lu(A);
```

LU和p的类型被推导。

当我们遍历一个map时，结构化绑定非常有用，该map的value_type是键及其关联值的pair。不再使用first和second访问pair成员，我们现在可以将它们命名为key和value：

![](img/5682e787fc967e93d7e33e8bac5f58a0_260_0.png)

```cpp
map<string, int> numbers = {{"Zero", 0}, {"One", 1}, {"Two", 2}};
```

```cpp
for (const auto& [key, value] : numbers)
cout << key << "->" << value << endl;
```

这里我们以常量引用的方式访问了key和value。请注意，即使没有const：

![](img/5682e787fc967e93d7e33e8bac5f58a0_260_1.png)

```cpp
for (auto& [key, value] : numbers)
cout << key << "->" << value << endl;
```

我们无法更改key。原因是我们拆分了一个类型为pair<const string, int>的对象（这是map内部存储条目的方式），并且第一个引用的类型被推导为const string&，方式与第3.1.2.2节中的常量参数相同。

=> c++17/structured_bindings_user.cpp

幸运的是，这个很好的新功能不仅限于标准类型，也可以应用于用户类型。它最容易用于仅具有公共成员的聚合类型。我们的lu结果可以返回一个仅将两个对象捆绑在一起的用户类：

![](img/5682e787fc967e93d7e33e8bac5f58a0_260_2.png)

```cpp
struct lu_result
{
    matrix LU;
    vector p;
};
auto lu(const matrix& A)
{
    // ...
    return lu_result{LU, p};
}

matrix A; // set A ...
auto [LU, p] = lu(A);
```

这里我们使用聚合初始化，并避免为此辅助类定义构造函数。结果类型的推导与之前相同。

要为具有`private`成员的结构化绑定提供支持，我们必须建立一个与`pair`和`tuple`等价的`get`接口。这需要一些模板特化，因此我们将其推迟到第3.5.5节。尽管如此，我们还是想先给你以下建议：

> **建议**
> 只要合适，就使用标准实用程序类的结构化绑定，并尽量避免为用户类实现`get`接口。

## C++11 3.4.6 定义类型

定义类型有两种方式：使用`typedef`或使用`using`。前者是在C中引入的，并从一开始就存在于C++中。这也是它唯一的优势：向后兼容性；我们有时在这本书中仅为了编写纯C++03代码而使用它。对于编写不需要使用pre-11编译器编译的新软件，我们强烈建议：

> **建议**
> 使用`using`代替`typedef`。

