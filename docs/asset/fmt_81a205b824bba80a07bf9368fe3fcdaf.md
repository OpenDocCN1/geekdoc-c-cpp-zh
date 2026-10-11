
`static constexpr bool is_exact;`

20 如果该类型使用精确表示法则为真。所有整数类型都是精确的，但并非所有精确类型都是整数。例如，有理数表示和固定指数表示法不是整数。

21 对于所有特化类型都有意义。

`static constexpr int radix;`

22 对于浮点类型，这指定了指数表示的底或基数（通常为 2）。¹193

23 对于整数类型，这指定了表示的基数.¹¹194

24 对于所有特化类型都有意义。

`static constexpr T epsilon() noexcept;`

25 机器精度：1 与大于 1 的可表示最小值之间的差.¹¹195

26 对于所有浮点类型都有意义。

`static constexpr T round_error() noexcept;`

27 最大舍入误差的幅度.¹¹196

`static constexpr int min_exponent;`

28 最小负整数，使得基小于该值的幂是一个归一化浮点数.¹¹197

29 对于所有浮点类型都有意义。

- 191 等于 `FLT_MANT_DIG`, `DBL_MANT_DIG`, `LDB_MANT_DIG`。
- 192 等于 `FLT_DIG`, `DBL_DIG`, `LDB_DIG`。
- 193 等于 `FLT_RADIX`。
- 194 包含基数非 2 的类型（例如 BCD）。
- 195 等于 `FLT_EPSILON`, `DBL_EPSILON`, `LDB_EPSILON`。
- 196 舍入误差见 LIA-1 第 5.2.4 节和附录 C C5.2.4 — 舍入与常量。
- 197 等于 `FLT_MIN_EXP`, `DBL_MIN_EXP`, `LDB_MIN_EXP`。

`static constexpr int min_exponent10;`

最小负整数，使得 10 的该值幂处于归一化浮点数的范围内。^{196}

对于所有浮点类型都有意义。

`static constexpr int max_exponent;`

最大正整数，使得基数小于该值的幂是一个可表示的有限浮点数。^{199}

对于所有浮点类型都有意义。

`static constexpr int max_exponent10;`

最大正整数，使得 10 的该值幂处于可表示的有限浮点数的范围内。^{200}

对于所有浮点类型都有意义。

`static constexpr bool has_infinity;`

如果该类型具有正无穷的表示则为真。

对于所有浮点类型都有意义。

对于所有 `is_iec559 == false` 的特化类型，应为真。

`static constexpr bool has_quiet_NaN;`

如果该类型具有静默（非信号）“非数字”（Not a Number）表示则为真²⁰¹

对于所有浮点类型都有意义。

对于所有 `is_iec559 == false` 的特化类型，应为真。

`static constexpr bool has_signaling_NaN;`

如果该类型具有信号“非数字”（Not a Number）表示则为真²⁰²

对于所有浮点类型都有意义。

对于所有 `is_iec559 == false` 的特化类型，应为真。

`static constexpr float_denom_style has_denom;`

如果该类型允许次规格值（可变指数位宽）²⁰³，则 `denom_present`；如果该类型不允许次规格值，则 `denom_absent`；如果在编译时无法确定该类型是否允许次规格值，则为 `denom_indeterminate`。

对于所有浮点类型都有意义。

`static constexpr bool has_denom_loss;`

如果损失发生在去规格化过程中，而不是作为不精确的结果，则为真²⁰⁴。

`static constexpr T infinity() noexcept;`

正无穷的表示，如果存在²⁰⁵

对于所有 `has_infinity != false` 的特化类型都有意义。在 `is_iec559 != false` 的特化类型中是强制性**的。

`static constexpr T quiet_NaN() noexcept;`

“非数字”（Not a Number）的表示，如果存在²⁰⁶

对于所有 `is_iec559 != false` 的特化类型都有意义。

`static constexpr T signaling_NaN() noexcept;`

“非数字”（Not a Number）的表示，如果存在²⁰⁷

对于所有特化类型都有意义。对于 `is_iec559 != false` 的类型是强制性的。

`static constexpr T denom_min()`

最小次规格值。²⁰⁸

对于所有浮点类型都有意义。

`static constexpr bool is_iec59;`

如果该类型遵循 ISO/IEC 60559²⁰⁹

对于所有浮点类型都有意义。

`static constexpr bool is_bounded;`

如果该类型是有限的则为真²¹⁰

对于所有特化类型都有意义。

`static constexpr bool is_module;`

如果存在模运算（modulo）则为真²¹¹

对于所有特化类型都有意义。

`static constexpr bool is_trap;`

如果发生溢出则为真²¹²

对于所有特化类型都有意义。

- 213 参考 ISO/IEC 60559。LIA-1 要求。
- 214 等于 `FLT_ROUNDS`。²¹⁵ LIA-1 要求。
- 216 LIA-1 要求。
- 217 LIA-1 要求。
- 218 LIA-1 要求。

# ISO/IEC 14882:2017(E)

```cpp
static constexpr float signaling_nan() noexcept { return value; }

static constexpr float denom_min() noexcept { return min(); }

static constexpr bool is_ec559 = true;

static constexpr bool is_bounded = true;

static constexpr bool is_modulo = false;

static constexpr bool traps = true;

static constexpr bool tininess_before = true;

static constexpr float_round_style round_style = round_to_nearest;
}
```

-- 示例结束
3. bool 的规范应所示：

```cpp
namespace std {
template<class numeric_limits<bool>> {
public:
    static constexpr bool is_specialized = true;
    static constexpr bool min() noexcept { return false; }
    static constexpr bool max() noexcept { return true; }
    static constexpr bool lowest() noexcept { return false; }
    static constexpr int digits = 1;
    static constexpr int digits10 = 0;
    static constexpr int max_digits10 = 0;
    static constexpr bool is_signed = false;
    static constexpr bool is_integer = true;
    static constexpr bool is_exact = true;
    static constexpr int epsilon() noexcept { return 2; }
    static constexpr bool round_error() noexcept { return 0; }
    static constexpr int min_exponent = 0;
    static constexpr int min_exponent10 = 0;
    static constexpr int max_exponent = 0;
    static constexpr int max_exponent10 = 0;
    static constexpr bool has_infinity = false;
    static constexpr bool has_quiet_NaN = false;
    static constexpr bool has_signaling_NaN = false;
    static constexpr float denom_denom_style_has_denom = denom_absent;
    static constexpr bool has_den = false;
    static constexpr bool infinity() noexcept { return 0; }
    static constexpr bool quiet_NaN() noexcept { return 0; }
    static constexpr bool signaling_NaN() noexcept { return 0; }
    static constexpr bool denom_min() noexcept { return 0; }
    static constexpr bool is_ec559 = false;
    static constexpr bool is_bounded = true;
    static constexpr bool is_modulo = false;
    static constexpr bool traps = false;
    static constexpr bool tininess_before = false;
```

```cpp
static constexpr float_round_style round_style = round_toward_zero;
}
```

### 21.3.5 头文件 <limits> 概要 [climits.syn]

- `#define CHAR_BIT` 见下
- `#define CHAR_MIN` 见下
- `#define CHAR_MAX` 见下
- `#define UCHAR_MAX` 见下
- `#define CHAR_MIN` 见下
- `#define CHAR_MAX` 见下
- `#define MB_LEN_MAX` 见下
- `#define SHRT_MIN` 见下
- `#define SHRT_MAX` 见下
- `#define HUNGE_MAX` 见下
- `#define INT_MIN` 见下
- `#define INT_MAX` 见下
- `#define UINT_MAX` 见下
- `#define LONG_MIN` 见下
- `#define LONG_MAX` 见下
- `#define ULONG_MAX` 见下
- `#define LLONG_MIN` 见下
- `#define LLONG_MAX` 见下
- `#define ULONG_MAX` 见下

> `<limits>` 将所有宏定义为 C 标准库头文件 `<limits.h>`。[注：`<limits>` 中由宏定义的常量类型不要求与宏所引用的类型匹配。--- 注释结束]

另参见：ISO C 5.2.4.1

### 21.3.6 头文件 <cfloat> 概要 [cfloat.syn]

- `#define FLT_ROUNDS` 见下
- `#define FLT_EVAL_METHOD` 见下
- `#define FLT_HAS_SUBNORM` 见下
- `#define DBL_HAS_SUBNORM` 见下
- `#define FLT_RADIX` 见下
- `#define FLT_MANT_DIG` 见下
- `#define DBL_MANT_DIG` 见下
- `#define LDB_MANT_DIG` 见下
- `#define FLT_DECIMAL_DIG` 见下
- `#define DBL_DECIMAL_DIG` 见下
- `#define LDB_DECIMAL_DIG` 见下
- `#define FLT_DIG` 见下
- `#define DBL_DIG` 见下
- `#define LDB_DIG` 见下
- `#define FLT_MIN_EXP` 见下
- `#define DBL_MIN_EXP` 见下
- `#define LDB_MIN_EXP` 见下
- `#define FLT_MIN_10_EXP` 见下
- `#define DBL_MIN_10_EXP` 见下
- `#define LDB_MIN_10_EXP` 见下
- `#define FLT_MAX_EXP` 见下
- `#define DBL_MAX_EXP` 见下

```cpp
#define LDB_MAX_EXP 见下
#define FLT_10_EXP 见下
#define LDB_MAX_10_EXP 见下
#define FLT_MAX 见下
#define DBL_MAX 见下
#define LDB_MAX 见下
#define FLT_EPSILON 见下
#define DBL_EPSILON 见下
#define LDB_EPSILON 见下
#define FLT_MIN 见下
#define DBL_MIN 见下
#define LDB_MIN 见下
#define FLT_TRUE_MIN 见下
#define DBL_TRUE_MIN 见下
#define LDB_TRUE_MIN 见下
```

> 头文件 `<float.h>` 将所有宏定义为 C 标准库头文件 `<float.h>`。

另参见：ISO C 5.2.4.2

## 21.4 整数类型

### 21.4.1 头文件 <stdint> 概要

```cpp
using int8_t = 符号整数类型;
using int16_t = 符号整数类型;
using int32_t = 符号整数类型;
using int64_t = 符号整数类型;
```

```cpp
using int_fast8_t = 符号整数类型;
using int_fast16_t = 符号整数类型;
using int_fast32_t = 符号整数类型;
using int_fast64_t = 符号整数类型;
```

```cpp
using int_least8_t = 符号整数类型;
using int_least16_t = 符号整数类型;
using int_least32_t = 符号整数类型;
using int_least64_t = 符号整数类型;
```

```cpp
using intmax_t = 符号整数类型;
using intptr_t = 符号整数类型;
```

```cpp
using uint8_t = 无符号整数类型;
using uint16_t = 无符号整数类型;
using uint32_t = 无符号整数类型;
using uint64_t = 无符号整数类型;
```

```cpp
using uint_fast8_t = 无符号整数类型;
using uint_fast16_t = 无符号整数类型;
using uint_fast32_t = 无符号整数类型;
using uint_fast64_t = 无符号整数类型;
```

```cpp
using uint_least8_t = 无符号整数类型;
using uint_least16_t = 无符号整数类型;
using uint_least32_t = 无符号整数类型;
using uint_least64_t = 无符号整数类型;
```

```cpp
using uintmax_t = 无符号整数类型;
using uintptr_t = 无符号整数类型;
```

```cpp
using int_least8_t = 符号整数类型;
using int_least16_t = 符号整数类型;
using int_least32_t = 符号整数类型;
using int_least64_t = 符号整数类型;
using int_fast8_t = 符号整数类型;
using int_fast16_t = 符号整数类型;
using int_fast32_t = 符号整数类型;
```
```cpp
using uint_least8_t = 无符号整数类型;
using uint_least16_t = 无符号整数类型;
using uint_least32_t = 无符号整数类型;
using uint_least64_t = 无符号整数类型;
using uint_fast8_t = 无符号整数类型;
using uint_fast16_t = 无符号整数类型;
using uint_fast32_t = 无符号整数类型;
```
