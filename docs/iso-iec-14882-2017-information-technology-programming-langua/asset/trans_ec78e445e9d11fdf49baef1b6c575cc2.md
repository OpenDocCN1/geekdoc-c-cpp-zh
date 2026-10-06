

# ISO/IEC 14882:2017(E)

表 41 — 复合类型分类谓词（续）

| 模板 | 条件 | 注释 |
| --- | --- | --- |
| template <class T> struct_fundamental; | T 是基础类型 (6.9.1) | |
| template <class T> struct_object; | T 是对象类型 (6.9) | |
| template <class T> struct_scalar; | T 是标量类型 (6.9) | |
| template <class T> struct_compound; | T 是复合类型 (6.9.2) | |
| template <class T> struct_member_pointer; | T 是指向非静态数据成员或非静态成员的指针 | [meta.unary.prop ] |

## 23.15.4 类型属性

- 1 这里的模板提供了对库中某些部分的访问，而无需定义这些模板的任何完全或部分特化版本。

- 2 不确定对于在本小节中声明的，使用类模板特化类作为模板参数实例化模板，是否会导致模板的隐式实例化，如果仅有 X 的语义要求该参数为完整类型。

- 3 为了定义本小节中的模板，对于任何类型 T，函数表达式 `declcl<T>()` 都被视为一个平凡的 (6.9.5) 函数，尽管有 23.2.7 的限制，在相应的定义的上下文中不视为对 `declcl` 的使用 (6.9.2)。

表 42 — 类型属性谓词

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T> struct_const; | T 被 const 修饰 (6.9.3) | |
| template <class T> struct_volatile; | T 被 volatile 修饰 (6.9.3) | remove_all_extents_<T> 应当是一个完整类型或 cv void |
| template <class T> struct_trivial; | T 是平凡类型 (6.9) | remove_all_extents_<T> 应当是一个完整类型或 cv void |
| template <class T> struct_trivially_copyable; | T 是平凡可拷贝类型 (6.9) | remove_all_extents_<T> 应当是一个完整类型或 cv void |
| template <class T> struct_is_layout; | T 是标准布局类型 (6.9) | remove_all_extents_<T> 应当是一个完整类型或 cv void |
| template <class T> struct_pod; | T 是 POD 类型 (6.9) | remove_all_extents_<T> 应当是一个完整类型或 cv void |

表 42 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
|---|---|---|---|
| `<class T> struct is_empty` | T 是类类型但不是联合类型，具有除长度为 0 的位域以外的非静态数据成员、没有成员函数、没有虚基类，且对于 `is_empty_vB` 的基类 B 为假。 | 如果 T 是非联合的类类型，T 应当是一个完整类型。 |
| `<class T> struct is_polymorphic` | T 是多态类（类 13.3） | 如果 T 是非联合的类类型，T 应当是一个完整类型。 |
| `<class T> struct is_abstract` | T 是抽象类（类 13.4） | 如果 T 是非联合的类类型，T 应当是一个完整类型。 |
| `<class T> struct is_final` | T 是标记有 `class-virt-specifier` final 的类类型（第 12 条）。[注：联合是一种可以标记为 final 的类类型。—注结束] | 如果 T 是类类型，T 应当是一个完整类型。 |
| `<class T> struct is_aggregate` | T 是聚合类型 (11.6.1) | `remove_all_extents_<T>` 应当是一个完整类型或 void。 |
| `<class T> struct is_signed` | 如果 `is_arithmetic_v<T>` 为真，结果同于 `T(-1) < T(0)`；假 | |
| `<class T> struct is_unsigned` | 如果 `is_arithmetic_v<T>` 为真，结果同于 `T(0) < T(-1)`；假 | |
| `<class T, class... Args> struct is_constructible` | 对于函数 T 或对于 const 类型 T，`is_constructible_v<T, Args...>` 为真；否则参见[下文] | T 和参数包 Args 中的所有类型应当是完整类型、`void` 或未知边界的数组。 |
| `<class T> struct is_default_constructible` | 如果 `is_constructible_v<T>` 为真。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |
| `<class T> struct is_copy_constructible` | 对于 (20.3.18) 中的引用类型 T，结果同于 `is_constructible_v<const T&>`；否则为假。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |

表 42 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T> struct is_move_constructible; | 对于可引用类型 T，结果同于 `is_constructible_v<T>&>`；否则为假。 | T 应当是一个完整类型、void，或未知边界的数组。 |
| template <class T, class U> struct is_assignable; | `decltype() = decltype(v)` 被良好地视为非求值的操作数（第 5 条）。访问检查是如同在一个与 T 和 U 无关的上下文中执行的。仅考虑赋值表达式的直接上下文的有效性。[注：表达式的完成可能会导致副作用，例如模板特化和函数模板特化的实例化、隐式定义函数的生成等。此类副作用不在“直接上下文”中，并可能导致程序格式不正确。—注] | T 和 U 应当是完整类型、`void` 或未知边界的数组。 |
| template <class T> struct is_copy_assignable; | 对于可引用类型 T，结果同于 `is_assignable_v<T>&`；否则为假。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |
| template <class T> struct is_move_assignable; | 对于可引用类型 T，结果同于 `is_assignable_v<T>&`；否则为假。 | T 应当是一个完整类型、void 或未知边界的数组。 |
| template <class T> struct is_assignable; | 对于可引用类型 T，结果同于 `is_assignable_v<T>`；否则为假。 | T 应当是一个完整类型、void 或未知边界的数组。 |
| template <class T, class U> struct is_swappable_with; | `declval<T>()` 和 `declval<U>()` 各被良好地视为非求值的操作数（第 8 条），如同在一个与 T 和 U 无关的上下文中执行（上下文 23.2.7）。仅考虑赋值表达式的直接上下文的有效性。 | T 和 U 应当是完整类型、void 或未知边界的数组。 | |
| template <class T> struct is_swappable; | 对于可引用类型 T，结果同于 `is_swappable_v<T>`；否则为假。 | T 应当是一个完整类型、void 或未知边界的数组。 |
| template <class T> struct is_destructible; | 或者 T 是引用类型，或者 T 是一个对于 `declval<T>().operator()` 是良好的完整对象。 | remove_all_extents_<T>。 |

表 42 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
|---|---|---|
| template <class T, class... Args> struct_trivially_constructible; | 按照 `is_constructible` 的定义相同，且已知不调用非平凡的操作 (6.9,15)。 | `is_constructible_v<T, Args...>` 为真。 |
| template <class T> struct is_trivially_default_constructible; | `is_constructible_v<T>` 为真。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |
| template <class T> struct is_trivially_move_constructible; | 对于可引用类型 T，结果同于 `is_constructible_v<T,>&>`；否则为假。 | T 应当是一个完整类型、void 或未知边界的数组。 |
| template <class T> struct is_trivially_copy_constructible; | 对于 (20.3.18) 中的引用类型 T，结果同于 `is_constructible_v<const T&>`；否则为假。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |
| template <class T> struct is_trivially_copy_assignable; | 对于可引用类型 T，结果同于 `is_assignable_v<T>&`；否则为假。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |
| template <class T> struct is_trivially_move_assignable; | 对于可引用类型 T，结果同于 `is_assignable_v<T>&`；否则为假。 | T 应当是一个完整类型、`void` 或未知边界的数组。 |

