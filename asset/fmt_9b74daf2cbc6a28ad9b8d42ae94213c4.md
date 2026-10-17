
```cpp
namespace ranges {
template<input_iterator I, no-throw-forward-iterator S, no-throw-sentinel<D>
requires_constructible_from<iter_value<D>, iterator_reference<I>>
uninitialized_move_n(I first, difference_t<I> n, O result)
uninitialized_move_n(I first, I n, O result);
}
```

8 前置条件：`[first, last)` 与 `first + [0, n)` 不重叠。

9 影响：等效于：

```cpp
auto t = uninitialized_move(counted_iterator(first, n),
    default_sentinel(first, last));
return (std::move(t.in).base(), out;
```

注意 2：如果抛出异常，范围 `{first + [0, n)` 中的某些对象处于有效但未定义状态。

## 25.11.7 uninitialized_fill

```cpp
template<class NoThrowForwardIterator, class T>
void uninitialized_fill(NoThrowForwardIterator first, const T& x);
```

影响：等效于：

```cpp
for (; first != last; ++first)
    new (void(*)(first)) (*first)
    typename iterator_traits<NoThrowForwardIterator>::value_type(x);
```

```cpp
namespace ranges {
template<class no-forward-iterator I, no-throw-sentinel<I> S, class T>
    requires constructible<T, value_t<I>, const T&>
    uninitialized_fill(I first, S last, const T& x);
template<class no-forward-range R, class T>
    requires constructible<T, value_t<R>, const T&>
    borrowed_iterator<T> uninitialized_fill(R&& r, const T& x);
}
}
```

影响：等效于：

```cpp
for (; first != last; ++first)
    new (void(*)(first)) remove_reference_t<I>(x)
return first;
```

```cpp
template<class NoThrowForwardIterator, class Size, class T>
NoThrowForwardIterator uninitialized_fill(NoThrowForwardIterator first, Size n, const T& x);
```

影响：等效于：

```cpp
for (; n; --n)
    new (void(*)(first))
    typename iterator_traits<NoThrowForwardIterator>::value_type(x);
return first;
```

```cpp
影响：等效于：
```cpp

return uninitialized_fill(counted_iterator(first, n), default_sentinel, x).base();

```
```

```cpp

namespace ranges {

template<destructible T>

constexpr destroy_at(T* location) noexcept;

}

```

+ 效果：
- T 是数组类型，等于 `destroy(begin(*location), end(*location))`。
- 否则，等于 `location->T()`。

```cpp

template<class NoThrowForwardIterator>

constexpr destroy(NoThrowForwardIterator first, NoThrowForwardIterator last);

```

效果：等于：
for (; first != last; ++first) {
    destroy(addressoof(first));
}

```cpp

namespace ranges {

template<no-throw-input-iterator I, no-throw-sentinel<I> S>

requires destructible<std::iter_value_t<I>>

constexpr destroy(I first, S last) noexcept;

template<no-throw-input-range R>

requires destructible<ranges::range_value_t<R>>

constexpr destroy(ranges::borrowed_iterator<R> first, R::sentinel r) noexcept;

}

```

效果：等于：
for (; first != last; ++first) {
    destroy(addressoof(first));
}
return first;

```cpp

template<class NoThrowForwardIterator, class Size>

constexpr destroy(NoThrowForwardIterator first, Size n);

```

效果：等于：
for (int i = 0; i < n; ++i) {
    destroy(addressoof(first));
}
return first;

```cpp

namespace ranges {

template<no-throw-input-iterator I>

requires destructible<std::iter_value_t<I>>

constexpr destroy(I first, iter_difference_t<I> n) noexcept;

}

```

效果：等于：
return destroy(counted_iterator(first, n), default_sentinel).base();

# 25.2 C 标准库算法

[alg.c.library]

> [注：`<cstdlib>` (17.2) 定义了本小节描述的函数。-- 注结束]

```cpp

void* search(const void* key, const void* base, size_t nmemb, size_t tsize, compare_ptr* compare);

void* bsearch(const void* key, const void* base, size_t nmemb, size_t tsize, compare_ptr* compare);

void* qsort(void* base, size_t nmemb, size_t tsize, compare_ptr* compare);

```

效果：这些函数与 C 标准库具有相同的语义。
前置条件：由 `base` 指向的数组为平凡类型（trivial type）。

抛出：由 `compar` (16.4.6.13) 抛出的任何异常。

参见：ISO C 7.22.5。

# ISO/IEC 14882:2020(E)

# 26 数学库 [numerics]

# 26.1 通用 [numerics.general]

+ 1 本节描述了 C++ 程序可能用于执行同义操作的组件。
2 以下子子句描述了用于复数类型、随机数生成、数值（n-at-a）数组、广义数值算法，以及浮点类型数学常数和函数的组件，如表 92 所示。

表 92：数学库摘要
| 子子句 | 头文件 |
|---|---|
| 26.2 要求 | <cfenv> |
| 26.3 浮点数环境 | |
| 26.4 复数 | <complex> |
| 26.5 位操作 | <bit> |
| 26.6 随机数生成 | <random> |
| 26.7 数值数组 | <valarray> |
| 26.8 浮点数类型的数学函数 | <cmath>, <cstdlib> |
| 26.9 数字 | <numbers> |

# 26.2 数值类型要求 [numerics.requirements]

+ 1 复数和 `valarray` 组件由它们包含和处理的信息的类型进行参数化。C++ 程序应仅使用数值类型实例化这些组件。数值类型是满足 `Cpp17DefaultConstructible`、`Cpp17CopyAssignable` 和 `Cpp17CopyConstructible` 要求的 cv 未限定类型 T (16.4.4.2)。
2 如果对 T 的任何操作抛出异常，则效果未定义。
3 此外，只有当 T 符合每个成员或关系指定的额外要求时，`valarray<>` 的许多成员和相关函数才能成功实例化并表现出定义的行为。

+ 4 [示例 1：实例化 `valarray<complex>` 是有效的，但 `valarray<complex>operator()` 无法实例化，因为复数没有任何重载运算符。示例结束]

# 26.3 浮点数环境 [cfenv]

# 26.3.1 头文件 <cfenv> 概要 [cfenv.syn]

```cpp

# FE_ALL_EXCEPT 见下文

# FE_DIVBYZERO 见下文 // 可

# FE_INEXACT 见下文 // 可

# FE_INVALID 见下文 // 可

# FE_OVERFLOW 见下文 // 可

# FE_UNDERFLOW 见下文 // 可

# FE_DOWNOWARD 见下文 // 可

# FE_TONAREST 见下文 // 可

# FE_TOWARDZERO 见下文 // 可

# FE_UPWARD 见下文 // 可

# FE_DFL_ENV 见下文

```

> 246 换句话说，值类型。这些包括算术类型、指针、更大的复数类以及数值类型的 `valarray` 实例化。

```cpp

namespace std {

  // 类型

  using fenv_t = 对象类型;

  using fcept_t = 整数类型;

  // 函数

  int feclecept(int except);

  int fegetexceptflag(fcept_t* plag, int except);

  int feraiseffect(fcept_t* int except);

  int fetexcept(const fcept_t* plag, int except);

  int fetetexcept(int except);

  int festground();

  int festround(int node);

  int fengetenv(fenv_t* penv);

  int feholdexceptenv(fenv_t* penv);

  int fenestenv(const fenv_t* penv);

}

```

# ISO/IEC 14882:2020(E)

## 26.4.3 类模板 complex

```cpp

namespace std {

template<class T> class complex {

public:

    using value_type = T;

    constexpr complex(const T& re = T(), const T& im = T());

    constexpr complex(const complex<T>&);

    template<class X> complex(const complex<X>&);

    constexpr T real() const;

    void real(T& re);

    constexpr T imag() const;

    void imag(T& im);

    constexpr complex& operator=(const T&);

    constexpr complex& operator+=(const T&);

    constexpr complex& operator*=(const T&);

    constexpr complex& operator**=(const T&);

    constexpr complex& operator/(const complex<T>&);

template<class X> constexpr complex& operator=(const complex<X>&);

template<class X> constexpr complex& operator+=(const complex<X>&);

template<class X> constexpr complex& operator-=(const complex<X>&);

template<class X> constexpr complex& operator*=(const complex<X>&);

template<class X> constexpr complex& operator/=(const complex<X>&);

};

```

`complex` 类描述了一个存储复数的笛卡尔分量 `real()` 和 `imag()` 的对象。

## 26.4.4 特殊化

```cpp

namespace std {

template<> class complex<float> {

public:

    using value_type = float;

constexpr complex(float re = 0.0f, float im = 0.0f);

constexpr complex(const complex<float>& k) = default;

constexpr explicit complex(const complex<double>& k);

constexpr explicit complex(const complex<long double>& k);

constexpr float real() const;

constexpr void real(float);

constexpr float imag() const;

constexpr void imag(float);

constexpr complex& operator=(float);

constexpr complex& operator+=(float);

constexpr complex& operator-=(float);

constexpr complex& operator*=(float);

constexpr complex& operator/(float);

constexpr complex& operator=(const complex<X>);

template<class X> constexpr complex& operator+=(const complex<X>);

template<class X> constexpr complex& operator-=(const complex<X>);

template<class X> constexpr complex& operator*=(const complex<X>);

template<class X> constexpr complex& operator/=(const complex<X>);
