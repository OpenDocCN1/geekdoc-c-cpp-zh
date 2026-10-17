
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

## 17.6 向量算术

The vector was designed in §12.2 to be a general mechanism for holding values, rather than flexible, and to fit the architecture of containers, iterators, and algorithms. However it does not support vector operations. Consequently, the standard library provides a `<valarray>`-like template, called `valarray`, that is less general and more amenable to optimization for numerical computation:

```cpp
template<typename T>
class valarray {
// ...
};
```

The usual arithmetic operations and the most common mathematical functions are supported by `valarray`. For example:

```cpp
valarray<double> a = a1*3.14+a2/a1; // numeric array operations +, /, and =
a2 += a*3.14;
a = abs(a);
```

The operations are vector operations; that is, they are applied to each element of the vectors involved.

In addition to arithmetic operations, `valarray` offers stride access to help implement

多维计算。

## 17.7 数值限制

在限制方面，标准库提供了用于描述内置类型属性的类——例如，浮点数的最大指数或整数的字节数。例如，我们可以断言 `char` 是有符号的：

点击此处查看代码图像

```
static_assert(numeric_limits<char>::is_signed
```

第二种（也是唯一的）之所以有效，是因为 `numeric_limits<int>::max()` 是一个 `constexpr` 函数 (1.6)。

我们可以为自己的用户定义类型定义 `numeric_limits`。

## 17.8 类型别名

基本类型（如 `int` 和 `long long`）的大小由实现定义；也就是说，它们在不同的 C++ 实现中可能有所不同。如果我们需要指定整数的大小，可以使用 `<stdint>` 中的别名，如 `int32_t` 和 `uint_64_t`。后者表示至少为 64 位的无符号整数。

奇特的 `_t` 后缀是 C 时代的遗留，在那个时代，认为一个能够反映而非别名的名称是重要的。

其他别名，例如 `size_t`（`sizeof` 返回的类型）和 `ptdiff_t`（一个指针减去另一个指针的结果类型）可以在 `<stddef>` 中找到。

## 17.9 数学常数

在进行数学计算时，我们需要常见的数学常数，如 `e`、`pi` 和 `log2`。标准库提供了它们。它们以两种形式存在：一个允许我们指定精确类型的模板（例如 `pi_v<T>`），以及一个最常用场景的短名称（例如 `pi_v<double>`）。例如：

点击此处查看代码图像

```
void area(float r)
{
    using namespace std::numbers; // 数学常数存储在这里

    double d = pi_v<double>*r*r;
    float f = pi_v<float>*r*r;

    // ...
}
```

在这种情况下，差异很小（我们必须以 16 位左右的精度才能看到它），但在真实的物理计算中，这些差异会迅速变得显著。在图形学和 AI 领域，常数的精度至关重要，而更小的数值表示也变得越来越重要。

在 `<numbers>` 中，我们找到了 `e`（欧拉数）、`log2`（e的对数）、`log10e`（e的10底对数）、`pi`、`inv_pi` (1/pi)、`inv_sqrtpi` (1/sqrt(pi))、`ln2`、`ln10`、`sqrt2` (sqrt(2))、`sqrt3` (sqrt(3))、`inv_sqrt3` (1/sqrt3)、`gamma`（欧拉常数）以及 `phi`（黄金比例）。

自然地，我们想要更多针对领域的数学常数和类型。这很容易实现，因为常数是变量模板，并针对 `double`（或该领域最有用的任何类型）进行了特化：

点击此处查看代码图像

```
template<typename T>
constexpr T tau_v = 2*pi_<T>;
constexpr double tau = tau<double>;
```

## 17.10 建议

- [1] 数值问题通常是微妙的。如果你对数值问题的数学方面不是百分之百确定，请取专家建议、进行实验或两者兼顾；§17.1。
- [2] 不要尝试只使用基础语言进行严肃的数值计算；请使用库；§17.1。
- [3] 在编写循环从序列中计算值之前，考虑 `accumulate()`、`inner_product()`、`partial_sum()` 和 `adjacent_difference()`：§17.3。
- [4] 对于大量数据，尝试使用并行和向量化算法；§17.3.1。
- [5] 使用 `std::complex` 进行复数运算；§17.4。
- [6] 将引擎绑定到你的随机数生成器；§17.5。
- [7] 注意确保你的随机数对于预期的用途具有足够的随机性；§17.5。
- [8] 不要使用 C 库的 `rand()`；它对于实际用途来说随机性不够；§17.5。
- [9] 当运行效率比相对于操作和元素类型的灵活性更重要时，使用 `varray` 进行数值计算；§17.6。
- [10] 数值类型的属性可以通过 `numeric_limits` 访问；§17.7。
- [11] 使用 `numeric_limits` 检查数值类型对于其用途是否足够；§17.7。
- [12] 如果你想指定整数类型的大小，请为整数类型使用别名；§17.8。

# 18 并发

> 保持简单：尽可能简单，但不要过简单了。
> – 阿尔伯·爱因斯坦

- 引言
- 任务与线程
  - 传递参数；返回结果
- 共享数据
  - 互斥锁与锁；原子
- 等待事件
- 任务通信
  - future 和 promise; packaged_task; async(); 停止线程
- 协程
  - 协作式多任务
- 建议

## 18.1 引言

并发——多个任务的并行执行——被广泛用于提高吞吞吐量（通过为单个计算使用多个处理器）或提高响应能力（通过允许程序的一个部分在等待响应时，另一部分能够继续运行）。所有现代编程语言都为此提供了支持。C++ 标准库提供的支持是 C 语言中使用了 20 多年的方案的可移植且类型安全的变体，并且几乎被现代硬件通用支持。标准库的支持主要针对支持系统级并发，而不是直接提供复杂的层层并发模型；这些模型可以使用使用标准库设施的库提供。

标准库支持在地址空间内并发执行多个线程。为了实现这一点，C++ 提供了一了一个合适的内存模型和一组原子操作。原子操作允许无锁编程 [Devchev,2010]。内存模型确保了只要程序员避免数据竞态（对可变数据的无控制并发访问），一切都会像人们直观预期的那样工作。然而，大多数用户会在标准库以及构建在它们之上的库看到并发。本节简要介绍了标准库并发设施的示例：线程、mutex、`lock()` 操作、packaged_tasks 和 futures。这些特性直接构建在操作系统之上，与操作系统相比不会产生性能代价。它们也没有保证比操作系统提供的有显著的性能提升。

不要单独地考虑并发。如果一个任务可以按顺序执行，那么顺序执行通常更快且更容易。从一个线程传递信息到另一个线程开销可能巨大。

作为使用并发特性的替代方案，我们可以使用并行算法来利用多个执行引擎来提高性能 (§13.6, §17.3.1)。

最后，C++ 支持协程；即在调用之间保持其状态的函数 (§18.6)。

## 18.2 任务与线程

我们将一个可能与其他计算一起执行的计算称为任务（task）。线程是任务在程序中的系统级表示。要与其他线程并发执行的任务是通过构造一个线程（在 `<thread>` 中）并以任务作为参数来启动的。任务是一个函数或函数对象：

点击此处查看代码图像

```
void f();
struct F {
    void operator()();
};
void user(void (*f)()) {
    thread t1(f);
    thread t2(F{});

    t1.join();
    t2.join();
}
```

`join()` 确保了我们在线程完成之前不会执行 `exit()`。“join”一个线程意味着“等待线程终止”。

很容易忘记调用 `join()`，而且结果通常很糟糕，因此标准库提供了 `jthread`，它是一个“自动连接的线程”，通过在析构函数中调用 `join()` 遵循了 RAII：

点击此处查看代码图像

```
void user()
{
    thread t1(f);    // f 在单独线程中执行
    thread t2(F());   // F() 在单独线程中执行
}
```

连接是通过析构函数完成的，因此顺序与构造相反。在这里，我们先等待 t2 再等待 t1。

程序的线程共享单个地址空间。在此空间内，线程与进程不同，进程通常不共享数据。由于线程共享地址空间，它们可以通过共享对象进行通信 ($18.3)。这种通信通常由锁或其他机制控制，以防止对变量的数据并发访问。

编写并发任务可能非常复杂。考虑任务 `f`（函数）和 `F`（函数对象）的可能实现：

点击此处查看代码图像

```
void f()
{
    cout << "Hello";
}
struct F
{
    void operator() { cout << "Parallel World!\n"; }
}
```

这是一个错误的错误示例；`f` 和 `F` 分别使用对象 `cout` 而没有使用任何形式的同步。结果的输出将不可预测的，并且在程序不同的执行运行之间发生变化，因为两个任务中单独操作的执行顺序没有定义。程序可能会产生“奇怪”的输出，例如

Parallel to World!

只有标准库中的特定保证保护我们不受 `ostream` 定义内部的数据竞态，这可能导致崩溃。

为了避免此类输出问题，让每个线程使用一个流或使用 `osyncstream` ($11.7.5)

在定义并发程序的任务时，我们的目标是保持它们完全分离，仅通过简单明显的方式进行通信。并发任务最简单的思考方式是一个恰好与其调用者并发运行的函数。为了让这工作，我们只需要传递参数、获取结果，并确保中间没有共享数据的使用（没有数据竞态）。

```cpp
void f(vector<double>& v); // Il函数：对 v 进行操作
```

```cpp
struct F {
    vector<double>& v; // Il函数对象：对 v 进行操作
    F(vector<double>& v, double vv) :v(vv) {}
    void operator()(); // Ill运算符：$7.3.2
};
```

```cpp
int main() {
    vector<double> some_vec(1, 2, 3, 4, 5, 6, 7, 8, 9);
    vector<double> vec2(10, 11, 12, 13, 14);
    thread t1(f, some_vec); // Il f(some_vec) 在另一个线程中执行
    thread t2(F(vec2)); // Il F(vec2) 在另一个线程中执行
}
```

`F(vec2)` 将参数保存到 `F` 中的 vector 中。`F` 现在可以使用 `vec2`，并且希望在它执行期间没有其他任务接受 `vec2`。通过按值传递 `vec2` 则会消除这种风险。

使用 `{ref(some_vec)}` 的初始化使用了一个线程变长模板构造函数，该构造函数可以接受任意序列的参数 ($8.4)。`ref` 是来自 `<functional>` 的一个类型函数，遗憾的是，它需要告诉变长模板将 `some_vec` 视为引用而非对象。如果没有 `ref()`，`some_vec` 将按值传递。编译器会检查在给定后续参数的情况下是否调用了第一个参数，并构建必要的函数对象以传递给线程。因此，如果 `F::operator()` 和 `f` 执行相同的算法，那么处理这两个任务的方式是等价的：在两种情况下，都为线程构造了一个执行所需的函数对象。

### 18.2.2 返回结果

在示例 §18.1 中，我通过非 const 引用引用传递参数。只有当我预计任务会修改所引用数据的值时，我才会这样做 ($1.7)。这是一种返回结果的隐晦方法，但并不罕见。不那么晦涩的技术是通过 const 引用传递输入数据，并将存放结果的位置作为单独的参数传递：

点击此处查看代码图像

```cpp
void f(const vector<double>& v, double* res); // Il 来自 v 的输入，将结果存放在 *res 中
```

```cpp
class F {
public:
    F(const vector<double>& vv, double* p) :v(vv), res(p) // Il 将结果存放在 *res 中
    void operator()();
private:
    const vector<double>& v; // Il 输入源
    double* res; // Il 输出目标
};
```

```cpp
double g(const vector<double>&); // Il 使用返回值
```

```cpp
void user(vector<double>& vec1, vector<double> vec2, vector<double> vec3) {
    double res1;
}
```

```cpp
double res2;
double res3;
```
