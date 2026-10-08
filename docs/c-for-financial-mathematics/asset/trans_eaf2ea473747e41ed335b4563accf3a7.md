

(iii) 定义

$$s_{t_i} = s_{t_{i-1}} + \left(\mu - \frac{1}{2}\sigma^2\right)\delta t_i + \sigma\sqrt{\delta t_i}\epsilon_i.$$ 

(iv) 定义 $S_{t_i} = \exp(s_{t_i})$.

在 $S_{t_i}$ 处生成的股票价格将与 Black-Scholes 模型给出的具有相同的联合概率分布。

基于该算法的数学表述，实现我们的辅助函数是 straightforward（直接明了的）的。你可以在 `BlackScholesModel.cpp` 中找到代码。

```cpp
vector<double> BlackScholesModel::generatePricePath(
	double toDate,
	int nSteps,
	double drift ) const {
vector<double> path(nSteps,0.0);
vector<double> epsilon = randn( nSteps );
double dt = (toDate-date)/nSteps;
double a = (drift-volatility*volatility*0.5)*dt;
double b = volatility*sqrt(dt);
double currentLogS = log( stockPrice );
for (int i=0; i<nSteps; i++) {
	double dLogS = a + b*epsilon[i];
	double logS = currentLogS + dLogS;
	path[i] = exp( logS );
	currentLogS = logS;
}
	return path;
}
```

我们只实现了等间隔时间点的算法。将其推广到任意时间点是很简单的。

在实现了该私有函数之后，公共函数非常简单。这些实现同样放置在 `BlackScholesModel.cpp` 中。

```cpp
vector<double> BlackScholesModel::generatePricePath(
	double toDate,
	int nSteps ) const {
	return generatePricePath(toDate, nSteps, drift );
}

vector<double> BlackScholesModel::
	generateRiskNeutralPricePath(
	double toDate,
	int nSteps ) const {
	return generatePricePath(
    toDate, nSteps, riskFreeRate );
}
```

需要注意的是，通过使用一种带有**私有**辅助函数的设计，我们避免了两次编写相同的复杂代码。

测试这段代码很重要。第一个测试是视觉上的，我们想检查这是否真的看起来像一条价格路径。我们可以使用 LineChart 类来做到这一点。

```cpp
void testVisually() {
    BlackScholesModel bsm;
    bsm.riskFreeRate = 0.05;
    bsm.volatility = 0.1;
    bsm.stockPrice = 100.0;
    bsm.date = 2.0;
    
    int nSteps = 1000;
    double maturity = 4.0;
    
    vector<double> path =
        bsm.generatePricePath( maturity, nSteps );
    double dt = (maturity-bsm.date)/nSteps;
    vector<double> times =
        linspace(dt,maturity,nSteps);
    LineChart lineChart;
    lineChart.setTitle("Stock price path");
    lineChart.setSeries(times, path);
    lineChart.writeAsHTML("examplePricePath.html");
}
```

这个函数使用了一个添加到 matlib 库中的辅助函数 `linspace`。调用 `linspace(a,b,n)` 生成 $a$ 和 $b$ 值之间 $n$ 个均匀分布的数字。输出图表如图 9.1 所示。视觉检查仅仅是观察它是否合理地像真实股票价格的历史记录。

你可以使用 FMLib9 运行此测试以获取相关代码。希望你认同，在 C++ 中生成如此复杂的图表是我们对 C++ 理解程度大幅提升的有力证据。

视觉测试很有用，但我们始终应确保对代码进行完全自动化的测试。原因是，一旦有了大量代码，就需要定期测试，以防我们不小心写入了 bug。如果我们的测试是完全自动化的，我们可以每次修改代码时都运行它们。

一个简单的测试是，如果我们的风险中性价格路径函数是正确的，那么最终股票价格的折现平均值应等于初始价格。我们在下面的代码中测试这一点：

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_172_0.png)

**图 9.1：** 一条模拟的股票价格路径。底部轴是以年为单位的时，垂直轴是以美元为单位的价格。

```cpp
void testRiskNeutralPricePath() {
    rng("default");
    
    BlackScholesModel bsm;
    bsm.riskFreeRate = 0.05;
    bsm.volatility = 0.1;
    bsm.stockPrice = 100.0;
    bsm.date = 2.0;
    
    int nPaths = 10000;
    int nsteps = 5;
    double maturity = 4.0;
    vector<double> finalPrices(nPaths, 0.0);
for (int i=0; i<nPaths; i++) {
    vector<double> path =
        bsm.generateRiskNeutralPricePath(
            maturity, nsteps );
    finalPrices[i] = path.back();
}
ASSERT_APPROX_EQUAL( mean( finalPrices ),
    exp( bsm.riskFreeRate*2.0)*bsm.stockPrice,
    0.5);
}
```

我们在下面这一行中引入了一个新特性：

```cpp
rng("default");
```

这不是对标准 C++ 函数的调用，而是 FM-Lib 库中的一个函数，它将随机数生成器的状态重置回其原始的“默认”状态。对 `randUniform` 和 `randn` 的调用每次将随机数生成器重置为默认状态时，总是生成完全相同的“随机数”序列。我们将“随机数”一词加上引号，因为生成的随机数并非真正随机。计算机生成的随机数仅在外表上*看似*随机，这与数字 $\pi$ 的小数位数看起来随机的方式非常相似。更准确地说，它们被称为*伪随机数*。

重置随机数生成器的状态对于测试非常有用，因为它保证了每次运行测试时，我们都使用相同的伪随机数。这意味着如果测试通过一次，它将永远通过；同样，如果失败一次，它将永远失败。在调试代码时，如果一个测试有时通过有时失败是非常令人沮丧的——尤其是当你每次更改代码都运行所有测试时。

**提示：依赖于随机数的测试**

在运行涉及随机数的测试之前，始终将随机数生成器重置为已知状态。

## 9.2 编写蒙特卡洛定价器

我们要编写一个名为 `MonteCarloPricer` 的类，该类配置有 `nScenarios`，即要生成的场景数量。这将默认为 10000。

MonteCarloPricer 还将有一个函数 `price`，它接受一个 Call-Option 和一个 `BlackScholesModel`。然后它应该通过蒙特卡洛方法计算 `CallOption` 的价格。

`MonteCarloPricer` 的 C++ 声明与上述自然语言规范所述基本相同。

```cpp
#pragma once
#include "stdafx.h"
#include "CallOption.h"
#include "BlackScholesModel.h"
class MonteCarloPricer {
public:
    /* 构造函数 */
    MonteCarloPricer();
    /* 场景数量 */
    int nScenarios;
    /* 给看涨期权定价 */
    double price( const CallOption& option,
                  const BlackScholesModel& model );
};
void testMonteCarloPricer();
```

注意那些现在熟悉的模式。头文件名为 `MonteCarloPricer.h`。它以 `#pragma once` 开头。我们 `#include "stdafx.h"`。构造函数看起来像一个名为 `MonteCarloPricer` 的函数声明，但没有返回类型。我们通过 `const` 引用传递 `option` 和 `model`。有一个函数用于启用代码测试。

C++ 文件的开头同样平凡：

```cpp
#include "MonteCarloPricer.h"
#include "matlib.h"
using namespace std;
MonteCarloPricer::MonteCarloPricer() :
    nScenarios(10000) {
}
```

C++ 文件名为 `MonteCarloPricer.cpp`。它包含 `MonteCarloPricer.h`。`MonteCarloPricer` 有一个默认构造函数，该构造函数为默认使用的场景数量选择一个值。

为了编写有趣的代码，我们提供了 `price` 函数的实现。这遵循算法 1。

```cpp
double MonteCarloPricer::price(
    const CallOption& callOption,
    const BlackScholesModel& model ) {
  double total= 0.0;
  for (int i=0; i<nScenarios; i++) {
    vector<double> path= model.
      generateRiskNeutralPricePath(
        callOption.maturity,
        1 );
    double stockPrice = path.back();
    double payoff=callOption.payoff(stockPrice);
    total+= payoff;
  }
  double mean = total/nScenarios;
  double r = model.riskFreeRate;
  double T = callOption.maturity - model.date;
  return exp(-r*T)*mean;
}
```

由于我们正在对仅依赖到期时股票价格的 CallOption 进行定价，我们计算中只需要一个时间步。

当然，我们也需要对此功能进行测试。我们可以将其与解析 Black-Scholes 公式进行比较。

```cpp
static void testPriceCallOption() {
  rng("default");

  CallOption c;
  c.strike = 110;
  c.maturity = 2;

  BlackScholesModel m;
  m.volatility = 0.1;
  m.riskFreeRate = 0.05;
  m.stockPrice = 100.0;
  m.drift = 0.1;
  m.date = 1;

  MonteCarloPricer pricer;
  double price = pricer.price( c, m );
  double expected = c.price( m );
  ASSERT_APPROX_EQUAL( price, expected, 0.1 );
}
```

