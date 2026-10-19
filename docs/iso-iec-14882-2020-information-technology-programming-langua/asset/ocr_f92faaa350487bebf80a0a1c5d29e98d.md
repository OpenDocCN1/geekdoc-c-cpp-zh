# 27.8.6 Class weekday [time.cal.wd]

# 27.8.6.1 Overview [time.cal.wd.overview]

```
template<class charT, class traits>
    basic_ostream<charT, traits>&
        operator<<(basic_ostream<charT, traits>& os, const year& y);
```

Effects: Equivalent to:

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

Effects: Attempts to parse the input stream is into the year y using the format flags given in the NTCTS fmt as specified in 27.13. If the parse fails to decode a valid year, is.setstate(ios_base::failbit) is called and y is not modified. If %Z is used and successfully parsed, that value will be assigned to *abbrev if abbrev is non-null. If %z (or a modified variant) is used and successfully parsed, that value will be assigned to *offset if offset is non-null.

Returns: is.

```
constexpr chrono::year operator"'y"(unsigned long long y) noexcept;
```

Returns: year{static_cast<int>(y)}.

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

1 weekday represents a day of the week in the civil calendar. It normally holds values in the range 0 to 6, corresponding to Sunday through Saturday, but it may hold non-negative values outside this range. It can be constructed with any unsigned value, which will be subsequently truncated to fit into weekday’s unspecified internal storage. weekday meets the Cpp17EqualityComparable (Table 25) requirements.

[Note 1: weekday is not Cpp17LessThanComparable because there is no universal consensus on which day is the first day of the week. weekday’s arithmetic operations treat the days of the week as a circular range, with no beginning and no end. — end note]

2 weekday is a trivially copyable and standard-layout class type.