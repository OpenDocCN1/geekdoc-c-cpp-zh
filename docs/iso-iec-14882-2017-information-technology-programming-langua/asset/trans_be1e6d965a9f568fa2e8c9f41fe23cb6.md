
# ISO/IEC 14882:2017(E)

表 50 — 其他变换（续）

| Template <class T> | Comments |
|--- |--- |
| struct underlying_type; | T 的成员类型定义**名称**。*要求：* T 应当是一个完全枚举类型 (10.2) |
| template <class Fn, class... ArgTypes> | 如果表达式 `INVOKE(declFn())`、`decltype(ArgTypes<...>)` 在被视为未展开的特化时（第 8 条）是良，则类型 `decltype(INVOKE(declFn()), decltype(ArgTypes<...>))` ` 的成员类型定义**名称**；否则，不定义任何类型。访问方式类似于在 Fn 和 ArgTypes 的上下文中进行。只有表达式的立即上下文的有效性可能会导致副作用，例如模板特化的实例化和函数模板特化的实例化。*注：* 这些副作用不在“立即上下文”中，并可能导致程序格式错误（ill-formed）。—— 备注结束 *要求：* Fn 和参数包 ArgTypes 中的所有类型均应当是完全类型、const void 或未知边界的数组。|

+ 1 [注：实现会定义 **aligned_storage**：
```cpp
template <size_t Len, size_t Alignment>
struct aligned_storage {
    typedef struct {
        alignas(Alignment) unsigned char __data[Len];
    } type;
};
```] —— 备注结束
2 是否支持任何扩展对齐由实现定义 (6.11)。
3 注：对于被视为类型参数包 T 的 **common_type**，成员类型应如下被定义或不定义：
(3.1) 如果 `size...(T)` 为零，则不定义成员类型。
(3.2) 如果 `size...(T)` 为一，令 D0 表示相同的类型，类型定义名称应表示与 `common_type<T0>` 相同的类型；否则，不定义成员类型。
(3.3) 如果 `size...(T)` 为二，令第一个和第二个类型分别表示为 T1 和 T2，令 D1 和 D2 分别表示 *decay_type<T1>* 和 *decay_type<T2>* 相同的类型。
(3.3.1) 如果 *is_same<V1, D1>* 为假或 *is_same<V2, D2>* 为假，令 C 表示如果作为共同类型，与 `common_type<D1, D2>` 相同的类型。
(3.3.2) 否则，令 C 表示（如果有）与 `decay_type(false ? decltype<D1>() : decltype<D2>())` 相同的类型。[注：如果存在 **common_type<D1, D2>** 的特化，则此不适用。—— 备注结束]
在这种情况下，成员类型定义名称应表示与 C 相同的类型。否则，不定义成员类型。
(3.4) 如果 `size...(T)` 大于二，令 T1、T2 和 R 分别表示第一个、第二个以及（构成 T 的剩余类型包）。令 C 表示如果作为 `common_type_t<T1, T2>`，则相同的类型。如果存在这样的类型 C，则成员类型定义名称类型应表示与 `common_type_t<C, R..>` 相同的类型。否则，不定义成员类型。

+ 注 B：在遵守 23.15.2 规定的情况下并根据 20.5.4.2.1，程序可以为类型 T1 和 T2 特化 common_type_t<T1, T2>使得 `is_same_v<T1, decay_t<T2>>` 为真。[注：当在模板参数之间需要显式转换时，需要此类特化。—— 备注结束] 这种特化可能不需要命名的成员，但如果有，该成员应为明确且未限定类型的类型定义名称，每个类型 T1 和 T2 都显式定义为该类型。此外，common_type_t<T1> 应表示与 `common_type_t<T2, T1>` 相同的类型（如果有）。违反此规则不需要诊断信息。

+ 示例：使用这些定义：

```
using PF1 = bool (&);
using PF2 = short (*)(long);

struct S {
    operator PF2() const;
    double operator()(int, int);
    void fn(const S);
    char* data;
};

using PMF = void (S::*)(long const);
using PMD = char (*)(S);
```

以下断言将：

```
static_assert(is_same_v<invoke_result_t<S, int, short>>, double, "error1");
static_assert(is_same_v<invoke_result_t<S, unsigned char, int&>>, double, "error2");
static_assert(is_same_v<invoke_result_t<S, bool>>, bool, "error3");
static_assert(is_same_v<invoke_result_t<TMF, unique_ptr<int>, void>>, void, "error4");
static_assert(is_same_v<invoke_result_t<PMD, S>>, char&, "error5");
```
—— 示例结束```

## 23.15.8 逻辑运算符特性 [meta.logical]

+ 此子类定义了将逻辑运算符应用于其他类型特性的特性。

```cpp
template<class... B> struct conjunction : 见下文 { };
```

+ conjunction 类构成了其模板参数的逻辑与。

+ 对于特化 conjunction<B1, ..., Bn>，如果存在类型参数 B1 使得 `bool(B1::value)` 为假，则不需要实例化 B1；注：这类似于 bool 运算符 && 的短路行为。—— 备注结束]

+ 每个模板类型参数 B1::value 的实例化应作为基类使用并可转换为 bool，不隐藏，且在类型中是明确的。

+ 特化 conjunction<B1, ..., Bn> 具有公共且明确的基类，该基类是：
- 列表中第一个使得 `bool(BI::value)` 为假的 B1 对应的 true_type；
- 如果不存在这样的 Bi，则是列表中的最后一个类型。

> [注：这意味着 conjunction 的特化并不一定继承自 true_type 或 false_type。—— 备注结束]

6 除了 conjunction 和 operator= 之外的类成员名称不应隐藏，且在 conjunction 中应该是明确的。

```cpp
template<class... B> struct distinction : 见下文 {};
```

7 disjunction 模板构成了其模板类型参数的逻辑或。

8 对于特化 disjunction<B1, ..., BN>，如果存在模板参数 B1 使得 `bool(B::value)` 为真；... 则不需要实例化 B1::value 对于 j = 1。[注：这允许内置运算符的短路行为。—— 备注结束]

9 每个类型参数 B1::value 的实例化应作为基类使用并共享一个可转换为 bool 的成员值，不隐藏，且在类型中是明确的。

10 特化 disjunction<B1, ..., BN> 具有公共且明确的基类，该基类是：
- (10.1) 列表中第一个使得 `bool(BI::value)` 为真的 BI 对应的 true_type；
- (10.2) 如果不存在这样的 Bi，则是列表中的最后一个类型。

> [注：这意味着 disjunction 的特化并不一定继承自 true_type 或 false_type。—— 备注结束]

11 除了 conjunction 和 operator= 之外的类成员名称不应隐藏，且在 conjunction 中应该是明确的。

```cpp
template<class... B> struct distinction : 见下文 {};
```
