
```cpp
template<class RealType = double>
class gamma_distribution {
public:
// 类型
typedef RealType result_type;
typedef unspecified param_type;

// 构造函数与重置函数
explicit gamma_distribution(RealType alpha = 1.0, RealType beta = 1.0);
explicit gamma_distribution(const param_type& param);
void reset();

// 生成函数
template<class URNG>
result_type operator()(URNG& g);
template<class URNG>
result_type operator()(URNG& g, const param_type& param);

// 属性函数
RealType alpha() const;
RealType beta() const;
param_type param() const;
void param(const param_type& param);
result_type min() const;
result_type max() const;
};
```

`explicit gamma_distribution(RealType alpha = 1.0, RealType beta = 1.0);`

- + 2 要求：0 < `alpha` 和 0 < `beta`。
- + 3 效果：构造一个 `gamma_distribution` 对象；`alpha` 和 `beta` 对应于分布的参数。

`RealType alpha() const;`

- 返回：构造对象时使用的 `alpha` 参数的值。

`RealType beta() const;`

- 返回：构造对象时使用的 `beta` 参数的值。

### 26.5.8.4.4 类模板 weibull_distribution [rand.dist.pois]

`weibull_distribution` 随机数产生 `x ≥ 0`，其分布符合概率密度函数

```
p(x|a,b) = \frac{a}{b} \left(\frac{x}{b}\right)^{a-1} \cdot \exp\left(-\left(\frac{x}{b}\right)^a\right)$
```

```cpp
template<class RealType = double>
class weibull_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef unspecified param_type;

    // 构造函数与重置函数
    explicit weibull_distribution(RealType a = 1.0, RealType b = 1.0);
    explicit weibull_distribution(const param_type& param);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& param);

    // 属性函数
    RealType alpha() const;
    RealType beta() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

*(注：此处原文文本在 Weibull 部分似乎存在错乱或重复，已根据上下文逻辑整理翻译)*

- + 2 要求：0 < `a` 和 0 < `b`。
- + 3 效果：构造一个 `weibull_distribution` 对象；`a` 和 `b` 对应于分布的参数。

---

### 26.5.8.4.5 类模板 extreme_value_distribution [rand.dist.pois]

1 `extreme_value_distribution` 随机数分布产生随机数 `x`，其分布符合概率密度函数

![](img/d989e0c024e88f07d640fc56ce571_982_0.png)

```cpp
template<class RealType>
class extreme_value_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef specified param_type;

    // 构造函数与重置函数
    explicit extreme_value_distribution(RealType a = 0.0, RealType b = 1.0);
    explicit extreme_value_distribution(const param_type& param);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& param);

    // 属性
    RealType a() const;
    RealType b() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

`extreme_value_distribution(RealType a = 0.0, RealType b = 1.0);`

- + 2 要求：0 < `a` 和 0 < `b`。
- + 3 效果：构造一个 `extreme_value_distribution` 对象；`a` 和 `b` 对应于分布的参数。

> ²⁸⁰) 对应此概率密度函数的分布也（通过可能的变量替换）称为 Gumbel 型、对数 Weibull 型或 Fisher-Tippett 分布。

©ISO/IEC N4296

2 Requires: 0 < `b`.

3 Effects: 构造一个 `extreme_value_distribution` 对象；`a` 和 `b` 分别对应该分布的参数。

`RealType a() const;`

4 Returns: 构建对象时使用的参数值。

`RealType b() const;`

5 Returns: 构建对象时使用的 `b` 参数值。

## 26.5.5 正态分布 [rand.dist.norm]

### 26.5.5.5.1 模板类 normal_distribution [rand.dist.norm.normal]

1 正态分布随机数产生的随机数 `x` 服从概率函数分布

```
p(x|\mu) = \frac{1}{\sigma\sqrt{2\pi}} \cdot \exp\left(\frac{(x-\mu)^2}{2\sigma^2}\right);
```

参数 `μ` 和 `σ` 也称为该分布的均值和标准差。

```cpp
template<class RealType>
class normal_distribution {
public:
    typedef RealType result_type;
    typedef unspecified param_type;

    // 构造函数和重置函数
    explicit normal_distribution(RealType mean = 0.0, RealType stddev = 1.0);
    explicit normal_distribution(const param_type& param);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
template<class URNG>
    result_type operator()(URNG& g, const param_type& param);

    // 属性函数
    RealType mean() const;
    RealType stddev() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

`explicit normal_distribution(RealType mean = 0.0, RealType stddev = 1.0);`

2 Requires: 0 < `stddev`.

3 Effects: 构造一个 `normal_distribution` 对象；`mean` 和 `stddev` 分别对应该分布的参数。

```cpp
RealType mean() const;
```

Returns: 构建对象时使用的 `mean` 参数值。

```cpp
RealType stddev() const;
```

Returns: 构建对象时使用的 `stddev` 参数值。

### 26.5.8.5.2 模板类 lognormal_distribution [rand.dist.norm.lognormal]

- 对数正态分布随机数分布产生的数字 `x > 0` 服从概率密度函数分布

```
$p(x|m,s) = \frac{1}{s\sqrt{2\pi}} \exp\left(-\frac{(\ln x-m)^2}{2s^2}\right)$
```

```cpp
template<class RealType = double>
class lognormal_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef RealType param_type;

    // 构造函数和重置函数
    explicit lognormal_distribution(RealType m = 0.0, RealType s = 1.0);
    explicit lognormal_distribution(const param_type& param);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& param);

    // 属性函数
    RealType m() const;
    RealType s() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit lognormal_distribution(RealType m = 0.0, RealType s = 1.0);
```

- Requires: `s < 0`.
- Effects: 构造一个 `lognormal_distribution` 对象；`m` 和 `s` 分别对应该分布的参数。

```cpp
RealType m() const;
```

Returns: 构建对象时使用的 `m` 参数值。

```cpp
RealType s() const;
```

Returns: 构建对象时使用的 `s` 参数值。

### 26.5.8.5.3 模板类 chi_squared_distribution [rand.dist.norm.chisq]

1 卡方分布随机数产生的随机数 `x > 0` 服从概率密度函数分布

$$p(x|n) = \frac{x^{(n/2)-1}}{\Gamma(n/2)}$$ 

```cpp
template<class RealType = double>
class chi_squared_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef unspecified param_type;

    // 构造函数和重置函数
    explicit chi_squared_distribution(RealType n = 1);
    explicit chi_squared_distribution(const param_type& param);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& param);

    // 属性函数
    RealType n() const;
    param_type param() const;
    void param(const param_type& param);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit chi_squared_distribution(RealType n = 1);
```

2 Requires: 0 < `n`.

3 Effects: 构造一个 `chi_squared_distribution` 对象；`n` 对应该分布的参数。

```cpp
RealType n() const;
```

Returns: 构建对象时使用的 `n` 参数值。

### 26.5.8.5.4 模板类 cauchy_distribution [rand.dist.norm.cauchy]

1 柯西分布随机数产生的随机数服从概率密度函数分布

$$p(x|a,b) = \frac{1}{\pi b \left(1 + \left(\frac{x-a}{b}\right)^2\right)}$$

```cpp
template<class RealType = double>
class cauchy_distribution
{
public:
    // 类型
    typedef RealType result_type;
    typedef unspecified param_type;

    // 构造函数和重置函数
    explicit cauchy_distribution(RealType a = 0.0, RealType b = 1.0);
    explicit cauchy_distribution(const param_type& parm);
    void reset();

    // 生成函数
    template<class URNG>
    result_type operator()(URNG& g);
    template<class URNG>
    result_type operator()(URNG& g, const param_type& parm);

    // 属性函数
    RealType a() const;
    RealType b() const;
    param_type parm(const param_type& parm);
    void a(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
cauchy_distribution(RealType a = 0.0, RealType b = 1.0)
```

- Requires: 0 < `b`.
- Effects: 构造一个 `cauchy_distribution` 对象；`a` 和 `b` 分别对应该分布的参数。

```cpp
RealType a() const;
```

Returns: 构建对象时使用的参数值。

```cpp
RealType b() const;
```

Returns: 构建对象时使用的参数值。

### 26.5.8.5 模板类 fisher_f_distribution [rand.dist.norm.f]

- F 分布随机数分布产生的数字 `x ≥ 0` 服从概率密度分布

```
p(x|m,n) = \frac{\Gamma((m+n)/2)}{\Gamma(m/2)} \cdot \left(\frac{mx}{n}\right)^{m/2-1} \cdot \left(1+\frac{mx}{n}\right)^{-(m+n)/2}
```
