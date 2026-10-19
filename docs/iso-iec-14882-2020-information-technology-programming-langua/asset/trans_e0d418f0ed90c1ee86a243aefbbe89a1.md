

(1.2) — 如果函数参数被描述为数组，则实际传递给函数的指针的值应使得所有地址计算和对象访问（如果指针确实指向此类数组的第一个元素则为有效）实际上都是有效的。

(1.3) — 如果函数参数绑定到右值引用参数，实现可以假定该参数是对此参数的唯一引用。

> [*Note 1:* 如果参数是形式为 `T&&` 的通用参数并且绑定了类型为 `A` 的右值，则参数绑定到左值引用（[13.10.3.2]），因此不属于前一句所述范围。 — *end note*]

> [*Note 2:* 如果程序在将左值传递给库函数时将左值转换为 xvalue（例如，通过调用函数并使用参数 `std::move(x)`），程序实际上是在要求该函数将该左值视为临时对象。实现可以自由地优化掉如果参数为左值则可能需要的别名检查。 — *end note*]

## 16.4.5.10 库对象访问

如果来自不同线程的标准库函数的调用可能引入数据竞争，则程序的行为是未定义的。可能发生这种情况的条件在 16.4.6.10 中指定。

> [*Note 1:* 修改在线程间共享的标准库类型对象，除非该类型的对象被明确指定为可在无数据竞争的情况下共享，或用户提供锁定机制，否则会带来未定义行为的风险。 — *end note*]

如果访问标准库类型的对象，并且对象的生命周期开始（6.7.3）未发生在访问之前，或访问未发生在对象生命周期结束之前，则行为是未定义的，除非另有规定。

> [*Note 2:* 这甚至适用于诸如互斥量等旨在用于线程同步的对象。 — *end note*]

## 16.4.5.11 语义要求

如果模板参数序列 Args *满足* 概念 C，则称其 *建模* 概念 C，如果 Args 满足 C（13.5.3）并且满足 C 的规范中给出的所有语义要求（如果有）。

如果程序的有效性或含义取决于模板参数序列是否建模概念，并且概念得到满足但未被建模，则程序格式错误，无需诊断。

如果在使用的点上未建模声明的约束的语义要求（16.3.2.3），则程序格式错误，无需诊断。

## 16.4.6 遵从的实现

### 16.4.6.1 概述

子条款 16.4.6 描述了 C++ 标准库实现上的约束和自由度。

实现对头文件的用法在 16.4.6.2 中讨论，其对宏的用法在 16.4.6.3 中，非成员函数在 16.4.6.4 中，成员函数在 16.4.6.5 中，避免数据竞争在 16.4.6.10 中，访问说明符在 16.4.6.11 中，类派生在 16.4.6.12 中，异常在 16.4.6.13 中。

### 16.4.6.2 头文件

C++ 头文件可以包含其他 C++ 头文件。C++ 头文件应提供其概要中出现的声明和定义。概要中显示为包含其他 C++ 头文件的 C++ 头文件应提供这些其他头文件概要中出现的声明和定义。

某些类型和宏在多个头文件中定义。每个此类实体都应定义为，任何定义它的头文件都可以在定义它的任何其他头文件之后包含（6.3）。

C 标准库头文件（D.10）应仅包含其对应的 C++ 标准库头文件，如 16.4.2.3 中所述。

### 16.4.6.3 对宏定义的限制

16.4.2.2 中描述的名称和全局函数签名由实现保留。

C 标准库定义的所有对象类宏并在本文中描述为扩展为整型常量表达式，也适用于 `#if` 预处理指令中，除非另有明确说明。

### 16.4.6.4 非成员函数 [global.functions]

1 是否将 C++ 标准库中的任何非成员函数定义为内联（9.2.8）是不确定的。

2 对第 17 条款至第 32 条款和附录 D 中描述的非成员函数签名的调用应表现得好像实现未声明任何额外的非成员函数签名。182

3 实现不得声明具有额外默认参数的非成员函数签名。

4 除非另有规定，标准库中的函数对非运算符、非成员函数的调用不使用通过参数相关名称查找（6.5.3）找到的来自另一个命名空间的函数。

> [Note 1: 措辞“除非另有规定”适用于诸如可交换的要求（16.4.4.3）之类的情况。重载运算符的例外允许在 ostream_::operator=（23.6.3.3）之类的情况下进行参数相关查找：
> 效果：
> *out_stream << value;
> if (delim != 0)
>   *out_stream << delim;
> return *this;
> — end note]

```
*out_stream << value;
if (delim != 0)
  *out_stream << delim;
return *this;
```

### 16.4.6.5 成员函数 [member.functions]

1 是否将 C++ 标准库中的任何成员函数定义为内联（9.2.8）是不确定的。

2 对于 C++ 标准库中描述的非虚成员函数，实现可以声明不同的成员函数签名集合，前提是任何对成员函数的调用如果从本文档中描述的声明集合中选择重载，则表现得好像选择了该重载。

> [Note 1: 例如，实现可以添加具有默认值的参数，或用两个或多个具有等效行为的成员函数替换具有默认参数的成员函数，或为成员函数名添加额外的签名。 — end note]

### 16.4.6.6 友元函数 [hidden.friends]

1 每当本文档在类或类模板定义内指定一个函数或函数模板的友元声明时，该声明应是实现提供的该函数或函数模板的唯一声明。

> [Note 1: 特别是，实现不允许在命名空间范围内提供该函数或函数模板的额外声明。 — *end note*]

> [Note 2: 这种友元函数或函数模板声明被称为隐藏友元，因为它既不可见于普通的非限定查找（6.5.2），也不可见于限定查找（6.5.4）。 — *end note*]

### 16.4.6.7 constexpr 函数和构造函数 [constexpr.functions]

1 本文明确要求某些标准库函数为 constexpr（9.2.6）。实现不得将任何标准库函数签名声明为 constexpr，除非明确要求。任何提供 constexpr 函数或构造函数非定义声明的头文件中，实现应提供相应的定义。

### 16.4.6.8 稳定算法的要求 [algorithm.stable]

1 当算法的要求说明其为“稳定”且未进一步阐述时，其含义为：

- (1.1) — 对于排序算法，等价元素的相对顺序得以保留。
- (1.2) — 对于移除和复制算法，未被移除元素的相对顺序得以保留。
- (1.3) — 对于合并算法，对于原始两个范围中的等价元素，来自第一个范围的元素（保留其原始顺序）在来自第二个范围的元素（保留其原始顺序）之前。

### 16.4.6.9 可重入性 [reentrancy]

1 除非本文档中明确指定，否则 C++ 标准库中哪些函数可以递归重入是实现定义的。

## 17 语言支持库 [support]

### 17.1 通用 [support.general]

1 本条款描述了在某些 C++ 程序执行期间隐式调用的函数签名，以及隐式生成的对象类型。它还描述了声明这些函数签名并定义任何相关类型的头文件。

2 以下子条款描述了库中通用的类型定义、预定义类型的特性、支持 C++ 程序启动和终止的函数、动态内存管理支持、动态类型识别支持、异常处理支持、初始化列表支持和其他运行时支持，如表 37 所总结。

表 37：语言支持库摘要 [tab:support.summary]

|  | 子条款 | 头文件 |
|---|---|---|
| 17.2 | 常用定义 | <cstddef>, <cstdlib> |
| 17.3 | 实现属性 | <cfloat>, <climits>, <limits>, <version> |
| 17.4 | 整数类型 | <cstdint> |
| 17.5 | 启动和终止 | <cstdlib> |
| 17.6 | 动态内存管理 | <new> |
| 17.7 | 类型识别 | <typeinfo> |
| 17.8 | 源位置 | <source_location> |
| 17.9 | 异常处理 | <exception> |
| 17.10 | 初始化列表 | <initializer_list> |
| 17.11 | 比较 | <compare> |
| 17.12 | 协程 | <coroutine> |
| 17.13 | 其他运行时支持 | <csetjmp>, <csignal>, <cstdarg>, <cstdlib> |

### 17.2 常用定义 [support.types]

#### 17.2.1 头文件 <cstddef> 概要 [cstddef.syn]

```
namespace std {
    using ptrdiff_t = see below;
    using size_t = see below;
    using max_align_t = see below;
    using nullptr_t = decltype(nullptr);

    enum class byte : unsigned char {};

    // 17.2.5, byte type operations
    template<class IntType>
        constexpr byte& operator<<=(byte& b, IntType shift) noexcept;
    template<class IntType>
        constexpr byte operator<<(byte b, IntType shift) noexcept;
    template<class IntType>
        constexpr byte& operator>>=(byte& b, IntType shift) noexcept;
    template<class IntType>
        constexpr byte operator>>(byte b, IntType shift) noexcept;
    constexpr byte& operator|=(byte& l, byte r) noexcept;
    constexpr byte operator|(byte l, byte r) noexcept;
    constexpr byte& operator&=(byte& l, byte r) noexcept;
    constexpr byte operator&(byte l, byte r) noexcept;
    constexpr byte& operator^=(byte& l, byte r) noexcept;
    constexpr byte operator^(byte l, byte r) noexcept;
    constexpr byte operator~(byte b) noexcept;
```

