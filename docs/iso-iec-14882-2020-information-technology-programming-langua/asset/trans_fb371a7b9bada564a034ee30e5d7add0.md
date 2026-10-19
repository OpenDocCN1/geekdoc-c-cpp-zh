

# ISO/IEC 14882:2020(E)

```
constexpr chrono::day day() const noexcept;
```

返回：d_。

```
constexpr bool ok() const noexcept;
```

返回：如果 m_.ok() 为 true，且 1d <= d_，并且 d_ 小于或等于月份 m_ 中的天数，则返回 true；否则返回 false。当 m_ == February 时，天数被视为 29。

# 27.8.9.3 非成员函数 [time.cal.md.nonmembers]

```
constexpr bool operator==(const month_day& x, const month_day& y) noexcept;
```

返回：x.month() == y.month() && x.day() == y.day()。

```
constexpr strong_ordering operator<=>(const month_day& x, const month_day& y) noexcept;
```

效果：等价于：
if (auto c = x.month() <=> y.month(); c != 0) return c;
return x.day() <=> y.day();

```
template<class charT, class traits>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os, const month_day& md);
```

效果：等价于：
return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{}/{}"),
md.month(), md.day());

```
template<class charT, class traits, class Alloc = allocator<charT>>
basic_istream<charT, traits>&
from_stream(basic_istream<charT, traits>& is, const charT* fmt,
month_day& md, basic_string<charT, traits, Alloc>* abbrev = nullptr,
minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 给出的格式标志，将输入流 is 解析为 month_day md。如果解析失败无法解码有效的 month_day，则调用 is.setstate(ios_base::failbit) 且 md 不会被修改。如果使用了 %Z 且成功解析，该值将被赋给 *abbrev（如果 abbrev 非空）。如果使用了 %z（或其修改变体）且成功解析，该值将被赋给 *offset（如果 offset 非空）。

返回：is。

# 27.8.10 类 month_day_last [time.cal.mdlast]

```
namespace std::chrono {
class month_day_last {
chrono::month m_; // exposition only
public:
constexpr explicit month_day_last(const chrono::month& m) noexcept;
constexpr chrono::month month() const noexcept;
constexpr bool ok() const noexcept;
};
}
```

1 month_day_last 表示一个月的最后一天。

2 [注 1：month_day_last 对象可以使用表达式 m/last 或 last/m 构造，其中 m 是类型为 month 的表达式。——注结束]

[示例 1：
constexpr auto mdl = February/last; // mdl 是尚未指定年份的二月的最后一天
static_assert(mdl.month() == February);
——示例结束]

3 month_day_last 是一个可 trivial 复制且标准布局的类类型。

# 27.8.11.3 非成员函数 [time.cal.mwd.nonmembers]

```
constexpr bool operator==(const month_weekday& x, const month_weekday& y) noexcept;
```

返回：x.month() == y.month() && x.weekday_indexed() == y.weekday_indexed()。

```
template<class charT, class traits>
    basic_ostream<charT, traits>&
    operator<<(basic_ostream<charT, traits>& os, const month_weekday& mwd);
```

效果：等价于：

```
return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{}/{}"),
    mwd.month(), mwd.weekday_indexed());
```

# 27.8.12 类 month_weekday_last [time.cal.mwdlast]

# 27.8.12.1 概述 [time.cal.mwdlast.overview]

```
namespace std::chrono {
  class month_weekday_last {
    chrono::month m_; // exposition only
    chrono::weekday_last wdl_; // exposition only
  public:
    constexpr month_weekday_last(const chrono::month& m,
        const chrono::weekday_last& wdl) noexcept;
    constexpr chrono::month month() const noexcept;
    constexpr chrono::weekday_last weekday_last() const noexcept;
    constexpr bool ok() const noexcept;
  };
}
```

1 month_weekday_last 表示尚未指定年份的一个月的最后一个工作日。为此 month_weekday_last 存储一个月份和一个 weekday_last。

2 [示例 1：
constexpr auto mwd
    = February/Tuesday[last]; // mwd 是尚未指定年份的二月的最后一个星期二
static_assert(mwd.month() == February);
static_assert(mwd.weekday_last() == Tuesday[last]);
——示例结束]

3 month_weekday_last 是一个可 trivial 复制且标准布局的类类型。

# 27.8.12.2 成员函数 [time.cal.mwdlast.members]

```
constexpr month_weekday_last(const chrono::month& m,
    const chrono::weekday_last& wdl) noexcept;
```

1 效果：将 m_ 初始化为 m，将 wdl_ 初始化为 wdl。

```
constexpr chrono::month month() const noexcept;
```

2 返回：m_。

```
constexpr chrono::weekday_last weekday_last() const noexcept;
```

3 返回：wdl_。

# 27.8.12.3 非成员函数 [time.cal.mwdlast.nonmembers]

```
constexpr bool operator==(const month_weekday_last& x, const month_weekday_last& y) noexcept;
```

1 返回：x.month() == y.month() && x.weekday_last() == y.weekday_last()。

# 27.8.13.3 非成员函数 [time.cal.ym.nonmembers]

```
constexpr year_month& operator+=(const years& dy) noexcept;
```

效果：*this = *this + dy。

返回：*this。

```
constexpr year_month& operator-=(const years& dy) noexcept;
```

效果：*this = *this - dy。

返回：*this。

```
constexpr bool ok() const noexcept;
```

返回：y_.ok() && m_.ok()。

```
constexpr bool operator==(const year_month& x, const year_month& y) noexcept;
```

返回：x.year() == y.year() && x.month() == y.month()。

```
constexpr strong_ordering operator<=>(const year_month& x, const year_month& y) noexcept;
```

效果：等价于：
if (auto c = x.year() <=> y.year(); c != 0) return c;
return x.month() <=> y.month();

```
constexpr year_month operator+(const year_month& ym, const months& dm) noexcept;
```

约束：如果调用者为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

返回：一个 year_month 值 z，使得 z.ok() && z - ym == dm 为 true。

复杂度：相对于 dm 的值，O(1)。

```
constexpr year_month operator+(const months& dm, const year_month& ym) noexcept;
```

约束：如果调用者为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

返回：ym + dm。

```
constexpr year_month operator-(const year_month& ym, const months& dm) noexcept;
```

约束：如果调用者为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

返回：ym + -dm。

# ISO/IEC 14882:2020(E)

```
return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{}/{}"), ym.year(), ym.month());
```

```
template<class charT, class traits, class Alloc = allocator<charT>>
basic_istream<charT, traits>&
from_stream(basic_istream<charT, traits>& is, const charT* fmt,
    year_month& ym, basic_string<charT, traits, Alloc>* abbrev = nullptr,
    minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 给出的格式标志，将输入流 is 解析为 year_month ym。如果解析失败无法解码有效的 year_month，则调用 is.setstate(ios_base::failbit) 且 ym 不会被修改。如果使用了 %Z 且成功解析，该值将被赋给 *abbrev（如果 abbrev 非空）。如果使用了 %z（或其修改变体）且成功解析，该值将被赋给 *offset（如果 offset 非空）。

返回：is。

# 27.8.14 类 year_month_day [time.cal.ymd]

# 27.8.14.1 概述 [time.cal.ymd.overview]

```
namespace std::chrono {
  class year_month_day {
    chrono::year y_;      // exposition only
    chrono::month m_;     // exposition only
    chrono::day d_;       // exposition only

  public:
    year_month_day() = default;
    constexpr year_month_day(const chrono::year& y, const chrono::month& m, const chrono::day& d) noexcept;
    constexpr year_month_day(const year_month_day_last& ymdl) noexcept;
    constexpr year_month_day(const sys_days& dp) noexcept;
    constexpr explicit year_month_day(const local_days& dp) noexcept;

    constexpr year_month_day& operator+=(const months& m) noexcept;
    constexpr year_month_day& operator-=(const months& m) noexcept;
    constexpr year_month_day& operator+=(const years& y) noexcept;
    constexpr year_month_day& operator-=(const years& y) noexcept;

    constexpr chrono::year year() const noexcept;
    constexpr chrono::month month() const noexcept;
    constexpr chrono::day day() const noexcept;

    constexpr operator sys_days() const noexcept;
    constexpr explicit operator local_days() const noexcept;
    constexpr bool ok() const noexcept;
  };
}
```

1 year_month_day 表示特定的年份、月份和日期。year_month_day 是一个基于字段的时间点，分辨率为天。

[注 1：year_month_day 支持基于年份和月份的算术运算，但不支持基于日的算术运算。对于后者，有一个转换为 sys_days 的转换，可高效支持基于日的算术运算。——注结束]

year_month_day 满足 Cpp17EqualityComparable（表 25）和 Cpp17LessThanComparable（表 26）要求。

2 year_month_day 是一个可 trivial 复制且标准布局的类类型。

# 27.8.14.2 成员函数 [time.cal.ymd.members]

```
constexpr year_month_day(const chrono::year& y, const chrono::month& m, const chrono::day& d) noexcept;
```

1 效果：将 y_ 初始化为 y，将 m_ 初始化为 m，将 d_ 初始化为 d。

