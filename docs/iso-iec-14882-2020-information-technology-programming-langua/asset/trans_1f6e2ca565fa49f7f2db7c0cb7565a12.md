

## ISO/IEC 14882:2020(E)

```
constexpr year_month_day(const year_month_day_last& ymdl) noexcept;
```

Effects: 初始化 y_ 为 ymdl.year()，m_ 为 ymdl.month()，d_ 为 ymdl.day()。

> [Note 1: 从 year_month_day_last 到 year_month_day 的此转换可能比将 year_month_day_last 转换为 sys_days，然后再将该 sys_days 转换为 year_month_day 更高效。 — end note]

```
constexpr year_month_day(const sys_days& dp) noexcept;
```

Effects: 构造一个与 dp 表示的日期对应的 year_month_day 类型的对象。

Remarks: 对于类型为 year_month_day 且 ymd.ok() 为 true 的任意值 ymd，ymd == year_month_day{sys_days{ymd}} 为 true。

```
constexpr explicit year_month_day(const local_days& dp) noexcept;
```

Effects: 等价于使用 sys_days{dp.time_since_epoch()} 构造。

```
constexpr year_month_day& operator+=(const months& m) noexcept;
```

Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

Effects: *this = *this + m。

Returns: *this。

```
constexpr year_month_day& operator-=(const months& m) noexcept;
```

Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

Effects: *this = *this - m。

Returns: *this。

```
constexpr year_month_day& year_month_day::operator+=(const years& y) noexcept;
```

Effects: *this = *this + y。

Returns: *this。

## 27.8.16 Class year_month_weekday [time.cal.ymwd]

### 27.8.16.1 Overview [time.cal.ymwd.overview]

```
constexpr year_month_day_last
    operator+(const months& dm, const year_month_day_last& ymdl) noexcept;
```

Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

Returns: ymdl + dm。

```
constexpr year_month_day_last
    operator-(const year_month_day_last& ymdl, const months& dm) noexcept;
```

Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

Returns: ymdl + (-dm)。

```
constexpr year_month_day_last
    operator+(const year_month_day_last& ymdl, const years& dy) noexcept;
```

Returns: {ymdl.year()+dy, ymdl.month_day_last()}。

```
template<class charT, class traits>
basic_ostream<charT, traits>&
    operator<<(basic_ostream<charT, traits>& os, const year_month_day_last& ymdl);
```

Effects: 等价于：
    return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{}/{}"),
        ymdl.year(), ymdl.month_day_last());

```
namespace std::chrono {
  class year_month_weekday {
    chrono::year y_;      // exposition only
    chrono::month m_;     // exposition only
    chrono::weekday_indexed wdi_;  // exposition only
    public:
    year_month_weekday() = default;
    constexpr year_month_weekday(const chrono::year& y, const chrono::month& m,
        const chrono::weekday_indexed& wdi) noexcept;
    constexpr year_month_weekday(const sys_days& dp) noexcept;
    constexpr explicit year_month_weekday(const local_days& dp) noexcept;
    constexpr year_month_weekday& operator+=(const months& m) noexcept;
    constexpr year_month_weekday& operator-=(const months& m) noexcept;
    constexpr year_month_weekday& operator+=(const years& y) noexcept;
    constexpr year_month_weekday& operator-=(const years& y) noexcept;
    constexpr chrono::year year() const noexcept;
    constexpr chrono::month month() const noexcept;
    constexpr chrono::weekday weekday() const noexcept;
    constexpr unsigned index() const noexcept;
    constexpr chrono::weekday_indexed weekday_indexed() const noexcept;
```

### 27.8.16.2 Member functions [time.cal.ymwd.members]

```
constexpr operator sys_days() const noexcept;
constexpr explicit operator local_days() const noexcept;
constexpr bool ok() const noexcept;
};
}
```

1 year_month_weekday 表示特定的年份、月份和月份中的第 n 个星期几。year_month_weekday 是一个基于字段的时间点，分辨率为天。

> [Note 1: year_month_weekday 支持以年和月为导向的算术运算，但不支持以日为导向的算术运算。对于后者，有一个转换为 sys_days 的转换，可高效支持以日为导向的算术运算。 — end note]

year_month_weekday 满足 Cpp17EqualityComparable（表 25）的要求。

2 year_month_weekday 是一个可 trivial 复制且标准布局的类类型。

```
constexpr year_month_weekday(const chrono::year& y, const chrono::month& m, const chrono::weekday_indexed& wdi) noexcept;
```

1 Effects: 初始化 y_ 为 y，m_ 为 m，wdi_ 为 wdi。

```
constexpr year_month_weekday(const sys_days& dp) noexcept;
```

2 Effects: 构造一个与 dp 表示的日期对应的 year_month_weekday 类型的对象。

3 Remarks: 对于类型为 year_month_weekday 且 ymd1.ok() 为 true 的任意值 ymd1，ymd1 == year_month_weekday{sys_days{ymd1}} 为 true。

```
constexpr explicit year_month_weekday(const local_days& dp) noexcept;
```

4 Effects: 等价于使用 sys_days{dp.time_since_epoch()} 构造。

```
constexpr year_month_weekday& operator+=(const months& m) noexcept;
```

5 Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

6 Effects: *this = *this + m。

7 Returns: *this。

```
constexpr year_month_weekday& operator-=(const months& m) noexcept;
```

8 Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

9 Effects: *this = *this - m。

### 27.8.16.3 Non-member functions [time.cal.ymwd.nonmembers]

```
constexpr unsigned index() const noexcept;
```

Returns: 返回 wdi_.index()。

```
constexpr chrono::weekday_indexed weekday_indexed() const noexcept;
```

Returns: 返回 wdi_。

```
constexpr operator sys_days() const noexcept;
```

Returns: 如果 y_.ok() && m_.ok() && wdi_.weekday().ok()，返回一个表示 year()/month() 的第一个 weekday() 之后 (index() - 1) * 7 天的 sys_days。如果 index() 为 0，则返回的 sys_days 表示 year()/month() 的第一个 weekday() 之前的 7 天。否则返回的值未指定。

```
constexpr explicit operator local_days() const noexcept;
```

Returns: 返回 local_days{sys_days{*this}.time_since_epoch()}。

```
constexpr bool ok() const noexcept;
```

Returns: 如果 y_.ok()、m_.ok() 或 wdi_.ok() 中任意一个为 false，则返回 false。否则，如果 *this 表示一个有效日期，则返回 true。否则返回 false。

```
constexpr bool operator==(const year_month_weekday& x, const year_month_weekday& y) noexcept;
```

Returns:

x.year() == y.year() && x.month() == y.month() && x.weekday_indexed() == y.weekday_indexed()

```
constexpr year_month_weekday operator+(const year_month_weekday& ymwd, const months& dm) noexcept;
```

Constraints: 如果调用方为 months 参数提供的参数可转换为 years，则其到 years 的隐式转换序列比其到 months 的隐式转换序列更差（12.4.4.3）。

Returns: 返回 (ymwd.year() / ymwd.month() + dm) / ymwd.weekday_indexed()。

```
template<class charT, class traits>
 basic_ostream<charT, traits>&
 operator<<(basic_ostream<charT, traits>& os, const year_month_weekday& ymwd);
```

Effects: 等价于：

return os << format(os.getloc(), STATICALLY-WIDEN<charT>("{\}/{}/{}"),
 ymwd.year(), ymwd.month(), ymwd.weekday_indexed());

