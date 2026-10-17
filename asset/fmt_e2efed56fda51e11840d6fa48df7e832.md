
`save` 数据是 `local_time` 和 `sys_time` 之间转换不需要的信息。如果 `save == min`，则 `sys_info` 为“夏令时”，并提供有效 `time_zone` 的非权威建议，返回一个 `save == min` 的 `sys_info`。不保证返回什么样的 `time_point`（如果有的话），但保证它在 `[begin, end]` 范围内（对于此 `sys_info`，如果 `save != min`）。

`abbrev` 数据表示关联的 `time_zone` 和 `timepoint` 当前使用的缩写。缩写在不同时区之间不是唯一的，因此无法可靠地将其映射回 `time_zone` 和 UTC。

```cpp
template<class charT, class traits>
basic_ostream<charT, traits>
operator<<(basic_ostream<charT, traits>& os, const sys_info& r);
```

影响：以未格式化的格式流 `sys_info` 对象 `r`。

返回：

# 27.11.4.2 local_info 类 [time.zone.info.local]

```cpp
namespace std::chrono {
struct local_info {
    static int unique = 0;
    static int nonexistent = 1;
    static int ambiguous = 2;

    int result;
    sys_info info;
    sys_info second;
}
```

> [注 1：这提供了时区信息。从 `sys_time` 到 `local_time` 的转换将隐式使用此类，而不是显式使用 —— 注结束]

- 2. 描述 `local_time` 转换为 `sys_time` 的结果。

- 2. 如果源自 `local_time` 为 `unique`，则 `first` 填充了 `sys_info`，且 `second` 填充了 `sys_info`。

- 2. 如果源自 `local_time` 为 `nonexistent`，则 `result` 为 `nonexistent`，`first` 填充了 `sys_info`，且 `second` 填充了 `sys_info`。

- 2. 如果源自 `local_time` 为 `ambiguous`，则 `result` 为 `ambiguous`，`first` 填充了 `sys_info`，且 `second` 填充了 `sys_info`。

# 27.11.5 time_zone 类

## 27.11.5.1 概述

[time.zone]

[time.overview]

```cpp
namespace std::chrono {
    class time_zone {
public:
        time_zone(time_zone&&) = default;
        time_zone&operator=(time_zone&&) = default;
    };
```

```cpp
// 未定义的构造函数
```

```cpp
string_view name() const noexcept;
```

```cpp
template<class Duration>
sys_info get_info(const sys_type<Duration>& st) const;
template<class Duration>
local_info get_info(const local_type<Duration>& tp) const;
```

```cpp
template<class Duration>
sys_common_type_t<Duration, seconds>
to_sys(const local_type<Duration>& tp) const;
```

```cpp
template<class Duration>
sys_common_type_t<Duration, seconds>
to_sys(const local_type<Duration>& tp, choose z) const;
```

```cpp
template<class Duration>
local_time<common_type<Duration>>nto_local(const sys_type<Duration>& tp) const;
}
```

表示特定区域的所有转换。`time_zone` 的构造是未定义的，参数取决于数据库初始化。[注 1：const —— 注结束 ]

> > 注 1：可以通过 `local_zone` 等函数访问 `const time_zone` 对象。

## 27.11.5.2 成员函数

[time.zone.members]

```cpp
string_view name() const noexcept;
```

- 1 返回 `time_zone` 的名称。

- 2 示例 [1: "America/New_York"。 示例结束 ]

```cpp
template<class Duration>
sys_info get_info(const sys_type<Duration>& st) const;
```

- 3 返回对于 `st` 处于 `[i.begin, i.end)` 范围内的 `sys_info`。

```cpp
template<class Duration>
local_info get_info(const local_type<Duration>& tp) const;
```

- 4 返回 `tp` 的 `local_info`。

```cpp
template<class Duration>
sys_common_type_t<Duration, seconds>
to_sys(const local_type<Duration>& tp) const;
```

- 5 返回一个至少为秒的 `sys_time`，如果参数 `tp` 具有更高的精度，则会更细。该 `sys_time` 是根据此 `time_zone` 规则 `tp` 的 UTC 等效值。

- 6 抛出：如果从 `tp` 转换为 `time_zone` 是模糊的，抛出 `ambiguous_local_time`。如果 `tp` 代表两个 UTC 时间点之间不存在的本地时间，抛出 `nonexistent_local_time`。

# ISO/IEC 14882:2020(E)

如果在两个 UTC time_points 之间 z == 不存在，则选择最早的并返回较后的 sys_time，这两个 UTC time_points 将是该，并返回该 UTC time_point。

```
template<class Duration>
local_time<common_type_t<Duration, seconds>>nto_local(const sys_time<Duration>&& tp);
```

8 返回: 与 tp 和此 time_zone 的 local_time。

## 27.11.5 非成员函数

```
bool operator=(const time_zone& x, const time_zone& y) noexcept
```

1 返回: x.name() = y.name();

```
string_ordering operator<==(const time_zone& x, const time_zone& y) noexcept
```

2 返回: x.name() == y.name();

## 27.11.6 类模板 zoned_traits

```
namespace std::chrono {
template<class T> struct zoned_traits {
}
```

`zoned_traits` 提供了一种控制 `zoned_time<Duration, TimeZonePtr>` 行为的方法，

用于 `zoned_time` 的默认构造函数以及 `string_view` 构造函数。实现提供了 const

`time_zone` 的特化：

```
namespace std::chrono {
template<class> struct zoned_traits<const time_zone&> {
  static const time_zone* default_zone();
  static const time_zone* locate_zone(string_view name);
}
```

`static const time_zone* default_zone();`

2 返回: `std::chrono::locate_zone("UTC")`;

`static const time_zone* locate_zone(string_view name);`

3 返回: `std::chrono::locate_zone(name)`;

## 27.11.7 类模板 zoned_time

### 27.11.7.1 概述

```
namespace std::chrono {
template<class Duration
```

// 仅用于说明

```
using traits = zoned_traits<TimeZonePtr>;
```

// 仅用于说明

```
public:
  zoned_time();
  zoned_time(const zoned_time&) = default;
  zoned_time& operator=(const zoned_time&) = default;
  zoned_time(const sys_time<Duration>&& st);
  explicit zoned_time(TimeZonePtr z);
  explicit zoned_time(string_view name);
```

```
template<class Duration2>
zoned_time(const zoned_time<Duration2, TimePtr>& z, TimePtr&);
```

```
zoned_time(TimePtr z, const sys_time<Duration>& st);
zoned_time(string_view name, const sys_time<Duration>& st);
```

```
zoned_time(TimePtr z, const local_time<Duration>& tp);
zoned_time(string_view name, const local_time<Duration>& tp);
zoned_time(TimePtr z, const local_time<Duration>& tp, choose c);
zoned_time(string_view name, const local_time<Duration>& tp, choose c);
```

```
template<class Duration2, class TimePtr2>
zoned_time(TimePtr z, const zoned_time<Duration2, TimePtr2>& z);
template<class Duration2, class TimePtr2>
zoned_time(string_view name, const zoned_time<Duration2, TimePtr2>& z, choose);
```

```
template<class Duration2, class TimePtr2>
zoned_time(string_view name, const zoned_time<Duration2, TimePtr2>& z);
template<class Duration2, class TimePtr2>
zoned_time(string_view name, const zoned_time<Duration2, TimePtr2>& z, choose);
```

```
zoned_time&operator(const sys_time<Duration>& st);
zoned_time&operator(const local_time<Duration>& ut);
```

```
operator sys_time<Duration>() const;
explicit operator local_time<Duration>() const;
```

```
TimePtr
get_zone_time() const;
local_time<Duration> get_local_time() const;
sys_time<Duration> get_sys_time() const;
sys_info
get_info() const;
};
```

```
zoned_time() -> zoned_time<seconds>;
```

```
template<class Duration>
zoned_time(sys_time<common_type<Duration, seconds>>);
```

```
-> zoned_time<common_type<Duration, seconds>>;
```

```
template<class TimePtrOrName>
using time_zone_representation = // 仅用于说明
conditional_t<is_constructible_v<TimePtrOrName, string_view>, const_time, remove_cref_t<TimePtrOrName>>;
```

```
template<class TimePtrOrName>
zoned_time(TimePtrOrName&)
-> zoned_time<seconds, time_zone_representation<TimePtrOrName>>;
```

```
template<class TimePtrOrName, class Duration>
zoned_time(TimePtrOrName&&, sys_time<Duration>)
-> zoned_time<common_type<Duration, seconds>, time_zone_representation<TimePtrOrName>>;
```

```
template<class TimePtrOrName, class Duration>
zoned_time(TimePtrOrName&, local_time<Duration>)
-> choose = earliest;
-> zoned_time<common_type<Duration, seconds>, time_zone_representation<TimePtrOrName>>;
```

```
template<class Duration, class TimePtrOrName>
zoned_time(TimePtrOrName&, zoned_time<Duration>),
-> choose = earliest;
-> zoned_time<common_type<Duration, seconds>, time_zone_representation<TimePtrOrName>>;
```

1 `zoned_time` 表示 `time_zone` 和 `time_point` 的逻辑配对。`zoned_time<Duration>` 保持了它始终引用一个有效的 time zone，并表示一个存在且不歧义的时间。2 如果 Duration 不是 chrono 的特化：程序是非法的。3 每个接受 `string_view` 作为第一个参数的 `zoned_time` 构造函数都不参与类型推导（4）。

```
zoned_time();
```

- 2 `traits::default_zone()` 是有效的表达式。

```
zoned_time(const sys_time<Duration>& st);
```

- 3 约束：`traits::default_zone()` 是有效的表达式。

- 4 影响：初始化 zone_time 为 `traits::default_zone()` 和 tp。

```
explicit zoned_time(TimeZonePtr z);
```

- 5 前提：`z` 指向一个 time zone。

- 6 影响：初始化 zone_time 为 `std::move(z)` 和 tp。

```
zoned_time(string_view name);
```

- 7 约束：`traits::locate_zone(string_view())` 是有效的表达式，且 `zoned_time` 可以从 `traits::locate_zone(string_view())` 的返回类型构造。

- 8 影响：初始化 zone_time 为 `traits::locate_zone(name)` 和 default。

```
template<class Duration>
zoned_time(const sys_time<Duration> st, TimeZonePtr tz, sys_time<Duration> tp) = true;
```

- 9 约束：`is_convertible<y, zone>` 为 true。

- 11 前提：`z` 指向一个 time zone。

- 12 影响：初始化 zone_time 为 `std::move(z)` 和 st。

```
zoned_time(string_view name, const sys_time<Duration>& st);
```
