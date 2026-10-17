
- [5] 如果日期是计算的结果，使用 `ok()` 检查有效性；§16.2.2。
- [6] 在处理不同位置的时间时，使用 `zoned_time`；§16.2.3。
- [7] 使用 lambda 表达式调用约的微小变化；§16.3.1。
- [8] 使用传统的函数调用时，使用 `mem_fn()` 或 lambda 创建一个可以调用成员函数的函数对象；§16.3.1, §16.3.2。
- [9] 当你需要存储某些可以被调用的内容时，使用 `function`；§16.3.3。
- [10] 优先使用概念（concepts）而不是显式使用类型谓词；§16.4.1。
- [11] 你可以编写代码显式地依赖类型的属性；§16.4.1, §16.4.2。
- [12] 尽可能优先使用概念而不是特质（traits）和 `enable_if`；§16.4.3。
- [13] 使用 `source_location` 在调试和日志消息中嵌入源代码位置；§ 16.5。
- [14] 避免显式使用 `std::move()`；§ 16.6; [CG: ES.56]。
- [15] 专门使用 `std::forward()` 进行转发；§ 16.6。
- [16] 在 `std::move()` 或 `std::forward()` 之后，永远不要从对象中读取；§ 16.6。
- [17] 使用 `std::byte` 表示（尚未）具有意义类型的数据；§ 16.7。
- [18] 使用无符号整数或位进行位操作 § 16.7。
- [19] 如果期望直接调用者能够处理问题，则从函数返回错误码；§16.8。
- [20] 如果无法期望直接调用者能够处理问题，则从函数中抛出异常；§16.8。
- [21] 如果尝试从问题中恢复是不合的，请调用 `exit()`、`quick_exit()` 或 `terminate()` 来退出程序；§16.8。
- [22] 任何通用库都不应该终止；§16.8。

# 17 数值

计算的目的是洞察，而不是数字。对于学生来说，数字往往是通往洞察的最佳道路。

## 17.1 引言

C++ 的设计初衷并不是为了数值计算。然而，数值计算通常发生在其他工作的范围内——例如科学计算、数据库访问、网络、仪表控制、模拟和财务分析——因此 C++ 成为大型系统中部分计算的极具载体。此外，数值方法已经从对浮点数的简单循环发展了很久。因此，最终结果是 C++ 被广泛用于科学、工程和其他涉及数值的计算。本章描述了标准库中支持数值的部分。

- 数学函数
- 数值算法
- 复数
- 随机数
- 向量算术
- 数值极限
- 类型别名
- 建议

## 17.2 数学函数

在 `<cmath>` 中，我们找到了标准的数学函数，如针对 `float`、`double` 和 `long double` 类型参数的 `sqrt()`、`log()` 和 `sin()`：

| 定的标准数学函数 |
|---|---|
| `abs(x)` | 绝对值 |
| `ceil(x)` | 大于 x 的最小整数 |
| `floor(x)` | 小于 x 的最大整数 |
| `sqrt(x)` | 平方根；x 必须是非负 |
| `cos(x)` | 余弦 |
| `sin(x)` | 正弦 |
| `tan(x)` | 正切 |
| `acos(x)` | 反余弦；结果为非负 |
| `asin(x)` | 反正弦；返回最接近 0 的结果 |
| `atan(x)` | 反正切 |
| `sinh(x)` | 双曲正弦 |
| `cosh(x)` | 双曲余弦 |
| `tanh(x)` | 双曲正切 |
| `exp(x)` | 以 e 为底的指数 |
| `exp2(x)` | 以 2 为底的指数 |
| `log(x)` | 自然对数，底为 e；x 必须为正 |
| `log2(x)` | 自然对数，底为 2；x 必须为正 |
| `log10(x)` | 以 10 为底的对数；x 必须为正 |

```cpp
errno = 0;      // 清除错误状态
double d = sqrt(-1);
if (errno==EDOM) {
    cerr << "sqrt() 未为负数定义";
}
errno = 0; // 清除旧错误状态
double dd = pow(numeric_limits<double>::max(), 2);
if (errno == ERANGE) {
    cerr << "pow() 结果太大";
}
```

更多的数学函数位于 `<cmath>`。所谓的特殊数学函数如 `beta(x)`、`zeta(j)` 和 `sph_bessel(j)` 也在 `<cmath>` 中。

## 17.3 数值算法

在 `<numeric>` 中，我们找到一组通用数值算法，如 `accumulate()`。

| 数值算法 |
|---|---|
| `accumulate(b,e,i)` | x 是 i 和 [b:e) 元素的和 |
| `accumulate(b,e,i,f)` | 使用 f 进行累加 |
| `inner_product(b,e,b2,i)` | x 是 [b:e) 和 [b2:b2+(e-b)] 的内积 |
| `inner_product(b,e,b2,i2,f,f2)` | 使用 f 和 * 进行内积 |
| `partial_sum(b,e,out)` | [out:out) 的元素 i 是 [b:b+i) 的和 |
| `partial_sum(b,e,out,f)` | 使用 f 进行部分和 |
| `adjacent_difference(b,e,out)` | 当 i>0 时，[out:out) 的元素 i 是 (b+i)-(b-1)；如果 e-b>0，则 out 为 b |
| `adjacent_difference(b,e,out,f)` | 使用 f 进行相邻差 |
| `iota(b,v,v)` | 为范围内的每个元素赋值 v 并递增；因此序列变为 v, v+1, v+2... |
| `gcd(n,m)` | x 是整数 n 和 m 的最大公约数 |
| `lcm(n,m)` | x 是整数 n 和 m 的最小公倍数 |
| `midpoint(n,m)` | x 是 n 和 m 之间的中点 |

这些算法通过让适用于所有类型的序列来泛化常用操作（如求和）。它们还让这些序列元素的操作成为一个参数。对于每个算法，通用版本都补充了一个使用该算法最常用运算符的版本。例如：

点击此处查看图像

```cpp
list<double> lst(1, 2, 3, 4, 5, 9999.99999);
auto s = accumulate(lst.begin(),lst.end(),0.0);
```

> // 它计算了和：10014.99999

这些算法适用于所有的标准库序列，并可以提供参数的操作 (§17.3)。

### 17.3.1 并行数值算法

在 `<numeric>` 中，数值算法 (§17.3) 具有并行版本，它们与顺序版本略有不同。特别是，并行版本允许以不指定的顺序对元素进行操作。并行数值算法还可以接受一个执行策略参数 (§13.6)：`seq`、`unseq`、`par` 和 `par_unseq`。

| 并行数值算法 | |
| :--- | :--- |
| `x=reduce(b,e)` | x=`accumulate(b,e,v)`, 但顺序不确定的 |
| `x=reduce(b,e)` | x=`reduce(b,e,v)`, 其中 v 是 b 的值 |
| `x=reduce(pol,b,e)` | 使用执行策略 pol 的 x=`reduce(b,e,v)` |
| `x=reduce(pol,b,e)` | p=`partial_sum(b,e,v)`, 其中 v 是 b 的值 |
| `p=exclusive_scan(pol,b,e,out)` | p=`partial_sum(b,e,out)`, 从第 i 个和中排除第 i 个输入元素 |
| `p=inclusive_scan(pol,b,e,out)` | p=`partial_sum(b,e,out)`, 将第 i 个输入元素包含在第 i 个和中 |
| `p=transform_reduce(pol,b,e,f,v)` | 对于 [b:e) 中的 x 执行 f(x)，然后 reduce |
| `p=transform_exclusive_scan(pol,b,e,out,f,v)` | 对于 [b:e] 中的 x 执行 f(x)，然后执行 exclusive_scan |
| `p=transform_inclusive_scan(pol,b,e,out,f)` | 对于 [b:e] 中的 x 执行 f(x)，然后执行 inclusive_scan |

为了简单起见，我保留了这些接受操作作为参数的版本，而不是仅仅使用 `+` 和 `*`。除了 `reduce()` 之外，我还保留了带有默认策略（顺序）和默认值的版本。

与 `<algorithm>` 中的并行算法 (§13.6)一样，我们可以指定执行策略：

点击此处查看代码图片

```
vector<double> v(1, 2, 3, 4, 5, 99999999);
auto s = reduce(v.begin(),v.end()); // 使用 double 作为累加器计算和
vector<double> large;
// 用大量值填充 large ...
auto s2 = reduce(par_unseq,large.begin(),large.end()); // 它利用可用并行性计算和
```

执行策略 `par`、`seq`、`unseq` 和 `par_unseq` 隐藏在 `<execution>` 的 `std::execution` 命名空间中。

通过测量来验证并行或向量化算法是否值得。

## 17.4 复数

标准库支持一组与 §5.2.1 中描述的 `complex` 类类似的复数类型。为了支持标量为单精度浮点数（floats）、双精度浮点数（doubles）等的复数，标准库的 `complex` 是一个模板：

点击此处查看代码图片

```cpp
template<typename Scalar>
class complex {
public:
    complex(const Scalar& re = {}, const Scalar& im = {}); // 默认函数参数；参见 3.4.1
    // ...
};
```

复数支持常用的算术操作和常见的数学函数。例如：

点击此处查看代码图片

```cpp
void f(complex<float> fl, complex<double> db) {
    complex<long double> ld (fl+sqrt(db));
    db += fl^3;
    fl = pow(1/fl,2);
    // ...
}
```

`sqrt()` 和 `pow()`（幂）函数是 `<complex>` (17.2) 中定义的常用数学函数。

## 17.5 随机数

随机数在许多范围内非常有用，例如测试、游戏、模拟和安全。应用领域的广泛性体现在标准库 `<random>` 提供的丰富随机数生成器中。随机数生成器由两部分组成：

- [1] 一个产生随机或伪随机值序列的引擎
- [2] 一个将这些值映射到某个范围内数学分布的分布器

分布的示例包括 `uniform_int_distribution`（所有整数产生的概率相等）、`normal_distribution`（“钟形曲线”）和 `exponential_distribution`（指数级增长）；每个对应某些样本示例。

点击此处查看代码图片

```cpp
using my_engine = random_engine;
using my_distribution = uniform_int_distribution<>;

my_engine eng;
my_distribution dist(1,6);
auto die = [&]{ return dist(eng); };

int x = die();
```

- 引擎的类型
- 分布的类型
- 引擎的默认版本
- 映射到整数 1 ..6 的分布
- 创建一个生成器
- 掷骰子：x 变为 [1:6] 中的一个值

得益于对质量和性能不妥协的关注，一位专家认为标准库随机数组件在成长后属于哪一个数值库。然而，它很难称得上“学者友好”。`using` 语句和 lambda 表达式让它变得直观了一些。

对于初学者（任何背景的）来说，随机数库的完全通用接口可能是一个严重的障碍。一个简单的均匀随机数生成器通常足够入门。例如：

点击此处查看代码图片

| Rand_int rnd(1,1) | 创建一个生成器 |
| :--- | :--- |
| int x = die(); | 掷骰子：x 变为 [1:6] 中的一个值 |
| uniform_distribution dist(1,6); | 映射到整数 1 ..6 的分布 |
| my_engine eng; | 引擎的默认版本 |
| my_distribution | 分布的类型 |
| using my_engine | 引擎的类型 |

| 特性 | 描述 |
| :--- | :--- |
| 引擎的类型 | `my_engine` |
| 分布的类型 | `my_distribution` |
| 引擎的默认版本 | `eng` |
| 映射到整数 1 ..6 的分布 | `dist(1,6)` |
| 创建一个生成器 | `auto die = [&]{ return dist(eng); };` |
| 掷骰子：x 变为 [1:6] 中的一个值 | `int x = die();` |
