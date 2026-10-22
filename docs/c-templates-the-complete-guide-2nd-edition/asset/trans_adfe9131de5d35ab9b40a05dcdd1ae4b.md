

如果产生了一个纯右值，引用类型会导致悬空引用，但幸运的是，对于这种情况，`decltype(auto)`会产生一个对象类型（而不是引用类型）。

与 `auto` 不同，`decltype(auto)` 不允许使用会修改其类型的限定符或声明符运算符。例如：

```cpp
decltype(auto)* p = (void*)nullptr; // invalid
int const N = 100;
decltype(auto) const NN = N*N; // invalid
```

还要注意，初始化器中的括号可能是有意义的（因为它们对于 `decltype` 构造来说是有意义的，如第 6.1 节第 91 页所述）：

```cpp
int x;
decltype(auto) z = x; // object of type int
decltype(auto) r = (x); // reference of type int&
```

这尤其意味着括号会对返回语句的有效性产生严重影响：

```cpp
int g();
...
decltype(auto) f() {
int r = g();
return (r); // run-time ERROR: returns reference to temporary
}
```

自 C++17 起，`decltype(auto)` 也可用于可推导的非类型参数（参见第 15.10.1 节第 296 页）。以下示例说明了这一点：

```cpp
template<decltype(auto) Val> class S
{
...};
constexpr int c = 42;
extern int v = 42;
S<c> sc; // #1 produces S<42>
S<(v)> sv; // #2 produces S<(int&)v>
```

在第 #1 行，`c` 周围缺少括号导致可推导参数的类型为 `c` 本身的类型（即 `int`）。由于 `c` 是值为 42 的常量表达式，这等价于 `S<42>`。在第 #2 行，括号导致 `decltype(auto)` 成为引用类型 `int&`，它可以绑定到类型为 `int` 的全局变量 `v`。因此，通过此声明，类模板依赖于对 `v` 的引用，并且 `v` 的值任何更改都可能影响类 `S` 的行为（有关详细信息，请参见第 11.4 节第 167 页）。`(S<v>` without ...

```cpp
template<typename T>
void deduceInitList(std::initializer_list<T>);
...
deduceInitList({ 2, 3, 5, 7 }); // OK: T deduced as int
```

那么推导就成功了。因此，用 `=` 标记进行拷贝初始化的 `auto` 变量与初始化列表的初始化是这样定义的：

```cpp
auto primes = { 2, 3, 5, 7 }; // primes is std::initializer_list<int>
deduceT(primes); // T deduced as std::initializer_list<int>
```

在 C++17 之前，对应的 `auto` 变量的直接初始化（即不使用 `=` 标记）也是这样处理的，但在 C++17 中已更改，以更好地匹配大多数程序员期望的行为：

```cpp
auto oops { 0, 8, 15 }; // ERROR in C++17
auto val { 2 }; // OK: val has type int in C++17
```

在 C++17 之前，这两种初始化都是有效的，将 `oops` 和 `val` 都初始化为类型 `initializer_list<int>`。

有趣的是，对于具有可推导占位符类型的函数，返回大括号初始化列表是无效的：

```cpp
auto subtleError() {
  return { 1, 2, 3 }; // ERROR
}
```

这是因为函数作用域中的初始化列表是一个指向底层数组对象的对象（其元素值在列表中指定），该对象在函数返回时过期。允许这种构造因此会鼓励实际上是悬空引用的情况。

当多个变量声明共享同一个 `auto` 时，会出现另一种特殊情况，如下所示：

```cpp
auto first = container.begin(), last = container.end();
```

在这种情况下，每个声明的推导都是独立进行的。换句话说，`first` 有一个发明的模板类型参数 `T1`，`last` 有另一个发明的模板类型参数 `T2`。只有当两种推导都成功，并且 `T1` 和 `T2` 的推导是相同类型时，声明才是良构的。这会产生一些有趣的情况：¹³

```cpp
char c;
auto *cp = &c, d = c; // OK
auto e = c, f = c+1; // ERROR: deduction mismatch char vs. int
```

这里，两个变量对使用共享的 `auto` 说明符声明。`cp` 和 `d` 的声明为 `auto` 推导出相同的类型 `char`，因此这是有效的代码。然而，`e` 和 `f` 的声明由于计算 `c+1` 时的提升而推导出 `char` 和 `int`，这种不一致导致错误。

对于推导返回类型的占位符，也会出现一个相当平行的特殊情况。考虑以下示例：

```cpp
auto f(bool b) {
if (b) {
return 42.0; // deduces return type double
} else {
return 0; // ERROR: deduction conflict
}
}
```

在这种情况下，每个 return 语句都是独立推导的，但如果推导出不同类型，程序就是无效的。如果返回的表达式递归调用函数，则无法进行推导，除非之前的推导已经确定了返回类型，否则程序无效。这意味着以下代码是无效的：

```cpp
auto f(int n)
{
if (n > 1) {
return n*f(n-1); // ERROR: type of f(n-1) unknown
} else {
return 1;
}
}
```

但以下在其他方面等价的代码是可以的：

```cpp
auto f(int n)
{
if (n <= 1) {
return 1; // return type is deduced to be int
} else {
return n*f(n-1); // OK: type of f(n-1) is int and so is type of n*f(n-1)
}
}
```

对 `addB()` 的调用因此不落入 SFINAE 过滤器，而是导致直接错误。因此，必须记住推导的返回类型不仅仅是复杂显式返回类型的简写，并且应谨慎使用（即理解它们不应在会依赖 SFINAE 属性的其他函数模板的签名中被调用）。

## 15.10.5 结构化绑定

C++17 添加了一个名为结构化绑定的新特性。¹⁴ 它最容易通过一个小示例来介绍：

```cpp
struct MaybeInt { bool valid; int value; };
MaybeInt g();
auto const&& [b, N] = g(); // binds b and N to the members of the result of g()
```

对 `g()` 的调用产生一个值（在本例中是类型为 `MaybeInt` 的简单类聚合），该值可以分解为“元素”（在本例中是 `MaybeInt` 的数据成员）。该调用的值是产生的，就好像方括号标识符列表 `[b, N]` 被替换为一个不同的变量名。如果该名称为 `e`，初始化将等价于：`auto const&& e = g();` 然后方括号标识符被绑定到 `e` 的元素。因此，你可以认为 `[b, N]` 引入了 `e` 的各个部分的命名（我们将在下面讨论该绑定的一些细节）。

在语法上，结构化绑定必须始终具有 `auto` 类型，可选择扩展为 `const` 和/或 `volatile` 限定符和/或 `&` 和/或 `&&` 声明符运算符（但不是 `*` 指针声明符或其他声明构造）。它后面跟着一个包含至少一个标识符的方括号列表（类似于 lambda 的“捕获”列表）。然后它必须后跟一个初始化器。

三种不同类型的实体可以初始化结构化绑定：

1. 第一种情况是简单的类类型，其中所有非静态数据成员都是公共的（如我们上面的示例）。对于此情况适用，所有非静态数据成员必须是公共的（要么全部直接在类本身中，要么全部在同一个、无歧义的公共基类中；不涉及匿名联合）。在这种情况下，方括号标识符的数量必须等于成员的数量，并且在结构化绑定的作用域内使用其中一个标识符相当于使用对象 `e` 所表示的相应成员（具有所有相关属性；例如，如果相应成员是位域，则它不是 ...

2. 第二种情况对应于 *数组*。这里有一个例子：

```cpp
int main() {
double pt[3];
auto& [x, y, z] = pt;
x = 3.0; y = 4.0; z = 0.0;
plot(pt);
}
```

不出所料，方括号标识符只是对未命名数组变量的相应元素的简写。数组元素的数量必须等于方括号标识符的数量。

这里是另一个例子：

```cpp
auto f() -> int(&)[2]; // f() returns reference to int array

auto [x, y] = f(); // #1
auto& [r, s] = f(); // #2
```

第 #1 行是特殊的：通常，对于这种情况，前面描述的实体 *e* 将从以下内容推导出来：`auto e = f();` 然而，这将推导出数组的衰减指针，这不是在对数组进行结构化绑定时发生的情况。相反，*e* 被推导为与初始化器类型对应的数组类型的变量。然后该数组按元素从初始化器 *复制*：这对于内置数组来说是一个有点不寻常的概念。¹⁵ 最后，`x` 和 `y` 成为表达式 `e[0]` 和 `e[1]` 的别名，分别。

第 #2 行不涉及数组复制并遵循 `auto` 的通常规则。因此，假设的 *e* 声明如下：`auto& e = f();` 这产生对数组的引用，并且 `x` 和 `y` 再次成为表达式 `e[0]` 和 `e[1]` 的别名，分别（它们是直接引用由对 `f()` 的调用产生的数组元素的左值）。

3. 最后，第三个选项允许 `std::tuple-like` 类通过使用 `get<>()` 的基于模板的协议将其元素分解。设 *E* 为表达式（*e*）的类型，其中 *e* 如上所述声明。由于 *E* 是表达式的类型，它永远不是引用类型。如果表达式 `std::tuple_size<E>::value` 是一个有效的积分常量表达式，它必须等于方括号标识符的数量（并且协议启动，优先于第一个选项，但不优先于第二个选项的 *数组*）。

