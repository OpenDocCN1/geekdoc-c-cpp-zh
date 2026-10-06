

# ISO/IEC 14882:2017(E)

```cpp
template <class Duration, class Clock, class Duration>
constexpr time_point<Clock, Duration>
floor(const time_point<Clock, Duration>&& tp);
template <class Duration, class Clock, class Duration>
constexpr time_point<Clock, Duration>
ceil(const time_point<Clock, Duration>&& tp);
template <class Duration, class Clock, class Duration>
constexpr time_point<Clock, Duration>
round(const time_point<Clock, Duration>&& tp);
```

// 23.17.5.9, 特殊化算法

```cpp
template <class Rep, class Period>
constexpr duration<Rep, Period> abs(duration<Rep, Period> d);
```

// 23.17.7, 时钟

```cpp
class system_clock;
class steady_clock;
class high_resolution_clock;
```

// 23.17.5.8, duration 字面量量的后缀

```cpp
operator""
```

```cpp
namespace chrono {
	using namespace ::chrono_literals;
}
```

## 23.17.3 时钟要求 [time.clock.req]

- 1 时钟是一个由持续时间（duration）、时间点（time_point）以及一个获取当前时间点的函数组成的包。时钟时间点的起点被称为时钟的纪元（epoch）。时钟应当满足表 52 中的要求。
- 2 在表 52 中，C1 和 C2 表示时钟类型。t1 和 t2 是由 Ci::now() 返回的，其中返回 t1 的调用发生在 (4.7) 返回 t2 的调用之前，且这两个调用都发生在 Ci::time_point::max() 之前。[注：这意味着 Ci 在 t1 和 t2 之间没有发生回绕（wrap around）。—— 注释结束]

# ISO/IEC 14882:2017(E)

表 52 — 时钟要求

| 表达式 | 返回类型 | 操作语义 |
|---|---|---|
| C1::rep | 算术类型或模拟算术类型的类 | C1::duration 的表示类型。 |
| C1::period | ratio 的特化版本 | 时钟以秒为单位的刻周期（tick period）。 |
| C1::duration | chrono:duration<C1::rep, C1::period> | 时钟的持续时间类型。 |
| C1::time_point | chrono:time_point<C1> or chrono:time_point<C2, C1::duration> | 时钟的时间点。C1 和 C2 应指向同一个纪元。 |
| C1::is_steady | const bool | 如果 <= C2 始终为真且刻之间的时间是恒定的，则为 true，否则为 false。 |
| C1::now() | C1::time_point | 返回一个代表当前时间点。 |

- 3 [注：这些持续时间的相对差异由时钟报告，国际单位（SI）定义是对实现质量的度量。—— 注释结束]

- 4 如果类型 TC 满足 TrivialClock（简单时钟）要求，则：
  (4.1) TC 满足时钟要求 (23.17.3)，
  (4.2) 类型 TC::rep: duration 和 TC::time_point 满足 EqualityComparable（表 20）、HashComparable（表 21）、DefaultConstructible（表 22）、CopyConstructible（表 24）、Copyable（表 26）、Desturable（表 27）以及数值类型的要求 (29.3)。注：这意味着对这些类型进行的操作不会抛出异常。—— 注释结束
  (4.3) 且 TC::rep: duration 和 TC::time_point 是可交换的 (20.5.3, 2)，
  (4.4) 函数 TC::now() 不抛异常，且
  (4.5) 类型 TC::time_point::clock 递归满足 TrivialClock。

## 23.17.4 时间相关的特性 [time.traits]

### 23.17.4.1 treat_as_floating_point [time.traits.is_fp]

```cpp
template <class Rep> struct treat_as_floating_point
: is_floating_point<Rep> {};
```

1 持续时间使用 treat_as_floating_point 特性来确定 duration 对象是否可以转换为具有不同刻周期的另一个持续时间。如果 treat_as_floating_point<Rep> 为真，则允许持续时间之间进行隐式转换。否则，隐式转换性取决于持续时间的刻周期。[注：该特性的意图是指示类行为是否类似于浮点类型，从而在用一个值除以另一个值时具有可以接受的精度损失。如果 treat_as_floating_point<Rep> 为假，且为了这些转换之目的它表现得像整数类型，则被拒绝。—— 注释结束]

# ISO/IEC 14882:2017(E)

## 23.17.4.2 duration_values [time.traits.duration_values]

```cpp
template <class Rep>
struct duration_values {
public:
    static constexpr Rep zero();
    static constexpr Rep min();
    static constexpr Rep max();
}
```

持续时间模板使用 duration_values 来...

# ISO/IEC 14882:2017(E)

## 23.17.5 持续时间类 [time.duration]

1 持续时间测量两个时间点（time_points）。持续时间拥有刻数（count）和一个刻周期。刻周期是从上刻到下一刻发生的时间，以秒为单位。它使用比例（ratio）表示。

```cpp
template <class Rep, Period = ratio<1>>
class duration {
public:
    using rep = Rep;
    using Period = typename Period::type;
private:
    Rep_; // 仅用于
public:
    // 23.17.5, 构造/拷贝/析构
    constexpr duration() = default;
    template <class Rep2>
    constexpr duration(const Rep2&, Period2 = Period) 
    template <class Rep2>
    constexpr duration(const Rep2, Period2& d) -duration(0) = default;
    constexpr duration(const duration) = default;
    duration& operator=(const duration) = default;
```

```cpp
// 23.17.5, 算术运算
    constexpr common_type<duration> operator+(const duration) const;
    constexpr common_type<duration> operator-(const duration) const;
    constexpr duration operator+(const duration&);
    constexpr duration operator+(int);
    duration& operator+=(const duration&);
    duration& operator+=(int);
    constexpr duration operator-(const duration&);
    duration& operator-=(const duration&);
    constexpr duration operator*(const rep& rhs);
    duration& operator*=(const rep& rhs);
    constexpr duration operator%(const rep& rhs);
    duration& operator%=(const rep& rhs);
```

```cpp
// 23.17.5, 特殊值
    static constexpr duration zero();
    static constexpr duration min();
    static constexpr duration max();
```

