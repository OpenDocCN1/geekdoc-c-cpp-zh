

### 20.3.1 使用多线程生成随机数

朴素的随机数生成器使用一个全局变量来存储随机数生成器的当前状态。要在多线程程序中使用它，我们需要添加一个互斥锁来保护这个全局变量。这可能会效率低下，因为多个线程会不断锁定和解锁同一个互斥锁。这意味着每个处理器的缓存会频繁地被写入主内存。

一种更好的方法是为每个线程使用独立的随机数生成器。只要我们为随机数生成器获取到合适的种子，应该就能够确保为每个线程生成的数字是独立的。

为了实现这种方法，我们希望在任何调用生成随机数的函数时，传递要使用的随机数生成器。你可能记得，我们用来生成随机数的类名是类 `mt19937`。

因此，`matlib` 中的诸如 `randn` 和 `randuniform` 等函数已经更新，允许你传入想要使用的随机数生成器：

```c
/* Create uniformly distributed random numbers */
Matrix randuniform( int rows, int cols );
/* Create normally distributed random numbers */
Matrix randn( int rows, int cols );
/* Create uniformly distributed random numbers */
Matrix randuniform(std::mt19937& random,
        int rows, int cols);
/* Create normally distributed random numbers */
Matrix randn(std::mt19937& random,
        int rows, int cols);
```

类似地，我们需要更新各种 `generatePricePaths` 函数，使它们接收一个 `mt19937` 实例。以下是 `MultiStockModel` 中此类方法之一的声明所做的更改。

```c
MarketSimulation generatePricePaths(
        std::mt19937& rng,
        double toDate,
        int nPaths,
        int nSteps) const;
```

此外，`MultiStockModel` 有一个函数，告诉我们生成给定的股票价格需要多少个随机数。

```c
/* How many random numbers are needed to generate the given paths? */
long long randSize(long long nPaths, long long nSteps) {
    return stockNames.size() * nPaths * nSteps;
}
```

这很有用，因为 `mt19937` 有一个 **discard** 函数，它可以用来快速更新随机数生成器的状态，就好像我们生成了给定数量的随机数，而不必承担生成那么多随机数的开销。利用这一点，我们可以启动 *n* 个线程，这些线程拥有能够生成计算所需数量的独立随机数的随机数生成器。注意，我们使用 *long long* 作为返回类型，仅仅是因为乘积理论上可能太大，无法保存在普通的 *int* 中。

## 20.3.2 多线程定价器

我们希望修改我们的 `MonteCarloPricer`，使 *price* 方法使用多个线程。作为第一步，我们应该重命名现有的 *price* 方法。让我们将其重命名为 *singleThreadedPrice*。

```c
double singleThreadedPrice(
    int taskNumber,
    int nScenarios,
    int nSteps,
    const ContinuousTimeOption& option,
    const MultiStockModel& model ) {
```

我们仍然希望调用这个方法，只是新的 *price* 函数将在单独的线程上多次调用 *singleThreadedPrice*。然后它将计算所有线程的平均结果。

注意，我们同时做了另一个小改动。函数 *singleThreadedPrice* 接受一个参数 **taskNumber**。这些一起用于初始化随机数生成器。以下是 *singleThreadedPrice* 实现内部的相关代码段：

```c
MultiStockModel subModel = model.getSubmodel(
      option.getStocks());

long long randSize = subModel.randSize(nScenarios,
                                        nSteps);

mt19937 rng;
rng.discard(randSize * taskNumber);
```

使用 **discard** 保证了如果我们创建 *n* 个任务并赋予它们从 0 到 *n* 的连续任务编号，那么用于蒙特卡洛计算的随机数集将与创建单个任务时使用的完全相同。特别是，使用的所有随机数都是独立的。

## 20.3.3 实现 Task

如果我们希望使用我们的 **Executor** 类，就需要编写一个 `Task` 的实现来执行蒙特卡洛定价。我们将创建多个相同的任务，将它们交给执行器，然后计算平均结果。我们的任务实例需要的主要工作是调用 `singleThreadedPrice`。

```c
class PriceTask : public Task {
public:
    /* Amount of random numbers to skip */
    int taskNumber;
    int nScenarios, nSteps;
    const ContinuousTimeOption& option;
    const MultiStockModel& model;
    /* Output data */
    double result;

    PriceTask(
              int taskNumber,
              int nScenarios,
              int nSteps,
              const ContinuousTimeOption& option,
              const MultiStockModel& model)
    :
        taskNumber(taskNumber),
        nScenarios(nScenarios),
        nSteps(nSteps),
        option(option),
        model(model) {}

    void execute() {
        result = singleThreadedPrice( taskNumber,
            nScenarios, nSteps, option, model);
    }
};
```

关于我们设计的一个值得注意的地方是，除了 `const` 引用外，我们的任务不与其他任务共享数据。因此，我们遵循了之前给出的设计建议，以最小化线程之间的通信量。

编写这个 `Task` 类相当繁琐。使用 lambda 函数会更好。如何实现这一点留作练习。

## 20.3.4 使用 Executor

现在我们需要创建并运行一定数量的任务。为了确定创建的最合适任务数量，我们简单地给 `MonteCarloPricer` 类添加一个新的配置参数 `nTasks`。

我们现在可以编写一个多线程 price 函数，该函数：
- 创建所需数量的任务；
- 运行它们以获得蒙特卡洛价格的估计值；并且
- 组合结果以获得更好的价格估计。

```c
double MonteCarloPricer::price(
    const ContinuousTimeOption& option,
    const MultiStockModel& model) const {
    ASSERT(nTasks >= 1);
    vector< shared_ptr<PriceTask> > tasks;
    shared_ptr<Executor> executor =
        Executor::newInstance(nTasks);
    for (int i = 0; i<nTasks; i++) {
        shared_ptr<PriceTask> task(new PriceTask(
            i, nScenarios/nTasks,
            nSteps, option, model));
        tasks.push_back(task);
        executor->addTask(task);
    }
    executor->join();
    double total = 0.0;
    for (int i = 0; i<nTasks; i++) {
        total += tasks[i]->result;
    }
    return total / nTasks;
}
```

最后，我们更新测试，以确认使用多线程定价期权的结果与使用单线程获得的结果相同。由于计算顺序略有不同，可能会存在非常微小的差异，因此不能期望得到完全相同的 double 值。然而，计算中使用了完全相同的随机数，因此这应该是唯一的差异来源。

## 20.3.5 关于设计的备注

首先，请注意 `Executor` 类是用静态工厂方法设计模式编写的。我们不需要知道它是如何实现的就可以使用它。事实上，如果你查看 `Executor.cpp` 中的代码，你会发现它非常精密。另一方面，每个 `Task` 都很容易编写。

其次，请注意与 `Task` 实例的唯一交互发生在它们运行之前和之后：
- 我们在构造函数中设置参数
- 我们在对 `Executor` 调用 `join` 之后访问结果

这种直接的方法比使用共享内存和互斥锁在线程之间发送数据要简单得多。注意执行金融计算的算法和处理线程的代码之间的完全分离。这是一个使用好的设计模式如何简化代码的例子。

# 20.4 协调线程

## 20.4.1 Pipeline 模式

命令设计模式允许我们非常轻松地编写多线程定价器。该模式之所以特别有效，是因为线程之间没有任何通信。

然而，有时你确实希望线程以更复杂的方式相互交互。在本节中，我们将描述一种设计模式，它允许两个线程以稍微复杂的方式协同工作。

考虑下面一个名为 `Pipeline` 的类：

```c
class Pipeline {
public:
    Pipeline();
    void write( double value );
    double read();
private:
    bool empty;
    double value;
    /* Mutex to coordinate threads */
    std::mutex mtx;
    /* Condition variable to signal between threads */
    std::condition_variable cv;
};
```

你可以使用 `Pipeline` 类将两个线程连接起来。

两个线程共享单个 `Pipeline` 对象。一个线程，即写线程，调用 `Pipeline` 上的 `write` 来存储一个值，然后等待直到另一个线程调用了 `read`。同时，读线程调用 `read`。读方法会等待直到数据可供 `read` 使用。

其理念是写线程应该执行计算的一部分，然后将结果存储在 `Pipeline` 中。读线程然后可以读取部分计算的结果并完成其余处理。

