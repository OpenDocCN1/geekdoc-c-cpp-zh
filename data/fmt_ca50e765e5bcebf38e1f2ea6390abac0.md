
# ISO/IEC 14882:2020(E)

```cpp
template<class ExecutionPolicy, class InputIterator, class NoThrowForwardIterator>
NoThrowForwardIterator uninitialized_move(ExecutionPolicy&& exec, // sec 25.9.5
    InputIterator first, InputIterator last,
    NoThrowForwardIterator result);
```

```cpp
template<class InputIterator, class Size, class NoThrowForwardIterator>
pair<InputIterator, NoThrowForwardIterator>
uninitialized_move_n(InputIterator first, Size n, NoThrowForwardIterator result);
```

```cpp
template<class ExecutionPolicy, class InputIterator, class Size, class NoThrowForwardIterator>
pair<InputIterator, NoThrowForwardIterator>
uninitialized_move_n(ExecutionPolicy&& exec, // sec 25.9.5
    InputIterator first, Size n, NoThrowForwardIterator result);
```

```cpp
namespace ranges {
template<class I, class D>
    using uninitialized_move_result = in_out_result<I, D>;

template<class InputIterator I, sentinel S1>
    no-throw-forward-iterator<I>, no-throw-sentinel<S1>
    requires constructible_from<value_t<I>, rvalue_reference<T>>
    uninitialized_move_result<I>;
    uninitialized_move(I first, S1 last, Output ofst);

template<class InputIterator I, range R>
    no-throw-forward-iterator<I>
    requires constructible_from<value_t<R>, rvalue_reference<T>>
    uninitialized_move_result<I>;
    uninitialized_move_n(I&& first, R&& range, Output out);
}
```

```cpp
template<class I, class D>
    using uninitialized_move_result = in_out_result<I, D>;

template<class InputIterator I, sentinel S>
    no-throw-forward-iterator<I>, no-throw-sentinel<S>
    requires constructible_from<value_t<I>, rvalue_reference<T>>
    uninitialized_move_result<I>;
    uninitialized_move_n(I first, S last, Output ofst);
```

```cpp
template<class NoThrowForwardIterator, class T>
    uninitialized_fill(NoThrowForwardIterator first, NoThrowForwardIterator last,
        const T& x);

template<class ExecutionPolicy, class T> // sec 25.9.5
    uninitialized_fill(ExecutionPolicy&& exec, NoThrowForwardIterator first,
        const T& x);
```

```cpp
template<class NoThrowForwardIterator, class Size, class T>
    uninitialized_fill_n(NoThrowForwardIterator first, Size n, const T& x);

template<class ExecutionPolicy, class Size, class T>
    uninitialized_fill_n(ExecutionPolicy&& exec, Size n, const T& x); // sec 25.9.5
```

```cpp
namespace ranges {
template<class I, class S>
    no-throw-sentinel<I>, class T
    requires constructible_from<value_t<I>, const T&>
    uninitialized_fill(I first, S last, const T& x);

template<class R>
    no-throw-forward_range R, class T
    requires constructible_from<value_t<R>, const T&>
    borrowed_iterator<T> uninitialized_fill(R&& range, const T& x);
}
```

# ISO/IEC 14882:2020(E)

```cpp
// 25.11.8. construct_at
template<class T, class... Args>
constexpr T* construct_at(T* location, Args&&... args);

namespace ranges {
    template<class T, class... Args>
    constexpr T* construct_at(T* location, Args&&... args);
}
```

```cpp
// 25.11.9. destroy
template<class T>
constexpr void destroy_at(T* location);

template<NoThrowForwardIterator>
constexpr void destroy(NoThrowForwardIterator first, NoThrowForwardIterator last);

template<ExecutionPolicy, NoThrowForwardIterator>
void destroy(ExecutionPolicy&& exec); // see 25.5.3

template<NoThrowForwardIterator, Size>
constexpr void destroy_n(NoThrowForwardIterator first, Size n);

template<ExecutionPolicy, NoThrowForwardIterator>
void destroy_n(ExecutionPolicy&& exec); // see 25.5.3
```

```cpp
namespace ranges {
    template<destructible T>
    constexpr void destroy_at(T* location);

    template<no_throw_iterator<I>, no_throw_sentinel<S>>
    requires destructible<value_t<I>>
    void destroy(I first, S last);

    template<range R>
    requires destructible<value_t<R>>
    void destroy_n(R&& range, size_t n);
}
```

```cpp
// 25.11.10. class unique_ptr
template<class T> struct default_delete;
template<class T> struct default_delete<T[]>;

template<class T, class D = default_delete<T>> class unique_ptr;
template<class T, class D> class unique_ptr<T[], D>;

template<class T, class... Args>
unique_ptr<T> make_unique(Args&&...); // T is not array

template<class T>
unique_ptr<T> make_unique(size_t n); // T is array

template<class T, class... Args>
unique_ptr<T> make_unique(Args&&...) = delete; // T is array

template<class T>
unique_ptr<T> make_unique_overwrite(); // T is not array

template<class T>
unique_ptr<T> make_unique_overwrite(size_t n); // T is array

template<class T, class... Args>
unique_ptr<T> make_unique_overwrite(Args&&...) = delete; // T is array

template<class T, class D>
void swap(unique_ptr<T, D>& x, unique_ptr<T, D>& y) noexcept;

template<class T1, class D1, class T2, class D2>
bool operator==(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);
```

# ISO/IEC 14882:2020(E)

```cpp
template<class T1, class D1, class T2, class D2>
bool operator<(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

template<class T1, class D1, class T2, class D2>
bool operator>(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

template<class T1, class D1, class T2, class D2>
bool operator<=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

template<class T1, class D1, class T2, class D2>
bool operator>=(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

requires three_comparable_with<typename unique_ptr<T1, D1>::pointer,
    compare_three_way_result<typename unique_ptr<T1, D1>::pointer,
    typename unique_ptr<T2, D2>::pointer>
operator<>(const unique_ptr<T1, D1>& x, const unique_ptr<T2, D2>& y);

template<class T, class D>
bool operator==(unique_ptr<T, D>& x, nullptr_t) noexcept;

template<class T, class D>
bool operator>(unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator<=(unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator>=(unique_ptr<T, D>& x, nullptr_t);

template<class T, class D>
bool operator==(nullptr_t, unique_ptr<T, D>& y);

template<class T, class D>
bool operator>>(nullptr_t, unique_ptr<T, D>& y);

template<class T, class D>
bool operator<=(nullptr_t, unique_ptr<T, D>& y);

template<class T, class D>
bool operator>=(nullptr_t, unique_ptr<T, D>& y);

requires three_comparable_with<typename unique_ptr<T, D>::pointer, nullptr_t>
operator<>(unique_ptr<T, D>& x, nullptr_t);

template<class E, class T, class D, class Y>
basic_ostream<E>& operator<<=(basic_ostream<E>& os, const unique_ptr<Y, D>& y);
```

```cpp
// 20.11.2. bad_weak_ptr
class bad_weak_ptr;

// 20.11.3. template shared_ptr
template<class T> class shared_ptr;

// 20.11.7. shared_ptr creation
template<class T, class... Args>
shared_ptr<T> make_shared(Args&&... args);

template<class T, class A, class... Args>
shared_ptr<T> allocate_shared(const A& a, Args&&... args);

template<class T>
shared_ptr<T> make_shared(size_t N);

template<class T, class A>
shared_ptr<T> allocate_shared(const A& a);
```

```cpp
// 20.11.4,weak_ptr specialized algorithms
template<class T> void swap(weak_ptr<T>& a, weak_ptr<T>& b) noexcept;
```

```cpp
// 20.11.5, class template owner_less
template<class T = void> struct owner_less;
```

```cpp
// 20.11.6, class template enable_shared_from_this
template<class T> class enable_shared_from_this;
```

```cpp
// 20.11.7, hash support
template<class T, class D> struct hash<unique_ptr<T, D>>;
template<class T> struct hash<shared_ptr<T>>;
```

```cpp
// 31.8.7, atomic smart pointers
template<class T> struct atomic;
template<class T> struct atomic<shared_ptr<T>>;
template<class T> struct atomic<weak_ptr<T>>;
```

# 20.10.3 Pointer_traits

[pointer.traits]

## 20.10.3.1 General

[pointer.traits.general]

- 1 类 `pointer_traits` 使用一个统一的接口来包含指针类类型的属性。
