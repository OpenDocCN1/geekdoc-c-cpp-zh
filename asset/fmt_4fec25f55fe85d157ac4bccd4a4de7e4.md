
```cpp
const vector<SimulRequest>& requests) = 0;

virtual void nextScenario(Scenario<T>& s) = 0;

};
```

每个特定模型的 API 实例化都必须设置模型，使其在仿真期间产生请求的折现因子。

## 13.4 索引

此外，在运行时，当模型为某些事件日期通信若干折现因子时，我们希望评估器能够直接为每个 `df` 节点选择正确的因子，而不需要在某些映射或表中查找其期限。因此，我们需要我们的访问者也索引每个事件日期所需的所有折现因子，并将它们的索引存储在 `df` 节点上。这看起来可能很困惑，所以让我们来看一个例子。

考虑以下（虚拟）脚本：

| | |
|---|---|
| 05Jan2021 | X = 100 |
| 05Jul2021 | Y pays 100 * df(05Jan2022) |
| 05Jan2022 | Z1 pays 100 * df(05Jan2023)<br>Z2 pays 100 * df(05Jan2024)<br>Z3 pays 100 * df(05Jan2025)<br>Z4 pays 200 * df(05Jan2025) |

解析后，折现期限被存储在 `df` 节点中：05Jul2021 事件对应为 05Jan2022；05Jan2022 事件的三个 `df` 节点对应为 05Jan2023、05Jan2024 和 05Jan2025。处理器访问所有 `df` 节点并收集以下信息：

- 05Jan2021 不需要折现因子。
- 05Jul2021 需要一个折现因子。其期限为 05Jan2022。由于只有一个，所以它的索引为 0。
- 05Jan2022 需要三个折现因子。它们的期限为 05Jan2023（索引 0）、05Jan2024（索引 1）和 05Jan2025（索引 2）。尽管我们四个 `df` 节点，但第三和第四个节点指向相同的期限；因此它们指向同一个折现因子。我们数了三个折现因子，所以索引了 0 到 2。

为了避免在运行时搜索折现因子的期限，处理器将每个请求折现因子的索引存储在它的 `df` 节点上。换句话说，我们以索引变量相同的方式索引计数，这些变量是脚本全局的，而折现因子是事件日期局部的（每个事件日期）。关于许多折现因子的信息（它们的期限和索引是什么）全部封装在 `SimulRequest::discMats` 中。向量的大小是折现因子的数量，`SimulRequest::discMats[i]` 是期限。例如，对于日期 05Jan2022，我们有 05Jan2023（索引 0）、05Jan2024（索引 1）和 05Jan2025（索引 2）。因此，`discMats[0] = 05Jan2023`，`discMats[1] = 05Jan2024` 且 `discMats[2] = 05Jan2025`。

固定收益工具

一个尚未到期的远期合约期权（也称为跨曲线期权），如下：

| 到期 | 期权支付看涨 ( fwd(FWDDATE), K) = 100 |

对于折扣，最好只通信远期合约（forwards），永远不要通信现货（spots），并扩展解析器使“spot)”仍然存在，但在解析时被解析为“fwd(FixingDate)”。

如何根据利率、回购（repo）、股息、便利收益率等计算远期合约是模型的职责。

但处理器的职责是为每个事件计算需要多少个远期合约、它们的期限日是什么、对它们进行索引，并将索引存储在 `fwd` 节点（spot 节点）上。仿真期间，模型按照评估器可以访问的完全相同的顺序计算模拟远期合约。这显然对我们折扣因子的处理是理想的，并且意味着我们将 `SimulRequest` 和 `SimulData` 对象扩展为：

```cpp
struct SimulRequest
{
    vector<Date> fwdMats;
    vector<pair<Date, Date>> discMats;
};

template <class T>
struct SimulData
{
    T numeraire;
    vector<T> fwds;
    vector<T> discounts;
}
```

## 13.9 LIBOR 与利率锚定

Libor 与折扣和远期一样，由模型内部计算。因此，对 Libor 的处理与折扣没有区别。所有事件日期的 Libor 都由处理器进行计数和索引，Libor 的期限存储在 Libor 节点上，连同其曲线的索引。这实际上是唯一的区别：Libor 通过三个要素进行指定、识别和索引：它们的索引和两个期限日。其他一切都相同：扩展的 `SimulRequest` 和 `SimulData` 对象被预先分配。Libor 的评估器从 `SimulData::libors[index]` 处随机访问 Libor，其中 `index` 是处理器存储在 Libor 节点上的 Libor 索引。每个索引标识每个事件日期的一个 Libor，并唯一对应于一个三元组 `(curveldx, T1, T2)`。

```cpp
struct SimulRequest
{
    vector<Date> fwdMats;
    vector<pair<Idx, Date>> discMats;
    vector<triplet<Idx, Date, Date>> liborMats;
};
```

```cpp
template <class T>
struct SimulData
{
    T numeraire;
    vector<T> fwds;
    vector<T> discounts;
    vector<T> libors;
};
```

这种*三元组*（triplet）显然是将不同类型的对象的*对*（pair）扩展到三个对象的程度。它实际上是一个 `typedef`，实例化了 C++11 标准库中更标准的 `tuple` 类：

```cpp
#include <tuple>
template <class T1, class T2, class T3>
using triplet = tuple<T1, T2, T3>;
```

`Idx` 用于库中标识曲线，通常是一个字符串。

```cpp
typedef string Idx;
```

一旦我们有了 Libor，我们也可以按照开发年金时完全相同的方式开发*交换率*（swapRate）和*交换现值*（swapPV）。

## 13.10 掉期与期权的脚本

结束了我们对利率支持的讨论。我们拥有编写掉期所需的所有部分：

```
start: STARTDATE      swap pays
end: ENDDATE          -libor(StartPeriod, EndPeriod, FLBASIS, FLIDX)
freq: FLFREQ          * cvg(StartPeriod, EndPeriod, FLBASIS)
fixing: start-2b
```

```
start: STARTDATE      swap pays
end: ENDDATE          CPN * cvg(StartPeriod, EndPeriod, FLBASIS)
freq: FIXFREQ          on EndPeriod
fixing: start-2b
```

固定收益工具

我们也可以通过封顶浮动利息来使其奇异化，例如：

| swap pays |
| :--- |
| start: STARTDATE -min( CAP, |
| end: ENDDATE liber(StartPeriod, EndPeriod, FLBASIS, FLIDX) |
| freq: FLFREQ * cvg(StartPeriod, EndPeriod, FLBASIS) |
| fixing: start-2b on EndPeriod |

而且当然，我们可以在预定义的计划上更改概念，使利息依赖于路径，对于上限（cap），我们有如下脚本：

| cap pays |
| :--- |
| start: STARTDATE liber(StartPeriod, EndPeriod, FLBASIS, FLIDX) |
| end: ENDDATE STRIKE |
| freq: FLFREQ * cvg(StartPeriod, EndPeriod, FLBASIS) |
| fixing: start-2b on EndPeriod |

对于掉期，我们可以使用类似的内容：

| swapt pays |
| :--- |
| EXPIRY-2B swapPV(START, END, FIXFREQ, STRIKE, FLBASIS, FLIDX), 0) |

但我们不建议这样做。这个脚本描述的是掉期的现金流，但一种通常被认为等效的收益支付。此外，这仅适用于标准掉期，例如，对封顶掉期的期权就不能这样编写脚本。在考虑信用时，这不再正确，并且丢失了关于现金流的重要信息。对掉期进行定价对于模型校准是可以的，但在风险管理背景下并不行。编写期权的正确方法应该是：

```
flCpn = lib(StartPeriod, EndPeriod, FLBASIS, FLIDX) 
* cvg(StartPeriod, EndPeriod, FLBASIS)
swap pays - flCpn on EndPeriod
if Exercised = 1
then swapt pays - flCpn on EndPeriod
end
```

```
fixCpn = CPN
start: STARTDATE
* cvg(StartPeriod, EndPeriod, FLBASIS)
end: ENDDATE
swap pays fixCpn on EndPeriod
freq: FLFREQ
if Exercised = 1
fixing: start-2b
then swap pays fixCpn on EndPeriod
if PV (swap) > 0
    then Exercised = 1
    else Exercised = 0
endif
STARTDATE-2B
```

脚本的最后一行（按时间顺序是第一行）值得注释，特别是因为看起来我们似乎仍然缺少了一部分。它说，如果掉期的现值（PV）为正，我们将 `Exercised` 设置为 1，意味着我们行使期权；否则将其设置为 0。随后，掉期期权的现金流都是掉期的现金流乘以 `Exercised`，这意味着它们只有在掉期期权行使时才计算，即当 `PV(swap)` 为正时。

# 14 多种资产

## 14.1 多种资产

某些衍生品依赖于多个标的资产。掉期通常由多个资产的联合路径组成。库中对这种支持与 Libor 类似，因为每条基础曲线都是命名的资产。实践中，这意味着 `fwd` 和 `spot` 关键字接受一个额外的参数，资产代码（通常是字符串）。现在，处理器不仅根据期限日索引远期合约，还根据资产代码索引。每个事件日期的远期合约根据代码和期限日进行指定、识别和索引。`SimulRequest` 对象相应扩展：

```cpp
struct SimulRequest
{
    vector<pair<Code, Date>> fwdMats;
    vector<pair<Date, Date>> discMats;
    vector<triplet<Idx, Date, Date>> liborMats;
};
```

不需要扩展 `SimulData`。结合上一节介绍的向量和预定义向量（包括字符串），我们拥有编写篮子期权所需的所有工具：

| NSTOCKS | 5 |
| :--- |
| STRIKE | 0.05 |
| TRADATE | loop (0, NSTOCKS) s0[ii] = spot(stocks[ii]) endLoop |
| EXPIRY | loop (0, NSTOCKS) s1 = spot(stocks[ii]) perf = perf + weights[ii] * (s1 - s0[ii]) / s0[ii] endLoop opt pays max(0, perf - STRIKE) |

使用预定义的向量 `WEIGHTS`：

| 0.20 |
| :--- |
| 0.10 |
| 0.15 |
| 0.25 |
| 0.30 |

以及预定义的字符串向量（资产代码）`STOCKS`：

| STOCK1 |
| STOCK2 |
| STOCK3 |
| STOCK4 |
| STOCK5 |

我们也可以做一个针对某只股票的看涨期权，带有另一只股票的障碍：

# 多种底层资产

| BARSTART | vAlive = 1 |

```
start: BARSTART
: BAREND
freq: BARFREQ
fixing:    if spot( BARSTOCK) > BARRIER
then vAlive = 0
endif
```

| MATURITY | opt pays vAlive |
* PAYOFF(spot(PAYSTOCK), STRIKE) | |

## 14.2 多币种

依赖多种货币资产和汇率的金融交易需要一种特殊的模型，通常称为 Quanto 模型（quanto模型）或混合模型。它们仍然是一组相关的单资产或收益率曲线的集合，但在涉及多种货币时，这变得非常复杂。首先，模型必须承认哪种货币是其本币，所有以不同货币计价的资产和汇率在其风险中性漂移中都带有额外风险，这种风险与其与本币的协方差对应，被称为 Quanto 调整（quanto adjustment）。其次，当每个货币的单独收益率模型本身是多因子时，全局相关矩阵的处理将非常困难。第三，（可能是随机的）汇率是该货币计价资产的（部分）风险中性漂移，而外汇汇率的 RN 漂移包含了本币和外国汇率之差，其中至少有一种汇率本身受量子化影响。最后，这些模型以难以校准而闻名。2000年代初，学术界和华尔街从业者投入了大量精力开发此类模型，以正确管理如可回赎反向双期（Callable Reverse Duals）之类的混合产品。如今，这些模型被复用于 xVA 领域，这是一种更复杂的期权，但也依赖于属于不同类别和货币的多种资产。

我们假设可以使用这样的模型，并且能够为基准货币（本币）提供无套利价值，其中资产价格、折扣和 Libor 属于各种货币。脚本还需要一个关于其本币的概念，理想情况下与模型相同，即除非另有说明，否则所有支付均以该货币进行。这也是进行评估时使用的货币，因此最终值和风险敏感性也以该货币表示。此外，我们假设模型知道资产和 Libor 以何种货币计价，并能够通过 Libor 索引从资产代码中查找信息。

# 现代计算金融

如果是这种情况，可能需要在模型的 API 包装器中进行某些查找。脚本库不需要了解所有信息。然而，折扣因子没有索引，对于以本币以外任何货币计价的折扣因子，必须显式提供货币作为参数。从所有角度来看，这意味着 `df` 的语法为：

```
df(T1 , T2, CCY)
```

其中如果省略 `CCY`，它在解析时将解析为本币。因此，折扣需要根据货币以及开始和结束时间进行索引，`SimulRequest` 对象也随之进行了扩展：

```cpp
struct SimulRequest {
  vector<pair<Code, Date>> fwdMats;
  vector<triplet<Ccy, Date, Date>> discMats;
  vector<triplet<Idx, Date, Date>> liborMats;
};
```

（`CCY` 是字符串或某些枚举的类型定义。）我们根据折扣在货币、开始和结束日期这个 3D 空间中的坐标来识别、指定并索引折扣。不需要扩展 `SimulData`。

这处理了股票、大商品和利率资产，但外汇还需要进一步探索。为了清晰起见，由于需要特殊处理，我们建议将外汇与股票和大商品资产分开，并在 `SimulRequest` 和 `SimulData` 中使用专门的关键字、节点和项目，而不是复用 `spot` 和 `fwd`。访问外汇/本币外汇的关键字是：

```
fx(dom, for, T)
```

其中 `T` 是远期到期日（如果省略，则在解析时解析为 `FixingDate`），这样我们可以访问远期外汇或现货外汇。到目前为止，这与股票/大商品远期非常相似。但我们也可以为非本币的支付开发一种非常方便的语法，并将其构建 `pays` 关键字中：

```
product pays amount on payDate payCcy
```

这当然是语法糖

```
product pays amount * fx(domCcy, payCcy, payDate) on payDate
```
