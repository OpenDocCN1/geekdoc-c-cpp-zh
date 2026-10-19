

## 27.5.5 特殊值 [time.duration.special]

```
constexpr duration& operator++();
    Effects: Equivalent to: ++rep_.
    Returns: *this.
```

```
constexpr duration operator++(int);
    Effects: Equivalent to: return duration(rep_++);
```

```
constexpr duration& operator--();
    Effects: Equivalent to: --rep_.
    Returns: *this.
```

```
constexpr duration operator--(int);
    Effects: Equivalent to: return duration(rep_--);
```

```
constexpr duration& operator+=(const duration& d);
    Effects: Equivalent to: rep_ += d.count().
    Returns: *this.
```

```
constexpr duration& operator-=(const duration& d);
    Effects: Equivalent to: rep_ -= d.count().
    Returns: *this.
```

```
constexpr duration& operator*=(const rep& rhs);
    Effects: Equivalent to: rep_ *= rhs.
    Returns: *this.
```

```
constexpr duration& operator/=(const rep& rhs);
    Effects: Equivalent to: rep_ /= rhs.
    Returns: *this.
```

```
constexpr duration& operator%=(const rep& rhs);
    Effects: Equivalent to: rep_ %= rhs.
    Returns: *this.
```

```
constexpr duration& operator%=(const duration& rhs);
    Effects: Equivalent to: rep_ %= rhs.count().
    Returns: *this.
```

```
static constexpr duration zero() noexcept;
    Returns: duration(duration_values<rep>::zero()).
```

```
static constexpr duration min() noexcept;
    Returns: duration(duration_values<rep>::min()).
```

```
static constexpr duration max() noexcept;
    Returns: duration(duration_values<rep>::max()).
```

## 27.5.6 非成员算术 [time.duration.nonmember]

1 在以下函数描述中，除非另有说明，CD 表示函数的返回类型。

## 27.5.7 比较 [time.duration.comparisons]

1 在以下函数描述中，CT 表示 common_type_t<A, B>，其中 A 和 B 是函数两个参数的类型。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr common_type_t<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator+(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs);
```

2 返回：CD(CD(lhs).count() + CD(rhs).count())。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr common_type_t<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator-(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs);
```

3 返回：CD(CD(lhs).count() - CD(rhs).count())。

```
template<class Rep1, class Period, class Rep2>
constexpr duration<common_type_t<Rep1, Rep2>, Period>
operator*(const duration<Rep1, Period>& d, const Rep2& s);
```

4 约束：is_convertible_v<const Rep2&, common_type_t<Rep1, Rep2>> 为 true。

5 返回：CD(CD(d).count() * s)。

```
template<class Rep1, class Rep2, class Period>
constexpr duration<common_type_t<Rep1, Rep2>, Period>
operator*(const Rep1& s, const duration<Rep2, Period>& d);
```

6 约束：is_convertible_v<const Rep1&, common_type_t<Rep1, Rep2>> 为 true。

7 返回：d * s。

```
template<class Rep1, class Period, class Rep2>
constexpr duration<common_type_t<Rep1, Rep2>, Period>
operator/(const duration<Rep1, Period>& d, const Rep2& s);
```

8 约束：is_convertible_v<const Rep2&, common_type_t<Rep1, Rep2>> 为 true 且 Rep2 不是 duration 的特化。

9 返回：CD(CD(d).count() / s)。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr common_type_t<Rep1, Rep2>
operator/(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs);
```

10 设 CD 为 common_type_t<duration<Rep1, Period1>, duration<Rep2, Period2>>。

11 返回：CD(lhs).count() / CD(rhs).count()。

```
template<class Rep1, class Period, class Rep2>
constexpr duration<common_type_t<Rep1, Rep2>, Period>
operator%(const duration<Rep1, Period>& d, const Rep2& s);
```

12 约束：is_convertible_v<const Rep2&, common_type_t<Rep1, Rep2>> 为 true 且 Rep2 不是 duration 的特化。

13 返回：CD(CD(d).count() % s)。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr common_type_t<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator%(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs);
```

14 返回：CD(CD(lhs).count() % CD(rhs).count())。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator==(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs);
```

2 返回：CT(lhs).count() == CT(rhs).count()。

## 27.5.8 转换 [time.duration.cast]

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator<(const duration<Rep1, Period1>& lhs,
    const duration<Rep2, Period2>& rhs);
```

返回：CT(lhs).count() < CT(rhs).count()。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator>(const duration<Rep1, Period1>& lhs,
    const duration<Rep2, Period2>& rhs);
```

返回：rhs < lhs。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator<=(const duration<Rep1, Period1>& lhs,
    const duration<Rep2, Period2>& rhs);
```

返回：!(rhs < lhs)。

```
template<class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator>=(const duration<Rep1, Period1>& lhs,
    const duration<Rep2, Period2>& rhs);
```

返回：!(lhs < rhs)。

```
template<class Rep1, class Period1, class Rep2, class Period2>
requires three_way_comparable<typename CT::rep>
constexpr auto operator<=>(const duration<Rep1, Period1>& lhs,
    const duration<Rep2, Period2>& rhs);
```

返回：CT(lhs).count() <=> CT(rhs).count()。

```
template<class ToDuration, class Rep, class Period>
constexpr ToDuration duration_cast(const duration<Rep, Period>& d);
```

约束：ToDuration 是 duration 的特化。

返回：设 CF 为 ratio_divide<Period, typename ToDuration::period>，CR 为 common_type<typename ToDuration::rep, Rep, intmax_t>::type。

- 如果 CF::num == 1 且 CF::den == 1，则返回
  ToDuration(static_cast<typename ToDuration::rep>(d.count()))
- 否则，如果 CF::num != 1 且 CF::den == 1，则返回
  ToDuration(static_cast<typename ToDuration::rep>(static_cast<CR>(d.count()) * static_cast<CR>(CF::num)))
- 否则，如果 CF::num == 1 且 CF::den != 1，则返回
  ToDuration(static_cast<typename ToDuration::rep>(static_cast<CR>(d.count()) / static_cast<CR>(CF::den)))
- 否则，返回
  ToDuration(static_cast<typename ToDuration::rep>(static_cast<CR>(d.count()) * static_cast<CR>(CF::num) / static_cast<CR>(CF::den)))

> [注 1：此函数不使用任何隐式转换；所有转换均使用 static_cast 执行。它在编译时已知一个或多个参数为 1 时避免乘法和除法。中间计算在最宽的表示中进行，仅在最后一步转换为目标表示。——注结束]

```
template<class ToDuration, class Rep, class Period>
constexpr ToDuration floor(const duration<Rep, Period>& d);
```

约束：ToDuration 是 duration 的特化。

返回：在 ToDuration 中可表示的最大结果 t，使得 t <= d。

```
template<class ToDuration, class Rep, class Period>
constexpr ToDuration ceil(const duration<Rep, Period>& d);
```

约束：ToDuration 是 duration 的特化。

## ISO/IEC 14882:2020(E)

返回：在 ToDuration 中可表示的最小结果 t，使得 t >= d。

```
template<class ToDuration, class Rep, class Period>
constexpr ToDuration round(const duration<Rep, Period>& d);
```

约束：ToDuration 是 duration 的特化且 treat_as_floating_point_v<typename ToDuration::rep> 为 false。

返回：最接近 d 的 ToDuration 值。如果有两个最接近的值，则返回满足 t % 2 == 0 的值 t。

## 27.5.9 时长文字后缀 [time.duration.literals]

1 本小节描述用于构造时长文字的字面量后缀。后缀 h、min、s、ms、us、ns 分别表示 hours、minutes、seconds、milliseconds、microseconds 和 nanoseconds 对应的时长值类型，如果它们应用于整数字面量。

2 如果这些后缀中的任何一个应用于浮点字面量，结果是具有未指定浮点表示的 chrono::duration 字面量。

3 如果这些后缀中的任何一个应用于整数字面量且 resulting chrono::duration 值因溢出而无法在结果类型中表示，则程序格式错误。

> [示例 1：以下代码展示了一些时长字面量。
> using namespace std::chrono_literals;
> auto constexpr aday=24h;
> auto constexpr lesson=45min;
> auto constexpr halfanhour=0.5h;
> —— 示例结束]

```
constexpr chrono::hours operator""h(unsigned long long hours);
constexpr chrono::duration<unspecified, ratio<3600, 1>> operator""h(long double hours);
```

返回：表示 hours 小时的时长字面量。

```
constexpr chrono::minutes operator""min(unsigned long long minutes);
constexpr chrono::duration<unspecified, ratio<60, 1>> operator""min(long double minutes);
```

返回：表示 minutes 分钟的时长字面量。

## 27.5.10 算法 [time.duration.alg]

```
template<class Rep, class Period>
constexpr duration<Rep, Period> abs(duration<Rep, Period> d);
```

约束：numeric_limits<Rep>::is_signed 为 true。

返回：如果 d >= d.zero()，返回 d，否则返回 -d。

