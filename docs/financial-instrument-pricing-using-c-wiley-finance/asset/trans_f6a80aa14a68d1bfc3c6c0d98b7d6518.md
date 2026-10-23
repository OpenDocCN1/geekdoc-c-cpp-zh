

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_943_0.png)

FIGURE 29.1 My first data dependency graph

其产生的输出以及总运行时间。我们将这些结果与基于任务的解决方案产生的结果进行比较。首先，简单的函数 F1、F2、F3 和 F4 定义为：

```
double F1(double a)
{
    std::cout << "F1\n";
    return a;
}
```

```
double F2(double x)
{
    std::cout << "F2\n";
    return x - 12.0;
}
```

```
double F3(double x)
{
    std::cout << "F3\n";
    return x + 10.0;
}
```

```
double F4(double x, double y)
```

```
{
    std::cout << "F4\n";
    return x + y;
}
```

实现图 29.1 中有向图的 C++ 顺序代码为：

```
double SequentialTaskGraph(double a)
{ // Single thread of control
    std::cout << "Sequential \n";
    double b = F1(a);
    double c = F2(a);
    double d = F3(c);
    double f = b + d;
    return f;
}
```

一个简单的测试用例为：

```
int main()
{
    double a = 22.0;
    std::cout << SequentialTaskGraph(a) << std::endl;
    return 0;
}
```

最终输出值为 42。此代码可以运行，但它没有利用图中潜在的并行性，因为 F1 和 F2 可以并行运行，F1 和 F3 也可以。我们还注意到此代码中没有副作用，因为所有函数都是纯的。我们将在第 29.4 节中了解如何使用 C++ 并发来并行化此代码。

## 29.3.2 Data Dependency Graph: Generalisations

在开始编程之前，我们给出一些数据依赖图的其他示例，以帮助我们深入了解发现并行性的方法。大多数图属于以下两类之一：

- Data flow graph: data is passed along the graph’s edges. Vertices receive data messages, transform them and then pass them on to other vertices.
- Data dependence graph: vertices operate directly on shared data and data is not passed along edges.

图 29.2 的示例是数据并行的示例，其中操作 B 使用来自操作 A 的三个不同输入执行。在这里我们看到相同的操作 B 对相同数据的不同子集执行。Bs 的输出在操作 C 中合并。图 29.3 是任务并行的示例，其中操作 B、C 和 D 可以并发执行。最后，图 29.4 是一个顺序依赖图。

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_945_0.png)

## FIGURE 29.2 Data parallelism

我们将在第 30 章讨论如何使用 Microsoft 的 Parallel Patterns Library (PPL) 实现数据依赖图。我们注意到 Intel 的 Threading Building Blocks (TBB) 对这些数据结构提供支持，尽管讨论 TBB 超出了本书的范围。在第 30 章中我们还将讨论基于任务的消息传递和数据流模型。

## 29.3.3 Steps to Parallelisation

很明显，我们需要一个流程来分析和设计在多处理器硬件上执行的程序，并实现它们。代码必须给出准确的结果，并且必须针对性能进行优化。为此，主要步骤的总结如下：

- 1. *Decomposition:* break the program into tasks.
- 2. *Assignment:* assign tasks to processes.

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_945_1.png)

## FIGURE 29.3 Functional parallelism

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_946_0.png)

**FIGURE 29.4** Sequential computation

- 3. *Orchestration*: data access, communication and synchronisation of processes.
- 4. *Mapping*: bind processes to processors.

这是一个迭代的过程，有时结合试错实验，我们可以花费大量时间使程序正确、无竞态条件并提高其加速比。

## 29.4 FUTURES AND PROMISES

这些术语起源于 20 世纪 70 年代末。Futures 和 promises 是用于在编程语言中同步程序执行的构造。它们描述了一个对象，该对象充当最初未知的结果的代理（术语 *delayed* 和 *deferred* 也被使用）。结果未知是因为计算该值尚未完成。

更精确地说，*future* 表示变量的只读占位符视图，而 *promise* 是可写的、单次赋值的实体，它设置 future 的值。简而言之，future 是值，而 promise 是设置值的（异步）函数。我们可以在不指定哪个特定 promise 将设置其值的情况下定义 future。不同的可能 promise 可能会设置 future 的值；然而，*值只能设置一次*。可以将 future 和 promise 关联起来，正如我们将看到的那样。

有很多功能需要介绍。为此，类模板
`std::future` 具有以下功能：

- 1. Create a future to hold the result of an asynchronous operation that is created using `std::async`, `std::packaged_task` or `std::promise`.
- 2. We can use several methods to query, wait for or extract a value from the `std::future`.
- 3. The asynchronous operation can modify *shared state* (which is linked to the created `std::future`) when it is ready to send the result to the creator.

类模板 `std::promise` 提供了一种设施，用于存储稍后通过 `std::future` 实例异步获取的结果/值或异常。它具有以下功能：

- 1. *Make ready*: store the result or exception in the shared state. The state is marked as ready.
- 2. *Release*: the promise gives up its reference to the shared state.
- 3. *Abandon*: the promise stores the exception of type `std::future_errc::broken_promise`, makes the shared state *ready* and then *releases* it.

类模板 `std::async` 异步运行一个函数（可能在单独的线程中），并返回一个 `std::future` 实例，该实例最终将保存函数调用的结果。类模板 `std::packaged_task` 包装一个 *callable object*（自由函数、lambda 表达式、bind 表达式或函数对象），以便它可以异步调用。其返回值或异常存储在共享状态中，可以通过 `std::future` 实例访问。

### 29.4.1 Examples of Futures and Promises in C++

我们现在给出一些如何定义异步函数的示例。一旦我们了解了在这些简单情况下如何使用功能，我们就可以将结果推广到更大的问题（依赖图）以及涉及可写共享数据的更复杂算法和应用程序。特别是，在此阶段很有趣的是思考如何将并行编程代码用于我们在第 9 章中介绍的设计。

方法是创建一个模拟真实算法的简单函数。在此情况下我们引入一个 *sleep operation*，它模拟 *load balancing* 效果和延迟：

```
double compute(double x)
{
    // Wait a while; simulates delays and load balancing effects
    std::default_random_engine dre(42);
    std::uniform_int_distribution<int> delay(0, 4000);
    std::this_thread::sleep_for (std::chrono::milliseconds(delay(dre)));

    return x*x;
}
```

我们还提供了一个使用 promise 作为输入参数的变体：

```
void computePromise(double x, std::promise<double> &p)
{
    // Wait a while
    std::default_random_engine dre(42);
    std::uniform_int_distribution<int> delay(0, 10);
    std::this_thread::sleep_for (std::chrono::milliseconds(delay(dre)));

    p.set_value(x*x);
}
```

在此后一种情况下请注意 promise 存储一个值，该值将在稍后阶段由 future 获取。

我们现在准备讨论运行算法的不同方式。第一个选项异步运行：

```
double x = std::sqrt(42.0);

// A. 'Direct' tasks
std::future<double> fut = std::async(compute, x);

// Get the shared data
double result = fut.get();
std::cout << "Result async : " << result << '\n';
```

第二个选项更复杂，因为我们正在创建一个 promise 并将其与 future 关联。我们显式创建一个运行算法的线程，并且 promise 存储计算结果。future 在算法完成之前等待获取值。调用方还等待线程完成（注意使用移动语义）：

```
// B. Using a promise
std::promise<double> pr;
std::future<double> futP = pr.get_future();

std::thread t(computePromise, x, std::move(pr));
futP.wait();
std::cout << "Result promise : " << futP.get() << '\n';
t.join();
```

第三个选项是使用在调用方同一线程中运行的 packaged task：

```
// C. (Delayed) packaged task
std::packaged_task<double(double)> task(compute);
std::future<double> fut2 = task.get_future();

task(x);
// Get the shared data
std::cout << "Starting packaged task: " << fut2.get() << '\n';
```

第四个也是最后一个选项是我们在自己的线程中运行任务时：

```
// D. Packaged task in a separate thread
{
    std::packaged_task<double(double)> task(compute);
    std::future<double> fut2 = task.get_future();

    std::thread t(std::move(task), x);
    t.join();

    // Get the shared data
    std::cout << "Starting packaged task from a separate thread: "
              << fut2.get() << '\n';
}
```

