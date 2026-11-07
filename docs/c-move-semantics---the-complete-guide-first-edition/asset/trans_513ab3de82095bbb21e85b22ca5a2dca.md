

```cpp
}
```

我们将 `range` 声明为通用引用的原因是，我们希望能够将其绑定到*每一个*范围上，以便可以使用它两次（一次用于请求其开始，一次用于请求其结束），而无需创建副本，也不会丢失该范围是否为 const 的信息。

该循环应适用于以下情况：

- 一个非常量值：

```cpp
std::vector<int> coll;
...
for (int& i : coll) {
    i *= 2;
}
```

- 一个 const 值：

```cpp
const std::vector<int> coll{0, 8, 15};
...
for (int i : coll) {
    ...
}
```

- 一个纯右值：

```cpp
for (int i : std::vector<int>{0, 8, 15}) {
    ...
}
```

请注意，对于所有这些情况，没有其他方式来声明 range：

- 使用 `auto`，我们会创建范围的副本（这会耗时，并禁止修改元素）。
- 使用 `auto&`，我们会禁止使用临时纯右值初始化范围。
- 使用 `const auto&&`，我们会失去所遍历范围的任何非常量性。

然而，请注意，按当前规定的方式，基于范围的 for 循环存在一个重大问题。如下代码：

```cpp
std::vector<std::string> createStrings();

...

for (char c : createStrings().at(0)) {    // fatal runtime error
    ...
}
```

会变成：

```cpp
std::vector<std::string> createStrings();
...
auto&& range = createStrings().at(0);    // OOPS: universal reference to reference
auto pos = range.begin();                // return value of createStrings() destroyed here
auto end = range.end();
for (; pos != end; ++pos) {
    char c = *pos;
}
...
```

所有有效引用都会延长其所绑定值的生命周期。这也适用于右值引用。然而，我们绑定的不是 `createStrings()` 的返回值（那样会正常工作）；我们绑定的是 `at()` 返回的、对 `createStrings()` 返回类型的引用。这意味着我们延长的是该引用的生命周期，而不是 `createStrings()` 返回值的生命周期。因此，该循环遍历的是已经被销毁的字符串。

### 使用基于范围的 for 循环

即使在*调用*基于范围的 for 循环时，通用引用也可能有意义。

要在遍历元素时修改它们，必须使用非常量引用。考虑一个函数模板，它将传入的值赋给传入集合的所有元素：

```cpp
template<typename Coll, typename T>
void assign(Coll& coll, const T& value) {
    for (auto& elem : coll) {
        elem = value;
    }
}
```

看起来它通常适用于所有容器和元素类型（在支持赋值的情况下）：

```cpp
std::vector<int> coll1{0, 8, 15};
...
assign(coll1, 42);   // OK

std::vector<std::string> coll2{"hello", "world"};
...
assign(coll2, "ok"); // OK
```

然而，有一种情况它会突然无法工作：

```cpp
std::vector<bool> collB{false, true, false};
...
assign(collB, true); // ERROR: cannot bind non-const lvalue reference to an rvalue
```

发生了什么？让我们看看基于范围的 for 循环在这里展开成的代码：

```cpp
std::vector<bool> coll{false, true, false};
...
{
    auto&& range = coll;                  // OK: universal reference to reference
    auto pos = range.begin();             // OK
    auto end = range.end();               // OK
    for ( ; pos != end; ++pos ) {         // OK
        auto& elem = *pos;                // ERROR: cannot bind non-const lvalue reference to an rvalue
        elem = elem + elem;
    }
}
```

问题在于，`std::vector<bool>` 中的元素不是 bool 类型的对象；它们是单个位。其实现方式是，对于 `std::vector<bool>`，对元素的引用类型*不是*对元素类型的引用。类 `std::vector<bool>` 的实现是主模板 `std::vector<T>` 实现的部分特化，其中对元素的引用是代理类的对象，你可以像使用引用一样使用它：

```cpp
namespace std {
    template<...>
      class vector<bool, ...> {
      public:
        ...
        class reference {
          ...
        };
        ...
      };
}
```

当解引用迭代器时，会返回这个类 `std::vector<bool>::reference` 的一个值。因此，在基于范围的 for 循环的展开中，语句

```cpp
auto& elem = *pos;
```

试图将一个非常量左值引用绑定到临时对象（纯右值），这是不允许的。然而，这个问题有一个解决方案：在调用基于范围的 `for` 循环时改用通用引用：

```cpp
template<typename Coll, typename T>
void assign(Coll& coll, const T& value) {
    for (auto&& elem : coll) {  // note: universal reference support proxy element types
        elem = value;
    }
}
```

由于通用引用可以绑定到任何值类别的任何对象（甚至是纯右值），因此将这段泛型代码用于 `vector<bool>` 现在可以编译：

```cpp
std::vector<bool> collB{false, true, false};
...
assign(collB, true);  // OK (universal reference used to bind to an element)
```

因此，我们找到了使用非转发通用引用的另一个原因：它们可以绑定到未实现为引用的引用类型。或者更一般地说：它们允许我们绑定到作为代理类型提供的非常量对象，以便操作对象。

### 11.4 Lambda 中的完美转发

如果你想完美转发泛型 lambda 的参数，你也必须使用通用引用和 `std::forward<>`。不过，你只需使用 `auto&&` 来声明通用引用。

考虑我们已经在函数模板中见过的示例：

```cpp
auto callFoo = [](auto&& arg) {        // arg is a universal/forwarding reference
    foo(std::forward<decltype(arg)>(arg));  // perfectly forward arg
};
```

```cpp
std::string s{"BLM"};
callFoo(s);                 // OK, arg is std::string&
callFoo(std::move(s));     // OK, arg is std::string&&
```

请注意，从 C++20 起，可以通过使用模板参数声明 lambda 来避免使用 decltype(arg)。

以下泛型 lambda 使用这一点来完美转发可变数量的参数：

```cpp
[](auto&&... args) {
    ...
    foo(std::forward<decltype(args)>(args)...);
};
```

请记住，lambda 只是定义函数对象（即定义了 operator() 以允许将其用作函数的对象）的一种简便方式。上面的定义会展开为一个编译器定义的类（闭包类型），其中通用引用被定义为模板参数：

```cpp
class NameDefinedByCompiler {
    ...
public:
    template<typename... Args>
    auto operator() (Args&&... args) const {
        ...
        foo(std::forward<decltype(args)>(args)...);
    }
};
```

再次注意，使用 const（或 volatile）限定的泛型右值引用不是通用引用。这也适用于 lambda。如果参数使用 const auto&& 声明，则只能传递右值：

```cpp
auto callFoo = [](const auto&& arg) {  // arg is not a universal reference
    ...
};
```

```cpp
const std::string cs{"BLM"};
callFoo(cs);                 // ERROR: cs is not an rvalue
callFoo(std::move(cs));     // OK, arg is const std::string&&
```

在这个 lambda 内部，使用 std::move() 就足以完美转发传入的参数。

本页有意留空

## 第 12 章：使用 `decltype(auto)` 完美返回

在讨论了完美转发参数以及完美传递返回值之后，我们现在必须讨论完美返回值。本章介绍新的占位符类型 `decltype(auto)`。我们还将看到一些令人惊讶的后果，例如强烈建议不要在 return 语句中使用不必要的括号。

### 12.1 完美返回

在泛型代码中，我们经常计算一个值，然后将其返回给调用者。问题是，我们如何完美地返回该值，同时仍保留它原本的类型和值类别？换句话说：我们应该如何声明以下函数的返回类型：

```cpp
template<typename T>
??? callFoo(T&& arg)
{
    return foo(std::forward<T>(arg));
}
```

在这个函数中，我们使用完美转发的参数 `arg` 调用一个名为 `foo()` 的函数。我们不知道 `foo()` 针对此类型返回什么；它可能是一个临时值（纯右值）、一个左值引用或一个右值引用。返回类型可能是 const，也可能不是 const。

那么，我们如何将 `foo()` 的返回值完美地返回给 `callFoo()` 的调用者？有几种方案行不通：

- 返回类型 `auto` 会移除 `foo()` 返回类型中的引用。例如，如果我们提供对容器元素的访问（将 `foo()` 视为 vector 的 `at()` 成员函数或下标运算符），`callFoo()` 将不再提供对该元素的访问。此外，我们可能会创建不必要的副本（如果没有被优化掉）。

