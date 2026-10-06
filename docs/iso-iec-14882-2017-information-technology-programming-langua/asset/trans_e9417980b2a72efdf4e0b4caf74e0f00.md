

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

## 21.3.5 头文件 <limits> 概要 [climits.syn]

- #define CHAR_BIT 见下
- #define CHAR_MIN 见下
- #define CHAR_MAX 见下
- #define UCHAR_MAX 见下
- #define CHAR_MIN 见下
- #define CHAR_MAX 见下
- #define MB_LEN_MAX 见下
- #define SHRT_MIN 见下
- #define SHRT_MAX 见下
- #define HUNGE_MAX 见下
- #define INT_MIN 见下
- #define INT_MAX 见下
- #define UINT_MAX 见下
- #define LONG_MIN 见下
- #define LONG_MAX 见下
- #define ULONG_MAX 见下
- #define LLONG_MIN 见下
- #define LLONG_MAX 见下
- #define ULONG_MAX 见下

> <limits> 将所有宏定义为 C 标准库头文件 <limits.h>。[注：<limits> 中由宏定义的常量类型不要求与宏所引用的类型匹配。--- 注释结束]

另参见：ISO C 5.2.4.1

## 21.3.6 头文件 <cfloat> 概要 [cfloat.syn]

- #define FLT_ROUNDS 见下
- #define FLT_EVAL_METHOD 见下
- #define FLT_HAS_SUBNORM 见下
- #define DBL_HAS_SUBNORM 见下
- #define FLT_RADIX 见下
- #define FLT_MANT_DIG 见下
- #define DBL_MANT_DIG 见下
- #define LDB_MANT_DIG 见下
- #define FLT_DECIMAL_DIG 见下
- #define DBL_DECIMAL_DIG 见下
- #define LDB_DECIMAL_DIG 见下
- #define FLT_DIG 见下
- #define DBL_DIG 见下
- #define LDB_DIG 见下
- #define FLT_MIN_EXP 见下
- #define DBL_MIN_EXP 见下
- #define LDB_MIN_EXP 见下
- #define FLT_MIN_10_EXP 见下
- #define DBL_MIN_10_EXP 见下
- #define LDB_MIN_10_EXP 见下
- #define FLT_MAX_EXP 见下
- #define DBL_MAX_EXP 见下

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

> 头文件 <float.h> 将所有宏定义为 C 标准库头文件 <float.h>。

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
cpp
using uint_least8_t = 无符号整数类型;
using uint_least16_t = 无符号整数类型;
using uint_least32_t = 无符号整数类型;
using uint_least64_t = 无符号整数类型;
using uint_fast8_t = 无符号整数类型;
using uint_fast16_t = 无符号整数类型;
using uint_fast32_t = 无符号整数类型;
```

```cpp
using int8_t = 符号整数类型;
using int16_t = 符号整数类型;
using int32_t = 符号整数类型;
using int64_t = 符号整数类型;
using uint8_t = 无符号整数类型;
using uint16_t = 无符号整数类型;
using uint32_t = 无符号整数类型;
using uint64_t = 无符号整数类型;
```

1 该头文件定义了大量的宏：
- INT_FAST_LEAST(8 32 64)_MIN
- INT_FAST_LEAST(8 32 64)_MAX
- INTMAX_PTR_MIN
- INTMAX_PTR_MAX
- PTRDIFF_SIZE_MAX
- SIZE_MAX

以及以下形式的：
- INT(8 32 64)_MIN
- INT(8 32 64)_MAX
- UINTMAX_C
- UINTMAX_C

2 该头文件将所有类型和宏定义为与 C 标准库头文件 <stdlib.h> 相同。
另参见：ISO C 7:20

## 21.5 开始与终止

> [注：头文件 <stdlib.h> (21.2.2) 了本子类中的函数。--- 注释结束]

```cpp
[[return]] void exit(int status) noexcept;
```

2 效果：该函数具有标准库语义。

3 备注：程序终止时不会析构自动、线程或静态存储周期的对象，也不会调用传递给 exit(it) 的句 (6.6.4)。_Exit 是信号安全的21.10.4。

```cpp
[[return]] void abort() noexcept;
```

4 效果：该函数具有标准库语义。

5 备注：程序终止时不会析构自动、线程或静态存储周期的对象，也不会调用传递给 exit(it) 的句 (6.6.4)。abort 是信号安全的21.10.4。

```cpp
int atexit(void (*handler)(void)) noexcept;
int atexit_s(void (*handler)(void)) noexcept;
```

6 效果：该函数注册由 f 指向的函数以便在正常程序持续期间无参数调用。在调用 exit(it) 之前 (4.7) 调用 axit() 是否成功是不确定的。[注：atexit() 函数不会引入数据竞态 (20.5.5)。--- 注释结束]

7 实现限制：实现应能够处理至少 32 个函数的注册。

8 返回：exit() 函数在注册时返回零，失败返回非零。

```cpp
[[return]] void exit(int status);
```

9 效果：
— 首先，析构具有线程持续且与当前线程相关的对象。
接下来，析构静态存储周期的对象并调用通过调用 exit 注册的函数¹215 参见 6.6.4 关于析构和调用顺序。（调用 exit(it) 不导致自动对象的析构。²216

215 一个函数每次被注册时都会调用一次。在主函数 (6.6.1) 不包含自动对象的程序中，所有函数都会被析构。

216 自动存储周期的对象被析构

