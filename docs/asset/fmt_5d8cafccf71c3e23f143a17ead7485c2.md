
由模板提供者确保在实例化模板时，不依赖模板参数的类型是可见的。此外，对于依赖模板参数的类型，在实例化模板时，由模板提供者确保它们是可见的。

> 注意：模板的定义和成员通常放在头文件中。

## 编译错误大多在实例化时报告

# C++ Primer 第五版

只有在实例化模板的特定实例时才生成代码这一事实，影响了我们如何了解模板内部代码的错误。通常情况下，有三个阶段编译器可能会标记错误。

第一阶段是编译模板时。编译器在这一阶段通常无法发现许多错误。它可以检测语法错误，例如忘记分号或拼错变量名，但无法发现类型。

第二个错误检测时间是在编译器看到模板的使用时。在这个阶段，编译器通常检查模板调用的参数是否合适。它还可以检查应该具有相同类型的两个参数是否如此。但无法更多。

当我们编写模板时，代码通常不能过于具体，但将使用的参数是具体的。例如，我们 `compare` 函数内部的代码：

点击此处查看代码图像

```
if (v1 < v2) return -1;      // 需要 T 对象支持 <
if (v2 < v1) return 1;       // 需要 T 对象支持 <
return 0;                    // 返回 int；不依赖于 T
```

假设参数类型具有 `<` 运算符。当编译器处理此模板体时，无法验证 `if` 语句中的条件是否合法。如果传递给 `compare` 的参数具有 `<` 操作，那么代码就是正确的，反之不然。例如：

点击此处查看代码图像

```
Sales_data << data1, data2;      data2) << endl;  // 错误：Sales_data 没有 <
cout << compare(data1, data2);
```

此调用实例化了一个将 `T` 替换为 `Sales_data` 的 `compare` 版本。`if` 尝试对 `Sales_data` 对象使用 `<`，但没有这样的运算符。这种实例化生成了一个无法编译的函数版本。然而，此类错误在编译器在 `Sales_data` 类型上实例化 `compare` 的定义之前无法检测。

> 警告：由调用者保证传递给模板的参数是有效的

支持模板所使用的任何操作，并确保这些操作在模板使用的上下文中表现正常。

## 练习 16.1.1 节

- **练习 16.1:** 定义实例化（`instantiation`）。

- **练习 16.2:** 编写并测试你自己的比较函数版本。

- **练习 16.3:** 在两个 `Sales_data` 对象上调用你的比较函数，以观察编译器在实例化期间如何处理错误。

- **练习 16.4:** 编写一个类似于库中 `find` 算法的模板。该函数需要两个模板参数，另一个用于指定值的类型。使用你的函数在 `vector<int>` 和 `list<string>` 中查找给定值。

- **练习 16.5:** 编写 § 6.2.4 (第 217 页) 中 `print` 函数的模板版本，该函数接收数组的引用，并能够处理任何大小和任何元素的数组。

- **练习 16.6:** 你将如何使用接受数组作为参数的库 `begin` 和 `end` 函数？定义你自己的这些函数版本。

- **练习 16.7:** 编写一个返回给定数组大小的 `constexpr` 模板。

- **练习 16.8:** 在第 108 页的“核心概念”中，我们注意到由于习惯，C++ 程序员倾向于使用 `!=` 而不是 `<`。请解释这一习惯的原理。

### 16.1.2. 类模板

类模板是生成类的蓝图。类模板与函数模板的区别在于，编译器无法推导出类模板的模板参数类型。相反，正如我们多次看到的，为了使用类模板，我们必须在模板名称后的尖括号 `< >` 内部提供额外信息（§ 3.3，第 97 页）。这些额外信息是用于替换模板参数的模板参数列表。

## 定义类模板

作为一个示例，我们将实现 `StrBlob` (§ 12.1.1，第 456 页) 的模板版本。我们将该模板命名为 `Blob`，以表示它不再特定于字符串。

与 `StrBlob` 一样，我们的模板将为它所持有的元素提供共享（且经过检查）访问。与该类不同，我们的模板可以用于几乎任意类型的元素。在使用库容器时，用户在使用 `Blob` 时必须指定元素类型。

与函数模板一样，类模板以 `template` 关键字开头，后紧跟模板参数列表。在类（及其成员）的定义中，我们使用模板作为在模板模板时将提供的类型或值的占位符：

# 点击此处查看代码图片

```
template <typename T> class Blob {
public:
    typedef T value_type;
    typedef typename std::vector<T>::size_type size_type;
    // 构造函数
    Blob();
    Blob(std::initializer_list<T> il);
    // Blob 中的元素数量
    size_type size() const { return data->size(); }
    bool empty() const { return data->empty(); }
    // 添加和移除元素
    void push_back(const T &t) { data->push_back(t); }
    // 移动版本：见 § 13.6.3 (第 548 页)
    void push_back(T&&t) { data->push_back(std::move(t)); }
    void pop_back();
    // 元素访问
    T& back();
    T& operator[](size_type i); // 定义在 § 14.5 (第 566 页)
private:
    std::shared_ptr<std::vector<T>> data;
    // 如果 data 无效则抛出 msg
    void check(size_type i, const std::string& msg) const;
};
```

我们的 `Blob` 包含一个名为 `T` 的模板参数。我们在任何引用 `Blob` 所持有元素类型的地方都使用该类型参数。例如，我们将提供访问 `Blob` 中元素的操作返回类型定义为 `T`。当用户实例化 `Blob` 时，这些对 `T` 的使用将被指定的模板参数类型替换。

除了模板参数列表外，这个类与 § 12.1.1（第 456 页）定义且在 § 12.1.6 中日期的版本相同。

## 实例化类模板

正如我们多次看到的，这个类与 § 12.1.1（第 456 页）定义且在 § 12.1.6 中日期的版本相同。

## 模板作用域内的模板类型引用

为了阅读代码，记住类模板的并不是类型的名称，这会有帮助。

## 类模板的成员函数

与任何类一样，我们可以在类体内部或外部定义类模板的成员函数。与其他任何类一样，在类体内定义的成员是隐式内联（`inline`）的。

`ret-type StrBlob::member-name(parm-list)`

对应的 `Blob` 成员将如下

点击此处查看代码图像

```cpp
template <typename T>
ret-type Blob<T>::member-name(parm-list)
```

## 检查与元素访问成员

我们首先定义检查成员，它用于验证一个给定的索引：

点击此处查看代码图像

```cpp
template <typename T>
void Blob<T>::check(size_type i, const std::string &msg)
{
    if (i >= data->size())
        throw std::out_of_range(msg);
}
```

除了类中的细节和模板参数列表名称外，该函数与原始的 `StrBlob` 成员相同。

下标运算符和 `back` 函数使用模板参数来指定返回类型，但在其他方面均保持不变

点击此处查看代码图像

```cpp
template <typename T>
T& Blob<T>::back()
{
    check(0, "back on empty Blob");
    return data->back();
}

template <typename T>
T& Blob<T>::operator[](size_type i)
{
    // 如果 i 太大，check 将抛出异常，防止访问不存在的元素
    check(i, "subscript out of range");
    return (*data)[i]);
}
```

在原始的 `StrBlob` 中，这些运算符返回 `string&`。模板版本将返回用于实例化 `Blob` 的任何类型。

`pop_back` 函数与我们原始的 `StrBlob` 成员几乎相同：

点击此处查看代码图像

```cpp
template <typename T>
void Blob<T>::pop_back()
```

```cpp
{
  check(0, "pop_back on empty Blob");
  data->pop_back();
}
```

下标运算符和 `back` 成员在 `const` 上进行了重载。我们将这些成员（以及 `front` 成员）的定义留作练习题。

## Blob 构造函数

与任何在类模板之外定义的其他成员一样，构造函数的开始是声明它所所属的类模板的模板参数：

点击此处查看代码图像

```cpp
template <typename T>
Blob<T>::Blob() : data(std::make_shared<std::vector<T>>()) { }
```

这里，我们在 `Blob<T>` 作用范围内定义了成员名称。与 `StrBlob` 默认构造函数（12.1.1，第 456 页）一样，该构造函数分配了一个空 `vector` 并将其指针存储在 `data` 中。正如我们看到的，我们使用类自身的类型参数作为分配的 `vector` 的模板参数。

同样，接收 `initializer_list` 的构造函数使用其类型 `T` 作为 `initializer_list` 参数的元素类型：

点击此处查看代码图像

```cpp
template <typename T>
Blob<T>::Blob(initializer_list<T> il)
  : data(std::make_shared<std::vector<T>>(il)) { }
```

与默认构造函数一样，此构造函数分配了一个新 `vector`。在这种情况下，我们从参数 `il` 初始化 `vector`。

要使用此构造函数，我们传递一个 `initializer_list`，其中的元素必须与 `Blob` 的元素类型兼容：

点击此处查看代码图像

```cpp
Blob<std::string> articles = {"a", "an", "the"};
```

该构造函数中的参数类型为 `initializer_list<string>`。列表中的每个字符串字面量都会被隐式转换为 `string`。

## 类模板成员函数的实例化

默认情况下，类模板的成员函数只有在程序使用该成员函数时才会被实例化。例如，这段代码

点击此处查看代码图像

```cpp
//
```

《C++ Primer》第五版

```cpp
// 实例化 Blob<int> 和 initializer_list<int> 构造函数
Blob<int> squares = {0,1,2,3,4,5,6,7,8,9};
// 实例化 Blob<int>::size() const
for (size_t i = 0; i != squares.size(); ++i) // 实例化 Blob<int>::operator[](size_t)
    squares[i] = i*; // 实例化
```

通过 `initializer_list<int>` 构造函数实例化了 `Blob<int>` 类及其所有的成员。

如果成员函数没有被实例化，它就不会被实例化。成员只有在我们使用它们时才被实例化的这一事实，允许我们实例化一个类型可能不满足模板相应操作要求的类（§9.2，第 329 页）。

> 注意：默认情况下，已实例化类模板的成员只有在成员成员被使用时才会被实例化。

## 在代码内部简化模板名称的使用

当我们使用类模板时，必须提供模板参数，这一规则有一个例外。在类本身的作用范围内，我们可以使用不带参数的模板名称：

点击此处查看代码图像

```cpp
// BlobPtr 在尝试访问不存在的元素时抛出异常
template <typename T> class BlobPtr {
public:
    BlobPtr() : curr(0) {}
    BlobPtr(T& a, size_t sz) : wptr(a.data()), curr(sz) {}
    T& operator*() const
        auto p = check(curr, "dereference past end");
        return (*p)[curr]; // (*p) 是对象指向的 vector
    // 增和递减
    BlobPtr& operator++; // 前置运算符
    BlobPtr& operator--();
private:
    // 如果 check 成功，返回 vector 的 shared_ptr
    std::shared_ptr<std::vector<T>> check(size_t const, const std::string &msg) const;
    // 存储 weak_ptr，这意味着底层 vector 可能被销毁
    std::weak_ptr<std::vector<T>> wptr;
    size_t curr; // 数组中的当前位置
};
```

仔细的读者会注意到 `BlobPtr` 的前置增递成员返回的是 `BlobPtr&` 而不是 `BlobPtr<T>&`。当我们在类模板的作用范围内时，编译器对待模板的引用就像我们提供了与模板所有者匹配的模板参数。也就是说，就像我们写的那样：

```cpp
BlobPtr<T>& operator++;
BlobPtr<T>& operator--;
```

## 在类外部使用类模板名称

当我们在类模板体之外定义成员时，必须记住，在看到类名之前，我们不在类作用范围内（§7.4，第 282 页）：

点击此处查看代码图像

```cpp
// 后置：增/递减对象返回不变的值
template <typename T>
BlobPtr<T>::operator++()
{
    // 后置增，返回当前状态
    BlobPtr<T> ret = *this;
    ++curr;
    return ret;
}

template <typename T>
BlobPtr<T>::operator--()
{
    // 后置减，返回当前状态
    BlobPtr<T> ret = *this;
    --curr;
    return ret;
}

template <typename T>
BlobPtr<T>::operator++()
{
    // 前置增
    ++curr;
    return *this;
}

template <typename T>
BlobPtr<T>::operator--()
{
    // 前置减
    --curr;
    return *this;
}
```

## 模板类型别名
