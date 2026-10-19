
#define __cpp_lib_optional 201606L // also in <optional>
#define __cpp_lib_parallel_algorithm 201603L // also in <algorithm>, <numeric>
#define __cpp_lib_polymorphic_allocator 201902L // also in <memory>
#define __cpp_lib_quoted_string_io 201304L // also in <iomanip>
#define __cpp_lib_ranges 201911L
// also in <algorithm>, <functional>, <iterator>, <memory>, <ranges>
#define __cpp_lib_raw_memory_algorithms 201606L // also in <memory>
#define __cpp_lib_remove_cvref 201711L // also in <type_traits>
#define __cpp_lib_result_of_sfinae 201210L // also in <functional>, <type_traits>
#define __cpp_lib_robust_nonmodifying_seq_ops 201304L // also in <algorithm>
#define __cpp_lib_sample 201603L // also in <algorithm>
#define __cpp_lib_scoped_lock 201703L // also in <mutex>
#define __cpp_lib_semaphore 201907L // also in <semaphore>
#define __cpp_lib_shared_mutex 201505L // also in <shared_mutex>
#define __cpp_lib_shared_ptr_arrays 201707L // also in <memory>
#define __cpp_lib_shared_weak_type 201606L // also in <memory>
#define __cpp_lib_shared_timed_mutex 201402L // also in <shared_mutex>
#define __cpp_lib_shift 201806L // also in <algorithm>
#define __cpp_lib_smart_ptr_for_overwrite 202002L // also in <memory>
#define __cpp_lib_source_location 201907L // also in <source_location>
#define __cpp_lib_span 202002L // also in <span>
#define __cpp_lib_ssize 201902L // also in <iterator>
#define __cpp_lib_starts_ends_with 201711L // also in <string>, <string_view>
#define __cpp_lib_string_udls 201304L // also in <string>
#define __cpp_lib_string_view 201803L // also in <string>, <string_view>
#define __cpp_lib_syncbuf 201803L // also in <sstream>
#define __cpp_lib_three_way_comparison 201907L // also in <compare>
#define __cpp_lib_to_address 201711L // also in <memory>
#define __cpp_lib_to_array 201907L // also in <array>
#define __cpp_lib_to_chars 201611L // also in <charconv>
#define __cpp_lib_transformation_trait_aliases 201304L // also in <type_traits>
#define __cpp_lib_transparent_operators 201510L // also in <memory>, <functional>
#define __cpp_lib_tuple_element_t 201402L // also in <tuple>
#define __cpp_lib_tuples_by_type 201304L // also in <utility>, <tuple>
#define __cpp_lib_type_identity 201806L // also in <type_traits>
#define __cpp_lib_type_trait_variable_templates 201510L // also in <type_traits>
#define __cpp_lib_uncaught_exceptions 201411L // also in <exception>
#define __cpp_lib_unordered_map_try_emplace 201411L // also in <unordered_map>
#define __cpp_lib_unwrap_ref 201811L // also in <type_traits>
#define __cpp_lib_variant 201606L // also in <variant>
#define __cpp_lib_void_t 201411L // also in <type_traits>

## 17.3.3 头文件 <limits> 摘要 [limits.syn]

```
namespace std {
  // 17.3.4, floating-point type properties
  enum float_round_style;
  enum float_denorm_style;

  // 17.3.5, class template numeric_limits
  template<class T> class numeric_limits;

  template<class T> class numeric_limits<const T>;
  template<class T> class numeric_limits<volatile T>;
  template<class T> class numeric_limits<const volatile T>;

  template<> class numeric_limits<bool>;

  template<> class numeric_limits<char>;
  template<> class numeric_limits<signed char>;
  template<> class numeric_limits<unsigned char>;
  template<> class numeric_limits<char8_t>;
  template<> class numeric_limits<char16_t>;
  template<> class numeric_limits<char32_t>;
  template<> class numeric_limits<wchar_t>;
```

```
template<> class numeric_limits<short>;
template<> class numeric_limits<int>;
template<> class numeric_limits<long>;
template<> class numeric_limits<long long>;
template<> class numeric_limits<unsigned short>;
template<> class numeric_limits<unsigned int>;
template<> class numeric_limits<unsigned long>;
template<> class numeric_limits<unsigned long long>;

template<> class numeric_limits<float>;
template<> class numeric_limits<double>;
template<> class numeric_limits<long double>;
}
```

## 17.3.4 浮点类型属性 [fp.style]

### 17.3.4.1 类型 float_round_style [round.style]

```
namespace std {
  enum float_round_style {
    round_indeterminate = -1,
    round_toward_zero   =  0,
    round_to_nearest    =  1,
    round_toward_infinity   =  2,
    round_toward_neg_infinity =  3
  };
}
```

1 浮点运算的舍入模式由以下值表征：

- (1.1) — 如果舍入方式不可确定，则为 round_indeterminate
- (1.2) — 如果舍入方式为向零舍入，则为 round_toward_zero
- (1.3) — 如果舍入方式为舍入到最近的可表示值，则为 round_to_nearest
- (1.4) — 如果舍入方式为向正无穷舍入，则为 round_toward_infinity
- (1.5) — 如果舍入方式为向负无穷舍入，则为 round_toward_neg_infinity

### 17.3.4.2 类型 float_denorm_style [denorm.style]

```
namespace std {
  enum float_denorm_style {
    denorm_indeterminate = -1,
    denorm_absent = 0,
    denorm_present = 1
  };
}
```

1 次正规数（指数位数量可变）的存在与否由以下值表征：

- (1.1) — 如果无法确定该类型是否允许次正规值，则为 denorm_indeterminate
- (1.2) — 如果该类型不允许次正规值，则为 denorm_absent
- (1.3) — 如果该类型允许次正规值，则为 denorm_present

## 17.3.5 类模板 numeric_limits [numeric.limits]

### 17.3.5.1 概述 [numeric.limits.general]

1 numeric_limits 类模板为 C++ 程序提供有关实现表示算术类型的各种属性的信息。

```
namespace std {
  template<class T> class numeric_limits {
  public:
    static constexpr bool is_specialized = false;
    static constexpr T min() noexcept { return T(); }
    static constexpr T max() noexcept { return T(); }
    static constexpr T lowest() noexcept { return T(); }
```

对所有浮点类型都有意义。

```
static constexpr int min_exponent10;
```

最小的负整数，使得 10 的该次幂处于规范化浮点数的范围内。[^199]

对所有浮点类型都有意义。

```
static constexpr int max_exponent;
```

最大的正整数，使得基数的（该整数减 1）次幂为可表示的有限浮点数。[^200]

对所有浮点类型都有意义。

```
static constexpr int max_exponent10;
```

最大的正整数，使得 10 的该次幂处于可表示的有限浮点数的范围内。[^201]

对所有浮点类型都有意义。

```
static constexpr bool has_infinity;
```

如果该类型具有正无穷的表示，则为 true。

对所有浮点类型都有意义。

对于所有 `is_iec559 != false` 的特化，应为 true。

```
static constexpr bool has_quiet_NaN;
```

如果该类型具有静默（非信号）“非数”的表示，则为 true。[^202]

对所有浮点类型都有意义。

对于所有 `is_iec559 != false` 的特化，应为 true。

```
static constexpr bool has_signaling_NaN;
```

如果该类型具有信号“非数”的表示，则为 true。[^203]

对所有浮点类型都有意义。

对于所有 `is_iec559 != false` 的特化，应为 true。

```
static constexpr float_denorm_style has_denorm;
```

如果该类型允许次正规值（指数位数量可变）[^204]，则为 `denorm_present`；如果该类型不允许次正规值，则为 `denorm_absent`；如果在编译时无法确定该类型是否允许次正规值，则为 `denorm_indeterminate`。

对所有浮点类型都有意义。

```
static constexpr bool has_denorm_loss;
```

如果精度损失被检测为非规范化损失而不是不精确结果，则为 true。[^205]

```
static constexpr T infinity() noexcept;
```

正无穷的表示（如果可用）。[^206]

对于所有 `has_infinity != false` 的特化有意义。在 `is_iec559 != false` 的特化中为必需。

[^199]: 等价于 FLT_MIN_10_EXP、DBL_MIN_10_EXP、LDBL_MIN_10_EXP。
[^200]: 等价于 FLT_MAX_EXP、DBL_MAX_EXP、LDBL_MAX_EXP。
[^201]: 等价于 FLT_MAX_10_EXP、DBL_MAX_10_EXP、LDBL_MAX_10_EXP。
[^202]: LIA-1 要求。
[^203]: LIA-1 要求。
[^204]: LIA-1 要求。
[^205]: 参见 ISO/IEC/IEEE 60559。
[^206]: LIA-1 要求。
