
以下声明将导致编译错误：

```cpp
#include <iostream>

template<class T, class U>
decltype(lhs * rhs) multiply(T lhs, U rhs) 
{
    return lhs * rhs;
}

int main() {
    auto value = multiply(2.3, 6);
    std::cout << value << std::endl;
}
```

输出：
error: 'lhs' was not declared in this scope

由于编译器是从左到右解析语句的。因此，当它遇到表达式 `(lhs * rhs)` 时，它不知道 `lhs` 和 `rhs` 是什么。尾随返回类型解决了这个问题。

# 代码简化

使用尾随返回类型可以简化代码。考虑以下函数指针声明：

```
void (*func(int i))(int) newFunc;
```

这声明 `newFunc` 为一个函数指针，它接受一个 `int` 参数并返回一个接受 `int` 参数并返回 `void` 的函数指针。这可以用更清晰的方式声明为：

```
auto newFunc(int x) -> void (*)(int);
```

# 现代 C++：变量初始化 (C++11)

变量初始化涉及声明变量并赋予其一个值。C++11 引入了变量初始化的标准语法。

在传统上，C++ 中的初始化可以通过括号、大括号或赋值运算符完成的。这导致了关于如何初始化变量或对象的困惑。C++11 引入了统一初始化，这意味着我们可以使用标准语法进行初始化。

# 拷贝赋值

拷贝赋值是将值放入变量的传统方法。在变量声明后，我们可以使用赋值运算符 `=` 赋予它一个值。这种类型的初始化被称为拷贝赋值（或简称为赋值）。

```cpp
int width               // 声明一个名为 width 的整型变量
width = 5;              // 将值 5 拷贝赋值给变量
```

拷贝赋值之所以这样命名，是因为它将 `=` 运算符右侧的值拷贝到运算符左侧的变量中。`=` 运算符被称为赋值运算符。

拷贝赋值的问题是它使用了两个语句（一个声明和一个赋值），因此消耗了更多的 CPU 周期。

我们可以将变量的声明和初始化合并为一步，以节省 CPU 周期：

```cpp
int width = 5;
```

# 直接初始化

C++11 引入了直接初始化：

```cpp
// 使用值 5 直接初始化变量 width
int width(5); // 等同于 int width (5);
```

对于原生数据类型（如整数），拷贝赋值和直接初始化在本质上是相同的。但对于某些复杂类型，直接初始化的性能可能于拷贝初始化。

接下来考虑：

```cpp
Foo foo(obj)
```

为了让该对象 `foo` 的直接初始化生效，`Foo` 必须有一个拷贝构造函数，或者一个接受 `obj` 作为按值调用的构造函数。否则该语句将无法编译。

# 大括号初始化

大括号初始化有两种形式：

```cpp
// 使用 5 直接大括号初始化变量 width（首选技术）
int width { 5 };
// 使用 5 拷贝大括号初始化变量
int width = { 5 };
```

使用空大括号初始化变量或对象表示零初始化。零初始化将变量初始化为符号零（适用于给定类型的零）。对于对象，零初始化需要一个不接受任何参数的构造函数。

```cpp
// 将字符串零初始化为空字符串
std::string msg {};
```

大括号初始化的额外优点是不允许收窄类型转换。这意味着如果我们尝试使用大括号初始化一个无法安全容纳该值的变量，编译器将抛出警告或错误。

从浮点数到整数的转换总是收窄的——即使是从 5.0 到 5。

```cpp
// 错误：收窄初始化：尝试将 float 类型
// 转换为 int 类型
```

```cpp
int width { 4.0 };
```

最佳实践是始终初始化变量。但有时，为了节省 CPU 周期，我们可以留未初始化变量。

使用大括号初始化强制执行值初始化。使用 `{}` 初始变量被设置为该类型的零值（例如，如果是指针，则设置为 `nullptr`）：

```cpp
string s;
string s {};
// s 有未定义的值
// s 初始化为空字符串
```

```cpp
int j;
int j {};
// j 有未定义的值
// j 初始化为 0
```

```cpp
int* p;
int* p {};
// p 有未定义的值
// p 初始化为 nullptr
```

# 返回 {} 的含义

考虑以下函数声明：

```cpp
FooFunction() { return {}; };
```

函数将返回一个 `Foo` 类型的默认对象。为了使该语句正常编译，`Foo` 必须有一个不接受任何参数的默认构造函数。

# std::initializer_list

另参：标准库：initializer_list

考虑 C++ 中的整数数组：

```cpp
int array[5];
```

我们可以用初始化列表初始化此数组：

```cpp
int array[5] {0, 1, 2, 3, 4};
```

大括号中的表达式被称为初始化列表。

以下对动态分配数组的初始化也可以编译：

```cpp
int *pArray = new int[5] {5, 4, 3, 2, 1};
```

现在考虑以下数组类：

```cpp
#include <iostream>
#include <initializer_list>
class IntArray {
    private:
    int m_length;
    int *m_data;
    public:
    IntArray(): m_length(0), m_data(nullptr) { }
    IntArray(int length) : m_length(length)
    {
      m_data = new int[length];
    }
    ~IntArray()
    {
      delete[] m_data;
    }
    int& operator[](int index)
    {
      return m_data[index];
    }
    int getLength() { return m_length; }
};

int main()
{
    IntArray array { 5, 4, 3, 2, 1 };
    for (int i = 0; i < array.getLength(); i++)
    {
        std::cout << array[i] << " ";
    }
    return 0;
}
```

输出：
5 4 3 2 1 

上述初始化 `IntArray array { 5, 4, 3, 2, 1 };` 无法编译，因为 `IntArray` 类没有处理初始化列表的构造函数。

在 C++11 中，当编译器使用大括号初始化列表时，它会隐式地转换为 `std::initializer_list<T>`。所有 STL 容器都有接受初始化列表作为参数的构造函数。这使得向量支持大括号初始化。

在 C++11 之前，初始化向量的唯一方法是这样的：

```cpp
std::vector<int> vec1;
for(int i = 0; i < 5; i++)
vec1.push_back(i);
```

但自 C++11 起，`std::vector` 包含了初始化列表构造函数，因此我们可以这样初始化向量：

```cpp
// C++11 之前错误
std::vector<int> vec = {1,2,3,4,5};
```

或者：

```cpp
std::vector<int> vec {1,2,3,4,5};
```

每当编译器看到大括号初始化列表 `{1,5,6,9,4}`，它都会隐创建一个 `std::initializer_list<T>` 对象，其中 `T` 是列表的数据类型。

我们可以这样创建 `std::initializer_list<T>` 的轻量对象：

```cpp
#include <initializer_list>
std::initializer_list<int> data = {1,2,3,4,5};
```

`std::initializer_list<T>` 是一个类似数组的容器。它具有以下函数：

- `size()`：返回列表的大小
- `begin()`：返回列表起始的迭代器
- `end()`：返回列表结束的迭代器

# 现代 C++：explicit 关键字 (C++11)

C++ 编译器会在需要时隐式执行类型转换。示例：

```cpp
int x = 3;
float y = x + 5.5;
```

在执行加法之前，`x` 会被转换为浮点数类型。隐式类型转换通常涉及类型扩展。

我们可以使用 *explicit* 关键字防止编译器隐式转换类型。*explicit* 常用于修饰构造函数。考虑以下示例：

```cpp
class Array {
    public:
        explicit Array(size_t x);
};
```

这将防止构造函数中参数 `x` 的隐式类型转换。
