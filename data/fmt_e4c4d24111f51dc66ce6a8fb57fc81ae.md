
# 20.11.1.6 特殊化算法

```cpp
template<class T, class D> void swap(unique_ptr<T, D>& x, unique_ptr<T, D>& y) noexcept;
```

1 约束：`is_swappable<D>` 为 true。

2 效果：调用 `x.swap(y)`。

```cpp
template<class T1, D1, T2, D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

3 返回：`x.get() == y.get()`

```cpp
template<class T1, D1, T2, D2> bool operator=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

4 令 `CT` 表示

```cpp
common_type<typename CT> unique_ptr<T1, D1>::pointer,
typename unique_ptr<T2, D2>::pointer;
```

5 强制要求

(5.1) `unique_ptr<T1, D1>::pointer` 可隐式转换为 `CT` 和

(5.2) `unique_ptr<T2, D2>::pointer` 可隐式转换为 `CT`。

前提条件：特化`<CT>` 是一个函数类型 (20.14)，它对指针值施加了严格排序 (25.8)。

7 返回：`less<CT>(x.get(), y.get())`.

```cpp
template<class T1, D1, T2, D2> bool operator<(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

8 返回：`y < x`。

```cpp
template<class T1, D1, T2, D2> bool operator<(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

9 返回：`(y < x)`。

```cpp
template<class T1, D1, T2, D2> bool operator==(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

10 返回：`(x != y)`。

```cpp
template<class T1, D1, T2, D2> requires_three_way_comparable<typename unique_ptr<T1, D1>::pointer>:
```

```cpp
compare_three_way_result<typename unique_ptr<T1, D1>::pointer>
typename unique_ptr<T2, D2>::pointer>
```

```cpp
operator<>(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

11 返回：`compare_three_way(x.get(), y.get())`.

```cpp
template<class T, class D> bool operator==(const unique_ptr<T, D>& x, nullptr_t) noexcept;
```

12 返回：`!x`。

```cpp
template<class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

前提条件：特化 `unique_ptr<T, D>::pointer` 是一个函数对象 (20.14)，它对指针值诱导了严格弱排序 (25.8)。

返回：第一个函数模板返回

```cpp
less_unique_ptr<T, D>::operator()>(x.get(), nullptr_t);
```

第二个函数模板返回

```cpp
less_unique_ptr<T, D>::operator()>(nullptr_t, x.get())
```

```cpp
template<class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

返回：第一个函数模板返回 `nullptr < x`。第二个函数模板返回 `x < (x)`。

```cpp
template<class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

返回：第一个函数模板返回 `!(x < x)`。第二个函数模板返回 `!(nullptr < x)`。

```cpp
template<class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

```cpp
,<class T,
 D,
___const unique_ptr<T,,>& x,
```

```cpp
template<class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);

requires three_way_comparable_with<typename unique_ptr<T, D>::pointer, nullptr_t>
compare_way_result_t<typename unique_ptr<T, D>::pointer, nullptr_t>
operator=(const unique_ptr<T, D>& x, nullptr_t);
```

返回：第一个函数模板返回 `!(x < nullptr)`。第二个函数模板返回 `(nullptr < x)`。

# 20.11.7 I/O

```cpp
template<class E, class T, class Y, class D>
basic_ostream<E, T, Y, D>
```

通过通过 获取的指针。

# ISO/IEC 14882:2020(E)

如果 `T` 不是数组类型，则通过 `p` 启用 `shared_from_this`。如果抛出异常，当 `T` 不是数组类型时调用 `delete`，否则调用 `delete[] p`。

后置条件：`use_count() == 1 && get() == p`。

抛出：`bad_alloc`，或当无法获取超出内存的资源时由实现定义的异常。
