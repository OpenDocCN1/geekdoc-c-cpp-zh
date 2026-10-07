
### 20.9.4 统一类型 [meta.unary]

- 1 此子类包含了用于在编译时查询类型属性的模板。
- 2 这些模板中的每一个都是类型特征（20.9.1），如果相应的恒等为真，则为 `true_type` 的基础特征，否则为 `false_type`。

### 20.9.4.1 原始类型分类 [meta.unary.cat]

- 1 原始类型分类对应 C++ 标准第 3.9 节中的描述。
- 2 对于任何给定的类型 T，将这些模板之一应用于 T 以及经过 cv 修饰的 T 的结果应相同。
- 3 [注：对于任何给定的类型 T，恰有一个原始类型分类的 `value` 成员为真。—— 注结束]

# ISO/IEC 14882:2011(E)

表 47 — 原始类型分类谓词

| 模板 | 条件 | 注释 |
|---|---|---|
| template <class T> struct is_void; | T 为 void | |
| template <class T> struct is_integral; | T 是整数类型 (3.9.1) | |
| template <class T> struct is_floating; | T 是浮点类型 (3.9.1) | |
| template <class T> struct is_array; | T 是已知或未知范围的数组 | 类模板数组 (23.3.2) 不是数组类型。 |
| template <class T> struct is_pointer; | T 是指针 (3.9.2) | 包含指向函数的指针，但不包括指向非静态成员的指针。 |
| template <class T> struct is_value_reference; | T 是值引用 | type (8.3.2) |
| template <class T> struct is_value_reference; | T 是值引用 | type (8.3.2) |
| template <class T> struct is_member_object_pointer; | T 是指向非静态数据成员的指针 | |
| template <class T> struct is_member_function_pointer; | T 是指向非静态成员成员的指针 | |
| template <class T> struct is_enum; | T 是枚举 | type (3.9.2) |
| template <class T> struct is_union; | T 是联合体类型 (3.9.2) | |
| template <class T> struct is_class; | T 是类类型但不是联合体类型 (3.9.2) | |
| template <class T> struct is_function; | T 是函数类型 (3.9.2) | |

## 20.9.4.2 复合类型特性 [meta.unary.comp]

- 1 这些模板根据第 3.9 节中的描述，提供了原始类型分类的方便组合。
- 2 对于任何给定的类型 T，将这些模板之一应用于 T 以及经过 cv 修饰的 T 应当产生相同的结果。

表 48 — 复合类型分类谓词

| 模板 | 条件 | 注释 |
|---|---|---|
| template <class T> struct is_reference; | T 是左值引用或值引用 | |
| template <class T> struct is_arithmetic; | T 是算术类型 (3.9.1) | |
| template <class T> struct is_fundamental; | T 是基本类型 (3.9.1) | |

表 48 — 复合类型分类谓词（续）

| 模板 | 条件 | 注释 |
|---|---|---|
| template <class T> struct is_object; | T 是对象类型 (3.9) | |
| template <class T> struct is_scalar; | T 是标量类型 (3.9) | |
| template <class T> struct is_compound; | T 是复合类型 (3.9.2) | |
| template <class T> struct is_member_pointer; | T 是指向非静态数据成员或非静态成员的指针 | |

## 20.9.4.3 类型属性 [meta.unary.prop]

- 1 这些模板提供了对类型某些更重要属性的访问。
- 2 不确定库是否定义了这些模板的任何完全特化或部分特化版本。
- 3 对于本节声明的所有类模板 X，使用作为类特化的类作为模板参数来实例化该模板，可能会导致模板参数的不完全实例化，当且仅当 X 的语义要求该参数必须是完整类型时是如此。

表 49 — 类型属性谓词

| 模板 | 条件 | 前提条件 |
|---|---|---|
| template <class T> struct_const; | T 经过 const 修饰 (3.9.3) | |
| template <class T> struct_volatile; | T 经过 volatile 修饰 (3.9.3) | T 应当是一个完整类型足以可能经过 cv 修饰）、void 或未知范围的数组 |
| template <class T> struct_trivially_copyable; | T 是平凡可拷贝类型 (3.9) | T 应当是一个完整类型足以可能经过 cv 修饰）、void 或未知范围的数组 |
| template <class T> struct_standard_layout; | T 是标准布局类型 (3.9) | T 应当是一个完整类型足以可能经过 cv 修饰）、void 或未知范围的数组 |
| template <class T> struct_pod; | T 是 POD 类型 (3.9) | T 应当是一个完整类型足以可能经过 cv 修饰）、void 或未知范围的数组 |
| template <class T> struct_literal_type; | T 是字面量类型 (3.9) | T 应当是一个完整类型足以可能经过 cv 修饰）、void 或未知范围的数组 |

表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
|---|---|---|
| template <class T> struct is_empty; | T 是类类型但不是联合体类型，且没有长度为 0 的非静态成员、没有虚函数、没有 is_empty::value 为 false 的基类。 | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_polymorphic; | T 是多态类 (10.3) | T 应当是一个完整类型。（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_abstract; | T 是抽象类 (10.4) | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_signed; | is_arithmetic<T>::value(-1) < T(0) | |
| template <class T> struct is_unsigned; | is_arithmetic<T>::value(0) < T(-1) | |
| template <class T>, class... Args struct is_constructible; | 下文 | T 和参数包 Args 中的所有类型应当完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_default_constructible; | is_constructible<T>::const value is true. | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_copy_constructible; | is_constructible<T, T&&>::value is true. | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_move_constructible; | is_constructible<T, T&&>::value is true. | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |

表 49 — 类型属性谓词（续）

| 模板 | 表达式 | 前提条件 |
|---|---|---|
| template <class T, class U> struct is_assignable; | declval<T>() = declval<U>(); 在被视为未赋值的操作数时是良好的（第 5 节）。访问检查是在与 T 和 U 无关的上下进行的。仅考虑赋值表达式的有效性。*注意：* 表达式可能会产生此类效应，如模板特化、函数特化、隐式定义的函数等。这些效应会导致程序错误。 | T 和 U 应当是完整类型。（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_copy_assignable; | is_assignable<T&>::value is true. | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_move_assignable; | is_assignable<T&&>::value is true. | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| template <class T> struct is_destructible; | 对于一个完整类型 T 和给定的 template <class U> struct { U; }; test<T>::test() 未被删除。 | T 应当是一个完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |

表 49 — 类型属性谓词（续）

| 模板 | 条件 | 前提条件 |
|---|---|---|
| <class T, class... Args> struct is_trivially_constructible; | is_constructible<T, Args>::value is true 且下文定义的 is_constructible 变量定义不是平凡的调用操作 (3.9, 12)。 | T 和参数包 Args 中的所有类型为完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T> struct is_trivially_default_constructible; | is_trivially_constructible<T>::const value is true. | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T> struct is_trivially_copy_constructible; | is_trivially_constructible<T, T&&>::value is true. | |
| <class T> struct is_trivially_move_constructible; | is_trivially_constructible<T, T&&>::value is true. | |
| <class T, class U> struct is_trivially_assignable; | is_assignable<T, U>::value is true 且下文定义的 is_assignable 不是平凡的调用操作 (3.9, 12)。 | T 和 U 应当是完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T> struct is_trivially_copy_assignable; | is_assignable<T, T&&>::value is true. | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T> struct is_trivially_move_assignable; | is_assignable<T, T&&>::value is true. | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T> struct is_trivially_destructible; | is_destructible<T>::value is true 且析构函数是已知的平凡的。 | T 应当是一个完整类型，（可能经过 cv 修饰）、void 或未知范围的数组。 |
| <class T, class... Args> struct is_nothrow_constructible; | is_constructible<T, Args>::value is true 且下文定义的 is_constructible 变量定义已知不抛出异常 (5.3.7)。 | T 和参数包 Args 中的所有类型为完整类型（可能经过 cv 修饰）、void 或未知范围的数组。 |

# ISO/IEC 14882:2011(E)

表 49 — 类型属性谓词（续接）

| 模板 | 条件 | 前提条件 |
|---|---|---|
| template <class T> struct is_nrow_constructible; | ::value 为 true。 | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| is_nrow_default_constructible; | | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct is_nrow_copy_constructible; | is_nrow_constructible<T>::value 为 true。 | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct is_nrow_move_constructible; | is_nrow_constructible<T>::value 为 true。 | （可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T, class U> struct is_nrow_assignable; | is_assignable<T,U>::value 为 true 且赋值不抛出任何异常（5.3.7）。 | T 和 U 必须是完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct is_nrow_copy_assignable; | is_nrow_assignable<T>::value 为 true。 | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct is_nrow_move_assignable; | is_nrow_assignable<T>::value 为 true。 | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct is_nrow_destructible; | is_destructible<T>::value 为 true 且析构函数已知不会抛出异常（5.3.7）。 | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |
| template <class T> struct has_virtual_destructor; | T 具有虚析构函数（12.4） | T 必须是一个完全类型（可能带有 cv 限定符）void，或未知边界的数组。 |

- 4 [示例：
```cpp
is_const<const volatile int>::value // true
is_const<const int*>::value // false
is_const<const int&>::value // false
is_const<const int[3]>::value // false
is_const<const int[3]>::value // true
```

- 5 [示例：
```cpp
remove_const<const volatile int>::type volatile int
```

### § 20.9.4.3

```cpp
remove_const<const int* const>::type // const int*
remove_const<const int&>::type // const int&
```
