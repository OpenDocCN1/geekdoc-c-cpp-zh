

有必要对标的证券价格变动的概率分布做出假设。我们首先在一个特别简单的框架中考虑这一点，即二项假设。标的证券的当前价格为 $S_0$。下一期价格只能取两个值，$S_u$ 和 $S_d$。

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_83_0.png)

如果能找到所有可能的未来“状态”，即对所有可能性进行枚举，就可以通过构造人为的“概率”（称为“状态价格概率”）来对证券进行估值，并使用这些概率求出标的证券的人为期望值，然后按无风险利率进行贴现。二项框架特别简单，因为只有两种可能的状态。如果我们找到一种状态的“概率” q，也就同时得到了另一种状态的概率 $(1-q)$。方程 8.1 展示了针对标的证券的这一计算。

$S_0 = e^{-rT}(qS_u + (1-q)S_d)$ (8.1)

现在，基于该标的证券的任何衍生证券都可以使用相同的“概率” q 进行定价。二项期权定价的贡献在于实际计算 q 的值。要进行估值，首先引入常数 u 和 d，它们由 $S_u = uS_0$ 和 $S_d = dS_0$ 隐式定义，从而得到如图 8.1 所示的价格过程。

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_83_1.png)

图 8.1：二项树

并计算人为的“概率” q 如下

$q = \frac{e^r - d}{u - d}$

二项框架下一期看涨期权的价格如公式 8.1 所示，并在 C++ 代码 8.1 中实现。

“状态价格概率” q 是基于无套利机会假设得出的。如果可以交易标的证券和无风险债券，就可以构建这两种资产的投资组合，以精确复制衍生证券的未来收益。由于该投资组合与衍生证券具有相同的未来收益，衍生证券的价格必须等于复制投资组合的成本。通过推导代数表达式，可以得到 q 作为上涨和下跌变动 u 和 d 的函数。

## 练习 8.1。

标的证券的价格遵循二项过程

$C_u = \max(0, S_u - K)$
$C_d = \max(0, S_d - K)$
$C_0 = e^{-r} (q C_u + (1-q) C_d)$
$q = \frac{e^r - d}{u - d}$
$S_u = u S_0$ 和 $S_d = d S_0$ 是下一期标的证券的可能值，$u$ 和 $d$ 是常数，$r$ 是（连续复利）无风险利率，$K$ 是看涨期权行权价。

## 公式 8.1：单期二项看涨期权价格

```
#include <cmath>        // standard mathematical library
#include <algorithm>    // defining the max() operator
using namespace std;

double option_price_call_european_binomial_single_period( const double& S, // spot price
        const double& X, // exercise price
        const double& r, // interest rate (per period)
        const double& u, // up movement
        const double& d){ // down movement
    double p_u = ( exp(r)-d)/(u-d);
    double p_down = 1.0-p_u;
    double c_u = max(0.0,(u*S-X));
    double c_d = max(0.0,(d*S-X));
    double call_price = exp(-r)*(p_u*c_u+p_down*c_d);
    return call_price;
};
```

## C++ 代码 8.1：欧式二项期权，单期

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_84_0.png)

单期看涨期权的收益为

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_84_1.png)

- 1. 展示如何将标的证券头寸与无风险债券头寸相结合，构建一个精确复制看涨期权收益的投资组合。
- 2. 利用此结果，展示公式 8.1 中所示的单期看涨期权定价公式。

## 8.3 多期二项定价

当然，假设下一期只有两种可能的未来状态有些不现实，但如果我们迭代这一假设，并假设每个日期，下一期只有两种可能的结果，而对于这两种结果中的每一种，又有两种新的结果，如下图所示：

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_85_0.png)

再多迭代几次这个想法，不同的终端状态数量会显著增加，我们就能更接近标的证券在终端日期的未来价格的现实分布。需要注意的是，要得到这样的图景，一个关键假设是因子 u 和 d 在每个日期都相同。

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_85_1.png)

在这样的环境下，定价是通过逆向推导进行的，从终端日期开始。在这里，我们知道标的证券的所有可能值。对于每个值，我们计算衍生证券的收益，并找出一期前可能的衍生证券价格集合。基于这些，我们可以再找出再前一期的期权价格，以此类推。沿着树向下推导到根节点，期权价格即为第一个节点的衍生证券价格。

例如，假设我们有两期，并对行权价为 K 的两期看涨期权进行定价。

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_86_0.png)

第一步：求出衍生证券的终端收益

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_86_1.png)

下一步：求出时刻 1 的两种可能看涨期权价格

$C_u = e^{-r}(qC_{uu} + (1-q)C_{ud})$
$C_d = e^{-r}(qC_{ud} + (1-q)C_{dd})$

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_86_2.png)

最后一步：使用时刻 1 的两种可能收益 $C_u$ 和 $C_d$，求出时刻 0 的期权价值

$C_0 = e^{-r}(qC_u + (1-q)C_d)$

因此，二项定价实际上涉及在二项树中“向后推导”，编程因此涉及遍历此类树的高效方式。描述此类树的明显数据结构在 C++ 代码 8.2 中所示，其中每个节点的值是通过计算到达该特定节点所使用的上涨和下跌步数来计算的。

## 练习 8.2。

```
#include <vector>
#include <cmath>
using namespace std;
vector< vector<double> > binomial_tree(const double& S0,
                                       const double& u,
                                       const double& d,
                                       const int& no_steps){
  vector< vector<double> > tree;
  for (int i=1;i<=no_steps;++i){
    vector<double> S(i);
    for (int j=0;j<i;++j){
      S[j] = S0*pow(u,j)*pow(d,i-j-1);
    }
    tree.push_back(S);
  }
  return tree;
};
```

## C++ 代码 8.2：构建二项树

从计算效率来看，C++ 代码 8.2 的方法并不最优，因为它需要大量调用 pow() 函数。更高效的方法是从前一节点进行乘法来构建树，例如第 j 个向量是第 j-1 个向量乘以 u，然后通过将最低元素乘以 d 来添加一个额外节点。

- 1. 实现这种替代的树构建过程。

基于 C++ 代码 8.2 中所示的三角数组结构对衍生品价格进行递归计算是最自然的方法，但基于对二项树结构的理解，通过一些巧妙的方法，我们可以使用 C++ 代码 8.3 中所示的更高效算法。请注意，这里我们只使用一个 vector<double>，而不是上面构建的三角数组。

## 示例

设 S = 100.0, K = 100.0, r = 0.025, u = 1.05 和 d = 1/u。

- 1. 对单期和两期欧洲式看涨期权进行定价。

```
C++ program
double S = 100.0; double K = 100.0; double r = 0.025;
double u = 1.05; double d = 1/u;
cout << " one period european call = "
     << option_price_european_binomial_single_period(S,K,r,u,d) << endl;
int no_periods = 2;
cout << " two period european call = "
     << option_price_european_binomial_multi_period_given_ud(S,K,r,u,d,no_periods) << endl;
Output from C++ program:
one period european call = 3.64342
two period european call = 5.44255
```

## 练习 8.3。

实现单期和多期二项看跌期权定价。

## 延伸阅读

单期二项模型的推导见例如 Bossaerts 和 Ødegaard (2001)、Hull (2011) 或 McDonald (2013)。

