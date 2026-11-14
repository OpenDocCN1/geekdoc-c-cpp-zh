

} } }

此处我们仅对 [-10, 10) 范围内的随机数进行了测试，用于实部和虚部；这是否足以获得对正确性的良好信心，尚属未定。在大型项目中，构建可复用的测试框架绝对是值得的。包含随机值生成和最内层循环中测试函数的嵌套循环模式适用于许多情况。它可以封装在一个类中，该类可能是可变参数的，以处理涉及不同数量变量的属性。随机值的生成也可以由特殊构造函数提供（例如，由标记标记），或者序列可以预先生成。可以想象不同的方法。本节中选择循环模式是为了简单起见。

要看出分配律不完全成立，我们可以将 `eps` 降低到非常小的值，甚至降到 0。然后，我们会看到类似下面的（缩写的）错误消息：

点击此处查看代码图片

```
Test detected that (-6.21,7.09) * ((2.52,-3.58) +
(-4.51,-3.91))
!= (-6.21,7.09) * (2.52,-3.58) + (-6.21,7.09) *
(-4.51,3.91)
terminate called after throwing 'distributivity_violated'
```

现在我们进入随机数生成的细节。

## 4.2.2.3 引擎

库 `<random>` 包含两种函数对象：生成器和分布。前者生成无符号整数序列（精确类型由每个类的类型别名提供）。每个值应具有大约相同的概率。分布类将这些数字映射到其概率对应于参数化分布的值上。

除非有特殊需求，否则我们可以直接使用 `default_random_engine`。其确切定义依赖于实现，但我们可以信任标准库开发人员选择了合适的引擎。我们必须牢记，随机数序列确定性地依赖于其种子，并且每次创建对象时，每个引擎都用相同的种子初始化。因此，给定类型的新引擎始终产生相同的序列，例如：

点击此处查看代码图片

```
void random_numbers()
{
    default_random_engine re;
    cout << "Random numbers: ";
    for (int i=0; i < 4; i++)
        cout << re() << (i < 3 ? ", " : "");
    cout << '\n';
}

int main ()
{
    random_numbers();
    random_numbers();
}
```

在作者的机器上产生了以下结果：

随机数: 16807 , 282475249 , 1622650073 , 984943658
随机数: 16807 , 282475249 , 1622650073 , 984943658

要在每次调用 random_numbers 时获得不同的序列，我们必须通过将其声明为 static 来创建持久引擎：

点击此处查看代码图片

```
void random_numbers()
{
    static default_random_engine re;
    ...
}
```

尽管如此，每次程序运行的序列仍然相同。为了克服这一点，我们必须将种子设置为几乎真正的随机值。这样的值由 random_device 提供：

点击此处查看代码图片

```
void random_numbers()
{
    static random_device rd;
    static default_random_engine re(rd());
    ...
}
```

random_device 返回一个依赖于硬件和操作系统事件测量的值，可以被视为几乎真正的随机值（即，实现了非常高的熵）。事实上，random_device 提供与引擎相同的接口，只是种子不能设置。因此，它也可以用于生成随机值，至少在性能不是问题时可以这样做。在我们的测试机器上，使用 default_random_engine 生成一百万个随机数耗时 4–13 ms，而使用 random_device 耗时 810–820 ms。在依赖高质量随机数的应用程序中，例如密码学，这种性能损失仍然可以接受。在大多数情况下，仅使用 random_device 生成初始种子，或稍后偶尔调用它，应该就足够了。

在生成器中，有主引擎、其参数化适配器以及预定义的适配引擎：

- 能够生成随机值的基本引擎：
  - linear_congruential_engine，
  - mersenne_twister_engine，以及
  - subtract_with_carry_engine。

- 从另一个引擎创建新引擎的引擎适配器：
  - discard_block_engine：每次忽略底层引擎的 n 个条目；
  - independent_bits_engine：将主随机数映射到 w 位；
  - shuffle_order_engine：通过保留最后几个值的内部缓冲区来修改随机数的顺序。

- 通过实例化或适配从基本引擎构建的预定义适配引擎：
  - knuth_b
  - minstd_rand
  - minstd_rand0
  - mt19937
  - mt19937_64
  - ranlux24
  - ranlux24_base
  - ranlux48
  - ranlux48_base

最后一组中的预定义引擎只是类型定义，例如：

点击此处查看代码图片

```
using knuth_b= shuffle_order_engine <minstd_rand0 , 256>;
```

## 4.2.2.4 分布概览

如前所述，分布类将无符号整数映射到参数化分布。表 4–3 总结了 C++11 中定义的分布。受篇幅限制，我们使用了一些缩写符号。分布的结果类型可以作为类模板的参数指定，其中 I 表示整数，R 表示实数类型。当构造函数（例如，m）和描述公式（例如，μ）中使用不同的符号时，我们在前置条件中表示等价关系（例如 m ≡ μ）。为保持一致性，我们在对数正态分布和正态分布中使用了相同的符号（与其他书籍、在线参考和标准不同）。

## 表 4–3：C++11 中定义的分布

| 分布 | 生成的值 |
|---|---|
| 均匀分布 | |
| uniform_int_distribution | 整数 |
| uniform_real_distribution | 实数 |
| 伯努利分布 | |
| bernoulli_distribution | 布尔值 |
| binomial_distribution | 整数 |
| negative_binomial_distribution | 整数 |
| geometric_distribution | 整数 |
| 泊松分布 | |
| poisson_distribution | 整数 |
| exponential_distribution | 实数 |
| gamma_distribution | 实数 |
| weibull_distribution | 实数 |
| extreme_value_distribution | 实数 |
| 正态分布 | |
| normal_distribution | 实数 |
| lognormal_distribution | 实数 |
| chi_squared_distribution | 实数 |
| cauchy_distribution | 实数 |
| fisher_f_distribution | 实数 |
| student_t_distribution | 实数 |
| 采样分布 | |
| discrete_distribution | 整数 |
| piecewise_constant_distribution | 实数 |
| piecewise_linear_distribution | 实数 |

## 4.2.2.5 使用分布

分布由随机数生成器参数化，例如：

```
default_random_engine re(random_device()());
normal_distribution<> normal;
```

```
for (int i= 0; i < 6; ++i)
    cout << normal(re) << endl;
```

此处我们创建了一个引擎——在构造函数中随机化——以及一个类型为 double、使用默认参数 μ = 0.0 和 σ = 1.0 的正态分布。在每次调用基于分布的生成器时，我们将随机引擎作为参数传递。以下是程序输出示例：

```
-0.339502
0.766392
-0.891504
0.218919
2.12442
-1.56393
```

当然，每次调用时结果都会不同。或者，我们可以使用 <functional> 头文件（§4.4.7）中的 bind 函数将分布绑定到引擎：

```
auto normal= bind(normal_distribution<>{},
    default_random_engine(random_device()())) ;
```

```
for (int i= 0; i < 6; ++i)
    cout << normal() << endl;
```

> C++14 函数对象 normal 现在可以不带参数调用。在这种情况下，bind 比 lambda 更简洁——即使使用 Init Capture（§3.8.1.3）：

```
auto normal= [re= default_random_engine(random_device()()),
    n= normal_distribution<>{}]() mutable
    { return n(re); };
```

在大多数其他场景中，lambda 表达式产生的程序源代码比 `bind` 更易读，但后者似乎更适合将随机引擎绑定到分布。

## 4.2.2.6 股价演化的随机模拟

利用正态分布，我们可以在 Fischer Black 和 Myron Scholes 的 Black-Scholes 模型中模拟股票股价的可能演化。数学背景例如在 Jan Rudli 的讲座 [54, 第 94–95 页]（不幸的是，是德语）以及其他定量金融出版物（如 [76]）中有所讨论。从初始价格 $s_0 = S_0^1$、预期收益率 $\mu$、波动率 $\sigma$、服从正态分布的随机值 $Z_i$ 和时间步长 $\Delta$ 出发，时刻 $t = i \cdot \Delta$ 的股价相对于前一时刻通过以下方式模拟：

$S_{i \cdot \Delta}^1 \sim S_{(i-1) \cdot \Delta}^1 \cdot e^{\sigma \cdot \sqrt{\Delta} \cdot Z_i + \Delta \cdot (\mu - \sigma^2 / 2)}$

令 $a = \sigma \cdot \sqrt{\Delta}$ 和 $b = \Delta \cdot (\mu - \sigma^2 / 2)$，方程简化为

$S_{i \cdot \Delta}^1 \sim S_{(i-1) \cdot \Delta}^1 \cdot e^{a \cdot Z_i + b}$。 (4.2)

=> c++11/black_scholes.cpp

根据 (4.2)，使用参数 $\mu = 0.05$、$\sigma = 0.3$、$\Delta = 1.0$ 和 $t = 20$ 作为常数，$S^1$ 的演化现在可以用几行代码编程实现：

点击此处查看代码图片

```cpp
default_random_engine re(random_device()());
normal_distribution<> normal;

const double mu= 0.05, sigma= 0.3, delta= 0.5, years= 20.0,
           a= sigma * sqrt(delta),
           b= delta * (mu - 0.5 * sigma * sigma);
vector <double> s = {345.2}; // Start with initial price

for (double t= 0.0; t < years; t+= delta)
  s.push_back(s.back() * exp(a * normal(re) + b) );
```

图 4-8 描绘了前一段代码中参数的五种可能的股价演化。

