

# 27.11.7.3 成员函数 [time.zone.zonedtime.members]

```
zoned_time(TimeZonePtr z, const local_time<Duration>& tp, choose c);
```

效果：等价于使用 {traits::locate_zone(name), tp} 构造。

前提条件：z 引用一个时区。

约束条件：

```
is_convertible_v<decltype(declval<TimeZonePtr&>().to_sys(local_time<Duration>{}, choose::earliest)), sys_time<duration>> is true.
```

效果：使用 std::move(z) 初始化 zone_，并使用 zone_->to_sys(tp, c) 初始化 tp_。

```
zoned_time(string_view name, const local_time<Duration>& tp, choose c);
```

约束条件：zoned_time 可从 traits::locate_zone(name) 的返回类型、local_time<Duration> 和 choose 构造。

效果：等价于使用 {traits::locate_zone(name), tp, c} 构造。

```
template<class Duration2, class TimeZonePtr2>
zoned_time(TimeZonePtr z, const zoned_time<Duration2, TimeZonePtr2>& y);
```

约束条件：is_convertible_v<sys_time<Duration2>, sys_time<Duration>> is true。

前提条件：z 引用一个有效的时区。

效果：使用 std::move(z) 初始化 zone_，并使用 y.tp_ 初始化 tp_。

```
template<class Duration2, class TimeZonePtr2>
zoned_time(TimeZonePtr z, const zoned_time<Duration2, TimeZonePtr2>& y, choose);
```

约束条件：is_convertible_v<sys_time<Duration2>, sys_time<Duration>> is true。

前提条件：z 引用一个有效的时区。

效果：等价于使用 {z, y} 构造。

[注 1：choose 参数无效。 — 结束注]

```
template<class Duration2, class TimeZonePtr2>
zoned_time(string_view name, const zoned_time<Duration2, TimeZonePtr2>& y);
```

约束条件：zoned_time 可从 traits::locate_zone(name) 的返回类型和类型 zoned_time<Duration2, TimeZonePtr2> 构造。

效果：等价于使用 {traits::locate_zone(name), y} 构造。

```
template<class Duration2, class TimeZonePtr2>
zoned_time(string_view name, const zoned_time<Duration2, TimeZonePtr2>& y, choose c);
```

约束条件：zoned_time 可从 traits::locate_zone(name) 的返回类型、类型 zoned_time<Duration2, TimeZonePtr2> 和类型 choose 构造。

效果：等价于使用 {traits::locate_zone(name), y, c} 构造。

[注 2：choose 参数无效。 — 结束注]

```
zoned_time& operator=(const sys_time<Duration>& st);
```

效果：赋值后，get_sys_time() == st。该赋值对 get_time_zone() 的返回值没有影响。

返回：*this。

```
zoned_time& operator=(const local_time<Duration>& lt);
```

效果：赋值后，get_local_time() == lt。该赋值对 get_time_zone() 的返回值没有影响。

返回：*this。

```
1977-01-01 00:00:00: 1s
1978-01-01 00:00:00: 1s
1979-01-01 00:00:00: 1s
1980-01-01 00:00:00: 1s
1981-07-01 00:00:00: 1s
1982-07-01 00:00:00: 1s
1983-07-01 00:00:00: 1s
1985-07-01 00:00:00: 1s
1988-01-01 00:00:00: 1s
1990-01-01 00:00:00: 1s
1991-01-01 00:00:00: 1s
1992-07-01 00:00:00: 1s
1993-07-01 00:00:00: 1s
1994-07-01 00:00:00: 1s
1996-01-01 00:00:00: 1s
1997-07-01 00:00:00: 1s
1999-01-01 00:00:00: 1s
2006-01-01 00:00:00: 1s
2009-01-01 00:00:00: 1s
2012-07-01 00:00:00: 1s
2015-07-01 00:00:00: 1s
2017-01-01 00:00:00: 1s
```

— 结束示例]

# 27.11.8.2 成员函数 [time.zone.leap.members]

```
constexpr sys_seconds date() const noexcept;
```

返回：闰秒被插入的日期和时间。

```
constexpr seconds value() const noexcept;
```

返回：+1s 表示正闰秒，或 -1s 表示负闰秒。

[注 1：截至 2019 年插入的所有闰秒均为正闰秒。 — 结束注]

# 27.11.8.3 非成员函数 [time.zone.leap.nonmembers]

```
constexpr bool operator==(const leap_second& x, const leap_second& y) noexcept;
```

返回：x.date() == y.date()。

```
constexpr strong_ordering operator<=>(const leap_second& x, const leap_second& y) noexcept;
```

返回：x.date() <=> y.date()。

```
template<class Duration>
    constexpr bool operator==(const leap_second& x, const sys_time<Duration>& y) noexcept;
```

返回：x.date() == y。

```
template<class Duration>
    constexpr bool operator<(const leap_second& x, const sys_time<Duration>& y) noexcept;
```

返回：x.date() < y。

```
template<class Duration>
    constexpr bool operator<(const sys_time<Duration>& x, const leap_second& y) noexcept;
```

返回：x < y.date()。

```
template<class Duration>
    constexpr bool operator>(const leap_second& x, const sys_time<Duration>& y) noexcept;
```

返回：y < x。

```
template<class Duration>
    constexpr bool operator>(const sys_time<Duration>& x, const leap_second& y) noexcept;
```

返回：y < x。

# 27.11.9 类 time_zone_link [time.zone.link]

# 27.11.9.1 概述 [time.zone.link.overview]

```
namespace std::chrono {
  class time_zone_link {
  public:
    time_zone_link(time_zone_link&&) = default;
    time_zone_link& operator=(time_zone_link&&) = default;

    // unspecified additional constructors

    string_view name() const noexcept;
    string_view target() const noexcept;
  };
}
```

time_zone_link 指定 time_zone 的替代名称。time_zone_link 在时区数据库初始化时构造。

# 27.11.9.2 成员函数 [time.zone.link.members]

```
string_view name() const noexcept;
```

返回：时区的替代名称。

```
string_view target() const noexcept;
```

返回：此 time_zone_link 提供替代名称的 time_zone 的名称。

# 27.11.9.3 非成员函数 [time.zone.link.nonmembers]

```
bool operator==(const time_zone_link& x, const time_zone_link& y) noexcept;
```

返回：x.name() == y.name()。

```
strong_ordering operator<=>(const time_zone_link& x, const time_zone_link& y) noexcept;
```

返回：x.name() <=> y.name()。

# 27.12 格式化 [time.format]

chrono 库（27.2）中的每个 formatter（20.20.5）特化都满足 Formatter 要求（20.20.5.1）。这些 formatter 的 parse 成员函数将格式规范解释为 chrono-format-spec，语法如下：

```
chrono-format-spec:
  fill-and-alignopt widthopt precisionopt chrono-specsopt
```

```
template<class Duration>
  constexpr bool operator<=(const leap_second& x, const sys_time<Duration>& y) noexcept;
  返回：!(y < x).
```

```
template<class Duration>
  constexpr bool operator<=(const sys_time<Duration>& x, const leap_second& y) noexcept;
  返回：!(y < x).
```

```
template<class Duration>
  constexpr bool operator>=(const leap_second& x, const sys_time<Duration>& y) noexcept;
  返回：!(x < y).
```

```
template<class Duration>
  constexpr bool operator>=(const sys_time<Duration>& x, const leap_second& y) noexcept;
  返回：!(x < y).
```

```
template<class Duration>
  requires three_way_comparable_with<sys_seconds, sys_time<Duration>>
  constexpr auto operator<=>(const leap_second& x, const sys_time<Duration>& y) noexcept;
  返回：x.date() <=> y.
```

解释该标志。格式字符串中除表 100 中表示的字符外的所有字符，除空白外，均从流中按原样解析。空白字符匹配输入流中零个或多个空白字符。

11 如果正在解析的类型无法表示格式标志所指的信息，则调用 is.setstate(ios_base::failbit)。

> [示例 1：duration 无法表示星期几。 — 结束示例]

然而，如果标志指的是“一天中的时间”（例如 %H、%I、%p 等），则 duration 的特化被解析为自午夜起经过的当天时间。

12 如果 from_stream 重载未能解析格式字符串指定的全部内容，或如果解析的信息不足以指定完整的 duration、time point 或历法数据结构，则在 basic_istream 上调用 setstate(ios_base::failbit)。

# 表 100：解析标志的含义 [tab:time.parse.spec]

| 标志 | 解析值 |
|------|--------------|
| %a | 区域设置的完整或缩写不区分大小写的星期几名称。 |
| %A | 等价于 %a。 |
| %b | 区域设置的完整或缩写不区分大小写的月份名称。 |
| %B | 等价于 %b。 |
| %c | 区域设置的日期和时间表示。修改后的命令 %Ec 解释区域设置的替代日期和时间表示。 |
| %C | 以十进制数表示的世纪。修改后的命令 %NC 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。修改后的命令 %EC 解释区域设置的世纪的替代表示。 |
| %d | 以十进制数表示的月份中的天数。修改后的命令 %Nd 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。修改后的命令 %Od 解释区域设置的月份中天数的替代表示。 |
| %D | 等价于 %m/%d/%y。 |
| %e | 等价于 %d 且可像 %d 一样修改。 |
| %F | 等价于 %Y-%m-%d。如果用宽度 N 修改，则宽度仅应用于 %Y。 |
| %g | ISO 星期年制的最后两位十进制数字。修改后的命令 %Ng 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。 |
| %G | 以十进制数表示的 ISO 星期年制年份。修改后的命令 %NG 指定要读取的最大字符数。如果未指定 N，则默认为 4。允许前导零但不是必需的。 |
| %h | 等价于 %b。 |
| %H | 以十进制数表示的小时（24 小时制）。修改后的命令 %NH 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。修改后的命令 %OH 解释区域设置的替代表示。 |
| %I | 以十进制数表示的小时（12 小时制）。修改后的命令 %NI 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。修改后的命令 %OI 解释区域设置的替代表示。 |
| %j | 如果正在解析的类型是 duration 的特化，则为天数的十进制数。否则，为以十进制数表示的年份中的天数。1 月 1 日为 1。在任何情况下，修改后的命令 %Nj 指定要读取的最大字符数。如果未指定 N，则默认为 3。允许前导零但不是必需的。 |
| %m | 以十进制数表示的月份。1 月为 1。修改后的命令 %Nm 指定要读取的最大字符数。如果未指定 N，则默认为 2。允许前导零但不是必需的。修改后的命令 %Om 解释区域设置的替代表示。

