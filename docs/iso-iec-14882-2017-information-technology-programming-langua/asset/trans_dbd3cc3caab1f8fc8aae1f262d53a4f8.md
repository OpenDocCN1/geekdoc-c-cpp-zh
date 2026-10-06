

# ISO/IEC 14882:2017(E)

```cpp
auto n = n;
auto f();
void g() { &f; }
auto sum(int i) {
if (i == 1)
return i;
else
return sum(i-1)+i;
}
```

```cpp
// error, n's type is unknown
// error, f's return type is unknown
// sum's return type is int
// OK, sum's return type has been deduced

-- end example


11 当函数体包含一个带有非依赖操作数的返回语句时，对于声明类型中包含占位符的模板，其返回类型推导会在定义实例化时发生返回类型推导。注意：因此，模板函数的任何特化都将导致实例化。从该实例化产生的任何错误不在函数类型的直接上下文中，并且可能是格式错误的 (17.7.2) -- end note | [示例]:

```cpp
template <T> auto f(T t) { return t; }
typef decltype(f(int())) int_t;
template<T> auto f(T t) { return t; }
void g() { (*f)(int*) = &f; }
```

```cpp
// 返回类型在实例化时被推导
// 实例化 <int> 以推导返回类型
// 实例化实例化两个 f 以确定返回类型，
// 选择了后一个

-- end example
```

12 声明返回类型使用占位符类型的函数或函数模板的重新声明或特化，也使用该占位符，而不是推导出的类型。[示例]:

```cpp
auto f();
auto f() { 42 };
int f();
decltype(auto f);
template<typename T> auto g(T t) { return t; }
auto g(int);
template char g(char);
template<> auto g(double);
template<class T> T g(T t) { return t; }
char g(char);
tauto g(float);
void h() { return g(42); };
template<typename T> struct A {
friend T frf(T);
auto frf(int i) { return i; };
```

```cpp
// 返回类型为 int
// error, 无法与 auto f()) 重载
// error, auto 和 decltype(auto) 不匹配
// #1
// error, 没有匹配的模板
// error, 未知返回类型的前置声明
// OK, 在功能上与 #1 等效
// OK, 现在有一个匹配的模板
// 匹配 #1
// error, 歧义
// 不是 K<int> 的友元

-- end example
```

13 使用占位符类型作为返回类型声明的函数不应该是虚函数 (13.3)。

14 显式声明 (17.7.2) 不导致使用占位符类型声明的实体的实例化，但也不会防止该实体为了确定其类型而按需要实例化。[示例]:

```cpp
template <typename T> auto f(T t) { return t; }
```

```cpp
extern template auto f(int); // 不实例化 f<int>
// 实例化 f<int> 以确定其返回类型，并且程序的某处
// 需要一个显式实例化定义
int (*p)(int) = f;
```

```cpp
// end example
```

## 10.1.7.4.1 占位符类型推导 [dcl.type.auto.deduct]

- 占位符类型推导是将包含占位符的类型替换为推导类型的过程。

- 包含占位符的类型 T 和对应的初始化器 e 如下所示确定：
    - 对于在包含占位符类型返回类型的函数中发生的声明-返回语句，T 是推导的返回类型，e 是返回语句的操作数。如果返回语句没有操作数，则 e 为 void()。
    - 对于包含占位符类型的变量声明，T 是该变量的推导类型，e 是初始化器。如果初始化是列表初始化，则初始化器应当为仅包含单个表达式的括号初始化列表（braced-init-list），或 e 为赋值表达式；T
    - 对于包含占位符类型的非类型参数声明，T 是该非类型参数的推导类型，e 是对应的参数。
在没有操作数或操作数类型为 T 的返回语句的情况下，T 应当是 decltype(auto) 或 ce auto。

如果推导的是返回语句且是括号初始化列表 (11.6.4)，则程序是格式错误的。

如果占位符是 auto 类型限定符，则替换 T 的推导类型 T 使用类型参数推导规则。从 T 开始，将出现的 auto 替换为带有新初始化器 e 的 std::initializer_list<U> 以获取 P。使用函数调用的模板参数推导规则 (17.8.2.1) 推导值 U，其中 P 是函数参数类型和对应的参数。如果推导失败，则该声明是格式错误的。否则，用推导出的 U 替换 P 中的 T。

```cpp
auto x = { 2 }; // decltype(x) is std::initializer_list<int>
auto x2 = { 1, 0 }; // error: multiple element type
auto x3 = { 3 };
auto x4 = {}; // decltype(x4) is std::initializer_list<int>
auto x5 = { 3 }; // decltype(x5) is int
```

```cpp
// end example
```

示例：

```cpp
const auto i = expr;
template<class U> void f(U u);
```

i 的类型是调用 f(expr) 中参数 u 的推导类型：

```cpp
// end example
```

如果占位符是 decltype(auto) 类型限定符，T 应当是占位符 auto。T 的推导类型如 10.1.7.2 所示，其中 e 是 decltype 的操作数：

```cpp
int& f();
auto x2(i); // decltype(xa) is int
decltype(auto) x2(i); // decltype(x2) is int
auto x3 = i; // decltype(xa3) is int
decltype(auto) x3d = i; // decltype(x3d) is int

```cpp
auto x4 = (i); // decltype(x4) is int
decltype(auto) x4d = i; // decltype(x4d) is int
auto x5 = f(); // decltype(x5a) is int
decltype(auto) x5d = f(); // decltype(x5d) is int&
auto x6 = {1, 2}; // decltype(x6a) is int
decltype(auto) x6d = {1, 2}; // error: is not an expression
auto x7 = i; // decltype(x7) is int
decltype(auto) x7d = i; // error: type is not plain decltype(auto)

-- end example
```

## 10.1.7 推导类类型

- 推导类类型的占位符在变量初始化声明 [11.6] 中的类型限定符被函数的返回类型 [16.3] 替换。

container c(); // OK, 推导 T 为 int
auto d = container(v.begin(), v.end()); // error, int is not an iterator
container e(5, 6);
-- end example

## 10.2 枚举声明

- 枚举带有命名常量的独立类型 [6.9.2]。它的名称在其作用域内变为枚举名。

enum-name:
    identifier

enum-specifier:
    enum-head { enumerator-list-opt }
    enum-head { enumerator-list , }

enum-head:
    enum-key attribute-specifier-seqopt enum-name-opt enum-base-opt

enum-head-name:
    named-name-specifier-seqopt identifier

opaque-enum-declaration:
    enum-key attribute-specifier-seqopt named-name-specifier-seqopt identifier enum-base-opt;

```cpp
enum-key:
  enum
  enum class
  enum struct

enum-base:
  : type-specifier-seq
enumerator-list:
  enumerator-definition
  enumerator-list, enumerator-definition

enumerator-definition:
  enumerator
  enumerator = constant-expression

enumerator:
  identifier attribute-specifier-seq
```

enum-head 和 opaque-enum-declaration 中的可选 attribute-specifier-seq 枚举；该 attribute-specifier-seq 中的属性此后每当命名时都被视为枚举的属性。enumerator-seq 中的 "enum nested-name-specifier identifier" 揭示了带有基类的枚举声明与未命名枚举类型位域声明之间的潜在歧义。[示例]:

```cpp
struct S {
  enum E : int {};
  enum E : int {};
}
```

-- end note | 如果枚举声明包含嵌套名称限定符，则该声明应当是显式特化 (17.7.3)。

enum-key 仅为 enum 的枚举声明及其枚举是非作用域的枚举。enum-keys class 和 enum struct 在语义上等价；使用其中之一的枚举声明是作用域枚举，其枚举是作用域枚举。对于整数类型，enum-base 的标识不可省略；任何 cv 校验均被忽略。如果枚举声明有 enum-base，则 enumerator-list 中的枚举成员声明为常量，并出现在任何需要常量的地方。enumerator-definition 的关联枚举值由 constant-expression 指出。如果第一个 enumerator-definition 有初始化器，则对应常量的值为零。没有初始化器的 enumerator-definition 将前一个枚举成员的值加一。[示例]:

```cpp
enum a { b, c=2 };
enum d { e, f=2 };
```

定义 a 和 d 为零，b 为一，f 为三。 -- end example | 枚举中的可选 attribute-specifier-seq 属于该枚举成员。

枚举声明是在当前作用域内对枚举的声明或新枚举的声明。注意：带有 enum-base-declaration 的枚举声明固定了底层类型，是一个完全类型。枚举列表可以在后续带有 enum-specifier 的声明提供。 -- end note | 作用域枚举不应再重新声明为非作用域或不同类型。非作用域枚举不应再重新声明为作用域，且每次重新声明应包含与原始声明类型相同的 enum-base。

4 如果 enum-key 后面跟着嵌套名称限定符，则 enum-specifier 应当引用一个枚举

