

```cpp
// 20.7.1.2, hash support
template<class T> struct hash;
template<class... Types> struct hash<variant<Types...>>;
template<> struct hash<monostate>;
}
```

## 20.7.3 类模板 variant

### 20.7.3.1 通用

```cpp
namespace std {
  template<class... Types>
  class variant {
  public:
    // 20.7.3.2, constructors
    constexpr variant() noexcept(see below);
    constexpr variant(const variant&);
    constexpr variant(variant&&) noexcept(see below);

    template<class T>
      constexpr variant(T&&) noexcept(see below);

    template<class T, class... Args>
      constexpr explicit variant(in_place_type_t<T>, Args&&...);
    template<class T, class U, class... Args>
      constexpr explicit variant(in_place_type_t<T>, initializer_list<U>, Args&&...);

    template<size_t I, class... Args>
      constexpr explicit variant(in_place_index_t<I>, Args&&...);
    template<size_t I, class U, class... Args>
      constexpr explicit variant(in_place_index_t<I>, initializer_list<U>, Args&&...);

    // 20.7.3.3, destructor
    ~variant();

    // 20.7.3.4, assignment
    constexpr variant& operator=(const variant&);
    constexpr variant& operator=(variant&&) noexcept(see below);

    template<class T> variant& operator=(T&&) noexcept(see below);

    // 20.7.3.5, modifiers
    template<class T, class... Args>
      T& emplace(Args&&...);
    template<class T, class U, class... Args>
      T& emplace(initializer_list<U>, Args&&...);
    template<size_t I, class... Args>
      variant_alternative_t<I, variant<Types...>>& emplace(Args&&...);
    template<size_t I, class U, class... Args>
      variant_alternative_t<I, variant<Types...>>& emplace(initializer_list<U>, Args&&...);

    // 20.7.3.6, value status
    constexpr bool valueless_by_exception() const noexcept;
    constexpr size_t index() const noexcept;

    // 20.7.3.7, swap
    void swap(variant&) noexcept(see below);
  };
}
```

¹ 任何 `variant` 实例在任意给定时刻要么持有其备选类型之一的值，要么不持有任何值。当 `variant` 实例持有备选类型 T 的值时，表示类型为 T 的值，被称为 variant 对象的 *所含值*，已在 variant 对象的存储中分配。实现不允许使用额外的存储，例如动态内存，来分配

is ill-formed, as both alternative types have an equally viable constructor for the argument. — end note]

效果：以 *this 初始化为持有备选类型 T_j，并如同以 std::forward<T>(t) 直接非列表初始化它一样直接非列表初始化所含值。

后置条件：holds_alternative<T_j>(*this) 为 true。

抛出：所选备选类型 T_j 初始化时抛出的任何异常。

说明：noexcept 内部的表达式等价于 is_nothrow_constructible_v<T_j, T>。如果 T_j 的所选构造函数是 constexpr 构造函数，则该构造函数是 constexpr 构造函数。

```
template<class T, class... Args> constexpr explicit variant(in_place_type_t<T>, Args&&... args);
```

约束：

- Types... 中恰好出现一次 T 且
- is_constructible_v<T, Args...> 为 true。

效果：如同以参数 std::forward<Args>(args)... 直接非列表初始化类型为 T 的对象一样初始化所含值...

后置条件：holds_alternative<T>(*this) 为 true。

抛出：调用 T 的所选构造函数时抛出的任何异常。

说明：如果 T 的所选构造函数是 constexpr 构造函数，则该构造函数是 constexpr 构造函数。

```
template<class T, class U, class... Args>
constexpr explicit variant(in_place_type_t<T>, initializer_list<U> il, Args&&... args);
```

约束：

- Types... 中恰好出现一次 T 且
- is_constructible_v<T, initializer_list<U>&, Args...> 为 true。

效果：如同以参数 il, std::forward<Args>(args)... 直接非列表初始化类型为 T 的对象一样初始化所含值...

后置条件：holds_alternative<T>(*this) 为 true。

抛出：调用 T 的所选构造函数时抛出的任何异常。

说明：如果 T 的所选构造函数是 constexpr 构造函数，则该构造函数是 constexpr 构造函数。

```
template<size_t I, class... Args> constexpr explicit variant(in_place_index_t<I>, Args&&... args);
```

约束：

- I 小于 sizeof...(Types) 且
- is_constructible_v<T_I, Args...> 为 true。

效果：如同以参数 std::forward<Args>(args)... 直接非列表初始化类型为 T_I 的对象一样初始化所含值...

后置条件：index() 为 I。

抛出：调用所选构造函数 T_I 时抛出的任何异常。

说明：如果 T_I 的所选构造函数是 constexpr 构造函数，则该构造函数是 constexpr 构造函数。

```
template<size_t I, class U, class... Args>
constexpr explicit variant(in_place_index_t<I>, initializer_list<U> il, Args&&... args);
```

约束：

- I 小于 sizeof...(Types) 且
- is_constructible_v<T_I, initializer_list<U>&, Args...> 为 true。

效果：如同以参数 il, std::forward<Args>(args)... 直接非列表初始化类型为 T_I 的对象一样初始化所含值...

*后置条件：* `index()` 为 `I`。

*说明：* 如果 `T_i` 的所选构造函数是 constexpr 构造函数，则该构造函数是 constexpr 构造函数。

### 20.7.3.3 析构函数

`~variant();`

*效果：* 如果 `valueless_by_exception()` 为 false，则销毁当前所含值。

*说明：* 如果对所有 `T_i`，`is_trivially_destructible_v<T_i>` 为 true，则该析构函数是平凡的。

### 20.7.3.4 赋值

`constexpr variant& operator=(const variant& rhs);`

令 `j` 为 `rhs.index()`。

*效果：*

- — 如果 *this 也不持有值也不持有 rhs，则无效果。
- — 否则，如果 *this 持有值但 rhs 不持有，则销毁 *this 中所含的值并将 *this 设置为不持有值。
- — 否则，如果 `index() == j`，则将 rhs 中所含的值赋给 *this 中所含的值。
- — 否则，如果 `is_nothrow_copy_constructible_v<T_j>` 为 true 或 `is_nothrow_move_constructible_v<T_j>` 为 false，则等价于 `emplace<j>(get<j>(rhs))`。
- — 否则，等价于 `operator=(variant(rhs))`。

*返回：* `*this`。

*后置条件：* `index() == rhs.index()`。

*说明：* 除非对所有 i，`is_copy_constructible_v<T_i> && is_copy_assignable_v<T_i>` 为 true，否则该运算符被定义为已删除。如果对所有 i，`is_trivially_copy_constructible_v<T_i> && is_trivially_copy_assignable_v<T_i> && is_trivially_destructible_v<T_i>` 为 true，则该赋值运算符是平凡的。

`constexpr variant& operator=(variant&& rhs) noexcept(see below);`

令 `j` 为 `rhs.index()`。

*约束：* 对所有 i，`is_move_constructible_v<T_i> && is_move_assignable_v<T_i>` 为 true。

*效果：*

- — 如果 *this 也不持有值也不持有 rhs，则无效果。
- — 否则，如果 *this 持有值但 rhs 不持有，则销毁 *this 中所含的值并将 *this 设置为不持有值。
- — 否则，如果 `index() == j`，则将 `get<j>(std::move(rhs))` 赋给 *this 中所含的值。
- — 否则，等价于 `emplace<j>(get<j>(std::move(rhs)))`。

*返回：* `*this`。

*说明：* 如果对所有 i，`is_trivially_move_constructible_v<T_i> && is_trivially_move_assignable_v<T_i> && is_trivially_destructible_v<T_i>` 为 true，则该赋值运算符是平凡的。`noexcept` 内部的表达式等价于：对所有 i，`is_nothrow_move_constructible_v<T_i> && is_nothrow_move_assignable_v<T_i>`。

- — 如果在调用 `T_j` 的移动构造时抛出异常（其中 j 为 `rhs.index()`），variant 将不持有值。
- — 如果在调用 `T_j` 的移动赋值时抛出异常，所含值的状态如 `T_j` 的移动赋值的异常安全保证所定义；`index()` 将为 `j`。

`template<class T> variant& operator=(T&& t) noexcept(see below);`

令 `T_j` 为按如下方式确定的类型：为每个备选类型 `T_i` 构建一个虚构函数 `FUN(T_i)`，其中 `T_i x[] = {std::forward<T>(t)};` 对某个虚构变量 x 是 well-formed 的。The

