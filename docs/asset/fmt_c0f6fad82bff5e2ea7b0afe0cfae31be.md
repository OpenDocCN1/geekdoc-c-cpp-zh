
### 9.2.9.5 `decltype` 限定符 [dcltype.decltype]

对于表达式 `E`，`decltype(E)` 表示的类型定义如下：

+   (1.1) 如果 `E` 是命名结构绑定的不带括号的 id-expression (9.6)，`decltype(E)` 是结构绑定规范中给出的引用类型；
(1.2) 否则，如果 `E` 是命名非类型模板的不带括号的 id-expression (13.2)，`decltype(E)` 是执行必要的类型推导 9.2.9.6, 9.2.9.7 后的类型参数；
(1.3) 否则，如果 `E` 是不带括号的 id-expression 或不带括号的类成员 (7.6.1.5)，`decltype(E)` 是命名 `E` 的实体类型。如果不存在此类实体，或者 `E` 指定一组重载函数，则程序格式错误；
(1.4) 否则，如果 `E` 是即将值 (xvalue)，`decltype(E)` 为 `T&&`，其中 `T` 是 `E` 的类型；
(1.5) 否则，如果 `E` 是左值 (lvalue)，`decltype(E)` 为 `T&`，其中 `T` 是 `E` 的类型；
(1.6) 否则，`decltype(E)` 为其类型。

`decltype` 限定符的的操作数是不经求值的表达式 (7.2)。

[示例 1:
`const int& foo;`
`int i;`
`struct A { double x; };`
`class B { public: A(int v) };`
`decltype(foo) x = 17;` // 类型为 `const int&`
`decltype(i) y = 2;` // 类型为 `int`
`decltype(a->x) z = 4;` // 类型为 `const double`
-- 示例结束

[注 1：确定 `decltype` 限定符的规则是一个纯值 (prvalue)，并且不是（可能带有括号的）立即调用 (7.7)，不应用临时转换 (7.3.5)，且不会为纯值产生对象。纯值的类型可以是不完全类型或抽象类类型。
注 2：具有泛型占位符类型确保了该函数是一个缩写模板函数 (9.3.4)，且该 lambda 是泛型 lambda (7.5.5)。 
使用占位符类型声明的变量类型通过其初始化进行推导。在 `dcl-specifier` 和 `type-specifier` 中，在任何允许声明的上下文中通过 `conversion-id`。如果函数包含返回类型 (U.3.4)，则返回类型指定函数的返回类型。否则，函数声明指定返回类型。如果函数的返回类型包含占位符类型，则通过函数体内的非丢弃返回语句进行推导 (8.5.2

注 3：与其不同，`auto-specifier` 对于声明是不必要的。使用占位符类型声明的变量在初始化声明 (9.4) 中是允许的。占位符类型应当作为 `dcl-specifiers` 之一，且 `dcl-specifier` 后面跟随一个或多个声明符，其后面跟随非空初始化。其形式为：

```
(expression-list
the expression-list 应该是一个赋值表达式)
```

### 9.2.9.6 占位符类型限定符 [dcl.auto]

### 9.2.9.6 通用 [dcl.auto]

```
placeholder-type-specifier:
type-constraint-opt auto
type-constraint (auto)
```

+   1 占位符类型限定符指定一个将被替换的占位符类型。

+   2 形式为 `constraint-opt auto` 的占位符类型限定符可以作为函数声明或 lambda 表达式的 `dcl-specifier`，如果它是引入返回类型的 `auto-specifier`，它就是一个泛型占位符。

[注 1：具有泛型占位符类型确保了函数是一个缩写模板函数 (9.3.4)，且该 lambda 是泛型 lambda (7.5.5)。— 结束]

+   3 使用占位符类型声明的变量类型通过其初始化进行推导。在 `dcl-specifier` 和 `type-specifier` 中，通过 `conversion-id` 在任何允许声明的上下文中。如果函数包含返回类型 (U.3.4)，返回类型指定函数的返回类型。否则，函数声明指定返回类型。如果函数的返回类型包含占位符类型，则通过函数体内的非丢弃返回语句进行推导 (8.5.2

# ISO/IEC 14882:2020(E)

```cpp
Example 1:
auto x = 5;               // OK: x has int
const auto *v = &x, u = 6; // OK: x has const int, u has const int
static auto y = 0.0;     // OK: y has double
auto int r;               // error: auto is not a storage-class-classifier
auto f() -> int;          // OK: f returns int
auto g() { return 0.0; } // OK: g returns double
// OK: g's return type will be deduced when it is defined
```

类型-指针（type-pointer）也可用于引入结构化推导（9.6）。

占位符类型（placeholder type）也可以用于新表达式（new-expression）中新类型标识符（new-type-id）或类型标识符（type-id）的类型指定符（type-specifier）中（7.6.2.8），以及模板参数（template-parameter）中的声明指定符参数推导声明符（decl-specifier-parameter-deduced-decl-specifier）（13.2）。

在 9.9.2.6 未显式允许的语文中使用占位符类型的程序是格式错误的（ill-formed）。

如果整数声明符列表（int-declarator-list）包含多个整数声明符（int-declarator），它们都构成了变量的声明。每个被声明变量的类型通过占位符类型推导（9.9.2.6）进行推导，如果替换占位符类型的类型在每次推导中不相同，则该程序是格式错误的。

```cpp
Example 2:
auto x = 5, y = &x; // OK: auto is int
auto a = 5, b = { 1, 2 }; // error: different types for auto
```

如果一个具有包含占位符类型的推导返回类型的程序具有多个非丢弃的返回语句（non-discarded return statements），则对每个返回语句进行返回类型推导。如果每次推导的返回类型不相同，则该程序是格式错误的。

如果一个使用占位符类型且具有推导返回类型的程序没有任何非丢弃的返回语句，则在函数体结束时从一个没有操作数数的返回语句中推导返回类型。

```cpp
Example 3:
auto f() { // OK: return type is void
auto g() { // error: cannot deduce auto* from void()
```

使用占位符类型且具有推导返回类型的导出函数（exported function），应在其包含导出声明的翻译单元中定义，位于私有模块片段（private-module-fragment，如果有）之外。

> [Note 2: 推导的返回类型不能具有内部链接（internal linkage）的名称（6.6）。— 注释结束]

如果在函数中已经见过一个未推导的占位符类型的名称，则该程序是格式错误的。一旦看到一个推导的返回语句，从该语句推导出的返回类型将用于函数的其余部分，包括其他返回语句中。

```cpp
Example 4:
auto n = n; // error: n initializer refers to n
auto f();
void v(int* k) { // error: f's return type is unknown
auto sum(int i) {
  if (i == 1)
    return 1; // sum's return type is int
  else
    return sum(i-1)+i;
}
```

当函数体包含带有非依赖性参数（non-dependent argument）的返回语句时，模板实体（templated entity）在定义实例化时会发生推导的返回。

> [Note 3: 因此，任何对模板函数的使用都会导致隐式实例化。此实例化产生的任何错误都不在函数类型的直接上下文中，并可能导致程序格式错误（13.10.5）。— 注释结束]

```cpp
Example 5:
template <class T> auto f(T t) { return t; } // return type deduced at instantiation time
typedef(f(int)) fint_; // instantiates f<int> to deduce return type
template<class T> auto f(T* t) { return *t; } // instantiates f<int> to determine return types,
void g() { int (*p)(int) = &f; } // chooses second
```

对于使用占位符类型的已声明返回类型的函数或函数模板的重新声明（redeclarations）或特化（specializations），也应使用该占位符，而不是推导类型。同样，对于不使用占位符类型的已声明返回类型的函数或函数模板的声明或特化，不应使用占位符。

```cpp
Example 6:
auto f();
auto f() { return 42; } // return type is int
auto f(); // OK
error: cannot overloaded with auto
int f(); // error: no matching template
decltype(auto) f(); // error: auto and decltype(auto) don't match

template <typename T> auto g(T t) { return t; } // #1
auto g(int); // OK, return type is int
decltype<auto> double(); // OK
```

占位符类型（placeholder type）的推导通过占位符类型推导 9.9.2.6 推导。
