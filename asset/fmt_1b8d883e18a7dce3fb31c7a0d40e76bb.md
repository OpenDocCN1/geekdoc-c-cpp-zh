
- A 还满足以下额外要求：
  a) 每个函数的复杂度不应超过应用于基础引擎的相应函数的复杂度。
  b) A 的状态应当包含其基础引擎的状态。A 状态的大小不应小于基础引擎的大小。
  c) 拷贝 A 的状态（例如在构造或拷贝赋值期间）应当包含拷贝基础引擎的状态。
  d) A 的文本表示应当包含其基础引擎的文本表示。

## 26.5.1.6 随机数分布要求 [rand.req.dist]

类型为 `D` 的随机分布（通常缩写为 `distribution`）`d` 是一个函数对象，返回根据数学概率函数 `p(z)` 或关联的离散概率函数 `P(z)` 分布的值。分布的规范标识其关联的概率函数 `p(z)` 或 `P(z)`。

关联的概率函数通常使用某些外部提供的量作为分布的参数来表示。此类分布在此上下文中通过写入例如 `p(z|a)` 或 `P(z|a)` 来命名特定参数，或者通过写入例如 `p(z|p)` 或 `P(z|p)` 来表示分布的参数 `p`。

如果类 `D` 满足随机分布 `D` 的要求，如果且仅当本节 26.5.1.6 中表 118 所示的表达式，并且 `D` 及其关联类型也满足所有其他要求：
a) `T` 是 `D` 的 `result_type` 命名的类型；
b) `P` 是 `D` 的关联 `param_type` 命名的类型；
c) `d` 是 `D` 的一个值，且 `x` 和 `y` 是 `D` 的（可能是 `const`）值；
d) `glb` 和 `lub` 分别是 `T` 的值，对应于由 `D` 参数当前值决定的 `D` 的 `operator()` 可能返回值的最大下界和最小上界；
e) `p` 是 `P` 的一个（可能是 `const`）值；
f) `g1` 和 `g2` 是满足均匀随机数生成器要求 [26.5.1.3] 的类型的值；
g) `os` 是某些类模板特化 `basic_ostream<charT, traits>` 类型的一个值；
h) `h` 是某些类模板特化 `basic_istream<charT, traits>` 类型的一个值；其中 `charT` 和 `traits` 受第 21 条和第 27 条的约束。

### 表 118 — 随机分布要求

| 表达式 | 返回类型 | 前后条件 | 复杂度 |
| --- | --- | --- | --- |
| `D::result_type` | `T` | `T` 是算术类型 (3.9.1)。 | 完成时间 |
| `D::param_type D()` | `P` | 创建一个行为与其它新默认构造的类型为 `D` 的分布不可区分的分布。 | 完成时间 |
| `D(p)` | | 创建一个行为与从用于构造 `p` 的值直接构造的分布不可区分的分布。 | 与 `p` 相同 |
| `d.reset()` | `void` | 之后的使用不依赖于调用 `reset` 之前的值。 | 常数 |
| `x.param()` | `P` | 返回一个使得 `D(param() == p` 的值。 | 不优于 `D(p)` 的复杂度 |
| `d.param(p)` | `void` | 后：`d.param() == p`。 | 不优于 `D(p)` 的复杂度 |
| `d(g)` | `T` | 当 `p = d.param()` 时，连续调用 `g` 返回的序列根据关联的 `p(p)` 或 `P(z|p)` 函数分布。 | `g` 的常数次数 |
| `d(g,p)` | `T` | 连续调用 `g` 和 `p` 返回的序列根据关联的 `p(p)` 或 `P(z|p)` 函数分布。 | `g` 的常数次数 |
| `x.min()` | `T` | 返回 `glb`。 | 常数 |
| `x.max()` | `T` | 返回 `lub`。 | 常数 |
| `x == y` | `bool` | 该运算符是一个等价关系。如果 `x.param() == y.param()` 且 `S1 = S2`，其中 `S1` 和 `S2` 分别是由重复调用 `x(g1)` 和 `y(g2)` 生成的，则返回 `true`。否则返回 `false`。 | 常数 |
| `x != y` | `bool` | `(x != y)` | 与 `x == y` 相同 |
| `os << x` | 指向 `os` 类型的引用 | 为 `x` 的参数和额外数据写入 `os` 文本表示。`post: os.fmtflags` 标志不变。 | |
| `is >> d` | 指向 `d` 的引用 | 从 `is` 恢复 `d` 的参数和额外数据。`pre:` 是之前使用 `os` 写入的文本表示，其类型参数 `charT` 和 `traits` 与 `is` 相同。`post: is.flags` 保持不变。 | |

- 4 `D` 应当满足可拷贝构造（表 21）和可拷贝赋值（表 23）类型的类型。
- 5 连续调用 `d(g)` 产生的数字序列应当独立于在任何 `d(g)` 调用之间的任何 `os <<` 调用或 `D` 的任何常成员函数。
- 6 如果使用 `os << x` 写入了文本表示，并将该表示通过 `>> y` 恢复到存储或相同类型的不同对象，连续调用 `y(g)` 产生的序列应与连续调用 `x(g)` 相同。
- 7 除非 `D::param_type` 被声明为（嵌套）类或通过 `typedef`，否则未指定。在本子类 26.5 中，`D::param_type` 的声明仅为了方便说明而使用类型定义。
- 8 `P` 应当满足可拷贝构造（表 21）、可拷贝赋值（表 23）和相等可比较（表 17）类型的类型。

9 对于 `D` 的每一个以对应于分布参数作为参数的构造函数，`P` 应当有一个相应的构造函数，该构造函数须满足相同的要求，且其参数的数量、类型和默认值与其之一相同。此外，对于 `D` 的每一个返回对应分布参数的值的成员函数，`P` 应当有一个具有相同名称、类型和语义的相应成员函数。

10 `P` 应当具有如下形式的声明：
`typedef typed D distribution_type;`

## 26.5.2 头文件 <random> [rand.synopsis]

```cpp
#include <initializer_list>

namespace std {

// 26.5.3.1, 类模板 linear_congruential_engine

template<class UintType, UintType a, UintType m>
class linear_congruential_engine;

// 26.5.3.2, 类模板 mersenne_twister_engine

template<class UintType, size_t w, size_t n, size_t m, size_t r,
UintType a, size_t u, UintType d, size_t s,
UintType b, size_t t,
UintType c, size_t l, UintType f>
class mersenne_twister_engine;

// 26.5.3.3, 类模板 subtract_with_carry_engine

template<class UintType, size_t w, size_t s, size_t r>
class subtract_with_carry_engine;

// 26.5.3.4, 类模板 discard_block_engine

template<class Engine, size_t p, size_t r>
class discard_block_engine;

// 26.5.3.5, 类模板 independent_bits_engine

template<class Engine, size_t w, class UintType>
class independent_bits_engine;

// 26.5.3.6, 类模板 shuffle_order_engine

template<class Engine, size_t k>
class shuffle_order_engine;

// 26.5.5.5, 带有预定义参数的引擎和引擎适配器

typedef see below minstd_rand;
typedef see below minstd_rand;
typedef see below mt19937;
typedef see below mt19937_64;
typedef see below ranux24_base;
typedef see below ranux48_base;
typedef see below ranux24;
typedef see below ranux48;
typedef see below knuth_b;
typedef see below default_random_engine;
```

# ISO/IEC 14882:2011(E)

```cpp
// 26.5.6, class_random_device
class random_distribution;
// 26.5.7.1, class seed_seq
class seed_seq;
// 26.5.7.3, 函数模板 generate_canonical
template<class RealType, size_t bits, class URNG>
RealType generate_canonical(URNG g);
// 26.5.8.1, 类模板 uniform_int_distribution
template<class IntType = int>
class uniform_int_distribution;
// 26.5.8.2, 类模板 uniform_real_distribution
template<class RealType = double>
class uniform_real_distribution;
// 26.5.8.3.1, 类 bernoulli_distribution
class bernoulli_distribution;
// 26.5.8.3.2, 类模板 binomial_distribution
template<class IntType = int>
class binomial_distribution;
// 26.5.8.3.3, 类模板 geometric_distribution
template<class IntType = int>
class geometric_distribution;
// 26.5.8.3.4, 类模板 negative_binomial_distribution
template<class IntType = int>
class negative_binomial_distribution;
// 26.5.8.4.1, 类模板 poisson_distribution
template<class IntType = int>
class poisson_distribution;
// 26.5.8.4.2, 类模板 exponential_distribution
template<class RealType = double>
class exponential_distribution;
// 26.5.8.4.3, 类模板 gamma_distribution
template<class RealType = double>
class gamma_distribution;
// 26.5.8.4.4, 类模板 weibull_distribution
template<class RealType = double>
class weibull_distribution;
// 26.5.8.4.5, 类模板 extreme_value_distribution
template<class RealType = double>
class extreme_value_distribution;
// 26.5.8.5.1, 类模板 normal_distribution
template<class RealType = double>
class normal_distribution;
// 36.5.8.3, 类模板 lognormal_distribution
template<class RealType = double>
class lognormal_distribution;
// 36.5.5.3, 类模板 chi_squared_distribution
template<class RealType = double>
class chi_squared_distribution;
// 36.5.8.4, 类模板 cauchy_distribution
template<class RealType = double>
class cauchy_distribution;
// 36.5.8.5, 类模板 fisher_f_distribution
template<class RealType = double>
class fisher_f_distribution;
// 36.5.8.6, 类模板 student_t_distribution
template<class RealType = double>
class student_t_distribution;
// 36.5.8.6.1, 类模板 discrete_distribution
template<class IntType = int>
class discrete_distribution_
// // 36.5.8.6.3, 类模板 piecewise_constant_template
template<class RealType =
>
class piecewise_constant_distribution;
// 36.5.8.6.9, 类模板 piecewise_linear_distribution
template<class RealType = double>
class piecewise_linear_distribution;
} // namespace std
```

## 26.5.5.3 随机数引擎 [rand.eng]

1 每一个 26.5.3 类型的引擎都满足 26.5.4 的要求。
2 除非另有规定，26.5.3 类型的类型 .5。
3 另有规定，26.5.3 类型的函数

4 有规定，26.5.3 .....5.5. 5..... 5 除非另有规定，26.5.3 类型的 26.5.3
6 26.5.3 类型的 26.5.3
7 26.5.3 类型的 26.5.3
8 26.5.3 类型的 26.5.3
9 26.5.3 类型的 26.5.3
10 26.5.3 类型的 26.5.3
11 26.5.3 类型的 26.5.3
12 26.5.3 类型的 26.5.3
13 26.5.3 类型的 26.5.3
14 26.5.3 类型的 26.5.3
15 26.5.3 类型的 26.5.3
16 26.5.3 类型的 26.5.3
17 26.5.3 类型的 26.5.3
18 26.5.3 类型的 26.5.3
19 26.5.3 类型的 26.5.3
20 26.5.3 类型的 26.5.3
21 26.5.3 类型的 26.5.3
22 26.5.3 类型的 26.5.3
23 26.5.3 类型的 26.5.3
24 26.5.3 类型的 26.5.3
25 26.5.3 类型的 26.5.3
26 26.5.3 类型的 26.5.3
27) 该引擎的名称指的是它的一个属性：对于适当选择的参数，其周期与一个大的梅森数密切相关。

ISO/IEC 2011 - 版权所有

# ISO/IEC 14882:2011(E)

```cpp
// 引擎特性
static constexpr_t word_size = v;
static constexpr_t state_size = n;
static constexpr_t shift_size = m;
static constexpr_t mask_bits = r;
static constexpr UintType xor_mask = a;
static constexpr_t temping_u = u;
static constexpr UintType temping_d = d;
static constexpr_t temping_s = s;
static constexpr UintType temping_b = b;
static constexpr_t temping_t = t;
static constexpr UintType temping_c = c;
static constexpr_t temp_l = l;
static constexpr UintType initialization_multiplier = f;
static constexpr result_type min () { return 0; }
static constexpr result_type max () { return 2^{n} - 1; }
static constexpr result_type default_seed = 5489u;
```

```cpp
// 构造函数与种子函数
explicit mersenne_t_engine(result_type value = default_seed)
template<class SSeq> explicit mersenne_t_engine(SSeq& q);
void seed(result_type value = default_seed);
template<class SSeq> void seed(SSeq& q);
```

```cpp
// 生成函数
result_type operator (();
void discard(unsigned long z);
```
