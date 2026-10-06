

# ISO/IEC 14882:2017(E)

(24.10) — is_convertible_v<const optional<U>&, T> 为 false,

(24.11) — is_assignable_v<T&, optional<U>> 为 false,

(24.12) — is_assignable_v<const T&, optional<U>> 为 false,

(24.13) — is_assignable_v<T&, const optional<U>&> 为 false, 以及

(24.14) — is_assignable_v<const T&, const optional<U>&> 为 false.

```
template<class...> T& elems(Args... args);
```

25 要求: is_constructible_v<T, Args...> 为 true。

26 影响: *this = nullptr. 它初始化包含的值，其方式相当于使用参数 `std::forward<Args>(args)...` 直接（非列表）初始化一个类型为 T 的对象。

27 后置条件: *this 包含一个值。

28 返回: 指向新包含值的引用。

29 抛出: 异常如果在 T 的选定构造函数期间抛出异常。

30 备注: 如果在调用 T::constructor 期间抛出异常，则此不包含任何值，且之前的 *val（如果有）已被销毁。

```
template<class U> T& elems(initializer_list<U> il, Args...);
```

31 影响: *this = nullptr. 它初始化包含的值，其方式相当于使用参数 `il` 和 `std::forward<Args>(args)...` 直接（非列表）初始化一个类型为 T 的对象。

32 后置条件: *this 包含一个值。

33 返回: 指向新包含值的引用。

34 抛出: 异常由 T 的选定构造函数抛出的异常。

35 备注: 如果在调用 T::constructor 期间抛出异常，则此不包含任何值，且之前的 *val（如果有）已被销毁。除非 is_constructible_v<T, initializer_list<U>&> 为 true，否则此函数不参与重载解析。

## 23.6.3. swap [optional.swap]

```
void swap(optional& rhs) noexcept(see below);
```

+ 1 要求: T 的左值应该是可交换的，且 is_move_constructible_v<T> 为 true。

+ 2 影响: 参见表 30。

+ 3 抛出: 表 39 相关部分中的操作抛出的任何异常。

+ 4 备注: 异常规格说明 `noexcept` 等于：

is_not_move_constructible<T> && !is_swapable<T>

如果抛出异常，`bool(*val and rhs)` 的结果保持不变。如果在调用函数 `swap` 期间抛出异常，*val 和 *rhs.val 的状态取决于 swap 对值的异常保证。如果在调用 T 的移动构造函数 期间抛出异常，*val 和 *rhs.val 的状态取决于异常安全保证。

## 23.6.3.5 Ob [optional.observe]

```
constexpr T* operator->() const;
constexpr T* operator->();
```

要求: *this 包含一个值。

表 39 — optional::swap(optional&) 影响

| *this 包含一个值 | *this 不包含一个值 |
|--- |--- |
| rhs 包含一个值 | 调用 swap(*this, *rhs) | 初始化 *this 的包含的值，其方式相当于使用 std::move(*rhs) 直接（非列表）初始化一个类型为 T 的对象，随后执行 rhs.val->T::(T)；后置条件是 *this 包含一个值且 rhs 不包含一个值 |
| rhs 不包含一个值 | 初始化 rhs 的包含的值，其方式相当于使用 std::move(*this) 直接（非列表）初始化一个类型为 T 的对象，随后执行 val->T::(T)；后置条件是 *this 不包含一个值 | 无影响 |

+ 2 返回: val。
3 抛出: 无。
4 备注: 这些函数应当是 constexpr 函数。
5 constexpr T& operator() const&;
6 constexpr T& operator() const&&;
7 要求: *this 包含一个值。
7 返回: val。
8 抛出: 无。
9 备注: 这些函数应当是 constexpr 函数。
10 constexpr T&& operator() const&&;
11 constexpr T&& operator() const&; 
12 要求: 等于：return std::move(*val);
13 constexpr explicit bool() const noexcept;
14 返回: 当且仅当 *this 包含一个值时为 true。
15 备注: 此函数应当是 constexpr 函数。
16 constexpr bool has_value() const noexcept;
17 返回: 当且仅当 *this 包含一个值时为 true。
18 备注: 此函数应当是 constexpr 函数。

```
constexpr const T& value() const;
constexpr T& value() &;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr T& value() &&;
constexpr const T& value() const;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
template<class U> constexpr T valueor(U&& v) &&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
template<class U> constexpr T valueor(U&& v) const;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
template<class U> constexpr T valueor(U&& v) const;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
constexpr reset() &&;
```

影响: 等于：

```
return
this) ? *val： throw
_optional_
();
```

```
template<class U> constexpr T valueor(U&& v) const&&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
template<class U> constexpr T valueor(U&& v) const&;
```


于 等于：

```
return (*this) ? *val : std::forward<U
v);
```

## 23.6.3.6 Modifiers

```
constexpr reset() &&;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
template<class U> constexpr T valueor(U&& v) const&&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
template<class U> constexpr T valueor(U&& v) const&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
constexpr T& operator() const&;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr T& operator() const&&;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr T& value() &&;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr T& value() &;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr const T& value() const;
```

影响: 等于：

```
return (*this) ? *val : throw bad_optional_access();
```

```
constexpr reset() &&;
```

+ 1 影响: *this = nullptr. 它销毁包含的值。
+ 2 后置条件: *this 不包含任何值。

```
template<class U> constexpr T valueor(U&& v) const&&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

```
template<class U> constexpr T valueor(U&& v) const&;
```

等于 等于：

```
return (*this) ? *val : std::forward<U>(v);
```

## 23.6.3.7 Comparison with nullopt [optional.nullops]

```
template <class T> constexpr bool operator==(const optional<T>& x, nullopt_t) noexcept;
```

```
template <class T> constexpr bool operator==(nullopt_t, const optional<T>& x) noexcept;
```

+   1 返回: !x.

