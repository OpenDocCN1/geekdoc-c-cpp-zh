

```cpp
public:
...
};
```

你现在需要为 `lackDMA` 类定义显式的析构函数、拷贝构造函数和赋值运算符吗？答案是不需要的。

首先，考虑析构函数的需求。如果你不定义，编译器会定义一个无所事事的默认析构函数。实际上，派生类的默认析构函数总是会执行操作；它在执行完自己的代码后会调用基类的析构函数。我们假设 `lackDMA` 的成员不需要任何特殊操作，因此默认析构函数就足够了。

接下来考虑拷贝构造函数。正如你在第 12 章中看到的，默认拷贝构造函数执行成员级拷贝（memberwise copying），这对于动态内存分配是不恰的。然而，对于 `lackDMA` 成员来说，成员级拷贝是可以的。这就涉及到继承自 `baseDMA` 对象的问题。因此，拷贝使用了针对相关数据类型定义的拷贝形式。将 `long` 拷贝到 `long`是通过普通赋值完成的。拷贝类成员或继承的类组件是通过该类的拷贝构造函数完成的。因此，`lackDMA` 部分的默认拷贝构造函数使用显式的 `basedDMA` 拷贝构造函数来拷贝 `baseDMA` 对象。所以，对于 `lackDMA` 成员，默认拷贝构造函数是好的，对于继承的 `baseDMA` 对象它也是好的。

相同的情况也适用于赋值。类的默认赋值运算符会自动为基类组件使用基类的赋值运算符。

这些关于被继承对象的属性也同样适用于其本身就是对象的类成员。例如，第 10 章“对象与类”通过使用 `string` 对象来表示公司名称，实现了 `Stock` 类。标准的 `string` 类使用了动态内存分配。现在你可以看到为什么这会产生问题。默认的 `Stock` 拷贝构造函数将使用 `string` 拷贝构造函数来拷贝对象的公司成员，默认的 `Stock` 赋值运算符将使用 `string` 赋值运算符来赋值对象的公司成员，而 `Stock` 析构函数（默认或其他）会自动调用 `string` 析构函数。

## 案例 2：派生类确实使用了 new

假设派生类使用了 `new`：

```cpp
// derived class with DMA
class hasDMA :public basedDMA
{
private:
    char * style; // use new in constructors
public:
    ...
};
```

# 继承与动态内存分配

在这种情况下，你自然必须为派生类定义显式的析构函数、拷贝构造函数和赋值运算符。让我们逐一考虑这些方法。

派生类的析构函数会自动调用基类的析构函数，因此它的责任是清理派生类构造函数执行之后的工作。因此，`hasDMA` 必须释放 `style` 指针管理的内存，并可以依靠 `baseDMA` 来释放 `label` 指针管理的内存：

```cpp
baseDMA::baseDMA() // takes care of baseDMA stuff
{
    delete [] label;
}
```

```cpp
hasDMA::hasDMA() // takes care of hasDMA stuff
{
    delete [] label;
}
```

接下来考虑拷贝构造函数。`baseDMA` 的拷贝构造函数遵循 `char` 数组的通常模式。它们使用 `strlen()` 找到存储 C 风格字符串所需的长度，分配足够的内存（字符数加上一个空字符），并使用 `strcpy()` 函数将原始字符串拷贝到目标：

```cpp
baseDMA::baseDMA(const baseDMA & rs)
{
    label = new char[std::strlen(rs.label) + 1];
    std::strcpy(label, rs.label);
    rating = rs.rating;
}
```

`hasDMA` 的拷贝构造函数只能访问 `hasDMA` 数据，因此它必须调用 `baseDMA` 的拷贝构造函数来处理数据的 `baseDMA` 部分：

```cpp
hasDMA::hasDMA(const hasDMA & hs)
{
    style = new char[std::strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
}
```

需要注意的是，成员初始化列表将一个 `hasDMA` 引用传递给 `baseDMA` 构造函数。并没有以 `hasDMA` 引用作为参数的 `baseDMA` 构造函数，但也不需要。这是因为 `baseDMA` 的拷贝构造函数有一个基引用参数，而基类可以引用派生类型。因此，`baseDMA` 拷贝构造函数使用 `hs` 参数中的 `baseDMA` 部分来构造新对象的 `baseDMA` 部分。

接下来考虑赋值运算符。`baseDMA` 的赋值运算符遵循通常模式：

```cpp
baseDMA &baseDMA::operator=(const baseDMA & rs)
{
    if (this == &rs)
        return *this;
    delete []label;
    label = new char[std::strlen(rs.label) + 1];
    std::strcpy(label, rs.label);
    rating = rs.rating;
    return *this;
}
```

由于 `hasDMA` 也使用了动态内存分配，它也需要一个显式的赋值运算符。作为 `hasDMA` 的方法，它只能直接访问 `hasDMA` 数据。尽管如此，派生类的显式赋值运算符必须处理对继承的基类赋值对象的赋值。你可以通过显式地调用基类赋值运算符来实现这一点，如下所示：

```cpp
hasDMA &hasDMA::operator=(const hasDMA & hs)
{
    if (this == &hs)
        return *this;
    baseDMA::operator=(hs); // copy base portion
    delete []style;
    style = new char[std::strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
    return *this;
}
```

下面的语句看起来可能有一点奇怪：
`baseDMA::operator=(hs); // copy base portion`

通过使用函数符号而不是赋值符号，`baseDMA::operator=(hs); // copy base portion` 
实际上，这句话意味着：`*this = hs;` 
默认，使用函数符号而不是赋值符号，派生赋值赋值运算符处理继承的基类赋值运算符。

