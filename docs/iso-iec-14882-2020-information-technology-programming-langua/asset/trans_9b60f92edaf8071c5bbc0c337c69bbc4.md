

```cpp
explicit random_device(const string& token);
```

*备注：* token 参数及默认构造函数所使用的 token 值的语义由实现定义。[^250]

*抛出：* 若 random_device 无法初始化，则抛出派生于 exception 的实现定义类型的值。

```cpp
double entropy() const noexcept;
```

*返回：* 若实现采用随机数引擎，则返回 0.0。否则，返回 operator() 所返回的随机数的熵估计值[^251]，范围在 min() 到 log2(max() + 1) 之间。

```cpp
result_type operator()();
```

*返回：* 一个不确定性随机值，在 min() 到 max()（含）之间均匀分布。如何生成这些值由实现定义。

*抛出：* 若无法获得随机数，则抛出派生于 exception 的实现定义类型的值。

## 26.6.8 工具 [rand.util]

### 26.6.8.1 类 seed_seq [rand.util.seedseq]

```cpp
class seed_seq {
public:
  // types
  using result_type = uint_least32_t;

  // constructors
  seed_seq();
  template<class T>
    seed_seq(initializer_list<T> il);
  template<class InputIterator>
    seed_seq(InputIterator begin, InputIterator end);

  // generating functions
  template<class RandomAccessIterator>
    void generate(RandomAccessIterator begin, RandomAccessIterator end);

  // property functions
  size_t size() const noexcept;
  template<class OutputIterator>
    void param(OutputIterator dest) const;

  // no copy functions
  seed_seq(const seed_seq&) = delete;
  void operator=(const seed_seq&) = delete;

private:
  vector<result_type> v;      // exposition only
};
```

```cpp
seed_seq();
```

*后置条件：* v.empty() 为 true。

*抛出：* 无。

```cpp
template<class T>
  seed_seq(initializer_list<T> il);
```

*要求：* T 是整数类型。

*效果：* 与 seed_seq(il.begin(), il.end()) 相同。

```cpp
template<class InputIterator>
    seed_seq(InputIterator begin, InputIterator end);
```

*要求：* iterator_traits<InputIterator>::value_type 是整数类型。

*前置条件：* InputIterator 满足 Cpp17InputIterator 要求 (23.3.5.3)。

*效果：* 通过以下算法初始化 v：

```cpp
for (InputIterator s = begin; s != end; ++s)
    v.push_back((*s) mod 2^32);
```

```cpp
template<class RandomAccessIterator>
void generate(RandomAccessIterator begin, RandomAccessIterator end);
```

*要求：* iterator_traits<RandomAccessIterator>::value_type 是无符号整数类型，能够容纳 32 位数量。

*前置条件：* RandomAccessIterator 满足 Cpp17RandomAccessIterator 要求 (23.3.5.7) 及可变迭代器的要求。

*效果：* 若 begin == end，则不执行任何操作。否则，设 s = v.size()、n = end − begin，按以下算法填充给定范围 [begin, end)。算法中每个运算均以 2^32 为模执行，每次对 begin 应用下标运算符时均以 n 为模，且 T(x) 定义为 x xor (x >> 27)：

- 初始化时，将范围内的每个元素设置为值 0x8b8b8b8b。此外，为在后续步骤中使用，令 p = (n − t)/2、q = p + t，其中

  t = (n ≥ 623) ? 11 : (n ≥ 68) ? 7 : (n ≥ 39) ? 5 : (n ≥ 7) ? 3 : (n − 1)/2；

- 以 m 为 s + 1 与 n 中的较大者，变换范围内的元素：对于 k = 0,…,m − 1，迭代计算值

  r1 = 1664525 · T(begin[k] xor begin[k + p] xor begin[k − 1])

  r2 = r1 + { s, k = 0; k mod n + v[k − 1], 0 < k ≤ s; k mod n, s < k }

  并按顺序将 begin[k + p] 增加 r1，将 begin[k + q] 增加 r2，将 begin[k] 设置为 r2。

- 从前一步结束处开始再次变换范围内的元素：对于 k = m,…,m + n − 1，迭代计算值

  r3 = 1566083941 · T(begin[k] + begin[k + p] + begin[k − 1])

  r4 = r3 − (k mod n)

  并按顺序将 begin[k + p] 与 r3 异或，将 begin[k + q] 与 r4 异或，将 begin[k] 设置为 r4。

*抛出：* begin 和 end 的 RandomAccessIterator 操作所抛出的异常及抛出时机。

```cpp
size_t size() const noexcept;
```

*返回：* 调用 param() 将返回的 32 位单位的数目。

*复杂度：* 常数时间。

```cpp
template<class OutputIterator>
void param(OutputIterator dest) const;
```

*要求：* result_type 类型的值可写入 dest (23.3.1)。

*前置条件：* OutputIterator 满足 Cpp17OutputIterator 要求 (23.3.5.4)。

*效果：* 将准备好的 32 位单位序列复制到给定目标，如同执行以下语句：

```cpp
copy(v.begin(), v.end(), dest);
```

*抛出：* dest 的 OutputIterator 操作所抛出的异常及抛出时机。

### 26.6.8.2 函数模板 generate_canonical [rand.util.canonical]

```cpp
template<class RealType, size_t bits, class URBG>
RealType generate_canonical(URBG& g);
```

*复杂度：* 恰好调用 g 的次数为 k = max(1, ⌈b / log2 R⌉)，其中 b[^252] 是 numeric_limits<RealType>::digits 与 bits 中的较小者，R 是 g.max() − g.min() + 1 的值。

*效果：* 调用 g() k 次，分别获得值 g₀, …, gₖ₋₁。使用 RealType 类型的算术计算数量

```
S = Σᵢ₌₀ᵏ⁻¹ (gᵢ − g.min()) · Rⁱ
```

*返回：* S / Rᵏ。

[注 1：0 ≤ S / Rᵏ < 1。 — 结束注]

*抛出：* g 所抛出的异常及抛出时机。

[注 2：若 g 产生的值 gᵢ 均匀分布，则该实例化的结果尽可能均匀分布。以这种方式获取值，可将均匀随机位生成器生成的值转换为随机数分布能够提供的值，这是该转换过程中一个有用的步骤。 — 结束注]

## 26.6.9 随机数分布类模板 [rand.dist]

### 26.6.9.1 总则 [rand.dist.general]

从本子条款 26.6.9 所指定的类模板实例化的每个类型均满足随机数分布 (26.6.3.6) 类型的要求。

本子条款 26.6.9 仅对 26.6.3.6 中未描述的分布操作或具有额外语义信息的操作提供描述。特别是，复制构造函数、复制赋值运算符、流运算符以及相等和不相等运算符的声明不出现在概要中。

生成每个指定分布的算法由实现定义。

本子条款中指定的每个概率密度函数 p(z) 和每个离散概率函数 P(zᵢ) 在其规定定义域之外的任何位置的值均为 0。

### 26.6.9.2 均匀分布 [rand.dist.uni]

#### 26.6.9.2.1 类模板 uniform_int_distribution [rand.dist.uni.int]

uniform_int_distribution 随机数分布产生随机整数 i（a ≤ i ≤ b），根据常数离散概率函数分布

P(i | a, b) = 1 / (b − a + 1)。

```cpp
template<class IntType = int>
class uniform_int_distribution {
public:
    // types
    using result_type = IntType;
    using param_type = unspecified;

    // constructors and reset functions
    uniform_int_distribution() : uniform_int_distribution(0) {}
    explicit uniform_int_distribution(IntType a, IntType b = numeric_limits<IntType>::max());
    explicit uniform_int_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);

    // property functions
    result_type a() const;
    result_type b() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit uniform_int_distribution(IntType a, IntType b = numeric_limits<IntType>::max());
```

*前置条件：* a ≤ b。

*备注：* a 和 b 分别对应于分布的相应参数。

```cpp
result_type a() const;
```

*返回：* 构造对象时使用的 a 参数的值。

```cpp
result_type b() const;
```

*返回：* 构造对象时使用的 b 参数的值。

#### 26.6.9.2.2 类模板 uniform_real_distribution [rand.dist.uni.real]

uniform_real_distribution 随机数分布产生随机数 x（a ≤ x < b），根据常数概率密度函数分布

p(x | a, b) = 1/(b − a)。

> [注 1：这意味着当 a == b 时，p(x | a, b) 未定义。 — 结束注]

```cpp
template<class RealType = double>
class uniform_real_distribution {
public:
    // types
    using result_type = RealType;
    using param_type = unspecified;

    // constructors and reset functions
    uniform_real_distribution() : uniform_real_distribution(0.0) {}
    explicit uniform_real_distribution(RealType a, RealType b = 1.0);
    explicit uniform_real_distribution(const param_type& parm);
    void reset();

    // generating functions
    template<class URBG>
    result_type operator()(URBG& g);
    template<class URBG>
    result_type operator()(URBG& g, const param_type& parm);

    // property functions
    result_type a() const;
    result_type b() const;
    param_type param() const;
    void param(const param_type& parm);
    result_type min() const;
    result_type max() const;
};
```

```cpp
explicit uniform_real_distribution(RealType a, RealType b = 1.0);
```

*前置条件：* a ≤ b 且 b − a ≤ numeric_limits<RealType>::max()。

*备注：* a 和 b 分别对应于分布的相应参数。

```cpp
result_type a() const;
```

*返回：* 构造对象时使用的 a 参数的值。

```cpp
result_type b() const;
```

*返回：* 构造对象时使用的 b 参数的值。

[^250]: 该参数旨在允许实现区分不同的随机性来源。

[^251]: 如果一个设备有 n 个状态，其各自概率为 P₀, …, Pₙ₋₁，则设备熵 S 定义为 S = −Σᵢ₌₀ⁿ⁻¹ Pᵢ · log Pᵢ。

[^252]: 引入 b 是为了避免试图产生比 RealType 所能容纳的更多的随机性位数。

