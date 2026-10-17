
# ISO/IEC 14882:2020(E)

```cpp
constexpr year_month_weekday_last
operator+(const year_month_weekday_last& ymmwdl, const months_& dm) noexcept;
constexpr year_month_weekday_last
operator+(const months_& dm, const year_month_weekday_last& ymmwdl) noexcept;
constexpr year_month_weekday_last
operator+(const year_month_weekday_last& ymmwdl, const days& dy) noexcept;
constexpr year_month_weekday_last
operator+(const days& dy, const year_month_weekday_last& ymmwdl) noexcept;
constexpr year_month_weekday_last
operator+(const year_month_weekday_last, const months_& dm) noexcept;
constexpr year_month_weekday_last
operator+(const year_month_weekday_last& ymmwdl, const days& dy) noexcept;

template<class T, class Traits>
basic_ostream<T, Traits>&
operator=(const basic_ostream<T, Traits>& os, const year_month_weekday_last& ymmwdl);
```

## 27.8.18, 公历历便捷语法运算符

```cpp
constexpr year_month
operator/(const year& y, const months_& m) noexcept;
constexpr year_month
operator/(const year& y, int m) noexcept;
constexpr month_day
operator/(const months_& m, const day& d) noexcept;
constexpr month_day
operator/(const months_& m, int d) noexcept;
constexpr month_day
operator/(int m, const day& d) noexcept;
constexpr month_day
operator/(const day& d, const months_& m) noexcept;
constexpr month_day
operator/(const day& d, int m) noexcept;
constexpr year_month_last
operator/(const months_& m, last_spec) noexcept;
constexpr month_day
operator/(int m, last_spec) noexcept;
constexpr month_day_last
operator/(last_spec, const months_& m) noexcept;
constexpr month_day
operator/(last_spec, int m) noexcept;
constexpr year_month_weekday
operator+(const months_& m, const weekday_indexed& wdi) noexcept;
constexpr year_month_weekday
operator/(int m, const weekday_indexed& wdi) noexcept;
constexpr year_month_weekday
operator/(const weekday_indexed& wdi, const months_& m) noexcept;
constexpr year_month_weekday
operator/(const weekday_indexed& wdi, int m) noexcept;
constexpr year_month_weekday_last
operator+(const months_& m, const weekday_last& wdl) noexcept;
constexpr year_month_weekday_last
operator/(int m, const weekday_last& wdl) noexcept;
constexpr year_month_weekday_last
operator/(const weekday_last& wdl, const months_& m) noexcept;
constexpr year_month_weekday_last
operator/(const weekday_last& wdl, int m) noexcept;
constexpr year_month_day
operator/(const year_month& ym, const day& d) noexcept;
constexpr year_month_day
operator/(const year_month& ym, int) noexcept;
constexpr year_month_day
operator/(const year& y, const month_day& md) noexcept;
constexpr year_month_day
operator/(int y, const month_day& md) noexcept;

constexpr pr_year_month_day
operator/(const month_day& kd, const year& y) noexcept;
constexpr pr_year_month_day
operator/(const month_day_k& md, int y) noexcept;
constexpr pr_year_month_day_last
operator/(const year_month& ym, last_spec) noexcept;
constexpr pr_year_month_day_last
operator/(const year& y, const month_day_last& mdl) noexcept;
constexpr pr_year_month_day_last
operator/(int y, const month_day_last& mdl) noexcept;
constexpr pr_year_month_day_last
operator/(const month_day_last& mdl, const year& y) noexcept;
constexpr pr_year_month_day_last
operator/(const month_day_last& mdl, int y) noexcept;
constexpr pr_year_month_week
operator/(const year_month& ym, const weekday_indexed& wd) noexcept;
constexpr pr_year_month_week
operator/(const year& y, const weekday_indexed& wd) noexcept;
constexpr pr_year_month_week
operator/(int y, const weekday_indexed& wd) noexcept;
constexpr pr_year_month_week
operator/(const weekday_indexed& wd, const year& y) noexcept;
constexpr pr_year_month_week_last
operator/(const weekday_indexed& wd, int y) noexcept;
constexpr pr_year_month_week_last
operator/(const year_month& ym, const weekday_last& wdl) noexcept;
constexpr pr_year_month_week_last
operator/(const year& y, const weekday_last& wdl) noexcept;
constexpr pr_year_month_week_last
operator/(int y, const weekday_last& wdl) noexcept;
constexpr pr_year_month_week_last
operator/(const weekday_last& wdl, const year& y) noexcept;
constexpr pr_year_month_week_last
operator/(const weekday_last& wdl, int y) noexcept;
```

## 27.9. class hh_mm_ss;

```cpp
template<class Duration> class hh_mm_ss;

template<class charT, class Traits, class Duration>
basic_ostream<charT, Traits>& operator<<=(const hh_mm_ss<Duration>& hms);
```

## 27.10.2 24小时函数

```cpp
constexpr bool is_am(const hours& h) noexcept;
constexpr bool is_pm(const hours& h) noexcept;
constexpr hours make_12(const hours& h, bool is_pm) noexcept;
```

## 27.11.1 时区数据库

```cpp
struct tzdb;
class tzdb_list;

const tzdb& get_tzdb();
const tzdb_list& get_tzdb_list();
const time_zone* locate_zone(string_view tz);
const time_zone* current_zone();
```

## 27.11.2. 远程时区支持

```cpp
const tzdb& reload_tzdb();
string remote_version();
```

## 27.11.3. 异常类

```cpp
class nonexistent_local_time;
class ambiguous_local_time;
```

## 27.11.4. 信息类

```cpp
struct sys_info;
template<class charT, class Traits>
basic_ostream<charT, Traits>& operator<<=(basic_ostream<charT, Traits>& os, const sys_info& si);

struct local_info;
template<class charT, class Traits>
basic_ostream<charT, Traits>& operator<<=(basic_ostream<charT, Traits>& os, const local_info& li);
```

## 27.11.5. 时区类

```cpp
enum class { earliest, latest };
class time_zone;

bool operator===(const time_zone& x, const time_zone& y) noexcept;
strong_ordering operator<==(const time_zone& x, const time_zone& y) noexcept;
```

## 27.11.6. 时区特性类

```cpp
template<class T> struct zoned_traits;
```

## 27.11.7. 时区时间类

```cpp
template<class Duration, class TimeZonePtr = const time_zone*> class zoned_time;

using zoned_seconds = zoned_time<seconds>;

template<class Duration1, class Duration2, class TimeZonePtr>
bool operator===(const Duration1& x, const Duration2& y, const TimeZonePtr& k);

template<class charT, class Traits, class TimeZonePtr>
basic_ostream<charT, Traits>& operator<<=(basic_ostream<charT, Traits>& os, const zoned_time<Duration, TimeZonePtr>& t);
```

## 27.11.8. 秒支持

```cpp
class leap_second;

bool operator===(const leap_second& x, const leap_second& y);
strong_ordering operator<=>(const leap_second& x, const leap_second& y);

template<class Duration>
bool operator===(const leap_second& x, const sys_time<Duration>& y);
template<class Duration>
bool operator<=(const leap_second& x, const sys_time<Duration>& y);
template<class Duration>
bool operator>=(const leap_second& x, const sys_time<Duration>& y);
```
