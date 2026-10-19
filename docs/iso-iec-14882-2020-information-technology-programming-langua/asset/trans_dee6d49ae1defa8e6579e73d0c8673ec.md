

### 27.8.5.3 非成员函数 [time.cal.year.nonmembers]

返回：作为进入此成员函数时存在的 *this 的副本。

```
constexpr year& operator--() noexcept;
```

效果：--y_。

返回：*this。

```
constexpr year operator--(int) noexcept;
```

效果：--(*this)。

返回：作为进入此成员函数时存在的 *this 的副本。

```
constexpr year& operator+=(const years& y) noexcept;
```

效果：*this = *this + y。

返回：*this。

```
constexpr year& operator-=(const years& y) noexcept;
```

效果：*this = *this - y。

返回：*this。

```
constexpr year operator+() const noexcept;
```

返回：*this。

```
constexpr year year::operator-() const noexcept;
```

返回：year{-y_}。

```
constexpr bool is_leap() const noexcept;
```

返回：y_ % 4 == 0 && (y_ % 100 != 0 || y_ % 400 == 0)。

```
constexpr explicit operator int() const noexcept;
```

返回：y_。

```
constexpr bool ok() const noexcept;
```

返回：min().y_ <= y_ && y_ <= max().y_。

```
static constexpr year min() noexcept;
```

返回：year{-32767}。

```
static constexpr year max() noexcept;
```

返回：year{32767}。

```
constexpr bool operator==(const year& x, const year& y) noexcept;
```

返回：int{x} == int{y}。

```
constexpr strong_ordering operator<=>(const year& x, const year& y) noexcept;
```

返回：int{x} <=> int{y}。

```
constexpr year operator+(const year& x, const years& y) noexcept;
```

返回：year{int{x} + y.count()}。

## 27.8.6 类 weekday [time.cal.wd]

### 27.8.6.1 概述 [time.cal.wd.overview]

```
template<class charT, class traits>
    basic_ostream<charT, traits>&
        operator<<(basic_ostream<charT, traits>& os, const year& y);
```

效果：等价于：

```
return os << (y.ok() ?
    format(STATICALLY-WIDEN<charT>("{:%Y}"), y) :
    format(STATICALLY-WIDEN<charT>("{:%Y} is not a valid year"), y));
```

```
template<class charT, class traits, class Alloc = allocator<charT>>
    basic_istream<charT, traits>&
    from_stream(basic_istream<charT, traits>& is, const charT* fmt,
        year& y, basic_string<charT, traits, Alloc>* abbrev = nullptr,
        minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 给出的格式标志将输入流 is 解析为 year y。如果解析未能解码出有效的年份，则调用 is.setstate(ios_base::failbit) 且 y 不会被修改。如果使用了 %Z 且成功解析，该值将被赋给 *abbrev（如果 abbrev 非空）。如果使用了 %z（或其修改变体）且成功解析，该值将被赋给 *offset（如果 offset 非空）。

返回：is。

```
constexpr chrono::year operator""y(unsigned long long y) noexcept;
```

返回：year{static_cast<int>(y)}。

```
namespace std::chrono {
  class weekday {
    unsigned char wd_;           // exposition only
  public:
    weekday() = default;
    constexpr explicit weekday(unsigned wd) noexcept;
    constexpr weekday(const sys_days& dp) noexcept;
    constexpr explicit weekday(const local_days& dp) noexcept;

    constexpr weekday& operator++() noexcept;
    constexpr weekday operator++(int) noexcept;
    constexpr weekday& operator--() noexcept;
    constexpr weekday operator--(int) noexcept;

    constexpr weekday& operator+=(const days& d) noexcept;
    constexpr weekday& operator-=(const days& d) noexcept;

    constexpr unsigned c_encoding() const noexcept;
    constexpr unsigned iso_encoding() const noexcept;
    constexpr bool ok() const noexcept;

    constexpr weekday_indexed operator[](unsigned index) const noexcept;
    constexpr weekday_last operator[](last_spec) const noexcept;
  };
}
```

1 weekday 表示民用历法中的星期几。它通常保存 0 到 6 范围内的值，对应星期日到星期六，但它可能保存超出此范围的非负值。它可以用任何无符号值构造，该值随后会被截断以适应 weekday 的未指定内部存储。weekday 满足 Cpp17EqualityComparable（表 25）要求。

[注 1：weekday 不是 Cpp17LessThanComparable，因为关于一周的第一天没有普遍共识。weekday 的算术运算将星期几视为一个环形范围，没有开始也没有结束。——注结束]

2 weekday 是一个可 trivial 复制且标准布局的类类型。

### 27.8.6.3 非成员函数 [time.cal.wd.nonmembers]

```
constexpr bool operator==(const weekday& x, const weekday& y) noexcept;
```

返回：x.wd_ == y.wd_。

```
constexpr weekday operator+(const weekday& x, const days& y) noexcept;
```

返回：

```
weekday{modulo(static_cast<long long>(x.wd_) + y.count(), 7)}
```

其中 modulo(n, 7) 计算 n 除以 7 的余数，使用欧几里得除法。

> [注 1：给定除数 7，欧几里得除法向负无穷截断，并且始终产生范围在 [0, 6] 内的余数。假设有符号求和中没有溢出，此操作即使在 !x.ok() 的情况下也会产生保存值在范围 [0, 6] 内的 weekday。——注结束]

> [示例 1：Monday + days{6} == Sunday。——示例结束]

```
constexpr weekday operator+(const days& x, const weekday& y) noexcept;
```

返回：y + x。

```
constexpr weekday operator-(const weekday& x, const days& y) noexcept;
```

返回：x + -y。

```
constexpr days operator-(const weekday& x, const weekday& y) noexcept;
```

返回：如果 x.ok() == true 且 y.ok() == true，则返回范围在 [days{0}, days{6}] 内的值 d，满足 y + d == x。否则返回的值未指定。

> [示例 2：Sunday - Monday == days{6}。——示例结束]

```
template<class charT, class traits>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os, const weekday& wd);
```

效果：等价于：

```
return os << (wd.ok() ?
format(os.getloc(), STATICALLY-WIDEN<charT>("{:%a}"), wd) :
format(os.getloc(), STATICALLY-WIDEN<charT>("{} is not a valid weekday"),
static_cast<unsigned>(wd.wd_)));
```

```
template<class charT, class traits, class Alloc = allocator<charT>>
basic_istream<charT, traits>&
from_stream(basic_istream<charT, traits>& is, const charT* fmt,
weekday& wd, basic_string<charT, traits, Alloc>* abbrev = nullptr,
minutes* offset = nullptr);
```

效果：尝试使用 27.13 中指定的 NTCTS fmt 给出的格式标志将输入流 is 解析为 weekday wd。如果解析未能解码出有效的星期几，则调用 is.setstate(ios_base::failbit) 且 wd 不会被修改。如果使用了 %Z 且成功解析，该值将被赋给 *abbrev（如果 abbrev 非空）。如果使用了 %z（或其修改变体）且成功解析，该值将被赋给 *offset（如果 offset 非空）。

返回：is。

## 27.8.7 类 weekday_indexed [time.cal.wdidx]

### 27.8.7.1 概述 [time.cal.wdidx.overview]

```
namespace std::chrono {
class weekday_indexed {
chrono::weekday wd_;           // exposition only
unsigned char index_;          // exposition only
public:
weekday_indexed() = default;
constexpr weekday_indexed(const chrono::weekday& wd, unsigned index) noexcept;
constexpr chrono::weekday weekday() const noexcept;
constexpr unsigned index() const noexcept;
constexpr bool ok() const noexcept;
};
}
```

### 27.8.7.2 成员函数 [time.cal.wdidx.members]

1 weekday_indexed 表示一个星期几和一个范围在 1 到 5 的小索引。此类用于表示一个月的第一个、第二个、第三个、第四个或第五个星期几。

2 [注 1：weekday_indexed 对象可以通过用无符号值索引一个 weekday 来构造。——注结束]

```
constexpr auto wdi = Sunday[2]; // wdi 是尚不确定的某个月的第二个星期日
static_assert(wdi.weekday() == Sunday);
static_assert(wdi.index() == 2);
```

3 weekday_indexed 是一个可 trivial 复制且标准布局的类类型。

```
constexpr weekday_indexed(const chrono::weekday& wd, unsigned index) noexcept;
```

1 效果：用 wd 初始化 wd_，用 index 初始化 index_。如果 !wd.ok() 或 index 不在范围 [0, 7] 内，所保存的值未指定。

```
constexpr chrono::weekday weekday() const noexcept;
```

2 返回：wd_。

```
constexpr unsigned index() const noexcept;
```

3 返回：index_。

```
constexpr bool ok() const noexcept;
```

4 返回：wd_.ok() && 1 <= index_ && index_ <= 5。

### 27.8.7.3 非成员函数 [time.cal.wdidx.nonmembers]

```
constexpr bool operator==(const weekday_indexed& x, const weekday_indexed& y) noexcept;
```

1 返回：x.weekday() == y.weekday() && x.index() == y.index()。

```
template<class charT, class traits>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os, const weekday_indexed& wdi);
```

2 效果：等价于：

```
auto i = wdi.index();
return os << (i >= 1 && i <= 5 ?
format(os.getloc(), STATICALLY-WIDEN<charT>("{0}[{1}]"), wdi.weekday(), i) :
format(os.getloc(), STATICALLY-WIDEN<charT>("{0}[{1} is not a valid index]"), wdi.weekday(), i));
```

## 27.8.8 类 weekday_last [time.cal.wdlast]

### 27.8.8.1 概述 [time.cal.wdlast.overview]

```
namespace std::chrono {
class weekday_last {
chrono::weekday wd_; // exposition only
public:
constexpr explicit weekday_last(const chrono::weekday& wd) noexcept;
constexpr chrono::weekday weekday() const noexcept;
constexpr bool ok() const noexcept;
};
}
```
