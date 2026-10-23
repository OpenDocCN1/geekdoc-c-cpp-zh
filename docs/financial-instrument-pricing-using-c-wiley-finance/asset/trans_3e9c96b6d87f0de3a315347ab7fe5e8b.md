

不超过 x 的数（这称为素数计数函数）。然后素数定理（Hunter, 1964）指出：

lim x → ∞ π(x) / (x / log x) = 1. (30.1)

我们还可以比较使用 PPL 的处理时间与相应的顺序代码。一种使用 Boost 动态位集的实现是：

```
const int n = 20;
std::set<int> mySet2;
std::cout << "Add elements to set ...: " << '\n';

for (std::size_t i = 0; i < n; ++i)
{
    mySet2.insert(i);
}

boost::dynamic_bitset<unsigned int> bs(n);

for (auto i = std::begin(mySet2); i != std::end(mySet2); ++i)
{
    if (IsPrime(*i))
    {
        bs.flip(static_cast<unsigned int>(*i));
    }
}
```

最后，我们可以检查所产生的数字确实是素数，因为对于任意两个素数，它们的最大公约数是 1，最小公倍数是它们的乘积。为此，我们应用 Boost Math Common Factor 库中的功能：

```
// Using unsigned long (compile time)
unsigned int p1 = 167; unsigned int p2 = 661;

// GCD(p1,p2) = 1 LCM(p1,p2) = p1*p2 for two primes p1 and p2
std::cout << "GCD and LCM of " << p1 << " and " << p2 << " are "
          << boost::math::gcd<unsigned int>(p1, p2) << " and "
          << boost::math::lcm<unsigned int>(p1, p2) << ", p1*p2: "
          << p1*p2 << '\n';
```

数论曾经被认为是一个没有实际应用的领域，但在近年来越来越多的素数被用作公钥密码算法的基础。它们也用于哈希表和伪随机数生成器。

## 30.4.2 一个扩展示例：合并和过滤集合

在本节中，我们给出一个可视为 MapReduce 简单情况的示例（参见 Miner and Shook, 2012）。MapReduce 是一种编程模型和实现，用于使用集群上的并行分布式算法处理和生成大型数据集。MapReduce 程序由一个执行过滤和排序的 Map( ) 方法和一个执行汇总操作的 Reduce( ) 方法组成。该模型是数据分析中 split-apply-combine 策略的特化。

作为这种模式的第一个示例，我们考虑创建一个集合集合，计算它们的成对并集，然后将这些集合合并为一个集合，即它们的并集。这样我们就避免了重复，从而减少了需要存储的数据量。首先，我们创建集合：

```
std::set<int> ms1;
for (int n = 1; n <= 5; ++n) { ms1.insert(n); }
std::set<int> ms2;
for (int n = 1; n <= 10; ++n) { ms2.insert(n); }
std::set<int> ms3;
for (int n = 11; n <= 50; ++n) { ms3.insert(n); }
std::set<int> ms4;
for (int n = 41; n <= 100; ++n) { ms3.insert(n); }

std::vector<std::set<int>> input{ ms1, ms2, ms3, ms4 };
```

下一步是定义从输入集合的元素计算的线程本地集合：

```
// Define and compute the local combiner sum (in parallel)
concurrency::combinable<std::set<int>> localSet([]()
{ return std::set<int>(); });

// Compute each local sum
concurrency::parallel_for(std::size_t(0), input.size(),
[&] (std::size_t i)
{
    // Each 'local' is a set<int>. Take the union of the current set and
    // thread-local set. 'Union' is a handy wrapper function for STL
    // std::set_union()
    Union<int>(input[i], localSet.local());
});
```

最后，我们聚合线程本地集合以产生最终结果，我们就完成了！

```
std::set<int> result;
// Add up local contributions and print it
// Merge each thread-local computation into the final result.
localSet.combine_each([&] (std::set<int>& local)
{
    Union<int>(local, result);
});

// Print the result
for (const auto& elem : result)
{
    std::cout << elem << ",";
}
```

```
void InsertValues(Vector& v, std::size_t L, std::size_t U)
{
    for (std::size_t i = L; i < U; ++i)
    {
        std::this_thread::sleep_for(std::chrono::milliseconds(2000));
        v.push_back(i);
    }
}

int main()
{
    Vector v;

    std::thread t1(InsertValues, std::ref(v), 0, 50);
    std::thread t2(InsertValues, std::ref(v), 50, 100);
    std::thread t3(InsertValues, std::ref(v), 100, 201);

    t1.join(); t2.join(); t3.join();
    std::cout << "Size: " << v.size() << '\n';

    // Combine the results.
    concurrency::combinable<int> sums;

    for (auto i = std::begin(v); i != std::end(v); ++i)
    {
        sums.local() += *i;
    }

    // Sum of 1st n integers = n(n+1)/2
    std::cout << "sum = " << sums.combine(std::plus<int>()) << '\n';
}
```

*并发对象* 是在组件之间并发共享的。并行计算并发对象的状态的过程产生的结果与串行计算相同状态的另一个过程产生的结果相同。`concurrency::combinable` 类（在第 30.4.1 节和第 30.4.2 节中引入）是并发对象类型的一个示例。*combinable* 类允许您并行执行计算，然后将这些计算合并为最终结果。我们在原本会使用同步机制的地方使用并发对象，例如使用互斥锁来同步对共享变量或资源的访问。

## 30.6 异步代理库和基于事件系统的介绍

在本节中，我们简要概述了一种并发模型，可视为基于共享状态的模型的替代方案。该模型基于 *独立组件* 之间的数据流，它们通过发送和接收消息相互通信。一种底层通信模式称为 *隐式调用*（也称为 *通知和发布-订阅* 惯用法（参见 GOF, 1995））。在这种情况下，我们不直接调用一个过程，而是组件宣布或广播一个或多个事件。系统中的其他组件可以通过将过程与其关联来注册（订阅）对事件的兴趣。当事件被宣布时，系统本身会调用所有为该事件注册的过程。因此，事件公告‘隐式’地导致其他模块中过程的调用（Shaw and Garlan, 1996）。简而言之，我们谈论的是基于事件或事件驱动的系统，这些系统的起源在于分组交换网络。特别是，没有全局时钟，时间模型受量子力学和狭义相对论的启发。每个代理都有自己的本地时间。

实现基于事件的系统的方法有很多。一些示例是：

- 使用面向对象的观察者模式（GOF, 1995）。
- 使用 Boost signals2 库（信号和槽）。
- 使用异步代理库（在本节中讨论）。

关于观察者模式和 Boost signals2 的讨论见 Demming and Duffy (2010)。

异步代理库（或简称为代理库）提供了基于参与者的编程模型（参见 Agha, 1990）和用于粗粒度数据流和流水线应用的消息传递接口。异步代理使应用程序能够利用延迟，在其他组件等待数据时执行工作。此功能减少了我们在使用线程时遇到的死锁。

### 30.6.1 代理库概述

异步代理（或代理）是与其它代理通信以解决更大计算任务的应用程序组件。并发运行时任务调度程序提供了一种高效的机制，使代理能够在无需抢占的情况下协作地阻塞和让出。

代理的生命周期如图 30.1 所示。代理在其生命周期中处于各种状态：

- created: 代理已被安排执行。
- runnable: 运行时正在为代理安排执行。
- started: 代理已启动并正在运行。
- done: 代理已完成处理。
- cancelled: 代理在进入 started 状态前已被取消。

异步代理库包括以下类型的消息块，在各种情况下很有用（也可以实现用户定义的消息块）：

- unbounded_buffer: 无界大小的并发队列。
- overwrite_buffer: 可多次更新的单个值。
- single_assignment: 只能设置一次的单个值。进一步的更新将被忽略。
- call: 每当向消息块添加值时就会被调用的函数。它是一个回调。
- transformer: 每当向消息块添加值时就会被调用的函数；函数的返回值会被添加到输出消息块。

