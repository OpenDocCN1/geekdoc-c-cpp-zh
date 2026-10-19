# 27.8.6.3 Non-member functions [time.cal.wd.nonmembers]

```
constexpr bool operator==(const weekday& x, const weekday& y) noexcept;
```

Returns: x.wd_ == y.wd_.

```
constexpr weekday operator+(const weekday& x, const days& y) noexcept;
```

Returns:

```
weekday{modulo(static_cast<long long>(x.wd_) + y.count(), 7)}
```

where modulo(n, 7) computes the remainder of n divided by 7 using Euclidean division.

> [Note 1: Given a divisor of 7, Euclidean division truncates towards negative infinity and always produces a remainder in the range of [0, 6]. Assuming no overflow in the signed summation, this operation results in a weekday holding a value in the range [0, 6] even if !x.ok(). — end note]

> [Example 1: Monday + days{6} == Sunday. — end example]

```
constexpr weekday operator+(const days& x, const weekday& y) noexcept;
```

Returns: y + x.

```
constexpr weekday operator-(const weekday& x, const days& y) noexcept;
```

Returns: x + -y.

```
constexpr days operator-(const weekday& x, const weekday& y) noexcept;
```

Returns: If x.ok() == true and y.ok() == true, returns a value d in the range [days{0}, days{6}] satisfying y + d == x. Otherwise the value returned is unspecified.

> [Example 2: Sunday - Monday == days{6}. — end example]

```
template<class charT, class traits>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os, const weekday& wd);
```

Effects: Equivalent to:

```
return os << (wd.ok() ?
format(os.getloc(), STATICALLY-WIDEN<charT>("{:%a}"), wd) :
format(os.getloc(), STATICALLY-WIDEN<charT>("{}") is not a valid weekday"),
static_cast<unsigned>(wd.wd_)));
```

```
template<class charT, class traits, class Alloc = allocator<charT>>
basic_istream<charT, traits>&
from_stream(basic_istream<charT, traits>& is, const charT* fmt,
weekday& wd, basic_string<charT, traits, Alloc>* abbrev = nullptr,
minutes* offset = nullptr);
```

Effects: Attempts to parse the input stream is into the weekday wd using the format flags given in the NTCTS fmt as specified in 27.13. If the parse fails to decode a valid weekday, is.setstate(ios_base::failbit) is called and wd is not modified. If %Z is used and successfully parsed, that value will be assigned to *abbrev if abbrev is non-null. If %z (or a modified variant) is used and successfully parsed, that value will be assigned to *offset if offset is non-null.

Returns: is.

# 27.8.7 Class weekday_indexed [time.cal.wdidx]

# 27.8.7.1 Overview [time.cal.wdidx.overview]

```
namespace std::chrono {
class weekday_indexed {
chrono::weekday wd_; // exposition only
unsigned char index_; // exposition only
public:
weekday_indexed() = default;
constexpr weekday_indexed(const chrono::weekday& wd, unsigned index) noexcept;
```