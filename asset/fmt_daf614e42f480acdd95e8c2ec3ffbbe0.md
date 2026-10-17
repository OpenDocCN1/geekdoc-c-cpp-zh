
`struct variant_alternative<I, variant<Types...>> { ... };`

`inline constexpr size_t variant_pos = -1;`

## 20.7.5 访问

`template<class T, class... Types>`

`constexpr bool holds_alternative(const variant<Types...>& v) noexcept;`

`template<size_t I, class... Types>`

`constexpr variant_alternative<I, variant<Types...>>& get(const variant<Types...>& v);`

`template<size_t I, class... Types>`

`constexpr variant_alternative<I, variant<Types...>>& get(variant<Types...>& v);`

# ISO/IEC 14882:2020(E)

```cpp
template<size_t I, class... Types>
constexpr variant_alternative_t<I, variant<Types...>>& get(const variant<Types...>);
template<size_t I, class... Types>
constexpr variant_alternative_t<I, variant<Types...>>& get(variant<Types...>);
template<class T, class... Types>
constexpr T& get(variant<Types...>);
template<class T, class... Types>
constexpr T& get(variant<Types...>) noexcept;
template<class T, class... Types>
constexpr T& get(const variant<Types...>);
template<class T, class... Types>
constexpr T& get(const variant<Types...>) noexcept;
template<size_t I, class... Types>
constexpr variant_alternative_t<I, variant<Types...>* get_if(variant<Types...>) noexcept;
template<size_t I, class... Types>
constexpr variant_alternative_t<I, variant<Types...>* get_if(const variant<Types...>) noexcept;
template<class T, class... Types>
constexpr T* get_if(variant<Types...>) noexcept;
template<class T, class... Types>
constexpr T* get_if(const variant<Types...>) noexcept;

// 20.7.6. 比较运算符
template<class T, class... Types>
constexpr bool operator==(const variant<Types...>, const variant<Types...>);
template<class T, class... Types>
constexpr bool operator!=(const variant<Types...>, const variant<Types...>);
template<class T, class... Types>
constexpr bool operator<(const variant<Types...>, const variant<Types...>);
template<class T, class... Types>
constexpr bool operator>(const variant<Types...>, const variant<Types...>);
template<class T, class... Types>
constexpr bool operator<=(const variant<Types...>, const variant<Types...>);
template<class T, class... Types>
constexpr common_comparison_category<T, three_way_comparable_t<Types>> operator<=>(const variant<Types...>, const variant<Types...>);

// 20.7.7. 访问
template<class Visitor, class... Variants>
constexpr void visit(Visitor&, Variants&);
template<class R, class Visitor, class... Variants>
constexpr R visit(Visitor&, Variants&);
// 20.7.8. monostate
struct monostate;
// 20.7.9. monostate 比较运算符
constexpr bool operator==(monostate, monostate) noexcept;
constexpr strong_ordering operator<=>(monostate, monostate) noexcept;
// 20.7.10. 特殊化算法
template<class T, class... Types>
void swap(variant<Types...>&&&, variant<Types...>) noexcept(see below);
// 20.7.11. class bad_variant_access
class bad_variant_access;
// 20.7.12, 哈希支持
template<class T> struct hash
template<class... Types> struct hash<variant<Types...>>;
template<T> struct hash<monostate>;
}
```

> 任何 `variant` 实例在任何时刻都持有其替代类型之一的值，或者不持有值。当 `variant` 实例持有替代类型 `T` 的值时，意味着类型为 `T` 的值（称为 `variant` 对象的 `contained_value`）位于 `variant` 的存储空间内。实现不允许使用额外的存储（例如动态内存）来分配该

包含的值。该变体应分配在变体存储的区域中，该区域对于 `Types` 中的所有类型都是适当对齐的。

`Types` 中的所有类型必须满足 `Cpp17Destructible` 要求（表 32）。

实例化一个没有模板参数的 `variant` 定义的程序是格式不正确的。

## 20.7.3.2 构造函数 [variant::ctor]

在接后的描述中，令 `i` 属于范围 `[0, sizeof...(Types)]`，且 `T_i` 为 `Types` 中的第 `i` 个类型。

```cpp
constexpr variant() noexcept(see below);
```

- 2 约束：`is_default_constructible_v<T_0>` 为 true。

- 3 效果：构造一个持有类型为 `T_0` 的值初始化值的变体。

- 4 后置条件：`valueless_by_exception()` 为 false 且 `index` 且 `index()` 为 0。

- 5 抛出：`T_0` 的值初始化时抛出的任何异常。

- 6 备注：此函数为 constexpr 当且仅当备选类型 `T_0` 的值初始化满足 constexpr 构造函数的要求。表达式 `noexcept` 等效于 `is_nothrow<T_0>()`。

> [注 1：参见类 `monostate`。 — 结束]

```cpp
constexpr variant(const variant& w);
```

- 7 效果：如果 `w` 持有值，则将变体初始化为与 `w` 相同，并使用 `get<j>(w)` 直接初始化包含的值，其中 `j` 为 `w.index()`。否则，初始化变体以持有一个值。

- 8 抛出：对于所有 `i`，直接初始化任何 `T` 时抛出的任何异常。

- 9 备注：如果对于所有 `i` `is_copy_constructible_v<T, T>` 为 true，则在下文定义。如果对于所有 `i` `is_trivial_move_constructible_v<T, T>` 为 true，则此构造函数是平凡的（trivial）。

```cpp
constexpr variant(variant&& w) noexcept(see below);
```

- 10 约束：对于所有 `i` `is_move_constructible_v<T>` 为 true。

- 11 效果：如果 `w` 持有值，则将变体初始化为与 `w` 相同，并使用 `get<j>(w)` 直接初始化包含的值，其中 `j` 为 `w.index()`。否则，初始化变体以持有一个值。

- 12 抛出：对于所有 `i`，移动构造任何 `T` 时抛出的任何异常。

- 13 备注：表达式 `noexcept` 等效于对于所有 `i` `is_nothrow_move_constructible_v<T, T>` 为 true 的逻辑与。如果对于所有 `i` `is_trivial_move_constructible_v<T, T>` 为 true，则此构造函数是平凡的。

```cpp
template<class T> constructor variant(T&& t) noexcept(see below);
```

令 `T` 为下文确定的类型：作为一个 `FUN(T)`；对于每个备选类型 `T`，使得 `T_i = {std::forward<T>(t)}` 对于某个实例变量 `x` 都是格式正确的。重载的 `FUN(T)` 通过表达式 `FUN(std::forward<T>(t))` 的重载解析进行选择，该表达式定义了备选类型 `T`，即构造后包含值的类型。

- 15 约束：

    - `sizeof...(Types)` 非零，

    - `is_same_remove_cref_t<T, variant>` 为 false，

    - `remove_cref_t<T>` 不是 `in_place_type_t` 或 `place_index_t` 的特化，

    - `is_constructible_v<variant, T>` 为 true，且

    - 表达式 `FUN(std::forward<T>(t))`（其中 `FUN` 为上述虚构函数集）是格式正确的。

> [注 2：`variant(string, string("abc"))` 是格式正确的，因为两个备选类型对于该参数都具有同样可行的构造函数。 — 结束]

效果：初始化 `*this*` 以持有备选类型 `Tj`，并如同使用 `std::forward<T>(t)` 进行直接非初始化一样直接初始化包含的值。

后置条件：`holds_alternative<T>(*this)` 为 true。

抛出：在初始化选定的备选类型（满足 `constructible<Tj, T>`）时抛出的任何异常。如果 `Tj` 选定的构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

```cpp
template<class T, class... Args> constexpr explicit variant(in_place_type<T>, Args&&...);
```

约束：

- `Types...` 中恰好有一个 `T`...

- `is_constructible<vT, Args...>` 为 true。

效果：初始化包含的值，如同使用参数 `std::forward<Args>(args...)` 对类型 `T` 的对象进行直接非初始化一样。

后置条件：`holds_alternative<T>(*this)` 为 true。

抛出：调用 `T` 的选定构造函数时抛出的任何异常。

备注：如果 `T` 的选定构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

```cpp
template<class T, class U, class... Args> constexpr explicit variant(in_place_type<T>, initializer_list<U> il, Args&&...);
```

约束：

- `Types...` 中恰好有一个 `T`...

- `is_constructible<vT, initializer_list<U>, Args...>` 为 true。

效果：初始化包含的值，如同使用参数 `il, std::forward<Args>(args...)` 对类型 `T` 的对象进行直接非初始化一样。

后置条件：`holds_alternative<T>(*this)` 为 true。

抛出：调用 `T` 的选定构造函数时抛出的任何异常。

备注：如果 `T` 的选定构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

```cpp
template<size_t I, class... Args> constexpr explicit variant(in_place_index_type<I>, Args&&...);
```

约束：

- `I` 小于 `sizeof...(Types)`

- `is_constructible<vTj, Args...>` 为 true。

效果：初始化包含的值，如同使用参数 `std::forward<Args>(args...)` 对类型 `Tj` 的对象进行直接非初始化一样。

后置条件：`index<T>()` 为 `I`。

抛出：调用 `Tj` 的选定构造函数时抛出的任何异常。

备注：如果 `Tj` 的选定构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

```cpp
template<size_t I, class... Args> constexpr explicit variant(in_place_index_type<I>, Args&&...);
```

约束：

- `I` 小于 `sizeof...(Types)`

- `is_constructible<vTj, Args...>` 为 true.

效果：初始化包含的值，如同使用参数 `std::forward<Args>(args...)` 对类型 `Tj` 的对象进行直接非初始化一样。

后置条件：`index<T>()` 为 `I`。

抛出：调用 `Tj` 的选定构造函数时抛出的任何异常。

备注：如果 `Tj` 的选定构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

```cpp
template<size_t I, class... Args> constexpr explicit variant(in_place_index_type<I>, Args&&...);
```

约束：

- `I` 小于 `sizeof...(Types)`

- `is_constructible<vTj, Args...>` 为 true.

效果：初始化包含的值，如同使用参数 `std::forward<Args>(args...)` 对类型 `Tj` 的对象进行直接非初始化一样。

后置条件：`index<T>()` 为 `I`.

抛出：调用 `Tj` 的选定构造函数时抛出的任何异常。

备注：如果 `Tj` 的选定构造函数是 constexpr 构造函数，则此为 constexpr 构造函数。

## 20.7.3.3 析构函数 [variant.dtor]

```cpp
variant();
```

效果：如果 `valueless_by_exception()` 为 false，则破坏包含的值。

备注：如果对于所有 `i` `trivially_destructible_v<T_i>` 为 true，则此析构函数是平凡的。

## 20.7.3.4 赋值 [variant.assign]

```cpp
constexpr variant& operator=(const variant& rhs);
```

- 令 `j` 为 `rhs.index()`；

- 效果：如果 `this` 不持有值，则没有效果。如果 `this` 持有值但 `rhs` 不持有，则破坏包含的值并设置为不持有值。

- 如果 `index() == j`，则将 `rhs` 的值赋值给 `*this`。

- 否则，等效于 `emplace<j>(rhs)`.

```cpp
constexpr variant& operator=(variant&& rhs) noexcept(see below);
```

- 令 `j` 为 `rhs.index()`；

- 约束：对于所有 `i` `is_move_constructible_v<T_j> && is_assignable_v<T_j>` 为 true。

- 效果：

    - 如果 `this` 不持有值，则没有效果。

    - 如果 `this` 持有值但 `rhs` 不持有，则破坏包含的值并设置为不持有值。

    - 如果 `index() == j`，则将 `rhs` 的值赋值给 `*this`。

    - 否则，等效于 `emplace<j>(std::move(rhs))`;

- 返回：`*this`;

- 备注：如果对于所有 `i` `is_copy_constructible_v<T_i> && is_assignable_v<T_i> && trivially_destructible_v<T_i>` 为 true，则此赋值运算符是平凡的。异常 `noexcept` 等于：`not_move_constructible_v<T_j> && is_assignable_v<T_j>`。

- 如果在调用 `T_j` 的移动赋值时（`j` 为 `rhs.index()`）抛出异常，变体将不持有值。
