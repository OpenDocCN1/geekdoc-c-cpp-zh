
### 20.3.1 使用多线程生成随机数

一种朴素的随机数生成器使用全局变量来存储随机数生成器的当前状态。要在多线程程序中使用它，我们需要添加互斥锁来保护这个全局变量。由于多个线程会不断地对同一把互斥锁进行加锁和解锁，这在潜在上是低效的。这意味着每个处理器的缓存会频繁地将数据写入主内存。

更好的方法是为每个线程使用单独的随机数生成器。只要我们为随机数生成器获取适当的种子，就应该能够确保为每个线程生成的数字是独立的。

为了实现这种方法，我们希望每当调用生成随机场景的函数时，都传递我们要使用的随机数生成器。你可能记得，我们用来生成随机数的类名是 **mt19937**。

因此，**matlib** 中诸如 **randn** 和 **randuniform** 等函数已被更新，允许你传入你想要使用的随机数生成器：

```cpp
/* Create uniformly distributed random numbers */
Matrix randuniform ( int rows, int cols );
/* Create normally distributed random numbers */
Matrix randn( int rows, int cols );
/* Create uniformly distributed random numbers */
Matrix randuniform(std::mt19937& random,
                   int rows, int cols);
/* Create normally distributed random numbers */
Matrix randn(std::mt19937& random,
             int rows, int cols);
```

同样，我们需要更新各种 **generatePricePaths** 函数，使它们接收一个 **mt19937** 实例。以下是 **MultiStockModel** 中这样一个方法的声明所做的更改。

```cpp
MarketSimulation generatePricePaths(
    std::mt19937& rng,
    double toDate,
    int nPaths,
    int nSteps) const;
```

此外，**MultiStockModel** 有一个函数可以告诉我们需要生成多少个随机数来生成给定的股票价格。

```cpp
/* How many random numbers are needed
   to generate the given paths? */
long long randSize(long long nPaths,
                   long long nSteps) {
    return stockNames.size()*nPaths*nSteps;
}
```

这很有用，因为 mt19937 有一个 discard（丢弃）函数，它可以快速更新随机数生成器的状态，就好像我们生成了给定数量的随机数，但不需要实际生成那么多随机数的开销。利用这一点，我们可以启动 $n$ 个线程，这些线程拥有的随机数生成器能够生成我们在计算中所需的任意数量的独立随机数。请注意，我们使用 long long 作为返回类型，仅仅是因为乘积可能会大到无法存储在普通的 int 中。

### 20.3.2 多线程定价器

我们想要修改我们的 MonteCarloPricer，使其价格方法使用多个线程。作为第一步，我们应该重命名现有的 price 方法。让我们将其重命名为 singleThreadedPrice

```cpp
double singleThreadedPrice(
 int taskNumber,
 int nScenarios,
 int nSteps,
 const ContinuousTimeOption& option,
 const MultiStockModel& model ) {
```

我们仍然希望调用这个方法，只是我们的新 price 函数将在单独的线程上多次调用 singleThreadedPrice。然后它将计算所有线程的平均结果。

请注意，我们同时做了另一个小改动。函数 singleThreadedPrice 接受一个参数 taskNumber。这两个值一起用于初始化随机数生成器。以下是 singleThreadedPrice 实现内部的相关代码片段：

```cpp
MultiStockModel subModel = model.getSubmodel(
 option.getStocks());
 long long randSize = subModel.randSize(nScenarios,
 nSteps);
 mt19937 rng;
 rng.discard(randSize*taskNumber);
```

这种 discard 的用法保证，如果我们创建 n 个任务并赋予它们从 0 到 n-1 的连续任务编号，那么用于蒙特卡洛计算的随机数集合将与创建一个单独任务时使用的完全相同。特别地，使用的所有随机数将是独立的。

### 20.3.3 实现 Task

如果我们希望使用我们的 Executor 类，我们需要编写一个 Task 的实现来执行蒙特卡洛定价。我们将创建多个相同的任务，将它们交给执行器，然后计算平均结果。我们的任务实例需要的主要工作是调用 singleThreadedPrice。

```cpp
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
            model(model) {
        }

        void execute() {
            result = singleThreadedPrice(taskNumber,
                nScenarios, nSteps, option, model);
        }
};
```

关于我们设计的一个值得注意的地方是，我们的任务除了 const 引用之外，不与其他任务共享数据。因此，我们遵循了前面给出的设计建议，以最小化线程之间的通信量。

编写这个 Task 类相当繁琐。使用 lambda 函数代替将会更好。这样做留作练习。

### 20.3.4 使用 Executor

我们现在需要创建一批任务并运行它们。为了确定创建任务的最合适数量，我们只需向 `MonteCarloPricer` 类添加一个新的配置参数 `nTasks`。

我们现在可以编写一个多线程的 `price` 函数，它：创建所需数量的任务；运行它们以获得蒙特卡洛价格的估计值；并组合结果以获得更优的价格估计。

```cpp
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

最后，我们更新测试以确认使用多个线程对期权进行定价的结果与使用单个线程获得的结果相同。由于计算顺序略有不同，可能会有极微小的差异，因此人们不期望得到完全相同的 double 值。尽管如此，计算中使用的随机数是完全相同的，所以这应该是唯一的差异来源。

### 20.3.5 关于设计的备注

首先，请注意 `Executor` 类是使用静态工厂方法设计模式编写的。我们不需要知道它是如何实现就可以使用它。事实上，如果你查看 `Executor.cpp` 中的代码，你会发现它非常复杂。另一方面，每个 `Task` 都很容易编写。

其次，请注意与 `Task` 实例的交互只发生在它们运行之前和之后：

- 我们在构造函数中设置参数
- 我们在对 *Executor* 调用 *join* 之后访问结果

这种直接的方法比使用共享内存和互斥锁在线程之间发送数据要简单得多。请注意，执行金融计算的算法与处理线程的代码之间是完全分离的。这是一个使用良好设计模式可以简化代码的示例。

## 20.4 线程协调

### 20.4.1 管道模式

命令设计模式使我们可以非常容易地编写一个多线程定价器。该模式特别有效，因为线程之间没有任何通信。

然而，有时你希望线程以更复杂的方式相互交互。在本节中，我们将描述一种设计模式，它以稍复杂的方式将两个线程连接在一起。

考虑以下称为 *Pipeline* 的类：

```cpp
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

你可以使用 *Pipeline* 类将两个线程连接在一起。

两个线程共享一个 *Pipeline* 对象。一个线程，即写线程，在 *Pipeline* 上调用 *write* 来存储一个值，然后等待另一个线程调用 *read*。与此同时，*read* 线程调用 *read*。*read* 方法将等待，直到有数据可供 *read*。

其思想是，写线程应该执行计算的一部分，然后将结果存储在 *Pipeline* 中。*read* 线程随后可以读取部分计算的结果并完成其余处理。如果

