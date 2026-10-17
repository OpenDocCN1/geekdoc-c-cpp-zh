
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

# ISO/IEC 14882:2017(E)

## 5

duration 的默认拷贝构造函数应当是 `constexpr` 函数，当且仅当成员 `rep_` 分别用于拷贝和移动所需的初始化满足 `constexpr` 函数的要求时。

```
[示例:
duration<long,ratio<60>> d; // 使用 long 存储分钟计数
duration<long, milli> d; // 使用 long 存储毫秒计数
duration<double,ratio<1,30>> d; // 使用 double 存储每个刻度为 1/30 秒的计数
// (30 Hz)
```

--- 示例结束]

## 23.17.51 duration 构造函数 [time.duration.cons]

```cpp
template <class Rep2>
constexpr explicit duration(const Rep2&;
```

- 1 备注（Remarks）：除非 `Rep2` 可隐式转换为 `rep` 且满足以下条件，否则该构造函数不参与重载解析：

- (1.1) --- `test_as_floating_point_v<rep>` 为 true

- (1.2) --- `test_as_floating_point_v<Rep2>` 为 false。

```
[示例:
duration<int, milli> d(3); // OK
duration<int, milli> d(3.5); // error
--- 示例结束]
```

- 2 效果（Effects）：构造一个 `duration` 类型的对象。

后置条件（Postconditions）：`count() = static_cast<rep>(r)`。

```cpp
template <class Rep2, class Period2>
constexpr duration(const Rep2&, Period2&)
```

- 4 备注（Remarks）：除非转换过程中发生溢出且 `test_as_floating_point_v<rep>` 为 true，或者同时 `ratio_divide<Period2, period>::den` 为 1 且 `test_as_floating_point_v<Rep2>` 为 false，否则该构造函数不参与重载解析。[注意：此项要求防止了在基于整数的 duration 类型之间转换时的隐式截断。这种构造很容易导致对 duration 值的混惑。[示例：]

```cpp
duration<int, milli> ms = ms; // OK
duration<int, milli> us = us; // error
--- 示例结束]
```

- 5 效果（Effects）：构造一个 `duration` 类型的对象，其 `struct_rep` 来自 `duration<duration>(d).count()`。

## 23.17.52 duration 观察者 [time.duration.observer]

```cpp
constexpr rep() const;
```

- 1 返回（Returns）：`rep_`。

## 23.17.53 duration 算术 [time.duration.arithmetic]

```cpp
constexpr common_type_t<duration> operator+(*this) const;
```

- 1 返回（Returns）：`common_type_t<duration>(*this)`。

```cpp
constexpr common_type_t<duration> operator() const;
2 返回（Returns）：`common_type_t<duration>(-rep_
constexpr duration& operator++();
3 效果（Effects）：相当于 `++rep_`。
4 返回（Returns）：`*this`。
constexpr duration operator++(int);
5 返回（Returns）：`duration(rep+)`。
constexpr duration& operator--();
6 效果（Effects）：相当于 `--rep_`。
7 返回（Returns）：`*this`。
constexpr duration operator--(int);
8 返回（Returns）：`duration(rep--)`。
constexpr duration& operator+=(const duration& d);
9 效果（Effects）：相当于 `rep_ += d.count()`。
10 返回（Returns）：`*this`。
constexpr duration& operator-=(const duration& d);
11 效果（Effects）：相当于 `rep_ -= d.count()`。
12 返回（Returns）：`*this`。
constexpr duration& operator*=(const rep& rhs);
13 效果（Effects）：相当于 `rep_ *= rhs`。
14 返回（Returns）：`*this`。
constexpr duration& operator/=(const rep& rhs);
15 效果（Effects）：相当于 `rep_ /= rhs`。
16 返回（Returns）：`*this`。
constexpr duration& operator%=(const duration& rhs);
17 效果（Effects）：相当于 `rep_ %= rhs.count()`。
18 返回（Returns）：`*this`。

## 23.17.5.4 duration 特值

```cpp

static constexpr duration zero();

1 返回（Returns）：`duration_values<rep>::zero()`。

static constexpr duration min();

2 返回（Returns）：`duration_values<rep>::min()`。

[time.duration.special]

```cpp
static constexpr duration max();
返回（Returns）：`duration_rep::max()`。

## 23.17.5. duration 非成员算术 [time.duration.member]

在函数描述中，`CT` 代表 `common_type_t<A, B>`，其中 `A` 和 `B` 是参数的类型。

```cpp

template <Class Rep1, Class Period1, Class Rep2, Class Period2>

constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>

operator+(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {

};

```

返回（Returns）：`CD(lhs.count()) + CD(rhs.count())`。

```cpp

template <Class Rep1, Class Period1, Class Rep2, Class Period2>

constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>

operator-(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {

};

```

返回（Returns）：`CD(lhs.count()) - CD(rhs.count())`。

```cpp

template <Class Rep1, Class Period1, Class Rep2, Class Period2>

constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>

operator*(const duration<Rep1, Period1>& d, const Rep2& s) {

};
```
