# 27.11.5 Class time_zone

# [time.zone.timezone]

# 27.11.5.1 Overview

# [time.zone.overview]

```
namespace std::chrono {
  class time_zone {
  public:
    time_zone(time_zone&&) = default;
    time_zone& operator=(time_zone&&) = default;

    // unspecified additional constructors

    string_view name() const noexcept;

    template<class Duration> sys_info get_info(const sys_time<Duration>& st) const;
    template<class Duration> local_info get_info(const local_time<Duration>& tp) const;

    template<class Duration>
      sys_time<common_type_t<Duration, seconds>>
      to_sys(const local_time<Duration>& tp) const;

    template<class Duration>
      sys_time<common_type_t<Duration, seconds>>
      to_sys(const local_time<Duration>& tp, choose z) const;

    template<class Duration>
      local_time<common_type_t<Duration, seconds>>
      to_local(const sys_time<Duration>& tp) const;
  };
}
```

1 A time_zone represents all time zone transitions for a specific geographic area. time_zone construction is unspecified, and performed as part of database initialization.

> [Note 1: const time_zone objects can be accessed via functions such as locate_zone. — end note]

# 27.11.5.2 Member functions

# [time.zone.members]

```
string_view name() const noexcept;
```

1 Returns: The name of the time_zone.

> [Example 1: "America/New_York". — end example]

```
template<class Duration>
  sys_info get_info(const sys_time<Duration>& st) const;
```

3 Returns: A sys_info i for which st is in the range [i.begin, i.end).

```
template<class Duration>
  local_info get_info(const local_time<Duration>& tp) const;
```

4 Returns: A local_info for tp.

```
template<class Duration>
  sys_time<common_type_t<Duration, seconds>>
  to_sys(const local_time<Duration>& tp) const;
```

5 Returns: A sys_time that is at least as fine as seconds, and will be finer if the argument tp has finer precision. This sys_time is the UTC equivalent of tp according to the rules of this time_zone.

6 Throws: If the conversion from tp to a sys_time is ambiguous, throws ambiguous_local_time. If the tp represents a non-existent time between two UTC time_points, throws nonexistent_local_time.

```
template<class Duration>
  sys_time<common_type_t<Duration, seconds>>
  to_sys(const local_time<Duration>& tp, choose z) const;
```

7 Returns: A sys_time that is at least as fine as seconds, and will be finer if the argument tp has finer precision. This sys_time is the UTC equivalent of tp according to the rules of this time_zone. If the conversion from tp to a sys_time is ambiguous, returns the earlier sys_time if z ==