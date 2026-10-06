

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

备注（Remarks）：除非 `Rep2` 可隐式转换为 `CR`，否则该运算符不参与重载解析。
返回（Returns）：`CD(d.count()) * s`。

```cpp
template <Class Rep1, Class Period1, Class Rep2>
constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator/(const duration<Rep1, Period1>& d, const Rep2& s) {
};
```

备注（Remarks）：除非 `Rep2` 可隐式转换为 `CR`，否则该运算符不参与重载解析。
返回（Returns）：`CD(d.count()) / s`。

```cpp
template <Class Rep1, Class Period1, Class Rep2, Class Period2>
constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator/(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

返回（Returns）：`CD(lhs.count()) / CD(rhs.count())`。

```cpp
template <Class Rep1, Class Period1, Class Rep2>
constexpr common_type<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator%(const duration<Rep1, Period1>& d, const Rep2& s) {
};
```

备注（Remarks）：除非 `Rep2` 可隐式转换为 `CR` 且 `Rep2` 不是 `duration` 的特化版本，否则该运算符不参与重载解析。
返回（Returns）：`CD(d.count()) % s`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr common_type_t<duration<Rep1, Period1>, duration<Rep2, Period2>>
operator!(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

返回（Returns）：`CD(lhs.count()) % CD(rhs.count())`。

## 23.17.5 比较

- 1 在函数中，`CT` 代表 `common_type_t<A, B>`，其中 `A` 和 `B` 是参数的类型：

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator==(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 2 返回（Returns）：`CT(lhs.count()) == CT(rhs.count())`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator>(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 3 返回（Returns）：`!(lhs == rhs)`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator<(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 4 返回（Returns）：`CT(lhs.count()) < CT(rhs.count())`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator<=(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 5 返回（Returns）：`!(lhs < rhs)`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator>=(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 6 返回（Returns）：`lhs < rhs`。

```cpp
template <class Rep1, class Period1, class Rep2, class Period2>
constexpr bool operator!=(const duration<Rep1, Period1>& lhs, const duration<Rep2, Period2>& rhs) {
};
```

- 7 返回（Returns）：`!(lhs >= rhs)`。

## 23.17.5 duration_cast

```cpp
template <class ToDuration, class Rep, class Period>
constexpr ToDuration duration_cast(const duration<Rep, Period>& d);
```

- 1 备注（Remarks）：除非 `ToDuration` 是 `duration` 的特化版本，否则该函数不参与重载解析。
- 2 返回（Returns）：设 `CF` 为 `ratio_divide(period)`，`CR` 为 `ToDuration::rep`。如果 `CF::num == 1` 且 `den == 1`，返回 `ToDuration(static_cast<ToDuration::rep>(d.count()))`。

```cpp
否则，如果 `CF::num != 1` 且 `den == 1`，返回 `ToDuration(static_cast<CR>(d.count()))`。
```

```
否则，如果 `CF::num == 1` 且 `den == 1`，返回 `static_cast<CR>(d.count())`。
```

```
否则，注意：此函数不使用任何隐式转换；所有转换通过 `static_cast` 完成。中间计算在最宽表示中进行，最后仅转换为目标表示。

```cpp
template <class ToDuration, class Rep, class Period>
constexpr Period floor(const duration<Rep, Period>& d); // 根据上下文修正的签名
```

备注（Remarks）：除非 `ToDuration` 是 `duration` 的特化版本，否则该函数不参与重载解析。
返回（Returns）：`ToDuration` 中满足 `t <= d` 的最大值。

```cpp
template <class ToDuration, class Rep, class Period>
constexpr Period ceil(const duration<Rep, Period>& d);
```

备注（Remarks）：除非 `ToDuration` 是 `duration` 的特化版本，否则该函数不参与重载解析。
返回（Returns）：`ToDuration` 中满足 `t >= d` 的最小值。

```cpp
template <class ToDuration, class Rep, class Period>
constexpr Period round(const duration<Rep, Period>& d);
```

备注（Remarks）：除非 `ToDuration` 是 `duration` 的特化版本，且 `treat_as_floating_point<typename ToDuration::rep>` 为 false。
返回（Returns）：距离 `d` 最近的 `ToDuration` 值。如果存在两个最近，返回 `t % 2 == 0` 的那个。

## 23.17.5-8 duration 字面量的后缀 [time::duration::ms,]

- 1 本节描述了构造 duration 字面量的后缀。当 h, min, s, us, ns 后缀应用于整数字面量时，对应的小时、分钟、秒、毫秒、微秒和纳秒值会被保留。
- 2 如果将这些后缀之一应用于浮点数字面量，结果是具有未指定浮点表示的 `chrono::literal`。
- 3 如果将这些后缀之一应用于整数字面量，且生成的 `chrono::duration` 值因溢出无法在结果类型中表示，则程序格式错误。
- 4 下面示例显示了某些 duration 字面量。
using namespace std::chrono_literals;
auto constexpr aday=24h;
auto constexpr lesson=45min;
auto constexpr halfhour=0.5h;
-- 示例结束 --

