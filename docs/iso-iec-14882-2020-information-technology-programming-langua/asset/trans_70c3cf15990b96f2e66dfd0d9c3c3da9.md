

表 14：*simple-type-specifiers* 和它们指定的类型  [tab:dcl.type.simple]

| Specifier(s) | Type |
|---|---|
| *type-name* | 所命名的类型 |
| *simple-template-id* | 13.3 中定义的类型 |
| *decltype-specifier* | 9.2.9.5 中定义的类型 |
| *placeholder-type-specifier* | 9.2.9.6 中定义的类型 |
| *template-name* | 9.2.9.7 中定义的类型 |
| `char` | "char" |
| `unsigned char` | "unsigned char" |
| `signed char` | "signed char" |
| `char8_t` | "char8_t" |
| `char16_t` | "char16_t" |
| `char32_t` | "char32_t" |
| `bool` | "bool" |
| `unsigned` | "unsigned int" |
| `unsigned int` | "unsigned int" |
| `signed` | "int" |
| `signed int` | "int" |
| `int` | "int" |
| `unsigned short int` | "unsigned short int" |
| `unsigned short` | "unsigned short int" |
| `unsigned long int` | "unsigned long int" |
| `unsigned long` | "unsigned long int" |
| `unsigned long long int` | "unsigned long long int" |
| `unsigned long long` | "unsigned long long int" |
| `signed long int` | "long int" |
| `signed long` | "long int" |
| `signed long long int` | "long long int" |
| `signed long long` | "long long int" |
| `long long int` | "long long int" |
| `long long` | "long long int" |
| `long int` | "long int" |
| `long` | "long int" |
| `signed short int` | "short int" |
| `signed short` | "short int" |
| `short int` | "short int" |
| `short` | "short int" |
| `wchar_t` | "wchar_t" |
| `float` | "float" |
| `double` | "double" |
| `long double` | "long double" |
| `void` | "void" |

除非它是显式特化（13.9.4）、显式实例化（13.9.3）或具有以下形式之一，否则格式错误：

```
class-key attribute-specifier-seq_opt identifier ;
friend class-key ::_opt identifier ;
friend class-key ::_opt simple-template-id ;
friend class-key nested-name-specifier identifier ;
friend class-key nested-name-specifier template_opt simple-template-id ;
```

在第一种情况下，如果有 *attribute-specifier-seq*，则它属于正在声明的类；*attribute-specifier-seq* 中的属性此后只要该类被命名就被视为该类的属性。

2 [注 1：6.5.5 描述了在 *elaborated-type-specifier* 中对 *identifier* 进行名称查找的进程。——注结束]

如果 *identifier* 或 *simple-template-id* 解析为 *class-name* 或 *enum-name*，则 *elaborated-type-specifier* 以与 *simple-type-specifier* 引入其 *type-name* 的方式相同的方式将其引入声明（9.2.9.3）。如果

为临时对象分配存储或强制执行与调用该类型析构函数相关的语义约束。——注结束]

[注 3：与前述规则不同，圆括号在此上下文中没有特殊含义。——注结束]

[示例 2：

```
template<class T> struct A { ~A() = delete; };
template<class T> auto h()
  -> A<T>;
template<class T> auto i(T)    // identity
  -> T;
template<class T> auto f(T)    // #1
  -> decltype(i(h<T>()));       // 强制完成 A<T> 并隐式使用 A<T>::~A()
                              // 用于 h() 使用引入的临时对象。
                              // （使用 i 不会引入临时对象。）
template<class T> auto f(T)    // #2
  -> void;
auto g() -> void {
  f(42);                        // OK：调用 #2。(#1 不是可行的候选：类型推导
                              // 失败（13.10.3），因为 A<int>::~A() 在其
                              // decltype-specifier 中被隐式使用)
}
template<class T> auto q(T)
  -> decltype((h<T>()));       // 不强制完成 A<T>；A<T>::~A() 未在
                              // 此 decltype-specifier 的上下文中隐式使用
void r() {
  q(42);                        // 错误：对 q 的推导成功，因此重载解析选择
                              // 特化 “q(T) -> decltype((h<T>()))” 且 T=int；
                              // 返回类型为 A<int>，因此引入临时对象并使用其析构函数，因此程序格式错误
}
— end example]
```

## 9.2.9.6 Placeholder type specifiers [dcl.spec.auto]

### 9.2.9.6.1 General [dcl.spec.auto.general]

```
placeholder-type-specifier:
  type-constraint_opt auto
  type-constraint_opt decltype ( auto )
```

1 placeholder-type-specifier 指定一个占位符类型，该类型将在稍后由初始化器推导替换。

2 形式为 type-constraint_opt auto 的 placeholder-type-specifier 可用作函数声明或 lambda 表达式的参数声明的 decl-specifier-seq 的 decl-specifier，并且如果它不是引入尾随返回类型的 auto type-specifier（见下文），则是函数声明或 lambda 表达式的通用参数类型占位符。

[注 1：具有通用参数类型占位符表示该函数是简写函数模板（9.3.4.6）或 lambda 是通用 lambda（7.5.5）。——注结束]

3 占位符类型可以与函数声明符一起出现在 decl-specifier-seq、type-specifier-seq、conversion-function-id 或 trailing-return-type 中，只要此类声明符有效即可。如果函数声明符包含尾随返回类型（9.3.4.6），则该尾随返回类型指定函数的声明返回类型。否则，函数声明符应声明一个函数。如果函数的声明返回类型包含占位符类型，则函数的返回类型从函数体中非丢弃的返回语句（如果有）推导（8.5.2）。

4 使用占位符类型声明的变量的类型从其初始化器推导。此用法允许在变量的初始化声明（9.4）中使用。占位符类型应作为 decl-specifier-seq 中的 decl-specifier 之一出现，并且 decl-specifier-seq 应跟随一个或多个声明符，每个声明符都应跟随一个非空的初始化器。在形式为
( expression-list )
的初始化器中，expression-list 应为单个 assignment-expression。

[示例 1：

```
auto x = 5; // OK: x has type int
const auto *v = &x, u = 6; // OK: v has type const int*, u has type const int
static auto y = 0.0; // OK: y has type double
auto int r; // error: auto is not a storage-class-specifier
auto f() -> int; // OK: f returns int
auto g() { return 0.0; } // OK: g returns double
auto h(); // OK: h’s return type will be deduced when it is defined
— end example]
```

auto type-specifier 也可用于引入结构化绑定声明（9.6）。

5 占位符类型还可以在 new-expression（7.6.2.8）的 new-type-id 或 type-id 的 type-specifier-seq 中使用，并作为模板参数（13.2）的 parameter-declaration 的 decl-specifier-seq 的 decl-specifier。

6 在 9.2.9.6 中未明确允许的上下文中使用占位符类型的程序是格式错误的。

7 如果 init-declarator-list 包含多个 init-declarator，它们都应形成变量的声明。每个声明变量的类型由占位符类型推导（9.2.9.6.2）确定，如果替换占位符类型的类型在每次推导中不相同，则程序是格式错误的。

[示例 2：

```
auto x = 5, *y = &x; // OK: auto is int
auto a = 5, b = { 1, 2 }; // error: different types for auto
— end example]
```

8 如果具有包含占位符类型的声明返回类型的函数有多个非丢弃返回语句，则返回类型针对每个此类返回语句进行推导。如果推导出的类型在每次推导中不相同，则程序是格式错误的。

9 如果具有使用占位符类型的声明返回类型的函数没有非丢弃返回语句，则返回类型推导为好像在函数体闭合大括号处有一个没有操作数的 return 语句。

[示例 3：

```
auto f() {} // OK, return type is void
auto* g() {} // error: cannot deduce auto* from void()
— end example]
```

10 具有使用占位符类型的声明返回类型的导出函数应在其导出声明所在的翻译单元中定义，在 private-module-fragment（如果有）之外。

[注 2：推导出的返回类型不能具有内部链接的名称（6.6）。——注结束]

11 如果实体名称具有未推导的占位符类型出现在表达式中，则程序是格式错误的。然而，一旦在函数中看到非丢弃返回语句，从该语句推导出的返回类型就可以在函数其余部分中使用，包括在其他返回语句中使用。

[示例 4：

```
auto n = n; // error: n’s initializer refers to n
auto f();
void g() { &f; } // error: f’s return type is unknown
auto sum(int i) {
if (i == 1)
return i; // sum’s return type is int
else
return sum(i-1)+i; // OK, sum’s return type has been deduced
}
— end example]
```

12 具有占位符类型的模板化实体，即函数或函数模板的声明类型的返回类型推导在定义实例化时发生，即使函数体包含具有非类型相关操作数的 return 语句也是如此。

[注 3：因此，函数模板的特化的任何使用都会导致隐式实例化。此实例化产生的任何错误都不在函数类型的直接上下文中，并且可能导致程序格式错误（13.10.3）。——注结束]

