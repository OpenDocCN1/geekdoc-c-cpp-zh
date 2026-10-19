
## ISO/IEC 14882:2020(E)

```
const tzdb& reload_tzdb();
```

Effects: This function first checks the version of the remote time zone database. If the versions of the local and remote databases are the same, there are no effects. Otherwise the remote database is pushed to the front of the tzdb_list accessed by get_tzdb_list().

Synchronization: This function is thread-safe with respect to get_tzdb_list().front() and get_tzdb_list().erase_after().

Postconditions: No pointers, references, or iterators are invalidated.

Returns: get_tzdb_list().front().

Throws: runtime_error if for any reason a reference cannot be returned to a valid tzdb.

```
string remote_version();
```

Returns: The latest remote database version.

> [Note 1: This can be compared with get_tzdb().version to discover if the local and remote databases are equivalent. — end note]

### 27.11.3 Exception classes [time.zone.exception]

### 27.11.3.1 Class nonexistent_local_time [time.zone.exception.nonexist]

```
namespace std::chrono {
  class nonexistent_local_time : public runtime_error {
  public:
    template<class Duration>
      nonexistent_local_time(const local_time<Duration>& tp, const local_info& i);
  };
}
```

nonexistent_local_time is thrown when an attempt is made to convert a non-existent local_time to a sys_time without specifying choose::earliest or choose::latest.

```
template<class Duration>
  nonexistent_local_time(const local_time<Duration>& tp, const local_info& i);
```

Preconditions: i.result == local_info::nonexistent is true.

Effects: Initializes the base class with a sequence of char equivalent to that produced by os.str() initialized as shown below:

```
ostringstream os;
os << tp << " is in a gap between\n"
<< local_seconds{i.first.end.time_since_epoch()} + i.first.offset << ' '
<< i.first.abbrev << " and\n"
<< local_seconds{i.second.begin.time_since_epoch()} + i.second.offset << ' '
<< i.second.abbrev
<< " which are both equivalent to\n"
<< i.first.end << " UTC";
```

[Example 1:

```
#include <chrono>
#include <iostream>

int main() {
  using namespace std::chrono;
  try {
    auto zt = zoned_time{"America/New_York",
                        local_days{Sunday[2]/March/2016} + 2h + 30min};
  } catch (const nonexistent_local_time& e) {
    std::cout << e.what() << '\n';
  }
}
```

Produces the output:

```
2016-03-13 02:30:00 is in a gap between
2016-03-13 02:00:00 EST and
```

### 27.11.5 Class time_zone [time.zone.timezone]

### 27.11.5.1 Overview [time.zone.overview]

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

### 27.11.5.2 Member functions [time.zone.members]

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

7 Returns: A sys_time that is at least as fine as seconds, and will be finer if the argument tp has finer precision. This sys_time is the UTC equivalent of tp according to the rules of this time_zone. If the conversion from tp to a sys_time is ambiguous, returns the earlier sys_time if z == choose::earliest, and returns the later sys_time if z == choose::latest. If the tp represents a non-existent time between two UTC time_points, then the two UTC time_points will be the same, and that UTC time_point will be returned.

```
template<class Duration>
    local_time<common_type_t<Duration, seconds>>
        to_local(const sys_time<Duration>& tp) const;
```

Returns: The local_time associated with tp and this time_zone.

### 27.11.5.3 Non-member functions [time.zone.nonmembers]

```
bool operator==(const time_zone& x, const time_zone& y) noexcept;
```

Returns: x.name() == y.name().

```
strong_ordering operator<=>(const time_zone& x, const time_zone& y) noexcept;
```

Returns: x.name() <=> y.name().

### 27.11.6 Class template zoned_traits [time.zone.zonedtraits]

```
namespace std::chrono {
    template<class T> struct zoned_traits {};
}
```

zoned_traits provides a means for customizing the behavior of zoned_time<Duration, TimeZonePtr> for the zoned_time default constructor, and constructors taking string_view. A specialization for const time_zone* is provided by the implementation:

```
namespace std::chrono {
    template<> struct zoned_traits<const time_zone*> {
        static const time_zone* default_zone();
        static const time_zone* locate_zone(string_view name);
    };
}
```

```
static const time_zone* default_zone();
```

Returns: std::chrono::locate_zone("UTC").

```
static const time_zone* locate_zone(string_view name);
```

Returns: std::chrono::locate_zone(name).

### 27.11.7 Class template zoned_time [time.zone.zonedtime]

### 27.11.7.1 Overview [time.zone.zonedtime.overview]

```
namespace std::chrono {
    template<class Duration, class TimeZonePtr = const time_zone*>
    class zoned_time {
    public:
        using duration = common_type_t<Duration, seconds>;

    private:
        TimeZonePtr zone_; // exposition only
        sys_time<duration> tp_; // exposition only

        using traits = zoned_traits<TimeZonePtr>; // exposition only

    public:
        zoned_time();
        zoned_time(const zoned_time&) = default;
        zoned_time& operator=(const zoned_time&) = default;

        zoned_time(const sys_time<Duration>& st);
        explicit zoned_time(TimeZonePtr z);
        explicit zoned_time(string_view name);
```

```
time-zone-representation<TimeZonePtrOrName>;
```

```
}
```

1 zoned_time represents a logical pairing of a time_zone and a time_point with precision Duration. zoned_time<Duration> maintains the invariant that it always refers to a valid time zone and represents a point in time that exists and is not ambiguous in that time zone.

2 If Duration is not a specialization of chrono::duration, the program is ill-formed.

3 Every constructor of zoned_time that accepts a string_view as its first parameter does not participate in class template argument deduction (12.4.2.9).

### 27.11.7.2 Constructors [time.zone.zonedtime.ctor]

```
zoned_time();
```

1 Constraints: traits::default_zone() is a well-formed expression.

2 Effects: Initializes zone_ with traits::default_zone() and default constructs tp_.

```
zoned_time(const sys_time<Duration>& st);
```

3 Constraints: traits::default_zone() is a well-formed expression.

4 Effects: Initializes zone_ with traits::default_zone() and tp_ with st.

```
explicit zoned_time(TimeZonePtr z);
```

5 Preconditions: z refers to a time zone.

6 Effects: Initializes zone_ with std::move(z) and default constructs tp_.

```
explicit zoned_time(string_view name);
```

7 Constraints: traits::locate_zone(string_view{}) is a well-formed expression and zoned_time is constructible from the return type of traits::locate_zone(string_view{}).

8 Effects: Initializes zone_ with traits::locate_zone(name) and default constructs tp_.

```
template<class Duration2>
  zoned_time(const zoned_time<Duration2, TimeZonePtr>& y);
```

9 Constraints: is_convertible_v<sys_time<Duration2>, sys_time<Duration>> is true.

10 Effects: Initializes zone_ with y.zone_ and tp_ with y.tp_.

```
zoned_time(TimeZonePtr z, const sys_time<Duration>& st);
```

11 Preconditions: z refers to a time zone.

12 Effects: Initializes zone_ with std::move(z) and tp_ with st.

```
zoned_time(string_view name, const sys_time<Duration>& st);
```

13 Constraints: zoned_time is constructible from the return type of traits::locate_zone(name) and st.

14 Effects: Equivalent to construction with {traits::locate_zone(name), st}.
