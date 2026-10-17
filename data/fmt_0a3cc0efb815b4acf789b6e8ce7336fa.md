
1. 模板 `integral_constant` 及其相关的类型定义 `true_type` 和 `false_type` 被用作基类，用于定义各种类型特性的接口。

# 20.10.4 一元类型特性

1. 此子句包含了可能用于编译时查询类型属性的模板。
2. 如果相应的条件为真，则这些模板中的每一个都应该是 `UnaryTrait(20.10.1)`，其 `BaseCharacteristic` 为 `true_type`；否则为 `false_type`。

# 20.10.4.1 主要类型分类

1. 主要类型分类对应于 C++ 标准第 3.9 节中的描述。
2. 对于任何给定的 `T`，将这些模板之一应用于 `T` 和经过 `const` 修饰的 `T` 应产生相同的结果。
3. 对于任何给定的类型 `T`，主要类型中恰好有一个类型的成员变量求值为为 `true`。尾注

| 模板 | 条件 | 注释 |
| --- | --- | --- |
| template <T> struct is_void; | T 是 void | |
| template <T> struct is_null_pointer; | T 是 std::nullptr_t (3.9.1) | |
| template <T> struct is_integral; | T 是整数类型 (3.9.1) | |
| template <T> struct is_floating_point; | T 是浮点类型 (3.9.1) | |
| template <T> struct is_array; | T 是已知或未知的范围的数组 (3.9.2) | 类模板数组 (23.3.2) 不是数组类型 |
| template <T> struct is_pointer; | T 是指针类型 (3.9.2) | 包括指向非静态成员的指针 |
| template <T> struct is_lvalue_reference; | T 是左值引用 (8.3.2) | |
| template <T> struct is_rvalue_reference; | T 是右值引用 (8.3.2) | |
| template <T> struct is_member_object_pointer; | T 是指向非静态数据成员的指针 | |
| template <T> struct is_member_function_pointer; | T 是指向非静态函数的指针 | |
| template <T> struct is_enum; | T 是枚举类型 (3.9.2) | |
| template <T> struct is_union; | T 是联合类型 (3.9.2) | |

# 表 47 — 主要分类（续）

| 模板 | 条件 | 注释 |
| --- | --- | --- |
| template <T> struct is_class; | T 是类类型但不是联合类型 (3.9.2) | |
| template <T> struct is_function; | T 是函数类型 (3.9.2) | |

# 20.10.4.2 复合类型特性 [meta.unary.comp]

1. 这些模板根据第 3.9 节中的描述，提供了主要类型的方便组合。
2. 对于任何给定的 `T`，将这些模板之一应用于 `T` 应产生相同的结果。

# 表 48 — 复合类型谓词

| 模板 | 条件 | 注释 |
| --- | --- | --- |
| template <class T> struct is_reference; | T 是内联引用或值引用 | |
| template <class T> struct is_arithmetic; | T 是算术类型 (3.9.1) | |
| template <class T> struct is_fundamental; | T 是基础类型 (3.9.1) | |
| template <class T> struct is_object; | T 是对象类型 (3.9) | |
| template <class T> struct is_scalar; | T 是标量类型 (3.9) | |
| template <class T> struct is_compound; | T 是复合类型 (3.9.2) | |
| template <class T> struct is_pointer; | T 是指向非静态数据成员或非静态函数的指针 | |

# 20.10.4.3 类型属性 [meta.unary.prop]

1. 这些模板提供了类型的一些更重要的属性。
2. 未未定义这些模板的任何完全或部分特化。
3. 对于本节中声明的所有类模板，用类参数实例化该模板，如果语义要求必须是完整类型，可能会导致该模板的隐式实例化。

# 表 49 — 类型属性谓词

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T> struct is_const; | T 是 const 修饰的 (3.9.3) | |
| template <class T> struct is_volatile; | T 是 volatile 修饰的 (3.9.3) | |

# 表 49 — 类型属性谓词（前提条件）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <T> struct is_trivial; | T 是平凡类型 (3.9) | `remove_all_extents<T>` 应当是完整类型或（可能是 cv 修饰的）void。 |
| template <T> struct is_trivially_copyable; | T 是可拷贝类型 (3.9) | `remove_all_extents<T>` 应当是完整类型或（可能是 cv 修饰的）void。 |
| template <T> struct is_standard_layout; | T 是标准布局类型 (3.9) | `remove_all_extents<T>` 应当是完整类型或（可能是 cv 修饰的）void。 |
| template <T> struct is_pod; | T 是 POD 类型 (3.9) | `remove_all_extents<T>` 应当是完整类型或（可能是 cv 修饰的）void。 |
| template <T> struct is_literal_type; | T 是字面量类型 (3.9) | `remove_all_extents<T>` 应当是完整类型或（可能是 cv 修饰的）void。 |
| template <T> struct is_empty; | T 是类类型但不是联合类型，没有长度为 0 的位域数据成员，没有虚成员函数，且没有值为 false 的基类 B | 如果 T 是非联合类类型，T 应当是完整类型。 |
| template <T> struct is_polymorphic; | T 是多态类 (10.3) | 如果 T 是非联合类类型，T 应当是完整类型。 |
| template <T> struct is_abstract; | T 是抽象类 (10.4) | 如果 T 是非联合类类型，T 应当是完整类型。 |
| template <T> struct is_final; | T 是标记为 final 类的类类型（第 9 节）。注意：联合类型是可以标记为 final 的类类型。—尾注 | 如果 T 是类类型，T 应当是完整类型。 |

# 表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T> struct is_signed; | 如果 `is_arithmetic<T>::value` 为真，则结果与 `integral_constant<bool, T(-1) < T(0)::value` 相同；否则为假 | |
| template <class T> struct is_unsigned; | 如果 `is_arithmetic<T>::value` 为真，则结果与 `integral_constant<bool, T(0) < T(-1)::value` 相同；否则为假 | |
| template <class T, class... Args> struct is_constructible; | 见下文 | T 和参数包 `Args` 中的所有类型应当是完整类型、（可能是 cv 修饰的）void 或未知范围的数组。 |
| template <class T> struct is_default_constructible; | `is_constructible<T>::value` 为真。 | T 应当是完整类型、（可能是 cv 修饰的）void 或未知范围的数组。 |
| template <class T> struct is_copy_constructible; | 对于可引用类型 `T`，结果与 `is_constructible<T, const T&>:value` 相同；否则为假。 | T 应当是完整类型、（可能是 cv 修饰的）void 或未知范围的数组。 |
| template <class T> struct is_move_constructible; | 对于可引用类型 `T`，结果与 `is_constructible<T, T&&>:value` 相同；否则为假。 | T 应当是完整类型、（可能是 cv 修饰的）void 或未知范围的数组。 |

# 表 49 — 类型属性谓词（续上）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T, class U> struct is_assignable; | 表达式 `declval<T>() = declval<U>()` 作为不求值的操作数时是格式良好的（第 5 条）。访问检查的执行如同在一个与 T 和 U 无关的上下文中进行。仅考虑赋值表达式的有效性。[注：该表达式的编译可能会导致侧效应，例如类模板特化的实例化和函数模板特化的实例化、隐式定义函数的生成等。此类侧效应不在“直接上下文”，且可能导致程序不符合规范。——结束] | T 和 U 应当是可能的类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_copy_assignable; | 对于可引用类型 T，结果与 `is_assignable<T&, const T::>::value` 相同，否则为 `false` | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_move_assignable; | 对于可引用类型 T，结果与 `is_assignable<T&, T&&>::value` 相同，否则为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |

# 表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T> struct is_destructible; | 对于引用类型，`is_destructible<T>::value` 为 `true` | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| | 对于不完全类型和函数类型，`is_destructible<T>::value` 为 `false`。 | | |
| | 对于对象以及给 `remove_all_extends<T>` 的 U，如果表达式 `std::declval<U>().()` 作为不求值的操作数时是格式良好的（第 5 条），则 `is_destructible<T>::value` 为 `true`，否则为 `false`。 | | |
| template <class T, Args...> struct is_trivially_constructible; | `is_constructible<T, Args>::value` 为 `true`，且下文定义的 `is_constructible` 变量定义已知未调用任何非平凡的操作（30, 12）。 | T 和参数包 `Args` 中的所有类型都应当是完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_trivially_default_constructible; | `is_trivially_constructible<T>::value` 为 `true`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_trivially_copy_constructible; | 对于引用类型 T，结果与 `is_trivially_constructible<T, const T&&>::value` 相同，否则为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_trivially_move_constructible; | 对于可引用类型 T，结果与 `is_trivially_constructible<T, T&&>::value` 相同，否则为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |

# 表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| struct is_trivially_assignable; | `is_assignable<T, U>::value` 为 `true` 且由 `is_assignable` 定义的赋值已知未调用非平凡的操作（3.9, 12）。 | T 和 U 应当是完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_trivially_copy_assignable; | 对于可引用类型 T，结果与 `is_trivially_assignable<T, const T&>::value` 相同，否则为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_trivially_move_assignable; | 对于可引用类型 T，结果与 `is_trivially_assignable<T, T&&>::value` 相同，否则为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_trivially_destructive; | `~::~value` 为 `true` 且指定的析构函数是平凡的。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_nothrow_constructible; | `is_constructible<T, Args...>::value` 为 `true` 且下文定义的 `is_constructible` 变量定义已知不抛出任何异常（5.3.7）。 | T 和参数包 `Args` 中的所有类型应当是完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_nothrow_default_constructible; | `is_nothrow_<T>::value` 为 `true`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_nothrow_copy_constructible; | 对于可引用类型 T，结果与 `is_nothrow_<T, const T>::value` 相同。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| struct is_nothrow_move_constructible; | 对于可引用类型 T，结果与 `is_nothrow_<T, T&&>::value` 相同。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |

# 表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
| --- | --- | --- |
| template <class T, class U> struct is_nothrow_assignable; | `is_assignable<T, U>::value` 为 `true` 且由 `is_assignable` 定义的赋值已知不抛出任何异常（5.3.7）。 | T 和 U 应当是完全类型、`void`（可能带有 cv 限定符）或未知边界的数组 |
| template <class T> struct is_nothrow_default_constructible; | `is_constructible<T>::value` 为 `true` 且下文定义的变量定义已知不抛出任何异常。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_nothrow_copy_constructible; | 对于可引用类型 T，结果与 `is_nothrow_<T, const T&>::value` 为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |
| template <class T> struct is_nothrow_move_constructible; | 对于可引用类型 T，结果与 `is_nothrow_<T, T&&>::value` 为 `false`。 | T 应当是一个完全类型、`void`（可能带有 cv 限定符）或未知边界的数组。 |

## 20.10.5 类型属性查询

此子句包含了用于编译时查询类型属性的断言。

| 模板 | 值 |
| --- | --- |
| template struct alignment_of; template <class T> struct rank; template <class T, unsigned I = 0> struct extent; | alignof(T)。要求:alignof(T)应当是一个有效表达式（5.3.6）如果 T 是数组，表示 T 的维数的整数值；否则为0。如果 T 不是数组，或者它的维度小于或等于 I，或者如果 I 为 0 且 T 类型为“未知边界的 U”，则否则；边界（8.3.4）第 I 个索引的边界从0开始 |

+   [示例:
// 以下断言成立：
asert(rank<int>::value == 0);
asert(rank<int>[2]>::value == 1);
asert(rank<int>[4]>::value == 2);
// 结束示例;

# ISO/IEC N4296

```cpp
```
