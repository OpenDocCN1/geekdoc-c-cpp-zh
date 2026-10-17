
`const size_t nParam = mdl.numParams();`

```cpp
// Allocate结果
AADSSimul results(nPath, nPay, nParam);
// 清空并初始化带
Number::tape->clear();
```

... 以及 `main.h` 中的入门级函数已经设置好以调用它。

接下来，我们为每个线程分配工作内存（暂不初始化任何内容）（包括主线程，即工作线程数 + 1）：

```cpp
// ...
// 我们每个线程都需要一个这样的对象
// 0: 主线程：线程
// 1 到 n: 工作线程
```

```cpp
ThreadPool *pool = ThreadPool::getInstance();
const size_t nThread = pool->numThreads();
```

```cpp
// 分配工作空间，暂不初始化任何内容
// 每个线程一个模型克隆
// 模型在使用 AAD 时是变的
vector<unique_ptr<Model<Number>>> models(nThread + 1);
for (auto& model : models) {
```

```cpp
model = mdl.clone();
model->allocate(prd.timeline(), prd.defline());
}
```

```cpp
// 每个线程一个场景
vector<vector<Number>> paths(nThread + 1);
for (auto& path : paths) {
```

```cpp
allocatePath(prd.defline());
}
```

```cpp
// 每个线程一个收益向量
vector<vector<Number>> payoffs(nThread + 1, vector<Number>(nPay));
// -工作空间
```

```cpp
// 工作线程的带
// 主线程拥有它自己的一个
vector<Tape> tapes(nThread);
```

```cpp
// 模型是否在此线程上初始化？
vector<int> mdlInit(nThread, 1, false);
...
```

我们还为了第 35 行为每个工作线程初始化了一个带的向量。主线程已经拥有一个带：在 `Number` 类型实例上声明的静态带在应用程序启动时会为主线程实例化一个副本，就像任何静态对象一样。

最后，我们在第 38 行有一个布尔值向量，对应每个线程，用于跟踪哪些线程完成了初始化阶段，从所有人都设为 `false` 开始。⁶

我们还必须初始化 RNG 和高斯向量，但为了实现这一点，我们需要仿真维度 `D`，而只有初始化的模型才能提供此信息。因此，下一步是初始化主线程的模型（主线程索引为 0，工作线程索引为 1 到 `nThread`）：

```cpp
...
// 初始化主线程
initModel4ParallelAAD(prd, *models[0], paths[0]);
// 标记主线程为已初始化
dlInit[0] = true;
// 初始化 RNG，每个线程一个
// 每个线程一个
vector<unique_ptr<RNG>> rngs(nThread + 1);
for (auto &random : rngs) {
  random = rng.clone();
  random->init(models[0]->simDim());
}
// 每个线程一个高斯向量
vector<vector<double>> gaussVecs
(nThread + 1, vector<double>(models[0]->simDim()));
...
```

接下来，我们将仿真循环分发到线程池进行并行处理，采用与第 7 章相同的技术：

```cpp
...
// 为 future 预留内存
vector<TaskHandle> futures;
futures.reserve(nPath / BATCHSIZE + 1);
```

> ⁶我们使用了 `vector<int>` 代替了 `vector<bool>`。由于历史原因，在标准 C++ 中，`vector<bool>` 不是线程安全的，应避免并发写入不同的条目。

```cpp
// 开始
size_t firstPath = 0;
size_t pathsLeft = nPath;
while (pathsLeft > 0)
{
    size_t pathsInTask = min<size_t>(pathsLeft, BATCHSIZE);
    futures.push_back(pool->spawnTask([&, firstPath, pathsInTask]() {
```

`lambda` 的体在不同的线程上执行。这里，带是执行线程的带，`pool->threadNum()` 返回执行线程的索引。我们第一的第一是记录这个索引并相应设置线程本地带：

```cpp
// ...
const size_t threadNum = pool->threadNum();
// 使用此线程的带
// 线程本地：每个线程都有自己的指针
// 注意主线程 -0 不需要重置
if (threadNum > 0) Number::tape = &tapes[threadNum - 1];
// ...
```

这是并行 AAD 的代码。带通过线程本地指针 `Number::tape` 访问。将其从执行线程设置到我们在 `tapes` 向量中分配的带。主线程 `0` 已经正确引用了它的全局带。不需要重置。

只有在这一阶段，我们才能在带上放置参数并初始化模型（除了之前的分配），从主线程传播所有线程的带：

```cpp
// ...
// 计算之间和路径级操作
// 上述操作已经传播并累积
// 我们执行一次传播
// 在主线程带上
Number::propagateToStart();
// 以及工作线程带上
Tape* mainThreadPtr = Number::tape;
for (size_t i = 0; i < nThread; ++i) {
    if (mdlInit[i + 1]) {
        // 设置带指针
        Number::tape = &tapes[i];
        // 在该带上传播
        Number::propagateToStart();
    }
}
// 重置带为主线程的带
Number::tape = mainThreadPtr;
// ...
```

我们首先在第 7 行的主线程的带上进行传播。然后，我们顺序传播主线程的其余 `n` 个带。为了从主线程传播数字 `i`，我们临时将主线程的带设置为带 `i`（第 15 行），并进行传播（第 17 行）。最后，我们在第 21 行将主线程的带重置为其静态带。

```cpp
// ...
// 获取 RNG 并使其向前跳
auto& random = rngs[threadNum];
random->skipTo(firstPath);
// ...
```

最后，并发代码其余执行第 7 章的内部循环，内容与串行微分相同：重置带（标记）、生成数字、仿真、计算收益、聚合它们、传播伴（标记）、存储结果，重复：

```cpp
// ...
// 进行仿真，完全与顺序一样
for (size_t i=0; i < pathsInTask; i++) {
  // 回溯带以标记
  // 注意这是执行线程的带
  Number::tape->rewindToMark();
  // 下一个高斯向量，维度 D
  random->nextG(gaussVecs[threadNum]);
  // 路径
  models[threadNum]->generatePath(
    gaussVecs[threadNum],
    paths[threadNum]);
  // 收益
  prd.payoffs(paths[threadNum], payoffs[threadNum]);
  // 传播伴随
  Number result = aggFun(payoffs[threadNum]);
  result.propagateToMark();
  // 存储路径结果
  results[firstPath + i].assign(
    payoffs[threadNum].begin(),
    payoffs[threadNum].end()
  );
  // 记得任务必须返回 bool
  return true;
}
pathsLeft -= pathsInTask;
firstPath += pathsInTask;
}
// 等待
for (auto& futures : pool) activeWait();
// ...
```

就像串行微分，所有的伴随在此阶段累积在带的持久部分上，我们必须将初始化器传回参数；参见第 416 页的图。区别在于伴随现在分布在多个线程的带上，但我们已经离开了并发代码并回到主线程。没关系；这是执行一次的传播；我们从主线程传播所有线程的带：

```cpp
// ...
// 在线程上累加敏感度
for (size_t j = 0; j < nParam; ++j)
{
    results.risks[j] = 0.0;
    for (size_t i = 0; i < models.size(); ++i)
    {
        if (mdlInit[i]) results.risks[j] +=
            models[i]->parameters()[j] - models[i]->adjoint();
    }
    results.risks[j] /= nPath;
}
```

我们几乎安全到达家了。所有的伴随都正确地累积了，但跨越了多个带和多个模型。每个线程的带包含了该线程处理的路径的伴随之和。伴随对每个模型访问。我们跨越模型汇总伴随，归一化、打包并返回：

```cpp
// ...
// 为 future 预留内存
vector<TaskHandle> futures;
futures.reserve(nPath / BATCHSIZE + 1);
```

> 这段代码是异常安全的。如果发生异常，主线程的带将不会被重置。

> 这种代码是异常安全的。

```cpp
return的。
```

代码位于 `mcBase.h`。

## 12.6 PARALLEL RESULTS

We reproduce the example on page 424, this time in parallel: a 3y 120 with a 150 barrier, in Dupire's model 1,800 local volatilities (of which 1,080 active) of 15% over 60 times and 30 spots, simulating 500,000 paths over 156 weekly steps with Sobol.

理想情况下，我们会编写一些 RAII 逻辑来无论如何都重置主线程的带。

不可思议的速度。我们不仅可以在工作站和笔记本电脑上生成闪电般的风险报告（包括针对 xVA 的报告），还能进行以前无法实现的研究。

例如，在我们的示例中，使用 Sobol 进行并行定价需要 350 毫秒，这意味着对于 1,080 个活跃局部波动率的有限差分风险计算需要超过 5 分钟（通过巨大的努力和对代码的侵入式修改，这可能会缩短到二到三分钟）。这太慢了。因此，通用的做法是降低准确性以在可接受的时间生成风险报告。使用 36 个月度时间步和 100,000 条路径，并行定价需要 20 毫秒，有限差分风险报告可能只需要十秒就能生成。然而，结果并不理想，如下方的图表所示，首先是欧期，然后是障碍期，并可与第 425 页的图表进行对比。

![](img/80e507b73893b76e8da2913200e76c47_440_0.png)

![](img/80e507b73893b76e8da2913200e76c47_441_0.png)

金融软件带来了一个遗憾的后果：用户被鼓励接受在合理时间内计算近似且不准确的风险。通过 AAD，我们可以在半秒内生成第 425 页所示的准确图表。我们甚至可以在一秒内运行 1 万条路径以生成更好、更平滑的风险报告。

有趣的是，一秒钟大约是使用单核上使用有限差分（FDM）代替蒙特卡洛方法生成相似准确度风险报告所需的时间。AAD 与并行性的结合大致将 FDM 的速度带到了蒙特卡洛模拟中。

使用 300 万条路径，我们在大约三秒内生成了下方更平滑的图表（即每个三秒，尽管我们在第 14 章中也是在三秒内生成了两者，且在第 15 章的改进后也是三秒）：

![](img/80e507b73893b76e8da2913200e76c47_442_0.png)

![](img/80e507b73893b76e8da2913200e76c47_442_1.png)

如果使用智能的多线程扰动（bumping），至少需要半小时，而在串行模式下至少需要四小时。从任何角度来看，如果没有 AAD，通过蒙特卡洛模拟获取如此精确的微桶（microbuckets）是不可能的。AAD 为金融风险管理开启了新的研究可能性。一个例子是它可以在几秒钟产生准确的微桶。对于其他可能意料之外的应用，请参考 Reghai 的 [97] 和 Andreasen 的 [82]。

我们重申，衍生品系统的主要目的不是产生对模型参数的敏感性，而是对市场工具的风险。因此，AAD 与扰动法之间的这种比较意义不大。通过直接扰动较少的市场价格并重复整个估值过程（包括模型参数的校准），可以更快地产生对对冲工具的敏感性。然而，以这种方式产生市场风险可能会导致通过校准进行微分时产生的不稳定性，且这些有价值的信息使用的工具与校准模型参数使用的工具不同。此外，模型参数本身的敏感性将不会被计算。最后，它无法提供极快速使用与校准模型参数不同的工具来计算风险的灵活性。

我们看到 AAD 可以产生对大量模型参数的敏感性，而无需担心计算大量敏感性的成本问题；产生风险的更好策略是首先如本章解释的那样，计算对模型参数的敏感性，然后将它们转换为对对冲工具的敏感性，正如下一章所解释的，在下一章中我们将 Dupire 模型对市场数据进行校准并产生风险——这种风险不是针对局部波动率的，而是针对隐含波动率的，隐含波动率直接反映了欧式期权的市场价格。

# 检查点与校准 Check-Pointing and Calibration

在上一章中，我们学习了常数时间内对模型参数进行模拟微分，并以极快的速度在 Dupire 模型中生成了*微桶*（局部波动率的敏感性）。在本章中，我们介绍了关键的检查点算法，将其应用于通过校准进行微分，以从模型参数的敏感性获得市场风险，并在 Dupire 模型中实现*超桶*（superbucket）风险报告（隐含波动率的敏感性）。

### 13.1 检查点 CHECK-POINTING

#### 通过检查点减少内存消耗

我们在第 11 章中指出，由于内存消耗，AAD 无法高效地对单核上运行超过 0.01 秒的计算进行微分。更长的计算（几乎所有实际相关的情况）必须分成短于 0.01 秒的片段，并对每个片段单独进行微分，在中间清空内存并在最后聚合敏感性。

这具体是如何通过插桩算法实现的？在路径模拟的情况下，这非常简单，因为敏感性是逐条路径计算并在最后取平均值的。但本节讨论的是一种更通用的解决方案，称为*检查点*（check-pointing）。检查点适用于金融及其他许多具有实际意义的问题。Huge 已在 [90] 中成功将其应用于多维 FDM 的微分。Huge 和 Savine 将其应用于高效地对 LSM 算法微分并生成完整的 xVA 风险。

形式上，我们对一个两步算法进行微分：

```
F(X) = H[G(X)]
```

$G: \mathbb{R}^n \to \mathbb{R}^m$ 是一个向量函数，$H: \mathbb{R}^m \to \mathbb{R}$ 是一个标量函数。

在校准模型的背景下，$H$ 是某些交易的价值。我们在上一章中学了在常数时间内对 $H$ 进行微分。$G$ 是一个从市场价格模型参数的显式函数，例如 Dupires 公式 [12]。

因此在这种情况下 $F(X) = H[X, G(X)]$ 而不是 $H[G(X)]$，但这并没有改变任何东西，因为

对于在高维路径上估值的具有大量现金流的产品（例如 xVA），我们会通过分离两者的微分来限制 RAM 消耗。

在所有这些情况下，由于 $H$ 是标量函数，可以通过 AAD（自动求微分）在常数时间内完成微分。理论上，$F$ 也是标量函数，因此也可以在常数时间内完成微分。但我们讨论了分离其微分的许多原因。因此，练习的是将 $F$ 的微分拆分为 $G$ 的微分和 $H$ 的微分，同时保持常数特性。问题在于 $G$ 不是标量函数，因此无法通过简单的 AAD 在常数时间内完成微分。为了实现这一点，我们需要额外的逻辑，而这种额外的逻辑被称为**检查点（check-pointing）**。

从形式上看，根据链式法则：

```
$$\frac{\partial F}{\partial X} = \frac{\partial G}{\partial X}\frac{\partial H}{\partial Y}$$
```
