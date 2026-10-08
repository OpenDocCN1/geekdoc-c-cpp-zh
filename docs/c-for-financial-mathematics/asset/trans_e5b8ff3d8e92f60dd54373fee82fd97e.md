
# 14.4.2 `runSimulation` 的实现

变量 `nSteps` 对应于差分方程推导过程中使用的数学变量 $N$。

我们决定使用 `shared_ptr` 来存储所有配置对象。当一个类需要引用另一个类的数据时，这应该是你的默认选择。另一种选择是使用类型为 `CallOption` 的成员变量，但这只能存储确切的 `CallOption` 类，而无法存储未来可能编写的子类。事实上，使用更通用类型的成员变量可能更好，这样我们可以模拟对冲其他类型的期权。参见练习 14.4.4。

## 技巧：使用 shared_ptr 引用其他类

通过指针存储对象更加灵活。因为这样在需要时可以持有对子类的引用。在构建引用其他类的类时，这应该是你的默认设计选择。

由于 `HedgingSimulator` 类的所有成员都是私有的，我们需要设置方法以便用户配置该类。我们还希望有一个构造函数，将数据初始化为合理的值。以下是相关的公共声明：

```cpp
void setToHedge(
    std::shared_ptr<CallOption> toHedge) {
    this->toHedge = toHedge;
}
void setSimulationModel(
    std::shared_ptr<BlackScholesModel> model) {
    this->simulationModel = model;
}
void setPricingModel(
    std::shared_ptr<BlackScholesModel> model) {
    this->pricingModel = model;
}
void setNSteps(int nSteps) {
    this->nSteps = nSteps;
}
/* 默认构造函数 */
HedgingSimulator();
```

我们期望该类的使用者设置要对冲的期权、选择要使用的模型和步数，然后要求我们的类运行模拟。我们提供了以下公共方法来执行此操作：

```cpp
/* 运行多次模拟并返回
   盈亏的向量 */
std::vector<double> runSimulations(
    int nSimulations) const;
```

为了实现此方法，我们希望使用三个辅助方法。这些是私有方法。声明如下所示：

```cpp
/* 运行一次模拟并计算
   盈亏 */
double runSimulation() const;
/* 我们应该向客户收取多少费用 */
double chooseCharge(double stockPrice) const;
/* 我们应该持有多少股票 */
double selectStockQuantity(
    double date,
    double stockPrice) const;
```

引入这些辅助方法仅仅是为了确保每个函数简短且易于阅读。例如，函数 `runSimulations` 只是多次调用 `runSimulation` 并将结果存储在向量中。

这就完成了 `HedgingSimulator` 类的成员变量和成员函数的列表。完整的类声明可以在文件 `HedgingSimulator.h` 中找到。

# 14.4.2 `runSimulation` 的实现

最有趣的代码是函数 `runSimulation` 的实现。它开始如下：

```cpp
double HedgingSimulator::runSimulation() const {
    double T = toHedge->getMaturity();
    double S0 = simulationModel->stockPrice;
    vector<double> pricePath =
        simulationModel->generatePricePath(T, nSteps);
    double dt = T / nSteps;
    double charge = chooseCharge(S0);
    double stockQuantity = selectStockQuantity(0, S0);
    double bankBalance = charge - stockQuantity * S0;
}
```

这段代码首先模拟 $\mathbb{P}$ 测度下的价格路径。然后计算交易者在时间 0 时的银行账户余额。这段代码本质上等价于推导公式 (14.1) 时使用的论证。最明显的变化是我们用更长的变量名重写了所有内容。另一个细节是我们调用了函数 `selectStockQuantity`，该函数决定我们在每个时间点需要持有多少股票。我们还调用了函数 `chooseCharge`，该函数决定向客户收取多少费用。通过将计算对冲所需股票数量的过程分离到自己的函数中，我们突出了 $\Delta$ 对冲策略与其他股票对冲策略相比的基本特征。此外，这将使代码易于增强，以便找出如果交易者决定追求另一种投资策略会发生什么。

接下来是一个循环，我们在每个中间时间点对模拟交易。

```cpp
for (int i = 0; i < nSteps - 1; i++) {
    double balanceWithInterest = bankBalance *
        exp(simulationModel->riskFreeRate * dt);
    double S = pricePath[i];
    double date = dt * (i + 1);
    double newStockQuantity =
        selectStockQuantity(date, S);
    double costs =
        (newStockQuantity - stockQuantity) * S;
    bankBalance = balanceWithInterest - costs;
    stockQuantity = newStockQuantity;
}
```

这段代码对应于公式 (14.2)。

最后，我们需要考虑到期时发生的情况。以下代码解决了这个问题，并完成了 `runSimulation` 的定义。

```cpp
double balanceWithInterest = bankBalance *
    exp(simulationModel->riskFreeRate * dt);
double S = pricePath[nSteps - 1];
double stockValue = stockQuantity * S;
double payout = toHedge->payoff(S);
return balanceWithInterest + stockValue - payout;
}
```

这段代码对应于公式 (14.3)。

# 14.4.3 实现 HedgingSimulator 的其他方法

我们的 `HedgingSimulator` 类实现的剩余细节极其简单明了。

`runSimulations` 只是多次调用 `runSimulation` 并将结果存储在向量中：

```cpp
std::vector<double>
HedgingSimulator::runSimulations(
    int nSimulations) const {
    std::vector<double> ret(nSimulations);
    for (int i = 0; i < nSimulations; i++) {
        ret[i] = runSimulation();
    }
    return ret;
}
```

默认构造函数确保新创建的 `HedgingSimulator` 为各种参数设置了合理的值。我们选择这些值，以便我们可以创建一个 `HedgingSimulator` 用于测试目的，而无需进行太多配置。

```cpp
HedgingSimulator::HedgingSimulator() {
    // 选择默认模型和期权
    shared_ptr<BlackScholesModel> model(
        new BlackScholesModel());
    model->stockPrice = 1;
    model->date = 0;
    model->riskFreeRate = 0.05;
    model->volatility = 0.2;
    model->drift = 0.10;
    shared_ptr<CallOption> option =
        make_shared<CallOption>();
    option->setStrike(model->stockPrice);
    option->setMaturity(1);
    setToHedge(option);
    setSimulationModel(model);
    setPricingModel(model);
    nSteps = 10;
}
```

函数 `selectStockQuantity` 将其工作委托给 `CallOption` 类上的一个函数 `delta`。该函数使用公式 (14.4) 计算看涨期权的 $\Delta$。将 $\Delta$ 的计算放入 `CallOption` 类中是合理的，因为我们经常需要计算期权的 $\Delta$。理想情况下，应该在整个期权层级中添加一个计算 $\Delta$ 的方法（参见练习 14.4.4）。

```cpp
double HedgingSimulator::selectStockQuantity(
    double date,
    double stockPrice) const {
    // 创建定价模型的副本
    BlackScholesModel pm = *pricingModel;
    pm.stockPrice = stockPrice;
    pm.date = date;
    return toHedge->delta(pm);
}
```

在上述代码中，这一行

```cpp
BlackScholesModel pm = *pricingModel;
```

很有趣。我们需要改变我们的定价模型，使其状态反映当前时间步的市场状态。成员变量 `pricingModel` 仅反映模拟开始时市场的状态。

我们不希望改变我们 `HedgingSimulator` 的实际配置，因此我们不希望改变成员变量 `pricingModel`。因此，我们创建一个全新的变量 `pm`，并将 `pricingModel` 的值复制到该变量中。然后我们可以设置变量 `pm` 的当前股票价格和日期，而无需改变变量 `pricingModel`。由于成员变量 `pricingModel` 使用指针存储数据，我们必须使用 `*` 将指针转换为我们随后复制的引用。

确定向客户收取金额 的代码类似。它利用了我们已经为看涨期权编写的价格函数。

```cpp
double HedgingSimulator::chooseCharge(
    double stockPrice) const {
    // 创建定价模型的副本
    BlackScholesModel pm = *pricingModel;
    pm.stockPrice = stockPrice;
    return toHedge->price(pm);
}
```

# 14.4.4 对 CallOption 的修改

我们需要向 `CallOption` 类添加一个新的公共函数来计算 Black-Scholes $\Delta$。以下是该函数的定义。

```cpp
double CallOption::delta(
    const BlackScholesModel& bsm) const {
    double S = bsm.stockPrice;
    double K = getStrike();
    double sigma = bsm.volatility;
    double r = bsm.riskFreeRate;
    double T = getMaturity() - bsm.date;

    double numerator = log(S/K) + (r + sigma * sigma * 0.5) * T;
    double denominator = sigma * sqrt(T);
    double d1 = numerator / denominator;
    return normcdf(d1);
}
```

