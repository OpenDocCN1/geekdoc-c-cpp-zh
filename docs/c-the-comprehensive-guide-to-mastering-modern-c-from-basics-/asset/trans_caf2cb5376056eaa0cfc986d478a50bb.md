
随机数。如果你看到 0.0，则使用了另一种——确定性的——引擎。

引擎实现了 28.3.3 其他生成器中的 `operator()`，它返回一个随机的原始位序列。

对于真正的实验，你还不能对其做很多事情。只有当与分布结合时，它才会变成正确范围内的随机数。

分布——例如 `uniform_int_distribution<int> d6{0,5}`——也重载了 `operator()`。如果你将引擎作为参数传递给它，位序列就会变成一个合适的随机数——对于范围在 0 到 5（包含）之间的 d6 来说，每个引擎的结果都是如此。

不同引擎返回的位序列质量有所不同。这种质量在数学上是可计算的，在某些场景下至关重要。我们的确定性计算机难以实现真正的随机性。因此，算法生成的只是伪随机性，所谓的伪随机数。

根据经验法则，生成位的时间越耗费，随机数序列就越好。我在这里写了一个程序，首先允许你测量单个引擎的速度，其次会显示当前系统中可能存在的所有引擎。

```
// https://godbolt.org/z/e67356bMgq
#include <random>
#include <chrono> // system_clock
#include <format>
```

#include <iostream>

using namespace std;
using namespace chrono;
const size_t LOOPS = 10*1000*1000;

template<typename ENGINE>
void measure(const string &title, ENGINE &engine) {
    const auto start = steady_clock::now();
    /* work hard */
    unsigned long long checksum = 0;
    size_t loops = LOOPS;
    while(loops-- > 0) {
        checksum += engine();
        const auto now = steady_clock::now();
        nanoseconds dur_ns = now - start;
        cout << std::format("{}: {:2}S ns/loop {:12} ns\n",
            title, dur_ns.count() / LOOPS, dur_ns.count());
    }
}

int main() {
    { random_engine e; measure("default", e); }
    { random_device e; measure("device", e); }
    { minstd_0 e; measure("minstd_0", e); }
    { minstd_rand e; measure("minstd_rand", e); }
    { mt19937 e; measure("mt19937", e); }
    { mt19937_64 e; measure("mt19937_64", e); }
    { ranlux24_base e; measure("ranlux24_base", e); }
    { ranlux48_base e; measure("ranlux48_base", e); }
    { ranlux24 e; measure("ranlux24", e); }
    { ranlux48 e; measure("ranlux48", e); }
    { knuth_b e; measure("knuth_b", e); }

    using wide_t = unsigned long long;
    independent_bits<ranlux48, sizeof(wide_t)*8, wide_t> e("indepranlux", e);

    using wide_t = unsigned long long;
    independent_bits<default_random_engine, 
        sizeof(wide_t)*8, wide_t> e;
    e();
    measure("indepdefault", e);
}
```

列表 28.18 随机数生成器的速度。

当然，结果在不同的系统上总是会有不同。
考虑以下片段：

| default: | 12 ns/loop | 12634216 ns |
| device: | 41 ns/loop | 41745604 ns |
| minstd_0: | 12 ns/loop | 12235403 ns |
| indep<ranlux>: | 1086 ns/loop | 10865402 |

你可以看到，这里的 `device` 并不慢，如果你使用 `indep<ranlux>`，是有原因的。

## 28.3.4 分布

随机数可以以各种特征生成——从简单的六面骰到浮点值。

对于六面骰，1 到 6 的每个数字出现的概率大致相等。但其他实验则不同。如果你投掷 10 枚硬币（一起）并统计正面次数，那么 0 到 10 的可能结果符合二项分布。如果你连续重复这个实验，你看到的正面次数比 5 次要少。对于这样的实验，你不需要从计算机生成 10 次正反面，可以使用 `binomial_distribution` 直接生成 0 到 10 之间的数字。你已经在列表 28.17 中看到单个骰子的均匀分布是什么样了。让我们使用列表 28.19 中的二项分布来模拟掷 10 枚硬币。

```
// https://godbolt.org/z/rv5Ya
#include <random>
#include <vector>
#include <iostream>
using namespace std;
int main() {
    static size_t size = 10;

    default_random_engine e(); // 随机生成器
    vector<size_t> counts(size+1);
    binomial_distribution<int> coins(size); // 掷10 枚硬币
    for(auto i=0; i<10000; ++i) // 掷硬币
        ++counts[coins(i)];
    for(auto c : counts) cout << c << " ";
    cout << '\n'; // 输出示例：
    // 10 195 5344 14043 24806 29505 24544 13973 5252 110 15
}
```

列表 28.19 二项分布。

如你所见，得到 0 次正面的概率远小于得到 6 次正面。假设你想要一个均匀分布，但这次不是 int 值，而是 double。你需要一个不同的分布函数——`uniform_real_distribution<double>`。

```
// https://godbolt.org/z/94Mccs
#include <random>
#include <iostream>

int main() {
    std::default_random_engine e();
    std::uniform_real_distribution<double> unif{3,7}; // 在半开区间 [3,7) 内
    double u = unif(e); // 生成随机数
    std::cout << u << '\n'; // 输出示例：
    // 3.52615
}
```

列表 28.20 一个“double”随机数。

## 每次都不同

如果你已经在 `uniform_int_distribution<int>` 的构造函数中提供了生成随机数的范围，那么当边界每次变化时，你都需要创建一个新的分布吗？

幸运的是，不需要。每个分布都有一个与该分布构造参数相同的 `param_type`。你可以将这样一个 `param_type` 实例传递给 `operator()` 的调用，从而改变每次调用时的生成条件。

```
// https://godbolt.org/z/xz64K3e5
#include <random>
#include <iostream>
int main() {
    std::default_random_engine e();
    using Dstr = std::uniform_int_distribution<int>; // 生成
    Dstr card(e);
    for(int n=32; n>=1; --n) {
        std::cout << (e, Dstr::param_type{1,n}) << "\n"; // 在此处指定参数
    }
    std::cout << '\n';
    // 输出示例：
    // 1 25 13 14 15 6 2 17 22 9 11 17 1 1 10 11 6 1 6 8 9 7 4 1
}
```

列表 28.21 为每个随机数单独更改生成参数。

在这里我模拟牌组每次抽牌减少一张。程序会打印不断减少的牌组中的点牌号。

## 分布之分布

所有分布的精确公式及其参数化的含义，当然在标准中已经提到了。对数学感兴趣的人来说，名称可能意味着更多。对于这些人来说，分布函数的参数化可能更有趣。在表 28.4 中，real 代表浮点数类型（如 float 或 double）。int 代表整数类型（如 int），但当然像 long long 等其他类型也是可能的。

| 分布 | 分布参数 |
| --- | --- |
| 均匀分布 | |
| uniform_int_distribution | Int a = 0, Int b = max() |
| uniform_real_distribution | Real a = 0.0, Real b = 1.0 |
| Bernoulli 族 | |
| bernoulli_distribution | double p = 0.5 |
| binomial_distribution | Int t = 1, double p = 0.5 |
| geometric_distribution | double p = 0.5 |

| 分布 | 分布参数 |
|---|---|
| negative_binomial_distribution | Int k = 1, double p = 0.5 |
| 泊松族 | |
| poisson_distribution | double mean = 1.0 |
| exponential_distribution | Real lambda = 1.0 |
| gamma_distribution | Real alpha = 1.0, Real beta = 1.0 |
| weibull_distribution | Real a = 1.0, Real b = 1.0 |
| extreme_value_distribution | Real a = 0.0, Real b = 1.0 |
| 正态分布 | |
| normal_distribution | Real mean = 0.0, Real stddev = 1.0 |
| lognormal_distribution | Real m = 0.0, Real s = 1.0 |
| chi_squared_distribution | Real n = 1 |
| cauchy_distribution | Real a = 0.0, Real b = 1.0 |
| fisher_f_distribution | Real m = 1, Real n = 1 |
| student_t_distribution | Real n = 1 |
