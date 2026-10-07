
- a) 通过初始化，将范围内的每个元素设置为值 `0x8b8b8b8b`。此外，在子集中使用，设置 `t = (n >= 623) ? 1 : (n >= 68) ? (n >= 39) ? 5 : (n >= 7) ? 3 : (n - 1)/2`；

- b) 以 `m` 为 `s+1` 和 `n` 的大小，转换范围内的元素：迭代地 `k = 0, ..., m-1`，计算值

```cpp
r1 = 166425-T(begin[k] xor begin[k+p] xor begin[k-1])
r2 = r1+\begin{cases} 0 & k=0 \\k mod n+v[k] & 0<k<=s \\k mod n & s<k \end{cases}
```

并且，按顺序将 `begin[k+p]` 增加 `r1`，将 `begin[k+q]` 增加 `r2`，并将 `begin[k]` 设置为 `r2`。

- c) 从上一步结束的地方再次转换范围内的元素：迭代地 `k = m, ..., m+n-1`，计算值

```cpp
r3 = 156083941-T(begin[k] + begin[k+p] + begin[k-1])
r4 = (k mod n)
```

按顺序通过 `r3` 更新 `begin[k+p]`，通过 `r4` 更新 `begin[k+q]`，并将 `begin[k]` 设置为 `r4`。

```cpp
size_t size() const;
```

返回：通过调用 `param()` 返回 `32` 位单元的数量。复杂度：常数时间。

```cpp
template<class OutputIterator>
void param(OutputIterator dest) const;
```

要求：`OutputIterator` 应当满足输出迭代器（表 `108`）类型。此外，表达式 `dest = rt` 应该是 `result_type` 的有效值。效果：将 `32` 位单元序列拷贝到目标，相当于执行语句：

```cpp
copy(v.begin(), v.end());
```

## 26.5.8 随机分布

### 26.5.8.1 通用

模板实例化满足随机分布（`26.5.1`）的要求。在本节 `26.5.8` 中仅为具有额外信息的分布提供了描述。特别是，未显示拷贝构造函数、赋值运算符、流运算符以及不等运算符。产生每个分布的算法是实现定义的。在本节指定的概率密度函数 `p(z)` 和离散概率函数 `P(z)` 在其定义域之外的。

### 26.5.7.2 模板 generate_canonical

模板实例化将一次或多次调用随机数生成器 `g` 的结果映射到指定的 `RealType` Member，如果结果 `$0 \le t_i < 1$`，则按如下方式均匀分布。注意：这种方式允许将随机数生成器生成的值转换为随机分布可以交付的值。

```cpp
template<class RealType, size_t bits, class URNG>
RealType generate_canonical(URNG& g);
```

复杂度：恰好调用 `g` `$k = \max(1, \lfloor\log_2 b\rfloor)$` 次，其中 `$2^k$` 是 `numeric_limits<RealType>;max() - g.min() + 1`。效果：调用 `$g()$` 次获取值 `$g_0, \dots, g_{k-1}$`。使用 `RealType` 算术计算数量。

```cpp
S = sum_{i=0}^{k-1} (g_i - g.min())
```

返回：`$S/2^k$`。抛出：`g` 抛出的异常。

### 26.5.8.2 均匀分布

#### 26.5.8.2.1 类 uniform_int_distribution

`uniform_int_distribution` 随机数产生随机整数 `$i，$a \le i \le b$`，根据常数概率函数 `$P(i, a, b) = 1/(b - a + 1)$` 分布。引入 `b` 是为了避免产生 `RealType` 能容纳更多的位。

```cpp
template<class IntType = int>
class uniform_int_distribution
{
public:
    // 类型
    typedef IntType result_type;
    typedef unspecified param_type;

    // 构造函数和重置函数
    explicit uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
    explicit uniform_int_distribution(const param_type& parm);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& parm);

    // 属性函数
    result_type a() const;
    result_type b() const;
    param_type param(const param_type& parm) const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
```

要求：`a <= b`。效果：构造一个 `uniform_int_distribution` 对象；`a` 和 `b` 对应于分布的参数。

`result_type a() const;`

返回：构造对象时使用的参数的值。

`result_type b() const;`

返回：构造对象时使用的参数的值。

#### 26.5.8.2.2 类 uniform_real_distribution [rand.dist.uni.real]

`uniform_real_distribution` 随机分布产生数字 `x`，`$a \le x < b$`，根据常数概率密度函数 `p(x|a,b) = 1/(b - a)` 分布。

```cpp
template<class RealType = double>
class uniform_real_distribution
{
public:
    // 类型
    typedef RealType result_type;
typedef unspecified_param_type;

// 构造函数和重置函数
explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);
explicit uniform_real_distribution(const param_type& parm);
void reset();

// 生成函数
template<class URNG>
result_type operator()(URNG& g);
template<class URNG>
result_type operator()(URNG& g, const param_type& parm);

// 属性函数
result_type a() const;
result_type b() const;
param_type param() const;
void param(const param_type& parm);
result_type min() const;
result_type max() const;

explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);
```

要求：`a <= b` 且 `a <= numeric_limits<RealType>::max()`。效果：构造一个 `uniform_real_distribution` 对象；`a` 和 `b` 对应于分布的参数。

`result_type a() const;`

返回：构造对象时使用的参数的值。

`result_type b() const;`

返回：构造对象时使用的参数的值。

### 26.5.8.3 伯努利分布 [rand.dist.bern]

#### 26.5.8.3.1 类 bernoulli_distribution [rand.dist.bern.noulli]

伯努利分布 随机数产生布尔值 `b`，根据离散概率函数

```cpp
P(b|p) = { p if b = true \ 1 - p if b = false }
```

```cpp
class bernoulli_distribution
{
public:
```

```cpp
explicit bernouilli_distribution(const param_type& parm);
void reset();
```

```cpp
// generating functions
template<class URNG>
result_type operator()(URNG& g);
template<class URNG>
result_type operator()(URNG& g, const param_type& parm);
```

```cpp
// property functions
double p() const;
param_type parm() const;
void param(const param_type& parm);
result_type min() const;
result_type max() const;
};
```

```cpp
explicit bernouilli_distribution(double p = 0.5);
```

- 2 Requires: `$0 \le p \le 1$`。

- 3 Effects: 构造一个 `bernouilli_distribution` 对象；`p` 对应分布的参数。

`double p() const;`

- 4 Returns: 构建对象时使用的 `p` 参数的值。

## 26.5.8.2 Class template binomial_distribution

[rand.dist.bern.bin]

- 1 二项分布（`binomial_distribution`）随机数产生根据离散概率函数分布的整数 `$i \ge 0$`

`$P(i|t,p) = \binom{t}{i} \cdot p^i \cdot (1-p)^{t-i}$`

```cpp
template<class IntType = int>
class binomial_distribution
{
public:
// types
typedef IntType result_type;
typedef unspecified param_type;
// constructors and reset functions
explicit binomial_distribution(IntType t = 1, double p = 0.5);
explicit binomial_distribution(const param_type& parm);
void reset();
// generating functions
template<class URNG>
result_type operator()(URNG& g);
template<class URNG>
result_type operator()(URNG& g, const param_type& parm);
```

§ 26.5.8.2

# ISO/IEC 14882:2011(E)

```cpp
// property functions
IntType t() const;
double p() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```cpp
explicit binomial_distribution(IntType t = 1, double p = 0.5);
```

- 2 Requires: `0 ≤ p ≤ 1 and 0 ≤ t.`。

- 3 Effects: 构造一个 `binomial_distribution` 对象；`t` 和 `p` 分别对应分布的参数。

```cpp
IntType t() const;
```

- 4 Returns: 构建对象时使用的 `t` 参数的值。

```cpp
double p() const;
```

- 5 Returns: 构建对象时使用的 `p` 参数的值。

### 26.5.8.3.3 Class template geometric_distribution [rand.dist.bern.go]

- 1 几何分布（`geometric_distribution`）随机数产生根据离散概率函数分布的整数 `$i \ge 0$`

`$P(i|p) = p \cdot (1-p)^i$`

```cpp
template<class IntType = int>
class geometric_distribution {
public:
  // types
  typedef IntType result_type;
  typedef unspecified_param_type;

  // constructors and reset functions
  explicit geometric_distribution(double p = 0.5);
  explicit geometric_distribution(const param_type& param);
  void reset();

  // member functions
template<class URNG>
  result_type operator()(URNG& g);
template<class URNG>
  result_type operator()(URNG& g, const param_type& param);

  // property functions
  double p() const;
  param_type param() const;
  void param(const param_type& param);
  result_type min() const;
  result_type max() const;
};
```

## § 26.5.8.3.3

# ISO/IEC 14882:2011(E)

```cpp
explicit geometric_distribution(double p = 0.5);

- 2 Requires: 0 < p < 1;

- 3 Effects: 构造一个 geometric_distribution 对象；p 对应分布的参数。

double p() const;

- 4 Returns: 构建对象时使用的 p 参数的值。
```

### 26.5.8.3.4 Class template negative_binomial_distribution [rand.dist.bern.negbin]

- 1 负二项分布（`negative_binomial_distribution`）随机数产生根据概率函数分布的随机整数 `$i \ge 0$`

```cpp
P(i|k,p) = \left(\frac{k+i-1}{i}\right)\cdot p^k \cdot (1-p)^i;
```

```cpp
template<class IntType = int>
class negative_binomial_distribution{
public:
    // types
    typedef IntType result_type;
    typedef unspecified param_type;

    // constructor and reset functions
    explicit negative_binomial_distribution(IntType k = 1, double p = 0.5);
    explicit negative_binomial_distribution(const param_type& param);
    void reset();

    // generating functions
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);

    // property functions
    IntType k() const;
    double p() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```
