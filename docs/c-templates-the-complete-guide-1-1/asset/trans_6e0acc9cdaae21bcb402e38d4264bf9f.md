

## 第16章

## 特化与重载

到目前为止，我们已经研究了 C++ 模板如何允许将泛型定义扩展为一组相关的类、函数或变量。尽管这是一种强大的机制，但在许多情况下，某个操作的泛型形式对于特定的模板参数替换来说远非最优。

在支持泛型编程的其他流行编程语言中，C++ 有些独特，因为它拥有丰富的特性，能够用更专门的设施透明地替换泛型定义。在本章中，我们将研究允许从纯泛型进行务实偏离的两种 C++ 语言机制：模板特化和函数模板的重载。

### 16.1 当“泛型代码”不太适用时

考虑以下示例：

```cpp
template<typename T>
class Array {
private:
  T* data;
  ...
public:
  Array(Array<T> const&);
  Array<T>& operator= (Array<T> const&);
  ...

  void exchangeWith (Array<T>* b) {
    T* tmp = data;
    data = b->data;
    b->data = tmp;
  }

  T& operator[] (std::size_t k) {
    return data[k];
  }
  ...
};

template<typename T> inline
void exchange (T* a, T* b)
{
  T tmp(*a);
  *a = *b;
  *b = tmp;
}
```

对于简单类型，`exchange()` 的泛型实现效果很好。然而，对于具有昂贵拷贝操作的类型，泛型实现可能比针对特定类型量身定制的实现昂贵得多——无论是在机器周期还是内存存储方面。任何 `exchange()` 的实现都需要调用一次 `Array<T>` 的拷贝构造函数和两次其拷贝赋值运算符。对于大型数据结构，这些拷贝通常涉及复制相对大量的内存。然而，`exchange()` 的功能或许可以通过仅交换内部数据指针来实现，就像成员函数 `exchangeWith()` 中所做的那样。

### 16.1.1 透明定制

在我们之前的示例中，成员函数 `exchangeWith()` 为泛型 `exchange()` 函数提供了一种高效的替代方案，但需要使用不同函数这一点在几个方面造成不便：

- 1. `Array` 类的用户必须记住一个额外的接口，并且在可能时必须小心地使用它。
- 2. 泛型算法通常无法区分各种可能性。例如：

```cpp
template<typename T>
void generic_algorithm (T* x, T* y)
```

基于这些考虑，C++ 模板提供了透明地定制函数模板和类模板的方法。对于函数模板，这是通过重载机制实现的。例如，我们可以编写一组重载的 `quickExchange` 函数，如下所示：

```cpp
template<typename T>
void quickExchange(T& a, T& b) // #1
{
    T tmp(a);
    a = b;
    b = tmp;
}

template<typename T>
void quickExchange(Array<T>* a, Array<T>* b) // #2
{
    quickExchange(*a, *b); // uses #1
}

void demo(Array<int>* p1, Array<int>* p2)
{
    int a=42, y=7;
    quickExchange(a, y); // uses #1
    quickExchange(p1, p2); // uses #2
}
```

第一次调用 `quickExchange()` 有两个 `int` 类型的实参，因此推导在 #1 处定义的第一个模板时成功，而第二个模板不会被考虑。第二次调用有两个 `Array<int>*` 类型的实参，推导在 #2 处的第二个模板时成功。因此，第二次调用与第二个模板精确匹配，第一个模板不会被考虑。

当然，我们也可以重载以定制类模板。然而，类模板不支持重载。我们可以特化类模板，但特化并不匹配模板实参的类型。它们不是重载。下一节将讨论一种更强大的类模板定制技术，称为偏特化。但现在，让我们再看几个函数模板重载的示例。

### 16.1.2 语义透明性

上一节中重载的使用在实现实例化过程的透明定制方面非常有用，但同时也有些误导。特别是，我们可以看到模板的实现可能不同，而通过重载选择出来的那个实现可能并不按预期行为。事实上，不同的行为并不总是相同的。

通过考虑比较两个 `Array<int>` 类型值交换的代码，可以戏剧性地说明这一点：

```cpp
void distinguish(Array<int> a1, Array<int> a2)
{
    int a = a1[0];
    int b = a1[1];
    a1[0] = a2[0];
    a2[0] = a; // a1[0] after this
    a1[1] = a2[1];
    a2[1] = b; // a1[1] after this
    quickExchange(a1, a2); // uses #2
}
```

```cpp
void distinguish(Array<int> a1, Array<int> a2)
{
    int* p = &a1[0];
    int* q = &a1[1];
    a1[0] = a2[0];
    a2[0] = *p; // p no longer after this
    a1[1] = a2[1];
    a2[1] = *q; // q no longer after this
    quickExchange(a1, a2); // uses #2
}
```

这个示例表明，在调用 `quickExchange()` 之后，指向第一个 `Array a1` 的指针 `p` 变成了指向第二个数组的指针。然而，指向数组 `a1` 的指针在交换操作之后仍然指向 `a1`。这意味着被指向的值被交换了。

另一方面，对于第二次调用，所创建的重载集包含 `f<int>(int)`（由第一个模板生成）和 `f<int>(int,int)`（由第二个模板生成），因此只有第二个模板匹配。

### 16.2.1 签名

如果两个函数具有不同的签名，它们可以在程序中共存。我们将函数的签名定义为以下信息：

- 1. 函数的非限定名称（或生成它的函数模板的名称）
- 2. 该名称的类或命名空间作用域，以及如果名称具有内部链接，则声明该名称的翻译单元
- 3. 函数的 `const`、`volatile` 或 `const volatile` 限定（如果它是具有此类限定符的成员函数）
- 4. 成员函数的类型（如果不是成员函数，则为函数的类型）
- 5. 函数参数的类型（如果函数是从函数模板生成的，则在替换模板参数之前）
- 6. 如果函数是从函数模板生成的，则为其返回类型
- 7. 如果函数是从函数模板生成的，则为其模板参数和模板实参

这意味着以下模板及其实例化原则上可以在同一程序中共存：

```cpp
template<typename T1, typename T2>
void f(T1, T2);

template<typename T1, typename T2>
void f(T2, T1);

template<typename T1>
long f(T1);

template<typename T1>
char f(T1);
```

然而，当它们在同一个作用域中声明时，它们并不总能被使用，因为同时实例化两者会产生重载歧义。例如，在声明了上述所有模板的情况下调用 `f(2, 42)` 显然会产生歧义。另一个示例如下所示：

```cpp
#include <iostream>

template<typename T1, typename T2>
void f(T1, T2)
{
    std::cout << "f1(T1, T2)\n";
}

template<typename T1, typename T2>
void f(T2, T1)
{
    std::cout << "f2(T2, T1)\n";
}

// fine so far
int main()
{
    f<char, char>('a', 'b'); // ERROR: ambiguous
}
```

这里，函数 `f<T1 = char, T2 = char>(T1, T2)` 可以与函数 `f<T1 = char, T2 = char>(T2, T1)` 共存，但重载解析永远不会优先选择其中一个。如果这些模板出现在不同的翻译单元中，那么这两个实例化实际上可以存在于同一个程序中（并且，例如，链接器不应抱怨重复定义，因为这些实例化的签名是不同的）：

