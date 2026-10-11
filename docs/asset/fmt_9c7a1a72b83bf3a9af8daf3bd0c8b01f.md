
所有这些实现代码都非常简单。然而，请停下来思考一下，我们的 `Portfolio` 实现现在可以存储任何类型的股票衍生品并对其定价的事实。它将始终根据所含衍生品的类型选择最高效的定价方法。看涨期权将使用看涨期权的 Black-Scholes 公式进行定价。看跌期权将使用看跌期权公式进行定价。其他期权将通过蒙特卡洛方法进行定价。同样，股票和无息债券的持仓将通过调用相应的定价函数进行定价。最终结果是一个极其通用且有用的类。

此外，我们的 `Portfolio` 也能同样适用于我们尚未实现的证券！如果我们库的使用者决定销售新型金融产品，他们可以提供我们类自己的实现。能够在无需重写所有软件的情况下应对快速变化的业务需求，是商业软件的一个基本特征。正是这种“可插拔性”使面向对象软件在金融行业中如此重要。

## 13.3 测试

正如我们在本书中一直强调的那样，软件开发的一个关键部分是测试您的代码是否正常工作。

在这个测试中，我们检查了看跌-看涨平价公式，我们将对此进行推导。一个由 1 单位看涨期权和 $-1$ 单位看跌期权组成的投资组合 $\mathbf{P}$（两者的执行价格均为 $K$），在到期时将支付等于

$$\max\{S_T - K, 0\} - \max\{K - S_T, 0\}$$

的金额（其中 $S_T$ 是到期时的股票价格）。通过分别考虑 $S_T < K$ 和 $S_T \geq K$ 的情况，可以看出该表达式简化为：

$$S_T - K.$$

因此，$\mathbf{P}$ 的价值等于 $S_T - K$ 的折现期望值。在 $\mathbb{Q}$-测度下，$S_T$ 的折现期望值必须为 $S_0$。我们推断出 $S_T - K$ 的折现期望值为：

$$ S_0 - e^{-rT} K. $$

这是 $\mathcal{P}$ 在时间 0 的价值。

下面的测试证实了当 $r=0$ 时，这对我们的 `Portfolio` 类成立。

```cpp
static void testPutCallParity() {
    shared_ptr<Portfolio> portfolio
        = Portfolio::newInstance();
    shared_ptr<CallOption> c
        = make_shared<CallOption>();
    c->setStrike(110);
    c->setMaturity(1.0);
    shared_ptr<PutOption> p = make_shared<PutOption>();
    p->setStrike(110);
    p->setMaturity(1.0);
    portfolio->add(100, c);
    portfolio->add(-100, p);
    BlackScholesModel bsm;
    bsm.volatility = 0.1;
    bsm.stockPrice = 100;
    bsm.riskFreeRate = 0;
    double expected = bsm.stockPrice - c->getStrike();
    double portfolioPrice = portfolio->price(bsm);
    ASSERT_APPROX_EQUAL(100 * expected,
        portfolioPrice, 0.0001);
}
```

人们可能会觉得我们应该为我们的 `Portfolio` 类编写更多测试，以测试它是否正确地为更复杂的投资组合定价。我们设计的一个核心好处是，为 **Portfolio** 类编写大量测试实际上并不是很有必要。我们已经有一套测试来确认各种不同类型的期权被正确定价。 **Portfolio** 类有一个非常简单的 *price* 方法，该方法的每一行都已经由我们的看跌-看涨平价测试覆盖。测试 **Portfolio** 是否能处理由复杂期权组成的投资组合不会带来任何新的东西。

## 13.4 UML

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_252_0.png)

**图 13.1：** Portfolio 类的设计。

图 13.1 总结了我们在本章中介绍的类，以 UML 图的形式呈现。

该图表明 **PortfolioImpl** 实现了接口 **Portfolio**，而 **Portfolio** 又继承了接口 *Priceable*。 *Priceable* 也由类 *CallOption* 实现。

另一方面，**PortfolioImpl** 包含一个 *Priceable* 对象的向量；这由标记为 *securities* 的箭头表示。这种关系是一种 *has a* 关系。**PortfolioImpl** 拥有一些相关的证券。所有这些关系都是 *is a* 关系，并通过类继承来实现。

箭头上的 `*` 符号表示 **PortfolioImpl** 可以拥有任意数量的相关证券。在 UML 中，你可以用数字或数字范围来标记任何关系的 *multiplicity*（重数）。例如，人类与其父母之间的“parents”关系可以标记为 multiplicity 2。`*` 仅仅表示重数没有限制。

`newInstance` 函数下方有下划线，以表示它是一个静态函数。

我们特意从图中省略了期权的完整层级结构，以保持其可读性。我们还表明 `CallOption` 拥有公共成员变量 *strike* 和 *maturity*，即使这些变量只能通过 get 和 set 方法访问。我们没有提到 **PortfolioImpl** 使用共享指针的向量来存储对 *Priceable* 对象的引用。因此，我们的图是对类的一种轻微简化。它的目的是阐明设计，而不是精确地反映代码。

## 13.5 局限性

我们并不声称本章中的代码是对期权投资组合定价的最终定论。以下是一些重要的局限性。

- (i) 我们在蒙特卡洛计算中使用了固定的情景数和步数，这应该是可配置的。
- (ii) 我们并没有尝试优化我们的代码。
- (iii) 我们没有利用现代计算机可用的多核 CPU。
- (iv) 我们的 ContinuousTimeOption 和 Priceable 接口不够通用。例如，它们无法处理离散时间期权和基于多个基础股票的期权。
- (v) 通过蒙特卡洛方法为投资组合定价时，持续生成随机数不是一个好主意。最好一次性生成所有风险因子，然后使用相同的情景来为每个元素定价。这既减少了随机数的生成，又确保了套期保值能精确地对冲。

这些局限性中的许多将在后续章节中解决。

## 练习

1. 13.5.1. 无息债券是一种金融工具，保证在到期日 T 支付价值 1。这些工具在实际中并不经常交易，但作为表示无风险银行账户的数学抽象是非常有用的。在时间 T 之前将资金存入无风险银行账户等同于投资于到期日为 T 的无息债券。风险中性定价理论告诉我们，无息债券在时间 0 的风险中性价格为 $\exp(-rT)$。

利用这一事实，为股票和无息债券创建 Priceable 接口的实现。

13.5.2. 实现 `UpAndInOption` 和 `DownAndInOption`。包含一个 `UpAndInOption` 和一个 `UpAndOutOption` 的组合应与包含一个 `CallOption` 的组合价值相同。使用 `Portfolio` 类验证这一点。对结果的准确性进行评论。

# 13.6 总结

在开发 `Portfolio` 的过程中，我们并没有遇到任何新的 C++ 语言特性，只是了解了一些用于有效使用 C++ 的设计模式。

- 使用 `shared_ptr` 来构建复杂的数据结构，以长期存储对象。
- 使用*静态工厂方法*设计模式来最大限度地隐藏信息并减少文件之间的依赖关系。
- 利用面向对象编程来实现可插拔的代码，即使出现新的需求也无需修改。

# 第 14 章
## 德尔塔对冲

在本章中，我们将展示如何将 C++ 应用于超越简单无风险定价的金融数学问题。特别是，练习将向你展示如何将面向对象编程技术应用于解决广泛的问题。

我们要解决的一个问题是，从数值上证明附录 A 中描述的*德尔塔对冲*策略是一种有效的交易策略。

在文献 [2] 中，已证明只要使用对现实的各种近似，德尔塔对冲策略就是完全无风险的。这些假设包括：必须在连续时间内重新调整仓位；股票价格必须在 ℙ 测度下遵循几何布朗运动；没有交易成本；市场必须是无限流动的；利率必须固定在水平 *r* ；等等。

我们将在本章中证明，如果将连续交易时间的假设弱化为在固定时间点交易，德尔塔对冲仍然是一种相当有效的策略。该策略不再完全无风险，但通过频繁地重新对冲，可以将风险降低到可接受的水平。

我们开发的软件可以轻松地增强，以测试削弱其他假设的影响。此外，可以轻松地改编软件，以测试其他对冲和投资策略的有效性。

## 14.1 离散时间德尔塔对冲

我们将模拟一只股票的交易，该股票按照 Black–Scholes ℙ-测度模型演变。这意味着我们可以使用现有的 **BlackScholesModel** 及其函数 *generatePricePath* 来模拟给定时间区间内的股票价格。时间 *t* 时的股票价格表示为 *S*_*t*。

在时间 0，一名交易员向客户出售了一只针对该股票的欧式看涨期权，执行价为 *K*，到期日为 *T*，价格为 Black–Scholes 价格。这意味着，作为价格 *P* 的交换，交易员承诺在时间 *T* 向客户支付如下金额：

$$\max\{S_{T} - K, 0\}$$

交易员的策略是对这一负债进行德尔塔对冲。他们在 $N$ 个离散时间步长中进行德尔塔对冲。因此，每个时间步长的长度为 $\delta t = \frac{T}{N}$。我们用整数 $i \in \{0, N - 1\}$ 来标记交易员进行对冲的时间点。因此，时间点 $i$ 发生在时间 $i\delta t$。在时间点 $i$，交易员将确保持有恰好 $\Delta_{i}$ 单位的股票，其中 $\Delta_{i}$ 是时间点 $i$ 时看涨期权的 Black–Scholes 德尔塔值。剩余的资金投资于无风险账户，该账户以固定利率 $r$ 增长。

我们用 $b_{i}$ 表示交易员在每个时间点 $i$ 的银行存款余额。在时间点 0，交易员将

$$ b_{0} = P - \Delta_{0} S_{0} \tag{14.1} $$

存入其无风险账户，并将其余本金 $\Delta_{0} S_{0}$ 投资于股票。然后，我们可以使用差分方程计算交易员在后续时间点 $i$ 的银行存款余额：

$$ b_{i} = e^{r \delta t} b_{i-1} - (\Delta_{i} - \Delta_{i-1}) S_{i \delta t}. \tag{14.2} $$

该方程之所以成立，是因为他们银行中的资金以利率 $r$ 增长，从而产生项 $e^{r \delta t} b_{i-1}$，代表交易员重新平衡其投资组合之前银行中的金额。然后，交易员需要重新平衡其投资组合，以确保持有 $\Delta_{i}$ 单位的股票。这意味着他们需要购买 $\left(\Delta_{i} - \Delta_{i-1}\right)$ 单位的股票。这解释了 $-\left(\Delta_{i} - \Delta_{i-1}\right) S_{i \delta t}$ 项。

在时间点 $N$，期权达到到期日。交易员不进行德尔塔对冲。相反，他们卖出剩余的股票持仓并支付负债。这告诉我们

$$ b_{N} = e^{r \delta t} b_{N-1} + \Delta_{N-1} S_{T} - \max\{S - K, 0\}. \tag{14.3} $$

这个最终的银行存款余额代表了交易员的盈亏。公式 (14.1) 到 (14.3) 的推导没有使用比德尔塔对冲策略的定义和基本会计计算更复杂的东西。这些计算并不比您用来理解自己个人账户和购物消费的计算更复杂。

我们可以使用差分方程 (14.1) 到 (14.3) 在给定的模拟股票价格集合下计算交易员的盈亏。我们需要的额外要素是 $\Delta_{i}$ 的显式公式。根据定义，$\Delta = \frac{\partial C}{\partial S}$，其中 $C$ 是看涨期权的价格，$S$ 是当前股票价格。这意味着只需对看涨期权价格的 Black–Scholes 公式 (A.6) 进行微分即可计算 $\Delta$。结果是

$$ \Delta = N(d_{1}) \tag{14.4} $$

其中 $N$ 和 $d_{1}$ 的定义如公式 (A.6) 所示。本节中的公式共同允许我们明确计算特定场景下交易员的盈亏。通过生成多个场景，我们可以计算交易员盈亏 (PnL) 的统计数据。最有趣的是，我们可以绘制交易员 PnL 的直方图。我们将在下一节中查看执行此操作所需的 C++ 代码。

## 14.2 在 C++ 中实现德尔塔对冲策略

鉴于前一节中的显式公式，实现德尔塔对冲策略是 straightforward 的。然而，如果直接将这些方程复制到 C++ 中，最终得到的代码将包含诸如 **b** 这样毫无助益名称的变量，对于没有文档可查的人来说，这些变量毫无意义。

编程中的惯例是使用长的变量名，以清楚地解释正在发生的事情。这与数学中使用单字母变量名的惯例相反。

你会看到下面的代码对所有变量使用英文名称，这清楚地展示了所有项是如何推导出来的。其优势在于，仅通过查看代码本身就可以理解，无需阅读另一个文件中的说明文档。

### 14.2.1 类声明

我们的第一步是声明一个用于运行我们对冲模拟的类。我们将该类命名为 **HedgingSimulator**。它将是一个可配置的类，允许用户设置要对冲的期权值、用于模拟的模型等。我们的设计包含一定的灵活性，允许用户设置一个用于生成股票价格的模型（`simulationModel`）和另一个用于计算向客户收取的金额以及每个时间点应持有的股票数量的模型（`pricingModel`）。通过拥有两个独立的模型，我们将能够测试如果交易员对市场的信念不正确会发生什么。

这些想法促使我们定义了一个名为 HedgingSimulator 的类的以下私有成员变量：

```cpp
private:
  /* The option that has been written */
  std::shared_ptr<CallOption> toHedge;
  /* The model used to simulate stock prices */
  std::shared_ptr<BlackScholesModel> simulationModel;
  /* The model used to compute prices and deltas */
  std::shared_ptr<BlackScholesModel> pricingModel;
  /* The number of steps to use */
```

# 14.4.2 `runSimulation` 的实现

变量 `nSteps` 对应于差分方程推导过程中使用的数学变量 $N$。

我们决定使用 `shared_ptr` 来存储所有配置对象。当一个类需要引用另一个类的数据时，这应该是你的默认选择。另一种选择是使用类型为 `CallOption` 的成员变量，但这只能存储确切的 `CallOption` 类，而无法存储未来可能编写的子类。事实上，使用更通用类型的成员变量可能更好，这样我们可以模拟对冲其他类型的期权。参见练习 14.4.4。

## 技巧：使用 shared_ptr 引用其他类

通过指针存储对象更加灵活。因为这样在需要时可以持有对子类的引用。在构建引用其他类的类时，这应该是你的默认设计选择。

由于 `HedgingSimulator` 类的所有成员都是私有的，我们需要设置方法以便用户配置该类。我们还希望有一个构造函数，将数据初始化为合理的值。以下是相关的公共声明：

```cpp
void setToHedge(std::shared_ptr<CallOption> toHedge) {
    this->toHedge = toHedge;
}
void setSimulationModel(std::shared_ptr<BlackScholesModel> model) {
    this->simulationModel = model;
}
void setPricingModel(std::shared_ptr<BlackScholesModel> model) {
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
/* 运行多次模拟并返回盈亏的向量 */
std::vector<double> runSimulations(int nSimulations) const;
```

为了实现此方法，我们希望使用三个辅助方法。这些是私有方法。声明如下所示：

```cpp
/* 运行一次模拟并计算盈亏 */
double runSimulation() const;
/* 我们应该向客户收取多少费用 */
double chooseCharge(double stockPrice) const;
/* 我们应该持有多少股票 */
double selectStockQuantity(double date, double stockPrice) const;
```
