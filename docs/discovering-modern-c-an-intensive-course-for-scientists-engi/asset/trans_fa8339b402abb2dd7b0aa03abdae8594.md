

参数为多个参数的函数，尤其是当参数类型来自不同命名空间时，歧义的概率会进一步上升，例如：

```cpp
namespace rocketry {
namespace mat {
...
template <typename Scalar, typename Matrix>
Matrix operator*(const Scalar& a, const Matrix& A) { ... }
}
namespace vec {
...
template <typename Scalar, typename Vector>
Vector operator*(const Scalar& a, const Vector& x) { ... }

template <typename Matrix, typename Vector>
Vector operator*(const Matrix& A, const Vector& x) { ... }
}
}
int main (int argc, char* argv[]) {
rocketry::mat::ober_matrix A;
rocketry::vec::ober_vector x, y;
y = A * x; // which overload is selected?
}
```

这里的意图很明确。嗯，对于人类读者来说是这样。对于编译器来说则不那么明确。A 的类型定义在 rocketry::mat 中，x 的类型定义在 rocketry::vec 中，因此 operator* 会在两个命名空间中进行查找。因此，所有三个模板重载都可用，并且没有哪一个比其他更匹配（尽管可能只有一个能编译通过）。

不幸的是，显式模板实例化与 ADL 不兼容。每当在函数调用中显式声明模板参数时，函数名不会在参数的命名空间中查找。⁶

调用哪个函数重载取决于迄今讨论过的规则：

- 命名空间嵌套和限定，
- 名称隐藏，
- ADL，以及
- 重载决议。

对于经常重载的函数，必须理解这种非平凡的相互作用，以确保不会出现歧义并且选择正确的重载。因此，我们在附录 A.6.2 中给出了一些示例。在处理较大的代码库并遇到意外的重载决议或歧义之前，可以随时推迟此讨论。

6. 问题在于 ADL 在编译过程中执行得太晚，开放尖括号已经被误读为小于号。要解决此问题，必须通过命名空间限定或使用 using 导入使函数可见（有关更多详细信息，请参阅标准 §14.8.1.8）。

### 3.2.3 命名空间限定或 ADL

许多程序员不想深入研究编译器如何选择重载或遇到歧义的复杂规则。他们会限定被调用函数的命名空间，并确切知道选择了哪个函数重载（假设该命名空间中的重载在重载决议中不存在歧义）。我们不责备他们；名称查找绝非易事。

当我们计划编写包含可与多种类型实例化的函数和类模板的优秀通用软件时，应考虑 ADL。我们将用许多程序员遇到的一个非常流行的性能错误（尤其是在 C++03 中）来演示这一点。标准库中包含一个名为 `swap` 的函数模板。它交换同类型两个对象的内容。旧的默认实现使用拷贝和一个临时对象：

```cpp
template <typename T>
inline void swap(T& x, T& y)
{
    T tmp(x); x = y; y = tmp;
}
```

它适用于所有具有拷贝构造函数和赋值运算符的类型。目前为止，一切都好。假设我们有两个向量，每个包含 1GB 数据。那么使用默认实现时，我们需要拷贝 3GB，并且还需要额外的 1GB 内存。或者我们可以做得更聪明一些：切换指向数据和大小信息的指针：

```cpp
template <typename Value>
class vector
{
    ...
    friend inline void swap(vector& x, vector& y)
    { std::swap(x.my_size, y.my_size); std::swap(x.data, y.data); }
    private:
    unsigned my_size;
    Value *data;
};
```

请注意，此示例包含一个内联友元函数。它声明了一个作为所含类友元的非成员函数。显然，这比分别声明友元和函数更简短。

假设我们需要在某个泛型函数中交换参数化类型的数据：

```cpp
template <typename T, typename U>
inline void some_function(T& x, T& y, const U& z, int i)
{
    ...
    std::swap(x, y); // can be expensive
    ...
}
```

我们采取了稳妥的做法，使用了适用于所有可拷贝类型的标准 swap 函数。但是我们拷贝了 3GB 数据。使用我们只切换指针的实现会快得多且更节省内存。可以通过一种通用的小改动来实现这一点：

```cpp
template <typename T, typename U>
inline void some_function(T& x, T& y, const U& z, int i)
{
    using std::swap;
    ...
    swap(x, y); // involves ADL
    ...
}
```

使用此实现时，两个 swap 重载都是候选项，但重载决议会优先选择我们类中的那个，因为其参数类型比标准实现更具体。更一般地说，任何针对用户类型的实现都比 std::swap 更具体。事实上，出于同样的原因，std::swap 已经为标准容器重载了。这是一个通用模式：

### 使用 using

不要限定可能存在用户类型重载的函数模板的命名空间。相反，应使名称可见并以非限定方式调用函数。

作为默认 swap 实现的补充：自 C++11 以来，默认做法是在两个参数和临时对象之间移动值：C++11

```cpp
template <typename T>
inline void swap(T& x, T& y)
{
    T tmp(move(x));
    x = move(y);
    y = move(tmp);
}
```

结果是，只要提供快速移动构造函数和赋值运算符，没有用户定义 swap 的类型也可以高效交换。只有既没有用户实现也没有移动支持的类型最终才会被拷贝。

## 3.3 类模板

在上一节中，我们描述了使用模板创建泛型函数的方法。模板也可用于创建泛型类。与泛型函数类似，类模板是标准中的正确术语，而 template class（或 templated class）在日常生活中更常用。在这些类中，数据成员的类型可以被参数化。

这对于向量、矩阵和列表等通用容器类尤其有用。我们也可以用参数化值类型扩展复数类。但是，我们已经在这个类上花费了太多时间，看点别的似乎更有趣。

### 3.3.1 容器示例

例如，让我们编写一个泛型向量类，这里的向量是指线性代数意义上的向量，而非 STL 向量。首先，我们实现一个仅包含最基本运算符的类：

### 列表 3-1：模板向量类

```cpp
template <typename T>
class vector
{
public:
    explicit vector(int size)
    : my_size(size), data( new T[my_size] )
    {
    }

    vector(const vector& that)
    : my_size(that.my_size), data(new T[my_size])
    {
        std::copy(&that.data[0], &that.data[that.my_size], &data[0]);
    }

    int size() const { return my_size; }

    const T& operator[](int i) const
    {
        check_index(i);
        return data[i];
    }
    // ...

private:
    int my_size;
    std::unique_ptr<T[]> data;
};
```

模板类与非模板类在本质上没有区别。唯一的区别是多了一个参数 T 作为元素类型的占位符。我们有像 my_size 这样的成员变量和像 size() 这样的成员函数，它们不受模板参数影响。其他函数（如下标运算符或拷贝构造函数）是参数化的，但仍与其非模板等价物相似：以前我们使用 double 的地方，现在都放入了类型参数 T（用于返回类型或分配内存）。同样，成员变量 data 只是被 T 参数化。

模板参数可以有默认值。假设我们的向量类不仅参数化值类型，还参数化方向和位置：

```cpp
struct row_major {}; // just for tagging
struct col_major {}; // ditto
struct heap {};
struct stack {};
```

```cpp
template <typename T = double, typename Orientation = col_major,
       typename Where = heap>
class vector;
```

向量的参数可以完全声明：

```cpp
vector<float, row_major, heap> v;
```

最后一个参数等于默认值，可以省略：

```cpp
vector<float, row_major> v;
```

与函数一样，只能省略最后的参数。例如，如果第二个参数
是默认值而最后一个不是，则必须全部写出：

```cpp
vector<float, col_major, stack> w;
```

当所有模板参数都设置为默认值时，我们当然可以全部省略。
但是，由于此处不讨论的语法原因，仍然需要写出尖括号：

```cpp
vector x; // Error: it is considered a non-template class
```

```cpp
vector<> y; // looks a bit strange but is correct
```

与函数参数的默认值不同，模板默认值可以引用前面的参数：

```cpp
template <typename T, typename U = T>
class pair;
```

这是一个用于两个可能具有不同类型的值的类。如果不是，我们可以只声明一次类型：

```cpp
pair<int, float> p1; // object with an int and float value
pair<int> p2; // object with two int values
```

默认值甚至可以是前面参数的表达式，我们将在第 5 章中看到。

### 3.3.2 设计统一的类和函数接口

=> c++03/accumulate_example.cpp

当我们编写泛型类和函数时，可以问自己一个鸡生蛋蛋生鸡的问题：哪个先来？我们可以选择先编写函数模板，然后通过实现相应方法来调整我们的类以适应它们。或者，我们可以先开发类的接口，然后针对该接口实现泛型函数。

当我们的泛型函数需要能够处理内置类型或标准库中的类时，情况会稍有不同。这些类无法更改，我们应该调整我们的函数以适应它们的接口。还有其他我们稍后将介绍的选项：特化和元编程，它们允许类型依赖的行为。

作为案例研究，我们使用标准模板库第 4.1 节中的 accumulate 函数。它是在程序员比今天更频繁地使用指针和普通数组的时代开发的。因此，STL 创建者 Alex Stepanov 和 David Musser 建立了一个极其通用的接口，它适用于指针和数组，也适用于他们库中的所有容器。

