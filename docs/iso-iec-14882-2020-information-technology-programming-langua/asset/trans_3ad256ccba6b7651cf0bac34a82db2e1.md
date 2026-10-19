

```
template<class charT, class traits, class Duration, class Alloc = allocator<charT>>
    basic_istream<charT, traits>&
        from_stream(basic_istream<charT, traits>& is, const charT* fmt,
                    utc_time<Duration>& tp, basic_string<charT, traits, Alloc>* abbrev = nullptr,
                    minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 中给出的格式标志，将输入流 is 解析为 utc_time tp。如果解析未能解码出有效日期，则调用 is.setstate(ios_base::failbit)，并且不修改 tp。如果使用了 %Z 并成功解析，且 abbrev 非空，则该值将被赋给 *abbrev。如果使用了 %z（或其修饰变体）并成功解析，且 offset 非空，则该值将被赋给 *offset。此外，解析出的偏移量将从成功解析的时间戳中减去，然后将该差值赋给 tp。

返回：is。

```
struct leap_second_info {
    bool      is_leap_second;
    seconds elapsed;
};
```

leap_second_info 类型具有上述指定的数据成员和特殊成员。除此之外，它没有其他基类或成员。

```
template<class Duration>
leap_second_info get_leap_second_info(const utc_time<Duration>& ut);
```

返回：一个 leap_second_info 对象 lsi，其中如果 ut 处于正闰秒插入期间，则 lsi.is_leap_second 为 true，否则为 false。lsi.elapsed 是 1970-01-01 与 ut 之间的闰秒总和。如果 lsi.is_leap_second 为 true，则 ut 所指向的闰秒包含在该总和中。

## 27.7.4 tai_clock 类 [time.clock.tai]

### 27.7.4.1 概述 [time.clock.tai.overview]

```
namespace std::chrono {
  class tai_clock {
  public:
    using rep
        = a signed arithmetic type;
    using period
        = ratio<unspecified, unspecified>;
    using duration
        = chrono::duration<rep, period>;
    using time_point
        = chrono::time_point<tai_clock>;
    static constexpr bool is_steady = unspecified;

    static time_point now();

    template<class Duration>
      static utc_time<common_type_t<Duration, seconds>>
        to_utc(const tai_time<Duration>&) noexcept;
    template<class Duration>
      static tai_time<common_type_t<Duration, seconds>>
        from_utc(const utc_time<Duration>&) noexcept;
  };
}
```

1 tai_clock 时钟测量自 1958-01-01 00:00:00 以来的秒数，并且在该日期比 UTC 领先 10s。也就是说，1958-01-01 00:00:00 TAI 相当于 1957-12-31 23:59:50 UTC。闰秒不会插入 TAI。因此，每次向 UTC 插入闰秒时，UTC 相对于 TAI 会再偏移一秒。例如，到 2000-01-01 为止，已经插入了 22 个正闰秒和 0 个负闰秒，所以 2000-01-01 00:00:00 UTC 相当于 2000-01-01 00:00:32 TAI（22s 加上初始的 10s 偏移）。

2 除非实现能够保证 tai_clock::now() 不传播异常，否则 tai_clock 不是 Cpp17TrivialClock。

> [注意 1：noexcept(from_utc(utc_clock::now())) 为 false。— 结束注释]

### 27.7.4.2 成员函数 [time.clock.tai.members]

```
static time_point now();
```

返回：from_utc(utc_clock::now())，或一个更精确的 tai_time 值。

```
template<class Duration>
    static utc_time<common_type_t<Duration, seconds>>
    to_utc(const tai_time<Duration>& t) noexcept;
```

返回：

```
utc_time<common_type_t<Duration, seconds>>{t.time_since_epoch()} - 378691210s
```

> [注意 1：
>
>     378691210s == sys_days{1970y/January/1} - sys_days{1958y/January/1} + 10s
>
> — 结束注释]

```
template<class Duration>
    static tai_time<common_type_t<Duration, seconds>>
    from_utc(const utc_time<Duration>& t) noexcept;
```

返回：

```
tai_time<common_type_t<Duration, seconds>>{t.time_since_epoch()} + 378691210s
```

> [注意 2：
>
>     378691210s == sys_days{1970y/January/1} - sys_days{1958y/January/1} + 10s
>
> — 结束注释]

### 27.7.4.3 非成员函数 [time.clock.tai.nonmembers]

```
template<class charT, class traits, class Duration>
    basic_ostream<charT, traits>&
    operator<<(basic_ostream<charT, traits>& os, const tai_time<Duration>& t);
```

效果：相当于：

```
return os << format(STATICALLY-WIDEN<charT>("{:%F %T}"), t);
```

> [示例 1：
>
>     auto st = sys_days{2000y/January/1};
>     auto tt = clock_cast<tai_clock>(st);
>     cout << format("{0:%F %T %Z} == {1:%F %T %Z}\n", st, tt);
>
>     产生以下输出：
>
>         2000-01-01 00:00:00 UTC == 2000-01-01 00:00:32 TAI
>
> — 结束示例]

```
template<class charT, class traits, class Duration, class Alloc = allocator<charT>>
    basic_istream<charT, traits>&
    from_stream(basic_istream<charT, traits>& is, const charT* fmt,
                tai_time<Duration>& tp, basic_string<charT, traits, Alloc>* abbrev = nullptr,
                minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 中给出的格式标志，将输入流 is 解析为 tai_time tp。如果解析未能解码出有效日期，则调用 is.setstate(ios_base::failbit)，并且不修改 tp。如果使用了 %Z 并成功解析，且 abbrev 非空，则该值将被赋给 *abbrev。如果使用了 %z（或其修饰变体）并成功解析，且 offset 非空，则该值将被赋给 *offset。此外，解析出的偏移量将从成功解析的时间戳中减去，然后将该差值赋给 tp。

返回：is。

## 27.7.5 gps_clock 类 [time.clock.gps]

### 27.7.5.1 概述 [time.clock.gps.overview]

```
namespace std::chrono {
  class gps_clock {
  public:
    using rep = a signed arithmetic type;
    using period = ratio<unspecified, unspecified>;
    using duration = chrono::duration<rep, period>;
    using time_point = chrono::time_point<gps_clock>;
    static constexpr bool is_steady = unspecified;

    static time_point now();

    template<class Duration>
      static utc_time<common_type_t<Duration, seconds>>
        to_utc(const gps_time<Duration>&) noexcept;
    template<class Duration>
      static gps_time<common_type_t<Duration, seconds>>
        from_utc(const utc_time<Duration>&) noexcept;
  };
}
```

1 gps_clock 时钟测量自 1980 年 1 月第一个星期日 00:00:00 UTC 以来的秒数。闰秒不会插入 GPS。因此，每次向 UTC 插入闰秒时，UTC 相对于 GPS 会再偏移一秒。除了从 1958y/January/1 到 1980y/January/Sunday[1] 的偏移之外，由于 1958 年到 1970 年之间的 10s 偏移以及 1970 年到 1980 年之间额外插入的 9 个闰秒，GPS 比 TAI 慢 19s。

2 除非实现能够保证 gps_clock::now() 不传播异常，否则 gps_clock 不是 Cpp17TrivialClock。

> [注意 1：noexcept(from_utc(utc_clock::now())) 为 false。— 结束注释]

### 27.7.5.2 成员函数 [time.clock.gps.members]

```
static time_point now();
```

1 返回：from_utc(utc_clock::now())，或一个更精确的 gps_time 值。

```
template<class Duration>
  static utc_time<common_type_t<Duration, seconds>>
    to_utc(const gps_time<Duration>& t) noexcept;
```

2 返回：

```
gps_time<common_type_t<Duration, seconds>>{t.time_since_epoch()} + 315964809s
```

> [注意 1：
> 315964809s == sys_days{1980y/January/Sunday[1]} - sys_days{1970y/January/1} + 9s
> — 结束注释]

```
template<class Duration>
  static gps_time<common_type_t<Duration, seconds>>
    from_utc(const utc_time<Duration>& t) noexcept;
```

3 返回：

```
gps_time<common_type_t<Duration, seconds>>{t.time_since_epoch()} - 315964809s
```

> [注意 2：
> 315964809s == sys_days{1980y/January/Sunday[1]} - sys_days{1970y/January/1} + 9s
> — 结束注释]

