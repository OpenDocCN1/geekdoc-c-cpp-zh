```
constexpr year_month_day
    operator/(const year_month& ym, const day& d) noexcept;
        Returns: {ym.year(), ym.month(), d}.

constexpr year_month_day
    operator/(const year_month& ym, int d) noexcept;
        Returns: ym / day(d).

constexpr year_month_day
    operator/(const year& y, const month_day& md) noexcept;
        Returns: y / md.month() / md.day().

constexpr year_month_day
    operator/(int y, const month_day& md) noexcept;
        Returns: year(y) / md.

constexpr year_month_day
    operator/(const month_day& md, const year& y) noexcept;
        Returns: y / md.

constexpr year_month_day
    operator/(const month_day& md, int y) noexcept;
        Returns: year(y) / md.

constexpr year_month_day_last
    operator/(const year_month& ym, last_spec) noexcept;
        Returns: {ym.year(), month_day_last{ym.month()}}.

constexpr year_month_day_last
    operator/(const year& y, const month_day_last& mdl) noexcept;
        Returns: {y, mdl}.

constexpr year_month_day_last
    operator/(int y, const month_day_last& mdl) noexcept;
        Returns: year(y) / mdl.

constexpr year_month_day_last
    operator/(const month_day_last& mdl, const year& y) noexcept;
        Returns: y / mdl.

constexpr year_month_day_last
    operator/(const month_day_last& mdl, int y) noexcept;
        Returns: year(y) / mdl.

constexpr year_month_weekday
    operator/(const year_month& ym, const weekday_indexed& wdi) noexcept;
        Returns: {ym.year(), ym.month(), wdi}.

constexpr year_month_weekday
    operator/(const year& y, const month_weekday& mwd) noexcept;
        Returns: {y, mwd.month(), mwd.weekday_indexed()}.

constexpr year_month_weekday
    operator/(int y, const month_weekday& mwd) noexcept;
        Returns: year(y) / mwd.

constexpr year_month_weekday
    operator/(const month_weekday& mwd, const year& y) noexcept;
        Returns: y / mwd.
```