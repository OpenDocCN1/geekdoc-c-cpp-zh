

# ISO/IEC 14882:2017(E)

```cpp
template <class Alloc, class U, class... Args>
variant(allocator_arg_t, const Alloc& a, in_place_type<T>,
       initializer_list<U> u, Args&&... args);
template <class Alloc, size_t I, class... Args>
variant(allocator_arg_t, const Alloc& a, in_place_index<I>, Args&&... args);
template <class Alloc, size_t I, class U, class... Args>
variant(allocator_arg_t, const Alloc& a, in_place_index<I>,
       initializer_list<U> u, Args&&... args);
```

34 要求：Alloc 满足 (20.5.3.5) 中 Allocator 的要求。

35 效果：与前面的构造函数等效，所包含的值是使用 uses-allocator 构造函数 (23.10.7.2) 构建的。

## 23.7.3.2 析构函数 [variant.dtor]

```cpp
~variant();
```

> 效果：如果 valueless_by_exception 为 false，则销毁包含的值。

> 备注：如果对于所有 T，is_trivially_destructible<v,T> == true，则此析构函数应当是平凡的（trivial）。

## 23.7.3.3 赋值 [variant.assign]

```cpp
variant& operator=(const variant& rhs);
```

- 令 j 为 rhs.index()。

> 效果：如果 rhs 均不持有值，则没有效果。否则，
- * 如果 this 持值但 rhs 没有，则销毁 *this 中包含的值并将 *this 设置为不持有值。否则。
- 如果 index() == j，则将 rhs 中包含的值赋予 *this 中包含的值。否则，
- 如果 is_nothrow_move_constructible<v,T> 或 is_no_move_constructible<v,T> 为 true，则等效于 emplace<j>(get<j>(rhs))。否则，
```cpp
this.
```

返回：*this。

后置条件：index() == rhs.index()。

> 备注：除非对于所有 i，is_copy_constructible<v,T> && is_copy_assignable<v,T> 为 true，否则此函数不参与重载解析。

```cpp
variant& operator=(variant&& rhs) noexcept(see below);
```

- 令 j 为 rhs.index()。

> 效果：如果 rhs 均不持有值，则没有效果。否则，
- * 如果 this 持值但 rhs 没有，则销毁 *this 中包含的值并将 *this 设置为不持有值。否则。
- 如果 index() == j，将 get<j>(rhs) 赋予 *this 中包含的值。否则，
- 等效于 emplace<j>(get<j>(std::move(rhs)))。

返回：*this。

9 备注：如果对于所有 i，is_move_assignable<v<T>> 为 true。noexcept 内部表达式等效于 v<T>，

- (9.1) 如果调用 T 的构造（带有 rhs.index()）期间抛出异常，variant 将不持有值。

- (9.2) 如果在调用 T 的移动赋值期间抛出异常，则赋值的值由 T 的移动赋值的异常保证定义；index() 将为 j。

```cpp
template <class T> void operator(T&&) noexcept(see below);
```

10 令 T 为按如下定义的类型：对于每个变体类型 T 构建一个虚函数 FUN(T)。重载 FUN(T) 通过函数 (std::forward<T>(t)) 的重载解析来定义，该函数定义了变体类型 T，它是赋值后容器的值。

11 效果：

- (11.1) 如果 this 持 T，将 std::forward<T>(t) 赋予 this 中包含的值。否则，
- (11.2) 如果 is_nothrow_move_constructible<v<T>> 为 true，则等效于 emplace(std::forward<T>(t))。
- (11.3) 等效于 operator(variant(std::forward<T>(t)))。

12 后置条件：holds_alternative<T>(this) 为 true，由上述虚函数选择的 T。

13 返回：

14 备注：除非 is_same_v<decay<T>, variant> 为 false，is_assignable_v<v<T>, T> && is_nothrow_constructible<v<T>, T> 为 true，且 FUN(std::forward<T>(t)) 的函数集合是良好的。

15 注意：

```cpp
variant<string, string> v;
v = "abc";
```

良好的，但两个变体类型都有可行的构造函数 --注意

16 noexcept 内部的表达式等效于：

- (16.1) 如果将 std::forward<T>(t) 赋值给 this 的值期间抛出异常，则容器的值由赋值的异常保证定义；exception_by_exception() 为 false
- 在初始化容器期间抛出异常，variant 将不持有值。

## 23.7.3.4 修饰符 [variant.mod]

```cpp
template <class T> void emplace(Args&...);
```

- I 是 T 在 Types 中的从零索引。
- 效果：等效于 return emplace(std::forward<Args>(args)...);
- 备注：除非 is_constructible<T, Args...> 为 true，且 T 在 Types 中出现一次，此函数不参与重载解析。

```cpp
template <class T, class U, class Args...> T& emplace(initializer_list<U> il, Args&...);
```

4 令 I 为 T 的从零索引。
5 效果：等效于 return replace(il, std::forward<Args>(args)...);
6 备注：除非 is_constructible<T, initializer_list<U>, Args...> 为 true，且 T 在 Types 中精确出现，此函数不参与重载解析。

```cpp
template <size_t I, class Args...> variant_alternative_t<I, Types>& emplace(Args&...);
```

7 要求：I 是 sizeof(Types)...。
8 效果：如果 valueless_by_exception() 为 false，则直接构造包含的值。初始化包含的值就像使用参数 std::forward<Args>(args) 非初始化该类型的 variant。
9 后置条件：index(I) == I。
10 返回：新包含的值。
11 抛出：在初始化包含的值期间抛出的异常。
12 备注：除非 is_constructible<T, initializer_list<U>, Args...> 为 true，此函数不参与重载解析。在初始化包含的值期间抛出异常，variant 可能不持有值。

```cpp
template <size_t I, class Args...> variant_alternative_t<I, Types>& emplace(initializer_list<U> il, Args&...);
```

13 要求：I 是 sizeof(Types)...。
14 效果：如果 valueless_by_exception() 为 false，则直接构造包含的值。初始化包含的值就像使用参数 std::forward<Args>(args) 非初始化该类型的 variant。
15 后置条件：index(I) == I。
16 返回：新包含的值。
17 抛出：在初始化包含的值期间抛出的异常。
18 备注：除非 is_constructible<T, initializer_list<U>, Args...> 为 true。在初始化包含的值期间抛出异常，variant 可能不持有值。

## 23.7.5 值状态 [variant.status]

```cpp
constexpr bool valueless_by_exception() const noexcept;
```

效果：当且仅当 variant 持值时返回 false。

> 注意：如果在类型更改的赋值期间抛出异常，variant 可能不持有值。后者意味着即使是 variant<float, int> 也可以变为 valueless_by_exception()，例如

```cpp
struct S { operator int() { throw; };
variant<float, int> v(S{});
```

constexpr size_t index() 如果 valueless_by_exception() 为 true，返回 `npos`。否则，返回包含的值的从零索引。

## 23.7.3.6 交换 [variant.swap]

```cpp
void swap(variant& lhs, variant& rhs) noexcept(see below);
```

- 要求：类型 T 的左值应当可交换的 (20.5.3.2)，且对于所有 i，is_move_constructible<T> 为 true。

效果：

- 如果 valueless_by_exception() && rhs.valueless_by_exception() 则没有效果。否则，
- 如果 index() == rhs.index()，swap(get<this>, get<rhs>) 其中 i 是 index(i)。否则，
- 交换 rhs 和 this 的值。

备注：如果在调用 swap(get<this>, get<rhs)) 期间发生异常，*this 和 rhs 包含的值的状态由 T 的移动构造函数的异常保证决定。noexcept 内部的表达式等效于所有 i 的 is_move_constructible<T> && is_not_swapable<T> 逻辑与。

