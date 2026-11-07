

参数 `b` 变成了指向 const 字符数组的引用（`const char (&)[6]`）。因此，类型 `char [6]` 被推导为类型 `T2`，并用作第二个成员的类型。然而，不能用数组来初始化数组成员，因为你无法复制数组。

在这种情况下，应使用**衰减后**的类型作为返回类型，也就是按值传递参数时得到的类型（对于字符串字面量是 `const char*`）。

- 因此，在 C++03 中，函数定义被改为按值传递：

```cpp
template<typename T1, typename T2>
pair<T1,T2> make_pair (T1 a, T2 b)
{
    return pair<T1,T2>(a,b);
}
```

> 正如你可以在问题解决的原理说明中读到的那样，*“这似乎是三个建议中对标准改动最小的一种，而且任何效率方面的顾虑都远不及该解决方案带来的优势。”*

- 到了 C++11，`make_pair()` 必须支持移动语义，这意味着参数必须成为通用/转发引用。我们再次遇到了问题：对于引用，参数类型不会衰减。因此，定义修改如下：

```cpp
template<typename T1, typename T2>
constexpr pair<typename decay<T1>::type, typename decay<T2>::type>
make_pair (T1&& a, T2&& b)
{
    return pair<typename decay<T1>::type,
                typename decay<T2>::type>(forward<T1>(a),
                                          forward<T2>(b));
}
```

从 C++14 开始，可以写成如下形式：

```cpp
template<typename T1, typename T2>
constexpr pair<decay_t<T1>, decay_t<T2>>
make_pair (T1&& a, T2&& b)
{
    return pair<decay_t<T1>, decay_t<T2>>(forward<T1>(a), forward<T2>(b));
}
```

自 C++11 起，真正的实现甚至更加复杂：为了支持 `std::ref()` 和 `std::cref()`，该函数还会解包 `std::reference_wrapper<>` 的实例。

C++ 标准库在许多地方以类似的方式完美转发传入的参数，并且常与使用 `std::decay<>` 相结合。

### 15.3.2 `std::optional<>` 的移动语义

`std::optional<>` 是自 C++17 起可用的值类型，它通过“*没有值*”这一状态扩展了*所含类型*的可能值。这样就无需将类型的某个特定值标记为具有这种语义（例如指针的值 0）。

可选对象也支持移动语义。如果你整体移动该对象，状态会被复制，而所含对象（如果有的话）会被移动。结果，被移动过的对象仍然具有相同的状态，但任何值都会变为未指定。

不过，你也可以将值移入或移出所含对象。例如：

```cpp
std::optional<std::string> os;
std::string s = "a very very long string";
os = std::move(s);          // OK，移动
std::string s2 = *os;       // OK，复制
std::string s3 = std::move(*os);  // OK，移动
```

注意，在最后一次调用之后，`os` 仍然含有一个字符串值，但和通常的被移动对象一样，该值是未指定的。因此，只要你不对该值做任何假设，就可以使用它。你甚至可以在此处赋一个新的字符串值。

还要注意，某些重载确保了临时 optional 对象会被移动。考虑一个返回 optional 字符串的函数：

```cpp
std::optional<std::string> func();
```

在这种情况下，以下移动值的操作是有明确定义的：

```cpp
std::string s4 = func().value();  // OK，移动
std::string s5 = *func();         // OK，移动
```

这种行为是通过使用引用限定符为相应的成员函数提供右值重载来实现的：

```cpp
namespace std {
  template<typename T>
  class optional {
    ...
    constexpr T& operator*() &;
    constexpr const T& operator*() const&;
    constexpr T&& operator*() &&;
    constexpr const T&& operator*() const&&;

    constexpr T& value() &;
    constexpr const T& value() const&;
    constexpr T&& value() &&;
    constexpr const T&& value() const&&;
  };
}
```

通过使用引用限定符，当为右值（临时对象或用 `std::move()` 标记的对象）调用操作时，该类可以返回被移动的值：

```cpp
std::vector<std::string> coll;
std::optional<std::string> optStr;
...
coll.push_back(std::move(optStr).value());  // OK，将成员移入 coll
```

注意，`std::optional<>` 是 C++ 标准库中少数使用 const 右值引用的地方。原因在于 `std::optional<>` 是一种包装类型，它希望确保即使 const 对象被 `std::move()` 标记，并且所含类型为 const 右值引用提供了特殊行为，相关操作也能做正确的事。

## 15.4 智能指针的移动语义

原始指针无法从移动语义中获益（它们的地址值总是被复制），而智能指针则可以从移动语义中获益。

- 共享指针（`std::shared_ptr<>`）支持移动语义，这很有用，因为移动一个共享指针比复制一个要便宜得多。
- 独占指针（`std::unique_ptr<>`）甚至只支持移动语义，因为复制独占指针是不可能的。

### 15.4.1 `std::shared_ptr<>` 的移动语义

共享指针具有共享所有权的概念。多个共享指针可以“拥有”同一个对象，当最后一个所有者被销毁（或被赋新值）时，会调用所拥有对象的“删除器”。

例如：

```cpp
{
  std::shared_ptr<int> sp1;                    // 初始化不拥有任何东西的共享指针
  {
    auto sp2{std::make_shared<int>(42)};       // 初始化拥有新 int 的共享指针
    ...
    sp1 = sp2;                                 // sp1 和 sp2 现在共享所有权
    ...
    *sp2 = 77;                                  // 通过 sp2 修改值
    ...
  }                                            // sp2 被销毁，sp1 是唯一所有者
  std::cout << *sp1 << '\n';                    // 通过 sp1 使用修改后的值
}                                              // 最后一个所有者被销毁，因此调用 delete
```

在这个例子中，赋值运算符复制了 int 的所有权，这意味着之后两个共享指针都拥有该对象。然而，注意复制所有权是一项相当昂贵的操作。这是因为需要一个计数器来跟踪所有者的数量：

- 每次复制共享指针时，所有者计数器都会递增
- 每次销毁共享指针或赋予新值时，所有者计数器都会递减

此外，修改计数器的值也很昂贵，因为这种修改是原子操作，以避免多个线程处理拥有同一对象的共享指针时出现问题。

```cpp
std::unique_ptr<std::string> source()
{
    static long id{};

    // 用 new 创建字符串并让 ptr 拥有它：
    auto ptr = std::make_unique<std::string>("obj" + std::to_string(++id));
    ...
    return ptr;          // 将所有权转移给调用者
}

int main()
{
    std::unique_ptr<std::string> p;
    for (int i = 0; i < 10; ++i) {
        p = source();     // p 获得返回对象的所有权
                          // （之前 source() 返回的对象被删除）
        std::cout << *p << '\n';
        ...
    }
} // p 所拥有的最后一个对象被删除
```

与通常的被移动类型一样，要将所有权传递给接收方（sink）函数，你只能使用 `std::move()` 来传递：

```cpp
std::vector<std::unique_ptr<std::string>> coll;
std::unique_ptr<std::string> up;
...
coll.push_back(up);                 // 错误：禁止复制
coll.push_back(std::move(up));      // OK，将所有权移入 coll 的新元素中
```

如果你将独占指针传递给一个按引用接收参数的潜在接收方函数，你无法知道所有权是否被移动。所有权是否被移动取决于函数的实现。在这种情况下，你可以使用 operator bool() 来再次检查状态：

```cpp
std::unique_ptr<std::string> up;
...
sink(std::move(up));  // 可能将所有权移交给 sink()
if (up) {              // 它仍然拥有所有权吗？
    ...
}
```

或者，你可以确保所有权已经消失（资源被释放）：

```cpp
std::unique_ptr<std::string> up;
...
sink(std::move(up));  // 可能将所有权移交给 sink()
up.reset();            // 确保所有权消失（资源被删除）
```

