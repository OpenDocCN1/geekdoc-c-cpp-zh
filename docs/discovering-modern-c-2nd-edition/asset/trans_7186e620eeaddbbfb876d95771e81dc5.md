

vector_sum 和 vector。因此，我们需要另一个表达式模板类和相应的操作：

```cpp
template <typename T>
class vector_sum3
{
public:
    vector_sum3(const vector<T>& v1, const vector<T>& v2,
                const vector<T>& v3)
    : v1{v1}, v2{v2}, v3{v3}
    { ... }

    T operator[](int i) const { return v1[i] + v2[i] + v3[i]; }
private:
    const vector<T>& v1, &v2, &v3;
};
```

```cpp
template <typename T>
vector_sum3<T> inline operator+(const vector_sum<T>& x,
                                const vector<T>& y)
{
    return {x.v1, x.v2, y};
}
```

此外，vector_sum 必须将我们的新加法运算符声明为友元以访问其私有成员，而 vector 需要为 vector_sum3 提供赋值操作。这变得越来越令人烦恼。另外，如果我们先执行第二次加法会怎样：w = x + (y + z)？那么我们需要另一个加法运算符。如果某些向量与标量相乘，例如 w = x + dot(x, y) * y + 4.3 * z，而这个标量积也由 ET 实现，会怎样？我们的实现工作量将陷入组合爆炸，我们需要一个更灵活的解决方案，我们将在下一节中介绍。

## 5.3.3 泛型表达式模板

=> c++11/expression_template_example2.cpp

到目前为止，我们从特定类（vector）入手，逐步泛化实现。虽然这有助于我们理解机制，但现在我们直接转向适用于任意向量类型及其视图的通用版本：

```cpp
template <typename V1, typename V2>
inline vector_sum<V1, V2> operator+(const V1& x, const V2& y)
{
    return {x, y};
}
```

我们现在需要一个带有任意参数的表达式类：

```cpp
template <typename V1, typename V2>
class vector_sum
{
public:
    vector_sum(const V1& v1, const V2& v2) : v1{v1}, v2{v2}
    {}

    ??? operator[](int i) const { return v1[i] + v2[i]; }

private:
    const V1& v1;
    const V2& v2;
};
```

这相当直接。唯一的问题是 operator[] 应该返回什么类型。为此，我们必须在每个类中定义 value_type（外部类型特征会更灵活，但我们希望在此保持尽可能简单）。在 vector_sum 中，我们可以取第一个参数的 value_type，而该类型本身可以从另一个类中获取。只要整个应用程序中的标量类型相同，这是一个可接受的解决方案。然而，我们在 3.11 节中看到，如果不注意结果类型，混合参数可能会产生完全荒谬的结果。为了应对混合运算，我们取参数 value types 的 common_type_t：

```cpp
template <typename V1, typename V2>
class vector_sum
{
    // ...
}
```

```cpp
using value_type = std::common_type_t<typename
V1::value_type,
typename V2::value_type>;
value_type operator[](int i) const { return v1[i] +
v2[i]; }
```

如果我们的类 `vector_sum` 不需要显式声明 `value_type`，可以在 C++14 中使用 `decltype(auto)` 作为返回类型，并将类型推断完全交给编译器。相比之下，当模板用 `vector_sum` 本身实例化时，后置返回类型不起作用，因为这会产生对自身的依赖。为了将不同种类的表达式赋值给向量类，我们还应将赋值运算符泛化：

```cpp
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

这个赋值运算符接受除 `vector<T>` 以外的每种类型，而 `vector<T>` 需要一个专用的复制赋值运算符。为了避免代码冗余，我们可以实现一个执行实际复制的方法，并从通用赋值和复制赋值中调用它。

## C++11 5.3.4 在过期前复制

刚刚引入的泛型表达式模板存在一个问题：当表达式变得更大时，引用的有效性。最终，我们会得到一个指向已销毁的子表达式 ET 对象的悬空引用。

因此，我们应该复制所有本身就是表达式的参数（例如 vector_sum），以避免悬空引用。相比之下，像 vector 这样的容器不应被复制，因为这会使 ET 比经典运算符更慢。因此，我们的第一个想法是区分容器和纯表达式。前者将像以前一样被引用，后者将被复制。这种方法的优点是只需更改 ET 类，而不需要更改返回 ET 对象的运算符。缺点是容器与纯表达式之间的区别需要通过类型特征进行显式声明。在我们的情况中，这些声明实际上并没有造成太多额外工作，因为大多数类型已经被明确分类。与其将类型分类为向量，不如将其声明为向量容器或表达式，而两者都表现得像向量。

=> c++17/expression_template_guided.cpp

这种方法适用于表达式模板的所有“正常”用例。未涵盖的是表达式中使用的临时容器，例如：

```cpp
w = x + y + z + vector(2.0, 8.4, 9.1, 11.1);
```

这仍然可能导致悬空引用。因此，作为右值传递的容器也应该被复制。我们可以通过复制所有右值并引用所有左值来简化这种方法：

```cpp
template <typename T>
using copy_or_cref = conditional_t<is_lvalue_reference_v<T>,
                                      remove_reference_t<T> const&,
                                      remove_reference_t<T>>;
```

其动机是，像 vector_sum 这样的纯表达式对象在常规使用中仅作为右值出现。即使在不太可能的场景中，有人显式创建 vector_sum 对象并将其传递给表达式，我们也不会遇到悬空引用。

现在是棘手的部分。vector_sum（及类似类）的每个成员变量的类型必须取决于我们处理的是左值还是右值。此外，这些成员数据类型只能依赖于类模板参数，因此后者必须反映左值和右值参数之间的区别。假设类参数已适当实例化，我们直接使用这些类型作为成员数据：

```cpp
template <typename V1, typename V2>
class vector_sum
{
    V1 v1;
    V2 v2;
};
```

剩下的挑战性任务是确定在哪里判断我们处理的是左值还是右值类参数。有两种选择。第一种涉及带有转发引用的构造函数：

```cpp
template <typename V1, typename V2>
vector_sum(V1&& v1, V2&& v2);
```

如果所有引用都正确转发给它，我们可以找出引用类型是什么。但是，我们不需要这些信息用于构造函数本身，而是用于类模板参数。为了传播参数类型，我们引入一个推导指南：

```cpp
template <typename V1, typename V2>
vector_sum(V1&&, V2&&)
-> vector_sum<copy_or_cref<V1>, copy_or_cref<V2>>;
```

为了触发此指南，我们的运算符必须返回不带显式模板类型的 vector_sum：

```cpp
template <typename V1, typename V2>
auto operator+(V1&& x, V2&& y)
{
    return vector_sum<std::forward<V1>(x), std::forward<V2>(y)>;
}
```

除了检查结果外，我们还检查前面表达式的类型：

```cpp
cout << typeid(x + y + z + vector{2.0, 8.4, 9.1,
11.1}).name();
```

然后我们就正确地复制或引用了：

```cpp
vector_sum<vector_sum<vector_sum<vector<float> const&,
                                 vector<float> const&>,
                                 vector<float> const&>,
                                 vector<double>>>
```

向量 x、y 和 z 都通过常量引用访问，而最后一个向量被复制到表达式模板中。所有 vector_sum 对象都按值存储。

=> c++17/expression_template_nonstale.cpp

尽管推导指南很酷，我们也可以直接在运算符中实例化 vector_sum：

```cpp
template <typename V1, typename V2>
auto operator+(V1&& x, V2&& y)
-> vector_sum<copy_or_cref<V1>, copy_or_cref<V2>>
{ return {x, y}; }
```

这种方法简化了像 vector_sum 这样的表达式模板类的实现。表达式的类型与之前的技术否则是相同的，考虑到运算符签名和推导指南的相似性，这并不令人惊讶。

**表达式模板总结：** 尽管 C++ 中运算符重载的可用性导致记法更优雅的代码，但科学界拒绝放弃使用 Fortran 编程或直接在 C/C++ 中实现循环。原因是传统的运算符实现开销太大。由于创建临时变量以及复制向量和矩阵对象的开销，C++ 运算符无法与用 Fortran 编写的程序的性能竞争。引入泛型后，这个问题得到了解决，并且

