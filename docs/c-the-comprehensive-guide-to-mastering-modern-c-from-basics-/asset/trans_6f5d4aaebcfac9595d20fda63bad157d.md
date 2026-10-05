
这里是任何时钟的一种简化表示：

```cpp
struct clock {
    using microseconds;             // 时钟的粒度
    using duration = time_point<some_clock>; // now() 的返回类型
    static time_point now() noexcept; // 获取当前时间
};
```

为了清晰起见，我省略了 `rep`、`period` 和 `is_steady` 成员。每个时钟都定义了自己的粒度。核心函数是 `now()`，我稍后会向你详细解释它。

你自己定义新时钟的可能性非常低。标准库提供了几个（到 C++20 为止，只有 `system_clock`、`steady_clock` 和 `high_resolution_clock`），你可以根据应用程序使用它们：

- *std::chrono::system_clock*
  如果你需要日历引用，请使用此时钟。通过此时钟，你可以获取当前时间或日期。它提供了 `sys_time` 并像我们日常生活中一样处理闰秒。当你格式化秒时，预期范围是 "00" 到 "59"。此时钟可以存储从 1970 年 1 月 1 日午夜 (UTC) 开始的值。然而，这仅从 C++20 开始才有保证；在此之前，起点并未定义。

- *std::chrono::steady_clock*
  这更像是一个秒表。通过它可以在程序内进行时间测量。它与一天中的时间或日历没有关系。

- *std::chrono::high_resolution_clock*
  这通常是其他时钟之一的别名，取决于哪个系统在时间测量上的粒度最细。实现可能会可以提供特别精确的时钟。

- *std::chrono::file_clock*
  这与 `std::file_system::file_type::clock` 是同一个时钟，由 `file_system::last_write_time()` 等函数返回。时钟的起点未指定。然而，你可以使用 `clock_cast` 将其转换为 `sys_time`，后者有明确的起点。

- *std::chrono::utc_clock*
  提供 `utc_time`，它类似于 `sys_time` 但考虑了闰秒。当你计算跨闰秒的差异时，`utc_time` 会将其考虑在内。当你格式化 `utc_time` 时，要考虑秒 "60"，而不仅仅是 "00" 到 "59"。

- *std::chrono::gps_clock*
  `gps_clock` 提供 `gps_time` 并从 1980 年 6 月 1 日开始。它不考虑闰秒。它可以非常精确，但不是必须如此。它目前比 `sys_time` 和 `utc_time` 快 18 秒。

- *std::chrono::tai_clock*
  国际原子时（根据法语名称缩写为 TAI）是一种非常精确的时间，不考虑闰秒。它从 1958 年 1 月 1 日开始。当你格式化 `tai_time` 时，它总是比 `gps_time` 快 19 秒。

![](img/290cf954dfcaad53865de6b98cca8e6f_1515_0.png)

当你获取某个时钟（如 `steady_clock`）的当前时间时，可以如下方式获取：

```cpp
steady_clock::time_point tp = steady_clock::now();
```

或者直接使用 `auto`：

```cpp
auto tp = steady_clock::now();
```

通常情况下，在处理 `<chrono>` 时，你经常可以使用 `auto`，从而不需要记住所有的返回类型。
例如，你可以用它来测量函数调用的时间。

```cpp
// https://cppbolt.org/z/3MGBByn4ds
#include <iostream>
#include <chrono>
long fib(long n) { return n<2 ? 1L : fib(n-1)+fib(n-2); }
int main() {
  using namespace std::chrono;
}
```

```cpp
auto t0 = steady_clock::now(); // 准备好，跑 -
auto res = fib(t0); // 开始！
auto t1 = steady_clock::now(); // 停止！
std::cout << "Result: " << res << "\n"; // 输出: 2584
std::cout << "Time: " << nanoseconds(t1-t0).count() << "\n";
// 输出: Time: 50727ns (例如)
```

**列表 28.32** 函数调用的简单计时。

只需用 `now()` 测量调用前后的时间，并每次获取一个点。在这两点之间，你计算 `t1-t0` 的差异并得到一个持续时间。对于输出，将此持续时间转换为适用于测量的时间单位——这里是 `nanoseconds{...}`。这样就完成了。

## 转换时间与闰秒

从 C++20 开始，你可以使用 `clock_cast<>` 在不同时间点类型之间转换值。时钟的起点和闰秒都被考虑在内。

为此，有一个 `clock_time_conversions<>` 属性性。支持 `to utc`、`from_utc`、`to_sys` 和 `from_sys` 的时钟可以使用 `clock_cast<>` 进行转换。

```cpp
// https://godbolt.org/zsgP75Kr8
#include <iostream>
#include <chrono>
using namespace std::chrono;
int main() {
    time_point tai_now = tai_clock::now(); // 输出: 2023-10-19 12:13:06
```
