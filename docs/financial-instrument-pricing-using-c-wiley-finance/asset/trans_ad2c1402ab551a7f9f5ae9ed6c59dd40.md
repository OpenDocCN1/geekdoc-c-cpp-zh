

## 32.2.4 C++ Futures

我们回顾一下，C++ std::future 是一种访问异步操作结果的机制。它具有可用于后续代码的返回类型（与线程不同）。future 的创建者可以使用多种方法来查询、等待或从 std::future 中提取值。在我们的例子中返回类型为 void，代码会阻塞（通过调用 wait()）直到结果可用，然后我们得到：

```
std::future<void> fut1(std::async(fn1));
std::future<void> fut2(std::async(fn2));
std::future<void> fut3(std::async(fn3));
std::future<void> fut4(std::async(fn4));
```

```
// Wait for results to become available
fut1.wait();
fut2.wait();
fut3.wait();
fut4.wait();
```

```
fut1.get();
fut2.get();
fut3.get();
fut4.get();
```

## 32.2.5 PPL Parallel Tasks

PPL 支持任务，这些任务隐藏了使用线程时遇到的低级细节。与线程不同，新任务不一定会立即开始执行。相反，它们在关联的任务调度程序将其从工作队列中移除时运行。程序的性能随核心数量而扩展。

PPL 并行任务的一个简单例子是 parallel_invoke 函数：

// Start the work functions
concurrency::parallel_invoke
(
    fn1,
    fn2,
    fn3,
    fn4
);
```

parallel_invoke 函数有重载版本，可接受多达九个参数，每个参数对应一个要与其他函数并行运行的函数。待运行的函数可以正常完成，也可以抛出异常而结束。

我们可以通过创建任务组对象并调用其 run 和 wait 方法来重现 parallel_invoke 的功能，例如：

// Parallel task using task group
concurrency::task_group tg;
```

```
tg.run(fn1);
tg.run(fn2);
tg.run(fn3);
tg.run(fn4);

tg.wait();
```

一种可以更好地利用线程的变化是将 run 和 wait 步骤合并为一个操作：

```
tg.run(fn1);
tg.run(fn2);
tg.run(fn3);
tg.wait();
tg.run_and_wait(fn4);
```

## 32.2.6 OpenMP Parallel Loops

OpenMP 支持循环并行模式（Chapman, Jost and Van der Pas, 2008; Mattson, Sanders and Massingill, 2005）。我们创建一个计算密集型函数数组并并行运行它们：

```
std::vector <std::function<void()>>
    tGroupFunctions = { fn1, fn2, fn3, fn4 };

#pragma omp parallel for
for (int i = 0; i < tGroupFunctions.size(); ++i)
{
    tGroupFunctions[i]();
}
```

我们必须确保并行程序在使用一个线程或使用多个线程执行时产生相同的结果。这称为顺序等价。由于舍入误差等原因，此要求可能并不总是可行。

OpenMP 中的循环并行非常容易编程，并且具有良好的性能特性。

## 32.2.7 Boost Thread Group

C++ Concurrency 没有将线程组建模为一个实体的功能。然而，我们将其模拟为线程数组，如第 32.2.3 节中已看到。我们回顾：

```
std::vector<std::shared_ptr<std::thread>> threadGroup;
std::vector <std::function<void()>>
    tGroupFunctions = { fn1, fn2, fn3, fn4 };
for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
```

```
```cpp
{
    threadGroup.emplace_back(std::shared_ptr<std::thread>
        (new std::thread(tGroupFunctions[i])));
}

for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
{
    if (threadGroup[i]->joinable())
    {
        threadGroup[i]->join();
    }
}
```
```

*Boost.Thread* 包含类 `thread_group`，它支持将一组线程作为一个实体创建和管理。组中的线程以某种方式相关。功能如下：

- 创建一个没有线程的新线程组。
- 删除组中的所有线程。
- 创建一个新线程并将其添加到组中。
- 在不删除线程的情况下从组中移除线程。
- `join_all()`: 对组中的每个线程调用 `join()`。
- `size()`: 给出组中线程的数量。

使用第 32.2.3 节中的变量，对应的代码为：

```
```cpp
boost::thread_group threads;
for (std::size_t i = 0; i < tGroupFunctions.size(); ++i)
{
    threads.create_thread(tGroupFunctions[i]);
}
std::cout << "Thread group size: " << threads.size() << '\n';

threads.join_all();
```
```

如果您不想为此问题使用 Boost 库，可以创建自己的类来模拟 Boost 线程组。

## 32.3 一族预测-校正格式

我们现在讨论一种用于单因子和多因子 SDE 的格式。它被称为 *predictor–corrector* 方法，是用于求解常微分方程的类似格式的推广（Lambert, 1991）。为了将其应用于 SDE，我们检查方程 (31.7) 给出的非线性问题。如果我们使用梯形法则离散化此 SDE，我们将在每个时间层得到一个非线性方程组，我们需要使用牛顿法或 Steffensen 方法等求解，例如：

X_{n+1} = X_n + { σ μ(X_{n+1}) + (1 − α) μ(X_n) } Δt + { β σ(X_{n+1}) + (1 − β) σ(X_n) } ΔW_n,    n ≥ 0
其中：
0 ≤ α ≤ 1,    0 ≤ β ≤ 1.    (32.4)

与其求解此方程，我们尝试通过用另一个已知量（称为预测值）替换“有问题的”时间层 n + 1 的未知解来将其线性化，该量 hopefully 接近它。为此，我们计算显式欧拉预测值：

X̃_{n+1} = X_n + μ(X_n) Δt + σ(X_n) ΔW_n,    n ≥ 0    (32.5)

随后我们将其用于校正方程：

X_{n+1} = X_n + { α μ(X_{n+1}) + (1 − α) μ(X_n) } Δt + { β σ(X̃_{n+1}) + (1 − β) σ(X_n) } ΔW_n,    n ≥ 0.    (32.6)

然而，我们通过使用校正的漂移函数修改方程 (31.7)：

μ̄_ρ(x) = μ(x) − β σ(x) ∂σ/∂x (x).    (32.7)

新的校正方程为：

X_{n+1} = X_n + { α μ̄_ρ(X̃_{n+1}) + (1 − α) μ̄_ρ(X_n) } Δt + { β σ(X̃_{n+1}) + (1 − β) σ(X_n) } ΔW_n, n ≥ 0.    (32.8)

该格式的解可以在无需使用非线性求解器的情况下找到。此外，您可以自定义该格式以支持漂移和扩散项应用于方程 (32.4) 和 (32.8) 的不同隐式和显式程度：

- A. 完全显式（α = β = 0）
- B. 完全隐式（α = β = 1）
- C. 漂移隐式扩散显式（α = 1, β = 0）
- D. 对称（α = β = 1/2）。    (32.9)

我们需要确定哪种参数组合会产生稳定的格式。我们已经看到，减少时间步长（这与增加区间 [0, T] 的细分数量相同）并不总是会提高精度，甚至可能导致严重的失真。这种现象在离散化确定性方程时并不常见，其中收敛通常是关于步长的单调的。

为了在 C++ 中建模这些格式，我们需要扩展 SDE 功能以包含扩散项的导数和由方程 (32.7) 定义的校正漂移函数（另见 Kloeden, Platen and Schurz, 1997, p. 198）。为此，我们提出一个类，它本质上是第 31 章中相应类的扩展：

// Functions of arity 2 (two input arguments)
template <typename T>
    using FunctionType = std::function<T (const T& arg1, const T& arg2)>;

// Interface to simulate any SDE with Drift/Diffusion
// Use a tuple to aggregate two functions into what is similar to an
// interface in C# or Java.
template <typename T>
    using ISde = std::tuple<FunctionType<T>, FunctionType<T>>;

template <typename T = double> class Sde
{
private:
    FunctionType<T> dr_;
    FunctionType<T> diff_;

    FunctionType<T> drCorr_;
    FunctionType<T> diffDeriv_;

    T ic;  // Initial condition
    T exp_; // Expiry

public:
    Sde() = default;
    Sde(const Sde<T> & sde2, const T& initialCondition, const T& expiry)
        : dr_(sde2.dr_), diff_(sde2.diff_), ic(initialCondition),
          drCorr_(sde2.drCorr_),diffDeriv_(sde2.diffDeriv_),exp_(expiry) {}
    Sde(const ISde<T> & functions, const FunctionType<T>&
        driftCorrected,
        const FunctionType<T>& diffusionDerivative,
        const T& initialCondition,const T& expiry)
        : dr_(std::get<0>(functions)),diff_(std::get<1>(functions)),
          drCorr_(driftCorrected), diffDeriv_(diffusionDerivative),
          ic(initialCondition), exp_(expiry) {}

    T Drift(const T& t, const T& S)
    {
        return dr_(t,S);
    }

    T Diffusion(const T& t, const T& S)
    {
        return diff_(t,S);
    }

    double DriftCorrected(double t, double x, double B)
    {
        return Drift(t,x)
            - B * Diffusion(t,x) * DiffusionDerivative(t,x);
    }
```
