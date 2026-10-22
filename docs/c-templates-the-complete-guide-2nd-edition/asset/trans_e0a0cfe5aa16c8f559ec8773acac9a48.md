

## 12.4.3 函数参数包

*函数参数包* 是一种匹配零个或多个函数调用参数的函数参数。与模板参数包类似，函数参数包使用省略号 (...) 在函数参数名称之前（或代替函数参数名称）引入，并且与模板参数包类似，函数参数包在使用时必须通过包展开进行展开。模板参数包和函数参数包合称为 *参数包*。

与模板参数包不同，函数参数包始终是包展开，因此其声明的类型必须包含至少一个参数包。在下面的示例中，我们引入了一个新的 Point 构造函数，它从提供的构造函数参数中复制初始化每个 mixin：

```cpp
template<typename... Mixins>
class Point : public Mixins...
{
double x, y, z;
public:
//default constructor, visitor function, etc. elided
Point(Mixins... mixins) // mixins is a function parameter pack
: Mixins(mixins)... { } //initialize each base with the supplied mixin value
};
```

```cpp
struct Color { char red, green, blue; };
struct Label { std::string name; };
Point<Color, Label> p({0x7F, 0, 0x7F}, {"center"});
```

函数模板的函数参数包可能依赖于该模板中声明的模板参数包，这允许函数模板接受任意数量的调用参数而不丢失类型信息：

```cpp
template<typename... Types>
void print(Types... values);
```

```cpp
int main()
{
std::string welcome("Welcome to ");
print(welcome, "C++", 2011, '\n'); //calls print<std::string, char const*, int, char>
}
```

调用函数模板 print() 时，参数的类型将被放入参数包中以替换模板类型参数包 `Types`，而实际参数值将被放入参数包中以替换函数参数包 `values`。参数如何从调用中确定的过程在第 15 章中有详细描述。现在只需注意，`Types` 中的第 *i* 个类型是 `values` 中第 *i* 个值的类型，并且这两个参数包都在函数模板 `print()` 的主体内可用。

`print()` 的实际实现使用递归模板实例化，这是一种在第 8.1 节第 123 页和第 23 章中描述的模板元编程技术。

在参数列表末尾出现的未命名函数参数包与 C 风格的“vararg”参数之间存在语法歧义。例如：

```cpp
template<typename T> void c_style(int, T...);
template<typename... T> void pack(int, T...);
```

在第一种情况下，`T...` 被视为 `T, ...`：类型为 T 的未命名参数，后跟 C 风格的 vararg 参数。在第二种情况下，`T...` 构造被视为函数参数包，因为 T 是一个有效的展开模式。可以通过在省略号前添加逗号来强制消除歧义（这确保省略号被视为 C 风格的“vararg”参数），或在 `...` 后跟一个标识符，使其成为命名的函数参数包。请注意，在通用 lambda 中，尾随的 `...` 如果紧接其前的类型（中间没有逗号）包含 auto，则将被视为表示参数包。

## 12.4.4 多个和嵌套的包展开

包展开的模式可以任意复杂，并且可能包含多个不同的参数包。在实例化包含多个参数包的包展开时，所有参数包必须具有相同的长度。由此产生的类型或值的序列将通过将每个参数包的第一个参数代入模式，然后是每个参数包的第二个参数，依此类推，按元素方式形成。例如，下面的函数在将其转发给函数对象 `f` 之前复制其所有参数：

```cpp
template<typename F, typename... Types>
void forwardCopy(F f, Types const&... values) {
  f(Types(values)...);
}
```

调用参数包展开命名了两个参数包，`Types` 和 `values`。在实例化此模板时，`Types` 和 `values` 参数包的按元素展开会产生一系列对象构造，这会通过将其转换为 `Types` 中的第 *i* 个类型来构建 `values` 中第 *i* 个值的副本。在包展开的语法解释下，三参数的 `forwardCopy` 看起来像这样：

```cpp
template<typename F, typename T1, typename T2, typename T3>
void forwardCopy(F f, T1 const& v1, T2 const& v2, T3 const& v3) {
  f(T1(v1), T2(v2), T3(v3));
}
```

包展开本身也可以嵌套。在这种情况下，参数包的每次出现都由其最近的封闭包展开“展开”（并且仅由该包展开）。下面的示例说明了涉及三个不同参数包的嵌套包展开：

```cpp
template<typename... OuterTypes>
class Nested {
  template<typename... InnerTypes>
  void f(InnerTypes const&... innerValues) {
    g(OuterTypes(InnerTypes(innerValues)...)...);
  }
};
```

在对 `g()` 的调用中，模式为 `InnerTypes(innerValues)` 的包展开是最内层的包展开，它展开了 `InnerTypes` 和 `innerValues`，并为 `OuterTypes` 所表示的对象的初始化产生了一系列函数调用参数。外层包展开的模式包含内层包展开，从内层展开产生的函数调用参数序列初始化 `OuterTypes` 中的每个类型，从而为函数 `g()` 产生一组调用参数。在此包展开的语法解释下，其中 `OuterTypes` 有两个参数，而 `InnerTypes` 和 `innerValues` 都有三个参数，嵌套变得更加明显：

```cpp
template<typename O1, typename O2>
class Nested {
  template<typename I1, typename I2, typename I3>
  void f(I1 const& iv1, I2 const& iv2, I3 const& iv3) {
    g(O1(I1(iv1), I2(iv2), I3(iv3)),
      O2(I1(iv1), I2(iv2), I3(iv3)));
  }
};
```

多个和嵌套的包展开是一种强大的工具（例如，参见第 26.2 节）。

## 12.4.5 零长度包展开

包展开的语法解释对于理解可变参数模板在不同数量参数下的实例化行为是有用的工具。然而，在存在零长度参数包的情况下，语法解释通常会失败。为了说明这一点，请考虑第 12.4.2 节第 202 页的 `Point` 类模板，用零个参数进行语法替换：

```cpp
template<>
class Point : {
Point() : { }
};
```

上面编写的代码格式错误，因为模板参数列表现在为空，并且空基类和基类初始化列表中各有一个多余的冒号字符。

包展开实际上是语义构造，参数包的任何大小的替换都不会影响包展开（或其封闭的可变参数模板）的解析方式。相反，当包展开展开为空列表时，程序在语义上表现得好像该列表不存在一样。实例化 `Point<>` 最终没有基类，其默认构造函数没有基类初始化器，但本身是格式良好的。此语义规则即使在零长度包展开的语法解释会是格式良好（但不同）的代码时也成立。例如：

```cpp
template<typename T, typename... Types>
void g(Types... values) {
    T v(values...);
}
```

可变参数函数模板 `g()` 创建一个值 `v`，该值从给定的值序列直接初始化。如果该值序列为空，则 `v` 的声明在语法上看起来像一个函数声明 `T v()`。然而，由于对包展开的替换是语义上的，并且不能影响解析产生的实体种类，`v` 是用零个参数初始化的，即值初始化。[^11]

