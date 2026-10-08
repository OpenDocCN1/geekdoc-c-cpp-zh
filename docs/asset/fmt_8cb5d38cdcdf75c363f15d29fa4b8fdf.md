
```
//构造函数和重置函数
explicit uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
explicit uniform_int_distribution(const param_type& param);
void reset();
```

```
// 生成函数
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);
```

```
// 属性函数
result_type a() const;
result_type b() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```
explicit uniform_int_distribution(IntType a = 0, IntType b = numeric_limits<IntType>::max());
```

- 2. 要求：$a \le b$。
- 3. 影响：构造一个 `uniform_int_distribution` 对象；$a$ 和 $b$ 对应于分布的参数。

```
result_type a() const;
```

- 4. 返回：构造对象时参数的值。

```
result_type b() const;
```

- 5. 返回：构造对象时 $b$ 参数的值。

### 26.5.8.2.2 类模板 uniform_real_distribution [rand.dist.uni.real]

`uniform_real_distribution` 随机数分布产生随机数 $x, a \le x < b$，按照常数密度函数分布：

```
p(x|a, b) = 1/(b - a).
```

```
template<class RealType = double>
class uniform_real_distribution
public:
// types
typedef RealType result_type;
typedef unspecified param_type;
```

```
// 构造函数和重置函数
explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);
explicit uniform_real_distribution(const param_type& param);
void reset();
```

```
// 生成函数
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);
```

```
// 属性函数
result_type a() const;
result_type b() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```
explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);
```

- 2. 要求：`numeric_limits<RealType>::max()`。
- 3. 影响：构造一个 `uniform_real_distribution` 对象；$a$ 和 $b$ 对应于分布的参数。
- 4. 返回：构造对象时参数的值。
- 5. 返回：构造对象时 $b$ 参数的值。

## 26.5.8.3 布尔值分布 [rand.dist.bern]

### 26.5.8.3.1 类模板 bernoulli_distribution [rand.dist.bern]

`bernoulli_distribution` 随机数产生布尔值，按照概率函数分布：$P(b|p) = p$ 为真，$1-p$ 为假。

```
class bernoulli_distribution {
public:
// types
typedef bool result_type;
typedef unspecified param_type;
```

```
// 构造函数和重置函数
explicit bernoulli_distribution(double p = 0.5);
explicit bernoulli_distribution(const param_type& param);
void reset();
```

```
// 生成函数
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);
```

```
// 属性函数
double p() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```
explicit bernoulli_distribution(double p = 0.5);
```

- 2. 要求：$0 \le p \le 1$。
- 3. 影响：构造一个 `bernoulli_distribution` 对象；$p$ 对应于分布的参数。

### 26.5.8.3.2 类模板 binomial_distribution [rand.dist.bern]

`binomial_distribution` 随机数分布产生整数 $i \ge 0$，按照离散概率函数分布：$P(i|t,p) = \binom{t}{i} p^i (1-p)^{t-i}$。

```
template<class IntType = int>
class binomial_distribution
{
public:
// types
typedef IntType result_type;
typedef unspecified param_type;
```

```
// 构造函数和重置函数
explicit binomial_distribution(IntType t = 1, double p = 0.5);
explicit binomial_distribution(const param_type& param);
void reset();
```

```
// 生成函数
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);
```

```
// 属性函数
IntType t() const;
double p() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```
explicit binomial_distribution(IntType t = 1, double p = 0.5);
```

- 2. 要求：$0 \le p \le 1$ 和 $0 \le t$。
- 3. 影响：构造一个 `binomial_distribution` 对象；$t$ 和 $p$ 对应于分布的参数。

### 26.5.8.3.3 类模板 geometric_distribution [rand.dist.bern.geo]

`geometric_distribution` 随机数分布产生整数 $i \ge 0$，按照离散概率函数分布：$P(i|p) = p \cdot (1 - p)^i$。

```
template<class IntType = int>
class geometric_distribution
{
public:
// types
typedef IntType result_type;
typedef unspecified param_type;
```

```
// 构造函数和重置函数
explicit geometric_distribution(double p = 0.5);
explicit geometric_distribution(const param_type& param);
void reset();
```

```
// 生成函数
template<class URNG>
result_type operator() (URNG& g);
template<class URNG>
result_type operator() (URNG& g, const param_type& param);
```

```
// 属性函数
double p() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

```
explicit geometric_distribution(double p = 0.5);
```

- 2. 要求：$0 < p < 1$。
- 3. 影响：构造一个 `geometric_distribution` 对象；$p$ 对应于分布的参数。

## 26.5.8.3.4 类模板 binomial_distribution [rand.dist.bern.nbin]

1 `negative_binomial_distribution` 随机数分布产生随机整数 $i \ge 0$，其分布符合以下离散概率函数

```
P(i|k) = \binom{k+i-1}{i} p^k (1-p)^i.
```

```cpp
template<class IntType = int>
class negative_binomial_distribution
{
public:
    // 类型
    typedef IntType result_type;
    typedef pair<IntType, double> param_type;
    // 构造函数与重置函数
    explicit negative_binomial_distribution(IntType k = 1, double p = 0.5);
    explicit negative_binomial_distribution(const param_type& parm);
    void reset();
    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& parm);
    // 属性函数
    IntType k() const;
    double p() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

`explicit negative_binomial_distribution(IntType k = 1, double p = 0.5);`

- 2 3 效果：构造一个 `negative_binomial_distribution` 对象；$k$ 和 $p$ 对应于分布的参数。

`IntType k() const;`

- 4 返回：构造对象时使用的 $k$ 参数的值。

`double p() const;`

- 5 返回：构造对象时使用的 $p$ 参数的值。

## 26.5.8.4 泊松分布 distributions [rand.dist.pois]

### 26.5.8.4.1 类模板 poisson_distribution [rand.dist.pois.poisson]

1 `poisson_distribution` 随机数分布产生整数值 $i \ge 0$，其分布符合以下离散概率函数

```
P(i|\mu) = \frac{e^{-\mu}\mu^i}{i!}.
```

分布参数 $\mu$ 也称为该分布的均值。

```cpp
template<class IntType = int>
class poisson_distribution
{
public:
    // 类型
    typedef IntType result_type;
    typedef unspecified param_type;
    // 构造函数与重置函数
    explicit poisson_distribution(double mean = 1.0);
    explicit poisson_distribution(const param_type& param);
    void reset();
    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& param);
    // 属性函数
    double mean() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

`poisson_distribution(double mean = 1.0);`

- + 2 要求：$0 < mean$。
- 3 效果：构造一个 `poisson_distribution` 对象；$mean$ 对应于分布的参数。

`double mean() const;`

- + 4 返回：构造对象时使用的 $mean$ 参数的值。

### 26.5.8.4.2 类模板 exponential_distribution [rand.dist.pois.exp]

- + 1 `exponential_distribution` 随机数分布产生随机数 $x > 0$，其分布符合以下概率密度函数

```
p(x|λ) = λe^{-λx}.
```

```cpp
template<class RealType>
class exponential_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef unspecified param_type;
    // 构造函数与重置函数
    explicit exponential_distribution(RealType lambda = 1.0);
explicit exponential_distribution(const param_type& param);
void reset();
```cpp
// 生成函数
template<class URNG>
result_type operator()(URNG& g);
template<class URNG>
result_type operator()(URNG& g, const param_type& param);

// 属性函数
RealType lambda() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
```

`explicit exponential_distribution(RealType lambda = 1.0);`

- + 2 要求：$0 < lambda$。
- 3 效果：构造一个 `exponential_distribution` 对象；$lambda$ 对应于分布的参数。

`RealType lambda() const;`

- + 4 返回：构造对象时使用的 $lambda$ 参数的值。

### 26.5.8.4.3 类模板 distribution [rand.dist.pois.gamma]

`gamma_distribution` 随机数分布产生随机数 $x > 0$，其分布符合概率密度函数

> p(x | \alpha, \beta) = \frac{e^{-x/\beta}}{\beta^{\alpha}\Gamma(\alpha)}} \cdot x^{\alpha-1}
