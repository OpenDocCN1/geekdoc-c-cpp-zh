

tp-=d 将 **tp** 向后移动：**tp.d-=d**
tp2=tp+d tp2=time_point<Clock>{tp.time_since_epoch()+d} tp2=d+tp
tp2=time_point<Clock>{d+tp.time_since_epoch()} tp2=tp-d tp2=time_point<Clock>{tp.time_since_epoch()-d} d=tp-tp2 d=duration{tp.time_since_epoch()-tp2.time_since_epoch()} tp2=tp.min() tp2=time_point(duration::min()); static; constexpr tp2=tp.max() tp2=time_point(duration::max()); static; constexpr tp==tp2
tp.time_since_epoch()==tp2.time_since_epoch() tp!=tp2 !(tp==tp2)
tp<tp2 tp.time_since_epoch()<tp2.time_since_epoch() tp<=tp2 !(tp2<tp)
tp>tp2 tp2<tp
tp>=tp2 !(tp<tp2)

**tp2=time_point_cast<D>(tp)** 将 **time_point** tp 转换为 **time_point<C,D>**：
**time_point<C,D>(duration_cast<D>(t.time_since_epoch()))** 例如：

## Section 35.2.2 time_point 1015

```
void test20() {
  auto tp = steady_clock::now();
  auto d1 = time_point_cast<hours>(tp).time_since_epoch().count()/24; // days since startofepoch

  using days = duration<long,ratio<24*60*60,1>>; // days’ duration
  auto d2 = time_point_cast<days>(tp).time_since_epoch().count(); // days since startofepoch
  if (d1!=d2) cout << "Impossible\n";
}
```

不访问时钟的 **time_point** 操作可以是 **constexpr**，但目前不保证如此。

## 35.2.3 Clocks

**time_point** 和 **duration** 值最终来自硬件时钟。在 **<chrono>** 中，标准库提供了时钟的基本接口。类 **system_clock** 表示从系统实时时钟获得的“墙上时钟时间”：

```
class system_clock {
public:
  using rep = /* implementation-defined signed type*/;
  using period = /* implementation-defined ratio<> */;
  using duration = chrono::duration<rep,period>;
  using time_point = chrono::time_point<system_clock>;
  // …
};
```

所有数据和函数成员都是 **static**。我们不显式处理时钟对象。相反，我们使用时钟类型：

is_steady

## Clock Members (§iso.20.11.7)

此时钟类型是否稳定？
即，对 now() 的所有连续调用是否满足 c.now()<=c.now() 且时钟滴答之间的时间是恒定的？ static

tp=now() tp 是调用时 system_clock 的 time_point； noexcept t=to_time_t(tp) t 是 time_point tp 的 time_t (§43.6)； noexcept tp=from_time_t(t) tp 是 time_t t 的 time_point； noexcept

例如：

```
void test3()
{
auto t1 = system_clock::now();
f(x); // do something
auto t2 = system_clock::now();
cout << “f(x) took ” << duration_cast<milliseconds>(t2-t1).count() << ” ms”;
}
```

系统提供三种命名时钟：

system_clock
steady_clock
high_resolution_clock

## Clock Types (§iso.20.11.7)

系统的实时时钟；系统的时钟可能被重置（向前或向后跳转）以匹配外部时钟 时间稳步向前移动的时钟；即时间不会倒退且时钟滴答之间的时间是恒定的 具有系统上最短时间增量的时钟

这三种时钟不必不同；标准库时钟名称可能是一个别名。我们可以这样确定时钟的基本属性：

```
cout << “min ” << system_clock::duration::min().count() << “, max ” << system_clock::duration::max().count() << “, ” << (treat_as_floating_point<system_clock::duration>::value ? “FP” : “integral”) << ‘\n’;
```

```
cout << (system_clock::is_steady?"steady\n": "not steady\n");
```

当我在其中一台系统上运行它时，得到的结果是：

min -9223372036854775808, max 9223372036854775807, integral not steady

不同系统和不同时钟可能给出不同的结果。

## 35.2.4 Time Traits

chrono 设施的实现依赖于一些标准设施，统称为时间特性。

duration 和 time_point 的转换规则取决于其表示是浮点数（因此允许舍入）还是整数：

```
template<typename Rep>
```

```
struct treat_as_floating_point : is_floating<Rep> { };
```

提供了一些标准值：

```
duration_values<Rep> (siso.20.11.4.2)
```

```
r=zero() r=Rep(0) ; static; constexpr
r=min() r=numeric_limits<Rep>::lowest(); static; constexpr
r=max() r=numeric_limits<Rep>::max(); static; constexpr
```

两个 duration 的公共类型是通过计算它们的最大公约数（GCD）确定的：

```
template<typename Rep1, typename P1, typename Rep2, typename P2>
struct common_type<duration<Rep1,P1>, duration<Rep2, P2>> {
using type = duration<typename common_type<Rep1,Rep2>::type, GCD<P1,P2>> ;
};
```

## Section 35.2.4 Time Traits 1017

这使得 type 成为一个别名，表示具有最大可能滴答周期的 duration，以便两个 duration 参数都可以不经除法运算转换为它。这意味着 common_type<R1,P1,R2,P2>::type 可以在不产生截断误差的情况下容纳 duration<R1,R2> 和 duration<R2,P2> 的任何值。然而，浮点 duration 可能存在舍入误差。

```
template<typename Clock, typename Duration1, typename Duration2>
struct common_type<time_point<Clock,Duration1>, time_point<Clock, Duration2>> { using type = time_point<Clock, typename common_type<Duration1, Duration2>::type>;
};
```

换句话说，要有 common_type，两个 time_point 必须具有共同的时钟类型。它们的 common_type 是具有其 duration 的 common_type 的 time_point。

## 35.3 Compile-Time Rational Arithmetic

在 <ratio> 中，我们找到类 ratio，它提供了编译时有理数运算。标准库使用 ratio 来提供时间 duration 和时间点的编译时表示 (§35.2)：

```
template<intmax_t N, intmax_t D = 1>
struct ratio {
static constexpr intmax_t num;
static constexpr intmax_t den;

using type = ratio<num,den>;
};
```

基本思想是将有理数的分子和分母编码为（值）模板参数。分母必须始终非零。

## ratio Arithmetic Operations (siso.20.10.4)

```
z=ratio_add<x,y> z.num=x::num *y::den+y::num*x::den; z.den=x::den*y::den
```

```
z=ratio_subtract<x,y> z.num=x::num*y::den-y::num*x::den; z.den=x::den*y::den
z=ratio_multiply<x,y> z.num=x::num*y::num; z.den=x::den*y::den
z=ratio_divide<x,y> z.num=x::num*y::den; z.den=x::den*y::num
ratio_equal<x,y> x::num==y::num && x::den==y::den
ratio_not_equal<x,y> !ratio_equal<x,y>::value
ratio_less<x,y> x::num*y::den < y::num*x::den
ratio_less_equal<x,y> !ratio_less<y,x>::value
ratio_not_equal<x,y> !ratio_less<y,x>::value
ratio_greater<x,y> ratio_less<y,x>::value
ratio_greater_equal<x,y> !ratio_less<x,y>::value
```

例如：

```
static_assert(ratio_add<ratio<1,3>, ratio<1,6>>::num == 1, “problem: 1/3+1/6 != 1/2”); static_assert(ratio_add<ratio<1,3>, ratio<1,6>>::den == 2, “problem: 1/3+1/6 != 1/2”); static_assert(ratio_multiply<ratio<1,3>, ratio<3,2>>::num == 1, “problem: 1/3*3/2 != 1/2”); static_assert(ratio_multiply<ratio<1,3>, ratio<3,2>>::den == 2, “problem: 1/3*3/2 != 1/2”);
```

显然，这不是表达数字和算术的方便方式。在 <chrono> 中，我们找到了时间有理数算术的常规记法（例如，+ 和 *） (§35.2)。同样，为了帮助表达单位值，标准库提供了常见的 SI 量级名称：

```
using yocto using zepto using atto using femto using pico using nano using micro
using milli using centi using deci using deca using hecto using kilo
using mega using giga using tera using peta using exa using zetta using yotta =
ratio<1,1000000000000000000000000>; // conditionally supported =
ratio<1,1000000000000000000000>; // conditionally supported =
ratio<1,1000000000000000000>;
= ratio<1,1000000000000000>;
= ratio<1,1000000000000>;
= ratio<1,1000000000>;
= ratio<1,1000000>;
= ratio<1,1000>;
= ratio<1,100>;
= ratio<1,10>;
= ratio<10,1>;
= ratio<100,1>;
= ratio<1000,1>;
= ratio<1000000,1>;
= ratio<1000000000,1>;
= ratio<1000000000000,1>;
= ratio<1000000000000000,1>;
= ratio<1000000000000000000,1>;
= ratio<1000000000000000000000,1>;
= ratio<1000000000000000000000000,1>; // conditionally supported =
ratio<1000000000000000000000000000,1>; // conditionally supported
```

使用示例请参见 §35.2.1。

