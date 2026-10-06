

# ISO/IEC 14882:2017(E)

构造函数。除非 `is_constructible_v<T, U&>` 为真、`is_name_v<decay_t<U>, in_place_t>` 为假，且 `is_same_v<decay_t<U>>` 为假，否则该构造函数不参与重载解析。该构造函数是显式的（explicit），当且仅当 `is_convertible_v<U&, T>` 为假。

```cpp
template <class U> explicit(const optional<U> rhs);
```

影响：如果 `rhs` 包含一个值，则在用表达式 *rhs* 直接初始化类型为 T 的对象时，将包含的值赋值。

后置条件：`bool(rhs) == *(this)`。

抛出异常：T 的选定构造函数抛出的任何异常。

备注：此构造函数不参与重载解析（注意：此处 OCR 文本似乎截断或重复了）

- (27.1) — `is_constructible_v<T, const U>` 为真。
- (27.2) — `is_constructible_v<T, optional<U>&>` 为假。
- (27.3) — `is_constructible_v<T, optional<U>>` 为假。
- (27.4) — `is_constructible_v<T, const optional<U>>` 为假，
- (27.5) — `is_constructible_v<T, const optional<U>&>` 为假，
- (27.6) — `is_convertible_v<optional<U>&, T>` 为假。
- (27.7) — `is_convertible_v<optional<U>&&, T>` 为假。
- (27.8) — `is_convertible_v<const optional<U>&, T>` 为假。
- (27.9) — `is_convertible_v<const optional<U>&&, T>` 为假。

该构造函数是显式的，当且仅当 `is_convertible_v<const U&, T>` 为假。

```cpp
template <class U> explicit(const optional<U> rhs);
```

影响：如果 `rhs` 包含一个值，则在用表达式 `move(*rhs)` 直接初始化类型为 T 的对象时，将包含的值赋值。`bool(rhs)` 变。

后置条件：`bool(rhs) == *(this)`。

抛出异常：T 的选定构造函数抛出的任何异常。

备注：此构造函数不参与重载解析

- (31.1) — `is_constructible_v<T, U&>` 为真，
- (31.2) — `is_constructible_v<T, optional<U>&>` 为假。
- (31.3) — `is_constructible_v<T, optional<U>>` 为假。
- (31.4) — `is_constructible_v<T, const optional<U>>` 为假，
- (31.5) — `is_constructible_v<T, const optional<U>&>` 为假，
- (31.6) — `is_convertible_v<optional<U>&, T>` 为假。
- (31.7) — `is_convertible_v<optional<U>&&, T>` 为假。
- (31.8) — `is_convertible_v<const optional<U>&, T>` 为假。
- (31.9) — `is_convertible_v<const optional<U>&&, T>` 为假。

该构造函数是显式的，当且仅当 `is_convertible_v<const U&, T>` 为假。

## 23.6.3.2 析构函数 [optional.dtor]

- optional(U);

影响：如果 `is_trivially_destructible_v<T>` 为真且 `*this` 包含一个值，则调用 `val->T::~T()`

备注：如果 `is_trivially_destructible_v<T>` 为真，则该析构函数应该是平凡析构函数（trivial destructor）。

## 23.6.3.3 赋值 [optional.assign]

optional<T>& operator=(nullopt_t) noexcept;

影响：`*this` 包含一个值，调用 `val->T::~T()` 销毁包含的值；否则无影响。

返回：*this*。

后置条件：`*this` 不包含一个值。

optional<T>& operator=(const optional& rhs);

影响：参见表 35。

| 表 35 — optional::operator=(const optional& rhs) 影响 | *this 包含一个值 | *this 不包含一个值 |
| :--- | :--- | :--- |
| rhs 包含一个值 | 将 `*rhs` 赋值给包含的值 | 仿若用 `*rhs` 直接非列表初始化一个类型为 T 的对象来初始化包含的值 |
| rhs 不包含一个值 | 通过调用 `val->T::~T()` 销毁包含的值 | 无影响 |

返回：*this*。

后置条件：`bool(rhs) == bool(*this)` 保持不变。

备注：如果抛出异常，表达式 `bool(*this)` 的结果保持不变。如果在调用 T 的拷贝构造函数期间抛出异常，则无影响。包含的值的状态由 T 的拷贝赋值的异常保证定义，除非 `copy_constructible_v<T>` 为真且 `is_assignable_v<T>` 为真。

optional<T>& operator=(optional& rhs) noexcept(bool(rhs)) 保持不变。

影响：参见表 36。

| 表 36 — optional::operator=(optional& rhs) 影响 | *this 包含一个值 | *this 不包含一个值 |
| :--- | :--- | :--- |
| rhs 包含一个值 | 将 `std::move(*rhs)` 赋值给包含的值 | 仿若用 `std::move(*rhs)` 直接非列表初始化一个类型为 T 的对象来初始化包含的值 |
| rhs 不包含一个值 | 通过调用 `val->T::~T()` 销毁包含的值 | 无影响 |

返回：*this*。

后置条件：`bool(rhs) == bool(*this)`。

备注：该异常等价于：`is_throw_move_assignable<T> && is_throw_move_constructible<T>`。如果抛出任何异常，表达式 `bool(*this)` 的结果保持不变。如果在调用 T 的移动构造函数期间抛出异常，`*rhs.val` 的状态由 T 的异常保证决定。如果在调用 T 的移动赋值期间抛出异常，该状态由 T 的异常保证决定。此运算符不参与重载解析，除非 `is_constructible<T>` 为真且 `is_assignable<T>` 为真。

```cpp
template <class U> optional<T>& operator=(U&& u);
```

影响：如果 `this` 包含一个值，将 `std::forward(u)` 传递给包含的值；仿若用 `u` 直接初始化类型为 T 的对象来包含的值。

返回：*this*。

后置条件：`*this` 包含一个值。

备注：如果抛出异常，`bool(*this)` 的结果保持不变。如果在调用 T 的构造函数期间抛出异常，包含的值的状态由 T 的异常保证决定。此赋值不参与重载解析，除非 `is_constructible<T, const U&>` 为真、`is_assignable<T, const U&>` 为真，且 `is_constructible<T, optional<U>&>` 为假。

```cpp
template <class U> optional<T>& operator=(const optional& rhs);
```

影响：参见表 37。（注意：此处表 37 缺失，但提供了表 38）

| 表 38 — operator=(optional<U> rhs 影响 | *this 包含一个值 | *this 不包含一个值 |
| :--- | :--- | :--- |
| rhs 包含一个值 | 将 `move(*rhs)` 赋值给包含的值 | 仿若用 `move(*rhs)` 直接初始化一个类型为 T 的对象来初始化包含的值 |
| rhs 不包含一个值 | 通过调用 `val->T::~T()` 销毁包含的值 | 无影响 |

返回：*this*。

后置条件：`bool(rhs) == *(this)`。

备注：如果在调用 T 的构造函数期间抛出异常，`*this` 的状态保持不变。如果在调用 T 的赋值期间抛出异常，包含的值的状态由 T 的异常保证决定。此赋值的顺序未确定。

- (24.1) — `is_constructible_v<T, U>` 为真。
- (24.2) — `is_assignable_v<optional<U>, T>` 为真。
- (24.3) — `is_constructible_v<T, optional<U>>` 为假。
- (24.4) — `is_assignable_v<optional<U>, T>` 为假。
- (24.5) — `is_constructible_v<T, const optional<U>` 为假。
- (24.6) — `is_assignable_v<T, const optional<U>` 为假。
- (24.7) — `is_convertible_v<optional<U>, T>` 为假。
- (24.8) — `is_convertible_v<optional<U>, T>` 为假。
- (24.9) — `is_convertible_v<const optional<U>, T>` 为假。
- (24.10) — `is_convertible_v<const optional<U>, T>` 为假。
- (24.11) — `is_assignable_v<T, optional<U>>` 为假。
- (24.12) — `is_assignable_v<optional<U>, T>` 为假。
- (24.13) — `is_assignable_v<optional<U>, const optional<U>` 为假。
- (24.14) — `is_assignable_v<const optional<U>, optional<U>` 为假。

```cpp
template <class U> operator=(optional<U> rhs); result of the expression (*rhs) 保持不变。
```

21 影响：参见表 38。

