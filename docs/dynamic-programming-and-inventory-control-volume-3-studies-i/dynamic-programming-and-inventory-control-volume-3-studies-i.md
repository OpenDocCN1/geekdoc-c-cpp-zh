# 动态规划与库存控制：第3卷 概率、优化与统计研究

本页故意留空

# 绪论

本书的目的是提出动态规划与马尔可夫决策过程的统一理论及其在运筹学与运营管理主要领域——库存控制中的应用。我们将在离散时间和连续时间中发展模型。在连续时间中，情况的多样性非常大。我们不会涵盖所有情况，而是专注于与库存控制相关的模型。在离散时间中，我们将主要关注无限时域模型。这也是动态规划的贝尔曼方程真正成为函数方程的情况，其解称为值函数。在有限时域下，动态规划导致递推关系，这是一种更简单的情况。当然，有限时域问题也可以被视为无限时域问题的近似，这将在我们的展示中使用。当时域无限时，折扣起着至关重要的作用。一个重要问题是当折扣因子趋于1时值函数的行为。值函数也趋于无穷大，但平均成本函数变得有意义。这种发展被称为遍历理论，其一个有趣的方面是，当解存在时，解可能比折扣小于1的情况更简单。然而，理论更复杂。这种简单性与问题变为静态而非动态的事实有关。复杂性源于这个静态问题是一种平均。平均过程并不平凡，可能并不直观。

另一个重要问题是冲动控制与连续控制之间的区别。在连续时间中，这种区别尤其容易理解。冲动控制会导致状态的瞬时跳跃，而连续控制只能导致状态的连续演化。在实践中，这种现象与固定成本相关，即仅仅因为做出决策而产生的成本，无论决策的影响如何。在离散时间中，这种区别在原则上消失，因为时间在构造上不是连续的。然而，固定成本仍然存在。其结果是，在离散时间中，冲动控制的适当表述仍然有意义且有用。确实，在离散时间中，通常假设决策的结果在期末实现，而决策是在期初做出的。离散时间中的冲动控制意味着结果也在期初实现，因此是瞬时的。我们还将在冲动控制的背景下考虑遍历控制，并证明一些目前在实践中使用的简单规则。

在第2章中，我们将介绍一些经典静态问题，这些问题是库存控制中感兴趣的动态模型的前提。所谓静态，是指我们需要求解一个普通优化问题。决策不依赖于时间。当只考虑一个时期时，会出现此类模型，



或当人们假设周期以周期方式重现时。我们将稍后重新审视周期模型，以检查其在静态情况下的最优性。

尽管这些领域已有大量文献，但我们认为本书存在重大差异。它并非控制理论与动态规划的通用教材，其含义在于系统动力学主要局限于库存模型。另一方面，对于这些模型，本书力求尽可能全面。然而，我们并未在离散时间中发展有限时域模型，因为现有文献已对其进行了大量描述。另一方面，遍历控制问题被详细讨论，并提供了概率证明和解析证明。如前所述，该模型在实践中极其重要，因为它类似于静态优化问题。然而，就严谨处理而言，文献有限。本工作中发展的技术可以扩展到更复杂的模型，涵盖库存控制的其他方面。从本书内容可以提出许多有趣的研究课题。

本书受益于我在德克萨斯大学达拉斯分校的教学，以及与德克萨斯大学达拉斯分校和香港理工大学同事的交流，同时也大大受益于亚洲大学世界级大学计划的支持。得益于此支持，得以专注于研究和撰写本书。最后，我要衷心感谢Laser Yuan对我的LYX排版所做的改进，以及IOS Press出版本书。

# 静态问题

## 2.1. 新闻贩子问题

这是该领域最古老的问题。它说明了一个单周期问题。新闻贩子不能将当天的报纸留到第二天。他订购q并面临随机需求D。这是一个具有累积分布函数（c.d.f，cumulative distribution function）F(x)的随机变量。我们记 \(\bar{F}(x) = 1 - F(x)\)，\(f(x) = \frac{dF}{dx}(x)\)。当订购量q大于需求时，他面临剩余成本；当订购量小于需求时，他面临短缺成本。因此，他的目标函数是

(2.1.1) \(J(q) = hE(q - D)^+ + pE(D - q)^+,\)

其中E表示数学期望。

最优q显然是以下方程的解

(2.1.2) \(F(\bar{q}) = \frac{p}{h+p}.\)

此外，假设新闻贩子以单位成本c购买报纸，则函数J(q)需改为

(2.1.3) \(J(q) = cq + hE(q - D)^+ + pE(D - q)^+.\)

我们需要假设p > c，否则没有购买动机（此时函数J(q)是递增的）。最优订单是以下方程的解

(2.1.4) \(F(\bar{q}) = \frac{p - c}{h + p}.\)

如果成本是K + cq，表示固定成本（与数量无关）和变量成本（与数量成正比）之和，只要决定订购，最优决策就不会改变。在这种情况下，金额K是无论如何都要支付的费用。然而，由于我们有不订购的可能性，此时成本为hED，新闻贩子必须比较hED与K + J(q)。如果第二个数高于第一个，则他选择不订购任何东西。

在公式(2.1.1)中，我们隐含地假设在一天结束时（更一般地说，在周期结束时）将需求D与订购量q进行比较。我们可以假设总需求D在整个周期内以均匀速率实现，从而获得更准确的处理。如果周期长度为1，则平均剩余量为 \(\int_0^1 (q - Dt)^+ dt\)，短缺量为 \(\int_0^1 (Dt - q)^+ dt\)，因此目标函数变为

(2.1.5) \(J(q) = hE \int_0^1 (q - Dt)^+ dt + pE \int_0^1 (Dt - q)^+ dt,\)

因此

\(J(q) = h \int_0^1 t F\left(\frac{q}{t}\right) dt + p \int_0^1 t F\left(\frac{q}{t}\right) dt\)

最优数量由以下给出

(2.1.6) \(F(\hat{q}) + \hat{q} \int_{\hat{q}}^{\infty} \frac{f(u)}{u} du = \frac{p}{h+p}.\)

很容易检查方程(2.1.6)有唯一解。

## 2.2. EOQ模型

### 2.2.1. 基础EOQ模型。

EOQ代表经济订货量。这也是一个著名且非常古老的模型。它由F.W. Harris，[23]和R.H. Wilson，[40]提出。该模型是确定性的。事实上，该模型不是静态的，而是动态的，且时间是连续的。当我们处理动态模型时，将重新审视它。然而，可以通过一个简单的周期性论证将其归约为静态模型。需求以每单位时间速率\(\lambda\)均匀（且持续地）实现。我们禁止短缺的可能性。当库存耗尽时，我们订购数量q。假设我们在时间0时以q开始，然后在时间T时，使得

\(q = \lambda T;\)

库存耗尽。显然，T可以作为一个周期。我们希望最小化周期内的平均成本。

周期内的库存水平由以下给出

\(y(t) = q - t\lambda.\)

购买q的成本由K + cq给出，其中K代表固定成本，c代表变量成本。存在与每单位时间持有数量成正比的存储成本。因此，在周期内，存储成本由以下给出

\(\int_0^T hy(t)dt = h \int_0^T (q - t\lambda)dt = \frac{hqT}{2}.\)

周期内的总成本可以写为

\(K + cq + \frac{hqT}{2} = T(c\lambda + C(q)),\)

与

\(C(q) = K \frac{\lambda}{q} + \frac{hq}{2}.\)

因此最优订单是（EOQ公式）

\(\hat{q} = \sqrt{\frac{2K\lambda}{h}}.\)

注意

\(K \frac{\lambda}{\hat{q}} = \frac{h\hat{q}}{2},\)

以及

\(C(\hat{q}) = h\hat{q}.\)

回顾每个周期的平均成本还包含常数\(\lambda c\)，因此最优平均成本为

\(h\hat{q} + \lambda c.\)

还要注意，q/2是平均库存，每单位时间的需求是\(\lambda\)；这意味着

\(\frac{\lambda}{\frac{q}{2}} = \text{库存周转率},\)

这是一个重要的管理指标。我们看到最优周转率是 \(\sqrt{\frac{2\lambda h}{K}}\)。如果降低成本K，则可以提高这一周转率。下一个问题是：我们是否确定遵循EOQ公式行动是最优的？

我们是否确定采用EOQ公式给出的周期性决策是最优的？虽然这看起来自然且长期使用，但证明它是有价值的。

此外，周期性决策没有考虑利率的可能性。如果对成本流进行折现，会有哪些变化？要正确回答这个问题，需要冲动控制的工具，这将在后面描述。

### 2.2.2. 变换EOQ公式。

现在假设没有即时交付。相反，交付以连续速率r提供。

由于没有短缺的可能性，必须有 \(r \ge \lambda\)。库存的演变由以下公式给出

\(y(t) = (r - \lambda)t, \forall t \le T_0 = \frac{q}{r},\)

\(y(t) = q - \lambda t, T_0 < t \le T = \frac{q}{\lambda}.\)

然后可以检查

\(\hat{q} = \sqrt{\frac{2K\lambda r}{h(r - \lambda)}}.\)

当 \(r = \lambda\) 时，该公式趋于 \(\infty\)。必须将其理解为：将在需求水平上进行连续交付。库存保持为0，每单位时间成本等于 \(c\lambda\)。在这种情况下没有优化。

## 2.3. 价格考虑

我们在这里认为，购买产品的成本由固定成本K、变量成本cq组成，这些是公司的内部成本。此外，每单位产品有一个购买价格，可能取决于购买量，例如，当可能有折扣时。我们将用\(\alpha\)表示该价格。我们还假设存储成本h通过关系 \(h = i\alpha\) 与\(\alpha\)相关联。

因此，在一个周期中，当价格固定时，对于订单q，我们得到以下成本

\(K + qc + c + i\alpha \frac{qT}{2}.\)

每单位时间我们得到 \(C(q) + \lambda c\)，其中

\(C(q) = \frac{K\lambda}{q} + (i\frac{q}{2} + \lambda)\alpha.\)

在此框架中，\(\alpha\)只是变量成本c的额外成本。我们现在研究折扣的影响。





### 2.3.1. 统一价格折扣的EOQ公式

假设我们引入数量折扣的可能性。我们假设产品的价格为 $\alpha_j$，如果订购数量落在区间 $[q_{j-1}, q_j)$ 内。那么我们有公式

$$
C(q) = \frac{K\lambda}{q} + \left(\frac{i}{2}q + \lambda\right) \sum_j \alpha_j \mathbb{1}_{\{q_{j-1} \le q < q_j\}}.
$$

我们注意到成本函数不是连续的。尽管如此，我们具有以下性质：

#### 练习 2.1. $C(q)$ 的最小值可以得到。找出它。

### 2.3.2. 递进折扣的EOQ公式

让我们考虑一个将导致连续函数的扩展，参见 V. Giard [20]。假设，如果 $q_{j-1} \le q < q_j$，则只有部分 $q - q_{j-1}$ 按价格 $\alpha_j$ 支付。设 $A_j$ 为采购数量 $q_j$ 的成本，则显然

$$
A_j = A_{j-1} + (q_j - q_{j-1})\alpha_j, \quad A_0 = 0,
$$

并且与之前一样的 $q$，全部采购成本为 $A_{j-1} + (q - q_{j-1})\alpha_j$，平均单价为 $\frac{A_{j-1} + (q - q_{j-1})\alpha_j}{q} = \alpha_j + \frac{B_j}{q}$，其中

$$
B_j = A_{j-1} - q_{j-1}\alpha_j,
$$

因此

$$
B_{j+1} = \sum_{h=1}^j q_h(\alpha_h - \alpha_{h+1}), \quad B_1 = 0,
$$

因此，我们有

$$
C(q) = \frac{K\lambda}{q} + \left(\frac{i}{2}q + \lambda\right) \sum_j \left(\alpha_j + \frac{B_j}{q}\right) \mathbb{1}_{\{q_{j-1} \le q < q_j\}}.
$$

该函数是连续的，因为

$$
\alpha_j + \frac{B_j}{q_j} = \alpha_{j+1} + \frac{B_{j+1}}{q_j}.
$$

如果 $j$ 从 1 运行到 $J$，则我们采用约定 $q_{J+1} = +\infty$。此外，$\alpha_{J+1}$ 是获取大于 $q_J$ 数量的价格。所以

$$
C(q) = \frac{K\lambda}{q} + \left(\frac{i}{2}q + \lambda\right) \sum_{j=1}^{J+1} \left(\alpha_j + \frac{B_j}{q}\right) \mathbb{1}_{\{q_{j-1} \le q < q_j\}}.
$$

#### 练习 2.2. 验证

$$
C(q) = \frac{K\lambda}{q} + \frac{i\alpha_1 q}{2} + \left(\frac{i}{2} + \frac{\lambda}{q}\right) \sum_{j=1}^J (\alpha_{j+1} - \alpha_j)(q - q_j)^+,
$$

因此 $C(q)$ 是分段可微的，并且

$$
C'(q) = -\frac{K\lambda}{q^2} + \frac{i\alpha_1}{2} - \frac{\lambda}{q^2} \sum_{j=1}^J (\alpha_{j+1} - \alpha_j)(q - q_j)^+ + \left(\frac{i}{2} + \frac{\lambda}{q}\right) \sum_{j=1}^J (\alpha_{j+1} - \alpha_j) \mathbb{1}_{q > q_j}
$$

#### 练习 2.3. 对于 $J = 1$，求 $\hat{q}$。

### 2.4. 稀缺资源下的多种产品

假设我们管理多种产品的库存，受全局约束（预算、存储可能性）。我们可以明确地制定问题：最小化

$$
\sum_j C_j(q_j) \qquad \sum_j a_j q_j \le A,
$$

并且，每当每个单独成本由EOQ公式得到时

$$
C_j(q_j) = \frac{K_j \lambda_j}{q_j} + h_j \frac{q_j}{2}.
$$

我们可以引入拉格朗日乘数 \(\gamma\) 并得到系统

$$
\hat{q}_j(\gamma) = \sqrt{\frac{2 K_j \lambda_j}{h_j + 2 \gamma a_j}},
$$

并且 \(\gamma = \hat{\gamma} > 0$ 是唯一解

$$
\sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j + 2 \gamma a_j}} = A.
$$

注意，如果 \(A \ge \sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j}}$，则解只是无约束问题的解（约束不严格）。因此我们可以假设

$$
\sum_j a_j \sqrt{\frac{2 K_j \lambda_j}{h_j}} > A,
$$

并且 \(\gamma$ 是唯一确定的。

我们注意到一个简单的情况，其中 \(\gamma$ 可以显式计算。假设我们有

$$
h_j = i \alpha_j, a_j = k \alpha_j,
$$

其中 \(\alpha_j$ 是产品 \(j$ 的采购价格。当 \(h_j$ 可以解释为机会成本且 \(i$ 是利率，并且约束在于库存总价值时，会出现这种情况。

#### 练习 2.4. 证明

$$
\hat{\gamma} = \frac{k}{2 A^2} \left( \sum_j \sqrt{2 K_j \lambda_j \alpha_j} \right)^2 - \frac{i}{2k}.
$$

### 2.5. 多种产品的连续生产

我们考虑使用相同制造系统连续生产多种产品的情况。设 \(r_j$ 为产品 \(j$ 的单位时间生产率。我们回顾 \(r_j > \lambda_j$。由于制造系统相同，我们必须有

$$
\sum_j \frac{r_j}{\lambda_j} < 1.
$$

我们将为所有产品强制一个共同周期 \( T$，例如，每年有相同数量的订单 \( \frac{1}{T}$。这在长期内可能不是最优的，但它大大简化了分析。

产品 \( j$ 的生产（订单）为 \( q_j = T \lambda_j$。因此我们使用 \( T$ 作为决策变量，而不再是订单水平。产品 \( j$ 的EOQ公式（用 \( T$ 表示）导致

$$
C_j(T) = \frac{K_j}{T} + \frac{h_j}{2} \lambda_j T \left( 1 - \frac{\lambda_j}{r_j} \right),
$$

并且我们必须最小化 \( \sum_j C_j(T)$。

#### 练习 2.5. 证明最优 \( T = \hat{T} \) 为

$$
\hat{T} = \sqrt{\frac{2 \sum_j K_j}{\sum_j h_j \lambda_j \left( 1 - \frac{\lambda_j}{r_j} \right)}}.
$$

### 2.6. 提前期

我们之前考虑过交付即时或以单位时间某个速率进行的情况。提前期的情况是获取订单需要一定延迟（这种延迟称为提前期）。我们将研究提前期对EOQ模型的影响。

#### 2.6.1. 不允许缺货

如果 \( L$ 是提前期，订单 \( q$ 将在下单后 \( L$ 个时间单位交付。如果不允许缺货，并且在提前期内不下任何订单，则我们必须有约束

$$
q \ge \lambda L,
$$

否则，在提前期内我们会损失库存。过一段时间后库存将变为负数，这是不允许的。在一个周期（两次交付之间的期间）长度为 \( \frac{q}{\lambda}$ 时，平均成本仍为

$$
C(q) = K \frac{\lambda}{q} + \frac{hq}{2}.
$$

EOQ问题变为

$$
\min_{q \ge \lambda L} C(q).
$$

特别是，如果由EOQ公式定义的 \( \hat{q}$ 满足约束，那么无论 \( L$ 的值如何，它都是最优值。但是，如果订单不再在库存为0时下单，而是在库存为 \( \lambda L$ 时下单。如果 \( \hat{q}$ 不满足约束，那么最优订单只是 \( \lambda L$，因为根据凸性，\( C(q)$ 对于 \( q \ge \lambda L$ 将是递增的。在这种情况下，在交付时下单，此时的库存也是 \( \lambda L$。

#### 2.6.2. 积压的可能性

我们现在描述一个具有提前期和积压可能性的库存模型，参见 [41]。积压意味着负库存是可能的。通过负库存，指的是无法满足的需求被记录下来。它可以稍后满足，但自然会有罚金。需求是连续的，单位时间速率为 \( \lambda$。成本结构如下：存在固定订购成本 \( K$ 和可变订购成本 \( c$（每单位订购数量）；每单位数量的持有成本 \( h$，以及每单位积压数量的积压罚金 \( p$。

下单和交付之间存在提前期 \( L$。在提前期内没有订单。我们已经看到，在没有积压的情况下，下单时的库存必然是 \( s = \lambda L$。在这里，由于积压是可能的，这种关系不一定成立。因此，\( s$ 是像订购数量 \( q$ 这样的决策变量。所以当前问题是一个带有两个变量 \( s, q$ 的优化问题。

由于提前期内没有订单，交付前的库存是 \( \nu = s - \lambda L$。交付后立即，它是 \( s - \lambda L + q$。为了避免订单累积的病态情况，我们将施加约束 \( q - \lambda L > 0$。

库存的最低值是 \( \nu$。如果有积压，这个数必然是负数。将 \( \nu, q$ 对作为决策变量很方便。下单时的库存值只是 \( s = \nu + q$。

一个周期是两次交付之间的期间 \( T$。我们计算周期内的各种成本（持有和积压），回顾在交付完成前没有新订单。我们可以在下单点取时间原点。因此，第一次交付发生在 \( L$，覆盖一个周期的期间是 \( (L, T+L)$。在时间 \( L$ 时，库存是 \( q - s - \lambda L = q + \nu$。然后以速率 \( \lambda$ 耗尽，直到下一次交付，此时它变为 \( s - \lambda L = \nu$。

因此我们有 \( q = \lambda T$。注意，对 \( q$ 的条件强制 \( T > L$。周期内的持有成本由公式给出

$$
h \int_L^{T+L} (q + \nu - \lambda(t - L))^+ dt = h \frac{((q+\nu)^+)^2}{2\lambda} - h \frac{((\nu)^+)^2}{2\lambda}.
$$

同样，积压成本由以下公式给出

$$
p \int_L^{T+L} (q + \nu - \lambda(t - L))^- dt = -p \frac{((q+\nu)^-)^2}{2\lambda} + p \frac{((\nu)^-)^2}{2\lambda}.
$$

订购成本是 \( K + cq$。平均成本通过除以周期持续时间 \( T$ 得到。

汇总结果，我们得到以下平均成本

$$
C(\nu, q) = c\lambda + \frac{\lambda K}{q} + h \left[ \frac{((q+\nu)^+)^2}{2q} - \frac{(\nu^+)^2}{2q} \right] + p \left[ \frac{(\nu^-)^2}{2q} - \frac{((q+\nu)^-)^2}{2q} \right],
$$

受约束 \( q > \lambda L$。函数 \( C(\nu, q)$ 在 \( [0, +\infty[$ 上显然在 \( \nu$ 中是递增的，因此我们可以假设 \( \nu \le 0$。

因此 \( C(\nu, q)$ 由以下公式给出

$$
C(\nu, q) = c\lambda + \frac{\lambda K}{q} + h \frac{((q+\nu)^+)^2}{2q} + p \left[ \frac{\nu^2}{2q} - \frac{((q+\nu)^-)^2}{2q} \right].
$$

对于 \( \nu \le -q$，函数在 \( \nu$ 中是递减的。其最小值在 \( \nu = -q$ 处达到，此时

$$
C(-q, q) = c\lambda + \frac{\lambda K}{q} + p \frac{q}{2}.
$$





当 \(\nu + q \ge 0\) 时，我们有

\(C(\nu, q) = c\lambda + \frac{\lambda K}{q} + h\frac{(q+\nu)^2}{2q} + p\frac{\nu^2}{2q}.\)

该函数在 \(\nu\) 处取得最小值，此时为

\(\nu(q) = -(1-\varpi)q, \quad \varpi = \frac{p}{h+p}.\)

可以看出，一定程度的积压是可以接受的。如果 \(p = \infty\)，则得到 \(\nu(q) = 0\)。这是合理的，因为积压的惩罚是无限的，因此禁止积压。

关于成本，我们有

\(C(\nu(q), q) = c\lambda + \frac{\lambda K}{q} + [h\varpi^2 + p(1-\varpi)^2]\frac{q}{2}.\)

注意到

\(h\varpi^2 + p(1-\varpi)^2 = \frac{hp}{h+p} = h\varpi < p,\)

我们可以断言

\(\min_{\nu} C(\nu, q) = C(\nu(q), q) = c\lambda + \frac{\lambda K}{q} + h\varpi\frac{q}{2}.\)

接下来需要对 \(q > \lambda L\) 的 \(q\) 最小化 \(C(\nu(q), q)\)。结果立即得出

\(\hat{q} = \max \left\{ \lambda L, \sqrt{\frac{2K\lambda}{h\varpi}} \right\},\)

并且

\(\min_{\{\nu, q > \lambda L\}} C(\nu, q) = c\lambda + \begin{cases} \sqrt{2K\lambda h\varpi}, & \text{如果 } L \le \sqrt{\frac{2K}{h\lambda\varpi}} \\ \frac{K}{L} + \frac{hL\lambda\varpi}{2}, & \text{如果 } L \ge \sqrt{\frac{2K}{h\lambda\varpi}} \end{cases}\)

当 \(L = 0\) 且 \(p = \infty\) 时（这意味着 \(\varpi = 1\)），我们恢复了 EOQ 公式。

#### 备注。

考虑满足以下条件的任意一对 \(\nu, q\)

\(\nu \le 0, q \ge \lambda L, s = \nu + \lambda L > 0.\)

特别是，对于一对 \(\nu(q), q\)（其中 \(\nu(q)\) 如前所述给出，而 \(q\) 为任意值），这些条件均满足。周期时长为 \(T\)，其中 \(q = \lambda T\)，且 \(T > L\)。让我们像上面一样，将下订单时刻作为时间原点，并考虑从 \(L\) 开始的一个周期。在周期 \(L, T + L\) 期间，库存从 \(\nu + q\) 下降到 \(\nu\)。它在时刻 \(L + T + \frac{\nu}{\lambda}\) 时消失，并保持为负值直到 \(L + T\)。

因此，平均积压量由以下公式给出

\(\frac{1}{T} \int_{L+T+\frac{\nu}{\lambda}}^{L+T} \lambda \left( t - (L + T + \frac{\nu}{\lambda}) \right) dt = \frac{\nu^2}{2T\lambda}.\)

在此积压期间，直到交付的等待时间为 \(L + T - t\)，当 \(t\) 从 \(L + T + \frac{\nu}{\lambda}\) 运行到 \(L + T\) 时，因此平均等待时间为

\(\frac{1}{T} \int_{L+T+\frac{\nu}{\lambda}}^{L+T} (L + T - t) dt = \frac{\nu^2}{2T\lambda^2}.\)

因此我们有

\(\text{平均积压量} = \lambda \text{ 平均等待时间}.\)

这等同于著名的 Little 法则，如果我们考虑在队列中等待的客户。积压量类似于队列中的客户数量，直到交付的等待时间类似于客户的等待时间。

### 2.7. 随机需求率：未满足的需求丢失

我们现在转向需求率 \(\lambda\) 为随机的情况。决策定义如下：当库存低于 \(s > 0\) 时，我们订购数量 \(q\)。我们假设交付存在前置时间 \(L\)，但由于 \(\lambda\) 是随机的，我们不能使用 \(\nu = s - \lambda L\)。因此，我们将一对 \(s, q\) 作为决策变量。与之前的确定性积压模型不同，我们将假设未得到满足的需求会丢失。这与新闻商模型类似。当然，当这种情况发生时会有惩罚。事实上，这一假设将大大简化处理。为了理解原因，我们转向周期。将周期定义为库存为 \(s\) 的两种情况之间的时间长度。我们仍用 \(T\) 表示这个时间长度。它现在是一个随机变量。因此，验证约束 \(T > L\) 不再清楚。我们将检查，当我们假设 \(g > s\) 时，这是可能的，这要归功于我们不允许积压的假设。

交付时刻之前的库存为 \((s - \lambda L)^+\)，交付时刻之后为 \(q + (s - \lambda L)^+\)。如果 \(T > L\)，在长度为 \(T - L\) 的时间间隔内，需求为 \(\lambda(T - L)\)，库存下降量为 \(q + (s - \lambda L)^+ - s\)。由此可得

\(\lambda T = q + (s - \lambda L)^+ > \lambda L,\)

由 \(s\) 满足的条件可得。问题是最小化表示为 \(C(s, q)\) 的预期平均成本。

#### 练习 2.6. 验证公式

\(C(s, q) = E \frac{1}{2[q + (s - \lambda L)^-]} [h(q^2 + 2q(s - \lambda L)^+) + p((s - L\lambda)^-)^2 + 2\lambda(K + cq)].\)

本页故意留空

# 第 3 章

# 马尔可夫链

本章介绍马尔可夫链的主要结果，这些结果用于建模状态演化。本章不对演化进行控制。

## 3.1. 记号

设 \( X \) 为一个度量空间。我们将限制于 \( R^d \) 或有限或可数集合之一。\( X \) 被称为 *状态空间*。如果 \( X = R^d \)，我们考虑 Borel \(\sigma\)-代数 \(\mathcal{X}\)；如果 \( X \) 是有限或可数的，则考虑 \( X \) 的所有子集组成的 \(\sigma\)-代数。转移概率 \(\pi(x, \Gamma)\) 定义在 \( X \times \mathcal{X} \) 上，并满足以下条件

(3.1.1)
\(\forall x, \pi(x, .) \text{ 是 } \mathcal{X} \text{ 上的概率},\)
\(\forall \Gamma \text{ 固定，}\pi(., \Gamma) \text{ 是 Borel 函数。}\)

我们定义

\(\Omega = X^N,\)

其中 \( N \) 表示正整数集合。因此 \(\Omega\) 的一个元素写作

\(\omega = (\omega_1, \cdots, \omega_n, \cdots).\)

规范随机过程（离散时间）由以下公式定义

\(y_n(\omega) = \omega_n.\)

我们将与 \(\Omega\) 关联的 \(\sigma\)-代数 \(\mathcal{A} = \mathcal{X}^N\) 定义为由以下矩形生成的代数

\(A_1 \times \cdots \times A_n, \forall n\)

\(A_1 \cdots A_n \in \mathcal{X}.\)

鉴于初始状态 \( y_1 \) 的概率分布，我们将在 \(\mathcal{X}\) 上定义 \( m \)，它将是与 \( m, \pi \) 关联的轨迹 \( y_n \) 的概率分布。

轨迹的概率定律源自 \(\Omega, \mathcal{A}\) 上的一个概率 \( P \)，使得对于任何测试函数 \(\phi(x_1, \cdots, x_n)\) 和任何 \( n \)，我们有

(3.1.2) \( E\phi(y_1, \cdots, y_n)\)
\( = \int dm(x_1) \int \pi(x_1, dx_2) \int \cdots \int \pi(x_{n-1}, dx_n) \phi(x_1, \cdots, x_n).\)

可以证明可以定义 \( P \) 使得关系 (3.1.2) 成立（Kolmogorov 理论，参见例如 M. Loeve [31]）。

## 3.2. 查普曼-科尔莫戈罗夫方程

### 3.2.1. 函数空间设置。

设 \( B \) 为从 \( X \) 到 \( R \) 的有界可测函数组成的 Banach 空间，配备范数

\(||f|| = \sup_x |f(x)|.\)

我们通过公式定义算子 \(\Phi \in \mathcal{L}(B; B)\)

\(\Phi f(x) = \int_X f(y)\pi(x, dy).\)

显然有

\(||\Phi|| \le 1\)

### 练习 3.1. 证明

(3.2.1) \( E[f(y_{n+1})|\mathcal{Y}^n] = \Phi f(y_n), \)

其中

\(\mathcal{Y}^n = \sigma(y_1, \cdots, y_n).\)

### 练习 3.2. 证明

(3.2.2) \( E[f(y_{n+1})|y_1] = \Phi^n f(y_1). \)

当 \(m = \delta_x\) 时，我们使用记法

\( E[f(y_{n+1})|y_1 = x] = \Phi^n f(x) = \int P(x, n, d\eta) f(\eta). \)

并且 \(P(x, n, d\eta)\) 表示在 \(y_1 = x\) 条件下 \(y_n\) 的概率分布。

设 \(\Gamma\) 为 \(X\) 的 Borel 子集，我们写

\(P(x, n, \Gamma) = \int P(x, n, d\eta) \mathbb{I}_\Gamma(\eta),\)

那么我们有查普曼-科尔莫戈罗夫方程

\(P(x, n + m, \Gamma) = \int P(x, n, d\eta) P(\eta, m, \Gamma),\)

并且还有

(3.2.3) \( E[\mathbb{I}_\Gamma(y_{k+n})|\mathcal{Y}^k] = P(y_k, n, \Gamma). \)

### 3.2.2. 线性增长函数。

此处我们考虑 \(X = R^d\)。对于库存控制的应用，将算子 \(\Phi\) 扩展到不仅有界而且具有线性增长的函数非常重要。设 \(B_1\) 为从 \(R^d\) 到 \(R\) 的具有线性增长的可测函数组成的 Banach 空间，配备范数

\(||f||_1 = \sup_x \left| \frac{f(x)}{1 + |x|} \right|.\)

算子 \(\Phi\) 不会自动在 \(B_1\) 上定义。首先假设 \(f\) 为正，则可以考虑序列 \(f_M = f \wedge M\) 并考虑序列 \(\Phi f_M\)。这是一个递增序列。因此它有一个极限，可能为 \(\infty\)。我们将假设

\(\frac{\Phi f_M(x)}{1 + |x|} \text{ 有界},\)



所以极限是有限的并定义了 \(\Phi f(x)\)。当 \(f\) 不是正的时，我们写 \(f = f^+ - f^-\) 并且由线性性

\(\Phi f(x) = \Phi f^+(x) - \Phi f^-(x).\)

算子 \(\Phi \in \mathcal{L}(B_1; B_1)\) 但我们不具有性质 \(||\Phi||_1 \le 1\)。这使事情复杂化，正如我们将看到的。

## 3.3. 停止时间

设 \(\nu\) 为相对于 \(\mathcal{Y}^n\) 的停止时间。由此，按定义

\(\{\nu \le k\} \subset \mathcal{Y}^k, \forall k.\)

我们回顾 \(\sigma\)-代数 \(\mathcal{Y}^\nu\) 的定义

\(A \in \mathcal{Y}^\nu \Leftrightarrow A \cap \{\nu \le k\} \subset \mathcal{Y}^k, \forall k.\)

我们接着陈述

**引理 3.1.** 我们有关系

(3.3.1) \(E[\Pi_t(y_{t+n})|\mathcal{Y}^\nu] = P(y_\nu, n, \Gamma).\)

**练习 3.3.** 证明关系 (3.3.1)。

在停止时间中，我们将考虑出口时间

\(\tau = \inf\{n : y_n \notin \mathcal{O}\},\)

\(\mathcal{O}\): \(X\) 的 Borel 子集。

## 3.4. 分析问题的解

### 3.4.1. 柯西问题。

我们有兴趣给出一些分析问题的概率解释。我们从柯西问题开始。设 \(f, g \in B\)。我们考虑由关系定义的函数序列 \(u^n \in B\)

(3.4.1) \(u^N = g, \quad u^n = f + \Phi u^{n+1},\)

然后我们有解释

(3.4.2) \(u^1(x) = E\left[\sum_{n=1}^{N-1} f(y_n) + g(y_N)|y_1 = x\right].\)

**练习 3.4.** 证明关系 (3.4.2)。

接下来我们考虑功能方程，对于 \(\alpha < 1\)

(3.4.3) \(u = f + \alpha \Phi u,\)

具有解释

(3.4.4) \(u(x) = E\left[\sum_{n=1}^{\infty} \alpha^{n-1} f(y_n)|y_1 = x\right].\)

一个重要问题是当 \(f\) 具有线性增长时求解方程 (3.4.3)。我们可以陈述以下结果

**命题 3.1.** 假设

(3.4.5) $$\sum_{n=1}^\infty \alpha^{n-1} \Phi^{n-1} |f|(x) < \infty, \forall x,$$

那么

(3.4.6) $$u(x) = \sum_{n=1}^\infty \alpha^{n-1} \Phi^{n-1} f(x),$$

是 (3.4.3) 的唯一解，使得

(3.4.7) $$\alpha^n \Phi^n u(x) \to 0, \text{ as } n \to \infty.$$

**证明.** 只需假设 $f > 0$。那么条件 (3.4.5) 是必要且充分的，以断言由 (3.4.6) 定义的函数 $u(x)$ 是良定义的。让我们首先表明它是一个解。考虑截断级数

$$u_n(x) = \sum_{j=1}^n \alpha^{j-1} \Phi^{j-1} f(x),$$

它满足递归

$$u_{n+1}(x) = f(x) + \alpha \Phi u_n(x), \quad u_1(x) = f(x),$$

那么我们有 $u_n(x) \le u(x)$ 并且 $u_n(x)$ 是单调递增的。如果 $u_*(x)$ 表示极限，我们注意到由勒贝格定理 $\Phi u_n(x)$ 也收敛到 $\Phi u_*(x)$。因此 $u_*$ 是 (3.4.3) 的解。但是 $u_*(x) = u(x)$。因此 $u$ 是一个解。现在对于任何解，我们通过迭代有

$$u(x) = u_n(x) + \alpha^n \Phi^n u(x),$$

因此如果 $u$ 是 $u_n$ 的极限，必然满足条件 (3.4.7)。反之，任何满足该条件的解都与 $u_n$ 的极限重合。证明完成。

### 3.4.2. 狄利克雷问题。

现在设 \(\mathcal{O}\) 为 \(X\) 的 Borel 子集。我们记 \(\tau\) 为 \(y_n\) 从 \(\mathcal{O}\) 的出口时间。按定义

$$y_n \in \mathcal{O}, \forall 1 \le n < \tau; y_\tau \in X - \mathcal{O},$$

并且如果 \(y_1 \in X - \mathcal{O}\)，则 \(\tau = 1\)。

我们考虑问题

(3.4.8) $$\begin{cases} u(x) = f(x) + \alpha \Phi u(x), \forall x \in \mathcal{O}, \ u(x) = g(x), \forall x \in X - \mathcal{O}, \end{cases}$$

其中 \(f, g \in B\)。

**定理 3.1.** 问题 (3.4.8) 在 \(B\) 中有且仅有一个解，具有以下解释

(3.4.9) $$u(x) = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} f(y_n) + \alpha^{\tau-1} g(y_\tau) | y_1 = x \right],$$

$$\text{where } \sum_{n=1}^0 = 0.$$

**证明.** 解 \(u\) 的存在性和唯一性源于我们寻找由以下定义的映射 \(T : B \to B\) 的不动点

$$Tw = \begin{cases} f + \alpha \Phi w, \text{ in } \mathcal{O}, \ g \text{ in } X - \mathcal{O}, \end{cases}$$

并且 T 是收缩映射，因为 \(\alpha < 1\)。接下来，我们可以写

\(u(y_n) \mathbf{I}_{n \le \tau - 1} = f(y_n) \mathbf{I}_{n \le \tau - 1} + \Phi u(y_n) \mathbf{I}_{n \le \tau - 1},\)

或

\(u(y_n) \mathbf{I}_{n \le \tau - 1} = f(y_n) \mathbf{I}_{n \le \tau - 1} + E[u(y_{n+1}) | \mathcal{Y}^n] \mathbf{I}_{n \le \tau - 1}.\)

此外 \(\mathbf{I}_{n \le \tau - 1}\) 是 \(\mathcal{Y}^m\) 可测的，因为

\(\mathbf{I}_{n \le \tau - 1} = 1 - \mathbf{I}_{\tau \le n}.\)

因此我们得到

\(\alpha^{n-1} u(y_n) \mathbf{I}_{n \le \tau - 1} = \alpha^{n-1} f(y_n) \mathbf{I}_{n \le \tau - 1} + \alpha^n E[u(y_{n+1}) \mathbf{I}_{n \le \tau - 1} | \mathcal{Y}^n].\)

取期望得到

\(\alpha^{n-1} E[u(y_n) \mathbf{I}_{n \le \tau - 1} | y_1 = x]\)
\(= \alpha^{n-1} E[f(y_n) \mathbf{I}_{n \le \tau - 1} | y_1 = x] + \alpha^n E[u(y_{n+1}) \mathbf{I}_{n \le \tau - 1} | y_1 = x].\)

对 \(n\) 求和这些关系。得到

\(E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} u(y_n) | y_1 = x \right] = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} f(y_n) | y_1 = x \right] + E \left[ \sum_{n=1}^{\tau-1} \alpha^n u(y_{n+1}) | y_1 = x \right].\)

这也意味着

\(E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} u(y_n) | y_1 = x \right] = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} f(y_n) | y_1 = x \right] + E \left[ \sum_{n=2}^{\tau} \alpha^{n-1} u(y_n) | y_1 = x \right].\)

消去项，得到公式 (3.4.9)。

### 3.4.3. 鞅性质。

我们陈述

**定理 3.2.** 对于任何函数 \(u \in B\) 我们有性质

(3.4.10)
\(u(y_n) + \sum_{j=0}^{n-1} (u - \Phi u)(y_j)\)
是一个 \(P, \mathcal{Y}^m\) 鞅

**证明.** 我们需要检查，对于 \(n \ge m\)

\(E \left[ u(y_n) - u(y_m) + \sum_{j=m}^{n-1} (u - \Phi u)(y_j) | \mathcal{Y}^m \right] = 0.\)

回顾

\(E[u(y_{j+1}) | \mathcal{Y}^j] = \Phi u(y_j).\)

由此结果容易得出。

同样可以检查

\(\alpha^n u(y_n) + \sum_{j=0}^{n-1} \alpha^j (u - \alpha \Phi u)(y_j),\)
是一个 \(P, \mathcal{Y}^m\) 鞅。

## 3.5. ergodic 理论

ergodic 理论的目标是研究马尔可夫链在无穷处的行为。如果我们将马尔可夫链视为动态系统，从时间 1 开始，处于状态 \(y_1 = x\)，那么我们感兴趣的是 \(y_n\) 的可能极限。如果系统是确定性的，它将是序列的普通极限，如果存在的话。由于 \(y_n\) 是随机的，我们更多地从 \(y_n\) 的概率分布的极限来思考，这意味着 \(P(x, n, \Gamma)\) 的极限。如果这个极限不仅存在，而且还独立于 \(x\)，我们就说具有 ergodic 行为。极限概率 \(m(\Gamma)\) 如果存在，被称为 **不变量度**。不变量度意味着如果初始状态按照 \(m(\Gamma)\) 分布，那么 \(y_n\) 的概率分布将保持相同的 \(m(\Gamma)\)（不变量度）。它是一个稳态。这个稳态在应用中具有强烈的兴趣。

### 3.5.1. 不变量度。

我们假设转移概率满足

(3.5.1)
\(\pi(x; dy) = \varpi(x, \eta) \mu(dy),\)

其中 \(\mu(dy)\) 是 \(X\) 上的正量度（不一定是概率）。此外，存在一个 Borel 集 \(X_0\) 使得 \(\mu(X_0) > 0\) 并且

(3.5.2)
\(\varpi(x, y) \ge \delta > 0, \forall x \in X, y \in X_0.\)

\(X, \mathcal{A}\) 上的概率测度 \(m\) 相对于转移概率 \(\pi(x, \Gamma)\) 是不变的，当且仅当

(3.5.3)
\(m(\Gamma) = \int_X m(dx) \pi(x, \Gamma), \forall \Gamma.\)

容易看出

(3.5.4)
\(m(\Gamma) = \int_X m(dx) P(x, n, \Gamma), \forall \Gamma.\)

右边表示当 \(y_1\) 的定律为 \(m\) 时 \(y_n\) 的概率定律。因此关系 (3.5.4) 表明这个概率也是 \(m\)，这解释了 *不变* 这个词。

### 3.5.2. 主要结果。

我们在这里呈现一个经典结果，参见 J.L. Doob [18]。

**定理 3.3.** 在假设 (3.5.1), (3.5.2) 下，存在相对于转移概率 \(\pi(x, \Gamma)\) 的唯一不变量度 \(m\) 并且

(3.5.5)
\(\left\| \Phi^n f - \int_X f(x) m(dx) \right\| \le 2 \|f\| \beta^{n-1} \quad \forall f \in B, \text{ with } 0 \le \beta < 1, \text{ independent of } f.\)

我们说该过程是 ergodic 的，这意味着其概率定律 \(P(x, n, \Gamma)\) 当 \(n\) 趋向于 \(\infty\) 时收敛到概率定律 \(m\)，无论初始状态 \(y_1 = x\) 如何。

**证明.** 假设 \(f \ge 0\)。我们定义

\(m_n(f) = \inf_x \Phi^n f(x), \quad M_n(f) = \sup_x \Phi^n f(x).\)





因此

$$
m_n(f) \le m_{n+1}(f),\\
M_n(f) \ge M_{n+1}(f),\\
m_n(f) \le M_n(f).
$$

我们依次有

$$
\begin{aligned}
M_{n+1}(f) - m_{n+1}(f) &= \sup_x \Phi^{n+1} f(x) - \inf_x \Phi^{n+1} f(x)\\
&= \sup_{x, \xi} (\Phi^{n+1} f(x) - \Phi^{n+1} f(\xi))\\
&= \sup_{x, \xi} [\Phi(\Phi^n f)(x) - \Phi(\Phi^n f)(\xi)]\\
&= \sup_{x, \xi} \left[ \int_X (\varpi(x, \eta) - \varpi(\xi, \eta)) \Phi^n f(\eta) \mu(d\eta) \right].
\end{aligned}
$$

由此可得

$$
\begin{aligned}
M_{n+1}(f) - m_{n+1}(f) &\le \sup_{x, \xi} \left[ \int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^+ \Phi^n f(\eta) \mu(d\eta) \right.\\
&\qquad \left. - \int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^- \Phi^n f(\eta) \mu(d\eta) \right]\\
&\le \sup_{x, \xi} \left[ M_n(f) \int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^+ \mu(d\eta) \right.\\
&\qquad \left. - m_n(f) \int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^- \mu(d\eta) \right].
\end{aligned}
$$

由于

$$
\int_X \varpi(x, \eta) \mu(d\eta) = \int_X \varpi(\xi, \eta) \mu(d\eta),
$$

\(M_n(f)\) 和 \(m_n(f)\) 的系数相同。

于是我们得到

$$
M_{n+1}(f) - m_{n+1}(f) \le (M_n(f) - m_n(f)) \sup_{x, \xi} \int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^+ \mu(d\eta).
$$

接下来

$$
\begin{aligned}
\int_X (\varpi(x, \eta) - \varpi(\xi, \eta))^+ \mu(d\eta)
&= \int_X (\varpi(x, \eta) - \varpi(\xi, \eta)) \mathbb{1}_{\{ \varpi(x, \eta) - \varpi(\xi, \eta) \ge 0 \}} \mu(d\eta)\\
&= 1 - \int_X \varpi(x, \eta) \mathbb{1}_{\{ \varpi(x, \eta) - \varpi(\xi, \eta) < 0 \}} \mu(d\eta)\\
&\qquad - \int_X \varpi(\xi, \eta) \mathbb{1}_{\{ \varpi(x, \eta) - \varpi(\xi, \eta) \ge 0 \}} \mu(d\eta)\\
&\le 1 - \int_{X_0} \varpi(x, \eta) \mathbb{1}_{\{ \varpi(x, \eta) - \varpi(\xi, \eta) < 0 \}} \mu(d\eta)\\
&\qquad - \int_{X_0} \varpi(\xi, \eta) \mathbb{1}_{\{ \varpi(x, \eta) - \varpi(\xi, \eta) \ge 0 \}} \mu(d\eta),
\end{aligned}
$$

并且由假设 (3.5.2) 可推出

$$
\begin{aligned}
&\le 1 - \delta \int_{X_0} \mathbb{1}_{\{\varpi(x, \eta) - \varpi(\xi, \eta) < 0\}} \mu(d\eta)\\
&\qquad - \delta \int_{X_0} \mathbb{1}_{\{\varpi(x, \eta) - \varpi(\xi, \eta) \ge 0\}} \mu(d\eta)\\
&= 1 - \delta \mu(X_0).
\end{aligned}
$$

因此我们已得到

$$
M_{n+1}(f) - m_{n+1}(f) \le (M_n(f) - m_n(f))(1 - \delta \mu(X_0)),
$$

故

$$
M_n(f) - m_n(f) \le (1 - \delta \mu(X_0))^{n-1} ||f||.
$$

我们推断出

$$
M_n(f) \Downarrow m(f); \quad m_n(f) \Uparrow m(f).
$$

我们还有不等式

$$
M_n(f) - m_n(f) \ge \Phi^n f(x) - m(f) \ge m_n(f) - M_n(f).
$$

我们已得到

$$
|\Phi^n f(x) - m(f)| \le M_n(f) - m_n(f) \le (1 - \delta \mu(X_0))^{n-1} ||f||.
$$

当 \(f\) 无定号时，利用 \(f\) 的正负部分分解，我们得到

$$
|\Phi^n f(x) - m(f)| \le M_n(f) - m_n(f) \le 2(1 - \delta \mu(X_0))^{n-1} ||f||,
$$

这就是期望的结果 (3.5.5)，其中 \(\beta = 1 - \delta \mu(X_0)\)。

尚需证明 \(m(f)\) 定义一个不变测度，且这样的不变测度是唯一的。映射 \(f \mapsto m(f)\) 是线性的，且 \(|m(f)| \le ||f||\)。若 \(f \ge 0\)，则 \(m(f) \ge 0\)，且 \(m(1) = 1\)。因此 \(m(f)\) 在 \(X, \mathcal{X}\) 上定义一个概率测度。显然

$$
m(f) = m(\Phi f).
$$

取 \(f = \mathbb{1}_{\Gamma}\) 得

$$
m(\Gamma) = \int_X m(dx) \pi(x, \Gamma),
$$

这证明了 \(m\) 是一个不变测度。若 \(\tilde{m}\) 是另一个不变测度，则按定义

$$
\tilde{m}(f) = \tilde{m}(\Phi^n f) \to m(f),
$$

故 \(\tilde{m} = m\)。证明完成。

### 3.5.3. 分析问题。

**定理 3.4.** 在假设 (3.5.1)、(3.5.2) 下，存在唯一一对 \(v \in B, \lambda \in R\)（\(v\) 以常数意义下唯一），使得

$$
\begin{aligned}
v - \Phi v + \lambda &= f, \quad \lambda = m(f)\\
m(v) &= 0,\\
m(v) &= m(\Phi v) = 0,\\
v(x) &= \lim_{\alpha \to 1} \left( u_\alpha - \frac{\lambda}{1 - \alpha} \right),\\
u_\alpha - \alpha \Phi u_\alpha &= f, \quad \alpha < 1.
\end{aligned}
$$

**证明。** 还可得

$$
\lambda = \lim_{\alpha \to 1} (1 - \alpha) u_\alpha,
$$

并且

$$
\lambda = \lim \frac{1}{N} \sum_{j=1}^N \Phi^j f, \text{ 在 } B.
$$

由方程 (3.5.6) 可推出

$$
m(v) - m(\Phi v) + \lambda = m(f).
$$

由于 \(m\) 是不变的，我们有 \(m(v) - m(\Phi v) = 0\)，故第二个性质 (3.5.6)。因此 \(\lambda\) 唯一。若存在两个解 \(v_1, v_2\)，则有

$$
v_1 - v_2 = \Phi(v_1 - v_2).
$$

故也

$$
v_1 - v_2 = \Phi(v_1 - v_2) \Rightarrow m(v_1) = m(v_2).
$$

因此 \(v_1\) 和 \(v_2\) 仅相差一个常数。若施加条件 \(m(v) = 0\)，则解唯一。为证明存在性，我们从方程 (3.5.6) 中定义的 \(u_\alpha\) 出发。此外

$$
u_\alpha = \sum_{n=0}^\infty \alpha^n \Phi^n f.
$$

故

$$
u_\alpha - \frac{\lambda}{1 - \alpha} = \sum_{n=0}^\infty \alpha^n \Phi^n (f - \lambda).
$$

由性质 (3.5.5) 可推出

$$
||\Phi^n(f - \lambda)|| \le 2 ||f|| |\beta|^{n-1}.
$$

由此可知，方程 (3.5.11) 定义的级数在 \(B\) 中绝对收敛。此外

$$
u_\alpha - \frac{\lambda}{1 - \alpha} \to v = \sum_{n=0}^\infty \Phi^n (f - \lambda).
$$

于是 \(v\) 是方程 (3.5.6) 的解。最后，性质 (3.5.8) 源于方程 (3.5.11) 右侧级数绝对收敛的事实。

## 3.6. 示例

### 3.6.1. 无积压的库存问题。

我们将考虑经典的无积压库存问题

$$
y_{n+1} = (y_n + v_n - D_n)^+,
$$

其中 \(D_n\) 是需求，建模为独立同分布变量序列，密度为 \(f\)。\(v_n\) 是订货量，我们假设以下策略

$$
v_n = S \mathbb{1}_{y_n=0}.
$$

因此，若初始库存不超过 \(S\)，则库存始终在 \(0\) 和 \(S\) 之间。故 \(X = [0, S]\)。我们已经看到，该模型在配备 Borel \(\sigma\)-代数的 \(X\) 上定义了一个马尔可夫链，其转移概率为

$$
\pi(x, d\eta) = \begin{cases} 
\overline{F}(x)\delta(\eta) + \mathbb{1}_{0 \le \eta < x} f(x - \eta) d\eta, & \text{if } x > 0 \\
\overline{F}(S)\delta(\eta) + \mathbb{1}_{0 \le \eta < S} f(S - \eta) d\eta, & \text{if } x = 0 
\end{cases}
$$

因此，它是 0 处的狄拉克概率与正库存上的概率密度的混合。

假设 \(\overline{F}(S) > 0\)，则定理 3.3 的条件满足。我们有

$$
\mu(d\eta) = \delta(\eta) + d\eta,
$$

和

$$
\varpi(x, \eta) = \begin{cases} 
\overline{F}(x)\mathbb{1}_{\eta=0} + \mathbb{1}_{0 < \eta < x} f(x - \eta), & \text{if } x > 0 \\
\overline{F}(S)\mathbb{1}_{\eta=0} + \mathbb{1}_{0 < \eta < S} f(S - \eta), & \text{if } x = 0 
\end{cases}
$$

我们可以取 \(X_0 = 0\) 和 \(\delta = \overline{F}(S)\)（此 \(\delta\) 不应与狄拉克测度 \(\delta(x)\) 混淆）。

事实上，我们可以直接求出不变测度。它是 \([0, S]\) 上的一个概率测度 \(m(dx)\)，记作如下

$$
m(dx) = A\delta(x) + B(x)dx, \quad A + \int_0^S B(x)dx = 1.
$$

为求 \(A\) 和 \(B(x)\)，我们必须写出关系式

$$
\int_0^S \phi(x)m(dx) = \int_0^S \phi(x)m(dx), \forall \phi.
$$

我们得到方程组

$$
\begin{aligned}
A &= A\overline{F}(S) + \int_0^S \overline{F}(x)B(x)dx,\\
B(\eta) &= A\overline{F}(S - \eta) + \int_\eta^S B(x)f(x - \eta)d\eta.
\end{aligned}
$$

于是我们有

**定理 3.5.** 假设 \(f(x) > 0\) 且连续。带归一化条件 (3.6.3) 的方程组 (3.6.4) 有唯一解。

**证明。** 我们注意到

$$
A = \frac{\int_0^S \overline{F}(x)B(x)dx}{F(S)}.
$$

将 \(A\) 代入第二个方程并取 \(\eta = S\) 得

$$
B(S) = f(0) \frac{\int_0^S \overline{F}(x)B(x)dx}{F(S)}.
$$

记

$$
u(\eta) = \frac{B(\eta)}{B(S)},
$$

第二个方程化简为

$$
u(\eta) = \frac{f(S-\eta)}{f(0)} + \int_\eta^S u(x)f(x-\eta)dx.
$$

那么方程 (3.6.6) 有且仅有一个解。确实，映射

$$
T : u \longrightarrow \frac{f(S-\eta)}{f(0)} + \int_\eta^S u(x)f(x-\eta)dx,
$$

是 \(C([0, S])\) 上的压缩映射，因为

$$
\|Tu_1 - Tu_2\| \le \|u_1 - u_2\| \int_0^S f(x)dx,
$$

并且

$$
\int_0^S f(x)dx < 1,
$$

且 \(B(S)\) 由

$$
B(S) \left[ \frac{\int_0^S \overline{F}(x)u(x)dx}{F(S)} + \int_0^S u(x)dx \right] = 1.
$$

定义。证明完成。在泊松分布 \(f(x) = \lambda \exp(-\lambda x)\) 的情况下，可得 \(u(\eta) = 1\) 且

$$
B(\eta) = \frac{\lambda}{1 + \lambda S}, \quad A = \frac{1}{1 + \lambda S}.
$$

### 3.6.2. 有积压的库存问题。

模型为

$$
y_{n+1} = y_n + v_n - D_n.
$$

因此允许负库存。订货遵循 \((s, S)\) 策略，其中 \(s < S, S > 0\)。即

$$
v_n = 0, \text{ if } y_n > s,
$$

$$
v_n = S - y_n, \text{ if } y_n \le s.
$$

显然，若 \(y_1 \le S\)，则对所有 \(n\)，\(y_n \le S\)。

我们有

$$
\begin{cases} 
\pi(x, dy) = f(S-\eta) \mathbb{1}_{\eta \le S} d\eta, & \text{if } x \le s \\
\pi(x, dy) = \mathbb{1}_{s \le x} f(x-\eta) d\eta, & \text{if } x > s 
\end{cases}
$$

我们有 \(X = (-\infty, S]\) 且 \(\mu(dy) = dy\)，其中

$$
\varpi(x, \eta) = \begin{cases} 
\mathbb{1}_{\eta \le s} f(S-\eta), & \text{if } x \le s \\
\mathbb{1}_{\eta \le x} f(x-\eta), & \text{if } x > s 
\end{cases}
$$

假设 \(f(x) > 0\) 且连续。则定理 3.3 的假设满足。我们取 \(X_0 = (s-1, s)\) 且

$$
\delta = \inf_{0 \le x \le S - s + 1} f(x).
$$





同样，我们可以直接研究不变测度的存在性和唯一性问题。我们寻找关于 \( X \) 上勒贝格测度的密度 \( m(x) \)。该密度必须满足方程

\[ m(\eta) = \int_{-\infty}^S m(x)\varpi(x, \eta) dx, \]

这相当于

\[ m(\eta) = f(S-\eta) \int_{-\infty}^{-s} m(x) dx + \int_s^S m(x) f(x-\eta) \mathbb{1}_{\{\eta \le x\}} dx \]

### 练习 3.5. 证明 \( m(\eta) \) 由以下公式唯一确定

\[ m(\eta) = \frac{f(S-\eta) + \int_s^S u(x) f(x-\eta) dx}{1 + \int_s^S u(y) dy}, \text{ if } \eta \le s \]

\[ m(\eta) = \frac{u(\eta)}{1 + \int_s^S u(y) dy}, \text{ if } s \le \eta \le S \]

其中函数 \( u(\eta) \) 在 \( s,S \) 上定义为积分方程的唯一解

\[ u(\eta) = f(S-\eta) + \int_\eta^S u(x) f(x-\eta) dx, s \le \eta \le S. \]

### 3.6.3. 有限个状态

假设 \( X \) 由有限个状态组成，记为 \( i = 1, \cdots, I \)。转移概率简化为矩阵 \( \varpi(i, j) \)。为了应用练习 3.3，只需假设存在一个状态 \( j_0 \)，使得

(3.6.8) \( \varpi(i, j_0), \forall i \in X. \)

唯一不变测度将满足

\[ m_i = \sum_j m_j \varpi(j, i), \sum_i m_i = 1, m_i \ge 0 \]

# 离散时间最优控制

离散时间马可夫控制过程的非常全面的介绍可以在 O. Hernández-Lerma 和 J.B. Lasserre 的书 [25] 中找到。我们的介绍更完整地讨论了唯一性问题，并将由动态规划（贝尔曼方程）产生的函数方程的研究与其在最优控制背景下的解释完全分开。

## 4.1. 确定性情况

### 4.1.1. 符号。

我们从确定性模型开始，尽管确定性情况可以嵌入随机情况。原因在于在确定性情况下不必担心信息问题。决策只是给定的值（开环控制）。在随机情况下，决策是信息状态的函数（闭环控制）。在确定性情况下可以调和这两种方法，但这仅为了获得主要结果而显得不必要地复杂。

我们考虑一个动态系统，其演化由以下方程控制

(4.1.1) 
\[ y_{n+1} = g(y_n, v_n), \quad y_1 = x. \]

此时，我们对函数 g 不需要任何特定假设，除了可测性。正如我们将看到的，讨论的第一部分将是代数性质的。状态空间是 X，一个度量空间 R^d 或离散空间。接下来我们考虑一个函数

(4.1.2) 
\[ l(x, v) \text{ 有下界。} \]

控制（或者更准确地说是控制策略）是度量空间子集 U 中的一系列值 v_1 ... v_n ...。控制记为 V。我们定义收益

(4.1.3) 
\[ J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n). \]

不失一般性，我们假设 l(x, v) >= 0。确实，如果 l(x, v) + C >= 0，我们可以将 J_x(V) 改为 J_x(V) + C / (1 - alpha) 从而获得非负性假设。折扣因子 alpha 小于 1。我们定义

(4.1.4) 
\[ u(x) = \inf_V J_x(V), \]

这是一个正数。函数 u(x) 称为值函数。我们假设

(4.1.5) 
\[ u(x) < \infty \]

### 4.1.2. 贝尔曼方程。

函数 u(x) 满足一个称为贝尔曼方程的函数方程，[2], [11]。正如我们将看到的，这仅仅是代数考虑的结果。对该函数方程的研究，独立于其起源，将在以后进行，并需要分析工具。

### 提议 4.1。

函数 u(x) 满足关系式

(4.1.6) 
\[ u(x) = \inf_{v \in U} [l(x, v) + \alpha u(g(x, v))]. \]

证明。从定义出发，我们可以写出

\[ u(x) = \inf_{v_1} \left[ l(x, v_1) + \alpha \inf_{v_2 \cdots v_n} \left[ \sum_{n=2}^\infty \alpha^{n-2} l(y_n, v_n) \right] \right], \]

但括号内的下确界显然是 u(g(x, v))。因此结果成立。

现在假设存在一个可测函数 \(\hat{v}(x)\)，使得 (4.1.6) 右边的下确界对于这个值和任何 x 的值都能取到。这样的函数称为反馈。我们可以在状态方程中使用这个反馈，并定义序列 \(\hat{y}_n\) 如下

\[ \hat{y}_{n+1} = g(\hat{y}_n, \hat{v}(\hat{y}_n)). \]

接下来定义 \(\hat{v}_n = \hat{v}(\hat{y}_n)\)，我们得到一个控制 \(\hat{V} = (\hat{v}_1 \cdots \hat{v}_n \cdots)\)。我们然后得到结果

### 提议 4.2。

\(\hat{V}\) 是最优的。

证明。通过归纳法可以验证

\[ u(x) = \sum_{j=1}^n \alpha^{n-1} l(\hat{y}_n, \hat{v}_n) + \alpha^n u(\hat{y}_{n+1}), \]

因此 u(x) \(\ge J_x(\hat{V})\)。然而，作为下确界，u(x) 也小于 \(J_x(\hat{V})\)。所以我们有等式，因此 \(\hat{V}\) 是最优的。

请注意，最优控制是通过对状态的反馈获得的。这一属性在确定性情况下是一个奇特之处，但在随机情况下将发挥根本作用，因为它具有信息内容。

### 4.1.3. 当约束集依赖于状态时的扩展。

然而，即使在确定性情况下，也存在信息重要的情况。即约束集 U 不是固定的，而是依赖于状态 U(x) 的情况。控制策略 V 不能只是 U 元素的简单序列 v_n，因为 U 不再固定。我们还必须满足 v_n \in U(y_n)。

然而，不难验证提议 4.1 证明中的论证仍然有效。贝尔曼方程变为

(4.1.7) 
\[ u(x) = \inf_{v \in U(x)} [l(x, v) + \alpha u(g(x, v))]. \]

### 4.2. 随机情况：一般表述

我们现在转向随机情况。正如我们将看到的，机制更加复杂。

### 4.2.1. 符号和假设。

概率设置与第 3 章相同。状态空间是 X，概率空间是 $\Omega = \mathcal{X}^N$，$\sigma$-代数为 $\mathcal{A} = \mathcal{X}^N$。标准过程记为 $y_n(\omega) = \omega_n$，它生成滤流 $\mathcal{Y}^n$。我们现在考虑一族转移概率，由参数 $v$（控制变量）索引。参数 $v$ 属于集合 $U$，即控制集，它是度量空间的一个闭子集。

转移概率记为 $\pi(x, v, dy)$。我们将其与 B 上的算子关联起来（X 上可测有界函数空间），同样由 v 索引

\(\Phi^v f(x) = \int_X f(y) \pi(x, v, dy).\)

我们现在将控制策略定义为取值于 U 的一系列 Borel 映射

$v_1(\eta_1), v_2(\eta_1, \eta_2)$

\(\cdots, v_n(\eta_1, \cdots, \eta_n), \cdots\)

这样的控制记为 V。然而，我们看到与确定性情况的主要区别，在确定性情况下控制只是一系列值。在随机情况下，控制必须以闭环方式定义。

对于控制 V 和初始状态 x，我们在 $\Omega$, $\mathcal{A}$ 上关联一个概率定律，即给定 $y_1 = x$ 时标准过程的条件定律。我们将其记为 $P^{V,x}$。对于任何测试函数 $f(x_1, \cdots, x_n)$，我们有

$E^{V,x} f(y_1, \cdots, y_n) = E[f(y_1, \cdots, y_n) | y_1 = x]$
$= \int \pi(x, v_1(x), dx_2) \int \pi(x_2, v_2(x, x_2), dx_3) \cdots$
$\int \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), dx_n) f(x_1, \cdots, x_n).$

$P^{V,x}$ 是一个受控马可夫链。严格来说，受控马可夫链不是马可夫链，因为由于决策规则，我们保留了所有先前状态的记忆。然而，可以与标准马可夫链做一些类比。我们引入

$P^{V,x}(n-1; x, \cdots, x_{n-1}, n; \Gamma) = \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), \Gamma)$

$P^{V,x}(m; x, \cdots, x_m; n; \Gamma) = \int \pi(x_m, v_m(x, x_2, \cdots, x_m), dx_{m+1} \cdots$
$\int \pi(x_{n-2}, v_{n-2}(x, x_2, \cdots, x_{n-2}), dx_{n-1} \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), \Gamma)$

### 练习 4.1. 验证

$P^{V,x}(k; y_1, \cdots, y_k; k+n, \Gamma) = E^{V,x}[\mathbb{I}_{\Gamma}(y_{k+n}) | \mathcal{Y}^k],$

这可以扩展到将 $k$ 替换为停时 $\nu$。验证

$P^{V,x}(\nu; y_1, \cdots, y_\nu; \nu+n, \Gamma) = E^{V,x}[\mathbb{I}_{\Gamma}(y_{\nu+n}) | \mathcal{D}^\nu]$

验证对于任何 $u \in B$

$u(y_n) + \sum_{j=1}^{n-1} (u(y_j) - \Phi^{v_j}(y_1, \cdots, y_j) u(y_j)),$



是一个 $\mathcal{Y}^n, P^{V,x}$ 鞅。还需验证

$$
\alpha^n u(y_n) + \sum_{j=1}^{n-1} \alpha^j (u(y_j) - \alpha \Phi^{v_j}(y_1, \cdots, y_j) u(y_j)),
$$

是一个 $\mathcal{Y}^n, P^{V,x}$ 鞅。

**注.** 我们可以将确定性情况视为马尔可夫链的一种特例，其中

$$
\pi(x, v, d\eta) = \delta_{g(x,v)}
$$

为点 $g(x, v)$ 处的迪拉克测度。然而，控制必须以闭环方式定义。我们无法以这种方式恢复开环控制。这就是为什么通过这条路径来考虑确定性问题是不必要地复杂。

## 4.2.2. 问题设定。

考虑

(4.2.1) $$l(x, v) \ge 0,$$

且 $U$ 是度量空间的一个子集。

我们考虑一个由转移概率 $\pi(x, v, \Gamma)$ 描述的受控马尔可夫链。考虑一个控制策略 $V$，并为标准过程 $y_n$ 构造相应的概率 $P^{V,x}$。控制中出现的函数 $v_n(x_1, \cdots, x_n)$ 必须取值于 $U$。

我们定义代价泛函

(4.2.2) $$
J_x(V) = E^{V,x} \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n).
$$

如果接受值 $+\infty$，则该量定义良好。值函数定义为

$$
u(x) = \inf_V J_x(V).
$$

一个重要的问题是，值函数是否满足一个函数方程，如同在确定性情况下那样，遵循代数论证。这变得高度非平凡，但我们将证明这是可能的，在一个对应用有用且在某种程度上模拟确定性情况的情况下。在上述一般情况下，我们将通过使用分析论证而非代数论证来避免这一困难。

## 4.2.3. 直接方法。

我们考虑动态系统演化描述如下的情况。考虑一个概率空间 $(\Omega, \mathcal{A}, P)$，在其上定义了一个由独立同分布随机变量组成的随机过程 $D_1 \cdots D_n \cdots$。符号 $D$ 唤起需求过程，该过程将在库存控制的应用中不断出现。我们用 $h(\xi)$ 表示一个通用 $D$ 的概率密度，为明确起见，它位于 $R^k$。过程 $y_n$ 由以下定义

$$
y_{n+1} = g(y_n, v_n, D_n) \quad y_1 = x.
$$

我们将假设需求是可观测的。在时刻 $n+1$，我们已观察到 $D_1 \cdots D_n$ 的值。所以

$$
v_n = v_n(D_1, \cdots, D_{n-1}) \quad n \ge 2,
$$

且 $v_1$ 是确定性的。这比 $v_n = v_n(y_1, \cdots, y_n)$ 更一般，并且自然地源于每个时刻可用的信息。如果 $U$ 依赖于 $x$，则我们有约束

$v_n(D_1, \cdots, D_{n-1}) \in U(y_n),$

且 $y_n$ 也是 $D_1, \cdots, D_{n-1}$ 的一个函数。算子 $\Phi^v f(x)$ 由以下给出

(4.2.3) $\Phi^v f(x) = E f(g(x, v, D)) = \int f(g(x, v, y)) \eta(dy).$

令 $V = \{v_1, \cdots, v_n, \cdots \}$ 为上述定义的控制。收益由以下给出

(4.2.4) $J_x(V) = E \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n).$

需要注意的是，期望是相对于固定概率 $P$ 取的，不像公式 (4.2.2) 那样依赖于控制策略。我们定义值函数

$u(x) = \inf_V J_x(V).$

**命题 4.3.** *值函数满足函数方程（贝尔曼方程）*

(4.2.5) $u(x) = \inf_{v \in U(x)} [l(x, v) + \alpha E u(g(x, v, D))].$

证明。令

$K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n),$

这是关于 $D_1, \cdots, D_n \cdots$ 的一个泛函。得益于随机变量的独立性，我们有

$EK(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = E_{D_1 D_2 \cdots} K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots),$

其中右侧作为下标的期望意味着必须依次取期望。我们从后往前开始。期望数量无限这一点不是问题，因为 $K$ 表达式中的每一项仅依赖于有限个需求。注意关系式

$K(x, v_1, \cdots, v_n, \cdots ; D_1, \cdots, D_n, \cdots) = l(x, v_1) + \alpha K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots).$

因此，对于固定的 $x, v_1, D_1$，我们可以写出

(4.2.6) $\inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots) = u(g(x, v_1, D_1)).$

现在关键点是验证

(4.2.7) $E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots) = \inf_{v_2 \cdots v_n \cdots} E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2, \cdots, v_n, \cdots ; D_2, \cdots, D_n, \cdots).$

换句话说，我们可以交换两个算子 $E_{D_1}$ 和 inf。其原因是决策变量 $v_2 \cdots, v_n \cdots$ 是所有随机变量（包括 $D_1$）的函数。更具体地说，我们首先可以断言

$E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots)$

其中，在右侧，决策变量是任意的。因此，方程 (4.2.7) 的左侧小于其右侧。另一方面，对于任何 $\epsilon$ 和任何固定的 $D_1$，我们可以找到一个依赖于 $D_1$ 的策略 $v_2^\epsilon, \cdots, v_n^\epsilon \cdots$，使得

$E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2^\epsilon, \cdots, v_n^\epsilon, \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) + \epsilon.$

因此

$E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2^\epsilon, \cdots, v_n^\epsilon, \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots) + \epsilon.$

因此也

$\inf_{v_2 \cdots v_n \cdots} E_{D_1 D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots, \cdots) \le E_{D_1} \inf_{v_2 \cdots v_n \cdots} E_{D_2 D_3 \cdots} K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots) + \epsilon,$

由于 $\epsilon$ 任意，(4.2.7) 的右侧小于左侧。故关系式 (4.2.7) 成立。该关系还意味着

$E u(g(x, v_1, D_1)) = \inf_{v_2 \cdots v_n \cdots} E K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots).$

但那么

$u(x) = \inf_v [l(x, v_1) + \alpha \inf_{v_2 \cdots v_n \cdots} E K(g(x, v_1, D_1), v_2 \cdots, v_n \cdots ; D_2 \cdots, D_n \cdots)],$

这蕴含了结果。

## 4.3. 函数方程

我们从假设开始。空间 $X = R^d$。控制集 $U$ 是 $R^k$ 的一个闭子集。如果 $\phi(x, v)$ 是两个变量的函数，我们写 $\phi_v(x) = \phi(x, v)$。我们将假设

(4.3.1) 若 $\phi_v(x) = \phi(x, v)$ 在 $x, v$ 中一致连续且有界，则 $\Phi^* \phi_v(x)$ 在 $v, x$ 中一致连续。

我们还假设

(4.3.2) $l_v(x) = l(x, v)$ 为下半连续且 $\ge 0$；$l(x, v)$ 在有界集上有界；$\Phi^* l_v(x)$ 在有界集上有界；$\{ v \in U \mid l(x, v) \le L, |x| \le M \} \subset \{ |v| \le K_{LM} \}$。

### 4.3.1. 技术结果。

我们首先回顾几个重要的技术结果。一些证明在附录中。

**引理 4.1.** 设 $f$ 是从度量空间 $X$ 到 $(-\infty, +\infty]$ 的一个映射，它是下半连续且下有界的。存在一个序列 $f_n(x) \in C(X)$（$X$ 上一致连续有界函数的空间），使得 $f_n(x)$ 逐点上升到 $f(x)$。

**引理 4.2.** 在假设 (4.3.1) 下，如果 $l_v(x) = l(x, v)$ 是下半连续且下有界的，那么关于对 $(v, x)$ 的函数 $\Phi^* l_v(x)$ 是下半连续且下有界的。

**引理 4.3.** 设 $F(x, v)$ 在两个变量中均为下半连续且下有界。如果 $U$ 是度量紧的，那么

$G(x) = \inf_{v \in U} F(x, v),$

也是下半连续且下有界的。

一个关键结果是，对于每个 $x$，存在一个极小值，它是 $x$ 的可测函数。

**定理 4.1.** 在引理 4.3 的假设下，存在一个博雷尔函数 $\hat{v}(x) : X \to U$，使得

$G(x) = F(x, \hat{v}(x)), \forall x.$

$U$ 是紧的这一事实在某些应用中可能不成立。我们在此介绍一种在应用中出现的情况，其中去掉了 $U$ 的紧性假设。假设

- $U$ 是 $R^d$ 的一个闭子集；
- $F(x, v)$ 是下半连续且下有界的；
- $\{v \mid F(x, v) \le F(x, v_0)\} \subset \{v \mid |v| \le \gamma(x)\}$；
- $\gamma(x)$ 在有界集上有界。

我们陈述

**定理 4.2.** 在引理 4.3 的假设下（$U$ 紧除外），且如果假设 (4.3.3) 成立，那么 $G(x)$ 是下半连续且下有界的，并且存在一个博雷尔映射 $\hat{v}(x)，它对任何 $x$ 都取得极小值。

### 4.3.2. 天花板函数。

我们首先考虑将固定控制 $v_0 \in U$ 作为参数的情况。引入方程

(4.3.4) $w_0(x) = l(x, v_0) + \alpha \Phi^{v_0} w_0(x).$

更精确地，我们考虑函数

(4.3.5) $w_0(x) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^{v_0})^{n-1} l_{v_0}(x),$

其中我们已记 $l_v(x) = l(x, v)$。

函数 $w_0(x)$ 定义为当 $N \uparrow +\infty$ 时的极限

$w_{0N}(x) = \sum_{n=1}^N \alpha^{n-1} (\Phi^{v_0})^{n-1} l_{v_0}(x).$





由于所有函数都是正的，极限定义良好，但可能取值 \( +\infty \)。回顾引理 4.2，我们可以断言函数 \( w_0(x) \) 也是下半连续的（l.s.c.）。我们将在后续中使用假设 (4.3.6)

(4.3.6)
\( w_0(x) < \infty, \forall x. \)
\( u_0(x) \text{ is bounded on bounded sets} \)

## 4.3.3. 贝尔曼方程。

我们考虑函数方程

(4.3.7)
\( u(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u(x)], \forall x. \)

现在不将此方程解释为控制问题的值函数来考虑。我们给出主要结果

### 定理 4.3.
在假设 (4.3.1)、(4.3.2)、(4.3.6) 下，函数方程 (4.3.7) 的解集满足

\( 0 \le u(x) \le w_0(x) \forall x, \)

非空，并具有最小解和最大解，分别记为 \( \underline{u}(x) \) 和 \( \overline{u}(x) \)。最小解是下半连续的（l.s.c.）。

**证明。** 考虑以下迭代

\( u_0(x) = 0, \)
\( u_{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u_n(x)]. \)

该序列单调递增。我们有

\( 0 \le u_n(x) \le w_0(x) \forall x, \)

可以通过递归验证。因此我们有 \( u_n(x) \uparrow u(x) \) 从而

\( u_{n+1}(x) \le \inf[(l(x, v) + \alpha \Phi^v u(x)], \forall x, \)

并且也有

\( u(x) \le \inf[(l(x, v) + \alpha \Phi^v u(x)], \forall x. \)

此外，得益于假设 (4.3.2)，函数 \( u_n(x) \) 是下半连续的（l.s.c.），因此存在 Borel 映射 \( v_n(x) \) 使得

\( u_{n+1}(x) = l(x, v_n(x)) + \alpha \Phi^{v_n(x)} u_n(x). \)

设 \( n \le m \)，我们可以写出

\( u_{m+1}(x) = l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_m(x) \)
\( \ge l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_n(x), \)

从而也有

\( u(x) \ge l(x, v_m(x)) + \alpha \Phi^{v_m(x)} u_n(x). \)

现在对于固定的 \( x \)，序列 \( v_m(x) \) 保持在一个紧集中，因此存在子序列使得 \( v_{m_k}(x) \to v^*(x) \)。请记住 \( n \) 是固定的，且 \( l(x, v) + \alpha \Phi^v u_n(x) \) 是下半连续的（l.s.c.）。

我们因此可以断言

\( u(x) \ge l(x, v^*(x)) + \alpha \Phi^{v^*} u_n(x). \)

现在令 \( n \) 趋向于 \( \infty \)，我们得到

\( u(x) \ge l(x, v^*(x)) + \alpha \Phi^{v^*} u(x), \)

从而

\(u(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

由于逆不等式成立，函数 \(u\) 是一个解。这个函数是最小解，因为如果存在另一个解 \(\tilde{u}\) 满足 \(0 \le \tilde{u} \le w_0(x)\)，则我们可以逐步验证 \(\tilde{u} \ge u_n\)，因此在极限下 \(\tilde{u} \ge u\)。我们将最小解记为 \(\underline{u}(x)\)。这个最小解是下半连续的（l.s.c.）。我们现在转向最大解。我们从上界函数开始并使用相同的迭代来定义一个递减序列，即

\(u^0(x) = w_0(x),\)
\(u^{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u^n(x)].\)

我们有 \(u^n(x) \downarrow u(x)\) 从而也有
\(u^{n+1}(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

因此，
\(u(x) \ge \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

另一方面，对于任意 \(v\)，我们可以写出不等式
\(u^{n+1}(x) \le [l(x, v) + \alpha \Phi^v u^n(x)].\)

在取极限时，我们必须小心 \(u^n(x)\) 是递减的。我们不能直接使用法图引理。然而序列 \(w_0(x) - u^n(x)\) 是递增且正的。因此，将法图引理应用于该序列，我们可以断言
\(\Phi^v u^n(x) \downarrow \Phi^v u(x).\)

由此可得
\(u(x) \le \inf_v [l(x, v) + \alpha \Phi^v u(x)].\)

并且由于逆不等式成立，函数 \(u\) 是方程 (4.3.7) 的一个解。可以轻松验证它是在区间 \(0, w_0(x)\) 内的最大解。这个最大解记为 \(\overline{u}(x)\)。证明已完成。\(\square\)

## 4.4. 概率解释

### 4.4.1. 最小解。
我们回顾单调递增过程

(4.4.1)
\(u_0(x) = 0,\)
\(u_{n+1}(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v u_n(x)].\)

函数 \(u_n(x)\) 是下半连续的（l.s.c.）且下有界。将存在一个取值于 \(U\) 的 Borel 函数 \(\hat{v}_n(x)\) 使得
\(u_{n+1}(x) = l(x, \hat{v}_n(x)) + \alpha \Phi^{\hat{v}_n(x)} u_n(x).\)

考虑由 (4.2.2) 定义的成本函数。让我们定义截断成本函数

\(J_x^n(V) = E^{V,x} \left[ \sum_{j=1}^n \alpha^{j-1} l(y_j, v_j) \right].\)

我们从上面引入的反馈定义控制策略

\(\hat{V}_n = (\hat{v}_1, \cdots, \hat{v}_n, \cdots),\)

其中

$$\begin{aligned} \hat{v}_{jn}(x_1, \cdots, x_j) &= \hat{v}_j(x_j), \forall 1 \le j \le n, \\ \hat{v}_{jn}(x_1, \cdots, x_j) &= \bar{v} \text{ (任意)} \forall j \ge n + 1. \end{aligned}$$

我们可以断言

### 引理 4.4.
我们有如下解释

$$u_n(x) = \inf_V J_x^n(V) \tag{4.4.2}$$

**证明。** 选取任意控制 \(V\)。对于 $j=0, \cdots, n-1$ 我们可以写出

$$\begin{aligned} u_{j+1}(y_{n-j}) &\le l(y_{n-j}, v_{n-j}) + \alpha \Phi^{v_{n-j}} u_j(y_{n-j}) \\ &= l(y_{n-j}, v_{n-j}) + \alpha E^{V,x}[u_j(y_{n-j+1}) | Y^{n-j}]. \end{aligned}$$

从而也有

$$E^{V,x} \alpha^{n-j-1} u_{j+1}(y_{n-j}) \le E^{V,x} \alpha^{n-j-1} l(y_{n-j}, v_{n-j}) + E^{V,x} \alpha^{n-j} u_j(y_{n-j+1}).$$

从 $j=0, \cdots, n-1$ 求和得到

$$u_n(x) \le J_x^n(V).$$

类似地，我们可以验证

$$u_n(x) = J_x^n(\tilde{V}_n),$$

结果已得到。

我们可以进一步断言

### 定理 4.4.
在假设 (4.3.1)、(4.3.2)、(4.3.6) 下，函数方程 (4.3.7) 在 0 和 $w_0$ 之间的最小解 $\underline{u}(x)$ 是值函数

$$\underline{u}(x) = \inf_V J_x(V).$$

而且存在一个最优控制策略 $\hat{V}$。

**证明。** 对于任意决策规则 \(V\)，根据引理 4.4，我们有

$$u_n(x) \le J_x^n(V) \le J_x(V).$$

因此

$$\underline{u}(x) \le J_x(V),$$

并且由于 \(V\) 是任意的

$$\underline{u}(x) \le \inf_V J_x(V).$$

另一方面，由于 $\underline{u}(x)$ 是正的下半连续函数，存在一个 Borel 映射 $\tilde{v}(x)$ 使得

$$\underline{u}(x) = l(x, \tilde{v}(x)) + \alpha \Phi^{\tilde{v}} \underline{u}(x).$$

然后定义控制策略 $\hat{V}$ 如下

$$\hat{V} = (\hat{v}_1, \cdots, \hat{v}_n, \cdots),$$

其中

$$\hat{v}_n(x_1, \cdots, x_n) = \hat{v}_n(x_n).$$

我们容易得到

$$\underline{u}(x) = \sum_{j=1}^n E^{V,x} \alpha^{j-1} l(y_j, \hat{v}_j) + \alpha^n E^{V,x} \underline{u}(y_{n+1}),$$

并且由于 \(\underline{u}(x) \ge 0\)，我们有

\(\underline{u}(x) \ge \sum_{j=1}^n E^{\hat{V},x} \alpha^{j-1} l(y_j, \hat{v}_j).\)

令 \(n \to \infty\) 得到

\(\underline{u}(x) \ge J_x(\hat{V}),\)

这实际上意味着相等。结果已得到。

### 4.4.2. 最大解。

我们现在转向最大解 \(\bar{u}(x)\) 的解释。我们首先解释通过递减序列得到的函数 \(u^n(x)\)

(4.4.3) \(\begin{aligned} u^0(x) &= w_0(x), \\ u^{n+1}(x) &= \inf_{v \in U} [l(x, v) + \alpha \Phi^v u^n(x)]. \end{aligned}\)

我们定义一组控制策略如下

(4.4.4) \(\begin{aligned} \mathcal{V}^n = \{V = (v_1, \cdots, v_j, \cdots) \text{ where} \\ v_j &= v_j(x_1, \cdots, x_j) \forall j \le n, \\ v_j &= v_0 \forall j \ge n+1 \}, \end{aligned}\)

其中函数 \(v_j\) 是取值于 \(U\) 的 Borel 函数。我们随后给出

### 引理 4.5.
我们有如下解释

(4.4.5) \(u^n(x) = \inf_{V \in \mathcal{V}^n} J_x(V)\)

**证明。** 通过与引理 4.4 类似的推理，对于任意控制策略 \(V\)（不一定属于 \(\mathcal{V}^n\)），我们可以写出

\(u^n(x) \le E^{V,x} \sum_{j=1}^n \alpha^{j-1} l(y_j, v_j) + E^{V,x} \alpha^n w_0(y_{n+1}).\)

现在取 \(V \in \mathcal{V}^n\)。对于 \(m \ge n\)，我们可以写出

\(E^{V,x} [\mathbf{I}_{\Gamma}(y_{m+1}) | y^m) = \Phi^{v_0} \mathbf{I}_{\Gamma}(y_m).\)

接下来考虑 \(w_0\)，对于 \(j \ge n+1\)，我们可以写出

\(w_0(y_j) = l(y_j, v_0) + \alpha E^{V,x} [w_0(y_{j+1}) | \mathcal{Y}^j].\)

特别是

\(E^{V,x} w_0(y_{n+1}) = E^{V,x} \sum_{j=n+1}^\infty \alpha^{j-n-1} l(y_j, v_0),\)

从而也有

\(u^n(x) \le E^{V,x} \sum_{j=1}^\infty \alpha^{j-1} l(y_j, v_j), \forall V \in \mathcal{V}^n.\)

接下来我们注意到函数 \(u^n(x)\) 是下半连续的，因此可以定义一个 Borel 映射 \(v^n(x)\) 使得

\(u^n(x) = l(x, v^n(x)) + \alpha \Phi^{v^n(x)} u^n(x).\)

然后定义

\(\hat{V}^n = (\hat{v}_1^n, \cdots, \hat{v}_j^n, \cdots),\)



其中

\(\tilde{v}_j^n(x_1, \cdots, x_j) = v_j(x_j), \forall j \le n\)
\(\tilde{v}_j^n(x_1, \cdots, x_j) = v_0, \forall j \ge n+1.\)

可得

\(u^n(x) = E^{V^n, x} \sum_{j=1}^n \alpha^{j-1} l(y_j, \tilde{v}_j^n) + \alpha^n E^{V^n, x} w_0(y_{n+1}).\)

因此

\(u^n(x) = E^{V^n, x} \sum_{j=1}^\infty \alpha^{j-1} l(y_j, \tilde{v}_j^n)\)

\(u^n(x) = J_x(\tilde{V}^n).\)

由于 \(\tilde{V}^n \in \mathcal{V}^n\)，引理的证明已完成。

为了最终给出最大解的解释，我们引入集合

\(\mathcal{V} = \{V|V = (v_1, \cdots, v_i, \cdots) \text{ where }\)
\(v_i = v_i(x_1, \cdots, x_i)\)
\(\alpha^{j-1} E^{V, x} \bar{u}(y_j) \to 0 \text{ as } j \to +\infty \}.\)

我们可以给出如下定理

### 定理 4.5. 在假设 (4.3.1)、(4.3.2)、(4.3.6) 下，函数方程 (4.3.7) 在 0 和 \(w_0\) 之间的最大解 \(\bar{u}(x)\) 由

\(\bar{u}(x) = \inf_{V \in \mathcal{V}} J_x(V)\)

给出。

### 证明. 考虑控制策略 \(\tilde{V}^n\)。我们将检查对于任意 \(n\)，它是否属于 \(\mathcal{V}\)。我们需要验证

\(\alpha^{k-1} E^{V^n, x} \bar{u}(y_k) \to 0 \text{ as } k \to +\infty.\)

我们可以假设 \(k \ge n+1\)。由于 \(\bar{u}(x) \le w_0(x)\)，只需验证

\(\alpha^{k-1} E^{V^n, x} w_0(y_k) \to 0 \text{ as } k \to +\infty.\)

然而

\(\alpha^{k-1} E^{V^n, x} w_0(y_k) = E^{V^n, x} \sum_{j=k}^\infty \alpha^{j-1} l(y_j, v_0),\)

当 \(k \ge n+1\) 时。

但级数

\(E^{V^n, x} \sum_{j=n+1}^\infty \alpha^{j-1} l(y_j, v_0) \le u^n(x) < \infty,\)

因此是收敛级数。故确实

\(E^{V^n, x} \sum_{j=k}^\infty \alpha^{j-1} l(y_j, v_0) \to 0 \text{ as } k \to \infty.\)

从而得出结果。接下来我们知道

\(u^n(x) = J_x(\tilde{V}^n).\)

因此

\( u^n(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \),

并且

\( \bar{u}(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \).

另一方面，对于任意控制（不一定属于 \(\mathcal{V}\)），我们可以写出

\(\bar{u}(x) \le E^{V,x} \sum_{j=1}^{n} \alpha^{j-1} l(y_j, v_j) + \alpha^n E^{V,x} \bar{u}(y_{n+1})\)

\(\le J_x(V) + \alpha^n E^{V,x} \bar{u}(y_{n+1}).\)

现在如果 \( V \in \mathcal{V} \)，第二项在 \( n \to \infty \) 时趋于 0。因此我们可以断言

\( \bar{u}(x) \le J_x(V) \forall V \in \mathcal{V} \),

这完成了定理的证明。

### 注记. 我们不声称右边 (4.4.7) 的下确界可达。而且最大解是上半连续（u.s.c.）的，而不是下半连续（l.s.c.）的。

### 4.5. 唯一性

我们考虑函数方程 (4.3.7) 在区间 \((0, w_0)\) 上的解的唯一性问题。唯一性的充要条件是最小解和最大解重合。要证明最小解和最大解重合，只需证明最优控制 \(\bar{V} \in \mathcal{V}\)。另一种方法是使用收缩性质（当可用时）。

### 定理 4.6. 假设 \( l(x, v) \) 有界。那么 (4.3.7) 存在唯一解。

### 证明. 我们可以使用收缩性质。回顾 \( B \) 表示 \( X = R^d \) 上有界函数空间。我们注意到 (4.3.7) 可以写成关于映射

\( T : B \to B, z = Tw, \)

的不动点，其中

\( Tw(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v(w)], \)

并且由于 \( l \) 有界，我们可以将 \( T \) 定义为从 \( B \) 到 \( B \) 的映射。当 \( \alpha < 1 \) 时，显然 \( T \) 是收缩映射。因此存在唯一的不动点。

### 注记. 由于 \( w_0 \) 有界，唯一性也直接由条件 (4.4.6) 始终满足这一事实得出。

此结果可以以多种方式推广。

### 定理 4.7. 假设

(4.5.1) \( 0 \le l(x, v) \le h|x| + c|v| + l_0, \)

(4.5.2) \( \Phi^v(|x|) \le \theta|x| + \lambda|v| + \mu, \)

且 \( U \) 为紧集。如果 \( \alpha\theta < 1 \)，则 (4.3.7) 在线性增长函数空间 \( B_1 \) 中的解存在且唯一。

### 证明. 在等式 (4.5.2) 中，我们用 \(|x|\) 表示函数 \(x \to |x|\)。我们为 \( B_1 \) 配备一个等价范数

\( ||u||_1 = \sup_x \frac{|u(x)|}{1 + \sigma|x|}, \)

其中 \(\sigma\) 可以任意选取且将被选得足够小。对于 \( v \in U \)，我们有

\( l(x, v) \le h|x| + l_1 \)

\( \Phi^v(|x|) \le \theta|x| + m \)

再次考虑在定理证明中定义的映射 \( T \)，这次是从 \( B_1 \) 到 \( B_1 \)。注意对于 \( w \in B_1 \) 和 \( v \in U \)，我们有

\( \alpha \Phi^v(w) \le \alpha[|w|](1 + \sigma\Phi^v(|x|)) \)
\( \le \alpha[|w|](1 + \sigma\theta|x| + \sigma m). \)

那么

\( ||Tw_1 - Tw_2|| \le \alpha|w||| \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|}. \)

得益于假设，我们有

\( \alpha \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|} \le \alpha(1 + \sigma m), \)

并且通过选择足够小的 \(\sigma\)，右边的数严格小于 1。因此 \( T \) 在 \( B_1 \) 中是收缩映射。存在性和唯一性随之而来。

### 注记. 同样，可以将前面的结果视为最大解和最小解重合这一事实的后果。确实，为了明确起见，取 \(v_0 = 0\)。我们首先注意到，从增长假设中我们有

(4.5.3) \quad w_0(x) \le \frac{h|x|}{1 - \alpha\theta} + \frac{l_0}{1 - \alpha} + \frac{\alpha m}{1 - \alpha\theta}.

取任意控制策略 \(V\)。从 \(V\) 的定义出发，参见 (4.4.6)，利用 \(\bar{u} \le w_0\) 这一事实，只需证明

\( \alpha^{j-1} E^{V,x}[y_j] \to 0 \text{ as } j \to +\infty. \)

然而

\( E^{V,x}[|y_{j+1}| | Y_j] = \Phi^{v_j}[x](y_j) \)
\( \le \theta|y_j| + m. \)

因此

\( E^{V,x}[|y_{j+1}|] \le \theta E^{V,x}[|y_j|] + m, \)

由此可得

\( E^{V,x}[|y_j|] \le \theta^{j-1}|x| + m \sum_{k=0}^{j-2} \theta^k \)
\( \le \theta^{j-1}|x| + m(j-1)\theta^{j-2}, \)

因为不失一般性，\(\theta \ge 1\)。由此可得 \(\alpha^{j-1} E^{V,x}[y_j] \to 0\) 当 \(j \to \infty\)。因此最大解和最小解重合，存在唯一性。

在 \( U \) 不是紧集的情况下，可以在以下情形下获得唯一性

(4.5.4)
\( h|x| + c|v| \le l(x, v) \)
\( \Phi^v(\Phi^0)^{j-1}|x| \ge (\Phi^0)^j|x|, \forall j, \forall v \in U \)

### 定理 4.8.

我们采用定理 4.7 的假设，但将 \( U \) 紧集替换为 (4.5.4)。那么我们在 \( B_1 \) 中拥有函数方程 (4.3.7) 解的存在性和唯一性。

### 证明. 证明包括在等式 (4.3.7) 右边找到 \( v \) 的一个先验界。我们将证明只需取 \( v \in U \) 使得

\( |v| \le \frac{l_0}{1-\alpha}, \)

然后我们可以假设 \( U \) 是紧集。确实，从 (4.3.7) 和对 \( l(x, v) \) 的假设出发，我们可以验证解 \( u(x) \) 必须满足

\( u(x) \ge h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|. \)

因此

\( l(x, v) + \alpha \Phi^v u(x) \ge c|v| + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|, \)

因此只需寻找 \( v \) 使得

\( c|v| + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x| \le w_0(x). \)

但是（回顾 \( v_0 = 0 \)）

\( w_0(x) \le \frac{l_0}{1-\alpha} + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|, \)

因此只需选取 \( |v| \le \frac{l_0}{c(1-\alpha)}. \)

本页故意留空

## 没有设置成本的库存控制

在本章中，我们将第 4 章的一般结果应用于库存控制的情况。我们将考虑不允许缺货（无积压）和允许缺货（积压）的情况。在不允许缺货的情况下，无法满足的需求将丢失，并产生罚金。设置成本的情况将在第 9 章中考虑。

### 5.1. 不允许缺货.

### 5.1.1. 问题的提出.

我们处于第 4 章第 4.2.3 节的情况。如果 \( y_n \) 表示时刻 n 的库存，则有演化

(5.1.1) \( y_{n+1} = (y_n + v_n - D_n)^+ \quad y_1 = x, \)

其中 \( v_n \) 是时刻 n 的控制，\( D_n \) 是需求，它是一组独立随机变量的序列，概率密度为 \( f(x) \)。我们用 \( F(x) \) 表示与 \( f(x) \) 关联的累积分布函数（CDF）。控制策略（称为 \( V \)）由一组可测函数 \( v_n(D_1, \cdots D_{n-1}) \) 定义。对于 \( n=1 \)，\( v_1 \) 只是一个确定数。引入 \(\sigma\)-代数 \( \mathcal{F}^n = \sigma(D_1, \cdots D_{n-1}) \)，\( v_n \) 是 \( \mathcal{F}^n \) 可测的。算子 \( \Phi^v \) 由

(5.1.2) \( \Phi^v \varphi(x) = E\varphi((x+v-D)^+). \)

给出。

转移概率由

(5.1.3) \( \pi(x, v; d\eta) = \bar{F}(x+v)\delta(\eta) + f(x+v-\eta)\mathbb{1}_{\eta \le x+v} d\eta, \)

给出，因此

(5.1.4) \( \Phi^v \phi(x) = \bar{F}(x+v)\phi(0) + \int_0^{x+v} f(x+v-\eta)\phi(\eta)d\eta. \)

集合 \( U = [0, \infty) \) 不是紧集。算子 \( \Phi^v \) 对测试函数 \( \phi(x, v) \) 的像由

(5.1.5) \( \Phi^v \phi_0(x) = \phi(0,v)\bar{F}(x+v) + \int_0^{x+v} \phi(x+v-\eta, v)f(\eta)d\eta, \)

给出，且假设 (4.3.1) 得到满足。

我们定义函数 \( l(x, v) \) 如下

(5.1.6) \( l(x, v) = cv + hx + p \int_{x+v}^{\infty} (\xi - x - v)f(\xi)d\xi. \)

它包含订购成本（纯变动成本）、持有成本和失去销售的罚金。我们注意到不等式

(5.1.7) \( cv + hx \le l(x, v) \le cv + hx + p\bar{D}, \)



其中 $D = \int_0^\infty \xi f(\xi) d\xi$. 事实上

(5.1.8) $$l(x, v) = cv + hx + pE(D - x - v)^+,$$

最后一项是在需求未得到满足时产生的惩罚成本。请注意，假设 (4.5.4) 已满足。

而且 $$\Phi^{hv} l_v(x) \le cv + hx + p\bar{D} + hv.$$

更一般地 $$(\Phi^n)^{hv} l_v(x) \le cv + hx + p\bar{D} + nhv.$$

此外，记 $x$ 为恒等函数 $x \to x$，则有 (5.1.9) $$\Phi^v x(x) = E(x + v - D)^+ \le x + v,$$

因此，假设 (4.5.2) 已满足，其中 $\theta = 1$ 且 $\lambda = 1, \mu = 0$.

## 5.1.2. 贝尔曼方程。

我们可以应用定理 4.8 的结果。函数方程 (4.3.7) 为

(5.1.10) $$u(x) = \inf_{v \ge 0} \left\{ l(x, v) + \alpha \left( u(0)\bar{F}(x+v) + \int_0^{x+v} u(x+v-\eta) f(\eta) d\eta \right) \right\}.$$

将 (5.1.10) 视为一对 $u(\cdot), \lambda$ 的系统很方便，其中 $u(\cdot)$ 是具有线性增长的局部可积函数，$\lambda$ 是正实数。该系统写为

(5.1.11) $$\begin{aligned} u(x) &= \inf_{v \ge 0} \left\{ l(x, v) + \alpha \left( \lambda \bar{F}(x+v) + \int_0^{x+v} u(x+v-\eta) f(\eta) d\eta \right) \right\} \\ \lambda &= \inf_{v \ge 0} \left\{ l(0, v) + \alpha \left( \lambda F(v) + \int_0^v u(v-\eta) f(\eta) d\eta \right) \right\} \end{aligned}$$

自然地，解 $u(x)$ 是连续的且 $u(0) = \lambda$。而且，(5.1.11) 右边极小值的自变量 $v$ 可以取为被 $p\bar{D} / c(1-\alpha)$ 界定。

回顾 $B_1$ 的定义，即线性增长函数空间，在当前情形下（自变量位于 $R^+$ 中），它简化为

$$u \in B_1 \Longleftrightarrow \frac{|u(x)|}{1+x} \le C.$$

作为定理 4.8 的结果，我们可以断言

定理 5.1. 假设 (5.1.2) 和 (5.1.6)。那么系统 (5.1.11) 在空间 $B_1 \times R$ 中有唯一解。函数 $u(x)$ 是连续的且 $\lambda = u(0)$。而且，$u(x)$ 是控制问题的值函数

$$u(x) = \inf J_x(V),$$

其中

(5.1.12) $$J_x(V) = E \left[ \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n) \right].$$

此外，存在一个最优控制，它由反馈 $\hat{v}(x)$ 得到，该反馈是一个博雷尔函数，取得 (5.1.11) 右边的极小值。有 $\hat{v}(x) \le \frac{p\bar{D}}{c(1-\alpha)}$。

注释。我们没有使用 4.2.1 节为一般马尔可夫链开发的 $P^{V,x}$ 构造，因为我们有 4.2.3 节中描述的表述。

## 5.1.3. 基准库存策略。

在本节中，我们将验证 $\hat{v}(x)$ 实际上非常简单，并由所谓的基准库存策略所表征。基准库存策略由一个数 $S$ 和公式表征

(5.1.13) $$
\hat{v}(x) = \begin{cases} S - x, & \text{if } x \le S \\ 0, & \text{if } x \ge S \end{cases}
$$

定理 5.2. 在假设 (5.1.2) 和 (5.1.6) 以及 $p > c$ 下，最优反馈是一个基准库存策略。函数 $u$ 是凸的且为 $C^1$。基准库存由公式给出

(5.1.14) $$
F(S) = \frac{c(1-\alpha) + \alpha h}{p - \alpha c + \alpha h}.
$$

有

(5.1.15) $$
u(S) = (h-c)S + \frac{cS + pE(S-D)^-}{1-\alpha} + (h-c)\frac{\alpha}{1-\alpha}E(S-D)^+.
$$

令

(5.1.16) $$
g(x) = (c + \alpha(h-c) - (p + \alpha(h-c))F(x))^+,
$$

则 $u'(x) = h - c + z(x)$，其中

(5.1.17) $$
z(x) = \sum_{n=1}^{\infty} \alpha^{n-1} g \star f^{*(n-1)},
$$

且 $\varphi \star \psi$ 表示卷积乘积

$$
\varphi \star \psi(x) = \int_0^x \varphi(x-\xi)\psi(\xi) d\xi,
$$

且 $f^{*(0)}(x) = \delta(x)$, $f^{*(1)}(x) = f(x)$.

证明。注意 $S$ 是唯一确定的，归功于假设 $p > c$。而且 $g(x) = 0$，当 $x \le S$ 时。因此 $z = 0$，当 $x \le S$ 时。级数 $z(x)$ 收敛，因为 $f$ 是有界的。

回顾

$$
l(x,v) = cv + hx + pE(x+v-D)^-,
$$

我们也可以写

$$
l(x,v) = (h-c)x + l_0(x+v),
$$

其中

$$
l_0(x) = cx + pE(x-D)^-.
$$

因此，方程 (5.1.11) 也可以写为

(5.1.18) $$
u(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v) + \alpha Eu((x+v-D)^+)\}.
$$

函数 $l_0(x)$ 在 $R^+$ 上是连续凸函数，并且当 $x \to +\infty$ 时趋于 $+\infty$。

存在唯一的 $S_0$ 使得

$$
l_0(S_0) = \inf_{x \ge 0} l_0(x).
$$

考虑递增序列。我们从 $u_1(x)$ 开始。显然我们可以写

$$
u_1(x) = \begin{cases} 
(h - c)x + l_0(S_0), & \forall x \le S_0 \\ 
(h - c)x + l_0(x), & \forall x \ge S_0 
\end{cases}
$$

其导数为

$$
(u_1)'(x) = \begin{cases} 
h - c, & \forall x < S_0 \\ 
h - c + (l_0)'(x), & \forall x > S_0 
\end{cases}
$$

该函数是连续且递增的，由此可知 $u_1(x)$ 是连续凸函数，并且当 $x \to +\infty$ 时趋于 $+\infty$。更一般地，假设

$$
\zeta_n(x) = l_0(x) + \alpha Eu_n((x - D)^+),
$$

是连续凸函数，并且当 $x \to +\infty$ 时趋于 $+\infty$。因此存在一个唯一的 $S_n$，定义为函数 $\zeta_n(x)$ 在 $x \ge 0$ 上的最小最小值（如果最小值不唯一）。因此我们可以写

$$
u_{n+1}(x) = \begin{cases} 
(h - c)x + \zeta_n(S_n), & \forall x \le S_n \\ 
(h - c)x + \zeta_n(x), & \forall x \ge S_n 
\end{cases}
$$

由此可得

$$
u'_{n+1}(x) = h - c + \zeta'_n(x)\mathbb{I}_{x > S_n},
$$

这是 $x$ 的一个递增函数。因此 $u_{n+1}(x)$ 也是一个连续凸函数，并且当 $x \to +\infty$ 时趋于 $+\infty$。然后考虑 $\zeta_{n+1}(x)$。我们有

$$
\begin{aligned}
\zeta'_{n+1}(x) &= l'_0(x) + \alpha E u'_{n+1}(x - D)\mathbb{I}_{x > D} \\
&= l'_0(x) + \alpha(h - c)F(x) + \alpha E \zeta'_n(x - D)\mathbb{I}_{x - D > S_n} \\
&= c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x) + \alpha E \zeta'_n(x - D)\mathbb{I}_{x - D > S_n},
\end{aligned}
$$

且该函数在 $x$ 中是递增的。因此 $\zeta_{n+1}(x)$ 是连续凸函数，并且当 $x \to +\infty$ 时趋于 $+\infty$。

由于所有 $u_m, \zeta_n$ 函数都是凸的，极限 $u, \zeta$ 也是凸的，且

$$
\zeta(x) = l_0(x) + \alpha Eu((x - D)^+).
$$

由于对任意 $x$ 都是凸且有限的，它们在 $x > 0$ 处也是连续的。它们也当 $x \to +\infty$ 时趋于 $+\infty$。因此最优反馈由基准库存 $S$ 定义，即 $\zeta(x)$ 的最小最小值。接下来，由 (5.1.18) 我们可以写

$$
u(x) = \begin{cases} 
(h - c)x + l_0(S) + \alpha Eu((S - D)^+), & \forall x \le S \\ 
(h - c)x + l_0(x) + \alpha Eu((x - D)^+), & \forall x \ge S 
\end{cases}
$$

由于 $(S - D)^+ \le S$。我们可以轻松计算

$$
Eu((S - D)^+) = \frac{(h - c)E(S - D)^+ + l_0(S)}{1 - \alpha},
$$

因此公式 (5.1.15) 得证。接下来

$$
\zeta'(x) = l'_0(x) + \alpha E[u'((x - D)^+)\mathbb{I}_{x > D}].
$$

我们表达 \(\zeta'(S) = 0$ 的事实。但是 \(u'((S-D)^+) = h - c$。然后 \(\zeta'(S)$ 可以轻松表达。公式 (5.1.14) 易得。还可得 \(u'(x)$ 在 \(S$ 处是连续的，因此 \(u(x)$ 是 \(C^1$。我们接下来定义

$$
\begin{aligned}
z(x) &= u'(x) - (h-c) \\
&= \zeta'(x) \mathbf{1}_{x \ge S}.
\end{aligned}
$$

对上述 \(x \ge S$ 时的 \(u(x)$ 表达式求导，我们得到

$$
z(x) = l'_0(x) + \alpha(h-c)F(x) + \alpha E[z(x-D)\mathbf{1}_{x \ge D}].
$$

注意到 \(z(x) = 0, \forall x \le S$，我们可以将此方程写为

$$
z(x) = g(x) + \alpha E z(x-D),
$$

该方程的解由级数 (5.1.17) 给出。证明完成。

我们已引入条件 \(p > c$。现在让我们考虑 \(c \ge p$ 的情况。

定理 5.3. 在假设 (5.1.2) 和 (5.1.6) 以及 \(p \le c$ 下，则 \(u(x) = u_0(x)$。因此 $\hat{v}(x) = 0$。

证明。考虑用递增序列逼近 $u$。我们有

$$
u_1(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v)\},
$$

但是，由假设 $l_0(x)$ 是单调递增的。因此

$$
u_1(x) = (h-c)x + l_0(x).
$$

然后

$$
u_2(x) = (h-c)x + \inf_{v \ge 0} \{l_0(x+v) + \alpha E u_1((x+v-D)^+)\}.
$$

但是

$$
l_0(x) + \alpha E u_1((x-D)^+) = l_0(x) + \alpha(h-c)E(x-D)^+ + \alpha E l_0((x-D)^+).
$$

由于 $l_0$ 是单调递增的，右边的最后一项是单调递增的。如果我们对前两项求导，我们得到

$$
l'_0(x) + \alpha(h-c)F(x) = c + \alpha(h-c) - (p + \alpha(h-c))F(x) \ge 0.
$$

因此 $l_0(x) + \alpha E u_1((x-D)^+)$ 是单调递增的，且极小值再次在 $v = 0$ 处取得，我们有

$$
u_2(x) = (h-c)x + l_0(x) + \alpha E u_1((x-D)^+).
$$

通过归纳，我们检查 $l_0(x) + \alpha E u_n((x-D)^+)$ 是单调递增的，且

$$
u_{n+1}(x) = (h-c)x + l_0(x) + \alpha E u_n((x-D)^+).
$$

因此

$$
u(x) = (h-c)x + l_0(x) + \alpha E u((x-D)^+),
$$

因此 $u(x) = w_0(x)$ 且 $\hat{v}(x) = 0$。证明已完成。





**注 5.1.** 基准库存政策满足 $\hat{v}(x) \le S$. 我们在定理 5.1 中已经看到 $\hat{v}(x) \le \frac{pD}{c(1-\alpha)}$. 让我们验证 $S \le \frac{pD}{c(1-\alpha)}$. 这由公式 (5.1.14) 得出。确实，我们有

$$D \ge SF(S) = S \frac{c(1-\alpha)+\alpha h}{p-\alpha c+\alpha h} \ge S \frac{c(1-\alpha)}{p},$$

由此得出结果。

假设 $x \le S$. 如果我们应用基准库存政策，那么库存永远不会大于 $S$. 因此我们在每个期都会下单，并且有

$y_n + v_n = S \quad n \ge 1$
$y_n = (S - D_{n-1})^+ \quad n \ge 2$

所以第一期的成本是 $(h-c)x+l_0(S)$，所有后续期的成本相同，等于 $(h-c)E(S-D)^+ + l_0(S)$. 因此总成本是

$$u(x) = (h-c)x + l_0(S) + \frac{\alpha}{1-\alpha}[(h-c)E(S-D)^+ + l_0(S)],$$

并且我们恢复了通过动态规划所获得的结果，并且通过对 $S$ 求导，我们恢复了 (5.1.14) 中的值。这种快速获得正确基准库存的方法不是动态规划的替代方案，因为它不能证明基准库存政策是最优的。它只是在 $S$ 的值上对基准库存政策进行的一种优化。我们可以对 $n \ge 2$ 表示 $v_n$，如下

$$v_n = \min(S, D_{n-1}).$$

如果取 $x = S$，这种方法可能具有误导性。有人可能会想在 $S$ 中最小化以下量

$$(h-c)S + l_0(S) + \frac{\alpha}{1-\alpha}[(h-c)E(S-D)^+ + l_0(S)],$$

这将导致一个错误的值。

## 5.2. 允许缺货

### 5.2.1. 问题陈述。

我们考虑库存 $y_n$ 的以下演化

$$y_{n+1} = y_n + v_n - D_n \quad y_1 = x,$$

其中需求 $D_n$ 是一组独立随机变量的序列，具有概率密度函数 $f(x)$ 和累积分布函数 $F(x)$. 算子 $\Phi^v$ 定义为

$$\Phi^v \phi(x) = E\phi(x+v-D) = \int_{-\infty}^{x+v} f(x+v-\eta)\phi(\eta)d\eta,$$

转移概率由以下给出

$$\pi(x, v; d\eta) = f(x+v-\eta)1_{\eta<x+v}d\eta.$$

控制策略 $v_n$ 同样是一组相对于过滤族 $\mathcal{F}^n = \sigma(D_1, \cdots D_{n-1})$ 可测的随机变量序列。我们引入每期成本

$$l(x, v) = cv + hx^+ + px^-,$$

其中 \(c\) 是每单位订单的变动成本，\(h\) 是每单位持有成本，\(p\) 是每单位缺货成本。我们接下来定义控制收益

$$
(5.2.4) \qquad J_z(V) = \sum_{n=1}^{\infty} \alpha^{n-1} E l(y_n, v_n).
$$

值函数 \( u(x) = \inf J_z(V) \) 是贝尔曼方程的解

$$
(5.2.5) \qquad u(x) = \inf_{v \ge 0} [l(x, v) + \alpha E u(x + v - D)].
$$

### 5.2.2. 贝尔曼方程。

考虑上界函数

$$
(5.2.6) \qquad w_0(x) = \sum_{n=1}^{\infty} \alpha^{n-1} (\Phi^0)^{n-1} (hx^+ + px^-)(x).
$$

很容易检查这个级数定义良好，并且

$$
(5.2.7) \qquad w_0(x) \le \max(h, p) \left[ \frac{|x|}{1-\alpha} + \frac{\bar{D}}{(1-\alpha)^2} \right].
$$

假设 (4.3.1)、(4.3.2)、(4.3.6) 得到满足。因此定理 4.3、4.4、4.5 的结果适用。我们可以声明

> **定理 5.4.** 在假设 (5.2.2)、(5.2.3) 下，函数方程 (5.2.5) 在区间 \( 0 \le u \le w_0 \) 内的解集非空，并具有一个最小解 \(\underline{u}\) 和一个最大解 \(\bar{u}\)。最小解是下半连续的。它与值函数重合。存在一个最优控制策略，通过反馈 \(\tilde{v}(x)\) 获得。

我们现在转向唯一性问题。我们可以检查性质 (4.5.1)、(4.5.2) 得到满足。然而，只有性质 (4.5.4) 的第一部分得到满足。因此我们不能直接应用定理 4.8。因此情况与定理 5.1 不同。关键问题是获得对反馈 \(\tilde{v}(x)\) 的估计。在高负库存的情况下，反馈不会有界。我们可以声明以下重要结果

> **命题 5.1.** 最优反馈满足

$$
(5.2.8) \qquad \tilde{v}(x) \le x^- + \frac{\alpha \bar{D}}{c(1-\alpha)^2} [h + (p+c)(1-\alpha)].
$$

证明。我们首先从下方对值函数进行估计。我们将检查

$$
(5.2.9) \qquad u(x) \ge \frac{hx^+}{1-\alpha} + px^- - \frac{h\alpha \bar{D}}{(1-\alpha)^2}.
$$

这个估计通过归纳法证明。我们从以下开始

$$u(x) \ge hx^+ + px^-,$$

然后，在方程 (5.2.5) 的右侧使用 \( u(x) \ge hx^+ \)，我们得到

$$
\begin{aligned}
u(x) \ge {} & hx^+ + px^- + \alpha h E(x - D)^+ \\
\ge {} & hx^+ + px^- + \alpha h(x^+ - \bar{D}) \\
= {} & hx^+ (1 + \alpha) + px^- - \alpha h \bar{D}.
\end{aligned}
$$

再次迭代，我们得到

$$u(x) \ge hx^+ (1 + \alpha + \alpha^2) + px^- - (\alpha + 2\alpha^2)h \bar{D},$$

一般来说

$$u(x) \ge hx^+(1 + \alpha + \cdots + \alpha^n) + px^- - (\alpha + 2\alpha^2 + \cdots + n\alpha^n)h\bar{D},$$

并令 \(n \to \infty\)，即可得到 (5.2.9)。

下一步是用一个合适的函数来最小化 \(u(x)\)。我们不使用 \(w_0(x)\)，而是使用函数 \(w(x)\)，它是以下方程的解

$$
(5.2.10) \qquad w(x) = (c+p)x^- + hx^+ + \alpha Ew(x^+ - D).
$$

我们声称 \(u(x) \le w(x)\)。确实，(5.2.10) 对应于使用反馈 \(x^-\) 时的收益。我们声称以下估计成立

$$
(5.2.11) \qquad w(x) \le (c+p)x^- + \frac{hx^+}{1-\alpha} + L,
$$

对于一个合适的常数 \(L\)。这可以通过归纳法检查，但为了确定常数 \(L\) 的值，我们假设 (5.2.10)，将其代入 (5.2.10) 的右侧。我们得到

$$w(x) \le (c+p)x^- + \frac{hx^+}{1-\alpha} + \alpha(p+c)\bar{D} + \alpha L,$$

如果以下条件成立，这将低于 (5.2.11) 的右侧

$$L \ge \frac{\alpha(p+c)\bar{D}}{1-\alpha},$$

因此我们可以取 \(L\) 的下界。

现在，回到函数方程 (5.2.5)，我们通过使用以下内容来最小化右侧括号内的量

$$u(x) \ge \frac{hx^+}{1-\alpha} - \frac{h\alpha\bar{D}}{(1-\alpha)^2}.$$

我们看到它被以下内容下界化

$$cv + \frac{hx^+}{1-\alpha} + px^- - \frac{h\alpha\bar{D}}{(1-\alpha)^2}.$$

因此，在寻找下确界时，我们可以将控制 \(v\) 限制在以下集合中

$$cv + \frac{hx^+}{1-\alpha} + px^- - \frac{h\alpha\bar{D}}{(1-\alpha)^2} \le w(x).$$

然后使用对 \(w(x)\) 的估计，我们推断可以将 \(v\) 的集合限制为由 (5.2.8) 的右侧界定。最优反馈必须满足这个界限，因此得到结果 (5.2.8)。

我们然后可以证明 (5.2.5) 在空间 \(B_1\) 中的解是唯一的，其中

$$u \in B_1 \iff \frac{|u(x)|}{1+|x|} \le C.$$

**定理 5.5.** 在假设 (5.2.2)、(5.2.3) 下，(5.2.5) 在空间 \(B_1\) 中的解是唯一的。而且 \(u\) 是连续的。

证明。像往常一样，我们将检查最小解和最大解是否重合。定义与最优反馈相关的最优控制。如果我们用 $\bar{V} = (\bar{v}_1, \cdots, \bar{v}_n, \cdots)$ 表示最优控制，用 $\{\bar{y}_1, \cdots, \bar{y}_n, \cdots\}$ 表示最优轨迹，我们必须证明 $\bar{V}$ 属于 $\mathcal{V}$，这意味着

$$\alpha^{j-1} E[\hat{y}_j] \to 0,$$

当 $j \to \infty$ 时。然而，从估计 (3.8) 并设定

$$C = \frac{c \alpha \bar{D}}{c(1-\alpha)^2} [h + (p+c)(1-\alpha)],$$

我们可以声明

$$\hat{y}_{n+1} \le \hat{y}_n^+ + C,$$

因此

$$\hat{y}_{n+1} \le x^+ + nC.$$

另一方面

$$\hat{y}_{n+1} \ge x - D_1 - \cdots - D_n.$$

因此

$$x - n\bar{D} \le E\hat{y}_{n+1} \le x^+ + nC,$$

条件得到满足，因此得到结果。

### 5.2.3. 基准库存政策

我们想要展示以下结果

### 定理 5.6. 我们假设 (5.2.2)、(5.2.3) 并且

$$c(1-\alpha) < p\alpha,$$

那么函数 $u$ 是凸的且 $C^1$，除了 $x=0$ 之外。最优反馈由基准库存政策给出，其中基准库存 $S$ 是以下方程的解

$$F(S) = \frac{c(1-\alpha) + \alpha h}{\alpha(p+h)}.$$

还具有

$$u(S) = hS + \frac{\alpha}{1-\alpha} [c\bar{D} + hE(S-D)^+ + pE(S-D)^-].$$

定义

$$g(x) = (c(1-\alpha) + \alpha h - \alpha(h+p)\bar{F}(x))^+,$$

那么函数 $z(x) = u'(x) + c - h \mathbb{I}_{x>0} + p \mathbb{I}_{x<0}$ 由以下给出

$$z(x) = \sum_{n=1}^{\infty} \alpha^{n-1} g * f^{*(n-1)},$$

与方程 (5.1.17) 中相同的记号。

证明。凸性通过考虑以下单调递增序列来证明

$$u_{n+1}(x) = hx^+ + px^- - cx + \inf_{v \ge 0} [c(x+v) + c\alpha E u_n(x+v-D)],$$

其中 $u_1(x) = l_0(x) = hx^+ + px^-$. 存在一个唯一的 $n_0 \ge 0$ 使得

$$\frac{\alpha p}{1-\alpha} (1 - \alpha^{n_0+1}) > c > \frac{\alpha p}{1-\alpha} (1 - \alpha^{n_0}).





如果 $n_0 = 0$，则意味着 $c < \alpha p$。我们声称

$$
u_n(x) = \sum_{j=1}^n \alpha^{j-1} (\Phi^{(j-1)} l_0)(x), \forall 1 \le n \le n_0 + 1.
$$

确实，我们有（此处我们将 $u_n(x)$ 用作该表达式中求和的定义）

$$
u'_n(x) = -p \frac{1-\alpha^n}{1-\alpha}, \forall x < 0
$$

因此

$$
c - \alpha p \frac{1-\alpha^n}{1-\alpha} > 0, \forall n \le n_0.
$$

因此，对于 $0 \le n \le n_0$，$cx + \alpha E u_n(x - D)$ 是递增的，从而 $u_n$ 是方程 (5.2.17) 的解，对 $0 \le n \le n_0$ 成立，这意味着该声明成立。

对于 $n \ge n_0 + 2$，存在 $S_n > 0$，使得

$$
c + \alpha E u'_n(S_n - D) = 0,
$$

且

$$
u_{n+1}(x) = \begin{cases} hx^+ + px^- - cx + cS_n + \alpha E u_n(S_n - D), & x < S_n \\ hx + \alpha E u_n(x - D), & x \ge S_n \end{cases}
$$

该结果通过归纳法证明，注意到 $u_n(x)$ 是凸的，并且当 $|x| \to +\infty$ 时趋于 $+\infty$。注意 $u_n$ 是 $C^1$ 的，除了在 $x=0$ 处。这证明了递增序列是凸的，并且当 $|x| \to +\infty$ 时趋于 $+\infty$。由此可见，$u$ 是凸的，并且当 $|x| \to +\infty$ 时趋于 $+\infty$。将 Bellman 方程 (5.2.5) 改写为

$$
u(x) = hx^+ + px^- - cx + \inf_{v \ge 0} [c(x+v) + \alpha E u(x+v-D)],
$$

我们可以看出，最优反馈由基准库存策略定义。

基准库存满足

$$
c + \alpha E u'(S - D) = 0,
$$

且

$$
E u(S - D) = \frac{c\bar{D} + h E(S-D)^+ + p E(S-D)^-}{1-\alpha}.
$$

此外，$S$ 是下式的解

$$
F(S) = \frac{c(1-\alpha) + \alpha b}{\alpha(p+h)}.
$$

我们很容易推导出 (5.2.14)。接下来，解 $u$ 可以写成

$$
u(x) = \begin{cases} -cx + hx^+ + px^- + cS + \frac{1}{1-\alpha} (c\bar{D} + h E(S-D)^+ + p E(S-D)^-), & \forall x \le S \\ hx^+ + px^- + \alpha E u(x-D), & \forall x \ge S \end{cases}
$$

我们可以看出，$u$ 是 $C^1$ 的，除了在 $x=0$ 处。按照定理陈述定义 $z$ 和 $g$，我们很容易看出 $z$ 是下式的解

$$
z(x) = g(x) + \alpha E z(x - D),
$$

该式由公式 (5.2.16) 求解。证明已完成。

我们现在可以转到 $c(1-\alpha) \ge \alpha p$ 的情况。我们有

### 定理 5.7.

我们假设 (5.2.2)、(5.2.3) 以及 \(c(1-\alpha) \ge \alpha p\)。则 \(u(x) = w_0(x)\)，其中

(5.2.19) \(w_0(x) = \sum_{j=1}^{\infty} \alpha^{j-1} (\Phi^0)^{j-1} l_0(x).\)

因此 \(\dot{v}(x) = 0\)。

### 证明.

事实上，如果我们查看前述定理的证明，当前假设对应于 $n_0 = +\infty$ 的情况。我们随后看到递增序列收敛于 $w_0(x)$。这证明了结果。

### 注释 5.2.

我们在提议 5.1 中得到了 \(\bar{v}(x) \le x^- + C\)。此外，根据基准库存策略，我们还有 \(\dot{v}(x) \le x^- + S\)。我们必须检查 $S \le C$。再次使用 $D \ge S\bar{F}(S)$，我们可以断言

\(\bar{D} \ge S \frac{c(1-\alpha) + \alpha h}{\alpha(p+h)},\)

因此

\(\frac{C}{S} \ge \frac{[h + (p+\alpha)(1-\alpha)](c(1-\alpha) + \alpha h)}{c(p+h)(1-\alpha)^2},\)

且右侧常数大于 1。

我们还有一个与注释 5.1 类似的注释

### 注释 5.3.

假设 \(x \le S$。如果我们应用基准库存策略，则我们将在每个时期下订单，并且有

\(y_n + v_n = S \quad n \ge 1\)
\(y_n = S - D_{n-1} \quad n \ge 2\)

因此 \(v_n = D_{n-1}$。由此可见，基准库存策略的成本是

\(u(x) = hx^+ + px^- + c(S-x) + \frac{\alpha}{1-\alpha}(c\bar{D} + hE(S-D)^+ + pE(S-D)^-),\)

并在 \(S$ 中最小化该表达式得到公式 (5.2.13)。

## 5.3. 确定性情况

确定性情况是随机情况的一个特例，除了平滑性之外。我们假设在每个时期面临固定需求 \(D$。我们简要描述结果。

### 5.3.1. 不允许缺货。

库存演变如下

(5.3.1) \(y_{n+1} = (y_n + v_n - D)^+ \quad y_1 = x,\)

成本泛函为

(5.3.2) \(J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n),\)

其中

(5.3.3) \(l(x,v) = (h-c)x + l_0(x+v),\)

且

(5.3.4) \(l_0(x) = cx + p(x-D)^-.\)

Bellman 方程为

(5.3.5) \( u(x) = (h - c)x + \inf_{v \ge 0} \{ l_0(x + v) + \alpha u((x + v - D)^+) \} \).

解 \( u(x) \) 是连续凸的，并且当 \( x \to +\infty$ 时趋于 \( +\infty \)。我们需要小心可微性。我们关注 \( l_0(x) + \alpha u((x - D)^+) \) 的最小值。如果 \( S \) 是最小值，则对于 \( x \le S \)，\( u(x) = (h - c)x + C$，因此对于 \( x \le S \)，我们有

\( l_0(x) + \alpha u((x - D)^+) = l_0(x) + \alpha(h - c)(x - D)^+ + \alpha C. \)

因此，我们必须有

\( l_0(x) + \alpha(h - c)(x - D)^+ \ge l_0(S) + \alpha(h - c)(S - D)^+, \quad \forall x < S. \)

回顾

\( l_0(x) + \alpha(h - c)(x - D)^+ = cx + p(x - D)^- + \alpha(h - c)(x - D)^+, \)

我们很容易看出，如果 \( p \ge c \)，则以唯一方式实现，其中 \( S = D$。如果 \( c > p \)，则 \( S = 0$。

因此，如果 \( p \ge c \)，我们有

\( u(x) = (h - c)x + \frac{cD}{1 - \alpha}, \quad \forall x \le D. \)

### 5.3.2. 允许积压。

在积压的情况下，我们有

(5.3.6) \( y_{n+1} = y_n + v_n - D \quad y_1 = x, \)

成本泛函为

(5.3.7) \( J_x(V) = \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n), \)

其中

\( l(x, v) = hx^+ + px^- + cv. \)

Bellman 方程变为

(5.3.8) \( u(x) = hx^+ + px^- - cx + \inf_{v \ge 0} \{ c(x + v) + \alpha u(x + v - D) \} \).

我们关注函数 \( cx + \alpha u(x - D) \) 的最小值。如果 \( S \) 是该最小值，则对于 \( x \le S \)，

\( u(x) = hx^+ + px^- - cx + C, \)

因此，对于 \( x \le S \)，函数 \( cx + \alpha[h(x - D)^+ + p(x - D)^- - c(x - D) + C] \) 必须在 \( S$ 处取得其最小值。我们得到，如果 \( cp \ge c(1 - \alpha) \)，则必然 \( S = D$，而如果 \( cp < c(1 - \alpha) \)，则必然 \( S = 0$。因此

\( u(x) = hx^+ + px^- - cx + \frac{cD}{1 - \alpha}, \quad \forall x \le D \)

## 离散时间中的遍历控制

在前几章中，我们始终考虑折扣因子 \(\alpha < 1$ 的控制问题。遍历控制问题对应于 \(\alpha = 1$ 的情况。这是一种极限情况，我们不能直接在公式中取 \(\alpha = 1$。值函数变为无穷大。我们在第 3 章中研究了无控制的情况。在本章中，我们发展了受控马尔可夫链的相应理论。

### 6.1. 有限状态数

我们在此研究马尔可夫链的最简单情况，即有限状态数。

### 6.1.1. 假设-记号。

我们考虑一个具有有限状态数的受控马尔可夫链。状态空间记为 \(X\)，转移概率归约为一个矩阵，定义为 \(\varpi^u(i, j) = P(y_{n+1} = j | y_n = i)$，其中 \(y_n$ 表示标准过程（时刻 \(n$ 时系统的状态）。控制 \(v \in U$。我们假设

- (6.1.1)
- U 紧集
- \(\varpi^u(i, j)\) 在 \(v\) 中连续，\(\forall i, j\)
- \(\varpi^u(i, j) > 0, \forall i, j, v\)

注意，此假设意味着下界一致有界，因为我们在紧集上有有限个严格连续函数。我们写

(6.1.2) \(\varpi^u(i, j) \ge \delta > 0.\)

我们用 \(\Phi^u$ 表示与矩阵 \(\varpi^u$ 关联的算子。我们回顾

\(\Phi^u f(i) = \sum_j \varpi^u(i, j) f(j).\)

此公式扩展到反馈 \(v(.)$。我们将通过以下方式定义 \(\Phi^{v(.)} f$：

\(\Phi^{v(.)} f(i) = \sum_j \varpi^{v(i)}(i, j) f(j).\)

与算子 \(\Phi^{v(.)}$ 关联的是转移矩阵 \(\varpi^{v(i)}(i, j)$。我们显然具有性质

(6.1.3) \(\varpi^{v(i)}(i, j) \ge \delta, \forall i, j\)

### 6.1.2. 遍历性质。

由于 (6.1.3)，对于任何给定的反馈，第 3 章中的性质 (3.5.2) 得到满足。因此将存在一个唯一的不变测度，记为 $m^{v(\cdot)}$，使得

(6.1.4) $$ \sum_i m_i^{v(\cdot)} \varpi^{v(i)}(i,j) = m_j^{v(\cdot)}, \forall j. $$

注意，此不变测度与控制的特定值无关，而是结合了所有可能的控制值。存在一种考虑所有 v(i) 值的平均效应。对于任何 \(f \in B\)，我们具有性质

(6.1.5) $$ \left\| (\Phi^{v(\cdot)})^n f - \sum_j m_j^{v(\cdot)} f_j \right\| \le 2 ||f|| \beta^{n-1}, \forall f \in B, \text{ with } \beta = 1 - \delta $$

### 6.1.3. 动态规划。

考虑函数 \(f(i,v)$，使得

(6.1.6) $$ l(i,v) \text{ continuous (hence bounded), } l \ge 0. $$

遍历控制的 Bellman 方程定义为

(6.1.7) $$ z(i) + \lambda = \inf_{v \in U} [l(i,v) + \Phi^v z(i)]. $$

我们看到右侧没有 \(\alpha$。更准确地说，\(\alpha = 1$。左侧有一个常数 \(\lambda$，这在带折扣的 Bellman 方程中不存在。事实上，我们将对 \((z, \lambda)$ 视为非线性方程 (6.1.7) 的解。我们的主要结果如下

**定理 6.1.7.** 在假设 (6.1.1) 和 (6.1.6) 下，存在且仅存在一对 \(z, \lambda$ 是 (6.1.7) 的解。

### 证明.

我们考虑带有折扣项的 Bellman 方程

(6.1.8) $$ u_\alpha(i) = \inf_{v \in U} [l(i,v) + \alpha \Phi^v u_\alpha(i)], $$

并将让 \(\alpha$ 趋于 1。

该方程承认唯一解 \(u_\alpha$，并且还存在一个最优反馈 \(v_\alpha(i)$，使得

$$ u_\alpha(i) = l(i, v_\alpha(i)) + \alpha \Phi^{v_\alpha(\cdot)} u_\alpha(i). $$

我们可以断言

$$ (1 - \alpha) ||u_\alpha|| \le ||l|| = \max_{i,v} l(i,v). $$

对于任何固定的 \(\alpha\)，存在唯一的不变测度 \(m^{v_\alpha(\cdot)}\)，使得

$$ \left\| (\Phi^{v_\alpha(\cdot)})^n \phi - \sum_j m_j^{v_\alpha(\cdot)} \phi_j \right\| \le 2 ||\phi|| \beta^{n-1}. $$

如果我们定义函数 \(h_\alpha$ 使得

$$ h_\alpha(i) = l(i, v_\alpha(i)) - (1 - \alpha) \Phi^{v_\alpha(\cdot)} u_\alpha(i), $$

那么我们有

$$ u_\alpha(i) - \Phi^{v_\alpha(\cdot)} u_\alpha(i) = h_\alpha(i), $$

因此

$$ \sum_i m_i^{v_\alpha(\cdot)} h_\alpha(i) = 0. $$




考虑方程

$$u - \Phi^{u_\alpha(\cdot)}u = h_\alpha,$$

由构造可知 \(u_\alpha\) 是一个解。另一个解是

$$\zeta_\alpha = \sum_{n=1}^\infty (\Phi^{u_\alpha(\cdot)})^{n-1} h_\alpha.$$

但两个解仅相差一个常数。因此

$$u_\alpha(i) - \zeta_\alpha(i) = K_\alpha, \forall i.$$

由此可得

$$\min_i u_\alpha(i) - \min_i \zeta_\alpha(i) = K_\alpha,$$

因此

$$u_\alpha - \min_i u_\alpha(i) = \zeta_\alpha - \min_i \zeta_\alpha(i).$$

从 \(h_\alpha\) 的表达式可以看出，当 \(\alpha\) 趋近于 1 时它是有界的。因此，从 \(\zeta_\alpha\) 的表达式可以检查出，当 \(\alpha\) 趋近于 1 时它也是有界的。因此，我们已建立

$$u_\alpha(i) - \min_j u_\alpha(j) \le C,$$

其中常数不依赖于 \(\alpha\) 也不依赖于 \(i\)。令

$$z_\alpha = u_\alpha - \min_j u_\alpha(j).$$

它在 \(\alpha\) 中有界（注意它是正的）并满足

$$z_\alpha(i) + \lambda_\alpha = \inf_{v \in U} [l(i, v) + \alpha \Phi^{v(\cdot)} z_\alpha(i)],$$

其中 \(\lambda_\alpha = (1-\alpha) \min u_\alpha\)，也在 \(\alpha\) 中有界。

我们可以提取子序列 \(z_{\alpha_k}, \lambda_{\alpha_k}\)，它们在 \(B\) 中对 \(z_\alpha\) 收敛到一个函数 \(z\)，在 \(R\) 中对 \(\lambda_\alpha\) 收敛到一个数 \(\lambda\)。很容易检查，\(z, \lambda\) 这一对是方程 (6.1.7) 的一个解。

让我们检查唯一性。假设我们有两个解 \(z_1, \lambda_1, z_2, \lambda_2\)。存在反馈 \(v_1(i), v_2(i)\) 使得

$$z_1(i) + \lambda_1 = l(i, v_1(i)) + \Phi^{v_1(\cdot)} z_1(i)$$
$$z_2(i) + \lambda_2 = l(i, v_2(i)) + \Phi^{v_2(\cdot)} z_2(i).$$

还要注意

$$z_2(i) + \lambda_2 \le l(i, v_1(i)) + \Phi^{v_1(\cdot)} z_2(i).$$

因此也

$$z_1(i) - z_2(i) + \lambda_1 - \lambda_2 \ge \Phi^{v_1(\cdot)}(z_1 - z_2)(i).$$

因此

$$\min_i(z_1(i) - z_2(i)) + \lambda_1 - \lambda_2 \ge \min_i(z_1(i) - z_2(i)).$$

我们得到 \(\lambda_1 - \lambda_2 \ge 0\)，并且通过对称性，反之亦然。因此 \(\lambda_1 = \lambda_2\)。

我们随后有

$$z_1(i) - z_2(i) \ge \Phi^{v_1(\cdot)}(z_1 - z_2)(i),$$

因此也

$$z_1(i) - z_2(i) \ge (\Phi^{v_1(\cdot)})^n(z_1 - z_2)(i).$$

这意味着，使用右边的极限

$$z_1(i) - z_2(i) \ge \sum_j m_j^{v_{i_0}}(z_1(j) - z_2(j)).$$

如果 \(i_0\) 是 \(z_1(i) - z_2(i)\) 的最小值索引，我们必然有

$$z_1(i_0) - z_2(i_0) = \sum_j m_j^{v_{i_0}}(z_1(j) - z_2(j)).$$

这也意味着

$$m_j^{v_{i_0}}(z_1(i_0) - z_2(i_0)) = m_j^{v_{i_0}}(z_1(j) - z_2(j)), \forall j.$$

现在从属性 (6.1.3) 我们很容易得到 \(m_j^{v_{i_0}} > \delta, \forall j\)，因此

$$z_1(i_0) - z_2(i_0) = z_1(j) - z_2(j), \forall j,$$

这证明了 \(z\) 直到一个加法常数的唯一性。

### 6.1.4. 扩展。

事实上，假设 (6.1.1) 过于强烈。只需假设

(6.1.9)

- $U \text{ compact}$
- $\varpi^{v_0}(i,j) \text{ is continuous in } v, \forall i, j.$
- $\varpi^{v_0}(i,j) > 0, \forall i, j \text{ and some } v_0$

我们想证明定理 6.1 的以下改进

### **定理 6.2.** 在假设 (6.1.9) 和 (6.1.6) 下，存在且仅存在一对 $\lambda, z$，它是 (6.1.7) 的解。

证明。对转移矩阵 $\varpi^{v_0}(i,j)$ 对应一个唯一的不变测度 $m_i^{v_0}$。这些数严格为正。我们可以考虑其逆

$$q_i^{v_0} = \frac{1}{m_i^{v_0}}.$$

在以下内容中，我们省略索引 $v_0$ 以简化记法。我们将写 $\varpi(i,j), m_i, q_i$，并且 $\Phi$ 将表示算子 $\Phi^{v_0}$。

考虑系统

(6.1.10)

$$q_{ij} - \sum_{k \neq j} \varpi(i,k)q_{kj} = 1, \forall j$$
$$q_{jj} = q_j$$

我们有

### **引理 6.1.** 系统 (6.1.10) 有一个唯一的正解。

证明。系统可以重写如下

$$q_{ij} - \sum_k \varpi(i,k)q_{kj} = \theta_{ij},$$

其中

$$\theta_{ij} = 1 - \varpi(i,j)q_j,$$

并且我们有

$$\sum_i m_i \theta_{ij} = 1 - \sum_i m_i \varpi(i,j)q_j = 1 - m_j q_j = 0.$$

从 (6.1.5) 结果随之而来。解是

$$q = \sum_{n=1}^{\infty} \alpha^{n-1} \Phi^{n-1} \theta.$$

数字 $q_{ij}$ 具有概率解释。确实，$q_{ij}$ 表示从状态 $i$ 出发到达 $j$（如果 $j=i$ 则返回 $i$）的平均时间。更精确地，我们可以写

$$q_{ij} = \sum_{n=1}^{\infty} n f^{(n)}(i, j),$$

其中 $f^{(n)}(i, j)$ 是从 $i$ 到 $j$ 在恰好 $n$ 步中到达的概率。我们有递推公式

$$f^{(n)}(i, j) = \sum_{k \neq j} \varpi(i, k) f^{(n-1)}(k, j), n \ge 2$$
$$f^{(1)}(i, j) = \varpi(i, j).$$

关键估计如下给出

### **引理 6.2.** 方程 (6.1.8) 的解 $u_\alpha$ 满足估计

$$(6.1.11) \quad u_\alpha(i) - u_\alpha(j) \le ||I|| q_{ij}.$$

证明。考虑递增迭代

$$u_\alpha^{k+1}(i) = \inf_{v \in U} [l(i, v) + \alpha \Phi^v u_\alpha^k(i)],$$

起始于 $u_\alpha^0(i) = 0$。我们将检查

$$u_\alpha^k(i) - u_\alpha^0(j) \le ||I|| q_{ij}, \forall k.$$

这个不等式对 $k=0$ 显然成立。假设它对 $k$ 成立，然后注意到

$$u_\alpha^{k+1}(i) \le ||I|| + \alpha \sum_l \varpi(i, l) u_\alpha^k(l),$$

并且由于所有量都是正的

$$u_\alpha^{k+1}(i) \le ||I|| + \sum_l \varpi(i, l) u_\alpha^k(l).$$

使用递推我们得到

$$u_\alpha^{k+1}(i) \le ||I|| + \sum_{l \neq j} \varpi(i, l) u_\alpha^k(j) + ||I|| q_{ij} + \varpi(i, j) u_\alpha^k(j)$$
$$= ||I|| + u_\alpha^k(j) + ||I|| (q_{ij} - 1)$$
$$= u_\alpha^k(j) + ||I|| q_{ij}.$$

并且由于序列是递增的，该属性随之而来。

将引理应用于 $j$ 对应于 $u_\alpha(j)$ 最小值的索引，并通过主导化我们还得到

$$u_\alpha(i) - \min_j u_\alpha(j) \le ||I|| \max_{ij} q_{ij}.$$

有了这个估计，证明可以以与定理 6.1 证明相同的方式进行。

### 6.1.5. 概率解释。

我们的下一个目标是解释方程 (6.1.7) 的解。像往常一样，我们将定义一个决策规则

$V = (v_1, \cdots, v_n, \cdots),$

与

$v_n = v_n(i_1 \cdots i_n),$

作为 $U$ 中索引值的函数。对 $V$ 和 $i$ 对应于 $\Omega, \mathcal{A}$ 上的一个概率测度，底层概率空间。

我们定义成本函数

$J_i(V) = \lim_{N \to \infty} \frac{1}{N} \sum_{n=1}^N E^{V,i}(y_n, v_n),$

考虑极限存在的 $V$。类似地，定义

$\bar{J} (V) = \lim_{\alpha \to 1} (1 - \alpha) \sum_{n=1}^\infty \alpha^{n-1} E^{V,i}(y_n, v_n).$

我们声明如下

### **定理 6.3.** 如果方程 (6.1.7) 存在一个解 $z(i), \lambda$ 并且存在一个反馈 $\hat{v}(i)$ 使得

$z(i) + \lambda = l(i, \hat{v}(i)) + \Phi^{\hat{v}(i)} z(i),$

那么有

$\lambda = \inf_V J_i(V) = \inf_V \bar{J}_i(V) = J_i(\hat{V}) = \bar{J}_i(\hat{V}),$

其中 $\hat{V}$ 是与反馈 $\hat{v}(.)$ 关联的决策规则。

证明。考虑任何决策规则 $V$。我们可以从方程 (6.1.7) 写出

$\lambda + E^{V,i} z(y_n) \le E^{V,i}[l(y_n, v_n) + z(y_{n+1})], \forall n,$

并且对于 $\hat{V}$ 我们有

$\lambda + E^{\hat{V},i} z(y_n) = E^{\hat{V},i}[l(y_n, v_n) + z(y_{n+1})], \forall n.$

因此

$\lambda N + z(x) \le \sum_{n=1}^N E^{V,i} l(y_n, v_n) + E^{V,i} z(y_{N+1}).$

因此也

$\lambda \le \liminf_{N \to \infty} \frac{1}{N} \sum_{n=1}^N E^{V,i} l(y_n, v_n), \forall V,$

最后

$\lambda \le \inf_V \liminf_{N \to \infty} \frac{1}{N} \sum_{n=1}^N E^{V,i} l(y_n, v_n) = \inf_V J_i(V).$

另一方面我们也有

$\lambda = \lim_{N \to \infty} \frac{1}{N} \sum_{n=1}^N E^{\hat{V},i} l(y_n, v_n) = J_i(\hat{V}).$

这个关系意味着

$$ \lambda \ge \inf_V \limsup_{N \to \infty} \frac{1}{N} \sum_{n=1}^N E^{V,i}(y_n, v_n). $$

汇总结果，我们得到

$$ \lambda = \inf_V J_i(V) = J_i(\hat{V}). $$

类似地，从相同的初始关系我们也有

$$ \lambda \alpha^{n-1}(1-\alpha) + \alpha^{n-1}(1-\alpha) E^{V,i} z(y_n) \\ \le \alpha^{n-1}(1-\alpha) E^{V,i} l(y_n, v_n) + \alpha^n (1-\alpha) E^{V,i} z(y_{n+1}) \\ +\alpha^{n-1}(1-\alpha)^2 E^{V,i} z(y_{n+1}) $$

相加我们得到

$$ \lambda + (1-\alpha)(z) \le (1-\alpha) \sum_{n=1}^\infty \alpha^{n-1} E^{V,i} l(y_n, v_n) + \sum_{n=1}^\infty \alpha^{n-1}(1-\alpha)^2 E^{V,i} z(y_{n+1}). $$

令 \(\alpha \to 1\) 并利用 \(z\) 是有界的事实，我们推断

$$ \lambda \le \liminf_{\alpha \to 1} (1-\alpha) \sum_{n=1}^\infty \alpha^{n-1} E^{V,i} l(y_n, v_n) = J_i(V). $$

另一方面也有

$$ \lambda = \lim_{\alpha \to 1} (1-\alpha) \sum_{n=1}^\infty \alpha^{n-1} E^{V,i} l(y_n, v_n) = J_i(\hat{V}), $$

这完成了所需结果的证明。

## 6.2. 无短缺库存的遍历控制

### 6.2.1. 收敛结果。

我们考虑定理 5.2 的情况。值函数是函数方程的唯一解

(6.2.1) \( u_\alpha(x) = (h-c)x + \inf_{v \ge 0} [l_0(x+v) + \alpha E u_\alpha((x+v-D)^+)], \)

其中

\( l_0(x) = cx + pE(x-D)^-. \)

我们知道最优反馈由基准库存策略 \(S_\alpha\) 定义，具有

(6.2.2) \( \bar{F}(S_\alpha) = \frac{c+\alpha(h-c)}{p+\alpha(h-c)}, \)

它有一个唯一解，因为 \(\rho > c\)。我们的目标是证明

### **定理 6.4.** 我们做出定理 5.2 的假设并且 \(c < p\)。唯一地通过

(6.2.3) \( \bar{F}(S) = \frac{h}{p+h-c}, \)

定义 \(S\)，并且通过

(6.2.4) \( \rho = p\bar{D} - S(p-c) + (p+h-c)E(S-D)^+. \)

定义数 \(\rho\)。




另定义

(6.2.5) $$g(x) = (h - (p + h - c)F(x))^+,$$

则 \( S_\alpha \uparrow S \) 且

$$u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x),$$

其中 \( u \) 由以下定义

(6.2.6) $$
\begin{aligned}
u(S) &= (h - c)(S - E(S - D)^+); \\
u'(x) &= h + c + z(x),
\end{aligned}$$

其中 \( z \) 由以下定义

(6.2.7) $$z(x) = \sum_{n=1}^{+\infty} g * f^{*(n-1)},$$

与方程 (5.1.17) 中相同的记号。

函数 \( u(x) \) 还满足

(6.2.8) $$u(x) = hx + pE(x - D)^- - \rho + Eu((x - D)^+), \forall x > S$$

(6.2.9) $$u(x) = hx + c(S - x) + pE(S - D)^- - \rho, \forall x \le S$$

并且还

(6.2.10) $$
\begin{aligned}
u(x) &= (h - c)x - \rho + \inf_{v \ge 0} [l_0(x + v) + Eu((x + v - D)^+)] \\
Eu((S - D)^+) &= 0
\end{aligned}$$

证明。由公式 (6.2.2) 可知 \( S_\alpha \) 向 \( S \) 的收敛是容易的。注意到

$$F(S_\alpha) = \frac{p - c}{p + \alpha(h - c)},$$

我们看到 \( S_\alpha \) 随 \( \alpha \) 增加。而且，一个简单的计算表明

$$u_\alpha(S_\alpha) = \frac{1}{1-\alpha}[pD + S_\alpha(h(1-\alpha) - p + \alpha c)] + (p + \alpha(h - c))E((S_\alpha - D)^+)],$$

由此，得益于 \( \rho \) 的选择，可得

(6.2.11) $$u_\alpha(S_\alpha) - \frac{\rho}{1-\alpha} \to (h - c)(S - E(S - D)^+).$$

现在，由定理 5.2 可得

由于

$$u'_\alpha(x) = h - c + z_\alpha(x),$$

其中

$$z_\alpha(x) = \sum_{n=1}^\infty \alpha^{n-1} g_\alpha * f^{*(n-1)}(x),$$

且

$$g_\alpha(x) = (c + \alpha(h - c) - (p + \alpha(h - c))F(x))^+.$$

显然，当 \( \alpha \to 1 \) 时 \( g_\alpha(x) \to g(x) \)。因此 \( z_\alpha(x) \to z(x) \)，由 (6.2.7) 定义，前提是该函数定义良好，即级数收敛。

考虑级数

$$H(x) = \sum_{n=2}^{+\infty} f^{*(n-1)}.$$

我们通过归纳法证明

$f^{*(n-1)}(x) \le ||f|| F^{n-2}(x), \forall n \ge 2$

因此

$H(x) \le ||f|| \sum_{n=2}^\infty F^{n-2}(x) = \frac{||f||}{F(x)}$

该界对于任何 \(x \ge 0\) 都定义良好。注意这需要隐含假设 \(f(x) > 0, \forall x\)。因此我们可以断言

$u'_\alpha(x) \to h - c + z(x).$

考虑 \(x > S\)。我们也可以假设 \(x > S_\alpha\)。因此

$u_\alpha(x) - u_\alpha(S_\alpha) = (h-c)(x-S_\alpha) + \int_{S_\alpha}^x z_\alpha(\xi) \, d\xi$
\(\to (h-c)(x-S) + \int_S^x z(\xi) \, d\xi\)

并由 (6.2.8) 推得

(6.2.12) \(u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x) = (h-c)(S-E(S-D)^+) + (h-c)(x-S) + \int_S^x z(\xi) d\xi,\)

若 \(x < S\)，我们同样可得

(6.2.13) \(u_\alpha(x) - \frac{\rho}{1-\alpha} \to u(x) = (h-c)(x-E(S-D)^+),\)

且两个公式在 \(x = S\) 处一致，与第一个公式 (6.2.6) 相同。为证明 (6.2.9)，我们对 \(x \le S\) 写出

$u(S) - u(x) = (h-c)(S-x),$

并注意到

$u(S) = hS + pE(S-D)^- - \rho.$

我们便可轻易得出结论。为证明 (6.2.8)，我们注意到可以写成

$z(x) = g(x) + Ez(x-D)$
$= g(x) + E[z(x-D) \mathbf{1}_{x>D}].$

将 \(z(x)\) 替换为 \(u'(x) - (h-c)\)，我们得到

$u'(x) - (h-c) = g(x) + E[u'(x-D) \mathbf{1}_{x>D}] - (h-c)F(x).$

但我们可以看到，对于 \(x \ge S\)，有

$g(x) = c + (h-c)F(x) - pF(x),$

因此前面的关系式变为

$u'(x) = h - pF(x) + E[u'(x-D) \mathbf{1}_{x>D}],$

也可以写成

$u'(x) = h + \frac{d}{dx} pE(x-D)^- + \frac{d}{dx} Eu((x-D)^+),$

在 \(S\) 和 \(x\) 之间积分，并利用 \(Eu((S-D)^+) = 0\) 以及 \(u(S)\) 的值，我们便可轻易得出 (6.2.8)。

证明已完成。

### 6.2.2. 概率解释。

假设我们采用基准库存政策，基准库存为 S。考虑 \( x \le S \) 及以下序列（其中 \( LS_n \) 表示第 n 期的未满足需求：

- \( y_1 = x, v_1 = S - x, LS_1 = (S - D_1)^- \);
- \( y_2 = (S - D_1)^+, v_2 = S - (S - D_1)^+, LS_2 = (S - D_2)^+ \);
- \(\dots\)
- \( y_{n+1} = (S - D_n)^+, v_{n+1} = (S - D_n)^+, LS_{n+1} = (S - D_{n+1})^+ \)。

除了 \( y_1 \) 外，所有随机变量 \( y_n, n \ge 2 \) 都有相同的概率分布，即

(6.2.14) \( \bar{F}(S)\delta(\eta) + f(S - \eta) 1_{\eta < S} d\eta \)。

过程 \( y_n \) 显然是 ergodic 的，公式 (6.2.14) 给出了不变测度。

如果按比率 \( \alpha \) 折现，我们得到成本

\( u_\alpha(x) = hx + c(S - x) + pE(S - D_1)^- + \sum_{n=1}^\infty \alpha^n E[c(S - (S - D_n)^+) + h(S - D_n)^+ + p(S - D_{n+1})^-] \),

因此

\( u_\alpha(x) = (h - c)(x - E(S - D)^+) + \frac{\rho}{1 - \alpha}, \)

从而得到 \( u(x) \) 的值。量

(6.2.15) \( E[c(S - (S - D)^+) + h(S - D)^+ + p(S - D)^-] \),

表示除第一期外一期的成本。对 S 求最小值可得到最优基准库存。这给出了 \( \rho \) 的解释。现在考虑 \( x > S \) 的情况。我们首先定义

\( y_{n+1} = y_n - D_n, y_1 = x, \)

\( LS_n = (y_n - D_n)^- \)。

令

\( \tau = \inf\{n \ge 1 | y_n \le S\}; \)

从第 \( \tau \) 期开始，我们回到库存低于 S 的情况，并按以下方式进行

- \( y_\tau = y_\tau, v_\tau = S - y_\tau, LS_\tau = (S - D_\tau)^- \),
- \( y_{\tau+n} = (S - D_{\tau+n-1})^+, v_{\tau+n} = S - (S - D_{\tau+n-1})^+, LS_{\tau+n} = (S - D_{\tau+n})^- \)。

相应的成本由以下给出

\( u_\alpha(x) = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} (hy_n + p(y_n - D_{n-1})^- \right] + E \alpha^{\tau-1} [(h - c)y_\tau + cS + p(S - D_\tau)^-] + \sum_{n=1}^\infty E \alpha^{\tau-1+n} [c(S - (S - D_{\tau+n-1})^+) + h(S - D_{\tau+n-1})^+ + p(S - D_{\tau+n})^-] \),

因此，通过适当的条件化

$$u_\alpha(x) - \frac{\rho}{1-\alpha} = E \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E \alpha^{\tau-1} (h - c)(y_\tau - E(S - D)^+)$$

并令 \(\alpha\) 趋近于 1，我们得到

$$u_\alpha(x) - \frac{\rho}{1-\alpha} \to E \left[ \sum_{n=1}^{\tau-1} (hy_n + p(y_n - D_{n+1})^- - \rho) \right] + E(h-c)(y_\tau - E(S - D)^+).$$

将 \(-(h-c)E(S-D)^+\) 替换为 \(cS + pE(S-D)^- - \rho\)，我们得到函数 \(u(x)\) 的概率解释，如 (6.2.8) 和 (6.2.9) 所定义。

## 6.3. 带积压的库存 Ergodic 控制

### 6.3.1. 收敛结果。

我们考虑定理 5.6.1 的情况。函数方程由以下给出

(6.3.1) \(u_\alpha(x) = -cx + hx^+ + px^- + \inf_{v \ge 0} [c(x+v) + \alpha E u_\alpha(x+v-D)].\)

我们知道最优反馈由基准库存政策 \(S_\alpha\) 定义，其中

(6.3.2) \(F(S_\alpha) = \frac{\alpha(h+c)-c}{\alpha(h+p)},\)

当且仅当 \(\alpha > \frac{c}{p+c}\) 时存在唯一解。由于我们将令 \(\alpha\) 趋近于 1，因此假设此条件成立。

我们的目标是证明

### 定理 6.5.

唯一地定义 \(S\) 为

(6.3.3) \(F(S) = \frac{h}{p+h},\)

数 \(\rho\) 由以下定义

(6.3.4) \(\rho = c\bar{D} + pE(S - D)^- + hE(S - D)^+,\)

并且

(6.3.5) \(g(x) = (h - (h + p)\bar{F}(x))^+,\)

则 \(S_\alpha \uparrow S\) 且

\(u_\alpha(x) - \frac{\rho}{1 - \alpha} \to u(x),\)

其中 \(u\) 由以下定义

(6.3.6) \(\begin{cases} u(S) = (h - c)\bar{D} - (p + h)E(S - D)^- \\ u'(x) = -c + h\bar{I}_{x>0} - p\bar{I}_{x<0} + z(x) \end{cases},\)

其中

(6.3.7) \(z(x) = \sum_{n=1}^{+\infty} g * f^{*(n-1)}(x).\)

函数 u 也是以下方程的解

(6.3.8) \( u(x) = hx - \rho + Eu(x - D), \quad \forall x > S \)
(6.3.9) \( u(x) = c(S - x) - \rho + hx^+ + px^-, \quad \forall x \le S \)

证明。由公式 (6.3.2) 可知 \( S_\alpha \) 向 \( S \) 的收敛是明确的。注意到

\( F(S_\alpha) = \frac{p+c}{p+h} - \frac{c}{\alpha(h+p)}, \)

我们看到 \( S_\alpha \) 随 \( \alpha \) 增加。而且，一个简单的计算表明

\( u_\alpha(S_\alpha) = hS_\alpha^+ + pS_\alpha^- + \frac{\alpha}{1-\alpha}[c\bar{D} + hE((S_\alpha - D)^+) + pE((S_\alpha - D)^-)], \)

由此，得益于 \( \rho \) 的选择，可得

\( u_\alpha(S_\alpha) - \frac{\rho}{1-\alpha} \to hS - [c\bar{D} + hE((S - D)^+) + pE((S - D)^-)]. \)

现在，由定理 5.6 可得

\( u'_\alpha(x) = -c + h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + z_\alpha(x), \)

其中

\( z_\alpha(x) = \sum_{n=1}^\infty \alpha^{n-1} g_\alpha * f^{*(n-1)}(x), \)

且

\( g_\alpha(x) = (c(1 - \alpha) + \alpha h - \alpha(h + p)F(x))^+. \)

同样，我们可以看到 \( z_\alpha(x) \to z(x) \)，由方程 (6.3.7) 定义。因此我们得到 (6.3.6)。为证明 (6.3.9)，我们使用 \( z(x) = 0, \forall x \le S \)，因此

\( u'(x) = -c + h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0}, \forall x \le S. \)

在 \( x \) 和 \( S \) 之间积分，并使用 \( u(S) = hS - \rho \)，公式 (6.3.9) 得证。为证明 (6.3.8)，我们注意到

\( u'(x) = h + Eu'(x - D), \forall x > S. \)

接下来我们验证 \( Eu(S - D) = 0 \)。这由 (6.3.8) 在 \( x = S - D \) 处应用并取数学期望得出。因此，在 \( S \) 和 \( x \) 之间积分，我们便可轻易得到 (6.3.9)。

证明已完成。注意 \( u \in C^1 \)，除了 \( x = 0 \) 处。

### 6.3.2. 概率解释。

我们如同在无缺货情况下一样进行。我们首先解释数 \( \rho \)。考虑一个周期，初始库存等于 \( S \)。周期结束时库存为 \( S - D \)。为了在下一周期以库存 \( S \) 面对新需求，我们需要订购 \( D \)。周期结束时，我们支付持有成本 \( h(S - D)^+ \)，如果出现缺货，则支付 \( pE(S - D)^- \)。因此，一个周期的期望成本为

\( cD + hE(S - D)^+ + pE(S - D)^-, \)

这正好是 \( \rho \)。为了找到最优 \( S \)，我们对 \( S \) 最小化该表达式。





考虑 \( x \le S \) 及以下序列
\( y_1 = x, v_1 = S - x; \)
\( y_2 = S - D_1, v_2 = D_1; \)
\( \dots \)
\( y_{n+1} = S - D_n, v_{n+1} = D_n. \)

如果按利率 \( \alpha \) 折现，我们得到成本
\( u_\alpha(x) = hx^+ + px^- + c(S-x) + \sum_{n=1}^\infty \alpha^n [\bar{c}D + hE(S-D)^+ + pE(S-D)^-], \)

因此
\( u_\alpha(x) = hx^+ + px^- + c(S-x) + \frac{\alpha \rho}{1 - \alpha}, \)

并且
\( u_\alpha(x) - \frac{\rho}{1 - \alpha} \to hx^+ + px^- + c(S-x) - \rho. \)

考虑 \( x > S \) 的情况。我们定义
\( y_{n+1} = y_n - D_n, y_1 = x. \)

令
\( \tau = \inf \{ n \ge 1 | y_n \le S \}. \)

从时期 \( \tau \) 开始，我们回到库存低于 \( S \) 的情况，并按以下方式进行
\( y_\tau = y_\tau, v_\tau = S - y_\tau, \)
\( y_{\tau+n} = S - D_{\tau+n-1}, v_{\tau+n} = D_{\tau+n-1}. \)

相应的成本由以下给出
\( u_\alpha(x) = E \sum_{n=1}^{\tau-1} \alpha^{n-1} h y_n + \)
\( + E \alpha^{\tau-1} [-c y_\tau + c S + h y_\tau^+ + p y_\tau^- \)
\( + \sum_{n=1}^\infty E \alpha^{\tau-1+n} [c D_{\tau+n-1} + h(S - D_{\tau+n-1})^+ + p(S - D_{\tau+n-1})^-] \)

因此，通过适当条件化，并考虑到 \( D_{\tau+n-1} \) 与 \( \tau \) 独立，对于 \( n \ge 1 \)
\( u_\alpha(x) - \frac{\rho}{1 - \alpha} = E \sum_{n=1}^{\tau-1} \alpha^{n-1} (h y_n - \rho) \)
\( + E \alpha^{\tau-1} (-c y_\tau + c S - \rho + h y_\tau^+ + p y_\tau^-) \)

并令 \( \alpha \) 趋于 1，我们得到
\( u_\alpha(x) - \frac{\rho}{1 - \alpha} \to E \sum_{n=1}^{\tau-1} (h y_n - \rho) \)
\( + E (-c y_\tau + c S - \rho + h y_\tau^+ + p y_\tau^-), \)

右边是 \( u(x) \) 的概率解释，如 (6.3.8)、(6.3.9) 所定义。

## 6.4. 确定性情况

确定性情况可以视为随机情况的特例。然而，我们可以直接查看第 5.3 节中得到的公式。在无缺货情况下，我们有以下公式

(6.4.1)
$$
u_\alpha(x) = \begin{cases} (h-c)x + \frac{cD}{1-\alpha}, & \forall x \le D \\ hx + \alpha u_\alpha(x-D), & \forall x \ge D \end{cases}
$$

基础库存 \(S_\alpha = D\)，不依赖于 \(\alpha\)，因此 \(S = D\)，且 \(\rho = cD\)。我们得到

(6.4.2)
$$
u_\alpha(x) - \frac{cD}{1-\alpha} \to u(x),
$$

其中 \(u(x)\) 是以下方程的解

$$
u(x) = \begin{cases} (h-c)x, & \forall x \le D \\ hx - cD + u(x-D), & \forall x \ge D \end{cases}
$$

同样，在积压情况下，我们有以下关系

$$
u_\alpha(x) = \begin{cases} (h-c)x + \frac{cD}{1-\alpha}, & \forall x \le D \\ hx + \alpha u_\alpha(x-D), & \forall x \ge D \end{cases}
$$

因此 \(S = D, \rho = cD\)。我们再次得到 (6.4.2)，其中

$$
u(x) = \begin{cases} hx^+ + px^- - cx, & \forall x \le D \\ hx^+ + px^- - cD + u(x-D), & \forall x \ge D \end{cases}
$$

# 最优停止问题

在本章中，我们考虑决策为停止时间的情况。它们可以归约为一般情况，但最好使用此类问题的特定方面。我们将首先定义感兴趣的函数方程，该方程源自动态规划，直接研究它，然后将其解释为以停止时间为决策的控制问题。

## 7.1. 动态规划

在介绍感兴趣的控制问题后，我们展示动态规划的函数方程。

### 7.1.1. 问题的表述。

我们考虑第 4 章的框架。我们回顾，决策规则是一个无穷序列

\(\hat{V} = \{\hat{v}_1, \cdots, \hat{v}_n, \cdots\},\)

其中

\(\hat{v}_n = \hat{v}_n(x_1, \cdots, x_n),\)

是取值于 \(U\) 的 Borel 映射。从决策规则，我们构造给定 \(y_1 = x\) 的规范随机过程 \(y_n\) 的概率 \(P^{V,x}\)，表示状态轨迹。状态空间是 \(X = \mathbb{R}^d\)。我们回顾滤流

\(\mathcal{Y}^n = \sigma(y_1, \cdots, y_n).\)

在当前情况下，将有一个不同性质的新决策变量，即相对于滤流 \(\mathcal{Y}^n\) 的停止时间 \(\tau\)。

我们考虑函数 \(l(x, v)\)，使得

(7.1.1) \(l(x, v) \ge 0; \quad \text{l.s.c.}\)

此外，我们还将考虑函数 \(\psi(x)\)，使得

(7.1.2) \(\psi(x) \ge 0; \quad \text{l.s.c.}\)

成本目标定义为

(7.1.3) \(J_x(V, \tau) = E^{V,x} \left[ \sum_{n=1}^{\tau-1} \alpha^{n-1} l(y_n, v_n) + \alpha^{\tau-1} \psi(y_\tau) \right]\)

### 7.1.2. 动态规划方程。

给出前面问题的值函数的函数方程定义为

(7.1.4) $$u(x) = \min \{ \psi(x), \inf_{v \in U} [l(x, v) + \alpha \Phi^v u(x)] \}, \forall x.$$

这个函数方程结合了第 4 章中研究的非线性算子与函数 $\psi(x)$。我们称这个函数为障碍。这指的是解 $u(x)$ 必须保持在障碍以下的事实。如方程 (7.1.4) 所示，它在成本函数中表示在决策时间 $\tau$ 时收到的回报。

我们将考虑在方程 (4.3.4) 中定义的上限函数 $w_0(x)$。

我们陈述主要结果

### 定理 7.1. 在假设 (7.1.1)、(7.1.2)、(4.3.1)、(4.3.2) 和 (4.3.6) 下，函数方程 (7.1.4) 的解集满足

$$
0 \le u(x) \le w_0(x) \quad \forall x,
$$

非空，并具有最小解和最大解，分别记为 $\underline{u}(x)$ 和 $\overline{u}(x)$。最小解是下半连续（l.s.c.），如果函数 $l(x, v)$ 和 $\psi$ 是连续的，则最大解是上半连续（u.s.c.）。

证明。设 $z$ 为下半连续（l.s.c.）且为正。定义

$$
Tz(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v z(x)].
$$

我们知道来自第 4 章，$Tz$ 也是下半连续（l.s.c.）且为正。设

$$
Sz(x) = \min[\psi(x), Tz(x)].
$$

我们使用以下练习来声称 $S(z)$ 也是下半连续（l.s.c.）且为正。

### 练习 7.1. 如果 $f$ 和 $g$ 是下半连续（l.s.c.）且下有界，则 $\min(f, g)$ 也是下半连续（l.s.c.）且下有界。

方程 (7.1.4) 的解函数 $u$ 是映射 $S$ 的不动点。映射 $S$ 是递增的，即如果 $z_1 \le z_2$，则 $Sz_1 \le Sz_2$。如果 $z \ge 0$，则 $Sz \ge 0$。假设 $z \le \tilde{w}$，则

$$
Sz(x) \le l(x, v) + \alpha \Phi^{w_0} w_0(x) = w_0(x).
$$

我们已检查 $S$ 将区间 $[0, w_0]$ 映射到自身。接下来考虑递减方案

$$
u^{n+1} = Su^n, \quad u^0 = w_0.
$$

显然

$$
u^0 \ge u^1 \ge \dots \ge u^n \dots \ge 0.
$$

我们可以说 $u^n \downarrow u$，其中 $u$ 是正 Borel 函数。显然 $u^{n+1} \ge Su$，因此也有 $u \ge Su$。另外

$$
\begin{aligned} u^{n+1}(x) &\le \psi(x) \\ u^{n+1}(x) &\le l(x, v) + \alpha \Phi^v u^n(x), \quad \forall v \end{aligned}
$$

令 $n$ 趋于 $+\infty$，得到

$$
\begin{aligned} u(x) &\le \psi(x) \\ u(x) &\le l(x, v) + \alpha \Phi^v u(x), \quad \forall v \end{aligned}
$$

因此 $u \le Su$。所以极限 $u$ 是 $S$ 的不动点。而且它是区间 $[0, w_0]$ 中的最大解。它是上半连续（u.s.c.），作为连续函数序列的递减极限。

### 练习 7.2. 检查 $u$ 是最大次解，即如果 $\tilde{u} \le S\tilde{u}$ 且 $0 \le \tilde{u} \le w_0$，则 $\tilde{u} \le u$。

最大解记为 $\bar{u}$。

证明续。接下来我们考虑递增序列

$u_{n+1} = S u_n, u_0 = 0.$

显然

$u_0 \le u_1 \le \cdots \le u_n \cdots \le w_0.$

因此 $u_n \uparrow u$ 且 $0 \le u \le w_0$，并且 $u$ 是下半连续（l.s.c.）。由于 $u_{n+1} \le S u$，我们得到 $u \le Su$。另一方面，存在 Borel 映射 $\tilde{v}_n(x)$，使得

$u_{n+1}(x) = \min[\psi(x), l(x, \tilde{v}_n(x)) + \alpha \Phi^{\tilde{v}_n(x)} u_n(x)].$

令 $m \ge n$。可以写成

$u_{m+1}(x) \ge \min[\psi(x), l(x, \tilde{v}_m(x)) + \alpha \Phi^{\tilde{v}_m(x)} u_n(x)],$

因此也有

$u(x) \ge \min[\psi(x), l(x, \tilde{v}_m(x)) + \alpha \Phi^{\tilde{v}_m(x)} u_n(x)].$

我们固定 $n$ 并令 $m \to \infty$。使用假设 (4.3.2)，我们看到序列 $\tilde{v}_m(x)$ 保持在一个紧集中（$x$ 固定，紧集依赖于 $x$）。因此我们可以提取一个收敛子序列 $\tilde{v}_{m_k}(x) \to v^*(x)$。由于 $v$ 的函数

$\min[\psi(x), l(x, v) + \alpha \Phi^v u_n(x)]$ 是下半连续（l.s.c.），

我们可以断言

$u(x) \ge \min[\psi(x), l(x, v^*(x)) + \alpha \Phi^{v^*(x)} u_n(x)].$

接下来令 $n \to \infty$，我们得到 $u \ge Su$，并从逆不等式看出 $u$ 是 $S$ 的不动点。

### 练习 7.3. 检查由递增序列得到的 $u$ 是最小解，即如果 $\tilde{u} = S\tilde{u}$ 且 $0 \le \tilde{u} \le w_0$，则 $\tilde{u} \ge u$。

最小解记为 $\underline{u}(x)$。

## 7.2. 解释

我们现在将最小解解释为由目标函数 (7.1.3) 定义的问题的值函数。然而，我们首先展示函数方程 (7.1.4) 可以写成标准形式，前提是我们扩展控制。

### 7.2.1. 另一种表述。

不难证明，$S$ 的不动点 $u$ 也可以写成普通动态规划函数方程的解，前提是引入一个额外控制

### 练习 7.4. 证明

$u(x) = \inf_{\{v \in U | 0 \le d \le 1\}} [d\psi(x) + (1-d)l(x, v) + \alpha(1-d)\Phi^v u(x)].$





在此形式下，对 \(u(x)\) 的解释，事实上将最小解解释为随机控制问题的值函数已成为标准。我们引入与控制变量 \(v, d\) 相关的 \(V, D\) 决策规则，即

\(V = \{v_1, \cdots, v_n, \cdots\}\)
\(D = \{d_1, \cdots, d_n, \cdots\}\)

和

\(v_n = v_n(x_1, \cdots, x_n)\)
\(d_n = d_n(x_1, \cdots, x_n)\)

函数 \(v_n\) 和 \(d_n\) 是 Borel 函数，其值域分别为 \(U\) 和 \([0, 1]\)。由于 \(\Phi^u\) 不依赖于 \(d\)，在 \(\Omega = X^N, \mathcal{A}\) 上定义的、与决策规则 \(V, D\) 及初始状态 \(x\) 相关的概率仅依赖于 \(V\) 和 \(x\)，并记作 \(P^{V,x}\)。考虑规范过程 \(y_n\)（参见第 3 章），我们知道

\(y_1 = x, P^{V,x} \text{ a.s.}\)

决策规则定义了随机过程 \(v_n(y_1, \cdots, y_n)\) 和 \(d_n(y_1, \cdots, y_n)\)，它们相对于由规范过程生成的滤流 \(\mathcal{Y}^n\) 是自适应的。

我们现在定义与 \(V, D, x\) 相关的收益如下

\(J_x(V, D) = E^{V,x} \sum_{j=1}^{\infty} \alpha^{j-1} (1 - d_{j-1}) \cdots (1 - d_1) d_j \psi(y_j) + (1 - d_j) l(y_j, v_j).\)

根据第 4 章的理论，我们可以断言，通过递增序列得到的 0 与 \(w_0\) 之间的最小解是该收益对应的值函数。即，我们有

\(\underline{u}(x) = \inf_{V,D} J_x(V, D)\)

## 7.2.2. 最优停止表述。

## 7.2.2. 最优停止表述。

使用上一节描述的技巧并不是处理最优停止问题的最佳方式。我们现在直接使用停止时间。令 \(\theta\) 为相对于滤流 \(\mathcal{Y}^n\) 的停止时间。我们定义收益

\(J_x(V, \theta) = E^{V,x} \left[ \sum_{j=1}^{\theta-1} \alpha^{j-1} l(y_j, v_j) + \alpha^{\theta-1} \psi(y_\theta) \mathbb{1}_{\theta < \infty} \right]\)

**Theorem 7.2.** 在定理 7.1 的假设下，最小解 \(\underline{u}(x)\) 满足

\(\underline{u}(x) = \inf_{V,\theta} J_x(V, \theta).\)

**PROOF.** 令 \(V\) 为一个决策规则，\(\theta\) 为相对于 \(\mathcal{Y}^n\) 的停止时间。考虑递增序列 \(u_n(x)\)。对于 \(0 \le j \le N - 1\)，我们可以写出

\(\alpha^{N-j-1} u_{j+1}(y_{N-j}) \mathbb{1}_{N-j < \theta} \le\)
\(\alpha^{N-j-1} l(y_{N-j}, v_{N-j}) \mathbb{1}_{N-j < \theta} + \alpha^{N-j} E^{V,x} [u(y_{N-j+1}) \mathbb{1}_{N-j < \theta} | \mathcal{Y}^{N-j}]\)

对两边取期望得到

\(E^{V,x} (\alpha^{N-j-1} u_{j+1}(y_{N-j}) \mathbb{1}_{N-j < \theta}) \le\)
\(E^{V,x} (\alpha^{N-j-1} l(y_{N-j}, v_{N-j}) \mathbb{1}_{N-j < \theta}) + E^{V,x} (\alpha^{N-j} u_j(y_{N-j+1}) \mathbb{1}_{N-j < \theta})\)

对 \(j = 0, \cdots, N-1\) 求和，我们得到

\( E^{V,x} \sum_{k=1}^{(\theta-1) \wedge N} \alpha^{k-1} u_{N-k+1}(y_k) \le E^{V,x} \sum_{k=1}^{(\theta-1) \wedge N} \alpha^{k-1} l(y_k, v_k) + E^{V,x} \sum_{k=2}^{\theta \wedge (N+1)} \alpha^{k-1} u_{N-k+1}(y_k). \)

消去项后我们推导出

\( u_N(x) E^{V,x} \mathbb{1}_{\theta \ge 2} \le E^{V,x} \sum_{k=1}^{(\theta-1) \wedge N} \alpha^{k-1} l(y_k, v_k) + E^{V,x} \alpha^{\theta-1} u_{N-\theta+1}(y_\theta) \mathbb{1}_{\theta \le N}, \)

其中我们使用了 \(u_0(x) = 0\) 的事实。在该关系式两边加上 \(u_N(x) E^{V,x} \mathbb{1}_{\theta=1}\)，令 \(N \to \infty\) 在右边，我们得到

\( u_N(x) \le \inf_{V,\theta} J_x(V, \theta). \)

因此也有

\( \underline{u}(x) \le \inf_{V,\theta} J_x(V, \theta). \)

接下来定义最优反馈 \(\tilde{v}(x)\)，它使 \(l(x,v) + \alpha \Phi^v \underline{u}(x)\) 在 \(v \in U\) 上取得最小值。我们将与此反馈关联一个决策规则 \(\tilde{V}\)。然后定义退出时间

\( \widehat{\theta} = \inf \{ n \ge 1 | \underline{u}(y_n) = \psi(y_n) \}, \)

其中

\( \widehat{\theta} = \infty \) 若 \( \underline{u}(y_n) < \psi(y_n), \forall n \).

我们验证对于 \(\forall N\)

\( \underline{u}(x) = E^{V,x} \left[ \sum_{k=1}^{(\widehat{\theta}-1) \wedge N} \alpha^{k-1} l(y_k, v_k) + \alpha^{(\widehat{\theta}-1) \wedge N} \underline{u}(y_{\widehat{\theta} \wedge (N+1)}) \right], \)

因此也有

\( \underline{u}(x) \ge E^{V,x} \left[ \sum_{k=1}^{(\widehat{\theta}-1) \wedge N} \alpha^{k-1} l(y_k, v_k) + \alpha^{\widehat{\theta}-1} \psi(y_{\widehat{\theta}}) \mathbb{1}_{\widehat{\theta} \le N+1} \right]. \)

令 \(N\) 趋于 \(\infty\)，我们得到

\( \underline{u}(x) \ge J_x(V, \widehat{\theta}), \)

定理的证明已完成。

## 7.2.3. 直接法。

## 7.2.3. 直接法。

我们已经表明最小解 \(\underline{u}(x)\) 有两种诠释

\( \underline{u}(x) = \inf_{V,\theta} J_x(V, \theta) = \inf_{V,D} J_x(V, D). \)

我们可以直接验证两个下确界的相等。首先注意，不失一般性，我们可以限制 \(d\) 仅取值 0 或 1。这是因为由 Bellman 方程得到的最优反馈（它允许得到最优决策规则）满足这一性质。

现在，考虑任何具有此性质的决策规则 \(D\)，我们定义

\(\theta_D = k, \quad \text{if } d_j = 0, j \le k-1, d_k = 1\)
\(\theta_D = \infty, \quad \text{if } d_j = 0, \forall j\)

然后可以验证 \(\theta_D\) 是一个 \(\mathcal{Y}^n\) 停止时间，且

\(J_x(V, \theta_D) = J_x(V, D),\)

由此我们推导出 \(\inf J_x(V, D) \ge \inf J_x(V, \theta)\)。

另一方面，若 \(\theta\) 是任意停止时间，我们定义

\(D_\theta = (d_1^\theta, \dots, d_j^\theta, \dots);\)
\(d_j^\theta = 0 \text{ if } j \le \theta - 1;\)
\(d_j^\theta = 1 \text{ if } j \ge \theta,\)

并且我们验证

\(J_x(V, \theta) = J_x(V, D_\theta),\)

由此得出

\(\inf J_x(V, \theta) \ge \inf J_x(V, D),\)

相等性随之成立。

## 7.3. 惩罚逼近

## 7.3. 惩罚逼近

在本节中，我们发展一个在实践中非常有用的新思想。回顾我们曾将函数 \(\psi\) 称为“障碍”，这让人联想到 \(u \le \psi\) 的事实。其思想是，我们可以通过支付惩罚来放弃此约束。当此惩罚为无穷大时，障碍约束将得到满足。

### 7.3.1. 表述。

### 7.3.1. 表述。

为了简化，我们考虑不带控制的最优停止问题。此外，我们假设

(7.3.1) \(l, \psi \in C, l \ge 0, \psi \ge 0,\)

其中 \(C = C(X)\) 表示在 \(X\) 上一致连续且有界函数的空间。在此额外假设下，存在唯一解 \(u\) 满足

(7.3.2) \(u(x) = \min[\psi(x), l(x) + \alpha \Phi u(x)].\)

我们知道该解是连续的。为了保证其一致连续，我们对 \(\Phi\) 作出额外假设，这加强了 (4.3.1)

(7.3.3) \(\Phi \varphi \in C, \text{若 } \varphi \text{ 是连续且有界的。}\)

我们将前面的问题与以下问题关联

(7.3.4) \(u_\epsilon(x) = l(x) + \alpha \Phi u_\epsilon(x) - \frac{1}{\epsilon} (u_\epsilon - \psi)^+(x),\)

称为惩罚逼近。其逻辑很简单。与其强加约束 \(u \le \psi\)，不如接受我们的未知函数超过约束 \(\psi\)，但随后在成本 \(l\) 中加入一个惩罚项，仅在函数超过约束时支付。显然，当 \(\epsilon\) 趋于 0 时，惩罚项变得非常大，迫使未知函数满足约束。请注意，方程 (7.3.4) 是一个非线性问题。

### 7.3.2. 惩罚问题的解

### 7.3.2. 惩罚问题的解

我们首先证明

**Lemma 7.1.** 在假设 (7.3.1) 和 (7.3.3) 下，惩罚问题 (7.3.4) 在 C 中存在唯一的正解。

**PROOF.** 将 (7.3.4) 写成等价形式很方便

$$u_\epsilon \left( 1 + \frac{1}{\epsilon} \right) = l + \alpha \Phi u_\epsilon + \frac{1}{\epsilon} \min(\psi, u_\epsilon)$$

**Exercise 7.5.** 证明上述断言。

因此 \(u_\epsilon\) 是由以下定义的映射 \(w_\epsilon = T_\epsilon(z)\) 的不动点

$$w_\epsilon \left( 1 + \frac{1}{\epsilon} \right) = l + \alpha \Phi w_\epsilon + \frac{1}{\epsilon} \min(\psi, z)$$

**Exercise 7.6.** 验证 \(T_\epsilon\) 是一个收缩映射，其常数为 \(\frac{1}{1+\epsilon(1-\alpha)}\)。

这完成了引理的证明。

**Lemma 7.2.** 我们有

$$0 \le u_\epsilon \le \max \left( \|\psi\|, \frac{\|l\|}{1-\alpha} \right).$$

而且 \(u_\epsilon\) 随 \(\epsilon \downarrow 0\) 单调递减。

**PROOF.** 若 \(z \ge 0\)，则 \(T_\epsilon(z) \ge 0\)。因此，由于 \(T_\epsilon\) 是单调的，我们得到 \(u_\epsilon \ge 0\)。

**Exercise 7.7.** 验证对于任意 \(z \ge 0\)，有

$$\|T_\epsilon z\| \le \max \left( \|\psi\|, \frac{\|l\|}{1-\alpha} \right),$$

因此解 \(u_\epsilon\) 也满足同样的估计。

进一步：为了证明单调性，考虑 \(\epsilon' < \epsilon\) 并令 \(w = T_\epsilon(u_{\epsilon'})\)。我们首先验证

$$(w - u_{\epsilon'}) \left( 1 + \frac{1}{\epsilon} \right) = \alpha \Phi(w - u_{\epsilon'}) + \left( \frac{1}{\epsilon'} - \frac{1}{\epsilon} \right) (u_{\epsilon'} - \psi)^+,$$

由此可得 \(w - u_{\epsilon'} \ge 0\)。因此 \(u_{\epsilon'} \le T_\epsilon(u_{\epsilon'})\)。迭代得到 \(u_{\epsilon'} \le T_\epsilon^n(u_{\epsilon'})\)。令 \(n\) 趋于 \(\infty\)，我们得到 \(u_{\epsilon'} \le u_\epsilon\)。引理的证明已完成。

### 7.3.3. 收敛性。

### 7.3.3. 收敛性。

我们给出以下收敛结果。

**Theorem 7.3.** 在假设 (7.3.1) 和 (7.3.3) 下，有 \(u_\epsilon \downarrow u\)，即方程 (7.3.2) 的解。

**PROOF.** 我们可以断言 \(u_\epsilon \downarrow u^*\)。由 (7.3.4) 可写出

$$u_\epsilon \le l + \alpha \Phi u_\epsilon,$$

因此

$$u^* \le l + \alpha \Phi u^*.$$

而且，由于 \(u_\epsilon\) 是有界的，我们可以断言 \((u_\epsilon - \psi)^+ \to 0\)。因此

$$u^* \le \psi.$$




注意

$(u_* - \psi)^-(u_* - l - \alpha \Phi u_*) = 0.$

我们可以取极限并得到

$(u^* - \psi)^-(u^* - l - \alpha \Phi u^*) = 0.$

利用性质 $u^* - \psi \le 0$，我们还可以写成

$(u^* - \psi)(u^* - l - \alpha \Phi u^*) = 0,$

这意味着 $u^*$ 是 (7.3.2) 的一个解。证明已完成。$\square$

## 7.4. 遍历情况

我们现在研究遍历问题，令 $\alpha \to 1$。

### 7.4.1. 模型设定。

我们这里将采用定理 7.1 的假设，并且还假设

(7.4.1) \( l, \psi \ge 0, \text{bounded}, l(x) \ge l_0 > 0. \)

我们考虑问题

(7.4.2) \( u_\alpha(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \alpha \Phi^* u_\alpha(x)] \right\}, \forall x. \)

我们知道它有一个唯一的 l.s.c. 连续解（通过收缩映射论证）。

问题是研究 $u_\alpha$ 当 $\alpha$ 趋于 1 时的极限。事实上，这个问题将比没有障碍 $\psi$ 的问题更容易。原因是因为函数 $u_\alpha$ 将保持有界。

### 7.4.2. 主要结果。

我们陈述主要结果

#### 定理 7.4.

我们采用定理 7.1 和 (7.4.1) 的假设。考虑方程

(7.4.3) \( u(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \Phi^* u(x)] \right\}, \forall x, \)

那么它有一个正有界 l.s.c. 解，且该解唯一。此外，当 \( \alpha \uparrow 1 \) 时，\( u_\alpha(x) \uparrow u(x) \)。

#### 证明。

我们证明解 $z$ 的存在性和唯一性。我们不能使用收缩映射的论证，因为 $\alpha = 1$。为了证明正有界 l.s.c. 解的存在性，我们考虑递增序列

u_0 = 0

u_{n+1}(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x, v) + \Phi^* u_n(x)] \right\}

那么显然

u_0 \le u_1 \cdots \le u_n \le \cdots \psi,

因此 \( u_n \uparrow u \ge 0 \)。此外，\( u \le \psi \) 且为 l.s.c.

仿照定理 7.1 证明中的推理，我们检查极限 $u$ 具有所需性质且是一个解。让我们证明 Borel 有界解的唯一性。我们不能使用收缩映射论证。我们使用以下技巧。我们首先排除 $\psi = 0$ 的情况，在这种情况下唯一解是 $u = 0$。

假设存在两个正有界解 \(z_1, z_2\)。假设存在一点 \(x^*\) 使得 \(z_2(x^*) < z_1(x^*)\)。那么我们有

$$\gamma = \inf_{\{x|z_1(x)>0\}} \frac{z_2(x)}{z_1(x)} < 1.$$

我们将展示一个矛盾。我们将构造一个数 \(\beta\) 满足 \(\gamma < \beta \le 1\)，使得 \(\beta z_1(x) \le z_2(x), \forall x\)。这将导出

$$\gamma = \inf_{\{x|z_1(x)>0\}} \frac{z_2(x)}{z_1(x)} \ge \beta,$$

这与假设矛盾。

令 \(0 < \lambda < 1\)。一个解 \(z\) 还满足

$$z(x) = \min \left\{ \lambda \psi(x) + (1-\lambda)z(x), \inf_{v \in U} [l(x,v) + (1-\lambda)z(x) + \lambda \Phi^v z(x)] \right\}.$$

这对 \(z_1\) 和 \(z_2\) 特别成立。注意

$$\beta z_1(x) = \min \left\{ \beta \lambda \psi(x) + (1-\lambda)\beta z_1(x), \inf_{v \in U} [\beta l(x,v) + (1-\lambda)\beta z_1(x) + \lambda \Phi^v \beta z_1(x)] \right\}.$$

有人可能会声称，当

$$\beta \lambda \psi(x) + (1-\lambda)\beta z_1(x) \le \lambda \psi(x) + (1-\lambda)z_2(x)$$
$$\lambda l(x,v) + (1-\lambda)\beta z_1(x) \le l(x,v) + (1-\lambda)z_2(x)$$

时，\(\beta z_1(x) \le z_2(x)\) 成立。

由于 \(z_2(x) \ge \gamma z_1(x)\)，要保证

$$\beta \lambda \psi(x) + (1-\lambda)\beta z_1(x) \le \lambda \psi(x) + (1-\lambda)\gamma z_1(x)$$
$$\lambda l(x,v) + (1-\lambda)\beta z_1(x) \le l(x,v) + (1-\lambda)\gamma z_1(x)$$

就足够了。

我们必须有

$$(1-\lambda)(\beta-\gamma)z_1(x) \le \lambda(1-\beta)\psi(x)$$
$$(1-\lambda)(\beta-\gamma)z_1(x) \le \lambda(1-\beta)l(x,v)$$

只需检查

$$(1-\lambda)(\beta-\gamma) \le \lambda(1-\beta)$$
$$(1-\lambda)(\beta-\gamma) \le \lambda(1-\beta) \frac{l_0}{\|\psi\|}$$

就足够了。

只需选择 \(\beta\) 使得

$$\frac{\beta-\gamma}{1-\beta} = \rho = \frac{\lambda}{1-\lambda} \min \left( 1, \frac{l_0}{\|\psi\|} \right),$$

从而

$$\beta = \frac{\rho+\gamma}{1+\rho}.$$

并且 \(\gamma < \beta \le 1\)。矛盾已确立。由此矛盾可得 \(z_2(x) \ge z_1(x), \forall x\)。由于 \(z_1\) 和 \(z_2\) 之间的对称性，我们得到 \(z_1 = z_2\)。唯一性已被证明。

为了完成证明，我们需要检查收敛性质。我们首先证明

$$\alpha \le \alpha' \Rightarrow u_\alpha \le u_{\alpha'}.$$

这个性质通过考虑递增序列得到

$$u_{\alpha, n+1}(x) = \min \left\{ \psi(x), \inf_{v} [l(x,v) + \alpha \Phi^v u_{\alpha,n}(x)] \right\}$$

以及 \(u_{\alpha,0}(x) = 0\)。显然

$$u_{\alpha,n}(x) \le u_{\alpha',n}(x) \to u_{\alpha,n+1}(x) \le u_{\alpha',n+1}(x),$$

单调性结果随之得出。

接下来我们写

$$u_\alpha(x) = \min \left\{ \psi(x), \inf_{v \in U} [l(x,v) + \Phi^v u_\alpha(x) - (1-\alpha)\Phi^v u_\alpha(x)] \right\}, \forall x.$$

由于 \(||(1-\alpha)\Phi^v u_\alpha|| \le (1-\alpha)||u_\alpha||\)，因此趋于 0，我们很容易看出 \(u_\alpha \uparrow u^*\)，它是 (7.4.3) 的解。证明已完成。

**备注。** 如果函数 \(l(x,v)\) 和 \(\psi\) 是连续的，那么 (7.4.3) 的解也是连续的。这是通过定义一个单调递减序列，收敛到一个解，该解是 u.s.c. 来检查的。由于唯一性，解是连续的。

### 7.4.3. 概率解释。

我们如同在第 7.2 节中一样，考虑一个决策规则 \(V\) 和一个停时 \(\theta\)。我们然后定义收益

$$J_x(V, \theta) = E^{V,x} \left[ \sum_{j=1}^{\theta-1} l(y_j, v_j) + \psi(y_\theta) \mathbf{1}_{\theta < \infty} \right].$$

我们可以陈述

#### 定理 7.5.

我们采用定理 7.4 的假设。我们然后有

$$u(x) = \inf_{V, \theta} J_x(V, \theta).$$

证明。我们首先注意到

$$\psi(x) \ge J_x(V, \theta) \ge l_0 E^{V,x}(\theta - 1),$$

因此，不受任何限制，我们可以假设 \(\theta < \infty\) a.s. \(P^{V,x}\)。然后可以检查不等式

$$u(x) \le E^{V,x} \left[ \sum_{j=1}^{\theta-1} l(y_j, v_j) + u(y_\theta) \right] \le J_x(V, \theta).$$

接下来定义反馈 \(\tilde{v}(x)\)，它是取值于 \(U\) 的 Borel 函数，在方程 (7.4.3) 中在 \(v\) 处取得下确界。我们然后定义

$$\tilde{\theta} = \inf \{ n \ge 1 | u(y_n) = \psi(y_n) \}.$$

我们可以断言

$$E^{V,x}[\tilde{\theta}] \le \frac{\psi(x)}{l_0}.$$

确实，对于任何 \(N\)，我们可以写

$$u(x) = E^{V,x} \left[ \sum_{j=1}^{\tilde{\theta} \wedge N - 1} l(y_j, v_j) + u(y_{\tilde{\theta} \wedge N}) \right] \ge l_0 E^{V,x} \tilde{\theta} \wedge N.$$

由于 \(u(x) \le \psi(x)\)，我们也得到

$$E^{\tilde{V},x}[\tilde{\theta} \wedge N] \le \frac{\psi(x)}{l_0}$$

并令 \(N\) 趋于 \(\infty\)，所需的估计就得到了。因此我们可以写

$$u(x) = E^{\tilde{V}, x} \left[ \sum_{j=1}^{\tilde{\theta}-1} l(y_j, v_j) + u(y_{\tilde{\theta}}) \right]$$

另外，由于 \(\tilde{\theta} < \infty\) a.s. \(P^{\tilde{V}, x}\)，有 \(u(y_{\tilde{\theta}}) = \psi(y_{\tilde{\theta}})\)。因此

$$u(x) = J_x(V, \tilde{\theta})$$

证明已完成。

**练习 7.8.** 检查当 \(l_0 = 0\) 时，\(u_n \uparrow\) 方程 (7.4.3) 的最小解。这个最小解是定理 7.5 陈述中定义的值函数。

本页故意留空

# 冲动控制

冲动控制主要在连续时间中被研究，参见 [8]。确实，在连续时间中，冲动控制与连续控制之间的差异非常明显。冲动控制允许系统状态发生跳跃。连续控制只允许系统状态的连续演化，并禁止跳跃。在离散时间中，当然没有连续演化，因此看起来这个概念失去了其特殊性；时刻 n+1 的状态可以被视为从时刻 n 的状态发生的跳跃。然而，我们将识别与最优停止的类比。可以将最优停止嵌入离散时间的标准控制问题中，但也可以以特定方式处理它。同样，冲动控制问题可以嵌入离散时间的标准控制问题中，但也可以以特定方式考虑它。在这种情况下，它看起来像最优停止，但有一系列停时而不是单一停时。我们将首先描述模型。然后我们引入基本工具，即来自动态规划的函数方程。我们直接通过分析技术研究它。最后我们进行解释。

## 8.1. 模型描述

### 8.1.1. 转移概率。

在此设置中，我们将考虑一个具有特殊特征的受控马尔可夫链。它既是一般框架的推广，也是特例。然而，我们需要 X 是向量空间或向量空间的子空间这一事实。为了明确概念，我们取 X = R^d 或 X = (R^d)^+。我们像通常一样考虑转移概率 \pi(x, v, d\eta)。我们然后定义转移概率

$$\pi(x, v, w, d\eta) = \pi(x + v, w, d\eta).$$

这确实是通常情况的推广，通过固定 w = 0 可以恢复通常情况，但也是特例，将对 v, w 视为一个控制。我们将与转移概率关联的算子定义为

$$\Phi^{v,w} f(x) = \int_{R^d} f(\eta) \pi(x, v, w, d\eta).$$

考虑与 \(\pi(x, v, d\eta)\) 关联的算子 $\Phi^v$，我们显然有

$$\Phi^{v,w} f(x) = \Phi^v f(x + w).$$

控制 v, w 在数学上相似，但在实践中作用不同。控制 v 修改转移概率，但不改变 x。控制 w 修改 x。它的影响是瞬时的，而不是发生在下一时期。这就是为什么它被称为冲动。因此，差异仍然有意义，尽管我们处于离散时间中。我们还注意到，如果假设 (4.3.1) 对于 $\Phi^{v,w}$ 成立，它也适用于 $\Phi^{v,w}$。




### 8.1.2. 假设。

我们现在定义一个成本函数。设 \( l(x, v) \) 满足 (4.3.2)，我们令

\[ l(x, v, w) = l(x + v, w) + c(w). \]

我们只考虑 \( w \in (R_+^d) \)，以符合我们所考虑的应用。然后我们假设特殊形式

\[ c(w) = K \mathbf{1}_{w \neq 0} + c_0(w) \]
\[ c_0(w) \text{ 是次线性正连续函数，} c_0(0) = 0 \]
\[ c_0(w) \to \infty \text{ 当 } |w| \to \infty \]

我们注意到函数 \( l(x, v, w) \) 满足 (4.3.2)。

**注。** 当然，\( c(w) \) 结构中的重要元素是 \( K \) 的存在，它仅在采取行动时存在，即 \( w \neq 0 \)。它被称为 _固定成本_（在库存文献中也称为 _设置成本_）。我们还注意到，即使 \( (x, v) \) 是连续的，函数 \( l(x, v, w) \) 也将保持下半连续（l.s.c）而不连续。

我们考虑一个决策规则 \( V, W \)，扩展了对 \( V \) 的通常定义。我们在 \( \Omega, \mathcal{A} \) 上关联一个概率 \( P^{V,W}_x \)，使得 \( y_1 = x \) 几乎必然（a.s.）。我们将考虑回报函数

\[ J_x(V, W) = E^{V,W}_x \left[ \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n, w_n) \right], \]

并且，如常，我们关注值函数

\[ u(x) = \inf_{V,W} J_x(V, W). \]

我们将需要一个上限函数。我们不能使用符号 \( w_0(x) \) 作为上限函数，因为我们有一个新的控制 \( w_n \)。通过取 \( w_n = 0 \) 和 \( v_n = v_0 \)，其中 \( v_0 \) 是 \( U \) 的固定元素，\( U \) 是约束空间，是度量空间的一个闭子集。定义

\[ v_0(x) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^{w_n} \circ^n - I_{l_\epsilon}(x)), \]

其中 \( l_\epsilon(x) = l(x, v) \)。我们做如下假设

\[ \psi_0(x) < \infty, \forall x. \]

我们取 \( \psi_0 \) 作为上限函数。它与没有冲动的控制问题相同。

我们现在可以写出与回报 (8.1.3) 对应的 Bellman 方程。这是功能方程

\[ u(x) = \inf \left\{ \begin{aligned} & [l(x, v, w) + \alpha \Phi^{v,w} u(x)]. \\ & v \in U \\ & w \ge 0 \end{aligned} \right\} \]

前面的方程等价于

\[ u(x) = \inf_{v \in U} \left\{ \begin{aligned} & [l(x + v, w) + c(w) + \alpha \Phi^u u(x + w)] \\ & w \ge 0 \end{aligned} \right\} \]

## 8.2. 功能方程的研究

### 8.2.1. 一般结果。

作为定理 4.3 的结果，我们可以陈述如下

定理 8.1. 在假设 (4.3.1)、(4.3.2)、(8.1.2)、(8.1.6) 下，满足

\[ 0 \le u(x) \le v_0(x) \quad \forall x, \]

的功能方程 (8.1.8) 的解集非空，并具有最小解和最大解，分别记为 \( \underline{u}(x) \) 和 \( \overline{u}(x) \)。最小解是下半连续的。

作为定理 4.4 的结果，我们还可以断言

定理 8.2. 在定理 8.1 的假设下，最小解是值函数

\[ \underline{u}(x) = \inf_{V,W} J_V(x, W). \]

此外，存在通过最优反馈 \( \hat{v}(x), \hat{w}(x) \) 得到的最优决策规则 \( \hat{V}, \hat{W} \)。

### 8.2.2. 有界情况。

在本节中，我们还假设

\[ (8.2.1) \quad l(x, v) \text{ 是有界的}, \]

则有

定理 8.3. 在定理 8.1 和 (8.2.1) 的假设下，(8.1.8) 在区间 \( 0, \psi_0 \) 中的解 \( u \) 是唯一的。

证明。函数 \( \psi_0 \) 是有界的。因此，最小解和最大解之间的所有解都是有界的。我们可以使用收缩映射论证。确实，设 \( z \) 为一个下半连续有界函数。我们考虑映射

\[ Tz(x) = \begin{cases} \inf_{v \in U} [l(x+w, v) + c(w) + \alpha \Phi^v z(x+w)]. \\ w \ge 0 \end{cases} \]

很容易检查它是系数为 \( \alpha \) 的收缩映射。因此，唯一性得证。

## 8.3. 另一种表述

### 8.3.1. 重写 Bellman 方程。

在本节中，我们考虑有界情况，因此解 \( u \) 是唯一的。我们可以将方程 (8.1.8) 重写如下

\[ (8.3.1) \quad u(x) = \min \left[ \inf_{v \in U} (l(x, v) + \alpha \Phi^v u(x)), \quad K + \inf_{\substack{v \in U \\ w \ge 0 \\ w \neq 0}} (l(x+w, v) + c_0(w) + \alpha \Phi^u u(x+w)) \right]. \]

我们现在将考虑 (8.3.1) 的另一种表述。

### 8.3.2. 变量分离。

在本节中，我们对函数 \( l(x, v) \) 做出更强的假设。我们将假设 (8.3.2) \( l(x, v) \) 一致连续、有界且为正。

我们将在 \( C = C(X) \)（一致连续有界函数空间）中寻找函数 \( u(x) \)。

我们在 \( C \) 上定义两个算子，即 \( T(z)(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v z(x)] \),

和

\[ M(z)(x) = K + \inf_{\substack{w \ge 0 \\ w \neq 0}} (c_0(w) + z(x + w)). \]

我们考虑以下问题：找到 \( u \in C \) 使得 (8.3.3) \( u(x) = \min[M(u)(x), T(u)(x)] \)。

我们的目标是证明以下内容

定理 8.4. 在假设 (4.3.1)、(4.3.2)、(8.1.2)、(8.3.2) 下，功能方程 (8.3.3) 存在且仅存在一个正有界解。该解属于 \( C \)。

### 8.3.3. 两种表述的同一性。

问题 (8.3.3) 和 (8.3.1)（等价于 (8.1.8)）是否一致并不明显。事实上，(8.1.8) 的解也是 (8.3.4) \( u(x) = \min[M(T(u))(x), T(u)(x)] \) 的解，

而不是 (8.3.3)。我们将证明 (8.3.3) 的解也是 (8.3.4) 的解，因此也是 (8.1.8) 的解。由于 (8.1.8) 的解是唯一的，只需证明 (8.3.3) 的解存在即可。那么 (8.3.3) 只有一个解，两个问题是等价的。为了证明 (8.3.3) 的解也是 (8.3.4) 的解，我们必须证明如果 \( u \) 是 (8.3.3) 的解，则 (8.3.5) \( u(x) = M(u)(x) \Rightarrow u(x) = M(T(u))(x) \),

而不仅仅是 \( u(x) \le M(T(u))(x) \)。确实，从 \( u \le Tu \Rightarrow M(u) \le M(T(u)) \),

我们得到 \( u(x) \le \min[M(T(u))(x), T(u)(x)] \),

并且 (8.3.5) 也蕴含逆不等式。因此，证明 (8.3.5) 是剩下的唯一事情。

设 \( x \) 使得 \( u(x) = M(u)(x) \)。设 \( \epsilon < \frac{K}{2} \)，我们可以找到 \( w_x \) 使得 \( u(x) \ge K + c_0(w_x) + u(x + w_x) - \epsilon \)。

我们将证明 (8.3.6) \( u(x + w_x) = T(u)(x + w_x) \),

这意味着 \( u(x) \ge K + c_0(w_x) + T(u)(x + w_x) - \epsilon \),

因此 \( u(x) \ge M(T(u))(x) - \epsilon \)。

由于 \( \epsilon \) 可以任意小，我们有 \( u(x) \ge M(T(u))(x) \)。由于逆不等式成立，我们有等式，因此 \( u \) 也是 (8.3.4) 的解。为了证明 (8.3.6)，我们声称如果 (8.3.6) 不成立，则应有

\[ u(x+w_x) = M(u)(x+w_x). \]

但此时存在 \( \bar{w}_x \) 使得

\[ u(x+w_x) \ge K + c_0(\bar{w}_x) + u(x+w_x+\bar{w}_x) - \epsilon. \]

汇总结果，我们可以写出

\[ u(x) \ge 2K + c_0(w_x) + c_0(\bar{w}_x) + u(x+w_x+\bar{w}_x) - 2\epsilon. \]

利用 \( c_0 \) 的次线性性质，我们可以断言

\[ u(x) \ge 2K + c_0(w_x+\bar{w}_x) + u(x+w_x+\bar{w}_x) - 2\epsilon. \]

因此也有

\[ u(x) > K + \inf_{w \ge 0} [c_0(w) + u(x+w)], \]

根据 \( \epsilon \) 的选择。这是一个矛盾。

**注 8.1.** 我们可以分别定义最优反馈 \( \hat{v}(x), \hat{w}(x) \)。首先通过最小化 \( l(x,v) + \Phi^{\hat{w}}(x,v) \) 定义 \( \hat{v}(x) \)。接下来，如果 \( u(x) < M(u)(x) \)，则 \( \hat{w}(x) = 0 \)。如果 \( u(x) = M(u)(x) \)，则 \( \hat{w} \) 在 \( w \ge 0 \) 中最小化 \( c_0(w) + u(x+w) \)。

### 8.3.4. 第二种表述的直接研究。

如果我们想研究 (8.3.3) 的不动点，上面得到的等价性以及应用于 \( v, w \) 对的一般理论表明不动点存在且唯一。因此，定理 8.4 的证明可以以这种方式进行。我们在此给出一个直接证明，这允许引入有用的技术，类似于用于最优停止的技术。事实上，我们在此考虑的冲动控制问题对应于选择最优停止时间序列，而不仅仅是一个。

我们首先证明最多存在一个正有界解。我们使用一种类似于用于遍历最优停止问题的方法，见第 7.4.2 节。然而，必须注意一个重大差异。

在这里我们需要 \( \alpha < 1 \) 才能处理有界解，而在最优停止问题中有一个自然界限，我们可以取 \( \alpha = 1 \)。

### 证明。唯一性

现在考虑两个正解 \( u_1, u_2 \)，它们被常数 \( C_0 \) 有界。定义

\[ \gamma = \sup \{ \beta \in [0, 1] \mid \beta u_1(x) \le u_2(x), \forall x \}. \]

这个数定义良好。确实

\[ \gamma = \inf_{\{x \mid u_1(x) > 0\}} \frac{u_2(x)}{u_1(x)}. \]

我们将证明 \( \gamma = 1 \)。这将蕴含 \( u_1(x) \le u_2(x) \forall x \)。通过对称性，我们也将得到逆性质，因此得到唯一性。

假设 \( 0 \le \gamma < 1 \)。我们将构造一个数 \( \beta \) 使得 \( \gamma < \beta \le 1 \) 且

\[ \beta u_1(x) \le u_2(x), \forall x, \]

这将导致矛盾。现在 \( \beta u_1 \) 满足

\[ \beta u_1 = \min \{ \beta M(u_1), \beta T(u_1) \}. \]





现在 \(\beta T(u_1)(x) \le T(\beta u_1)(x)\)。假设我们找到 \(\beta\) 使得 \(\gamma < \beta \le 1\) 且 \(\beta M(u_1)(x) \le M(u_2)(x)\)。

那么将由下面的引理 8.1 得出 \(\beta u_1(x) \le u_2(x), \forall x\)，故 \(\beta \le \gamma\)，这将是一个矛盾。验证所需性质意味着

\(K\beta + \inf_{w \ge 0} (\beta c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + u_2(x+w))\).

利用 \(\gamma u_1 \le u_2\)，只需验证

\(K\beta + \inf_{w \ge 0} (\beta c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w))\).

or

\(K\beta + \inf_{w \ge 0} (c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w))\).

我们希望 \(\beta > \gamma\)。由于 \(u_1 - C_0 \le 0, u_2 - C_0 \le 0\)，我们还有

\(\inf_{w \ge 0} (c_0(w) + \beta u_1(x+w)) \le \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w)) + (\beta - \gamma)C_0\).

因此，只需选择 \(\beta\) 使得

\((\beta - \gamma)C_0 \le K(1 - \beta)\).

设

\(\rho = \frac{K}{C_0}\).

我们可以取

\(\beta = \frac{\rho + \gamma}{\rho + 1}, \gamma < \beta \le 1\).

我们现在证明存在性。我们从一些初步结果开始。

**引理 8.1.** 设 \(\psi \in C\) 且 \(S(w) = z \in C\) 是

\(z = \min[\psi, T(z)]\).

的解。若 \(\zeta \in C\) 满足

\(\zeta \le \psi, \zeta \le T(\zeta)\),

则 \(\zeta \le z\)。

证明。考虑映射 \(\Sigma : C \to C\)，定义为

\(\Sigma(z) = \min[\psi, T(z)]\).

算子 \(\Sigma\) 是收缩映射且单调递增。由于根据假设

\(z = \Sigma^n(z), \zeta \le \Sigma^n(\zeta)\),

故

\(z - \zeta \ge \Sigma^n(z) - \Sigma^n(\zeta)\).

令 \(n\) 趋于 \(\infty\)，右边趋于 0。因此结果已得到。

**引理 8.2.** 算子 \(S\) 是凹的，即

\(S(\lambda \psi_1 + (1-\lambda)\psi_2) \ge \lambda S(\psi_1) + (1-\lambda)S(\psi_2), \forall \lambda \in [0, 1]\)

**练习 8.1.** 证明 \(T\) 是凹的，并进一步验证 \(S\) 也是凹的，利用引理 8.1。

**引理 8.3.** 算子 \(S\) 是单调递增的

**练习 8.2.** 利用引理 8.1 证明引理 8.3。

接下来定义

\(A(z)(x) = S(M)(z)(x)\)。

**练习 8.3.** 验证 \(A\) 是凹的且单调递增。

令 \(\overline{u}\) 为 \(\overline{u} = T(\overline{u})\) 的唯一解。则 \(0 \le \overline{u} \le C_0\)。我们可以定义 \(\lambda > 0\) 使得 \(\lambda \overline{u}(x) \le K, \forall x\)。

我们给出如下结论

**引理 8.4.** 设 \(z, \zeta \in C\) 为正，且 \(\beta \in [0, 1]\) 使得

\(z(x) - \zeta(x) \le \beta z(x), \forall x,\)

则

\(A(z)(x) - A(\zeta)(x) \le \beta(1-\lambda)A(z)(x), \forall x.\)

根据假设，\((1-\beta)z(x) \le \zeta(x)\)。利用 \(A\) 的单调性和凹性，我们可以写出

\(A(\zeta)(x) \ge A((1-\beta)z)(x) \ge (1-\beta)A(z)(x) + \beta A(0)(x)\)

然而 \(A(0) = S(M(0)) = S(K)\)。但由 \(\lambda \overline{u}(x) \le K\) 且 \(\lambda \overline{u}(x) = \lambda T(\overline{u})(x)\)，故 \(\lambda \overline{u}(x) \le T(\lambda \overline{u})(x)\)，利用引理 8.1 可得

\(\lambda \overline{u}(x) \le S(K) = A(0).\)

综合以上结果，我们写出

\(A(\zeta)(x) \ge (1-\beta)A(z)(x) + \beta \lambda \overline{u}(x).\)

现在

\(A(z) \le T A(z) \quad \overline{u} = T \overline{u}\)

并且通过与引理 8.1 类似的推理，我们推导出 \(A(z)(x) \le \overline{u}(x)\)。因此

\(A(\zeta)(x) \ge (1-\beta)A(z)(x) + \beta \lambda A(z)(x),\)

这正是性质 (8.3.8)。

我们可以转向定理 8.4 中存在性的直接证明。

证明。存在性：

这等同于证明算子 \(A\) 有一个不动点。我们考虑递减序列

\(u^{n+1} = A(u^n) \quad u^0 = \overline{u}\)

我们有

\(u^0 \ge \dots \ge u^n \ge \dots\)

由于 \(u^0 - u^1 \le u^0\)，由引理 8.4 可得

\(A(u^0) - A(u^1) \le (1-\lambda)A(u^0),\)

即

\(u^1 - u^2 \le (1-\lambda)u^1.\)

迭代可得

\(u^m - u^{m+1} \le (1-\lambda)^m u^m \le (1-\lambda)^m u^0.\)

我们容易推断，对于 \( n \ge m \)

\( u^m - u^n \le \frac{(1-\lambda)^m}{\lambda} u^0. \)

令 \( n \) 趋于 \(\infty\)，我们得到 \( u^n \downarrow u \)，因此也有

\( u^m - u \le \frac{(1-\lambda)^m}{\lambda} u^0 \le \frac{(1-\lambda)^m}{\lambda} C_0, \)

这证明了极限 \( u \in C(X) \)。接下来我们检查

\( M(u^n) \downarrow M(u) \text{ and in } C \)

\( T(u^{n+1}) \downarrow T(u) \text{ and in } C \)

由于

\( u^{n+1} = \min[M(u^n), T(u^{n+1})], \)

极限 \( u \) 是一个解。证明已完成。

## 8.4. 概率解释

在定理 8.2 中，我们已经用随机控制问题的值函数给出了函数方程 (8.18) 解的一种概率解释。该表述中没有停时。以类似于最优停止中所见的方式（参见定理 7.5），我们将得到一种涉及停时作为决策变量的不同表述。事实上，我们将解释第二种表述，即方程 (8.3.3)。同样，为简化技术细节，我们仅限于 (8.3.3)，这意味着成本 \( l(x, v) \) 是有界的。

我们采取一种控制策略 \( V = \{v_1, \cdots, v_n, \cdots \} \)，其中 \( v_n \) 是 \( \mathcal{Y}_n \) 可测的，且属于 \( U \)。控制策略 \( W\) 将以略有不同的方式定义。我们考虑一组 \( \mathcal{Y}^m \) 停时 \( \{\tau_1, \cdots, \tau_n, \cdots \} \)。我们假设没有累积，即 \( \tau_n < \tau_{n+1}, \forall n, \text{a.s.} \)。考虑 \( \tau_n \) 之前事件的 \(\sigma\)-代数 \( \mathcal{Y}^{\tau_n} \) 以及一组 \( \mathcal{Y}^{\tau_n} \) 可测的随机变量 \( \xi_{\tau_n} \)，其值在 \( X = R^d \) 中。\( \xi_{\tau_n} \ge 0, \neq 0 \)。我们关联如下定义的控制 \( W = \{w_1, \cdots, w_n, \cdots \} \)

\( w_{\tau_n} = \xi_{\tau_n}, \)

\( w_j = 0 \text{ if } j \neq \tau_1, \cdots, \tau_n, \cdots \)

我们可以验证 \( w_j \) 是 \( \mathcal{Y}^j \) 可测的，\( \forall j \)。然后我们可以考虑 \( J_x(V, W) \) 并将其写为

\( J_x(V, W) = E^{V, W}_x \sum_{n=1}^\infty \alpha^{\tau_n - 1} \left[ K + c_0(\xi_{\tau_n}) + l(y_{\tau_n} + \xi_{\tau_n}, v_{\tau_n}) + \sum_{j=\tau_n+1}^{\tau_{n+1}-1} \alpha^{j-\tau_n} l(y_j, v_j) \right]. \)

对于最优反馈 \( \hat{v}(x), \hat{w}(x) \)，我们关联如下定义的控制策略 \( \hat{V}, \hat{W} \)

\( \hat{v}_n = \hat{v}(y_n) \)

\( \hat{w}_n = \hat{w}(y_n) \)

接下来定义

\(\hat{\tau}_1 = \inf\{n \ge 1 | \hat{w}_n \neq 0\}\)

\(\hat{\tau}_2 = \inf\{n \ge \hat{\tau}_1 + 1 | \hat{w}_n \neq 0\}\)

\(\dots\)

和

\(\hat{\xi}_{\hat{\tau}_j} = \hat{w}_{\hat{\tau}_j}\)。

使用与定理 7.2 类似的论证，我们可以得到

\(u(x) = J_*(V, \hat{W}) = \inf J_*(V, W)\)

本页故意留空

# 带设置成本的库存控制

冲动控制技术将现在应用于研究库存控制中的设置成本情况。第 5 章中引入的基准库存策略将被 H. Scarf [35] 引入并由许多作者研究的 s, S 策略概念所取代。我们将首先考虑一种无积压的确定性情况，但不同于第 5 章第 5.3 节的情况。

## 9.1. 确定性模型

### 9.1.1. 模型描述。

我们假设库存按以下方式演变

\[
(9.1.1) \quad y_{n+1} = y_n + v_n - D \quad y_1 = x,
\]

并受约束

\[
(9.1.2) \quad v_n \ge 0, y_n \ge 0.
\]

新之处在于状态约束。没有未满足的需求。由于需求 \( D \) 是确定性的，这转化为对控制的约束，该约束取决于状态

\[
(9.1.3) \quad v_n \ge D - y_n.
\]

定义 \( V = \{v_1, \cdots, v_n, \cdots\} \)，我们考虑目标函数

\[
(9.1.4) \quad J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} [K \mathbb{I}_{v_n > 0} + c v_n + h y_n],
\]

并且我们想要研究值函数

\[
(9.1.5) \quad u(x) = \inf_V J_x(V).
\]

新增项是固定成本 \( K \mathbb{I}_{v_n > 0} \)，仅在订单 \( v_n \) 不为 0 时支付。这不是一个连续函数。如果我们记

\[
(9.1.6) \quad l(x, v) = K \mathbb{I}_{v > 0} + cv + hx,
\]

则函数 \( l(x, v) \) 在 \( v \) 中不连续。然而它是下半连续的。

### 9.1.2. 贝尔曼方程。

贝尔曼方程写为

\[
(9.1.7) \quad u(x) = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v > 0} + cv + \alpha u(x + v - D)].
\]

这个函数方程属于第 4 章研究的一般类别。我们将关注具体方面。

第一个重要事实如下



## 引理 9.1.

方程 (9.1.7) 右侧的 $v$ 集合可以由以下式子界定

(9.1.8)
$$ cv \le \frac{K+cD}{1-\alpha} + \frac{\alpha Dh}{(1-\alpha)^2}. $$

证明. 结果将由以下估计得出

$$ u(x) \ge \frac{hx}{1-\alpha} - \frac{\alpha Dh}{(1-\alpha)^2}, $$

该估计通过对函数方程 (9.1.7) 进行迭代得到，起始条件为 $u(x) \ge hx$。接下来，我们寻找 $u(x)$ 的上界函数。由于约束条件，我们不能像通常那样取对应 $v=0$ 的函数。我们将取 $v=D$。因此我们考虑函数方程

$$ w_0(x) = hx + K + cD + \alpha w_0(x), $$

其简化形式为

(9.1.9)
$$ w_0(x) = \frac{hx + K + cD}{1 - \alpha}. $$

我们寻找 (9.1.7) 在区间 $0 \le u(x) \le w_0(x)$ 内的解。从 $u$ 的下界和上界函数提供的上界出发，由方程 (9.1.7) 推出，$v$ 的值可由以下约束限制

$$ hx + cv + \frac{\alpha h(x-D)}{1-\alpha} - \frac{hD\alpha^2}{(1-\alpha)^2} \le \frac{hx + K + cD}{1-\alpha}. $$

我们看到含 $x$ 的项消去，剩下的就是估计 (9.1.8)。证明完毕。

由于 $v$ 的集合是有界的，我们可以应用定理 (4.2.4) 的技术来断言

## 定理 9.1.

在假设 (9.1.6) 下，函数方程 (9.1.7) 有且仅有一个下半连续（l.s.c.）解。该解即为值函数 (9.1.5)。此外，存在一个由反馈 $\tilde{v}(x)$ 定义的最优控制策略 $\tilde{v}$，它取得了 (9.1.7) 右侧的下确界。

### 9.1.3. 求解最优控制策略.

在本节中，我们有兴趣表征最优反馈 $\tilde{v}(x)$。我们首先给出方程 (9.1.7) 的另一种、更方便的形式。我们引入

(9.1.10)
$$ z(x) = cx + \alpha u(x). $$

然后很容易将方程 (9.1.7) 改写为如下形式

(9.1.11)
$$ u(x) = (h-c)x + cD + \inf_{\eta \ge \max(x, D)} [K \mathbb{1}_{\eta > x} + z(\eta - D)]. $$

我们从以下不等式开始

### 引理 9.2.

(9.1.12)
$$ z(x) \le K + z(y), \forall y > x. $$

证明. 设 \(x < y\)。由方程 (9.1.11) 可写出

$$
\begin{aligned}
u(x) + (c - h)x &= cD + \inf_{\eta \ge \max(x,D)} [K \mathbf{I}_{\eta > x} + z(\eta - D)] \\
\le cD + K + \inf_{\eta \ge \max(y,D)} z(\eta - D) \\
\le K + cD + \inf_{\eta \ge \max(y,D)} [K \mathbf{I}_{\eta > y} + z(\eta - D)] \\
\le K + u(y) + (c - h)y,
\end{aligned}
$$

这意味着

$$ u(x) + cx \le K + u(y) + cy.$$

但接着

$$
\begin{aligned}
z(x) &= \alpha(u(x) + cx) + cx(1 - \alpha) \\
\le \alpha K + \alpha(u(y) + cy) + cy(1 - \alpha) \\
\le K + z(y),
\end{aligned}
$$

结果得证。

### 命题 9.1.

解 \(u(x)\) 满足以下性质

(9.1.13)
\(x < D \implies u(x) = (h - c)x + cD + K + \inf_{\eta \ge 0} z(\eta)\)

(9.1.14)
\(x \ge D \implies u(x) = hx + \alpha(x - D).\)

证明. 对于 \(x < D\)，方程 (9.1.11) 写为

$$ u(x) = (h - c)x + cD + \inf_{\eta \ge D} [K \mathbf{I}_{\eta > x} + z(\eta - D)]. $$

因此

$$ u(x) = (h - c)x + cD + K + \inf_{\eta \ge D} z(\eta - D). $$

从而性质 (9.1.13) 得证。接下来，若 \(x \ge D\)，方程 (9.1.11) 变为

$$ u(x) = (h - c)x + cD + \inf_{\eta \ge x} [K \mathbf{I}_{\eta > x} + z(\eta - D)]. $$

但由引理 9.2 可知

$$ z(x - D) \le K + z(\eta - D), \forall x < \eta, $$

故

$$ u(x) = (h - c)x + cD + z(x - D). $$

回顾 \(z(x)\) 的定义，推出 (9.1.14)。证明完毕。

### 引理 9.3.

我们有以下性质

$$ \alpha u(0) \le u(0) \le cD. $$

证明. 我们有 \(\alpha u(0) = z(0)\)。现在由 (9.1.13)

$$ u(0) = cD + K + \inf_{\eta \ge 0} z(\eta). $$

但 \(\inf_{\eta \ge 0} z(\eta)\) 在某点 \(\eta^* \ge 0\) 处取得。但由引理 9.2 可知

$$ z(0) \le K + z(\eta^*), $$

结果随之得证。

我们现在可以断言主要结果

## 定理 9.2.

我们假设 (9.1.6)。最优反馈表征如下

(9.1.15)
\(\hat{v}(x) = \begin{cases} 0, & \text{if } x \ge D \\ D(1+\hat{k}) - x, & \text{if } x < D \end{cases}\)

其中 \(\hat{k}\) 是一个正整数，使以下量取得最小值

(9.1.16)
\(\lambda(k) = \frac{K + c(k+1)D + \alpha h D F(k)}{1 - \alpha^{k+1}},\)

其中

(9.1.17)
\(F(k) = \frac{\alpha^{k+1} - (k+1)\alpha + k}{(1 - \alpha)^2}.\)

证明. 由命题 9.1 可知 \(u(x)\) 是分段线性的，但不连续。不连续点为 \(Dk, k = 1, 2, \cdots\) 我们记

$$ u(0) = cD + K + \inf_{\eta \ge 0} z(\eta). $$

我们可以轻易得到 \(u((kD)^+)\) 和 \(u((kD)^-)\) 的公式，其中这些符号分别表示在点 \(kD\) 处的右极限和左极限。确实，对于 \(k \ge 1\)

$$ u(((j+1)D)^-) = hD(j+1) + \alpha u((jD)^-), $$

我们轻易推出

(9.1.18)
\(u(((k+1)D)^-) = hD \sum_{j=0}^k (k+1-j)\alpha^j + \alpha^k(u(0) - cD), k \ge 0.\)

类似地，对于 \(k \ge 0\)

$$ u(((j+1)D)^+) = hD(j+1) + \alpha u((jD)^+), $$

因此

(9.1.19)
\(u(((k+1)D)^+) = hD \sum_{j=0}^k (k+1-j)\alpha^j + \alpha^{k+1}u(0), k \ge 0.\)

由引理 9.3 可见

$$ u(((k+1)D)^+) \le u(((k+1)D)^-), \forall k \ge 0 $$

由于 \(z(x)\) 也是分段线性的，且与 \(u(x)\) 具有相同的不连续点，由此不等式可知

(9.1.20)
\(\inf_{\eta \ge 0} z(\eta) = \inf_{k \ge 0} [ckD + \alpha u((kD)^+)].\)

我们可以对 \(k \ge 1\) 计算

$$ F(k) = \sum_{j=0}^{k-1} (k-j)\alpha^j $$
$$ = k \frac{1-\alpha^k}{1-\alpha} - \frac{\alpha}{(1-\alpha)^2}(1 - k\alpha^{k-1} + (k-1)\alpha^k) $$
$$ = \frac{\alpha^{k+1} - (k+1)\alpha + k}{(1-\alpha)^2}. $$

注意，该表达式对 \(k=0\) 也成立，取 \(F(0)=0\)。因此我们可以写出

$$ u((kD)^+) = F(k) + \alpha^k u(0), k \ge 0 $$

因此由 (9.1.20) 可得

(9.1.21)
\( \inf_{n \ge 0} z(n) = \inf_{k \ge 0} [ckD + \alpha h D F(k) + \alpha^{k+1} u(0)] . $$

现在由 (9.1.13) 可知

$$ u(0) = K + \inf_{k \ge 0} [c(k+1)D + \alpha h D F(k) + \alpha^{k+1} u(0)] , $$

由此轻易得出

$$ u(0) = \inf_{k \ge 0} \lambda(k), $$

其中 \(\lambda(k)\) 由 (9.1.16) 给出。若 \(\hat{k}\) 取得下确界，则 \(\hat{k}D\) 也取得 \(z(n)\) 的下确界。由于对于 \(x < D\)，该下确界由 \(x + \hat{v}(x) - D\) 取得，根据反馈的定义，我们可断言

$$ x + \hat{v}(x) - D = \hat{k}D, $$

从而得到 (9.1.15)。注意 \(\lambda(k)\) 取得其下确界，因为当 \(k \to \infty\) 时 \(\lambda(k) \to \infty\)。

我们现在考虑特殊情况

### 命题 9.2.

假设

(9.1.22)
\( \alpha(K + cD) \le cD + \alpha hD, \)

则 \(\hat{k} = 0\).

证明. 我们利用以下事实：\(\hat{k}\) 也是使 \(c(k+1)D + \alpha h D F(k) + \alpha^{k+1} u(0)\) 取得最小值的 \(k\) 值。让我们证明，在做出该假设时，该函数关于 \(k\) 是单调递增的。利用

$$ F(k+1) - F(k) = \frac{1 - \alpha^{k+1}}{1 - \alpha}, $$

我们必须检查，对于任何 \(k\)，都有

$$ u(0)(\alpha^{k+1} - \alpha^{k+2}) \le cD + \alpha hD \frac{1 - \alpha^{k+1}}{1 - \alpha}. $$

我们知道

$$ u(0) \le w_0(0) = \frac{K + cD}{1 - \alpha}. $$

因此，只需验证

$$ \alpha^{k+1}(K + cD) \le cD + \alpha hD \frac{1 - \alpha^{k+1}}{1 - \alpha}, $$

即

$$ \alpha^{k+1} \left[ K + cD + \frac{hD\alpha}{1 - \alpha} \right] \le cD + \frac{\alpha hD}{1 - \alpha}, $$

并且只需检查当 \(k=0\) 时该不等式成立，这正是条件 (9.1.22)。

### 注释 9.1.

最优反馈据说源于 s, S 策略，其中 s = D 且 S = D(k + 1)。注意，若 K = 0，则 (9.1.22) 成立且 k = 0，这意味着 s = S。在这种情况下，我们有一个基础库存策略，基础库存等于需求。若我们考虑最优策略 \(\hat{V} = \{\hat{v}_1, \cdots, \hat{v}_n, \cdots \}\) 及相应的库存演化 \(\hat{y}_1, \cdots, \hat{y}_n, \cdots\)，则具有以下性质

(9.1.23)
\(\hat{y}_n \hat{v}_n = 0, \forall n\)

该性质称为 Wagner-Whitin 定理。

## 9.2. 固定成本且无短缺的库存控制

### 9.2.1. 贝尔曼方程

我们考虑第 5 章第 5.1 节的类比。我们定义函数 \(l(x, v)\) 如下

(9.2.1)
\(l(x, v) = K \mathbf{1}_{\{v>0\}} + cv + hx + p E(x + v - D)^- ,\)

这与方程 (5.1.8) 相同，只是每次下订单时都会产生固定成本 \(K\)，无论订单大小。注意 \(K \mathbf{1}_{\{v>0\}}\) 是下半连续的。它包含订购成本（纯粹的变动成本）、持有成本以及销售损失的惩罚。我们注意到以下不等式

(9.2.2)
\(K \mathbf{1}_{\{v>0\}} + cv + hx \le l(x, v) \le K \mathbf{1}_{\{v>0\}} + cv + hx + p \bar{D},\)

其中 \(\bar{D} = ED\)。因此函数 \(l(x, v)\) 满足性质 (4.3.2)、(4.5.1) 以及第一个条件 (4.5.4)，其中

(9.2.3)
\(l_0 = p \bar{D}.\)

算子 \(\Phi^v\) 由 (5.1.2) 定义，或等价地由 (5.1.5) 定义。我们注意到假设 (4.3.1)、(4.5.2)、(4.5.4) 均满足。

因此第 4 章的结果，特别是定理 4.8 适用。函数方程 (4.3.7) 读作

(9.2.4)
\(u(x) = \inf_{v \ge 0} \{ l(x, v) + \alpha E u((x + v - D)^+) \}.\)

我们也可以将其写为

(9.2.5)
\(u(x) = (h - c)x + \inf_{\eta \ge x} \{ K \mathbf{1}_{\{\eta > x\}} + c\eta + p E((\eta - D)^-) + \alpha E u((\eta - D)^+) \}.\)

相应的控制问题表述如下：状态方程为

(9.2.6)
\(y_{n+1} = (y_n + v_n - D_n)^+ \quad y_1 = x,\)

其中 \(D_n\) 相互独立且同分布，概率密度为 \(f(.)\)，累积分布函数为 \(F(.)\)。目标函数为

(9.2.7)
\(J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} E l(y_n, v_n),\)

与往常一样，\(V = \{v_1, \cdots, v_n, \cdots \}\)。这种表述当然等同于第 4 章中描述的受控马尔可夫链。我们可以断言



### 定理 9.3.
在假设 (9.2.1) 和 (5.1.2) 下，方程 (9.2.4) 在空间 $B_1$ 中存在且仅存在一个解。该函数是下半连续的（l.s.c.）。存在一个最优反馈 $\hat{v}(x)$，满足估计

(9.2.8)
\(\hat{v}(x) \le \frac{p\bar{D}}{c(1-\alpha)}.\)

解 \(u(x) = \inf_v J_v(x)$，即值函数。存在一个最优控制策略 \(\hat{V}$，由反馈 \(\hat{v}(x)$ 得出。

## 9.2.2. 最优策略.

重要的问题是刻画最优反馈，就像我们在无固定成本 \(K = 0$ 的情况下所做的那样，参见第 5 章，第 5.1.3 节。当存在固定成本时，我们无法得到基准库存策略。我们已经在确定性情况下看到，参见第 9.1 节，最优反馈是由 s, S 策略得到的，其中 \(s = D$。我们将看到，这种结构在随机情况下依然有效，只是 s, S 的值自然不同。遵循第 8 章发展的冲动控制理论，我们将确定 s, S 的值。

我们引入算子

(9.2.9)
\(T(u)(x) = hx + pE((x - D)^-) + \alpha Eu((x - D)^+),\)

(9.2.10)
\(M(u)(x) = K + \inf_{\eta \ge x} [(c - h)(\eta - x) + u(\eta)].\)

我们现在面临与第 8.3 节类似的情况。我们注意到函数方程 (9.2.5) 等价于

\(u(x) = \min[T(u)(x), M(T(u))(x)].\)

然而，这也等价于

(9.2.11)
\(u(x) = \min[T(u)(x), M(u)(x)].\)

这种表述是 (9.2.5) 的冲动控制表述。没有“连续”控制，因此算子 \(T(u)(x)$ 是仿射的。我们处于定理 8.4 的条件下，关于成本有界性有一个重要的区别。请注意，这里的变量订购成本是 \((c - h)v$ 所以我们假设

(9.2.12)
\(p > c > h.\)

第一个不等式是必不可少的，因为否则没有订购动机。第二个不等式不那么关键，但为了与我们对冲动控制问题的一般表述保持一致而采用。此外，它对于得到 s, S 策略将是必不可少的。我们不能使用定理 8.4 来证明解的存在性和唯一性，因为函数 \((x, v)$ 不是有界的。然而，通过与表述 (9.2.5) 的等价性，我们知道情况确实如此。因此，构造一个最优反馈由 s, S 策略给出的解就足够了。

我们从一些记号开始。定义

(9.2.13)
\(g(x) = (p - \alpha(c - h))E(x - D)^+ - (p - c)x + p\bar{D}.\)

对于任何 \(s \ge 0$，接下来定义

(9.2.14)
\(g_s(x) = (g(x) - g(s)) \mathbb{1}_{x > s}.\)

让我们设定

(9.2.15)
$$H_s(x) = \sum_{n=1}^\infty \alpha^{n-1} g_s * f^{*(n-1)}(x),$$

采用 (5.1.17) 的记号。

### 引理 9.4.
函数 $H_s(x)$ 在大于或等于 $s$ 的点处取得其最小值。取最小的最小值，定义一个函数 $S(s)$ 和

(9.2.16)
$$H_s(S(s)) = \inf_{\eta \ge s} H_s(\eta).$$

证明. 我们可以将 $H_s(x)$ 写为

$$H_s(x) = g_s(x) + \alpha g_s * f + \sum_{n=2}^\infty \alpha^n g_s * f^{*(n)}(x).$$

考虑

$$F^{(n)}(x) = \int_0^x f^{(n)}(\xi) \, d\xi,$$

则 $F^{(0)}(x) = 1, F^{(1)}(x) = F(x)$。如果

$$\Gamma(x) = \sum_{n=0}^\infty \alpha^n F^{(n)}(x),$$

那么我们可以轻松验证公式

(9.2.17)
$$H_s(x) = \int_s^x \Gamma(x-\xi) \mu(\xi) d\xi,$$

其中 $\mu = g'$。为函数 $F^{(n)}(x)$ 给出概率解释是有用的。事实上，我们有

$$F^{(n)}(x) = P(D_1 + \cdots + D_n \le x),$$

其中 $D_1, \cdots, D_n$ 是 $n$ 个独立同分布的随机变量，具有相同的概率密度 $f(x)$。这样一来，很明显

$$F^{(n)}(x) \uparrow 1, \text{ 当 } x \to \infty, \quad \Gamma(x) \uparrow \frac{1}{1-\alpha}, \text{ 当 } x \uparrow \infty.$$

因此，当 $x \uparrow \infty$ 时，$H_s(x) \to +\infty$。我们可以检查

$$H'_s(s+0) = \mu(s) = c(1-\alpha) + \alpha h - (p-\alpha(c-h))\bar{F}(s).$$

由于 $p > c$，函数 $\mu(s)$ 从 $-(p-c)$ 增加到 $(c(1-\alpha)+\alpha h)$。因此它在一点 $\bar{s}$ 处消失，并且对于 $0 \le s < \bar{s}$ 严格为负。这个 $\bar{s}$ 简单地是由公式 (5.1.14) 识别的基准库存。

首先考虑 $s \in [0, \bar{s}]$。因此 $H'_s(s+0) < 0$，函数 $H_s(x)$ 在 $x$ 接近 $s$ 时变为严格负值。此外

$$\begin{aligned} H_s(x) &= \int_s^x \Gamma(x-\xi)\mu(\xi)d\xi + \int_x^\infty \Gamma(x-\xi)\mu(\xi)d\xi \\ \ge \frac{1}{1-\alpha}(g(s) - g(s)) + g(x) - g(s). \end{aligned}$$

因此，当 $x \to \infty$ 时，$H_s(x) \to \infty$。由于它是连续函数，它在 $[0, \infty)$ 上取得其最小值。通过取最小的最小值（如果有多个），我们唯一地定义数字 \( S(s) \)。还要注意，如果 \( s \ge \bar{s}$，$H_s(x)$ 在 \( x \) 中是递增的，而对于 \( s < \bar{s}$，$H_s(x)$ 在区间 \( [s, \bar{s}) \) 上在 \( x \) 中是递减的，因此 \( S(s) = s$ 如果 \( s \ge \bar{s}$，$S(s) > s$ 如果 \( s < \bar{s}$。

还可以得出，对于 \( s < \bar{s}$，\( H'_s(S(s)) = 0$。因此

\(\frac{dH_s(S(s))}{ds} = \frac{\partial}{\partial s} H_s(x)_{x=S(s)}, \text{ 如果 } s < \bar{s}.\)

所以

(9.2.18)
\(\frac{dH_s(S(s))}{ds} = -\mu(s)\Gamma(S(s) - s) > 0, \text{ 如果 } s < \bar{s}.\)

显然，对于 \( s \ge \bar{s}$，$H_s(S(s)) = 0$。属性 (9.2.16) 已经证明。

现在考虑 \( S_0 = S(0)$。我们有

\( H_0(x) = \int_0^x \Gamma(\xi)\mu(x - \xi)d\xi. \)

所以

\( H'_0(x) = \mu(0)\Gamma(x) + \int_0^x \mu'(x - \xi)\Gamma(\xi) d\xi \)
\( = (c - p)\Gamma(x) + (p - \alpha(c - h)) \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

然而，很容易检查 \( \Gamma(x) \) 满足更新方程

(9.2.19)
\( \Gamma(x) = 1 + \alpha \int_0^x f(x - \xi)\Gamma(\xi) d\xi. \)

因此

\( H'_0(x) = \frac{1}{\alpha}[(p - \alpha(p - h))\Gamma(x) - (p - \alpha(c - h))]. \)

因此 \( S_0 \) 由以下给出

(9.2.20)
\( \Gamma(S_0) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)}. \)

我们需要假设

(9.2.21)
\( H_0(S_0) = \int_0^{S_0} \Gamma(\xi)\mu(S_0 - \xi)d\xi < -K. \)

我们可以陈述以下

### 定理 9.4.
在定理 9.3 和 (9.2.12), (9.2.21) 的假设下，函数方程 (9.2.5) 的最优反馈 \( \psi(x) \) 由一个 \( s, S \) 策略给出。\( s$ 的值是唯一的值，使得

(9.2.22)
\( K + \inf_{\eta \ge s} H_s(\eta) = 0, \)

并且 \( S(s) = s$。此外，函数 \( u(x) \) 是连续的

证明. 考虑函数 \( \inf_{\eta \ge s} H_s(\eta) = H_s(S(s)) \)。

我们有 \( H_s(S(s)) = 0$ 对于 \( s \ge \bar{s}$。从假设中，我们有 \( H_0(S(0)) < -K$。从 (9.2.18) 我们知道，对于 \( s < \bar{s}$，$H_s(S(s))$ 在 \( s$ 中是严格递增的。因此，将有一个且仅有一个 \( s$，使得 (9.2.22) 得到验证。因此，对 \( s, S$ 就被明确识别。我们将构造 (9.2.11) 的一个解，其最优反馈由一个 \( s, S$ 策略定义，使用刚刚定义的 \( s, S$ 值。为了简化记号，我们省略下标 s,S。我们使用记号 H(x) 表示 H_s(x)，使用特定的 s。考虑函数

(9.2.23)
\( u(x) = H(x) + (h - c)x + \frac{g(s)}{1 - \alpha} \).

由于 H(x) 是连续的，函数 u(x) 是连续的。然后 u(x) 满足

(9.2.24)
\( u(x) = \begin{cases} (h - c)x + \frac{g(s)}{1 - \alpha}, & x \le s \\ hx + pE(x - D)^- + \alpha Eu(x - D)^+, & x \ge s \end{cases} \)

并且，从 s 的选择中

(9.2.25)
\( K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] = \frac{g(s)}{1 - \alpha}, \)

因此也

(9.2.26)
\(\begin{aligned} u(s) + (c - h)s &= K + \inf_{\eta \ge s} [u(\eta) + (c - h)\eta] \\ &= K + u(S) + (c - h)S \end{aligned}\)

由于

\( u(x) = -(c - h)x + \frac{g(s)}{1 - \alpha}, \quad x \le s, \)

函数 u(x) + (c - h)x 在 $[0, s]$ 上是常数。因此

\(\inf_{\eta \ge x} [(c - h)\eta + u(\eta)] = \inf_{\eta \ge s} [(c - h)\eta + u(\eta)], \quad \forall x \le s.\)

因此函数 u 满足

\(\begin{aligned} u(x) &= M(u)(x), \forall x \le s \\ u(x) &= T(u)(x), \forall x \ge s \end{aligned}\)

因此，剩下要证明的是

\(\begin{aligned} u(x) \le T(u)(x), \forall x \le s \\ u(x) \le M(u)(x), \forall x \ge s \end{aligned}\)

用 H 表示，第一个不等式等于 $g_s(x) \ge 0, \forall x \le s$。这是成立的，因为 $\mu(\xi) < 0, \forall x \le \xi < s < S$。第二个不等式更复杂。用 H 表示，它等于

(9.2.27)
\( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s. \)

要证明 (9.2.27) 我们首先注意到，对于 x \ge s 我们有 \inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge s} H(\eta) \ge -K。所以不等式每当 H(x) \le 0 时肯定成立。然后考虑称为 x_0 的最小数，使得 H 变为正。我们有

\( H(x_0) = 0, H(x) < 0 \quad \forall x, s < x < x_0. \)

我们可以声称 $g_s(x_0) > 0$。这从关系 $g_s(x_0) = -\alpha E H(x_0 - D)$ 和 x_0 的定义所导出的性质中得出。为了继续，我们注意到关系 (9.2.15) 意味着

\( H(x) = g_s(x) + \alpha E H(x - D), \)

这对任何 x 成立，只要我们在 x \le 0 时通过将 H 的定义扩展为 0。





令 \xi > 0。我们考虑区域 x \ge x_0 - \xi。因此，低于 s 的值是可能的，甚至负值也是可能的。我们可以写出不等式

(9.2.28) \quad H(x) \le g_s(x) + \alpha E(H(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x.

这源于以下事实

E(H(x - D) \mathbb{1}_{x - D \le x_0 - \xi}) \le 0.

接下来定义

M(x) = H(x + \xi) + K.

显然 M(x) \ge 0。利用这一正性，我们可以写出

M(x) \ge \alpha E(M(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}) + M(x) - \alpha E M(x - D).

现在对于 x \ge x_0 - \xi，我们有

H(x + \xi) - \alpha E H(x + \xi - D) = g_s(x + \xi),

因此

M(x) - \alpha E M(x - D) = g_s(x + \xi) + K(1 - \alpha).

因此我们有

(9.2.29) \quad M(x) \ge g_s(x + \xi) + \alpha E(M(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi.

我们声称

(9.2.30) \quad g_s(x + \xi) \ge g_s(x), \forall x \ge x_0 - \xi.

确实，注意到 g_s(x + \xi) \ge g_s(x_0) \ge 0，因为 g 在 [s, \infty) 上是递增的。因此，当 x < s 时，不等式显然成立。如果 x \ge s，该不等式等价于 g(x + \xi) \ge g(x)。根据单调性性质，当 x \ge s 时这总是成立。因此，剩下的情况是 x < s < \xi。但在这种情况下，g_s(x) < 0，不等式满足。

让我们定义 Y(x) = H(x) - M(x)。根据不等式 (9.2.29) 和 (9.2.30)，我们可以得出

Y(x) \le \alpha E(Y(x - D) \mathbb{1}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi,

且 Y(x_0 - \xi) \le -K.

这两个性质蕴含 Y(x) \le 0, \forall x \ge x_0 - \xi。因此我们已得到 (9.2.27) 对所有 x \ge x_0 - \xi 成立，特别是对于 x > x_0 正如所期望的那样。我们已完成证明：由函数 H(x) 表征并由 (9.2.23) 定义的函数 u(x) 是 (9.2.11) 或 (9.2.5) 的一个解。因此它是值函数。

此外，s, S 策略与一个反馈相关联

(9.2.31) \quad \hat{v}(x) = \begin{cases} S - x, & \text{如果 } x \le s \\ 0, & \text{如果 } x > s \end{cases}

它是与 u 对应的最优反馈，这意味着

u(x) = l(x, \hat{v}(x)) + \alpha E u((x + \hat{v}(x) - D)^+).

对于这个反馈规则，我们可以关联一个概率 P^{\hat{v}, x}，在此概率下规范过程 y_n 演化为

y_{n+1} = (y_n + \hat{v}_n - D_n)^+ ,

其中 \(\tilde{v}_n = \tilde{v}(y_n)\)。我们还可以陈述
\(u(x) = \sum_{j=1}^n E^{\tilde{v}, x} l(y_j, \tilde{v}_j) + \alpha^n E^{\tilde{v}, \tau} u(y_{n+1}),\)

对于任意 n。但根据 s, S 策略的定义，有 0 \le y_{n+1} \le \max(x, S)。因此 u(y_{n+1}) 是有界的，故当 n \to \infty 时我们得到 u(x) = J_{\tilde{v}}(V).

**备注。** 当 K=0 时，我们有 s=S，且 S 由公式 (5.1.14) 给出。函数 u(x) 变为 C^1。

让我们证明以下性质

**命题 9.3.** 函数 S(s) 在 s 中是递减的，故 \bar{s} \le S(s) \le \min(S_0, \frac{p\bar{D}}{c(1-\alpha)}).

**证明.** 从关系 H'_s(S(s)) = 0 我们推导出
\frac{\partial}{\partial s} H'_s(S(s)) + H''_s(S(s)) S'(s) = 0.

现在，由于 S(s) 是一个极小值，H''_s(S(s)) > 0. 接下来使用
H'_s(x) = \mu(x) + \int_x^\infty \Gamma'(x-\xi)\mu(\xi)d\xi,

因此
\frac{\partial}{\partial s} H'_s(x) = -\Gamma'(x-s)\mu(s),

当 s < \bar{s} 时这为正，因为 \mu(s) < 0. 由此可得 S'(s) < 0. 结果得证。

**备注.** 我们知道 \bar{s} \le \frac{p\bar{D}}{c(1-\alpha)}，参见备注 5.1，因为 \bar{s} 对应于无固定成本情况下的基础库存策略。陈述中的不等式蕴含 \bar{s} \le S_0. 让我们直接证明这一事实。确实，我们使用（来自 \Gamma 的方程，(9.2.19））

\Gamma(S_0) \le \frac{1}{1-\alpha F(S_0)} = \frac{1}{1-\alpha + \alpha \bar{F}(S_0)}.

由此可得
F(S_0) \le \frac{c(1-\alpha) + \alpha h}{p - \alpha(c-h)} = \bar{F}(s),

由此我们推断 S_0 \ge \bar{s}. 另一方面，S_0 不一定与 \frac{p\bar{D}}{c(1-\alpha)} 可比。

## 9.2.3. K-凸性理论。

当 K=0 时，我们也证明了解是凸的。最优反馈的基础库存性质是凸性、连续性以及最小解在 x \uparrow \infty 时趋于 \infty 的直接结果。u 上的性质是递增序列 u_n 的类似性质的结果。

在当前背景下，最小解不能是凸的。幸运的是，这一性质可以被另一性质所取代，即 K-凸性。这，连同连续性和在无穷处趋于无穷的增长性，将足以保证最优反馈由一个 s, S 策略描述。这是文献中证明 s, S 策略的方式，自 H. Scarf 的开创性著作 [35] 以来。我们在上一节中看到，冲动控制技术允许在不使用 K-凸性的情况下获得结果。L. Benkherouf [3] 也在积压情况中考虑了类似的方法，这将在下一节中讨论。

然而还有一个额外的困难，因为该函数仅在正参数上定义。因此我们需要澄清仅在正参数上定义的 K-凸函数的性质，这在文献中通常不是这种情况。

一个函数 f 是 K-凸的，当且仅当对于 a < b < c 我们有

$$K + f(c) - f(b) \ge \frac{c-b}{b-a}(f(b) - f(a)).$$

我们需要考虑定义在 [0, \infty) 上的函数。在这种情况下，该性质对 a \ge 0 成立。

**定理 9.5.** 设 f(x) 是定义在 [0, \infty) 上的 K-凸函数，它是连续的，并且当 x \to \infty 时 f(x) \to \infty. 那么，存在数 s, S，其中 s \le S，使得

$$\begin{aligned} f(S) &= \min f(x) \\ s &= 0 \text{ 如果 } f(0) \le K + f(S) \\ f(s) &= K + f(S), \text{ 如果 } f(0) > K + f(S) \\ f(x) \text{ 在 } [0, s] \text{ 上严格递减，如果 } s > 0 \\ f(x) \le K + f(y), \forall x < y \end{aligned}$$

**证明.** 连续性和增长条件蕴含存在一点 S，在此处下确界达到。如果最小值在多个点达到，我们取 S 为最小的最小值。首先假设 f(0) \le K + f(S)，那么我们只需证明最后一句。取任意 x 使得 0 < x < S. 我们将证明 f(x) \le K + f(S). 这将蕴含 x < S 时的结果。当 f(x) \le f(0) 时，该陈述显然成立。因此我们可以假设 f(x) > f(0). 如果陈述不成立，那么我们将有 f(x) > K + f(S).

然而 K-凸性将蕴含

$$K + f(S) - f(x) \ge \frac{S-x}{x}(f(x) - f(0)),$$

这导致矛盾。剩下需要考虑的情况是 y > x > S，此时从 K-凸性我们得到

$$K + f(y) - f(x) \ge \frac{y-x}{x-S}(f(x) - f(S)) \ge 0.$$

s = 0 的情况已完成。因此我们可以假设 f(0) > K + f(S). 由于连续性，存在满足其定义条件的 s. 如果有多个，我们取最小值。令 0 < x < s, 应用 K-凸性我们有

$$0 = K + f(S) - f(S) \ge \frac{S-s}{s-x}(f(s) - f(x)),$$

因此

$$f(x) > f(s), \forall x < s.$$

现在取 0 < x_1 < x_2 < s, 再次由 K-凸性我们有

K + f(S) - f(x_2) \ge \frac{S - x_2}{x_2 - x_1} (f(x_2) - f(x_1)),

由于左边为负，我们得到 f(x_2) - f(x_1) < 0.

现在令 s < x < S，我们有

f(s) - f(x) = K + f(S) - f(x) \ge \frac{S - x}{x - s} (f(x) - f(s)),

这蕴含 f(s) > f(x). 最后，对于 s < x < y 我们可以写出

K + f(y) - f(x) \ge \frac{y - x}{x - S} (f(x) - f(S)) \ge 0.

证明已完成。

考虑

h(x) = \inf_{\eta \ge x} [f(\eta) + K \mathbf{1}_{\{\eta > x\}}],

那么

### 练习 9.1. 证明

$$h(x) = \begin{cases} f(x), & \text{如果 } s = 0 \\ f(s), & \text{如果 } 0 < x \le s \\ f(x), & \text{如果 } x > s \end{cases}$$

并且 h(x) 是 K-凸且连续的。注意 h(x) = f(\max(s, x)).

### 练习 9.2.

证明当 s > 0 时

h(x) \le h(y) + K, \forall x < y

我们将此理论应用于函数方程 (9.2.5). 我们设

G(\eta) = c\eta + p\mathbb{E}((\eta - D)^-) + \alpha \mathbb{E}u((\eta - D)^+),

那么方程 (9.2.5) 可以写成

(9.2.32) u(x) = (h - c)x + \inf_{\eta \ge x} \{K \mathbf{1}_{\{\eta > x\}} + G(\eta)\}.

我们将证明

u(x), G(x) \text{ 是 } K - \text{凸}.

显然当 x \uparrow \infty 时 G(x) \uparrow \infty. 为了保证 G(x) 连续，我们将做如下技术假设

(9.2.33) f \text{ 是连续的}.

### 练习 9.3. 证明每当 (9.2.33) 满足时，Eu((y - D)^+) 是连续的，因此 G(y) 也是连续的。由于 G(x) 是 K-凸的、连续的，并且当 x 趋于 \infty 时趋于 \infty，最优反馈由一个 s, S 策略描述。

**定理 9.6.** 在定理 9.9 及 (9.12)、(9.2.21)、(9.2.33) 的假设下，函数方程 (9.2.5) 的解是连续的、K-凸的，并且当 x \uparrow \infty 时趋于 \infty. 最优反馈由一个 s, S 策略定义。





证明。唯一需要证明的是 $K$-凸性。只需证明递增序列的 $K$-凸性即可。这通过归纳法证明。我们注意到

$$u_{n+1}(x) = (h-c)x + \inf_{\eta \ge x} \{K \mathbb{I}_{\eta > x} + G_n(\eta)\};$$

与

$$G_n(\eta) = c\eta + pE((\eta - D)^-) + \alpha E u_n((\eta - D)^+).$$

我们通过归纳法证明函数 $u_n(x), G_n(x)$ 是 $K$-凸的。假设它们是连续的，并且当 $x \to +\infty$ 时趋向于 $+\infty$。根据定理 9.5，我们将与 $G_n(x)$ 关联两个数 $s_n, S_n$。我们有如下表示式

$$u_{n+1}(x) = (h-c)x + G_n(\max(x, s_n)).$$

根据练习 9.1，我们推断 $u_{n+1}$ 也是 $K$-凸且连续的。另外，当 $x \to +\infty$ 时，$u_{n+1}(x) \to +\infty$。于是我们有

$$G_{n+1}(x) = cx + pE((x-D)^-) + \alpha(h-c)E((x-D)^+)) + \alpha E G_n(\max(x-D, s_n)).$$

函数

$$cx + pE((x-D)^-) + \alpha(h-c)E((x-D)^+) = (c(1-\alpha) + \alpha h)x + \alpha(h-c)D + (p+\alpha(h-c))E((x-D)^-)),$$

是凸的，且 $G_n(\max(x-D, s_n))$ 是 $K$-凸的。由此可知 $G_{n+1}(x)$ 是 $K$-凸的。它是连续的，并且当 $x \to +\infty$ 时趋向于 $+\infty$。

在取极限时，这一性质得以保持。

## 9.2.4. 概率方法.

我们将直接评估对应于任意 ($s,S$) 策略的成本。我们有如下

### 定理 9.7.
设 $V_{s,S}$ 为对应于 ($s,S$) 策略的控制，由反馈定义

$$V_{s,S} = \begin{cases} S-x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{cases}$$

对应的成本为：当 $x \le s$ 时

$$J_x(V_{s,S}) = (h-c)x + \frac{g(s)}{1-\alpha} + \frac{K+H_1(S)}{(1-\alpha)\Gamma(S-s)}.$$

当 $x > s$ 时，有

$$J_x(V_{s,S}) = (h-c)x + H_s(x) + \frac{g(s)}{1-\alpha} + (1-(1-\alpha)\Gamma(x-s)) \frac{K+H_1(S)}{(1-\alpha)\Gamma(S-s)}.$$

该函数在 $x=s$ 处除外是连续的。

### 证明.
设 $V_{s,S} = (v_1, \cdots, v_n \cdots)$ 和 $y_1, y_2 \cdots, y_n \cdots$ 为相应的库存演化。我们有 $y_1 = x$。我们首先考虑情况

- I. $x \le s$:

此时我们有 $v_1 = S-x$。我们设 $\tau_1 = 1$ 并定义停时序列

$$\tau_{k+1} = \tau_k + 1 + \inf \{n \ge 0 | D_{\tau_k} + \cdots + D_{\tau_k+n} \ge S-s\}.$$

回顾滤流 $\mathcal{F}^n = \sigma(D_1, \cdots, D_n), n \ge 1$。我们有

### 引理 9.5.
随机时间 \(\tau_k\) 相对于滤流 \(\mathcal{F}^{n-1}\) 是停时。此外，\(\tau_{k+1}-\tau_k-1\) 和 \(D_{\tau_k}, \cdots, D_{\tau_k+n}, n \ge 0\)，与 \(\mathcal{F}^{n-1}\) 相互独立。

### 证明.
我们将证明

\(\{\tau_k = n\} \in \mathcal{F}^{n-1}, n \ge 1.\)

我们对 \(k$ 进行归纳证明。当 \(k=1$ 时结果成立。注意 \(\tau_k \ge k$。假设结果对 \(\tau_k$ 成立，我们希望对 \(\tau_{k+1}$ 也成立。只需假设 \(n \ge k+1$，因为否则集合为空。若 \(n = k+1\)，则有

\(\{\tau_{k+1} = k+1\} = \{\tau_k = k\} \cap \{D_k \ge S - s\} \in \mathcal{F}^k,\)

结果成立。因此我们可以假设 \(n \ge k+2$。此时有

\(\{\tau_{k+1} = n\} = (\{\tau_k = n-1\} \cap \{D_{n-1} \ge S - s\})\)
\(\cup_{j=k}^{n-2} (\{\tau_k = j\} \cap \{D_j + \cdots + D_{n-1} \ge S - s\} \cap \{D_j + \cdots + D_{n-2} < S - s\}\)
\(\cap \{D_j + \cdots + D_{n-2} < S - s\}),\)

根据归纳假设，这属于 \(\mathcal{F}^{n-1}$。现在我们来证明第二部分。设 \(\xi\) 为一个 \(\mathcal{F}^{n-1}$ 可测的随机变量。那么 \(\mathbb{1}_{\{\tau_k \le j\}}$ 是 \(\mathcal{F}^{n-1}$ 可测的，\(j \ge k$。接下来考虑由公式定义的随机变量

\(\Phi(\tau_{k+1} - \tau_k - 1, D_{\tau_k}, \cdots, D_{\tau_k+m}),\)

其中函数 \(\Phi$ 是确定性的。我们必须证明

(9.2.38) \(E\Phi(\tau_{k+1} - \tau_k - 1, D_{\tau_k}, \cdots, D_{\tau_k+m}) \xi = E\Phi(\tau_{k+1} - \tau_k - 1, D_{\tau_k}, \cdots, D_{\tau_k+m})E\xi.\)

记 \(X = \Phi(\tau_{k+1} - \tau_k - 1, D_{\tau_k}, \cdots, D_{\tau_k+m})$。我们有

\(EX\xi = \sum_{j=k}^{\infty} \sum_{h=k}^{\infty} E\Phi(h, D_j, \cdots, D_{j+m})\mathbb{1}_{\tau_k=j}\mathbb{1}_{\tau_{k+1}=j+h+1}\xi\)
\(= \sum_{j=k}^{\infty} \sum_{h=k}^{\infty} E\Phi(h, D_j, \cdots, D_{j+m})\mathbb{1}_{\tau_k=j}\xi \mathbb{1}_{D_j+\cdots+D_{j+h} \ge S-s} \mathbb{1}_{D_j+\cdots+D_{j+h-1} < S-s}\)
\(+ \sum_{j=k}^{\infty} E\Phi(0, D_j, \cdots, D_{j+m})\mathbb{1}_{\tau_k=j}\xi \mathbb{1}_{D_j \ge S-s}.\)

由于 \(\mathbb{1}_{\tau_k=j}$ 是 \(\mathcal{F}^{j-1}$ 可测的，我们得到

\(EX\xi = \sum_{j=k}^{\infty} \sum_{h=k}^{\infty} E\Phi(h, D_j, \cdots, D_{j+m})\mathbb{1}_{D_j+\cdots+D_{j+h} \ge S-s} \mathbb{1}_{D_j+\cdots+D_{j+h-1} < S-s} E\mathbb{1}_{\tau_k=j}\xi\)
\(+ \sum_{j=k}^{\infty} E\Phi(0, D_j, \cdots, D_{j+m})\mathbb{1}_{D_j \ge S-s} E\mathbb{1}_{\tau_k=j}\xi.\)

但是

\(E\Phi(h, D_j, \cdots, D_{j+m})\mathbb{1}_{D_j+\cdots+D_{j+h} \ge S-s} = E\Phi(h, D_1, \cdots, D_{1+m})\mathbb{1}_{D_1+\cdots+D_{1+h} \ge S-s} = A_h;\)
\(E\Phi(0, D_j, \cdots, D_{j+m})\mathbb{1}_{D_j \ge S-s} = E\Phi(0, D_1, \cdots, D_{1+m})\mathbb{1}_{D_1 \ge S-s} = A_0,\)

与 $j$ 无关。因此

$$EX\xi = \sum_{h=0}^\infty A_h E\xi.$$

此外，应用此关系我们也有 $EX = \sum_{h=0}^\infty A_h$，从而 $EX\xi = EX E\xi$，即性质 (9.2.38)。这结束了引理的证明。

我们继续定理 9.7 的证明。控制 $V_{s,S}$ 的订货时刻是时间 $\tau_k$。此时库存为

$$y_{\tau_k} = (S - (D_{\tau_{k-1}} + \dots + D_{\tau_k - 1}))^+, \forall k \ge 2$$

订货量为

$$v_{\tau_k} = S - y_{\tau_k}, \forall k \ge 2$$

接下来我们可以定义缺货损失。在时间 $\tau_k - 1$，有

$$LS_{\tau_k-1} = (S - (D_{\tau_{k-1}} + \dots + D_{\tau_k - 1}))^-, \forall k \ge 2$$

我们最后定义时间 $\tau_{k+1}$ 和 $\tau_{k+1}-1$ 之间的库存，如果 $\tau_{k+1}-2 \ge \tau_k$。如果 $\tau_{k+1}-1 = \tau_k$，则自然有 $y_{\tau_{k+1}} = y_{\tau_k+1}$。否则

$$y_{\tau_k+1} = S - D_{\tau_k};$$
$$\dots$$
$$y_{\tau_{k+1}-1} = S - (D_{\tau_k} + \dots + D_{\tau_{k+1}-2}).$$

因此我们可以写出

$$(9.2.39) \quad J_x(V_{s,S}) = (h-c)x + K + cS + p \sum_{k=2}^\infty E\alpha^{\tau_k-2} LS_{\tau_k-1}$$
$$+ \sum_{k=2}^\infty E\alpha^{\tau_k-1}(K+cS+(h-c)y_{\tau_k})$$
$$+ h \sum_{k=1}^\infty E\alpha^{\tau_k-1}(\alpha y_{\tau_k+1} + \dots + y_{\tau_k+\tau_{k+1}-\tau_k-1}\alpha^{\tau_{k+1}-\tau_k-1}).$$
$$= I + II + III$$

我们首先考虑项 III。我们首先注意到

$$(9.2.40) \quad y_{\tau_k+1} + \dots + y_{\tau_k+\tau_{k+1}-\tau_k-1}\alpha^{\tau_{k+1}-\tau_k-2}$$
$$= S \frac{1-\alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} - \sum_{j=0}^{\tau_{k+1}-\tau_k-2} \alpha^j \sum_{l=0}^j D_{\tau_k+l}$$
$$= S \frac{1-\alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} - \sum_{l=0}^{\tau_{k+1}-\tau_k-1} D_{\tau_k+l} \frac{\alpha^l - \alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha}.$$

注意左边仅在 $\tau_{k+1} - \tau_k - 2 \ge 0$ 时有定义，当 $\tau_{k+1} - \tau_k - 1 = 0$ 时必须解释为 0。然而右边在

\(\tau_{k+1} - \tau_k - 1 \ge 0$ 时有定义，且当 \(\tau_{k+1} - \tau_k - 1 = 0$ 时消失。因此，公式 (9.2.40) 对于 \(\tau_{k+1} - \tau_k - 1 \ge 0$ 是有效的。根据引理 9.5，我们有

(9.2.41) \( E[y_{\tau_k+1} \cdots y_{\tau_k+\tau_{k+1}-\tau_k-1} | \mathcal{F}^{\tau_k}] = E \left[ S \frac{1-\alpha^\theta}{1-\alpha} - \sum_{l=0}^\theta D_{1+l} \frac{\alpha^l - \alpha^\theta}{1-\alpha} \right], \)

其中 \(\theta = \tau_{k+1} - \tau_k - 1$。注意对于 \(k \ge 1$，

\( y_{\tau_{k+1}} = (S - (D_{\tau_k} + \cdots + D_{\tau_k+\tau_{k+1}-\tau_k-1}))^+, \)

和

\(\alpha^{\tau_{k+1}-1} y_{\tau_{k+1}} = \alpha^{\tau_k-1} \alpha^{\tau_{k+1}-\tau_k-1} \alpha (S - (D_{\tau_k} + \cdots + D_{\tau_k+\tau_{k+1}-\tau_k-1}))^+.\)

因此我们可以断言

(9.2.42) \( E[\alpha^{\tau_{k+1}-1} y_{\tau_{k+1}} | \mathcal{F}^{\tau_k}] = \alpha^{\tau_k-1} \alpha E \alpha^\theta (S - (D_1 + \cdots + D_{1+\theta}))^+. \)

类似地，对于 \(k \ge 1$

\(\alpha^{\tau_{k+1}-2} L S_{\tau_{k+1}-1} = \alpha^{\tau_k-1} \alpha^{\tau_{k+1}-\tau_k-1} (S - (D_{\tau_k} + \cdots + D_{\tau_k+\tau_{k+1}-\tau_k-1}))^-.\)

因此

(9.2.43) \( E[\alpha^{\tau_{k+1}-2} L S_{\tau_{k+1}-1} | \mathcal{F}^{\tau_k}] = \alpha^{\tau_k-1} E \alpha^\theta (S - (D_1 + \cdots + D_{1+\theta}))^-. \)

我们可以断言

\( I = (h-c)x + K + cS + p \sum_{k=1}^\infty E \alpha^{\tau_k-1} E \alpha^\theta (S - (D_1 + \cdots + D_{1+\theta}))^-; \ II = \sum_{k=1}^\infty E \alpha^{\tau_k-1} E \alpha^\theta [\alpha(K+cS) + \alpha(h-c)(S - (D_1 + \cdots + D_{1+\theta}))^+]; \ III = h \alpha \sum_{k=1}^\infty E \alpha^{\tau_k-1} E \left[ S \frac{1-\alpha^\theta}{1-\alpha} - \sum_{l=0}^\theta D_{1+l} \frac{\alpha^l - \alpha^\theta}{1-\alpha} \right]. \)

接下来使用 \(\alpha^{\tau_{k+1}-1} = \alpha^{\tau_k-1} \alpha^{\tau_{k+1}-\tau_k-1} \alpha$，我们得到

\( E \alpha^{\tau_{k+1}-1} = E \alpha^{\tau_k-1} E \alpha \alpha^\theta, \)

并且由于 \(E \alpha^{\tau_1-1} = 1$，我们得到

(9.2.44) \( E \alpha^{\tau_k-1} = (E \alpha \alpha^\theta)^{k-1}, k \ge 1. \)

汇总结果，我们可以断言

(9.2.45) \( J_x(V_{s, S}) = (h-c)x + K + cS + \frac{1}{1-E \alpha \alpha^\theta} E \alpha^\theta [\alpha(K+cS) + \alpha(h-c)(S - (D_1 + \cdots + D_{1+\theta}))^+] + \frac{1}{1-E \alpha \alpha^\theta} E \left[ \alpha^\theta p (S - (D_1 + \cdots + D_{1+\theta}))^- + h \alpha \left( S \frac{1-\alpha^\theta}{1-\alpha} - \sum_{l=0}^\theta D_{1+l} \frac{\alpha^l - \alpha^\theta}{1-\alpha} \right) \right]. \)





## 引理 9.6. 我们有

(9.2.46)

$$E\alpha^\theta = 1 - (1-\alpha)\Gamma(S - s)$$

(9.2.47)

$$E\alpha^\theta \Phi(D_1 + \dots + D_{1+\theta}) = \dots$$

### 证明：

我们可以写

$$E\alpha^\theta = \sum_{n=0}^\infty \alpha^n E \mathbb{I}_{\theta=n}$$ 
$$= E \mathbb{I}_{D_1 \ge S-s} + \sum_{n=1}^\infty \alpha^n E \mathbb{I}_{D_1+\dots+D_{1+n} \ge S-s} \mathbb{I}_{D_1+\dots+D_n < S-s}$$ 
$$= 1 - F(S-s) + \sum_{n=1}^\infty \alpha^n (F^{(n)}(S-s) - F^{(n+1)}(S-s))$$ 
$$= \sum_{n=0}^\infty \alpha^n (F^{(n)}(S-s) - F^{(n+1)}(S-s))$$ 
$$= \frac{1}{\alpha} - \left(\frac{1}{\alpha} - 1\right) \sum_{n=0}^\infty \alpha^n F^{(n)}(S-s),$$

因此性质 (9.2.46) 得证。接下来，我们写

$$E\alpha^\theta \Phi(D_1 + \dots + D_{1+\theta})$$

$$= \sum_{n=0}^\infty \alpha^n E \mathbb{I}_{\theta=n} \Phi(D_1 + \dots + D_n) E \Phi(D_1) \mathbb{I}_{D_1 \ge S-s}$$ 
$$+ \sum_{n=1}^\infty \alpha^n E \Phi(D_1 + \dots + D_n) \mathbb{I}_{D_1+\dots+D_{1+n} \ge S-s} \mathbb{I}_{D_1+\dots+D_n < S-s}$$ 
$$= E \Phi(D_1) \mathbb{I}_{D_1 \ge S-s}$$ 
$$+ \sum_{n=1}^\infty \alpha^n E \Phi(D_1 + \dots + D_n) (\mathbb{I}_{D_1+\dots+D_n < S-s} - \mathbb{I}_{D_1+\dots+D_{1+n} < S-s})$$ 
$$= E \Phi(D) \mathbb{I}_{D \ge S-s}$$ 
$$+ \sum_{n=1}^\infty \alpha^n \int_0^{S-s} f^{(n)}(x) E \Phi(x+D) dx - \sum_{n=1}^\infty \alpha^n \int_0^{S-s} f^{(n+1)}(x) \Phi(x) dx$$ 
$$= E \Phi(D) \mathbb{I}_{D \ge S-s}$$ 
$$+ \int_0^{S-s} \Gamma(x) E \Phi(x+D) dx - \frac{1}{\alpha} \int_0^{S-s} (\Gamma(x) - \alpha f(x)) \Phi(x) dx$$ 
$$= E \Phi(D) - \frac{1}{\alpha} \int_0^{S-s} \Gamma'(x) (\Phi(x) - \alpha E \Phi(x+D)) dx,$$

通过分部积分，我们得到 (9.2.47)。

我们现在需要计算

$$
\begin{aligned}
E \sum_{l=0}^\theta \alpha^l D_{1+l} &= E \sum_{l=0}^\infty \alpha^l D_{1+l} \mathbb{I}_{\theta \ge l} \\
&= \bar{D} + E \sum_{l=1}^\infty \alpha^l D_{1+l} \mathbb{I}_{\theta \ge l} \\
&= \bar{D} + E \sum_{l=1}^\infty \alpha^l D_{1+l} \mathbb{I}_{D_1 + \dots + D_{1+l} < S-s} \\
&= \bar{D} + \bar{D} \sum_{l=1}^\infty \alpha^l F^{(l)}(S-s).
\end{aligned}
$$

因此

(9.2.48) \quad E \sum_{l=0}^\theta \alpha^l D_{1+l} = \bar{D}\Gamma(S-s).

我们现在可以汇总结果来计算

$$
\begin{aligned}
(9.2.49) \quad J_\pi(V_s, s) &= (h-\alpha)x + K + cS \\
&+ \frac{1}{(1-\alpha)\Gamma(S-s)} E\alpha^\theta \Phi(D_1 + \dots + D_{1+\theta}) \\
&+ \frac{1}{(1-\alpha)\Gamma(S-s)} \left[ (K - \frac{\alpha}{\alpha}(p+(h-c)\alpha))(1-(1-\alpha)\Gamma(S-s)) \right. \\
&\left. + \frac{h\alpha(\Gamma(S-s)(S(1-\alpha)-\bar{D}))}{1-\alpha} \right].
\end{aligned}
$$

其中

$$
\Phi(x) = (p + \alpha(h-c))(S-x)^+ + \left(p + \frac{h\alpha}{1-\alpha}\right)x.
$$

我们有

$$
\Phi'(x) = p + \frac{h\alpha}{1-\alpha} - (p + \alpha(h-c))\mathbb{I}_{S>x},
$$

因此

$$
\begin{aligned}
\Phi(S-s) - \alpha E\Phi(S-s+D) &= (p + \alpha(h-c))(s - \alpha E(s-D)^+) \\
&+ ((1-\alpha)p + \alpha h)(S-s) - \alpha \bar{D} \left(p + \frac{h\alpha}{1-\alpha}\right),
\end{aligned}
$$

$$
\Phi'(x) - \alpha E\Phi'(x+D) = (1-\alpha)p + h\alpha - (p + \alpha(h-c))(1-\alpha F(S-x))\mathbb{I}_{S>x}.
$$

我们可以应用公式 (9.2.47) 来获得，经过重排后

$$
\begin{aligned}
E\alpha^\theta \Phi(D_1 + \dots + D_{1+\theta}) &= \frac{1}{\alpha} S(p + \alpha(h-c)) \\
&- \frac{1}{\alpha} \Gamma(S-s) \left[ S((1-\alpha)p + h\alpha) + s\alpha(p-c) \right. \\
&\left. - \alpha(p + \alpha(h-c))E(s-D)^+ - \alpha \bar{D} \left(p + \frac{h\alpha}{1-\alpha}\right) \right] \\
&+ \int_0^{S-s} \Gamma(x) [c - p + (p + \alpha(h-c))F(S-x)] dx.
\end{aligned}
$$

在 (9.2.49) 中使用此公式，我们推导出

$$
\begin{aligned}
J(V_s, s) &= (h - c)x + cS + \frac{K}{(1 - \alpha)\Gamma(S - s)} \\
&- \frac{1}{1 - \alpha} [cS(1 - \alpha) + s(p - c) - (p + \alpha(h - c))E(s - D)^+ - p\bar{D}] \\
&+ \frac{1}{(1 - \alpha)\Gamma(S - s)} \int_0^{S - s} \Gamma(x)[c - p + (p + \alpha(h - c))F(s - x)]dx
\end{aligned}
$$

方程 (9.2.35) 很容易得出。

我们现在考虑情况

### II- \( x > s \) :

现在 \( \tau_1 \ge 2 \)。我们有定义

$$
\tau_1 = 2 + \inf\{n \ge 0 | D_1 + \cdots + D_{1+n} \ge x - s\}.
$$

而且

$$
y_{\tau_1} = (x - (D_1 + \cdots + D_{\tau_1 - 1}))^+ \quad LS_{\tau_1 - 1} = (x - (D_1 + \cdots + D_{\tau_1 - 1}))^-,
$$

并且 \( v_{\tau_1} = S - y_{\tau_1} \)。而且如果 \( \tau_1 \ge 3 \)，我们有

$$
\begin{aligned}
y_2 &= x - D_1; \\
&\dots \\
y_{\tau_1 - 1} &= x - (D_1 + \cdots + D_{\tau_1 - 2}).
\end{aligned}
$$

根据构造 \( D_1 + \cdots + D_{\tau_1 - 1} \ge x - s \)。因此 \( y_{\tau_1} \le s \)，且 \( \tau_1 \) 是第一个订货点。它是一个有限停止时间。从 \( \tau_1 \) 开始，序列 \( \tau_k, k \ge 2 \) 如在 (9.2.37) 中定义。量 \( y_{\tau_k}, LS_{\tau_k - 1}, v_{\tau_k} \) 如在第一部分中定义，当然 \( \tau_1 \neq 1 \) 并给出新定义。我们可以写

(9.2.50) \( J_x(V_s, s) = J_x^1(V_s, s) + J_x^2(V_s, s),\)

其中

(9.2.51) \( J_x^1(V_s, s) = hx + hE(\alpha y_2 + \cdots + \alpha^{\tau_1 - 2}) \\
+ E\alpha^{\tau_1 - 1}(K + cS + (h - c)y_{\tau_1}) + pE\alpha^{\tau_1 - 2}LS_{\tau_1 - 1},\)

(9.2.52) \( J_x^2(V_s, s) = p \sum_{k=2}^\infty E\alpha^{\tau_k - 2}LS_{\tau_k - 1} + \sum_{k=2}^\infty E\alpha^{\tau_k - 1}(K + cS + (h - c)y_{\tau_k}) \\
+ h \sum_{k=1}^\infty E\alpha^{\tau_k - 1}(\alpha y_{\tau_k + 1} + \cdots + y_{\tau_k + \tau_{k+1} - \tau_k - 1} \alpha^{\tau_{k+1} - \tau_k - 1}).\)

我们从 \( J_x^2(V_s, s) \) 开始，它与第一部分的计算密切相关。我们有

$$
J_x^2(V_s, s) = [\Gamma(S - s)(g(s) - (K + cS)(1 - \alpha)) + K + H_s(S)] \sum_{k=1}^\infty E\alpha^{\tau_k - 1},
$$

和

$$
\sum_{k=1}^\infty E\alpha^{\tau_k - 1} = \frac{E\alpha^{\tau_1 - 1}}{(1 - \alpha)\Gamma(S - s)}.
$$

因此

(9.2.53) $$J_x^2(V_s, s) = E\alpha^{\tau_1-1} \left[ \frac{g(s)}{1-\alpha} - (K+cS) + \frac{K+H_s(S)}{(1-\alpha)\Gamma(S-s)} \right].$$

现在 \( \tau_1 - 2 \) 和 \( \theta \) 具有相同的分布，其中 \( S \) 被 \( x \) 替换。因此我们可以写出公式

(9.2.54) $$E\alpha^{\tau_1-2} = \frac{1-(1-\alpha)\Gamma(x-s)}{\alpha};$$

(9.2.55) $$E\alpha^{\tau_1-2}\Phi(D_1 + \dots + D_{1+\tau_1-2}) = -\frac{1}{\alpha}\Gamma(x-s)(\Phi(x-s) - \alpha E\Phi(x-s+D)) + \frac{\Phi(0)}{\alpha} + \frac{1}{\alpha} \int_0^{x-s} \Gamma(x) \Phi(x - \alpha E \Phi(x+D)) dx.$$

然后可以计算 \( J_x^2(V_s, s) \)，与第一部分的计算类似，并得到公式 (9.2.36)。这结束了定理 9.7 的证明。

从公式 (9.2.35) 和 (9.2.36) 可以清楚地看出，可以独立于 \( x \) 优化 \( S \)。只需最小化函数

(9.2.56) $$Z_s(x) = \frac{K+H_s(x)}{\Gamma(x-s)},$$

对于 \( x \ge s \)。很容易检查存在最小值，并且我们总可以取最小的最小值。确实，有 \( Z_s(s) = K \) 且 \( Z_s(x) \to +\infty \) 当 \( x \to +\infty \)，因为 \( \Gamma(x-s) \to \frac{1}{1-\alpha} \) 当 \( x \to +\infty \)。因此，实际上只剩下一个选择，即 \( s \) 的值。我们可以通过公式定义函数 \( u_s(x) \)

(9.2.57) $$u_s(x) = (h-c)x + H_s(x) + \frac{g(s)}{1-\alpha} + \frac{(1-(1-\alpha)\Gamma(x-s))}{1-\alpha} \inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)}, \quad \forall x > s$$

(9.2.58) $$u_s(x) = (h-c)x + \frac{g(s)}{1-\alpha} + \frac{1}{1-\alpha} \inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)}, \quad \forall x \le s$$

在 \( x=s \) 处存在不连续性，除非

(9.2.59) $$\inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)} = 0,$$

这等价于条件 \( K + \inf_{\xi \ge s} H_s(\xi) = 0 \)。我们恢复了由冲动控制的解析理论（定理 9.4）得到的 \( s, S \) 对。因此，\( s \) 的选择由成本函数的连续性条件决定，而不是由优化决定（与 \( S \) 的选择不同）。然而，我们在定理 9.4 中已经表明，由这个 \( s, S \) 控制策略定义的函数是值函数，并且是 Bellman 方程的解。





## 9.2.5. 不变量度.

库存由 (s, S) 策略控制，保持在区间 X = [0, S] 内。若初始状态 \(y_1 = x \in X\)。由于该状态空间为紧集，该过程是 ergodic 的。情况与第 3 章第 3.6.1 节非常相似。该节中发展的示例实际上是 s = 0 的情况。受控马尔可夫链由转移概率定义

(9.2.60) 
\[
\pi_{s,S}(x, dy) = \left\{ \begin{array}{ll} F(x)\delta(dy) + f(x-\eta)1_{\eta < x} d\eta, & \text{if } x > s \\ \bar{F}(S)\delta(dy) + f(S-\eta)1_{\eta < S} d\eta, & \text{if } x \le s \end{array} \right.
\]

为简化记法，我们将不再显式提及下标 s, S。与马尔可夫链相关的算子 \(\Phi = \Phi_{s,S}\) 为（见第 3 章）

(9.2.61) 
\[
\Phi \varphi(x) = 1_{x > s} \left[ \varphi(0)F(x) + \int_0^x \varphi(\eta)f(x-\eta)d\eta \right] + 1_{x \le s} \left[ \varphi(0)\bar{F}(S) + \int_0^S \varphi(\eta)f(S-\eta)d\eta \right].
\]

即使 \(\varphi\) 是连续的，像 \(\Phi \varphi(.)\) 在 s 处也是不连续的。例如，假设 \(\bar{F}(S) > 0\)，足以蕴含 ergodicity，见第 3 章。X 上的不变量度 m(dx) 必须满足方程

(9.2.62) 
\[
\int_0^S \varphi(\eta)m(d\eta) = \int_0^S \int_0^S m(dx)\pi(x; d\eta)\varphi(\eta), \forall \varphi(.) \text{ bounded}.
\]

根据 ergodic 理论，我们知道 (9.2.62) 存在且仅存在一个量度解。我们假设形式为

(9.2.63) 
\[
m(dx) = A\delta(x) + B(x)dx,
\]

其中 \(\delta(x)\) 是 0 处的 Dirac 量度。由于 m(dx) 是概率量度，必须满足关系式

(9.2.64) 
\[
A + \int_0^S B(x)dx = 1.
\]

我们引入积分方程

(9.2.65) 
\[
z(\eta) = \frac{f(S-\eta)}{f(0)} + \int_s^S 1_{x > \eta} f(x-\eta)z(x)dx,
\]

并在 (0, S) 上的可测有界函数空间 B(0, S) 中寻找解。我们有

### 定理 9.8. 我们假设 \(\bar{F}(S) > 0\)。则方程 (9.2.65) 在 B(0, S) 中有唯一解。接下来定义

(9.2.66) 
\[
B(S) = \frac{F(S)}{\int_0^S F(x)z(x)dx + \int_0^s F(x)z(x)dx + \int_s^S F(S)z(x)dx},
\]

以及 \(B(x) = B(S)z(x), x \in (0, S)\)。则由 (9.2.63) 定义的量度 m(dx) 是唯一的不变量度。

证明。映射

\(z(.) \Longrightarrow T(z)(.),\)

由以下定义

\(T(z)(\eta) = \frac{f(S-\eta)}{f(0)} + \int_s^S 1_{x > \eta} f(x-\eta)z(x)dx,\)

满足

\[
||T(z_1) - T(z_2)|| \le F(S)||z_1 - z_2||,
\]

根据假设，它是一个收缩映射。因此它存在不动点。容易验证函数 B(x) 满足

\[
(9.2.67) \quad B(\eta) + \int_s^S B(x)[f(S-\eta) - f(x-\eta) \mathbb{1}_{x>\eta}] dx = f(S-\eta),
\]

我们还有

\[
(9.2.68) \quad A = F(S) + \int_s^S B(x)(F(S) - F(x)) dx.
\]

经过变形，我们还有

\[
A = \frac{\int_s^S \bar{F}(x)B(x)dx + \bar{F}(S)\int_0^s B(x)dx}{F(S)}; \quad B(\eta) = f(S-\eta) \left( A + \int_0^s B(x)dx \right) + \int_s^S f(x-\eta)B(x)\mathbb{1}_{x>\eta} dx,
\]

对于任意量度 \(\varphi()\)，我们可以验证关系式 (9.2.62)。因此 m(dx) 是一个不变量度。根据 ergodicity 性质，它是唯一的。

现在考虑目标函数 (9.2.7)，当我们应用由 (s, S) 策略定义的控制 V = V_{s,S} 时。库存 y_n 变得 ergodic，因此我们有

\[
(1 - \alpha) \int_0^S J_x(V_s, m)_{s,S}(dx) = \int_0^s [hx + (K + c(S-x)) \mathbb{1}_{x \le s} + p(E(x-D)^- \mathbb{1}_{x \le s} + E(x-D)^+ \mathbb{1}_{x > s})] m_s(dx).
\]

根据不变量度的性质 (9.2.62)，该表达式也等于

\[
(9.2.69) \quad (1 - \alpha) \int_0^S J_x(V_s, m)_{s,S}(dx) = pd + h \int_0^S x m_s(dx) + \int_0^S (K + (c-p)(S-x)) m_s(dx).
\]

在以下内容中，我们省略下标 s,S 以简化记法。使用函数 g(x) 的定义，见 (9.2.13)，我们还有

\[
(1 - \alpha) \int_0^S J_x(V)m(dx) = (h-c)(1 - \alpha) \int_0^S xm(dx) + K \int_0^S m(dx) + \int_0^S (g(x)\mathbb{1}_{x>s} + g(s)\mathbb{1}_{x \le s}) m(dx).
\]

现在使用函数 H(x)，它满足

\[
H(x) = (g(x) - g(s)) \mathbb{1}_{x>s} + \alpha E H((x-D)^+),
\]

我们还得到

\[
(9.2.70) \quad \int_0^S J_x(V)m(dx) = \int_0^S ((h-c)x + H(x))m(dx) + \frac{g(s)}{1-\alpha} + \frac{K+H(S)}{1-\alpha} \int_0^S m(dx).
\]

### 练习 9.4. 直接由给出 \(J_\pi(V)\) 的公式，即公式 (9.2.35)、(9.2.36)，推导公式 (9.2.70)。需要证明函数 \(\Gamma(x)\) 满足关系式

\[
(9.2.71) \quad \Gamma(S-s)\int_0^s m(dx) + (1-\alpha)\int_s^S \Gamma(x-s)m(dx) = 1.
\]

确实，从 \(\Gamma\) 的方程出发，可以得出

\[
(\Gamma(x-s)-1)\mathbf{1}_{x>s} = \alpha \mathbf{1}_{x>s} E\Gamma(x-s-D)\mathbf{1}_{x-s-D>0},
\]

以及

\[
\Gamma(S-s)-1 = \alpha E\Gamma(S-s-D)\mathbf{1}_{S-s-D>0}.
\]

因此

\[
(\Gamma(x-s)-1)\mathbf{1}_{x>s} + \mathbf{1}_{x \le s}(\Gamma(S-s)-1) = \alpha[\mathbf{1}_{x>s}E\Gamma(x-s-D)\mathbf{1}_{x-s-D>0} + \mathbf{1}_{x \le s}E\Gamma(S-s-D)\mathbf{1}_{S-s-D>0}].
\]

对两边关于不变量度进行积分，得到

\[
\int_s^S \Gamma(x-s)m(dx) + \Gamma(S-s)\int_0^s m(dx) = 1 = \alpha \int_s^S \Gamma(x-s)m(dx),
\]

其中我们使用了不变量度的基本性质 (9.2.62)，作用于测试函数 \(\varphi(x) = \Gamma(x-s)\mathbf{1}_{x>s}\)。这就是结果 (9.2.71)。

## 9.2.6. 特例.

考虑 \(f(x) = \beta \exp -\beta x\) 的情况。我们可以得到解析公式。首先有

\[
(9.2.72) \quad \Gamma(x) = \frac{1}{1-\alpha} - \frac{\alpha}{1-\alpha} \exp -\beta(1-\alpha)x,
\]

then

\[
(9.2.73) \quad \mu(x) = c(1-\alpha) + \alpha h - (p - \alpha(c-h)) \exp -\beta x;
\]

\[
(9.2.74) \quad g(x) = p\bar{D} - \frac{p-\alpha(c-h)}{\beta} + (c(1-\alpha) + \alpha h)x + \frac{p-\alpha(c-h)}{\beta} \exp -\beta x.
\]

使 \(\mu(s) = 0\) 的值 \(\bar{s}\) 由以下给出

\[
(9.2.75) \quad \exp -\beta \bar{s} = \frac{c(1-\alpha) + \alpha h}{p - \alpha(c-h)}.
\]

接下来，对于 \(x \ge s\)，我们有

\[
(9.2.76) \quad H(x) = \frac{c(1-\alpha) + \alpha h}{1-\alpha}(x-s) - \frac{1-\exp -\beta(1-\alpha)(x-s)}{\beta(1-\alpha)} \cdot \left[ \frac{\alpha}{1-\alpha}(c(1-\alpha) + \alpha h) + (p - \alpha(c-h)) \exp -\beta s \right].
\]

对于 \(s \le \bar{s}\)，数 \(S\) 由方程 \(H'(S) = 0\) 唯一确定，即

\[
(9.2.77) \quad \exp -\beta(1-\alpha)(S-s) = \frac{c(1-\alpha) + \alpha h}{\alpha(c(1-\alpha) + \alpha h) + (1-\alpha)(p - \alpha(c-h)) \exp -\beta s}.
\]

我们推导出

\[
(9.2.78) \quad H(S) = \frac{c(1-\alpha)+\alpha h}{1-\alpha}(S-s) - \frac{(p-\alpha(c-h))\exp -\beta s - (c(1-\alpha)+\alpha h)}{\beta(1-\alpha)},
\]

且 \(s\) 由方程 \(H_s(S(s)) = -K\) 定义，假设 \(H_0(S(0)) < -K\)。数 \(S_0 = S(0)\) 由以下定义

\[
(9.2.79) \quad \exp -\beta(1-\alpha)S_0 = \frac{c(1-\alpha)+\alpha h}{p(1-\alpha)+\alpha h},
\]

且条件等价于

\[
(9.2.80) \quad \frac{c(1-\alpha)+\alpha h}{1-\alpha}S_0 - \frac{p-c}{\beta(1-\alpha)} < -K.
\]

现在转向不变量度。方程 (9.2.65) 的解为

\[
(9.2.81) \quad z(\eta) = \left\{ \begin{array}{ll} 1, & \text{if } \eta > s \\ \exp -\beta(s-\eta), & \text{if } \eta \le s \end{array} \right.
\]

Then \(B(S) = \frac{\beta}{1+\beta(S-s)}\) 因此

\[
(9.2.82) \quad B(\eta) = \left\{ \begin{array}{ll} \frac{\beta}{1+\beta(S-s)}, & \text{if } \eta > s \\ \frac{\beta \exp -\beta(S-\eta)}{1+\beta(S-s)}, & \text{if } \eta \le s \end{array} \right. \qquad A = \frac{\exp -\beta s}{1+\beta(S-s)}.
\]

## 9.3. 带固定成本和积压的库存控制

### 9.3.1. 贝尔曼方程。我们考虑第 5.2 节的情况，其中添加了固定成本。贝尔曼函数方程由以下给出

\[
(9.3.1) \quad u(x) = \inf_{v \ge 0} [l(x,v) + \alpha E u(x+v-D)],
\]

with

\[
(9.3.2) \quad l(x,v) = K \mathbb{I}_{v>0} + cv + hx^+ + px^-.
\]

我们也将 (9.3.1) 写为

\[
(9.3.3) \quad u(x) = hx^+ + px^- + \inf_{v \ge 0} [K \mathbb{I}_{v>0} + cv + \alpha E u(x+v-D)].
\]

我们定义天花板函数由线性方程

\[
(9.3.4) \quad w_0(x) = hx^+ + px^- + \alpha E w_0(x-D).
\]

Recalling

\[
(9.3.5) \quad \Phi^\varphi(x) = E \varphi(x+v-D),
\]

then

\[
(9.3.6) \quad w_0(x) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^0)^{n-1} (hx^+ + px^-)(x),
\]

and the series is well defined with

\[
(9.3.7) \quad w_0(x) \le \max(h,p) \left[ \frac{|x|}{1-\alpha} + \frac{D}{(1-\alpha)^2} \right].
\]





假设 (4.3.1)、(4.3.2)、(4.3.6) 已满足。因此，定理 4.3、4.4、4.5 的结果适用。我们可以得出

## 定理 9.9.
在假设 (9.3.1)、(9.3.5) 下，函数方程 (9.3.3) 在区间 \(0 \le u \le w_0\) 上的解集非空，并具有最小解和最大解 \(\underline{y}\) 与 \(\bar{y}\)。最小解是下半连续的（l.s.c.）。它与值函数重合。存在一个最优控制策略，可通过反馈 \(\hat{v}(x)\) 得到。

我们可以像无固定成本的情况一样，检查最优反馈的一个估计。

## 提议 9.4.
最优反馈满足

(9.3.8)
\[
\hat{v}(x) \le x^- + \frac{\alpha \bar{D}}{c(1-\alpha)^2}[h + (p+c)(1-\alpha)] + \frac{\alpha K}{1-\alpha}.
\]

证明。我们首先从下方对值函数进行估计。这与无固定成本的情况相同，证明也相同，

\[
u(x) \ge \frac{hx^+}{1-\alpha} + px^- - \frac{ha\bar{D}}{(1-\alpha)^2}.
\]

下一步是通过一个合适的函数来最大化 \(u(x)\)。我们不使用 \(w_0(x)\)，而是使用 \(w(x)\)，它是以下方程的解：

\[
w(x) = K 1_{x<0} + (c+p)x^- + hx^+ + \alpha E w(x^+ - D).
\]

我们有 \(u(x) \le w(x)\)。以下估计成立

\[
w(x) \le (c+p)x^- + \frac{hx^+}{1-\alpha} + \frac{K+\alpha(c+p)\bar{D}}{1-\alpha}.
\]

现在，回到函数方程 (9.3.3)，我们利用

\[
u(x) \ge \frac{hx^+}{1-\alpha} - \frac{ha\bar{D}}{(1-\alpha)^2}.
\]

来最小化右边括号内的量。

我们看到它具有以下下界：

\[
K + cv + \frac{hx^+}{1-\alpha} + px^- - \frac{ha\bar{D}}{(1-\alpha)^2}.
\]

因此，在求下确界时，我们可以将控制 \(v\) 限制在集合

\[
K + cv + \frac{hx^+}{1-\alpha} + px^- - \frac{ha\bar{D}}{(1-\alpha)^2} \le w(x).
\]

中。

然后利用对 \(w(x)\) 的估计，我们推断可以将 \(v\) 的集合限制在由 (9.3.8) 右边界定的范围内。最优反馈必须满足此界，因此得到结果 (9.3.8)。

然后我们可以证明 (9.3.3) 在空间 \(B_1\) 中的解的唯一性，其中

\[
u \in B_1 \Longleftrightarrow \frac{|u(x)|}{1+|x|} \le C.
\]

## 定理 9.10.
在假设 (9.3.1)、(9.3.5) 下，(9.3.3) 在空间 \(B_1\) 中的解是唯一的。函数 \(u\) 是下半连续的（l.s.c.）。

证明。像往常一样，我们将检查最小解和最大解是否重合。定义与最优反馈相关的最优控制。如果我们将最优控制记为 \(\bar{V} = (\bar{v}_1, \cdots, \bar{v}_n, \cdots)\)，最优轨迹记为 \(\{\bar{y}_1, \cdots, \bar{y}_n, \cdots\}\)，我们必须证明 \(\bar{V}\) 属于 \(\mathcal{V}\)，这意味着

\[
\alpha^{j-1} E[\bar{y}_j] \to 0,
\]

当 \(j \to \infty\) 时。然而，根据估计 (9.3.8) 并令

\[
C = \frac{\alpha D}{c(1-\alpha)^2} [h + (p+c)(1-\alpha)] + \frac{\alpha K}{1-\alpha},
\]

我们可以得出

\[
\bar{y}_{n+1} \le \bar{y}_n^+ + C,
\]

因此

\[
\bar{y}_{n+1} \le x^+ + nC.
\]

另一方面

\[
\hat{y}_{n+1} \ge x - D_1 - \cdots - D_n.
\]

因此

\[
x - nD \le E\hat{y}_{n+1} \le x^+ + nC,
\]

条件满足，从而得到结果。

### 9.3.2. s, S 策略.
我们的目标现在是得到最优反馈。我们希望表明它源自一个 s, S 策略。

首先我们引入算子

(9.3.9)
\[
T(u)(x) = hx^+ + px^- + \alpha Eu(x - D),
\]

和

(9.3.10)
\[
M(u)(x) = \inf_{\eta \ge x^+} [K \mathbf{1}_{\eta > x} + (c-h)(\eta^+ - x^+) + (p+c)(\eta^- - x^+) + u(\eta)].
\]

这个算子比无短缺情况下引入的算子（见 9.2.10）稍微复杂一些。如果假设 \(c > h\) 成立，从库存 x 到库存 \(\eta \ge x\) 的变动成本是正的，但它不是差值 \(\eta - x\) 的函数，因为库存为正或负时含义不同。

函数方程 (9.3.3) 可以写成

\[
u(x) = \min[T(u)(x), M(T(u))(x)],
\]

并且如同在 (9.2.11) 中所见，这等价于

\[
u(x) = \min[T(u)(x), M(u)(x)].
\]

接下来定义

(9.3.11)
\[
g(x) = cx(1-\alpha) + \alpha cD + \alpha hE(x-D)^+ + \alpha pE(x-D)^-,
\]

和

(9.3.12)
\[
g_s(x) = (g(x) - g(s))\mathbf{1}_{x > s}.
\]

然后我们通过求解以下方程来定义函数 \(H_s(x)\)：

(9.3.13)
\[
H_s(x) = g_s(x) + \alpha E H_s(x - D).
\]

我们知道解由以下给出

(9.3.14)
\[
H_s(x) = g_s(x) + \alpha g_s * f + \sum_{n=2}^{\infty} \alpha^n g_s * f^{(n)}(x),
\]

并使用

\[
F^{(n)}(x) = \int_0^x f^{(n)}(\xi) d\xi,
\]

和

\[
\Gamma(x) = \sum_{n=0}^{\infty} \alpha^n F^{(n)}(x),
\]

然后我们可以轻松验证公式

(9.3.15)
\[
H_s(x) = \int_s^x \Gamma(x - \xi) \mu(\xi) d\xi,
\]

其中 \(\mu = g'\)。函数 \(\Gamma(x)\) 是更新方程 (9.2.19) 的解。

## 引理 9.7.
假设

(9.3.16)
\[
h < c < p \frac{\alpha}{1-\alpha},
\]

则函数 \(H_s(x)\) 在 \(x \ge s\) 处取得其最小值。取最小的最小值，定义一个函数 \(S(s)\)。如果 \(\bar{s}\) 是满足 \(\mu(s) = 0, \bar{s} > 0\) 的唯一值，则 \(S(s) = \bar{s}, \forall s \ge \bar{s}\)。方程

(9.3.17)
\[
H_s(S(s)) = \inf_{\eta \ge s} H_s(\eta) = -K,
\]

有一个唯一解 \(s < \bar{s}\)。

证明。这与引理 9.4 的证明类似。我们有

(9.3.18)
\[
g'(x) = \mu(x) = c(1 - \alpha) + \alpha h - \alpha(h + p)\bar{F}(x).
\]

得益于条件 (9.3.16)，我们可以定义 \(\bar{s} > 0\)，使得 \(\mu(\bar{s}) = 0\) 且 \(\mu(x) < 0, \forall x < \bar{s}\) 以及 \(\mu(x) > 0, \forall x > \bar{s}\)。由于 \(\Gamma\) 是递增函数，函数 \(H_s(x)\) 在 \(x\) 上是递增的，只要 \(s \ge \bar{s}\)。因此我们可以断言

\[
S(s) = s, \quad \inf_{\eta \ge s} H_s(\eta) = 0, \quad \text{如果 } s \ge \bar{s}.
\]

因此我们将可能的 \(s\) 集合限制为满足 \(s < \bar{s}\)。显然，对于 \(s < \bar{s} < x\)

\[
H_s(x) = H_s(\bar{s}) + \int_{\bar{s}}^x \Gamma(x - \xi) \mu(\xi) d\xi.
\]

我们又有

\[
H_s(x) \ge \frac{1}{1-\alpha} (g(\bar{s}) - g(s)) + g(x) - g(s).
\]

因此当 \(x \uparrow \infty\) 时 \(H_s(x) \rightarrow \infty\)。由于 \(H'_s(s+) = \mu(s) < 0\)，函数 \(H_s(x)\) 在 \((s, \infty)\) 上取得一个负最小值。如果有多个，我们称 \(S(s)\) 为最小的最小值。我们有

\[
H'_s(S(s)) = 0.
\]

接下来我们有

\[
\frac{d}{ds} H_s(S(s)) = \frac{\partial}{\partial s} H_s(x)|_{S(s)} = -\Gamma(S(s) - s)\mu(s) > 0.
\]

另外

\[
H_s(S(s)) \le H_s(\bar{s}) = \int_s^{\bar{s}} \Gamma(\bar{s} - \xi)\mu(\xi)d\xi \le \frac{1}{\alpha} \int_s^{\bar{s}} \mu(\xi)d\xi = \frac{1}{\alpha}(g(\bar{s}) - g(s)).
\]

由于当 \( s \to -\infty \) 时 \( g(s) \to +\infty \)，我们有当 \( s \to -\infty \) 时 \( H_s(S(s)) \to +\infty \)。因此，当 \( s \) 从 \( -\infty \) 增加到 \(\bar{s}\) 时，函数 \(\inf_{\eta \ge s} H_s(\eta)\) 从 \(-\infty\) 增加到 0。因此存在一个唯一的 \( s \)，使其等于 \(-K\)。我们可以通过求解代数方程组来找到 \(s, S\) 对

(9.3.19)
\[
\begin{aligned}
\Gamma(S - s)\mu(s) + \int_s^S \Gamma(S - \xi)\mu'(\xi)d\xi &= 0; \\
\int_s^S \Gamma(S - \xi)\mu(\xi)d\xi &= -K.
\end{aligned}
\]

我们最终可以得出

## 定理 9.11.
在假设 (9.3.2)、(9.3.5) 和 (9.3.16) 下，函数方程 (9.3.3) 在 \( B_1 \) 中有一个唯一解，它是连续的，当 \(|x|\) 趋向于 \(+\infty\) 时趋向于 \(+\infty\)。最优反馈由一个 \(s, S\) 策略定义，该策略是系统 (10.3.22) 的解。

证明。通过求解 (10.3.22) 定义了 \(s, S\)（它唯一确定 \(s\)，然后确定 \(S\)，可能取最小值），我们考虑由 (9.3.15) 给出的 \(H_s(x)\)。从现在起我们将丢弃下标 \(s\)，因此考虑 \(H(x)\)。然后我们定义

(9.3.20)
\[
u(x) = H(x) + hx^+ + px^- - cx + \frac{g(s)}{1-\alpha}.
\]

那么 \(u(x)\) 满足

(9.3.21)
\[
u(x) = \begin{cases} hx^+ + px^- - cx + \frac{g(s)}{1-\alpha}, & x \le s \\ hx^+ + px^- + \alpha E[u(x-D)], & x \ge s \end{cases}
\]

该函数是连续的，并且当 \(|x| \to +\infty\) 时趋向于 \(+\infty\)。并且，根据 \(s\) 的选择，对于 \(x \le s\)

\[
\begin{aligned}
u(x) &= K + \inf_{\eta \ge x} [\eta u(\eta) + (c-h)(\eta^+ - x^+) - (c+p)(\eta^- - x^-)] \\
&= K + \inf_{\eta \ge x} [\eta u(\eta) + (c-h)(\eta^+ - x^+) - (c+p)(\eta^- - x^-)].
\end{aligned}
\]

因此函数 \(u\) 满足

\[
u(x) = \begin{cases} M(u)(x), & \forall x \le s \\ T(u)(x), & \forall x \ge s \end{cases}
\]

因此还需要证明

\[
\begin{aligned}
u(x) \le T(u)(x), & \quad \forall x \le s \\
u(x) \le M(u)(x), & \quad \forall x \ge s
\end{aligned}
\]

用 \(H\) 表示，第一个不等式等价于 \(g'(x) \ge 0, \forall x \le s\)。这是成立的，因为 \(\mu(\xi) < 0, \forall \xi < s\)。用 \(H\) 表示，第二个不等式等价于

(9.3.22)
\[
H(x) \le K + \inf_{\eta \ge x} H(\eta), \quad \forall x \ge s.
\]




要证明 (9.3.22)，我们首先注意到对于 \(x \ge s\) 有 \(\inf_{\eta \ge x} H(\eta) \ge \inf_{\eta \ge x} H(\eta) = -K\)。因此，只要 \(H(x) \le 0\)，不等式当然成立。接着考虑称为 \(x_0\) 的最小数，使得 \(H\) 变为正数。此时有 \(H(x_0) = 0, H(x) < 0 \forall x, s < x < x_0\)。

我们可以断言 \(g_s(x_0) > 0\)。这源于关系式 \(g_s(x_0) = -\alpha EH(x_0 - D)\) 以及由 \(x_0\) 的定义得出的性质。

令 \(\xi > 0\)。我们将考虑区域 \(x \ge x_0 - \xi\)。我们可以写出不等式 \(H(x) \le g_s(x) + \alpha E(H(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\)，这源于事实 \(E(H(x - D)\mathbb{I}_{x - D \le x_0 - \xi}) \le 0\)。

接下来定义 \(M(x) = H(x + \xi) + K\)。

显然 \(M(x) \ge 0\)。得益于这种非负性，我们可以写出 \(EM(x - D) \ge E(M(x - D)\mathbb{I}_{x - D \ge x_0 - \xi})\)。

现在对于 \(x \ge x_0 - \xi\)，有 \(H(x + \xi) - \alpha EH(x + \xi - D) = g_s(x + \xi)\)，因此 \(M(x) - \alpha EM(x - D) = g_s(x + \xi) + K(1 - \alpha)\)。

因此我们有 \(M(x) \ge g_s(x + \xi) + \alpha E(M(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\)。

我们可以断言 \(g_s(x + \xi) \ge g_s(x), \forall x \ge x_0 - \xi\)。

确实，注意到 \(g_s(x + \xi) \ge g_s(x_0) \ge 0\)，因为 \(g\) 在 \([s, \infty)\) 上是递增的。因此，当 \(x < s\) 时，不等式显而易见。如果 \(x \ge s\)，则不等式等价于 \(g(x + \xi) \ge g(x)\)。根据单调性性质，当 \(x \ge s\) 时这成立。因此剩下的情况是 \(s < x < s\)。但在这种情况下，\(g_s(x) < 0\)，不等式成立。

让我们定义 \(Y(x) = H(x) - M(x)\)。根据上述不等式，我们可以断言 \(Y(x) \le \alpha E(Y(x - D)\mathbb{I}_{x - D \ge x_0 - \xi}), \forall x \ge x_0 - \xi\)，且 \(Y(x_0 - \xi) \le -K\)。

这两个性质蕴含 \(Y(x) \le 0, \forall x \ge x_0 - \xi\)。因此我们得到了 (9.3.22) 对 \(\forall x \ge x_0 - \xi\) 成立，特别是对于 \(x > x_0\) 也成立，正如所期望的。所以 \(u\) 是函数方程 (9.3.3) 的解，因此是值函数。由 \(s, S\) 策略定义的反馈是最优的。

**注。** (9.3.22) 的另一种证明 我们将给出 (9.3.22) 的另一种证明，使用源自 [3] 的一个想法。

**证明。** 我们回顾 \(H(x) = g_s(x) + \alpha EH(x - D)\)，并且我们想要证明 \(H(x) \le K + \inf_{\eta \ge x} H(\eta)\)。

定义

$$B(x) = H(x) - \inf_{\eta \ge x} H(\eta).$$

所以我们想要证明

$$B(x) \le K.$$

对于 $x \le s$ 我们有

$$B(x) = - \inf_{\eta \ge x} H(\eta) = - \inf_{\eta \ge x} H(\eta) = K.$$

考虑第一个点 $x_0$，使得 $x_0 > s$ 且 \(H(x_0) = 0\)，\(H(x) \le 0, \forall x \le x_0\)。对于 \(s \le x \le x_0\) 我们有

$$B(x) \le - \inf_{\eta \ge x} H(\eta) \le - \inf_{\eta \ge x} H(\eta) = K.$$

还剩下要考虑的情况是 \(x > x_0\)。假设存在一点 \(x' > x_0\) 使得 \(B(x') \ge K\)。那么将存在一点 \(x'\) 使得

$$\bar{s} < x_0 \le x', B(x') = 0, B(x) < K, x < x'.$$

定义点 \(x_3\) 使得

$$H(x_3) = \inf_{\eta \ge x'} H(\eta).$$

点 \(x_3\) 被唯一地定义为 \(x'\) 之后的最小下确界。而且 \(x_3 \neq x'\)，因为

$$B(x') = H(x') - H(x_3) = K.$$

接下来定义 \(x_2\) 使得

$$H(x_2) = \max_{\eta \le x_3} H(\eta) = \max_{s \le \eta \le x_3} H(\eta).$$

我们取 \(x_2\) 为最小最大值。那么我们可以断言 \(x_2 \ge x'\)。确实，如果 \(x_2 < x'\)，则

$$\inf_{\eta \ge x_2} H(\eta) \le \inf_{\eta \ge x'} H(\eta),$$

且

$$H(x_2) - \inf_{\eta \ge x_2} H(\eta) \ge H(x') - \inf_{\eta \ge x'} H(\eta) = K,$$

这将与 \(x'\) 的定义矛盾。因此 \(x' \le x_2 \le x_3\)。而且 \(x_2 \neq x_3\)，因为

$$H(x_2) - H(x_3) \ge H(x') - H(x_3) = B(x') = K.$$

让我们现在验证

(9.3.23) $$H(x) - H(y) \le H(x_2) - H(x_3), \forall x \le y \le x_3.$$

确实，如果 \(x < x'\)，则

$$H(x) - H(y) \le H(x) - \inf_{\eta \ge x} H(\eta) < K \le H(x_2) - H(x_3).$$

接下来，如果 \(x' \le x \le y \le x_3\)，则

$$H(x) - H(y) \le H(x_2) - H(x_3).$$

汇总结果我们注意到

$$s < \bar{s} < x_0 \le x' \le x_2 < x_3.$$

现在

$$H(x_2) = g(x_2) - g(s) + \alpha E H(x_2 - D);$$
$$H(x_3) = g(x_3) - g(s) + \alpha E H(x_3 - D),$$

并且我们有

$$g(x_2) - g(x_3) < 0;$$
$$H(x_2 - D) - H(x_3 - D) < H(x_2) - H(x_3),$$

由此，相减方程得出 \(H(x_2) < H(x_3)\)。这与 \(x_2\) 的定义矛盾。

我们最终得到了命题 9.3 的等价形式。

## 命题 9.5. 函数 \(S(s)\) 是递减的，因此若 \(s \le \bar{s}\) 则 \(S(s) \ge \bar{s}\)，且当 \(s \to -\infty\) 时 \(S(s) \to S^+\)，其中

(9.3.24) $$
\Gamma(S^+) = \frac{p - (c - h)(1 - \alpha)}{(1 - \alpha)(h + p)}.
$$

**证明。** 第一个性质的证明同命题 9.3。第二个性质源自定义 \(S(s)\) 的第一个方程 (10.3.22)。根据单调性，我们知道 \(S(s) \uparrow S^+\)。然后

$$\Gamma(S - s)\mu(s) \uparrow \frac{c(1 - \alpha) - \alpha p}{1 - \alpha}.$$

我们可以对第一个方程 (10.3.22) 取极限并得到

$$
\frac{c(1 - \alpha) - \alpha p}{1 - \alpha} + \alpha(h + p) \int_0^{S^*} \Gamma(S^* - \xi) f(\xi) d\xi = 0,
$$

然后使用更新方程，我们得到公式 (9.3.24)。我们可以直接验证 \(S^* \ge \bar{s}\)。确实，使用

$$
1 - \alpha + \alpha \bar{F}(S^*) \le \frac{1}{\Gamma(S^*)} = \frac{(1 - \alpha)(h + p)}{p - (c - h)(1 - \alpha)}.
$$

因此

$$
\alpha \bar{F}(S^*) \le (1 - \alpha) \frac{c(1 - \alpha) + h \alpha}{p - (c - h)(1 - \alpha)}.
$$

但是，根据假设 (9.3.16)，我们推导出

$$
\frac{1 - \alpha}{p - (c - h)(1 - \alpha)} \le \frac{1}{h + p}.
$$

根据 \(\bar{F}(s)\) 的表达式，我们得到 \(\bar{F}(S^*) \le \bar{F}(s)\)，结果随之得出。

最后我们可以检查 \(K\)-凸性性质

## 命题 9.6. 函数 \(u(x)\) 是 \(K\)-凸的。

**证明。** 这与定理 9.6 中的证明相同。可以通过归纳法证明递增序列是 \(K\)-凸的，因此该性质对极限也成立。

**注。** 如果做出技术假设 (9.2.33)，那么 \(Eu(x - D)\) 是连续的，最优反馈的 \(s, S\) 性质可以作为 \(K\)-凸性理论的结果来证明，如同定理 9.6 的证明中那样。

最后，考虑以下情况

$$
(9.3.25) \quad c > \frac{p\alpha}{1-\alpha},
$$

则函数 \(H_x(x)\) 在 \(x\) 中总是递增。因此 \(S(s) = s, \forall s\)。由此可知最优反馈是 \(\hat{v}(x) = 0\)。

## 9.3.3. 概率方法。

如同我们在无积压情况中所做的那样，我们将直接评估任意 \(s, S\) 策略对应的成本。我们有以下

## 定理 9.12. 设 \(V_{s,S}\) 为对应于 \(s, S\) 策略的控制，由反馈定义

$$
(9.3.26) \quad V_{s,S} = \left\{ \begin{array}{ll} S - x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{array} \right.
$$

对应的成本是：对于 \(x \le s\)

$$
(9.3.27) \quad J_s(V_{s,S}) = hx^+ + px^- - cx + \frac{g(s)}{1-\alpha} + \frac{K + H_1(S)}{(1-\alpha)\Gamma(S-s)}.
$$

对于 \(x > s\)，有

$$
(9.3.28) \quad J_s(V_{s,S}) = hx^+ + px^- - cx + H_s(x) + \frac{g(s)}{1-\alpha} + (1 - (1-\alpha)\Gamma(x-s)) \frac{K + H_s(S)}{(1-\alpha)\Gamma(S-s)}.
$$

该函数在 \(x = s\) 处除外是连续的。

**证明。** 这些函数与无积压情况相同，然而函数 \(g, H\) 是对应于当前情况的，参见 (9.3.11), (9.3.13)。数 \(s\) 是实数，为了简化，我们取 \(S > 0\) 且 \(\ge s\)。

设 \(V_{s,S} = (v_1, \cdots, v_n, \cdots)\) 和 \(y_1, y_2, \cdots, y_n \cdots\) 为相应的库存演化。我们有 \(y_1 = x\)。我们首先考虑以下情况

- **I-** \(x \le s \le 0\):

此时我们有 \(v_1 = S - x\)。我们令 \(\tau_1 = 1\) 并定义停止时间序列

$$
(9.3.29) \quad \tau_{k+1} = \tau_k + 1 + \inf\{n \ge 0 \mid D_{\tau_k} + \cdots + D_{\tau_k+n} \ge S - s\}.
$$

由于 \(S - s \ge S\)，我们还需要另一组停止时间序列

$$
(9.3.30) \quad \theta_{k+1} = \tau_k + 1 + \inf\{n \ge 0 \mid D_{\tau_k} + \cdots + D_{\tau_k+n} \ge S\},
$$

并且我们有 \(\tau_k \le \theta_{k+1} \le \tau_{k+1}\)。

根据引理 9.5，只需将 \(S - s\) 替换为 \(S\)，我们可以看到对于 \(k \ge 2\)，\(\theta_k\) 是相对于滤流 \(\mathcal{F}^{n-1}\) 的停止时间。而且 \(\theta_{k+1} - \tau_k - 1\) 和 \(D_{\tau_k}, \cdots, D_{\tau_k+n}, n \ge 0\) 与 \(\mathcal{F}^n\) 相互独立。控制 \(V_{s,S}\) 的订购时间是时间 \(\tau_k\)。此时库存为

$$
y_{\tau_k} = S - (D_{\tau_{k-1}} + \cdots + D_{\tau_k - 1}) \le s, \forall k \ge 2
$$

订购量为

$$
v_{\tau_k} = S - y_{\tau_k}, \forall k \ge 2
$$




让我们考虑时间 \(\tau_k+1\) 和 \(\tau_{k+1}-1\) 之间的库存，如果 \(\tau_{k+1}-2 \ge \tau_k\)。如果 \(\tau_{k+1}-1 = \tau_k\)，则有 \(y_{\tau_k+1} = y_{\tau_{k+1}}\)。否则，考虑 \(\theta_{k+1}\) 的位置很重要。如果 \(\theta_{k+1} = \tau_k + 1\)，则第一个库存 \(y_{\tau_k+1}\) 为负，且直到 \(\tau_{k+1}-1\) 的所有库存均为负。如果 \(\tau_{k+1}-1 \ge \theta_{k+1} \ge \tau_k+2\)，则有

\(\begin{aligned} y_{\tau_k+1} &= S - D_{\tau_k} > 0 \\ \dots \\ y_{\theta_{k+1}} &= S - (D_{\tau_k} + \dots + D_{\theta_{k+1}-2}) > 0 \\ y_{\theta_{k+1}} &= S - (D_{\tau_k} + \dots + D_{\theta_{k+1}-1}) \le 0 \\ y_{\tau_{k+1}-1} &= S - (D_{\tau_k} + \dots + D_{\tau_{k+1}-2}) \le 0 \end{aligned}\)

如果 \(\theta_{k+1} = \tau_{k+1}\)，则从 \(\tau_k + 1\) 到 \(\tau_{k+1} - 1\) 的库存均为正。因此我们可以写

\(\begin{aligned} J_\tau(V_s, s) &= \sum_{k=1}^\infty E \alpha^{\tau_k-1} (K + cS - (c+p))y_{\tau_k} \\ &+ \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1}(hy_n^+ + py_n^-). \end{aligned}\)

我们也可以写

(9.3.31) \(\begin{aligned} J_\tau(V_s, s) &= K + cS - (p+c)x \\ &+ \sum_{k=2}^\infty E \alpha^{\tau_k-1}(K + cS - cy_{\tau_k}) \\ &+ (h+p)E \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\theta_{k+1}-1} \alpha^{n-1}y_n \\ &- pE \sum_{k=1}^\infty \sum_{n=\tau_k+1}^{\tau_{k+1}} \alpha^{n-1}y_n, \end{aligned}\)

我们将其写为

\(J_\tau(V_s, s) = K + cS - (p+c)x + Z_1.\)

让我们计算 \(Z_1\)。我们首先注意到

\(\begin{aligned} E \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\theta_{k+1}-1} \alpha^{n-1}y_n &= E \sum_{n=\tau_k+1}^\infty \alpha^{\tau_k-1} \left[ S\alpha \frac{1-\alpha^{\theta_{k+1}-\tau_k-1}}{1-\alpha} \right. \\ &\left. - \sum_{l=0}^{\theta_{k+1}-\tau_k-1} D_{\tau_k+l} \alpha^l \frac{\alpha - \alpha^{\theta_{k+1}-\tau_k-1}}{1-\alpha} \right]. \end{aligned}\)

同样地，有

\(\begin{aligned} E \sum_{k=1}^\infty \sum_{n=\tau_k+1}^{\tau_{k+1}} \alpha^{n-1}y_n &= E \sum_{k=1}^\infty \alpha^{\tau_k-1} \left[ S\alpha \frac{1-\alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} \right. \\ &\left. - \sum_{l=0}^{\tau_{k+1}-\tau_k-1} D_{\tau_k+l} \alpha^l \frac{\alpha - \alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} \right]. \end{aligned}\)

我们还写

\(\sum_{k=2}^{\infty} E \alpha^{\tau_k - 1}(K + cS - c y_{\tau_k}) = E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} \alpha^{\tau_{k+1} - \tau_k - 1} \left( \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right).\)

从独立性性质我们可以写

\(E \left[ S \alpha \frac{1 - \alpha^{\theta_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\theta_{k+1} - \tau_k - 1} D_{\tau_k + l} \frac{\alpha^l - \alpha^{\theta_{k+1} - \tau_k - 1}}{1 - \alpha} \middle| \mathcal{F}^{\tau_k} \right] = E \left[ S \alpha \frac{1 - \alpha^{\tilde{\theta}}}{1 - \alpha} - \sum_{l=0}^{\tilde{\theta}} D_{1+l} \frac{\alpha^l - \alpha^{\tilde{\theta}}}{1 - \alpha} \right],\)

其中 \(\tilde{\theta} = \theta_2 - 2\)。同样地

\(E \left[ S \alpha \frac{1 - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \frac{\alpha^l - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} \middle| \mathcal{F}^{\tau_k} \right] = E \left[ S \alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \frac{\alpha^l - \alpha \alpha^{\theta}}{1 - \alpha} \right],\)

其中 \(\theta = \tau_2 - 2\)。最后

\(E \left[ \alpha^{\tau_{k+1} - \tau_k - 1} \left( \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) \middle| \mathcal{F}^{\tau_k} \right] = E \left[ \alpha^{\theta} \left( \alpha K + \alpha c \sum_{l=0}^{\theta} D_{1+l} \right) \right].\)

因此我们有

\(Z_1 = E X_1 E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1},\)

以及

\(E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} = \sum_{k=1}^{\infty} (E \alpha \alpha^{\theta})^{k-1},\)

并且根据引理 9.6

\(E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} = \frac{1}{(1 - \alpha) \Gamma(S - s)}.\)

此外

\(X_1 = \alpha^{\theta} \left( \alpha K + \alpha c \sum_{l=0}^{\theta} D_{1+l} \right) + (h + p) \left( S \alpha \frac{1 - \alpha^{\hat{\theta}}}{1 - \alpha} - \sum_{l=0}^{\hat{\theta}} D_{1+l} \frac{\alpha^l - \alpha^{\hat{\theta}}}{1 - \alpha} \right) - p \left( S \alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \frac{\alpha^l - \alpha \alpha^{\theta}}{1 - \alpha} \right).\)

我们回顾

$$E \sum_{l=0}^a \alpha^l D_{l+1} = D\Gamma(S-s),$$

以及

$$E\alpha^\theta \sum_{l=0}^\theta D_{l+1} = D\Gamma(S-s) + \frac{1-\alpha}{\alpha} \left( \int_0^{S-s} \Gamma(x)dx - (S-s)\Gamma(S-s) \right).$$

因此，汇总结果我们得到

$$EX_1 = K(1-(1-\alpha)\Gamma(S-s)) - cS(1-\alpha)\Gamma(S-s) \\
+\Gamma(S-s)(\alpha cD + sc(1-\alpha) + p\alpha D - p\alpha s) \\
+(p+h) \left( \int_0^S \Gamma(\xi)d\xi - S \right) + (c(1-\alpha) - p\alpha) \int_0^{S-s} \Gamma(\xi)d\xi.$$

注意

$$g(s) = \alpha cD + sc(1-\alpha) + p\alpha D - p\alpha s.$$

此外，根据 \(\Gamma\) 的积分方程 (9.2.19)，通过积分我们有

$$\Gamma(S) - S = \alpha \int_0^\infty \Gamma(S-\xi)F(\xi)d\xi \\
= \alpha \int_s^S \Gamma(S-\xi)F(\xi)d\xi.$$

因为 \(s \le 0\) 且 \(F(\xi) = 0\)，对于 \(\xi \le 0\)。另外

$$\int_0^{S-s} \Gamma(\xi)d\xi = \int_s^S \Gamma(S-\xi)d\xi.$$

因此

$$(p+h) \left( \int_0^S \Gamma(\xi)d\xi - S \right) + (c(1-\alpha) - p\alpha) \int_0^{S-s} \Gamma(\xi)d\xi \\
= \int_s^S \Gamma(S-\xi)(c(1-\alpha) - p\alpha + \alpha(p+h)F(\xi))d\xi \\
= \int_s^S \Gamma(S-\xi)\mu(\xi)d\xi \\
= H(S).$$

因此

$$EX_1 = K(1-(1-\alpha)\Gamma(S-s)) - cS(1-\alpha)\Gamma(S-s) + \Gamma(S-s)g(s) + H(S).$$

由此可得

$$Z_1 = \frac{K+H(S)}{(1-\alpha)\Gamma(S-s)} + \frac{g(s)}{1-\alpha} - (K+cS),$$

这意味着

$$J_s(V_{s,S}) = -(p+c)x + \frac{g(s)}{1-\alpha} + \frac{K+H(S)}{(1-\alpha)\Gamma(S-s)},$$

因此，在此情况下 (9.3.27) 得证。

## II- \( s \ge 0, x \le s \):

在这种情况下，停止时间 \(\theta_k\) 不相关。然而 \(y(\tau_k)\) 可以是正或负。我们可以写

\(J_s(V_s, s) = K + c(S - x) + hx^+ + px^- + \sum_{k=1}^{\infty} E\alpha^{\tau_{k+1}-1}(K + c(S - y_{\tau_{k+1}}) + hy_{\tau_{k+1}}^+ + py_{\tau_{k+1}}^-) + hE \sum_{k=1}^{\infty} \mathbf{I}_{\tau_{k+1} \ge \tau_k + 2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1} y_n.\)

按照之前的操作，我们得到

\(\sum_{k=1}^{\infty} \mathbf{I}_{\tau_{k+1} \ge \tau_k + 2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1} y_n = \sum_{k=1}^{\infty} \alpha^{\tau_k-1} \left[ S\alpha \frac{1 - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \alpha \frac{\alpha^l - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} \right],\)

以及

\(\sum_{k=1}^{\infty} \alpha^{\tau_{k+1}-1}(K + c(S - y_{\tau_{k+1}}) + hy_{\tau_{k+1}}^+ + py_{\tau_{k+1}}^-) = \sum_{k=1}^{\infty} \alpha^{\tau_k-1} \alpha^{\tau_{k+1} - \tau_k - 1} \left[ \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} + \alpha h \left( S - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) + \alpha p \left( S - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) \right].\)

由此可得

\(J_s(V_s, s) = K + c(S - x) + hx^+ + px^- + Z_2,\)

其中

\(Z_2 = \frac{EX_2}{(1 - \alpha)\Gamma(S - s)},\)

以及

\(X_2 = \alpha^{\theta} \Phi \left( \sum_{l=0}^{\theta} D_{1+l} \right) + h \left[ S\alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \alpha \frac{\alpha^l - \alpha^{\theta}}{1 - \alpha} \right],\)

其中

\(\Phi(\xi) = \alpha K + \alpha c + \alpha h(S - \xi)^+ + \alpha p(S - \xi)^-.\)

要计算 \(EX_2\)，我们需要使用引理 9.6 的公式 (9.2.47)。重排后我们得到

\(E\alpha^{\theta} \Phi \left( \sum_{l=0}^{\theta} D_{1+l} \right) = K(1 - (1 - \alpha)\Gamma(S - s)) - cS(1 - \alpha)\Gamma(S - s) - hs\Gamma(S - s) + \Gamma(S - s)g(s) + H(S) + hS - h \int_s^S \Gamma(S - \xi) d\xi,\)



和之前的结果

```
EhS\left[\alpha \frac{1-\alpha^\theta}{1-\alpha} - \sum_{l=0}^\theta D_{1+l}\alpha \frac{\alpha^l - \alpha^\theta}{1-\alpha}\right] = sh\Gamma(S-s) - hS + h\int_s^S \Gamma(S-\xi)d\xi.
```

因此

```
EX_2 = K + H(S) - (K+cS)(1-\alpha)\Gamma(S-s) + \Gamma(S-s)g(s) = EX_1.
```

因此 \( Z_2 = Z_1 \) 我们再次得到 (9.3.27)。

接下来我们考虑情况

### III. \( x > 0 > s \)

现在 \( \tau_1 \ge 2 \)。我们有定义

```
\tau_1 = 2 + \inf\{n \ge 0 | D_1 + \dots + D_{1+n} \ge x - s\},
```

并且我们需要引入

```
\theta_1 = 2 + \inf\{n \ge 0 | D_1 + \dots + D_{1+n} \ge x\},
```

并且 \( \theta_1 \le \tau_1 \)。我们可以写

```
J_x(V_s, s) = hx + E\mathbf{I}_{\tau_1 \ge 3} \sum_{j=0}^{\tau_1-3} \alpha^{j+1}(hy_{j+2}^+ + py_{j+2}^-) + E\alpha^{\tau_1-1}(K+cS-(c+p)y_{\tau_1}) + \dot{Z}_1.
```

数量 \( \dot{Z}_1 \) 源自与 \( Z_1 \) 相同的定义，参见 (9.3.31)，只是 \( \tau_1 \) 不等于 1。利用独立性性质可以验证

```
\dot{Z}_1 = Z_1 E\alpha^{\tau_1-1}.
```

现在 \( \tau_1 - 2 \) 与 \( \theta \) 具有相同的分布，只是对于 \( x \) 必须放宽 \( S \)。由此可得

```
(9.3.32)
\( E\alpha^{\tau_1-1} = 1 - (1-\alpha)\Gamma(x-s). \)
```

接下来我们写

```
E\mathbf{I}_{\tau_1 \ge 3} \sum_{j=0}^{\tau_1-3} \alpha^{j+1}(hy_{j+2}^+ + py_{j+2}^-)
= (h+p)E\mathbf{I}_{\theta_1 \ge 3} \sum_{j=0}^{\theta_1-3} \alpha^{j+1}y_{j+2} - pE\mathbf{I}_{\tau_1 \ge 3} \sum_{j=0}^{\tau_1-3} \alpha^{j+1}y_{j+2}
= (h+p)E\left[ x \frac{\alpha - \alpha\alpha^{\theta_1-2}}{1-\alpha} - \sum_{l=0}^{\theta_1-2} D_{1+l} \alpha \frac{\alpha^l - \alpha\alpha^{\theta_1-2}}{1-\alpha} \right]
-pE\left[ x \frac{\alpha - \alpha\alpha^{\tau_1-2}}{1-\alpha} - \sum_{l=0}^{\tau_1-2} D_{1+l} \alpha \frac{\alpha^l - \alpha\alpha^{\tau_1-2}}{1-\alpha} \right].
```

然后

```
E\alpha^{\tau_1-1}(K+cS-(c+p)y_{\tau_1}) = E\alpha^{\tau_1-1}\left[ K+cS-(c+p)x+(p+c)\sum_{l=0}^{\tau_1-2} D_{1+l} \right].
```

我们得到

```
\(J_x(V_s, s) = Y_1 + (1 - (1 - \alpha)\Gamma(x - s)) \left[ \frac{K + H(S)}{(1 - \alpha)\Gamma(S - s)} - (K + cS) + \frac{g(s)}{1 - \alpha} \right],\)
```

其中

```
\(Y_1 = hx + (h + p)E \left[ x \frac{\alpha - \alpha\alpha^{\theta_1-2}}{1 - \alpha} - \sum_{l=0}^{\theta_1 - 2} D_{1+l} \alpha \frac{\alpha^l - \alpha\alpha^{\theta_1-2}}{1 - \alpha} \right] - pE \left[ x \frac{\alpha - \alpha\alpha^{\tau_1-2}}{1 - \alpha} - \sum_{l=0}^{\tau_1 - 2} D_{1+l} \alpha \frac{\alpha^l - \alpha\alpha^{\tau_1-2}}{1 - \alpha} \right] + E \alpha^{\tau_1 - 1} \left[ K + cS - (p + c)x + (p + c) \sum_{l=0}^{\tau_1 - 2} D_{1+l} \right].\)
```

含有 \(\tau_1 - 2\) 和 \(\theta_1 - 2\) 的表达式与之前用 \(\theta\) 和 \(\vartheta\) 的类似表达式相同，只是将 \(S\) 替换为 \(x\)。因此

```
\(Y_1 = hx - cx + (K + cS)(1 - (1 - \alpha)\Gamma(x - s)) + g(s)\Gamma(x - s) + (h + p) \left( \int_0^x \Gamma(\xi) d\xi - x \right) + (c(1 - \alpha) - p\alpha) \int_0^{x-s} \Gamma(\xi) d\xi.\)
```

我们注意到

```
\((h+p) \left( \int_0^x \Gamma(\xi) d\xi - x \right) + (c(1 - \alpha) - p\alpha) \int_0^{x-s} \Gamma(\xi) d\xi = H(x),\)
```

利用 \(s < 0\) 的事实，如同我们之前对 \(H(S)\) 所做的那样。汇总结果我们得到 (9.3.28)。

我们转向情况

### IV. \(0 > x > s\).

我们于是有

```
\(J_x(V_s, s) = -px - pE \sum_{j=0}^{\tau_1 - 2} \alpha^{j+1} y_{j+2} + E \alpha^{\tau_1 - 1} (K + cS - c y_{\tau_1}) + \tilde{Z}_1.\)
```

我们再次看到

```
\(J_x(V_s, s) = -px - cx + H(x) + g(s)\Gamma(x - s) + (K + cS)(1 - (1 - \alpha)\Gamma(x - s)) + \tilde{Z}_1,\)
```

我们再次得到 (9.3.28)。

还剩下最后一种情况需要考虑

### V. \(x > s > 0\).

使用类似技术我们验证

```
\(J_x(V_s, s) = Y_2 + \tilde{Z}_2,\)
```

其中

```
\(\tilde{Z}_2 = Z_2(1-(1-\alpha)\Gamma(x-s))\)
\(= Z_1(1-(1-\alpha)\Gamma(x-s))\)
\(= (1-(1-\alpha)\Gamma(x-s)) \left[ \frac{K+H(S)}{(1-\alpha)\Gamma(S-s)} - (K+cS) + \frac{g(s)}{1-\alpha} \right],\)
```

并且

```
\(Y_2 = hx + hE \sum_{j=0}^{n-1} \alpha^{j+1} y_{j+2} + E \alpha^{n-1}(K+cS-cy_n) + (h+p)E \alpha^{n-1} y_n,\)
```

所以

```
\(Y_2 = hx + hE \left[ x \frac{\alpha - \alpha \alpha^{n-2}}{1-\alpha} - \sum_{l=0}^{n-2} D_{1+l} \frac{\alpha^l - \alpha \alpha^{n-2}}{1-\alpha} \right]\)
\(+ E \alpha^{n-1} \Phi_x \left( \sum_{l=0}^{n-2} D_{1+l} \right),\)
```

其中

```
\(\Phi_x(\xi) = \alpha K + \alpha c(S-x) + \alpha \xi + \alpha(h+p)(x-\xi)^-.\)
```

请注意，这里 \(x\) 只是一个参数（之前扮演 \(S\) 的角色）。使用熟悉的技术我们可以验证

```
\(Y_2 = hx - cx + H(x) + (K+cS)(1-(1-\alpha)\Gamma(x-s)) + \Gamma(x-s)g(s),\)
```

并且 (9.3.28) 得到验证。证明完成。\(\square\)

在积压情况中我们有与无积压情况相同的情形。从公式 (9.3.27)、(9.3.28) 可以看出，可以独立于 \(x\) 优化 \(S\)。只需最小化函数

```
\(Z_s(x) = \frac{K+H_s(x)}{\Gamma(x-s)},\)
```

对于 \(x \ge s\)。很容易验证存在最小值，我们总可以取最小的最小值。这与无积压情况相同。因此实际上只剩下一个选择，即 \(s\) 的值。然后我们可以通过公式定义函数 \(u_s(x)\)：

```
(9.3.33)
\(u_s(x) = -cx + hx^+ + px^- + H_s(x) + \frac{g(s)}{1-\alpha}\)
\(+ \frac{(1-(1-\alpha)\Gamma(x-s))}{1-\alpha} \inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)}, \quad \forall x > s\)
```

```
(9.3.34)
\(u_s(x) = (h-c)x + \frac{g(s)}{1-\alpha} +\)
\(+ \frac{1}{1-\alpha} \inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)}, \quad \forall x \le s\)
```

对于 \(x=s\) 存在不连续性，除非

```
(9.3.35)
\(\inf_{\xi \ge s} \frac{K+H_s(\xi)}{\Gamma(\xi-s)} = 0,\)
```

这等价于条件 \(K + \inf_{\xi \ge s} Z_s(\xi) = 0\)。我们恢复了由冲动控制的解析理论（定理 9.11）得到的 \(s, S\) 对。因此 \(s\) 的选择由成本函数的连续性条件决定，而非优化（与 \(S\) 的选择不同）。至于无积压情况，我们在定理 9.11 中已表明，由该 \(s, S\) 控制策略定义的函数是值函数，并且是贝尔曼方程的解。

## 9.3.4. 不变测度。

我们已经在第 3 章第 3.6.2 节中得到了不变测度。我们回顾结果。状态空间是 \(X = (-\infty, S)\)，不变测度相对于勒贝格测度的密度由以下给出

```
\(m(\eta) = \begin{cases} \frac{f(S-\eta)+\int_{\eta}^{S} z(x)f(x-\eta)dx}{1+\int_{\eta}^{S} z(y)dy}, & \text{if } \eta \le s \\ \frac{z(\eta)}{1+\int_{\eta}^{S} z(y)dy}, & \text{if } s \le \eta \le S \end{cases}\)
```

其中函数 \(z(\eta)\) 在 \(s, S\) 中定义为积分方程的唯一解

```
\(z(\eta) = f(S-\eta) + \int_{\eta}^{S} z(x)f(x-\eta)dx, \quad s \le \eta \le S,\)
```

若 \(F(S) < 1\)，则在 \(B(s, S)\) 中存在唯一解。

现在考虑目标函数 \(J_{\bar{\nu}}(V_s)\)，当我们应用由 \(s, S\) 策略定义的控制 \(V = V_{s,S}\) 时。库存 \(y_n\) 变得遍历，因此我们有

```
\((1-\alpha)\int_{-\infty}^{S} J_{\bar{\nu}}(V_{s,S})m_{s,S}(x)dx = \int_{-\infty}^{S} [hx^+ + px^- + (K+c(S-x))\mathbb{1}_{s \le x}]m_{s,S}(x)dx.\)
```

请注意，积分定义良好，因为 \(D\) 是有限的，参见下文 (9.3.38)。

同样

```
\((1-\alpha)\int_{-\infty}^{S} J_{\bar{\nu}}(V_{s,S})m_{s,S}(x)dx = \int_{-\infty}^{S} [(1-\alpha)(hx^+ + px^- - cx) + (K+c(S-x))\mathbb{1}_{s \le x}]m_{s,S}(x)dx + \int_{-\infty}^{S} [c(1-\alpha)x + \alpha(hx^+ + px^-)]m_{s,S}(x)dx.\)
```

我们省略下标 s, S 以简化符号。回顾

```
\(g(x) = cx(1-\alpha) + \alpha c\bar{D} + \alpha h E(x-D)^+ + \alpha p E(x-D)^-.\)
```

由此可得

```
\(g(x)\mathbb{1}_{x>s} + g(S)\mathbb{1}_{x \le s} = c(1-\alpha)x + \alpha c\bar{D} + c(1-\alpha)(S-x)\mathbb{1}_{x \le s} + \alpha h E(x-D)^+ \mathbb{1}_{x>s} + \alpha h E(S-D)^+ \mathbb{1}_{x \le s} + \alpha p E(x-D)^- \mathbb{1}_{x>s} + \alpha p E(S-D)^- \mathbb{1}_{x \le s}.\)
```

另一方面，从给出 \(H(x)\) 的方程，参见 (9.3.13)，我们有

```
\(g(x)\mathbb{1}_{x>s} + g(S)\mathbb{1}_{x \le s} = H(x) + H(S)\mathbb{1}_{x \le s} + g(s) - \alpha [EH(x-D)\mathbb{1}_{x>s} + EH(S-D)\mathbb{1}_{x \le s}].\)
```





对不变量测度进行积分，并利用其基本性质，我们得到

\[
\int_{-\infty}^s (g(x)\mathbb{I}_{x>s} + g(s)\mathbb{I}_{x \le s})m(x)dx
= \alpha c\bar{D} + \int_{-\infty}^s [c(1-\alpha)x + \alpha h^+ + \alpha p^-]m(x)dx
+ c(1-\alpha) \int_{-\infty}^s (S-x)m(x)dx
= (1-\alpha) \int_{-\infty}^s H(x)m(x)dx + g(s) + H(s) \int_{-\infty}^s m(x)dx.
\]

因此

\[
(1-\alpha) \int_{-\infty}^s J_x(V)m(x)dx = \int_{-\infty}^s (1-\alpha)(hx^+ + px^- - cx + H(x))m(x)dx
+(K+H(s)) \int_{-\infty}^s m(x)dx + g(s) + c\alpha \left[ \int_{-\infty}^s (S-x)m(x)dx - D \right].
\]

现在我们使用性质

(9.3.38) \(\bar{D} = \int_{-\infty}^s (S-x)m(x)dx.\)

这由以下等式得出

\(\int_{-\infty}^s xm(x)dx = \int_{-\infty}^s [\mathbb{I}_{x>s}E(x-D) + \mathbb{I}_{x \le s}E(S-D)]m(x)dx,\)

这是不变量测度基本性质的结果。

因此，我们得到

(9.3.39) \(\int_{-\infty}^s J_x(V)m(x)dx = \int_{-\infty}^s (hx^+ + px^- - cx + H(x))m(x)dx\)
\(+ \frac{g(s)}{1-\alpha} + \frac{K+H(s)}{1-\alpha} \int_{-\infty}^s m(x)dx.\)

我们可以直接从公式(9.3.39)以及给出\(J_x(V)\)的公式(9.3.27)、(9.3.28)中推导出来。需要证明函数\(\Gamma(x)\)满足关系式

(9.3.40) \(\Gamma(S-s) \int_{-\infty}^s m(dx) + (1-\alpha) \int_s^S \Gamma(x-s)m(dx) = 1,\)

这与(9.2.71)类似。

### 9.3.5. 特殊情况。

考虑情形\(f(x) = \beta \exp -\beta x\)。我们回顾一下

(9.3.41) \(\Gamma(x) = \frac{1}{1-\alpha} - \frac{\alpha}{1-\alpha} \exp -\beta(1-\alpha)x,\)

那么

(9.3.42) \(\mu(x) = c(1-\alpha) + \alpha h - \alpha(p+h) \exp -\beta x^+,\)

并且

(9.3.43) \(g(x) = c(1-\alpha)x + \alpha(hx^+ + px^-) + \alpha(c+p)\bar{D} + \alpha \frac{h+p}{\beta}(\exp -\beta x^+ - 1).\)

使得\(\mu(\bar{s}) = 0\)的值\(\bar{s} > 0\)由以下给出

(9.3.44) \(\exp -\beta\bar{s} = \frac{c(1-\alpha) + \alpha h}{\alpha(p + h)},\)

得益于假设(9.3.16)。

接下来，对于\(x > s\)，我们有

\[
H'(x) = c(1 - \alpha) + \alpha h - \alpha(p + h) \exp -\beta x^+
+ \frac{\alpha}{1-\alpha}(c(1-\alpha) + \alpha h)[1 - \exp -\beta(1-\alpha)(x-s)]
- \alpha^2\beta(p+h) \exp -\beta(1-\alpha)x \left\{ \frac{\exp -\beta(1-\alpha)x^- - \exp -\beta(1-\alpha)s^-}{\beta(1-\alpha)} \right.
\left. - \frac{\exp -\beta\alpha x^+ - \exp -\beta\alpha s^+}{\beta\alpha} \right\};
\]

对于\(s \le \bar{s}\)，数字\(S\)由方程\(H'(S) = 0\)唯一确定。

现在让我们转向不变量测度。(9.3.37)的解是\(z(\eta) = \beta\)，并且

(9.3.45) \(m(\eta) = \begin{cases} \frac{\beta}{1 + \beta(S - s)}, & \text{if } s \le \eta \le S \\ \frac{\beta \exp -\beta(S - \eta)}{1 + \beta(S - s)}, & \text{if } \eta \le s \end{cases}\)

# 带设置成本的库存遍历控制

在本章中，我们将考虑前一章研究的情况，即\(\alpha \to 1\)的情况。

## 10.1. 确定性情形

### 10.1.1. 问题设定。

我们考虑函数方程

(10.1.1) \( u_\alpha(x) = hx + \inf_{v \ge (D-x)^+} [K \mathbf{1}_{v>0} + cv + \alpha u_\alpha(x+v-D)], \)

其中我们强调了对\(\alpha\)的依赖。我们知道最优反馈由以下给出

(10.1.2) \( \hat{v}_\alpha(x) = \begin{cases} 0, & \text{if } x \ge D \\ D(\hat{k}_\alpha + 1) - x, & \text{if } x < D \end{cases} \)

其中\(\hat{k}_\alpha\)使以下最小化

\( \lambda_\alpha(k) = \frac{K + c(k+1)D + \alpha h D F_\alpha(k)}{1 - \alpha^{k+1}}, \)

其中

\( F_\alpha(k) = \frac{\alpha^{k+1} - (k+1)\alpha + k}{(1 - \alpha)^2}. \)

我们希望研究当\(\alpha \to 1\)时\(u_\alpha(x)\)和\(\hat{v}_\alpha(x)\)的行为。

### 10.1.2. 收敛性。

我们定义使以下最小化的整数\(\hat{k}\)

(10.1.3) \( \lambda_1(k) = \frac{K}{k+1} + hD\frac{k}{2}, \)

在\(k \ge 0\)范围内。接下来我们定义

(10.1.4) \( \rho = cD + \lambda_1(\hat{k}), \)

然后我们可以给出以下收敛结果

### 定理 10.1. 当\(\alpha \to 1\)时，我们具有以下性质

(10.1.5) \( \varrho_\alpha = (1 - \alpha)u_\alpha(0) \to \rho; \)

(10.1.6) \( z_\alpha(x) = u_\alpha(x) - u_\alpha(0) \to z(x), \)

其中

(10.1.7) \( z(x) = \begin{cases} (h-c)x, & \text{if } x < D \\ hx - \rho + z(x-D), & \text{if } x \ge D \end{cases} \)

我们也可以写成

(10.1.8) \( z(x) + \rho = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v>0} + cv + z(x+v-D)], \)

并且由(10.1.11)、(10.1.4)给出的对\(z(x), \rho\)是(10.1.8)的唯一解。此外，最优反馈是

(10.1.9) \( \hat{v}(x) = \begin{cases} 0, & \text{if } x \ge D \\ D(\hat{k}+1) - x, & \text{if } x < D \end{cases} \)

证明。(10.1.11)的解简单地为

(10.1.10) \( z(kD + \xi) = hD \frac{k(k+1)}{2} + \xi h(k+1) - k\rho, \forall 0 \le \xi < D; \)
\( z(((k+1)D)^+) = hD \frac{(k+1)(k+2)}{2} - (k+1)\rho, \)

其中再次\(z(((k+1)D)^+)\)表示在点\((k+1)D\)处的右极限。我们知道

\( u_\alpha(0) = \lambda_\alpha(\hat{k}_\alpha), \)

并且很容易验证

\( (1-\alpha)\lambda_\alpha(k) \to cD + \lambda_1(k), \forall k. \)

这一性质传递到下确界上，

\( \hat{k}_\alpha \to \hat{k}, \)

这证明了(10.1.5)。根据定义，

(10.1.11) \( z_\alpha(x) = \begin{cases} (h-c)x, & \text{if } x < D \\ hx - \rho_\alpha + z_\alpha(x-D), & \text{if } x \ge D \end{cases} \)

得益于(10.1.5)，\(z_\alpha(x)\)到\(z(x)\)的收敛容易得到。为了证明(10.1.8)，我们来看(10.1.11)，它可以写成

(10.1.12) \( z_\alpha(x) + \rho_\alpha = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v>0} + cv + \alpha z_\alpha(x+v-D)]. \)

我们注意到关系式

(10.1.13) \( \rho_\alpha = K + Dc(\hat{k}_\alpha+1) + \alpha z_\alpha(\hat{k}_\alpha D). \)

记

\( G_\alpha(x, v) = K \mathbb{I}_{v>0} + c(v+x) + \alpha z_\alpha(x+v-D), \)

并且

\( G_\alpha(x) = \inf_{v \ge (D-x)^+} G_\alpha(x, v) = G_\alpha(x, \hat{v}_\alpha(x)), \)

类似地

\( G(x, v) = K \mathbb{I}_{v>0} + c(v+x) + z(x+v-D); \)
\( G(x) = \inf_{v \ge (D-x)^+} G(x, v) = G(x, \hat{v}(x)). \)

我们声称

(10.1.14) \( G_\alpha(x) \to G(x). \)

确实，当\(x \ge D\)时，\(G_\alpha(x) = G_\alpha(x, 0) \to G(x, 0) = G(x)\)。当\(x < D\)时，则由(10.1.13)和\(\hat{v}_\alpha(x)\)的表达式

\( G_\alpha(x) = \rho_\alpha \to \rho = G(x). \)

我们可以对(10.1.12)取极限并得到(10.1.8)和(10.1.9)。证明已完成。

### 10.1.3. 解释。

\(\rho\)的解释很容易。考虑库存演化

\(y_{n+1} = y_n + v_n - D, \quad y_1 = 0,\)

并使用以下策略。在时刻1下订单，\(v_1 = (k+1)D\)（我们必须下订单，否则库存将变为负数，这是被禁止的）。然后我们不再下订单，直到库存变为0。这发生在时刻\(k+1\)。该策略的成本为

\(K + cD(k+1) + hD \frac{k(k+1)}{2},\)

单位时间的成本为

\(\frac{K}{k+1} + cD + \frac{hDk}{2}.\)

所以\(\rho\)是最小平均成本。关于\(z(x)\)，我们可以参考(10.1.8)并将其解释为贝尔曼方程。考虑演化

\(y_{n+1} = y_n + v_n - D, \quad y_1 = x\)
\(v_n \ge (D - y_n)^+\)

和成本泛函

(10.1.15) \(J_x(V) = \sum_{n=1}^\infty [K \mathbb{I}_{v_n > 0} + c v_n + h y_n - \rho],\)

那么有

\(z(x) = \inf_V J_x(V).\)

**注释。** 如果我们考虑定义\(\lambda_1(k)\)的方程(10.1.3)并做变量变换\(q = Dk\)，我们得到，做近似\(D(k+1) \sim q\)，

\(\lambda_1(k) = \tilde{\lambda}_1(q) = \frac{KD}{q} + \frac{hq}{2},\)

我们恢复了导致EOQ公式的成本，参见第2.2.1节。

## 10.2. 带固定成本且无短缺的库存遍历控制

### 10.2.1. 问题陈述。

我们考虑贝尔曼方程

(10.2.1) \(u_\alpha(x) = (h-c)x + \inf_{\eta \ge x} \{ K \mathbb{I}_{\eta > x} + c\eta + pE((\eta - D)^-) + \alpha E u_\alpha((\eta - D)^+) \},\)

在9.2节中研究。定义

(10.2.2) \(g_\alpha(x) = (p - \alpha(c-h))E(x-D)^+ - (p-c)x + pD,\)

并且

(10.2.3) \(g_{\alpha,s}(x) = (g_\alpha(x) - g_\alpha(s)) \mathbb{I}_{s \ge x},\)

(10.2.4) \(H_{\alpha,s}(x) = \sum_{n=1}^\infty \alpha^{n-1} g_{\alpha,s} * f^{*(n-1)}(x).\)





令 \(\mu_\alpha(x) = g'_\alpha(x)\)，则

(10.2.5) \(H_{\alpha, s}(x) = \int_s^x \Gamma_\alpha(x - \xi) \mu_\alpha(\xi) d\xi,\)

其中 \(\Gamma_\alpha(x)\) 是更新方程的解

(10.2.6) \(\Gamma_\alpha(x) = 1 + \alpha \int_0^x f(x - \xi) \Gamma_\alpha(\xi) d\xi.\)

我们定义函数 \(S_\alpha(s)\) 使得

(10.2.7) \(\inf_{\eta \ge s} H_{\alpha, s}(\eta) = H_{\alpha, s}(S_\alpha(s)),\)

且对 \(s_\alpha, S_\alpha\) 由关系式定义

(10.2.8) \(\inf_{\eta \ge s_\alpha} H_{\alpha, s_\alpha}(\eta) + K = 0, \quad S_\alpha = S_\alpha(s_\alpha).\)

我们知道

(10.2.9) \(0 \le s_\alpha \le \bar{s}_\alpha,\)

其中

(10.2.10) \(c(1 - \alpha) + \alpha h - (p - \alpha(c - h))\bar{F}(\bar{s}_\alpha) = 0.\)

最后

(10.2.11) \(u_\alpha(x) = H_{\alpha, s_\alpha}(x) + (h - c)x + \frac{g_\alpha(s_\alpha)}{1 - \alpha}.\)

我们希望研究当 \(\alpha \uparrow 1\) 时 \(u_\alpha(x)\) 的行为。

## 10.2.2. 收敛.

我们做如下假设

(10.2.12) \(F(x) < 1, \forall x.\)

得益于假设 (10.2.12)，函数 \(\Gamma_\alpha(x)\) 收敛到 \(\Gamma(x)\)，其中

\(\Gamma(x) = \sum_{n=0}^\infty F^{(n)}(x).\)

我们注意到

\(\Gamma(x) \le \frac{1}{1 - F(x)};\)

且 \(\Gamma(x)\) 是更新方程的解

(10.2.13) \(\Gamma(x) = 1 + \int_0^x f(x - \xi) \Gamma(\xi) d\xi.\)

接下来有

(10.2.14) \(\mu_\alpha(x) \to \mu(x) = h - (p - c + h)\bar{F}(x).\)

同样

(10.2.15) \(\begin{aligned} g_\alpha(x) \to g(x) &= hx + p\bar{D} - (p - c + h) \int_0^x \bar{F}(\xi) d\xi \\ &= hx + (c - h)D + (p - c + h)E(x - D)^- \end{aligned}\)

函数

(10.2.16) \(H_{\alpha, s}(x) \to H_s(x) = \int_s^x \Gamma(x - \xi) \mu(\xi) d\xi.\)

假设 (9.2.12)，我们定义 \(\bar{s}\) 使得 \(\mu(\bar{s}) = 0\)，且 \(\mu(s) < 0, \forall 0 \le s < \bar{s}\)，\(\mu(s) > 0, \forall s > \bar{s}\)。

**引理 10.1.** 对 \(x \ge s\) 的 \(H_s(x)\) 的最小值在严格大于 \(\bar{s}\) 的点处取得。而且 \(\min_{x \ge s} H_s(x) < 0\)。

证明. 与对 \(H_{\alpha,s}(x)\) 所做的不同，我们不能依赖于 \(H_{\alpha,s}(x) \to +\infty\) 当 \(x \to +\infty\) 的事实。这是因为 \(\Gamma(x)\) 不像 \(\Gamma_\alpha(x)\) 那样先验有界。对于 \(s < \bar{s}\)，我们可以假设 \(s \le \bar{s}_\alpha\)。因此我们有

\(s \le \bar{s}_\alpha < S_\alpha(s) < S_\alpha(0).\)

回顾

\(\Gamma_\alpha(S_\alpha(0)) = \frac{p - \alpha(c - h)}{p - \alpha(p - h)},\)

我们可以断言 \(S_\alpha(0) \to S(0)\) 是

(10.2.17) \(\Gamma(S(0)) = \frac{p - c + h}{h}.\)

的解。因此我们可以提取 \(S_\alpha(s)\) 的一个子序列，它收敛到 \(S^*_s\)。显然 \(s < \bar{s} \le S^*_s \le S(0)\)。

显然 \(H_{\alpha,s}(S_\alpha(s)) \to H_s(S^*_s)\)。由于 \(H_{\alpha,s}(S_\alpha(s)) \le H_{\alpha,s}(x), \forall x \ge s\)，我们也得到 \(H_s(S^*_s) \le H_s(x), \forall x \ge s\)。因此 \(H_s(S^*_s) = \inf_{x \ge s} H_s(x)\)。所以下确界被取得。由于 \(H_s(\bar{s}+) < 0\)，下确界不在 \(s\) 处取得且严格为负。注意 \(S^*_s\) 是方程的解

(10.2.18) \(\Gamma(S - s)\mu(s) + (p - c + h) \int_s^{S^*} \Gamma(S - \xi) f(\xi) d\xi = 0,\)

因此如果 \(s < \bar{s}\)，我们不能有 \(S^*_s = s\)。

我们然后唯一地定义最小值，称为 \(S(s)\) 且 \(S(s) > \bar{s}\)。而且 \(S(s) = s, \forall s \ge \bar{s}\)。

我们又有

\(\frac{d}{ds} H_s(S(s)) = -\Gamma(S(s) - s)\mu(s) > 0, 0 \le s < \bar{s}.\)

函数 \(H_s(S(s))\) 从 \(H_0(S(0))\) 增加到 0，当 \(s\) 从 0 到 \(\bar{s}\)。

假设

(10.2.19) \(H_0(S(0)) < -K,\)

则存在唯一的 \(s\) 使得

(10.2.20) \(H_s(S(s)) = -K.\)

**定理 10.2.** 我们假设 (9.2.12), (10.2.12), (10.2.19)，则我们有

(10.2.21) \(s_\alpha \to s, \quad S_\alpha \to S;\)

(10.2.22) \(u_\alpha(x) = \frac{g_\alpha(s_\alpha)}{1-\alpha} \to u(x) = H(x) + (h-c)x.\)

**证明.** 我们再次使用 \(S_\alpha(s)\) 是递减的事实，见命题 9.3。因此 \(S_\alpha = S_\alpha(s_\alpha) \le S_\alpha(0)\)，它保持有界。我们有 \(S_\alpha(0) \to S(0) = S_0\)（为了简化记号）。而且 \(H_\alpha(0, S_\alpha(0)) \to H_0(S_0)\)。因此，从假设 (10.2.19)，我们可以假设，对于 \(\alpha\) 足够接近 1，\(H_\alpha(0, S_\alpha(0)) < -K\)。因此对 \(s_\alpha, S_\alpha\) 定义良好，且这些数保持有界。所以我们可以提取一个收敛到 \(s^*, S^*\) 的子序列。从 \(H_\alpha(x)\) 的表达式，我们容易推断出 \(H_{\alpha, s_\alpha}(S_\alpha) = -K \to H_{s^*}(S^*)\)。由此得到 \(s^* = s, S^* = S\)，由方程 (10.2.20), (10.2.18) 定义。

我们注意到

(10.2.24) \(g(x) = hx + p \int_x^\infty F(\xi) d\xi + (c-h) \int_0^x F(\xi) d\xi,\)

所以它是正函数，得益于假设 (9.2.12)。因此 \(\rho > 0\)。显然 \((1-\alpha)u_\alpha(x) - g_\alpha(s_\alpha) \to 0, \text{ 当 } \alpha \uparrow 1,\)

因此

\((1-\alpha)u_\alpha(x) \to \rho = g(s).\)

我们回顾我们还有

\(H(x) + \rho = g(x) + EH((x-D)^+), \forall x \ge s; H(x) = 0, \forall x \le s,\)

其中 \(H(x) = H_s(x)\)，由 (10.2.16) 定义，针对特定的 \(s\)，即 \(s_\alpha\) 的极限。让我们检查这些条件是否可以总结为

(10.2.25) \(H(x) + \rho = + \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + g(\eta) + EH((\eta - D)^+)].\)

如果 (10.2.25) 满足，那么 \(u\) 的方程 (10.2.23) 立即得出，使用 \(g(x)\) 的定义。

让我们检查 (10.2.25)。首先取 \(x \le s\)。那么 \(H(x) = 0\)。如果我们表示 (10.2.25) 的右边，那么我们必须考虑 \(\eta = x\) 和 \(\eta > x\) 的情况。对于 \(\eta = x\) 我们有

\(-\rho + g(x) + EH((x-D)^+) = g(x) - g(s) > 0,\)

因为 \(x < s < \bar{s}\)。另一方面对于 \(x < \eta < s\) 我们有

\(-\rho + K + g(\eta) + EH((\eta - D)^+) = -\rho + K + g(\eta),\)

它是递减的。因此

\(-\rho + K + \inf_{\eta \ge x} [g(\eta) + EH((\eta - D)^+)]\)
\(= -\rho + K + \inf_{\eta \ge x} [g(\eta) + EH((\eta - D)^+)]\)
\(= -\rho + K + \inf_{\eta \ge x} [H(\eta) + g(s)] = 0.\)

因此 (10.2.25) 对 \(x \le s\) 得到验证。假设 \(x > s\)。那么

(10.2.26) \(-\rho + \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + g(\eta) + EH((\eta - D)^+)] = \inf_{\eta \ge x} [K \mathbf{1}_{\eta > x} + H(\eta)].\)

但是，从 (12.5.3) 我们有，记 \(H_\alpha(x) = H_{\alpha, s_\alpha}(x)\)

\(H_\alpha(x) \le K + \inf_{\eta \ge x} H_\alpha(\eta), \forall x \ge s_\alpha.\)

但是 \( H_{\alpha, s_\alpha}(x) \to H(x) \)。我们取极限并得到

\( H(x) \le K + \inf_{\eta \ge x} H(\eta), \forall x \ge s \)

并且 (10.2.26) 的右边是 \( H(x) \)。这完成了定理的证明。

## 10.2.3. 概率解释.

我们现在给出 \(\rho\) 和 (10.2.23) 的解 \(u(x)\) 的解释。我们首先将 \(s, S\) 策略与一个不变量度 \(m_{s, S}(dx)\) 关联起来。而且方程 (10.2.23), (10.2.25) 中的下确界由与 \(s, S\) 策略关联的反馈 \(\hat{v}(x)\) 取得。我们仍将其记为 \(s, S\) 以节省记号。

注意到以下内容很方便

(10.2.27) \( l(x, v) = p\bar{D} + (h - p)x + \mathbb{I}_{v > 0}(K + (c - p)v) + pE(x + v - D)^+, \text{和} \)

和

(10.2.28) \( l(x, \hat{v}(x)) = p\bar{D} + (h - p)x + \mathbb{I}_{x \le S}(K + (c - p)(S - x)) + p[\mathbb{I}_{x \le S}E(S - D)^+ + \mathbb{I}_{x > S}E(x - D)^+], \)

并且 (10.2.23) 读作

(10.2.29) \( u(x) = l(x, \hat{v}(x)) - \rho + Eu(x + \hat{v}(x) - D). \)

让我们用 \( m_{h_c(x)}(dx) \) 表示不变量度 \( m_{s, S}(dx) \)，为了记号的一致性。从 (10.2.29) 得出

(10.2.30) \( \rho = \int l(x, \hat{v}(x))m_{h_c(x)}(dx). \)

注意 \( m_{h_c(x)}(dx) \) 的状态空间是 \( [0, S] \) 但可以取为 \( [0, \infty) \) 以使用固定状态空间。现在定义反馈集合 \( \mathcal{U}_b \) 使得

(10.2.31) \( \mathcal{U}_b = \{v(.) \ge 0 | \exists M \text{ 使得 } x + v(x) \le \max(x, M)\} . \)

如果 \( v(.) \in \mathcal{U}_b \)，必然 \( v(x) = 0 \)，如果 \( x \ge M \)。由反馈 \( v(.) \) 控制的马尔可夫链是遍历的，状态空间为 \( [0, M] \)。我们用 \( m_{v(.)}(dx) \) 表示相应的不变量度。注意由 \( s, S \) 策略定义的反馈属于 \( \mathcal{U}_b \)。我们然后有

**定理 10.3.** 我们做定理 10.2 的假设。我们有

(10.2.32) \( \rho = \inf_{v(.) \in \mathcal{U}_b} \int l(x, v(x))m_{v(.)}(dx), \)

并且存在一个由 \( s, S \) 策略定义的最优反馈。这个 \( s, S \) 策略已在定理 10.2 中定义。

证明. 考虑 \( \mathcal{U}_b \) 中的一个反馈 \( v(.) \)。从 (10.2.23) 我们可以陈述

(10.2.33) \( u(x) + \rho \le l(x, v(x)) + Eu(x + v(x) - D)^+. \)

对不变量度 \( m_{v(.)}(dx) \) 积分得到

\( \rho \le \int l(x, v(x))m_{v(.)}(dx). \)

考虑到 (10.2.30) 结果立即得出。





### 注释 10.1.
设 \( J_{\alpha, x}(v(\cdot)) \) 为带折扣 \(\alpha\) 的受控马尔可夫链的成本泛函，其中控制由属于 \( \mathcal{U}_b \) 的反馈 \( v(\cdot) \) 定义。根据 ergodic 理论，我们可以断言

(10.2.34) \[
(1 - \alpha) J_{\alpha, x}(v(\cdot)) \to \int l(\xi, v(\xi)) m_{v(\cdot)}(d\xi).
\]

因此我们还有

(10.2.35) \[
\rho = \inf_{v(\cdot) \in \mathcal{U}_b} \lim_{n \to \infty} (1 - \alpha) J_{\alpha, x}(v(\cdot)).
\]

让我们也给出函数 \( u(x) \) 的解释。选取 \( \mathcal{U}_b \) 中的一个反馈。记 \( y_n, v_n \) 为对应的轨迹，其中

\[
y_{n+1} = (y_n + v_n - D_n)^+ \quad v_n = v(y_n); \quad y_1 = x.
\]

### 引理 10.2.
我们有性质

(10.2.36) \[
Eu(y_n) \to \int u(x) m_{v(\cdot)}(dx).
\]

**证明。** 该积分定义良好，因为函数 \( u(x) \) 是连续的，且 \( m_{v(\cdot)}(dx) \) 的值域为 \( [0, M] \)。事实上，(10.2.36) 对任意连续函数均成立。通过取 \( u(x) \) 的正部和负部，我们可以假设 \( u(x) \ge 0 \)。考虑数列 \( u_\epsilon(x) = \frac{u(x)}{1 + \epsilon u(x)} \)。我们注意到 \( 0 \le y_n \le \max(x, M) \)。因此 \( Eu(y_n) < \infty \)，我们可以写成

(10.2.37) \[
Eu(y_n) = Eu_\epsilon(y_n) + \epsilon \frac{u^2(y_n)}{1 + \epsilon u(y_n)}.
\]

且 \( \frac{u^2(y_n)}{1 + \epsilon u(y_n)} \le C = \max_{\xi \in [0, \max(x, M)]} u^2(\xi) \)。若初始库存 \( x > M \)，我们注意到

\[
\{y_{n+1} > M\} = \{D_1 + \cdots + D_n < x - M\}.
\]

因此

\[
P(\{y_{n+1} > M\}) = F^{(n)}(x - M) \le F^n(x - M).
\]

现在

\[
\limsup_{n \to \infty} Eu_\epsilon(y_n) = \limsup_{n \to \infty} Eu_\epsilon(y_{n+n_0}) \le \frac{1}{\epsilon} P(y_{n_0} > M) + \limsup_{n \to \infty} E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}).
\]

根据 ergodic 理论，利用 \( u_\epsilon(x) \) 有界（由 \( \frac{1}{\epsilon} \) 界限）的事实，我们有

\[
E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}) \to \int u_\epsilon(x) m_{v(\cdot)}(dx), \quad \text{as } n \to \infty.
\]

因此

\[
\limsup_{n \to \infty} Eu_\epsilon(y_n) \le \int u_\epsilon(x) m_{v(\cdot)}(dx) + \frac{1}{\epsilon} P(y_{n_0} > M).
\]

令 \( n_0 \to \infty \)，我们得到

\[
\limsup_{n \to \infty} Eu_\epsilon(y_n) \le \int u_\epsilon(x) m_{v(\cdot)}(dx).
\]

另一方面，我们还有

\[
\liminf_{n \to \infty} Eu_\epsilon(y_n) = \liminf_{n \to \infty} Eu_\epsilon(y_{n+n_0}) \ge \liminf_{n \to \infty} E I_{\{y_{n_0} \le M\}} u_\epsilon(y_{n+n_0}).
\]

因此

\[
\liminf_{n \to \infty} E u_\epsilon(y_n) \ge \int u_\epsilon(x) m_{v(\cdot)}(dx).
\]

故

\[
E u_\epsilon(y_n) \to \int u_\epsilon(x) m_{v(\cdot)}(dx),
\]

当 \( n \to \infty \)。现在令 \( \epsilon \to 0 \) 并使用法图引理，我们推断

\[
\int u_\epsilon(x) m_{v(\cdot)}(dx) \to \int u(x) m_{v(\cdot)}(dx).
\]

另一方面，由 (10.2.37)，我们有

\[
|Eu(y_n) - Eu_\epsilon(y_n)| \le C\epsilon,
\]

故

\[
\limsup_{n \to \infty} E u(y_n) \le \int u(x) m_{v(\cdot)}(dx) + C\epsilon.
\]

令 \( \epsilon \to 0 \)，我们得到

\[
\limsup_{n \to \infty} E u(y_n) \le \int u(x) m_{v(\cdot)}(dx).
\]

现在，

\[
\liminf_{n \to \infty} E u(y_n) \ge \liminf_{n \to \infty} E u_\epsilon(y_n) = \int u_\epsilon(x) m_{v(\cdot)}(dx).
\]

令 \( \epsilon \to 0 \)，并使用勒贝格定理，我们得到

\[
\liminf_{n \to \infty} E u(y_n) \ge \int u(x) m_{v(\cdot)}(dx),
\]

结果随之得出。

考虑一个反馈 \( v(\cdot) \in \mathcal{U}_b \)，并考虑 \( y_n, v_n \) 的对应轨迹。定义

(10.2.38) \[
J_x^n(v(\cdot)) = \sum_{j=1}^n E(l(y_j, v_j)) - n\rho.
\]

我们断言

### 定理 10.4.
我们采用定理 10.2 的假设。那么 \( J_x^n(\hat{v}(\cdot)) \) 在 \( n \to \infty \) 时有极限，并且

(10.2.39) \[
u(x) = \lim_{n \to \infty} J_x^n(\hat{v}(\cdot)) + \int u(x) m_{v(\cdot)}(dx).
\]

此外，对于 \( v(\cdot) \in \mathcal{U}_b \)，\( J_x^n(v(\cdot)) \) 下有界，并且有

(10.2.40) \[
u(x) = \inf_{v(\cdot) \in \mathcal{U}_b} \left[ \liminf_{n \to \infty} J_x^n(v(\cdot)) + \int u(x) m_{v(\cdot)}(dx) \right].
\]

**证明。** 由方程 (10.2.29) 我们容易验证

\[
u(x) = J_x^n(\hat{v}(\cdot)) + Eu(\hat{y}_{n+1}),
\]

并由 (10.2.36) 我们容易推导出性质 (10.2.39)。同样，考虑任何属于 \( \mathcal{U}_b \) 的反馈，我们可以使用 (10.2.31) (10.2.31) 写出

\[
u(x) \le J_x^n(v(\cdot)) + Eu(y_{n+1}).
\]

再次使用 (10.2.36)，我们得到

\[
u(x) \le \liminf_{n \to \infty} J_x^n(v(\cdot)) + \int u(x) m_{v(\cdot)}(dx),
\]

性质 (10.2.40) 随之得出。

我们看到函数 \( u(\cdot) \) 进入目标函数的定义。

## 10.2.4. 特殊情况.

我们考虑指数分布 \( f(x) = \beta \exp -\beta x \) 的特殊情况。更新方程 (10.2.13) 的解 \( \Gamma(x) \) 容易看出为

(10.2.41) \[
\Gamma(x) = 1 + \beta x.
\]

接下来我们有

(10.2.42) \[
\mu(x) = h - (p - c + h) \exp -\beta x,
\]

以及

(10.2.43) \[
g(x) = hx + \frac{p}{\beta} - \frac{p - c + h}{\beta} (1 - \exp -\beta x).
\]

我们接着计算，对于 \( x > s \)

(10.2.44) \[
H(x) = \int_s^x \Gamma(x - \xi) \mu(\xi) d\xi
= h(x - s) + \frac{\beta h}{2} (x - s)^2 - (p - c + h)(x - s) \exp -\beta s
\]

数 \( \bar{s} \) 满足 \( \mu(\bar{s})=0 \)，因此

(10.2.45) \[
\exp -\beta \bar{s} = \frac{h}{p - c + h}.
\]

我们因此考虑 \( 0 \le s \le \bar{s} \)。我们通过 \( H'(S) = 0 \) 定义 \( S(s) \)，因此

(10.2.46) \[
h + \beta h(S - s) - (p - c + h) \exp -\beta s = 0.
\]

该方程对于 \( s \le \bar{s} \) 有唯一解 \( S = S(s) \)，并且容易验证 \( S \ge s \)。我们接下来定义 \( s \) 的值。我们需要一个条件，参见 (10.2.19)。令 \( S_0 = S(0) \)。由 (10.2.46) 代入 \( s = 0 \)，我们得到 \( S_0 = \frac{p-c}{\beta h} \)，接着，由公式 (10.2.44) 代入 \( s = 0 \)，我们看到 \( H_0(S_0) = - \frac{(p-c)^2}{2\beta h} \)，且 \( K \) 的条件为

(10.2.47) \[
K < \frac{(p-c)^2}{2\beta h}.
\]

为了定义 \( s \)，我们必须写出方程 \( H_s(S) = -K \)。使用公式 (10.2.44) 和 (10.2.46)，我们验证

\[
H_s(S(s)) = - \frac{[(p - c + h) \exp -\beta s - h]^2}{2\beta h},
\]

并且我们容易得到 \( s \) 的值，由

(10.2.48) \[
\exp -\beta s = \frac{h + \sqrt{2\beta h K}}{p - c + h}.
\]

得益于条件 (10.2.47)，(10.2.48) 的右端小于 1，因此 \( s < \bar{s} \) 定义良好。将 (10.2.48) 代入 (10.2.46)，我们可以验证公式

(10.2.49) \[
S - s = \sqrt{\frac{2K}{\beta h}} = \sqrt{\frac{2KD}{h}}.
\]

### 注释 10.2.
如果我们与确定性情况 (10.1.3) 相比，其中我们有一个 \( s, S \) 策略，且 \( s = D \) 与 \( S = D(k + 1) \)，所以 \( S - s = D\bar{k} \)。整数 \( \bar{k} \) 最小化 \( K/(k+1) + hDk/2 \)。将 \( \bar{k} \) 和 \( k + 1 \) 视为同一实数，我们得到 \( \bar{k} = \sqrt{2K/(hD)} \)，因此 \( S - s = \sqrt{2KD/h} \)，这正是 (10.2.49)，当然 \( D = \bar{D} \)。所以订购量与确定性等价情况相同，但订购点 \( s \) 不是 \( D \)。它考虑了随机性，以及当某些需求未得到满足时的惩罚。这在确定性情况下不可能发生。

我们接下来可以得到数 \( \rho = g(s) \)。使用 (10.2.48) 我们得到

\[
\rho = hs + \frac{c}{\beta} + \frac{\sqrt{2\beta hK}}{\beta},
\]

因此也有

(10.2.50) \[
\rho = \frac{c}{\beta} + hS,
\]

这也等价于确定性情况，参见 (10.1.4)。让我们通过概率解释，定理 10.3 来恢复这个公式。我们不会选取 \( \mathcal{U}_b \) 中的任何反馈，而只选取由 \( s, S \) 策略定义的那些反馈。所以考虑一个由 \( s, S \) 策略定义的反馈。我们称其为 \( v_{s,S} \)。我们考虑相应受控马尔可夫链的不变测度。我们称其为 \( m_{s,S}(dx) \)，参见 (9.2.82)

(10.2.51) \[
m_{s,S}(dx) = \frac{\exp^{-\beta s}}{1 + \beta(S - s)}\delta(x - s) + \frac{\beta \exp^{-\beta(x - s)}}{1 + \beta(S - s)} dx.
\]

让我们记 \( l_{s,S}(x) = l(x, v_{s,S}(x)) \)。我们容易验证公式

(10.2.52) \[
l_{s,S}(x) = (K - (p - c)(S - x))\mathbb{1}_{x \le s} + pD + (h - p)x
\]

(10.2.53) \[
+ p\mathbb{1}_{x > E}(x - D)^+ + p\mathbb{1}_{x \le s} E(S - D)^+.
\]

该公式是通用的，并不仅限于指数分布的特殊情况。我们接着计算 ergodic 成本

\[
J_{s,S} = \int_0^s l_{s,S}(x)m_{s,S}(dx).
\]

利用不变测度的性质，在积分关系 (10.2.52) 的最后部分时，我们得到

(10.2.54) \[
J_{s,S} = pD + (K - (p - c)S) \int_0^s m_{s,S}(dx) + (p - c) \int_0^\infty x m_{s,S}(dx) + h \int_0^\infty x m_{s,S}(dx).




我们现在使用特殊情况，其中不变量由 (10.2.51) 给出，且 \(\bar{D} = \frac{1}{\beta}\)。经过一些冗长但简单的计算后，我们得到公式

\[
J_{s,S} = \frac{c - \frac{h}{2}}{\beta} + \frac{K + \frac{p - c + h}{\beta} \exp -\beta s - \frac{h}{2\beta}}{1 + \beta(S - s)} + h\left(\frac{1}{2}(S - s) + s\right).
\]

我们现在可以尝试在两个参数 \(s, S - s\) 上最小化这个表达式。我们首先固定 \(s\) 并在 \(S - s\) 上最小化。我们得到条件

\[
\frac{K + \frac{p - c + h}{\beta} \exp -\beta s - \frac{h}{2\beta}}{(1 + \beta(S - s))^2} = \frac{h}{2\beta^2},
\]

这定义了 \(S(s)\)。然后我们可以计算 \(J_s = J_{s,S(s)}\)。我们得到简单表达式

\[
J_s = \frac{c}{\beta} + hS(s).
\]

由于我们要最小化 \(J_s\)，我们找到使 \(S'(s) = 0\) 的 \(s\)。现在将 (10.2.56) 写成

\[
(1 + \beta(S - s))^2 = \frac{2\beta}{h} K + 2 \frac{p - c + h}{h} \exp -\beta s - 1.
\]

我们对这个表达式关于 \(s\) 求导，并考虑到 \(S'(s) = 0\)。我们很容易检查这意味着

\[
1 + \beta(S - s) = \frac{p - c + h}{h} \exp -\beta s,
\]

这正是 (10.2.46)。在 (10.2.56) 中使用此关系并整理后，我们得到

\[
K = \frac{h\beta}{2}(S - s)^2,
\]

这正是 (10.2.49)。因此，数 \(\rho\) 是所有可能的 \(s, S\) 策略下的循环成本的最小值。

## 10.3. 带固定成本和积压的循环库存控制

### 10.3.1. 问题陈述。

我们考虑 Bellman 方程

\[
u_\alpha(x) = -cx + hx^+ + px^- + \inf_{\eta \ge x} \{ K \mathbf{1}_{\eta > x} + c\eta + \alpha E u_\alpha(\eta - D) \},
\]

在 9.3 节中研究过。定义

\[
g_\alpha(x) = c(1 - \alpha) + \alpha cD + \alpha h E(x - D)^+ + \alpha p E(x - D)^-,
\]

和

\[
\mu_\alpha(x) = g'_\alpha(x) = c(1 - \alpha) + \alpha h - \alpha(h + p)\bar{F}(x).
\]

那么

\[
H_{\alpha,s}(x) = \int_s^x \Gamma_\alpha(x - \xi) \mu_\alpha(\xi) \,d\xi,
\]

其中 \(\Gamma_\alpha(x)\) 是更新方程的解

(10.3.5)
\[
\Gamma_\alpha(x) = 1 + \alpha \int_0^x f(x-\xi)\Gamma_\alpha(\xi)\,d\xi.
\]

我们定义函数 \(S_\alpha(s)\) 使得

(10.3.6)
\[
\inf_{\eta \ge s} H_{\alpha,s}(\eta) = H_{\alpha,s}(S_\alpha(s)),
\]

而对 \(s_\alpha, S_\alpha\) 由关系定义

(10.3.7)
\[
\inf_{\eta \ge s_\alpha} H_{\alpha,s_\alpha}(\eta) + K = 0, \quad S_\alpha = S_\alpha(s_\alpha).
\]

我们知道

(10.3.8)
\[
s_\alpha \le \bar{s}_\alpha,
\]

其中

(10.3.9)
\[
c(1-\alpha) + ch - \alpha(p+h)\bar{F}(\bar{s}_\alpha) = 0.
\]

那么

(10.3.10)
\[
u_\alpha(x) = H_{\alpha,s_\alpha}(x) - cx + hx^+ + px^- + \frac{g_\alpha(s_\alpha)}{1-\alpha}.
\]

我们想要研究当 \(\alpha \uparrow 1\) 时 \(u_\alpha(x)\) 的行为。

### 10.3.2. 收敛性。

我们做如下假设

(10.3.11)
\[
f(x) \text{ is continuous, } f(x) > 0, \forall x.
\]

我们回顾 \(D = \int_0^{+\infty} x f(x) \,dx < \infty\)。另外 \(F(x) < 1, \forall x.\)

函数 \(\Gamma_\alpha(x)\) 收敛到 \(\Gamma(x)\)，其中

(10.3.12)
\[
\Gamma(x) = 1 + \int_0^x f(x-\xi)\Gamma(\xi)\,d\xi.
\]

接下来我们有

(10.3.13)
\[
\mu_\alpha(x) \to \mu(x) = h - (p+h)F(x).
\]

类似地

(10.3.14)
\[
g_\alpha(x) \to g(x) = cD + hE(x-D)^+ + pE(x-D)^-.
\]

函数

(10.3.15)
\[
H_{\alpha,s}(x) \to H_s(x) = \int_s^x \Gamma(x-\xi)\mu(\xi)\,d\xi.
\]

我们可以定义 \(\bar{s} > 0\) 使得 \(\mu(\bar{s}) = 0\) 且 \(\mu(x) < 0, \forall x < \bar{s}\) 以及 \(\mu(x) > 0, \forall x > \bar{s}\)。由于 \(\Gamma\) 是递增函数，函数 \(H_s(x)\) 在 \(x\) 上递增，只要 \(s \ge \bar{s}\)。因此我们可以断言

\[
S(s) = s, \quad \inf_{\eta \ge s} H_s(\eta) = 0, \text{ if } s \ge \bar{s}.
\]

因此我们将可能的 \(s\) 集合限制为满足 \(s < \bar{s}\)。

### 引理 10.3.

对于 \(s < \bar{s}\)，\(H_s(x)\) 在 \(x \ge s\) 上的下确界在严格大于 \(\bar{s}\) 的点处取得。而且 \(\inf_{x \ge s} H_s(x) < 0\)。

证明。我们不能像在引理 10.1 中那样论证。原因是我们不再有由 \(S_\alpha(0)\) 提供的先验界。其对应物将是 \(S_\alpha(-\infty)\)。然而，从公式 (9.3.24) 我们可以看出，当 \(\alpha \uparrow 1\) 时 \(S_\alpha(-\infty)\) 不是有界的。我们将改为依赖于估计

(10.3.16)
\[
1 + B_1 x \le \Gamma(x) \le 1 + B_2 x, \quad B_2 = \sup_{x \ge 0} \frac{F(x)}{\int_0^x F(\xi) \,d\xi}, \quad B_1 = \inf_{x \ge 0} \frac{F(x)}{\int_0^x F(\xi) \,d\xi}.
\]

请注意数 \(B_1, B_2\) 是定义良好的。确实，函数 \(G(x) = \frac{F(x)}{\int_0^x F(\xi) \,d\xi}\) 当 \(x \to 0\) 时收敛到 \(f(0) > 0\)，当 \(x \to \infty\) 时收敛到 \(\frac{1}{D}\)。而且它是连续的。记

\[
z(x) = \Gamma(x) - 1 - Bx,
\]

那么 \(z\) 是下式的解

\[
z(x) = F(x) - B \int_0^x F(\xi) \,d\xi + \int_0^x z(x - \xi) f(\xi) \,d\xi.
\]

如果 \(F(x) - B \int_0^x F(\xi) \,d\xi \le 0\)，则函数 \(z(x)\) 也为负。类似地，如果 \(F(x) - B \int_0^x F(\xi) \,d\xi \ge 0\)，则它为正。估计 (10.3.16) 很容易得出。接下来我们表示

\[
\begin{aligned}
H_s(x) &= \int_s^x \Gamma(x - \xi) \mu(\xi) \,d\xi \\
&= h \int_s^x \Gamma(x - \xi) \,d\xi - (p + h) \int_s^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi.
\end{aligned}
\]

如果 \(s > 0\)，我们得到

\[
H_s(x) \ge h \int_s^x \Gamma(x - \xi) \,d\xi - (p + h) \int_0^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi.
\]

然而

(10.3.17)
\[
\int_0^x \Gamma(x - \xi) \bar{F}(\xi) \,d\xi = x,
\]

这可以通过对左边求导并显示导数为 1 来简单看出。因此，由 (10.3.16) 和 (10.3.17)，

\[
\begin{aligned}
H_s(x) &\ge h(x - s) + \frac{h B_1}{2} (x - s)^2 - (p + h) x \\
&= \frac{h B_1}{2} (x - s)^2 - p x - h s, \quad x > s > 0.
\end{aligned}
\]

(10.3.18)

现在如果 \(s < 0\)，我们有

\[
H_s(x) = -p \int_0^x \Gamma(x - \xi) \,d\xi + h \int_0^x \Gamma(x - \xi) \,d\xi - (p + h) x,
\]

并且使用 (10.3.16) 我们很容易得到

(10.3.19)
\[
H_s(x) \ge p s + \frac{B_2}{2} (-s^2 + 2sx) - p x + h \frac{B_1}{2} x^2, \quad s < 0 < x.
\]

因此，在两种情况下，当 \(x \uparrow \infty\) 时 \(H_s(x) \to \infty\)。另外 \(H'_s(s+) = \mu(s) < 0\)。因此函数 \(H_s(x)\) 在 \((s, \infty)\) 上取得一个负最小值。如果有多个，我们称 \(S(s)\) 为最小的最小值。

我们有

\[
H'_s(S(s)) = 0.
\]

接下来我们有

\[
\frac{d}{ds}H_s(S(s)) = \frac{\partial}{\partial s}H_s(s)\big|_{S(s)} = -\Gamma(S(s) - s)\mu(s) > 0.
\]

而且 \( S(s) > s > 0 \)。对于 \( s < 0, x > 0 \) 我们有

(10.3.20)
\[
H_s(x) = -p \int_0^x \Gamma(x - \xi) \,d\xi + h \int_0^x \Gamma(\xi) \,d\xi - (p + h)x, \quad \forall s < 0 < x.
\]

由此可得

\[
H'_s(x) = (p + h)\Gamma(x) - p\Gamma(x - s) - (p + h),
\]

因此 \( S(s) \) 是方程的解

(10.3.21)
\[
(p + h)\Gamma(S) - p\Gamma(S - s) - (p + h) = 0.
\]

由此可知，当 \( s \to -\infty \) 时，\( S(s) \to +\infty \)。否则，将与 (10.3.21) 矛盾。此外，对于 \( s > 0 \) 我们有

\[
H_s(S(s)) \le H_s(0) = -p \int_0^\infty \Gamma(\xi) \,d\xi \le ps,
\]

由此可知，当 \( s \to -\infty \) 时，\( H_s(S(s)) \to -\infty \)。

因此，函数 \( \inf_{y \ge s} H_s(y) \) 从 \(-\infty\) 增加到 0，当 \( s \) 从 \(-\infty\) 增加到 \(\bar{s}\) 时。因此存在一个唯一的 \( s\) 使其等于 \(-K\)。我们可以通过求解代数方程组来找到对 \(s, S\)

(10.3.22)
\[
\begin{aligned}
\Gamma(S - s)\mu(s) + \int_s^S \Gamma(S - \xi)\mu'(d\xi) &= 0 \\
\int_s^S \Gamma(S - \xi)\mu(d\xi) &= -K
\end{aligned}
\]

### 定理 10.5.

我们假设 \( h < c \) 和 (10.3.11)，那么我们有

(10.3.23)
\[
s_\alpha \to s, \quad S_\alpha \to S,
\]

其中对 \(s, S\) 是 (10.3.22) 的解。令 \( H(x) = H_s(x) \)。那么

(10.3.24)
\[
u_\alpha(x) - \frac{g_\alpha(s_\alpha)}{1 - \alpha} \to u(x) = H(x) - cx + hx^+ + px^-.
\]

令 \( \rho = g(s) \)，那么 \( \rho > 0 \) 并且有

(10.3.25)
\[
u(x) + \rho = -cx + hx^+ + px^- + \inf_{\eta \ge x} \{K \mathbf{1}_{\eta > x} + c\eta + Eu(\eta - D)\}.
\]

证明。让我们检查 \( s_\alpha \) 是有界的。由于 \( s_\alpha < \bar{s} \)，足以假设 \( s_\alpha < 0 \)。我们有 \( S_\alpha > 0 \)。我们可以写

\[
-K = H_{\alpha, s_\alpha}(S_\alpha) \le H_{\alpha, s_\alpha}(0)
\]
\[
= (c(1 - \alpha) - \alpha p) \int_{s_\alpha}^0 \Gamma_\alpha(-\xi) \,d\xi \le -s_\alpha(c(1 - \alpha) - \alpha p)
\]

这意味着

\[
s_\alpha^- \le \frac{K}{\alpha p - c(1 - \alpha)},
\]

因此 \( s_\alpha \) 保持有界。但是，然后，使用估计 (10.3.18)、(10.3.19) 我们立即得到 \( S_\alpha \) 也保持有界。因此我们可以提取一个子序列


收敛于 \(s^*, S^*\)。由 \(H_{\alpha, s_\alpha}(x)\) 的表达式，我们很容易推导出 \(H_{\alpha, s_\alpha}(S_\alpha) = -K \to H_\alpha(S^*)\)。由此可得 \(s^* = s, S^* = S\)，为方程 (10.3.22) 的解。值 \(s\) 唯一确定，且由于 \(S_\alpha\) 是最小下确界，我们也得到 \(S\) 是最小极小值。

请注意

\(g(x) = cD + hE(x-D)^+ + pE(x-D)^-,\)

所以它是一个正函数。故 \(\rho > 0\)。显然

\((1-\alpha)u_\alpha(x) - g_\alpha(s_\alpha) \to 0, \text{当 } \alpha \uparrow 1,\)

故

\((1-\alpha)u_\alpha(x) \to \rho = g(s).\)

我们还记得我们也有

\(H(x) + \rho = g(x) + EH(x-D), \forall x \ge s\)
\(H(x) = 0, \forall x \le s\)

其中 \(H(x) = H_s(x)\)，由 (10.3.15) 定义，针对特定的 \(s\)，即 \(s_\alpha\) 的极限。

我们可以检查这些条件可以总结为

(10.3.26) \(H(x) + \rho = \inf_{\eta \ge x} [K 1_{\eta > x} + g(\eta) + EH(\eta - D)].\)

如果 (10.3.26) 成立，则利用 \(g(x)\) 的定义，关于 \(u\) 的方程 (10.3.25) 立即得出。

(10.3.26) 的证明与定理 10.2 中 (10.2.25) 的证明相同。

这完成了定理的证明。

## 10.3.3. 概率解释。

我们现在给出 \(\rho\) 以及 (10.3.25) 的解 \(u(x)\) 的解释。我们首先将一个 \(s, S\) 策略与一个不变测度 \(m_{s,S}(dx)\) 关联起来。而且，方程 (10.3.25)、(10.3.26) 中的下确界由一个与 \(s, S\) 策略关联的反馈 \(\hat{v}(x)\) 取得。为了节省符号，我们仍将其记作 \(s, S\)。

我们记得

(10.3.27) \(l(x, v) = K 1_{x > 0} + cv + hx^+ + px^-,\)

和

(10.3.28) \(l(x, \hat{v}(x)) = 1_{x \le s} (K + c(S-x)) + hx^+ + px^-,\)

且 (10.3.25) 读作

(10.3.29) \(u(x) = l(x, \hat{v}(x)) - \rho + Eu(x + \hat{v}(x) - D).\)

我们记 \(m_{l(\cdot)}(\text{d}x)\) 为不变测度 \(m_{s,S}(\text{d}x)\)，以符号保持一致。由 (10.3.29) 可得

(10.3.30) \(\rho = \int l(x, \hat{v}(x)) m_{l(\cdot)}(\text{d}x).\)

请注意，\(m_{l(\cdot)}(\text{d}x)\) 的状态空间是 \((-\infty, S]\)，但可以取为 \((-\infty, \infty)\) 以便使用固定的状态空间（与 \(S\) 无关）。我们接下来定义反馈集合 \(\mathcal{U}_b\)，使得

(10.3.31) \(\mathcal{U}_b = \{v(\cdot) \ge 0 \mid \exists M \text{ 使得 } -M \le x + v(x) \le \max(x, M)\}.\)

若 \(v(\cdot) \in \mathcal{U}_b\)，则必然在 \(x \ge M\) 时有 \(v(x) = 0\)。由反馈 \(v(\cdot)\) 控制的马尔可夫链在状态空间 \((-\infty, M]\) 上是遍历的。确实，转移概率为

\(\pi(x, dy) = \mathbf{1}_{y < x + v(x)} f(x + v(x) - \eta) d\eta\)。

若取 \(X_0 = [-M-2, -M-1]\)，则对于 \(\eta \in X_0\)，有

\(\mathbf{1}_{y < x + v(x)} f(x + v(x) - \eta) \ge \inf_{y \in [1, 2+M]} f(y) > 0\)。

我们将相应的不变测度记为 \(m_{v(\cdot)}(dx)\)。请注意，由 \(s, S\) 策略定义的反馈属于 \(\mathcal{U}_b\)。我们于是有

### 定理 10.6. 我们采用定理 10.5 的假设。我们有

(10.3.32) \(\rho = \inf_{v(\cdot) \in \mathcal{U}_b} \int l(x, v(x)) m_{v(\cdot)}(dx),\)

并且存在一个由 \(s, S\) 策略定义的最优反馈 \(v(\cdot)\)。这个 \(s, S\) 策略已在定理 10.5 中定义。

**证明。** 考虑一个在 \(\mathcal{U}_b\) 中的反馈 \(v(\cdot)\)。由 (10.3.25) 可得

(10.3.33) \(u(x) + \rho \le l(x, v(x)) + E u(x + v(x) - D)\)。

对不变测度 \(m_{v(\cdot)}(dx)\) 进行积分得

\(\rho \le \int l(x, v(x)) m_{v(\cdot)}(dx)\)。

该积分有限。确实，有

\(\int |x| m_{v(\cdot)}(dx) = \int E |x + v(x) - D| m_{v(\cdot)}(dx) \le M + D\)。

由于

\(l(x, v(x)) = K \mathbf{1}_{x > 0} + c|x + v(x)| - cx + hx^+ + px^-,\)

它对 \(m_{v(\cdot)}(dx)\) 有有限积分。回顾还有

\(u(x) = H(x) - cx + hx^+ + px^-,\)

并注意到

\(\int |H(x)| m_{v(\cdot)}(dx) = \int_s^M |H(x)| m_{v(\cdot)}(dx) < \infty\),

我们也看到 \(|u(\cdot)|\) 对 \(m_{v(\cdot)}(dx)\) 是可积的。

考虑到 (10.3.30)，结果立即得出。

### 注 10.3. 令 \(J_{\alpha, x}(v(\cdot))\) 为受控马尔可夫链的折扣系数 \(\alpha\) 的成本泛函，控制由属于 \(\mathcal{U}_b\) 的反馈 \(v(\cdot)\) 定义。根据遍历理论，我们可以断言

(10.3.34) \((1 - \alpha) J_{\alpha, x}(v(\cdot)) \to \int l(\xi, v(\xi)) m_{v(\cdot)}(d\xi)\)。

因此我们也有

(10.3.35) \(\rho = \inf_{v(\cdot) \in \mathcal{U}_b} \lim_{\alpha \to 1} (1 - \alpha) J_{\alpha, x}(v(\cdot))\)。

我们还给出函数 \(u(x)\) 的解释。我们选取一个在 \(\mathcal{U}_b\) 中的反馈。我们记 \(y_n, v_n\) 为相应的轨迹，其中

\(y_{n+1} = y_n + v_n - D_n \quad v_n = v(y_n); \quad y_1 = x\)

### 引理 10.4. 我们有性质

(10.3.36) \( Eu(y_n) \to \int u(x)m_{v(\cdot)}(dx). \)

**证明。** 该积分定义良好，如在定理 10.6 的证明中所见。然而，我们不能像引理 10.2 的证明那样进行，因为 \( y_n \) 不保持在紧区间内。然而我们有

(10.3.37) \( E\varphi(y_n) \to \int \varphi(x)m_{v(\cdot)}(dx), \)

对于任何在状态空间 \((-\infty, M]\) 上连续且有界的函数 \( \varphi(x) \)。这如同在引理 10.2 中完成，使用遍历理论和处理初始值 \( x > M \) 情况的程序。回顾

\( u(x) = H(x) - cx + hx^+ + px^-,\)

并注意到 \( H(x) \) 在 \((-\infty, M]\) 上是连续且有界的，仍需证明性质 (10.3.37) 对于 \( \varphi(x) = x^+ \) 或 \( x^- \) 成立。对于 \( x^+ \) 这立即成立，因为它在 \((-\infty, M]\) 上是连续且有界的。对于 \( x^- \)，人们注意到

\( Ey_{n+1}^- = EG(y_n),\)

其中

\( G(x) = E(x + v(x) - D)^-,\)

并且人们注意到

\( G(x) \le M + \bar{D},\)

因此它是连续且有界的。证明已完成。

让我们考虑一个反馈 \( v(\cdot) \in \mathcal{U}_b \) 并考虑 \( y_n, v_n \) 的相应轨迹

定义

(10.3.38) \( J_\pi^n(v(\cdot)) = \sum_{j=1}^n E(l(y_j, v_j)) - n\rho. \)

我们然后断言

### 定理 10.7. 我们采用定理 10.5 的假设。那么 \( J_\pi^n(\hat{v}(\cdot)) \) 在 \( n \to \infty \) 时有极限，并且

(10.3.39) \( u(x) = \lim_{n \to \infty} J_\pi^n(\hat{v}(\cdot)) + \int u(x)m_{v(\cdot)}(dx). \)

此外，对于 \( v(\cdot) \in \mathcal{U}_b \)，\( J_\pi^n(v(\cdot)) \) 下有界，并且有

(10.3.40) \( u(x) = \inf_{v(\cdot) \in \mathcal{U}_b} \left[ \liminf_{n \to \infty} J_\pi^n(v(\cdot)) + \int u(x)m_{v(\cdot)}(dx) \right]. \)

**证明。** 证明与定理 10.4 的证明相同。

## 10.3.4. 特殊情况。

我们考虑指数分布 \(f(x) = \beta \exp -\beta x\) 的特殊情况。我们记得 \(\Gamma(x) = 1 + \beta x\)。

接下来我们有

(10.3.41) 
\(\mu(x) = h - (p + h) \exp -\beta x^+,\)

和

(10.3.42) 
\(g(x) = hx^+ + px^- + (c + p)D - \frac{p+h}{\beta}(1 - \exp -\beta x^+).\)

我们接下来计算函数 \(H(x)\)，对于 \(x > s\)。我们使用公式

\(H'(x) = \begin{cases} -p\Gamma(x - s), & \text{当 } x < 0 \\ -p\Gamma(x - s) + (p + h)(\Gamma(x) - 1), & \text{当 } s < 0 < x \\ h\Gamma(x - s) - (p + h)F(x) - (p + h) \int_s^x \Gamma'(x - \xi)F(\xi)d\xi & \text{当 } 0 < s < x \end{cases}\)

因此

\(H'(x) = \begin{cases} -p(1 + \beta(x - s)), & \text{当 } x < 0 \\ -p(1 + \beta(x - s)) + (p + h)\beta x, & \text{当 } s < 0 < x \\ h(1 + \beta(x - s)) - (p + h) \exp -\beta s & \text{当 } 0 < s < x \end{cases}\)

我们然后得到，对于 \(x > s\)

(10.3.43) 
\(H(x) = -p \left( x - s + \frac{\beta}{2}(x - s)^2 \right) + (h + p) \left[ (x - s^+)^+ (1 - \exp -\beta s^+) + \frac{\beta}{2}(x^+ - s^+)^2 \right].\)

数 \(\bar{s}\) 满足 \(\mu(\bar{s})=0\)，因此

(10.3.44) 
\(\exp -\beta \bar{s} = \frac{h}{p + h}.\)

我们因此考虑 \(s \le \bar{s}\)。我们通过 \(H'(S) = 0\) 定义 \(S(s)\)，因此

(10.3.45) 
\(S(s) = \frac{p\beta s^- - h(1 - \beta s^+) + (h + p) \exp -\beta s^+}{h\beta}.\)

我们可以看到 \(S(\bar{s}) = \bar{s}\)，并且 \(S(s)\) 在 \(s \le \bar{s}\) 时是递减的。此外 \(S(-\infty) = +\infty\)。

我们接下来定义 \(s\) 的值。我们首先得到公式

(10.3.46) 
\(H_s(S(s)) = - \frac{1}{2h\beta} [ (h + p) \exp -\beta s^+ - h ]^2 - \frac{\beta p}{2h} (p + h)(s^-)^2 - \frac{p(p + h)}{h} s^-.\)

我们可以直接在这个公式上检查，当 \(s\) 从 \(-\infty\) 增长到 \(\bar{s}\) 时，\(H_s(S(s))\) 从 \(-\infty\) 增加到 0。因此存在一个唯一的 \(s\) 使得 \(H_s(S(s)) = -K\)。

### 练习 10.1. 检查

(10.3.47) 
\(K < \frac{p^2}{2h\beta} \implies (p + h) \exp -\beta s = h + \sqrt{2h\beta K}, s > 0,\)

并且对于 \(K > \frac{p^2}{2h\beta}\)，\(s\) 是下式的负根

(10.3.48) 
\(\frac{s^2\beta(p + h)}{2h} - \frac{sp(p + h)}{h} + \frac{p^2}{2h\beta} - K = 0.\)




我们接下来可以得到数 \(\rho = g(s)\)。首先，由 (10.3.46) 得，

\((h+p)\exp -\beta s^+ = h + \sqrt{2h\beta} \sqrt{K - \frac{p(p+h)}{h}s^- \left(1 + \beta \frac{s^-}{2}\right)},\)

然后利用 (10.3.42)，我们得到

(10.3.49) \(\rho = hs^+ + ps^- + \frac{c}{\beta} + \frac{\sqrt{2h\beta}}{\beta} \sqrt{K - \frac{p(p+h)}{h}s^- \left(1 + \beta \frac{s^-}{2}\right)},\)

利用 S 的公式，我们再次得到 (10.2.50)，即

(10.3.50) \(\rho = \frac{c}{\beta} + hS.\)

让我们通过概率解释（定理 10.6）来恢复这个公式。我们将只考虑 s,S 策略。

因此，考虑由 s,S 策略定义的反馈。我们称其为 \(v_{s,S}\)。我们考虑相应受控马尔可夫链的不变量度。我们称其为 \(m_{s,S}(dx)\)，参见 (9.3.45)

(10.3.51) \(m_{s,S}(dx) = \frac{\beta \exp -\beta(x-s)^-}{1 + \beta(S-s)} dx.\)

令 \(l_{s,S}(x) = l(x, v_{s,S}(x))\)。我们回顾公式 (10.3.28) 并计算 ergodic 成本

\(J_{s,S} = \int_0^S l_{s,S}(x)m_{s,S}(dx).\)

我们得到

(10.3.52) \(J_{s,S} = K \int_0^{s^+} m_{s,S}(dx) + c \int_0^S (S-x)m_{s,S}(dx) + h \int_0^S x m_{s,S}(dx) - p \int_{-\infty}^0 x m_{s,S}(dx).\)

利用 (10.3.51) 给出的不变量度，我们得到公式

(10.3.53) \(J_{s,S} = \frac{c}{\beta} + \frac{K - \frac{h}{\beta} + \frac{h+p}{\beta}\exp -\beta s^+ + h\beta \frac{S^2}{2} + hs^+ + ps^- + \frac{p\beta}{2}(s^-)^2 - \frac{h\beta}{2}(s^+)^2}{1 + \beta(S-s)}.\)

现在我们可以尝试在两个参数 s, S - s 中最小化这个表达式。我们首先固定 s 并在 S 中最小化。我们得到条件

(10.3.54) \(\frac{K - \frac{h}{\beta} + \frac{h+p}{\beta}\exp -\beta s^+ + h\beta \frac{S^2}{2} + hs^+ + ps^- + \frac{p\beta}{2}(s^-)^2 - \frac{h\beta}{2}(s^+)^2}{1 + \beta(S-s)} = hS,\)

这定义了 S(s)。然后我们可以计算 \(J_s = J_{s,S(s)}\)。我们得到简单的表达式

(10.3.55) \(J_s = \frac{c}{\beta} + hS(s).\)

由于我们想最小化 $J_s$，我们找到使 $S'(s) = 0$ 的 $s$。现在将 (10.3.54) 写为

(10.3.56) \(K - \frac{h}{\beta} + \frac{h+p}{\beta} \exp -\beta s^+ - h\beta \frac{S^2}{2} + hs^+ + ps^- + \frac{p\beta}{2}(s^-)^2 - \frac{h\beta}{2}(s^+)^2 - hS + h\beta Ss = 0.\)

我们对 $s$ 对这个表达式求导，并考虑到 $S'(s) = 0$。我们很容易检查这意味着

\(h\beta S = -h + \beta(hs^+ + ps^-) + (h+p)\exp -\beta s^+,\)

这正是 (10.3.45)。在 (10.3.56) 中使用此关系并重新排列，我们得到

\(K - \frac{1}{2h\beta}[(h+p)\exp -\beta s^+ - h]^2 - \frac{\beta p}{2h}(p+h)(s^-)^2 - \frac{p(p+h)}{h}s^- = 0,\)

这等于 $H_s(S(s)) = -K$。因此，数 $\rho$ 是在所有可能的 s,S 策略中 ergodic 成本的最小值。

本页故意留空

# 带扩展的动态库存模型

## 11.1. 带产能的库存管理

我们考虑动态库存模型，没有设置成本，参见第 5 章。为了明确概念，我们只研究有积压的情况，参见第 5.2 节。通过带产能的库存管理，我们指的是订单大小有限制。因此，如果 x 表示订单前的库存，\(\eta\) 表示订单后的库存，那么我们有约束

\(x \le \eta \le x + Q,\)

其中 \(Q\) 表示订单大小的上限。我们改编 Bellman 方程 (5.2.5)，如下

(11.1.1) \(u(x) = \inf_{0 \le v \le Q} [l(x, v) + \alpha Eu(x + v - D)],\)

其中

(11.1.2) \(l(x, v) = hx^+ + px^- + cv,\)

所以

(11.1.3) \(u(x) = hx^+ + px^- - cx + \inf_{x \le \eta \le x + Q} [c\eta + \alpha Eu(\eta - D)].\)

我们首先陈述

**定理 11.1。** 在假设 (11.1.2) 下，(11.1.1) 在空间 \(B_1\) 中的解是唯一的。而且 \(u\) 是连续的。存在一个最优反馈 \(\tilde{v}(x, Q)\)。

**证明。** 证明与定理 5.5 类似，甚至更简单，因为控制 \(v\) 是有界的。我们省略细节。\(\square\)

我们想研究相对于基础库存策略的修改。让我们用 \(u(x, Q)\) 表示 (11.1.1) 的解。我们陈述

**定理 11.2。** 假设，

(11.1.4) \(c(1 - \alpha) - p\alpha < 0, \quad f(x) \text{ continuous, bounded.}\)

(11.1.1) 的解 \(u(x, Q)\) 在 \(x\) 中是凸的，\(C^1\)，除了在 0 处，它有左导数和右导数，并且当 \(|x| \to \infty\) 时 \(u(x, Q) \to \infty\)。令

(11.1.5) \(G(Q, x) = cx + \alpha Eu(x - D, Q).\)

那么 G(x, Q) 是凸的，C^1，且当 |x| \to +\infty 时 G(x, Q) \to +\infty。令 S(Q) 为 G(x, Q) 的最小值，则反馈 v(x, Q) 由公式给出

(11.1.6) \(\hat{v}(x, Q) = \begin{cases} Q, & \text{if } x < S(Q) - Q \\ S(Q) - x, & \text{if } S(Q) - Q < x < S(Q) \\ 0, & \text{if } x > S(Q) \end{cases}\)

S(Q) 在 Q 中是递减的且严格为正。导数 u'_n(x, Q) 在 Q 中递增，除了在 0 处。在 0 处，该性质适用于左导数和右导数。

**证明。** 我们考虑单调递增过程 u_n(x)。我们从 u_0(x) = 0, u_1(x, Q) = hx^+ + px^- 开始

(11.1.7) \(u_{n+1}(x, Q) = hx^+ + px^- - cx + \inf_{\{t \le x \le t+Q\}} [cy + \alpha E u_n(\eta - D, Q)].\)

如我们在 Q = +\infty 的情况中所见，参见第 5 章，第 5.2 节，对于 1 \le n \le n_0 + 1 且

\(\frac{\alpha p}{1-\alpha}(1 - \alpha^{n_0+1}) > c \ge \frac{\alpha p}{1-\alpha}(1 - \alpha^{n_0}),\)

我们有 u_n(x, Q) = u_n(x)，其中

(11.1.8) \(u_{n+1}(x) = hx^+ + px^- + \alpha E u_n(x - D), 0 \le n \le n_0.\)

当 n_0 = 0 时这很明显，这对应于 \alpha p > c。所以我们可以假设 c \ge \alpha p。我们有 n_0 \ge 1。

由序列 (11.1.8) 定义的函数 u_n(x) 是凸的，并且

\(u'_n(x) = -p \frac{1-\alpha^n}{1-\alpha}, x < 0, 1 \le n \le n_0 + 1,\)

因此

\(G_n(x) = cx + \alpha E u_n(x - D),\)

对于 0 \le n \le n_0，这也是凸的且单调递增。注意 G_n(x) 是 C^1，因为

\(G'_n(x) = c + \alpha \int_{-\infty}^x u'_n(z) (x-z) dz,\)

并且

\(G'_n(x) = c - \alpha p \frac{1-\alpha^n}{1-\alpha} \ge 0, \forall x \le 0, 0 \le n \le n_0\)

由此可知 u_n(x) 满足 (11.1.7)，因此 u_n(x, Q) = u_n(x)，\forall 1 \le n \le n_0 + 1。显然当 |x| \to +\infty 时 u_n(x) \to +\infty，并且 u_n(x) 除了在 0 处外是 C^1。有

\(u'_n(0+) = h - \alpha p \frac{1-\alpha^{n-1}}{1-\alpha}, 1 \le n \le n_0 + 1\)

现在考虑 u_{n_0+2}(x, Q)。注意

\(G'_{n_0+1}(x) = c - \alpha p \frac{1-\alpha^{n_0+1}}{1-\alpha}, x \le 0\)

因此，对于 x 为负，函数 G_{n_0+1}(x) 严格递减，并且当 x \to +\infty 时趋于 +\infty。因此它有一个最小值。

而且最小值是严格为正的。取最小的最小值，我们以唯一方式定义它并称其为 \(S_{n_0+1}\)。我们有

\(u_{n_0+2}(x, Q) = \begin{cases} hx^+ + px^- - cx + G_{n_0+1}(x+Q), & \text{if } x < S_{n_0+1} - Q \\ hx^+ + px^- - cx + G_{n_0+1}(S_{n_0+1}), & \text{if } S_{n_0+1} - Q < x < S_{n_0+1} \\ hx^+ + px^- - cx + G_{n_0+1}(x) & \text{if } x > S_{n_0+1} \end{cases}\)

我们首先看到这个函数是凸的。这源于性质

\(g_{n_0+1}(x) = \inf_{-x \le y \le x+Q} G_{n_0+1}(y), \quad (11.1.9)\)

是凸的，因为 \(G_{n_0+1}(x)\) 是凸的。该函数显然是连续的。它除了在 0 处外是 \(C^1\)。而且当 \(|x| \to +\infty\) 时 \(G_{n_0+1}(x) \to +\infty\)，并且当 \(|x| \to +\infty\) 时 \(u_{n_0+2}(x, Q) \to +\infty\)。我们还可以检查 \(u_{n_0+2}(x, Q)\) 在 \(Q\) 中是单调递增的，\(\forall x \neq 0\)，在 0 处的左导数和右导数也是如此。那么

\(G_{n_0+2}(x, Q) = cx + \alpha E u_{n_0+2}(x - D, Q),\)

是凸的，\(C^1\) 并且

\(G_{n_0+2}(x, Q) \ge cx + \alpha[hE(x-D)^+ + pE(x-D)^- - c(x-D)] \ge |c(1-\alpha) - \alpha p|x \to +\infty, \text{as } x \to +\infty\)

所以当 \(|x| \to +\infty\) 时 \(G_{n_0+2}(x, Q) \to +\infty\)。而且 \(G'_{n_0+2}(x, Q)\) 在 \(Q\) 中是单调递增的。此外，对于 \(x < 0\)，从上面的 \(u_{n_0+2}(x, Q)\) 表达式我们有 \(u'_{n_0+2}(x, Q) \le -p - c\)，因此

\(G'_{n_0+2}(x, Q) \le c(1-\alpha) - \alpha p < 0, \forall x \le 0\)

因此 \(G_{n_0+2}(x, Q)\) 在一点 \(S_{n_0+2}(Q) > 0\) 处取得其最小值。通过取最小的最小值，可以以唯一方式定义 \(S_{n_0+2}(Q)\)。函数 \(S_{n_0+2}(Q)\) 是单调递减的。确实，如果 \(Q_1 \le Q_2\)，则写

\(G'_{n_0+2}(S_{n_0+2}(Q_1), Q_1) = G'_{n_0+2}(S_{n_0+2}(Q_2), Q_2) = 0,\)

因此

\(G'_{n_0+2}(S_{n_0+2}(Q_1), Q_2) \ge 0,\)

由此可得 \(S_{n_0+2}(Q_1) \ge S_{n_0+2}(Q_2)\)。我们现在假设，对于 \(n \ge n_0 + 2\)，有

\(u_n(x, Q)\) 是凸的 \(C^1\)，除了 \(x=0\)，\(u'_n(x, Q)\) 在 \(Q\) 中递增，\(\forall x \neq 0\)，当 \(|x| \to +\infty\) 时 \(u_n(x, Q) \to +\infty\)

在 0 处，\(u'_n(x, Q)\) 有左极限和右极限，且两个极限在 \(Q\) 中递增。我们还假设

\(u'_n(x, Q) \le -c - p, \forall x < 0.\)

函数

\(G_n(x, Q) = cx + \alpha E u_n(x - D),\)

是凸的，\(C^1\) 并且

\(G_n(x, Q) \ge cx + \alpha[hE(x-D)^+ + pE(x-D)^- - c(x-D)],\)

因此，再次从假设 (11.1.4) 我们得到当 \(|x| \to +\infty\) 时 \(G_n(x, Q) \to +\infty\)。而且 \(G'_n(x, Q)\) 在 \(Q\) 中是单调递增的。由此可知 \(G_n(x, Q)\) 在一点 \(S_n(Q)\) 处取得其最小值。通过取最小的最小值，我们可以


以唯一方式定义该点。该点严格为正，因为 \(G'_n(x, Q) \le c(1-\alpha) - \alpha p < 0, \forall x \le S\)。因此，我们可以将 \(u_{n+1}(x, Q)\) 写为如下形式

```
\(\begin{align*} u_{n+1}(x, Q) = \begin{cases} hx^+ + px^- - cx + G_n(x+Q, Q), & \text{if } x < S_n(Q) - Q \\ hx^+ + px^- - cx + G_n(S_n(Q), Q), & \text{if } S_n(Q) - Q < x < S_n(Q) \\ hx^+ + px^- - cx + G_n(x, Q) & \text{if } x > S_n(Q) \end{cases} \end{align*}\)
```

然后我们检查 \(u_{n+1}(x, Q)\) 是否具有与 \(u_n(x, Q)\) 相同的性质。注意 \(S_n(Q)\) 关于 \(Q\) 单调递减。

由 \(u_n(x, Q)\) 的凸性可知，极限 \(u(x, Q)\) 是凸的。

由于 \(u(x, Q) \ge u_n(x, Q)\)，我们得到当 \(|x| \to +\infty\) 时 \(u(x, Q) \to +\infty\)。另外，由 (11.1.5) 定义的 \(G(x, Q)\) 是凸的、连续的，且当 \(|x| \to +\infty\) 时趋于 \(+\infty\)。函数 \(G(x, Q)\) 在一点 \(S(Q)\) 处取得其最小值，通过取最小的最小值，我们可以唯一地定义 \(S(Q)\)。公式 (11.1.6) 定义了一个最优反馈。现在让我们证明 \(u(x, Q)\) 是 \(C^1\) 的，除了在 0 处。我们首先注意到如下估计

```
\(|u'_n(x, Q)| \le \frac{\max(h, p) + c}{1 - \alpha}.\)
```

因此，极限 \(u(x, Q)\) 是 Lipschitz 连续的。但随后 \(G(x, Q)\) 是 \(C^1\) 的，因为

```
\(G'(x, Q) = c + \alpha \int_{-\infty}^x u'(z, Q) f(x-z) dz,\)
```

且 \(G'(S(Q), Q) = 0\)。函数

```
\(g(x, Q) = \inf_{x \le z \le x+Q} G(z, Q),\)
```

也是 \(C^1\) 的。因此

```
\(u(x, Q) = hx^+ + px^- - cx + g(x, Q),\)
```

也是 \(C^1\) 的，除了在 0 处。由于 \(G'(0, Q) \le c(1-\alpha) - \alpha p < 0\)，故 \(S(Q) > 0\)。我们还可以检查 \(S(Q)\) 是递减的，且 \(u'(x, Q)\) 关于 \(Q\) 单调递增。

证明已完成。

### 注释 11.1。

\(S(Q)\) 没有显式公式。它满足

```
\(c + \alpha Eu'(S(Q) - D) = 0.\)
```

然而，与 \(Q = +\infty\) 的情况不同，无法显式地表达 \(Eu'(S(Q) - D)\)。定义

```
\(\begin{align*} z(x) &= u'(x) - h \mathbb{1}_{x > 0} + p \mathbb{1}_{x < 0} + c \\ g(x) &= c(1-\alpha) + \alpha h - \alpha (p+h) \bar{F}(x), \end{align*}\)
```

则条件变为

```
(11.1.10) \(g(S(Q)) + \alpha Ez(S(Q) - D) = 0.\)
```

当 \(Q = +\infty\) 时，\(z(x) = 0, \forall x \le S\)，但当 \(Q\) 有限时不成立。函数 \(z(x)\) 是下列问题的解

```
(11.1.11) \(z(x) = \begin{cases} g(x+Q) + \alpha Ez(x+Q-D), & \text{if } x < S(Q) - Q \\ 0 & \text{if } S(Q) - Q < x < S(Q) \end{cases}\)
```

仅需对 \(x \le S(Q) - Q\) 定义 \(z(x)\)。我们得到问题

```
\(z(x) = g(x+Q) + \alpha Ez(x+Q-D) \mathbb{1}_{D > (x+2Q-S(Q))^+},\)
```

这等价于积分方程

```
(11.1.12) 
\( z(x) = g(x+Q) + \alpha \int_{-\infty}^{\min\{x+Q, S\}} z(\eta) f(x+Q-\eta) d\eta. \)
```

对每个 \( S > 0 \)，我们求解积分方程 (11.1.12)。然后通过代数方程 (11.1.10) 定义 \( S(Q) \)。

设置成本的情况尚未解决。最优反馈不太可能由 \( s(Q), S(Q) \) 策略给出。

## 11.2. 多供应商问题

### 11.2.1. 问题描述。

我们在这里介绍 E. Porteus [33] 考虑的一个问题。它推广了第 9 章中发展的带设置成本的库存控制问题。对于订货，现在假设存在多个供应商来源。更准确地说，订购成本函数由以下给出

```
(11.2.1) 
\( C(z) = \begin{cases} 0, & \text{if } z=0 \\ \min_i(K_i + c_i z) & \text{if } z>0 \end{cases} \, \)
```

其中

```
(11.2.2) 
\( c_1 > c_2 > \cdots > c_M > 0, \quad 0 < K_1 < K_2 < \cdots < K_M. \)
```

变动成本和固定成本变化方向相反。因此，不存在单一供应商同时兼具最低的变动成本和固定成本。可以进行权衡。当然，这就是困难的根源。

### 练习 11.1。

证明函数 \( C(z) \) 在 \( z \ge 0 \) 上是凹函数且 \( C(0) = 0 \)。证明在 \( R^+ \) 上凹且在 0 处消失的函数 \( C(z) \) 满足次可加性

```
(11.2.3) 
\( C(z_1 + z_2) \le C(z_1) + C(z_2). \)
```

### 练习 11.2。

证明以下性质

```
\( C(z) = \left\{ \begin{array}{l} \min_{v_1 + \cdots + v_M = z \\ v_i \ge 0} \sum_{i=1}^M (K_i \mathbb{1}_{v_i > 0} + c_i v_i). \end{array} \right. \)
```

这通过对 \( M \) 进行递归来证明。它可以解释为：在供应商之间拆分订单没有意义。需要选择单一供应商。

我们考虑带缺货的动态库存控制问题。我们可以轻松写出动态规划方程。

```
(11.2.4) 
\( u(x) = hx^+ + px^- + \inf_{i=1,\dots,M \\ \eta \ge x} [K_i \mathbb{1}_{\eta > x} + c_i(\eta - x) + \alpha E u(\eta - D)]. \)
```

若令

```
(11.2.5) 
\( w(x) = u(x) - hx^+ - px^- , \)
```

动态规划方程等价于

```
(11.2.6) 
\( w(x) = \inf_{\eta \ge x} [C(\eta - x) + \alpha E(h(\eta - D)^+ + p(\eta - D)^- + w(\eta - D))]. \)
```

引入以下记法很方便。定义

$$g_i(x) = c_i(x + \overline{D}) + \alpha(w(x) + hx^+ + px^-),$$

以及

$$G_i(x) = E g_i(x - D).$$

还令

$$G_i^*(x) = \min \left[ G_i(x), \inf_{y \ge x} (K_i + G_i(y)) \right] = \inf_{y \ge x} (K_i \mathbb{1}_{y > x} + G_i(y)),$$

以及

$$w_i(x) = -c_i x + G_i^*(x).$$

最后，动态规划方程 (11.2.6) 变为

$$w(x) = \min_{1 \le i \le M} w_i(x).$$

目标是证明以下结果

### 定理 11.3。

假设 (11.11)、(11.2) 以及

$$(11.2.7) \quad c_1 - \alpha c_M - \alpha p < 0,$$

以及对需求概率密度的限制，即下述性质 $\mathcal{P}$（$f$ 为泊松分布或泊松分布的卷积）。那么 (11.2.4) 右侧的反馈 \(\delta(x)\) 由广义 s,S 策略给出。这意味着存在一个双序列

$$(11.2.8) \quad s_m^* < s_{m-1}^* < \cdots < s_1^* < S_1 < S_2 \cdots < S_m, \quad 1 \le m \le M,$$

带有反馈

$$(11.2.9) \quad \delta(x) = \begin{cases} S_m & \text{if } x \le s_m^* \\ S_i & \text{if } s_{i+1}^* < x \le s_i^*, i=1, \cdots, m-1 \\ x & \text{if } x > s_1^* \end{cases}$$

## 11.2.2. 辅助结果

我们需要 K 凸性理论的一些扩展。我们从满足代数性质的函数 $G_i(x)$ 开始。稍后，我们将证明前一节中用相同记法定义的函数满足这些性质。

考虑函数 $G_i(x)$，$i = 1, \cdots, M$，它们是连续的，且当 $|x| \to +\infty$ 时 $G_i(x) \to \infty$。我们假设存在 $a_i$ 使得 $G_i(x)$ 在 $(-\infty, a_i]$ 上递减，并满足

$$G_i(x) < K_i + G_i(y), \forall a_i < x < y.$$

我们说 $G_i(x)$ 在 $[a_i, +\infty)$ 上是 $K_i$ 非递减的。我们还假设关系

$$G_{i+1}(x) - G_i(x) = (c_{i+1} - c_i)x.$$

我们令

$$G_i^*(x) = \inf_{y \ge x} (K_i \mathbb{1}_{y > x} + G_i(y)),$$

以及

$$w_i(x) = -c_i x + G_i^*(x).$$

最后，我们有兴趣计算

$$(11.2.10) \quad w(x) = \min_{1 \le i \le M} w_i(x).$$

优化问题分为两步。对每个 $i$，找到最优

$\bar{y}_i = \delta_i(x)$,

它在 $G_i^*(x)$ 的定义中在 $y$ 上取得最小值。然后在 $w(x)$ 的定义中找到正确的索引 $i(x)$。表达订单作为库存函数的反馈函数由以下给出

$\bar{y} = \delta(x) = \delta_{(i(x))}(x)$.

除了索引之外，该框架让人联想到 $K$ 凸性。然而，函数 $G_i(x)$ 不是 $K_i$ 凸的，但它们享有一个相近的性质，即准 $K_i$ 凸性。去掉索引，我们通过以下定义 $K$ 准凸性

$G(\theta x + (1-\theta)y) \le \max[G(x), K + G(y)], \forall x \le y$

### 练习 11.3。

证明函数 $G_i(x)$ 的 $K$ 准凸性性质。还证明一个 $K$ 凸函数是 $K$ 准凸的。

### 练习 11.4。

给出一个在 $(-\infty, a]$ 上递减、在 $[a, \infty)$ 上 $K$ 非递减，但不是 $K$ 凸的函数示例。

首先容易检查的一点是 $\delta_i(x)$ 由 $s_i, S_i$ 策略给出。确实存在

$s_i \le a_i \le S_i$,

使得

$G_i(S_i) = \min_y G_i(y)$,

以及

$G_i(s_i) = K_i + G_i(S_i)$.

那么显然

$\delta_i(x) = \begin{cases} S_i, & \text{if } x \le s_i \\ x, & \text{if } x > s_i \end{cases}$

还要注意性质

$G_i(x) \le G_i(s_i), \text{ for } s_i \le x \le S_i$

### 注释 11.2。

如果函数 $G_i(x)$ 是 $K_i$ 凸的，那么我们可以将其与满足上述性质的 $s_i, S_i$ 关联。通过取 $a_i = s_i$，我们可以看到在 $(-\infty, a_i]$ 上递减和在 $[a_i, \infty)$ 上 $K_i$ 非递减的性质是满足的。

我们注意到

$G'_i(x) = \begin{cases} G_i(s_i), & \text{if } x \le s_i \\ G_i(x), & \text{if } x \ge s_i \end{cases}$

因此它是一个连续函数，且 $w_i(x)$ 也是连续的。

### 练习 11.5。

证明 $w(x)$ 也是连续的。

具有以下性质

### 引理 11.1。

$a_1 \le S_1 \le S_2 \le \cdots \le S_M$。



证明。注意，根据 $S_i$ 的定义，有

$$G_{i+1}(S_i) - G_i(S_i) \ge G_{i+1}(S_{i+1}) - G_i(S_{i+1}),$$

因此

$$(c_{i+1} - c_i)S_i \ge (c_{i+1} - c_i)S_{i+1},$$

从而

$$S_i \le S_{i+1}.$$

还具有以下性质

### 引理 11.2.

如果 $s_i \le s_j$，对 $i \le j$ 则 $w_i(x) \ge w_j(x)$ 对所有 $x$ 成立

**证明。** 如果 $x \le s_i$ 则

$$\begin{aligned} w_i(x) &= -c_i x + G_i(s_i) \\ &= -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ \ge -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ &= -c_i x + (c_i - c_j)s_i + w_j(x) + c_j x \\ \ge w_j(x) \end{aligned}$$

如果 $s_i \le x \le s_j$，则

$$\begin{aligned} w_i(x) &= -c_i x + G_i(x) \\ &= -c_i x + G_j(x) \\ \ge -c_i x + G_j(s_i) \\ &= w_j(x) \end{aligned}$$

最后，如果 $x \ge s_j$，则 $w_i(x) = w_j(x)$

证明结束。

因此可以舍弃供应商 $i$。因此剩下 $m \le M$ 个供应商，其配置如下

$$s_m < s_{m-1} < \cdots < s_1 \le S_1 \le \cdots \le S_m.$$

我们现在定义广义 $s, S$ 策略的概念（参见定理陈述）。它由一个双序列组成

$$s_m^* < s_{m-1}^* < \cdots < s_i^* < S_i < S_2 \cdots < S_m,$$

伴随反馈

$$\delta(x) = \begin{cases} S_m, & \text{if } x \le s_m^* \\ S_i, & \text{if } s_{i+1}^* < x \le s_i^*, i = 1, \cdots, m-1 \\ x, & \text{if } x > s_1^* \end{cases}$$

回顾 $\delta(x) = \delta_{i(x)}(x)$，我们看到广义 $s, S$ 策略只有在以下条件下才可能

$$s_i^* \le s_i, s_1^* = s_1.$$

我们可以将优化问题的主要结果表述如下

### 定理 11.4.

(11.2.10) 中的函数 \( w(x) \) 通过广义 \( s,S \) 策略得到。具体来说，存在 $m \le M$ 和 $[1, \cdots, M]$ 的一个子集，我们可以将其按递增顺序重新编号为 $[1, \cdots, m]$，以及一个关联序列 $s_i^*$，满足 $s_i^* > s_{i+1}^*, s_i^* \le s_i, s_1^* = s_1$，使得

$$w(x) = \begin{cases} -c_m x + G_m(s_m), & \text{if } x \le s_m^*, i(x) = m \\ -c_i x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^*, i=1, \cdots, m-1, i(x)=i \\ -c_1 x + G_1(x), & \text{if } x > s_1^* = s_1, \text{no order} \end{cases}$$

**证明。** 定义

$$s_{ij} = \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j};$$

$$s_j^* = \min \left( s_{j1}, \min_{i=1,\cdots,j-1} s_{ij} \right).$$

我们将证明

$$i(x) \text{ may be chosen } \ge j \text{ if } x \le s_j^*$$
$$i(x) \text{ may be chosen } \le j - 1 \text{ if } x > s_j^*$$

事实上，如果 $x \le s_j^*$，则

$$w_j(x) = -c_j x + G_j(s_j),$$

并且对于 $i \le j-1$，$x \le s_{ij}$ 蕴含

$$x \le \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j}.$$

因此

$$w_j(x) \le -c_i x + G_i(s_i), \forall i \le j-1.$$

然而

$$w_i(x) = \begin{cases} -c_i x + G_i(s_i), & \text{if } x \le s_i \\ -c_{i+1} x + G_i(x), & \text{if } x > s_i \end{cases}$$

还要注意

$$w_i(x) \le -c_i x + G_i(x), \forall x.$$

因此如果 $x \le s_i$，我们可以断言 $w_i(x) \ge w_j(x)$。另一方面，如果 $x > s_i$，则 $w_i(x) = -c_{i+1}x + G_i(x) \ge w_j(x)$。所以第一部分已证明。

假设现在 $x > s_j^*$，我们要证明存在某个 $i \le j-1$，使得 $w_i(x) \le w_j(x)$。有几种情况。如果 $s_j^* = s_i$，则 $w_j(x) = -c_j x + G_j(x)$，因此

$$w_j(x) = -c_i x + G_i(x) \ge w_i(x) \forall i \neq j.$$

假设 $s_j^* = \min_{i=1,\cdots,j-1} s_i < s_j$，那么如果 $x \ge s_j$，我们有与之前相同的情况。剩下的情况是 $s_j^* < x < s_j$。在这种情况下，$w_j(x) = -c_j x + G_i(s_i)$，并且存在 $i \le j-1$，使得 $s_{ij} = s_j^* < x$，这蕴含 $w_j(x) > -c_{i+1}x + G_i(s_i)$。而且 $s_i > s_j$，因为 $i \le j-1$。因此 $x < s_i$，且 $w_i(x) = -c_{i+1}x + G_i(s_i)$。我们立即得到 $w_i(x) < w_j(x)$。所以我们已经证明存在 $i \le j-1$，优于或等价于 $j$。

由此可得

$$s_i^* \le s_j^*$$

那么供应商 $i$ 永远不会被选择。事实上，我们知道如果 $x \le s_j^*$，我们可以在供应商 $j, \cdots, M$ 中选择，因此索引 $i$ 可以被排除。另一方面，如果 $x > s_j^* \ge s_i^*$，那么 $i$ 和 $j$ 都可以被排除。因此我们消除所有索引 $i$，使得存在 $j > i$ 且 $s_i^* \le s_j^*$。剩下 $m$ 个索引，且 $s_i^*$ 递减。我们可以重新编号它们，并以此定义序列 $s_1^* > s_2^* > \dots > s_m^*$。由此可知，如果 $s_{i+1}^* < x \le s_i^*$，则 $i(x)$ 可以在大于或等于 $i$ 的索引中选择，但我们可以排除 $i+1, \dots, m$，因此 $i$ 是最优的。如果 $x > s_1^* = s_1$，我们可以消除所有索引，因此不订购是最优的。

证明已完成。

我们现在证明函数 $w$ 的一些性质

### 推论 11.1.

函数 $w(x)$ 在 $(-\infty, a_1]$ 上递减，且 $w(x) + c_1 x$ 在 $[a_1, +\infty)$ 上是 $K_1$ 非递减的。

**证明。** 回顾 $w(x)$ 是连续的。从引理 11.4 中证明的公式可知，$w(x)$ 在 $(-\infty, s_1]$ 上递减，并且根据 $G_1$ 的性质，在 $(s_1, a_1)$ 上也递减。第二部分显而易见。

让我们检查 $w$ 的其他性质。

### 推论 11.2.

$w(x) + c_i x$ 在整条直线 $R$ 上是 $K_i$ 非递减的。假设 $a_m \ge 0$，则 $w(x) + c_m x$ 在 $(-\infty, 0]$ 上递减。

**证明。** 注意到 $G_i(x) = G_1(x) + (c_i - c_1)x$。

我们可以写出 $G_i^*(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + G_1(y) - c_1 y + c_i y \}$。

因为 $w_i(x) = -c_i x + G_i^*(x)$。

由此可得 $w_i(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + c_i(y - x) + G_1(y) - c_1 y \}$。

由此可得 $w(x) = \inf_{z \ge x} \{ C(z - x) + G_1(z) - c_1 z \}$。

其中 $C(z) = \min_{i=1}^m \{ K_i \mathbb{I}_{z > 0} + c_i z \}$。

取 $y \ge x$，则 $w(x) \le \inf_{z \ge y} \{ C(z - x) + G_1(z) - c_1 z \}$。

并且根据 $C(z)$ 的次可加性，以及 $z \ge y \ge x$，可得 $w(x) \le w(y) + C(y - x)$。

由此我们推断 $w(x) \le w(y) + K_i + c_i(y - x)$，对所有 $i$ 成立。

因此 $w(x) + c_i x$ 在整条直线 $R$ 上是 $K_i$ 非递减的。接下来

$$w(x) + c_m x = \begin{cases} G_m(s_m), & \text{if } x \le s_m^* \\ (c_m - c_i)x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^* \\ (c_m - c_1)x + G_1(x), & \text{if } x > s_1^* \end{cases}$$

事实上，可以观察到 $w(x) + c_m x = G_m(x)$，如果 $x > s_1^*$。

从上述表达式，使用 $c_m \le c_i$ 对所有 $i$，以及 $a_m \ge 0$ 的事实，因此 $G_m(x)$ 在 $(-\infty, 0]$ 上递减，推论 11.2 的第二部分随之得出。

## 11.2.3. 多供应商问题的应用。

要将前面的结果应用于多供应商问题，我们需要一个额外的中间结果。考虑一个分段连续的函数 $\psi(x)$，当 $|x| \to +\infty$ 时趋于 $+\infty$，因此达到其最小值。设 $D$ 为一个正随机变量，密度为 $f$。量 $\chi(x) = E\psi(x - D)$ 是一个连续函数，当 $x \to +\infty$ 时也趋于 $+\infty$。

练习 11.6。证明前述性质。使用 $\psi(x)$ 达到其最小值这一事实。

然而，如果 $\psi$ 在 $(-\infty, a]$ 上递减，且在 $[a, +\infty)$ 上是非 $K$ 递减的，那么该性质不会传递给 $\chi$。只要 $\psi$ 是准 $K$ 凸的，就会出现同样的糟糕情况。在 $K$ 凸的情况下，该性质会传递。不过要注意，$\chi(x)$ 在 $(-\infty, a]$ 上递减，并且由于当 $x \to +\infty$ 时它趋于 $+\infty$，必然存在某个 $b \ge a$，使得 $\chi(x)$ 在 $(-\infty, b]$ 上递减，之后可能增加。因此 $b$ 是一个局部最小值。我们希望将自己限制在分布 $f$ 上，使得以下性质 $\mathcal{P}$ 成立：函数 $\chi$ 在 $[b, +\infty)$ 上是非 $K$ 递减的。

让我们证明，每当分布 $f$ 是泊松分布或泊松分布的卷积时，性质 $\mathcal{P}$ 成立。假设 $f$ 是参数为 $\lambda$ 的泊松分布，则 $f(x) = \lambda \exp -\lambda x$。

练习 11.7。验证 $\chi'(x) = \lambda(\psi(x) - \chi(x))$。

设 $S$ 为 $\chi$ 的最小值。由于 $\chi'(b) = \chi'(S) = 0$，我们有 $\chi(S) = \psi(S)$ 且 $\chi(b) = \psi(b)$。设 $h > 0$。考虑函数 $z(x) = \chi(x) - \chi(x + h) - K$，则我们有 $z(b) \le \chi(b) - \chi(S) - K = \psi(b) - \psi(S) - K \le 0$，因为 $a \le b \le S$。

练习 11.8。验证 $z'(x) \le -\lambda z(x)$。

因此 $\frac{dz}{dx} \exp \lambda x \le 0$，

由此可得 $z(x) \exp \lambda x \le z(b) \exp \lambda b$，对所有 $x \ge b$ 成立，因此 $z(x) \le 0$，对所有 $x \ge b$ 成立。这意味着 $\chi$ 对 $x \ge b$ 是 $K$ 非递减的。性质 $\mathcal{P}$ 传递到泊松分布的卷积。事实上，如果 $D = \sum_{j=1}^J D_j$，


假设随机变量 \( D^j \) 相互独立且服从泊松分布（参数为 \( \lambda^j \)），则定义

\(\gamma^j(x) = E\psi \left( x - \sum_{i=1}^j D_i \right), \gamma^0(x) = \psi(x).\)

显然 \(\chi(x) = \gamma^j(x)\).

### 练习 11.9. 证明

\(\gamma^j(x) = E\gamma^{j-1}(x - D_j).\)

由于每个需求都服从泊松分布，可以递归地验证，存在一个 \( b \)，使得 \(\chi(x)\) 在 \((-\infty, b]\) 上单调递减，在 \([b, +\infty)\) 上 \( K \) 单调非递减。

我们现在可以求解多供应商问题了。引入如下算子比较方便，方程 (11.2.6) 中的 \( w \) 是其不动点。更准确地说，引入函数 \( v(x) \)，使得

- (11.2.12)
- \( v \) 是连续的，\( (c_M + \alpha h)x + \alpha v(x) \to +\infty \)，当 \( x \to +\infty \)
- \( (c_1 - \alpha p)x + \alpha v(x) \to +\infty \)，当 \( x \to -\infty \)
- \( v(x) + c_M x \) 在 \((-\infty, 0]\) 上单调递减
- \( v(x) + c_i x \) 在 \( R \) 上 \( K_i \) 单调非递减

注意，根据第三个条件，我们还有

\( v(x) \to +\infty, \text{ as } x \to -\infty. \)

我们引入一个算子，该算子依次将函数 \( v(x) \) 关联到函数

\( g_i(v)(x) = c_i(x + \overline{D}) + \alpha(hx^+ + px^-) + \alpha v(x), \)

和

\( G_i(v)(x) = Eg_i(v)(x - D). \)

还令

\( G_i^*(v)(x) = \inf_{y \ge x} (K_i \mathbf{1}_{y > x} + G_i(v)(y)), \)

和

\( w_i(v)(x) = -c_i x + G_i^*(v)(x), \)
\( w(v)(x) = \min_{1 \le i \le M} w_i(v)(x). \)

那么，我们可以断言

\( w(x) = w(w)(x). \)

我们从以下内容开始

### 引理 11.3. 假设 (11.2.7) 且需求 \( D \) 满足性质 \( \mathcal{P} \). 在 \( G_i(v) \) 的记号中省略 \( v \)，我们可以断言

- (11.2.13)
- \( G_i \) 是连续的，\( G_i \to +\infty, \text{ as } |x| \to +\infty \)
- \( \exists a_i \ge 0 \text{ 使得 } G_i \text{ 在 } (-\infty, a_i] \) 上单调递减
- \( G_i \) 在 \( (a_i, +\infty) \) 上 \( K_i \) 单调非递减

证明。写出

\(g_t(x) = c_t \overline{D} + (c_t - c_t)x + (c_t - \alpha c_M)x + \alpha(hx^+ + px^-) + \alpha(c_M x + v(x)),\)

我们立即从假设 (11.2.7) 和 \(v\) 的性质看出

\(g_t(x)\) 在 \((-\infty, 0)\) 上单调递减。

再写出

\(g_t(x) = c_t \overline{D} + (1-\alpha)c_t x + \alpha(hx^+ + px^-) + \alpha(c_t x + v(x)),\)

我们从 \(v\) 的性质得到

\(g_t(x)\) 在 \([0, +\infty)\) 上非 \(K_t\) 单调递减。

显然，\(g_t(x) \to +\infty\) 当 \(|x| \to +\infty\)。由此可知，由数学期望的平滑效应，\(G_t(x)\) 是连续的。\(G_t(x) \to +\infty\)，当 \(|x| \to +\infty\)，并且由于需求满足性质 \(\mathcal{P}\)，存在 \(a_t \ge 0\)，使得 (11.2.13) 得到验证。

从之前考虑的中间优化问题的一般分析，特别是推论 11.2 可知，\(w(v)\) 满足与 \(v\) 相同的性质，即 (11.2.12)。此外，最优反馈 \(\delta(v)(x)\) 由广义 s,S 政策给出。

我们将上述发展应用于多供应商问题。我们从 \(w_0(x) = -c_M x\) 开始。如果假设 (11.2.7)，则该函数满足 (11.2.12) 中通用函数 \(v\) 的性质。因此递归可以开始。这完成了定理 11.3 的证明。\(\square\)

本页故意留空

# 马尔可夫需求下的库存控制

## 12.1. 引言

在迄今考虑的所有模型中，需求都被视为一组独立同分布的随机变量。实际上，连续需求出于许多原因是相关的。建模这种关联的最简单方法是假设需求本身构成一个马尔可夫过程，或源自一个马尔可夫过程。我们在这里的目标是展示前几章中描述的方法如何适应这种情况。在 D. Beyer 等人最近的一本书 [12] 中，对这些问题进行了全面的介绍。我们也参考该书的参考文献以了解相关文献。在这项工作中，作者认为需求来自一个底层的需求状态，该状态被建模为具有有限状态数的马尔可夫链。状态数有限这一事实简化了数学论证。我们将在这里讨论需求本身是马尔可夫过程的情况。

### 12.2. 无积压且无设置成本

### 12.2.1. 模型。

设 \(\Omega, \mathcal{A}, P\) 为概率空间，其上定义了马尔可夫链 \(z_n\)。这个马尔可夫链表示需求。其状态空间为 \(R^+\)，其转移概率为 \(f(\zeta|z)\)。我们假设

- (12.2.1) \(f(\zeta|z)\) 在两个变量中一致连续且有界
- (12.2.2) \(\int_0^{+\infty} \zeta f(\zeta|z) d\zeta \le c_0 z + c_1.\)

我们可以假设 \(z_1 = z\)，一个固定常数，或者更一般地，一个具有给定概率分布的随机变量。我们定义滤流 \(\mathcal{F}^n = \sigma(z_1, \cdots, z_n).\)

一个控制策略，记为 \(V\)，是随机变量序列 \(v_n\)，使得 \(v_n\) 是 \(\mathcal{F}^n\) 可测的。当 \(z_1 = z\) 时，\(v_1\) 是确定的。同样，我们通常假设 \(v_n \ge 0\)。我们接下来将库存定义为序列，其中

- (12.2.3) \(y_{n+1} = (y_n + v_n - z_{n+1})^+, \quad y_1 = x.\)

过程 \(y_n\) 适应于滤流 \(\mathcal{F}^n\)。联合过程 \(y_n, z_n\) 也是一个马尔可夫链。

对于测试函数 \(\varphi(x, z)\)（在 \(R^+ \times R^+\) 上有界连续），我们可以写出

\(E[\varphi(y_2, z_2)|y_1 = x, z_1 = z, v_1 = v]\)
\(= E[\varphi((x + v - z)^+, z_2)|z_1 = z]\)
\(= \int_{z+v}^{+\infty} \varphi(0, z)f(\zeta|z)d\zeta + \int_0^{x+v} \varphi(x + v - \zeta, z)f(\zeta|z)d\zeta\)

这定义了一个马尔可夫链，与其关联的算子为

(12.2.4) \(\Phi^v\varphi(x, z) = \int_{z+v}^{+\infty} \varphi(0, \zeta)f(\zeta|z)d\zeta + \int_0^{x+v} \varphi(x + v - \zeta, \zeta)f(\zeta|z)d\zeta,\)

因此转移概率由

(12.2.5) \(\pi(x, z, v, d\xi, d\zeta) = \delta(\xi) \otimes f(\zeta|z)\mathbb{1}_{z+v > x}d\zeta\)
\(+\delta(\xi - (x + v - \zeta)) \otimes f(\zeta|z)\mathbb{1}_{x+v < \zeta}d\zeta.\)

给出。

我们接下来定义函数

(12.2.6) \(l(x, z, v) = cv + hx + p \int_{z+v}^{\infty} (\zeta - x - v)f(\zeta|z)d\zeta,\)

它将模拟一期成本。成本函数为

(12.2.7) \(J_{x,z}(V) = E \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, z_n, v_n).\)

我们关注的值函数为

(12.2.8) \(u(x, z) = \inf_V J_{x,z}(V).\)

我们首先注意到性质 (4.3.1)、(4.3.2) 已满足。为继续，我们需要指定一个上限函数。它对应于恒等为 0 的控制。令 \(l_u(x, z) = l(x, z, v)\)。注意不等式。

(12.2.9) \(cv + hx \le l_u(x, z) \le cv + hx + p(c_0 z + c_1),\)

和

(12.2.10) \(cv \le \Phi^v l_u(x, z) \le cv + h(x + v) + p(c_0^2 z + c_0 c_1 + c_1).\)

然后考虑函数

(12.2.11) \(w_0(x, z) = \sum_{n=1}^{\infty} \alpha^{n-1} (\Phi^0)^{n-1} l_0(x, z)\)

### 引理 12.1. 我们假设

(12.2.12) \(\alpha c_0 < 1,\)

则级数 \(w_0(x, z) < \infty\)，更精确地说

(12.2.13) \(w_0(x, z) \le \frac{hx}{1 - \alpha} + \frac{pc_0 z}{1 - \alpha c_0} + \frac{pc_1}{(1 - \alpha)(1 - c_0 \alpha)}.\)

证明。这是公式 (12.2.11) 和 (12.2.10) 的直接结果。

我们现在可以写出贝尔曼方程

(12.2.14) \(u(x, z) = \inf_{v \ge 0} [l(x, z, v) + \alpha \Phi^v u(x, z)].\)

我们陈述以下内容

### 定理 12.1. 我们假设 (12.2.1)、(12.2.2)、(12.2.6)、(12.2.12)。那么方程 (12.2.14) 存在唯一解，满足 \(0 \le u \le w_0\)。它是连续的，并与值函数 (12.2.8) 重合。存在最优反馈 \(\hat{v}(x,z)\) 和最优控制策略 \(\hat{V}\)。

证明。我们首先注意到定理 4.4 和 4.3 的条件已满足。因此方程 (12.2.14) 的解集非空。它有一个最小解和一个最大解。最小解是下半连续的（l.s.c.），最大解是上半连续的（u.s.c.）。最小解与值函数重合。存在最优反馈 \(\hat{v}(x,z)\) 和最优控制策略 \(\hat{V}\)。为证明唯一性，我们需要证明最小解和最大解重合。我们首先证明 \(\hat{v}(x,z)\) 的一个界。首先，提及 \(w_0\) 的一个稍好估计会比较方便。确实，我们可以写出

\(\text{(12.2.15)} \quad w_0(x,z) \le h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z) + \frac{p c_0 z}{1-c_0 \alpha} + \frac{p c_1}{(1-\alpha)(1-c_0 \alpha)},\)

并且 (12.2.13) 仅通过使用 \(\Phi^0(x,x) \le x\) 从 (12.2.15) 得出。接下来，从 (12.2.14) 出发，考虑 \(\underline{u}\)，即最小解，我们可以断言

\(\underline{u}(x,z) \ge h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z),\)

这源于 \(l(x,z,v) \ge hx\)，以及

\(\text{(12.2.16)} \quad \Phi^v \varphi(x,z) \ge \Phi^0 \varphi(x,z), \forall v \ge 0, \forall \varphi \text{ 在 } x \text{ 中单调递增}.\)

因此，我们可以写出

\(l(x,z,v) + \alpha \Phi^v \underline{u}(x,z) \ge c v + h \sum_{n=1}^\infty (\alpha \Phi^0)^{n-1} x(x,z).\)

因此，在对 \(v\) 求最小值时，我们可以从上方界定 \(v\) 的范围。更精确地说，我们得到

\(\text{(12.2.17)} \quad \hat{v}(x,z) \le \frac{p c_0 z}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

我们考虑从最优反馈得到的最优轨迹 \(\hat{y}_n, z_n\)，即

其中 \(\hat{y}_1 = x, z_1 = z\)。

根据第 4 章第 4.5 节，如果我们能验证 \(\hat{V} \in \mathcal{V}\)，即

\(\alpha^n E \hat{u}(y_{n+1}, z_{n+1}) \to 0, \text{ 当 } n \to \infty\)

则最大解将与最小解重合。将 \(\hat{u}\) 替换为 \(w_0\) 就足够了，根据估计 (12.2.13)，只需证明

\(\text{(12.2.18)} \quad \alpha^n E \hat{y}_{n+1}, \quad \alpha^n E z_{n+1} \to 0, \text{ 当 } n \to \infty.\)

然而，根据标准的马尔可夫论证，\(\alpha^n E z_{n+1} \le (\alpha c_0)^n z\)。根据假设 (12.2.12)，(12.2.18) 的第二部分立即得出。接下来我们使用

\(\hat{y}_{n+1} \le \hat{y}_n + \hat{v}_n\)
\(\le \hat{y}_n + \frac{p c_0 z_n}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)




因此

\(E\hat{y}_{n+1} \le E\hat{y}_n + \frac{p c_0^2 z}{c(1-c_0 \alpha)} + \frac{p c_1}{c(1-\alpha)(1-c_0 \alpha)},\)

并且我们推导出估计

\(E\hat{y}_{n+1} \le x + \frac{p z c_0}{c(1-c_0 \alpha)} \frac{1-c_0^n}{1-c_0} + \frac{n p c_1}{c(1-\alpha)(1-c_0 \alpha)}.\)

再次使用假设 (12.2.12)，我们推导出 (12.2.18) 的第一部分。证明完成。

## 12.2.2. 基准库存政策。

我们现在要验证最优反馈 \(\hat{v}(x, z)\) 可以通过基准库存政策获得，其中基准库存取决于 \(z\) 的值。我们有

### 定理 12.2.

我们采用定理 12.1 的假设且 \(p > c\)。我们还假设

(12.2.19) \(f(x, z) \ge a_0(M) > 0, \forall x, z \le M.\)

那么函数 \(u(x, z)\) 在自变量 \(x\) 上是凸的且为 \(C^1\)。此外，最优反馈由以下给出

(12.2.20) \(\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{若 } x \le S(z) \\ 0, & \text{若 } x \ge S(z) \end{cases}\)

函数 \(S(z)\) 一致连续，且关于 \(x\) 的导数 \(u'(x, z)\) 也是一致连续的。

证明。我们考虑递增过程

\(u_{n+1}(x, z) = \inf_{v \ge 0} [\langle x, z, v \rangle + \alpha \Phi^u u_n(x, z)], \quad u_0(x) = 0\)

我们也将其写为

\(u_{n+1}(x, z) = (h - c)x + \inf_{\eta \ge z} \{c\eta + p E[(\eta - z_2)^-] \mid z_1 = z\} + \alpha E[u_n((\eta - z_2)^+, z_2) \mid z_1 = z],\)

并且我们将递归地证明序列 \(u_n(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)。定义

\(G_n(x, z) = cx + p E[(x - z_2)^- \mid z_1 = z] + \alpha E[u_n((x - z_2)^+, z_2) \mid z_1 = z],\)

那么函数 \(G_n(x, z)\) 在 \(S_n(z)\) 处取得其最小值，其中 \(S_n(z)\) 可以通过取最小的最小值来唯一确定。我们首先考虑

\(G_0(x, z) = cx + p E[(x - z_2)^- \mid z_1 = z].\)

它在 \(x\) 上是凸的且为 \(C^1\)。我们有

\(G'_0(x, z) = c - p \bar{F}(x|z),\)

其中

\(\bar{F}(x|z) = \int_x^\infty f(\xi|z) d\xi.\)

函数 \(G'_0(x, z)\) 随 \(x\) 增加，从 \(c-p < 0\) 增加到 \(c\)。得益于假设，我们唯一地定义 \(S_0(z)\) 使得 \(G'_0(S_0, z) = 0\)。根据凸性，我们可以断言

\(u_1(x, z) = \begin{cases} (h-c)x + G_0(S_0(z), z), & \text{若 } x \le S_0(z) \\ (h-c)x + G_0(x, z), & \text{若 } x \ge S_0(z) \end{cases}\)

我们看到 \(u_1(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)。然后

\(G_1(x, z) = cx + pE[(x - z_2)^-|z_1 = z] + \alpha(h - c)E[(x - z_2)^+|z_1 = z] + \alpha E[G_0(\max(x - z_2, S_0(z_2)), z_2)|z_1 = z]\)

并且我们看到 \(G_1(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)。通过归纳我们检查 \(u_n(x, z)\)、\(G_n(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)。

此外

\(G'_n(x, z) = c - p\bar{F}(x|z) + \alpha E[u'_n(x - z_2, z_2)\mathbb{1}_{x \ge z_2}|z_1 = z]\)

我们看到 \(G'_n(0, z) = c - p\) 并且可以检查 \(G'_n(+\infty, z) = c + h\alpha \frac{1-\alpha^n}{1-\alpha}\)。因此存在一点 \(S_n(z)\) 使得 \(G'_n(S_n(z), z) = 0\)。注意 \(S_n(z) > 0\)，因为 \(G'_n(0, z) = c - p < 0\)。我们有

\(u_{n+1}(x, z) = \begin{cases} (h-c)x + G_n(S_n(z), z), & \text{若 } x \le S_n(z) \\ (h-c)x + G_n(x, z), & \text{若 } x \ge S_n(z) \end{cases}\)

由此可知极限 \(u(x, z)\) 在 \(x\) 上是凸的。显然当 \(x \to +\infty\) 时，\(u(x, z) \to +\infty\)。

此外

\(G(x, z) = cx + pE[(x - z_2)^-|z_1 = z] + \alpha E[u((x - z_2)^+, z_2)|z_1 = z]\)

它是凸的，并且当 \(x \to +\infty\) 时趋于 \(+\infty\)。因此最小值在 \(S(z)\) 处取得，可以通过取最小的最小值来唯一地定义。

由于 \(h-c \le u'_n(x, z) \le \frac{h}{1-\alpha}\)，我们可以断言 \(u(x, z)\) 在 \(x\) 上是 Lipschitz 连续的。对 \(G(x, z)\) 也是如此。但是

\(G'(x, z) = c - p\bar{F}(x|z) + \alpha E[u'(x - z_2, z_2)\mathbb{1}_{x \ge z_2}|z_1 = z] \to c - p \text{ as } x \to 0\)

因此也有 \(S(z) > 0\)。然后，根据凸性

\(u(x, z) = \begin{cases} (h-c)x + G(S(z), z), & \text{若 } x \le S(z) \\ (h-c)x + G(x, z), & \text{若 } x \ge S(z) \end{cases}\)

接下来，从

\(c - p\bar{F}(S_n(z)|z) + \alpha E[u'_n(S_n(z) - z_2, z_2)\mathbb{1}_{S_n(z) > z_2}|z_1 = z] = 0\)

我们推导，使用对 \(u'_n\) 的估计和性质

\(\bar{F}(S_n(z)|z) \le \frac{c_2 + c_1}{S_n(z)}\)

得出

(12.2.21) \(S_n(z) \le \frac{(c_2 + c_1)(p + \alpha(h - c))}{c + \alpha(h - c)}.\)

同样的估计对 \(S(z)\) 也成立。可以轻松检查 \(S_n(z) \to S(z)\)，并且 \(S(z)\) 是 \(G(x, z)\) 在 \(x\) 上的最小最小值。此外，根据 \(G(x, z)\) 在两个自变量上的连续性性质，我们可以检查 \(S(z)\) 是一个连续函数。由 (12.5.12) 定义的反馈 \(\hat{v}(x, z)\) 在两个自变量上也是连续的。定义

\(\chi(x, z) = u'(x, z) - h + c\)

作为 \(B\)（\(R^+ \times R^+\) 上可测有界函数空间）的一个元素，那么 \(\chi\) 是 \(B\) 中方程的唯一解

(12.2.22) \(\chi(x, z) = g(x + \hat{v}(x, z), z) + \alpha E[\chi(x + \hat{v}(x, z) - z_2, z_2) \mathbf{1}_{\hat{v}(x, z) > z_2} | z_1 = z], x, z \in R^+,\)

其中

\(g(x, z) = c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x|z).\)

由于函数 \(g(x + \hat{v}(x, z), z)\) 在 \(x, z\) 对上是连续的，解 \(\chi(x, z)\) 也是连续的。

让我们检查 \(S(z)\) 是一致连续的。让我们首先检查

(12.2.23) \((G'(x_1, z) - G'(x_2, z))(x_1 - x_2) \ge (p - \alpha(c - h))(F(x_1|z) - F(x_2|z))(x_1 - x_2).\)

假设，为了明确起见，\(x_1 > x_2\)。我们有

\((G'(x_1, z) - G'(x_2, z))(x_1 - x_2) = p(F(x_1|z) - F(x_2|z))(x_1 - x_2) + \alpha E[(u'(x_1 - z_2, z_2) - u'(x_2 - z_2, z_2))(x_1 - x_2) \mathbf{1}_{z_2 < x_1} | z_1 = z] + \alpha E[u'(x_1 - z_2, z_2) \mathbf{1}_{x_2 < z_2 \le x_1} (x_1 - x_2) | z_1 = z]\)

第二项来自 \(u\) 的凸性而为正。使用对 \(u'\) 的左估计对最后一项，我们推导出 (12.2.23)。我们然后得到

\((S(z) - S(z'))(G'(S(z), z') - G'(S(z'), z)) \ge (p - \alpha(c - h))(S(z) - S(z')) \left[ \int_{S(z')}^{S(z)} (f(\xi|z) + f(\xi|z')) d\xi \right]\)

如果 \(z, z' < m\)，那么从 (12.2.21) 我们可以找到 \(M_m > m\) 使得 \(S(z), S(z') < M_m\)。根据假设 (12.2.19)，我们推导出

\((S(z) - S(z'))(G'(S(z), z') - G'(S(z'), z)) \ge 2a_0(M_m)(p - \alpha(c - h))(S(z) - S(z'))^2\)

接下来我们有

\(G'(x, z') - G'(x, z) = \int_0^x (p + \alpha u'(x - \zeta, \zeta))(f(\zeta|z') - f(\zeta|z)) d\zeta,\)

因此

\(|G'(x, z') - G'(x, z)| \le xC \sup_{0 < \zeta < x} |f(\zeta|z') - f(\zeta|z)|.\)

将此估计应用于 \(x = S(z)\) 和 \(x = S(z')\) 并结合估计，我们很容易得到 \(S(z)\) 是一致连续的。由此可知反馈 \(\hat{v}(x, z)\) 是一致连续的。然后从 (12.2.22)，我们得到 \(\chi(x, z)\) 是一致连续的。证明已完成。

### **注释 12.1.** 我们有 \(\chi(x, z) = 0, \forall x \le S(z)\)，并且

(12.2.24) \(\chi(x, z) = g(x, z) + \alpha E[\chi(x - z_2, z_2) \mathbf{1}_{x > z_2} | z_1 = z], \forall x \ge S(z)\)

此外

(12.2.25) \(0 = g(S(z), z) + \alpha E[\chi(S(z) - z_2, z_2) \mathbf{1}_{S(z) > z_2} | z_1 = z].\)

所以 \(S(z)\) 不是 \(g(S(z), z) = 0\) 的解。如果我们考虑函数

$G^*(x, z) = (p + \alpha(h - c))E[(x - z_2)^+|z_1 = z] - (p - c)x + pE[z_2|z_1 = z]$,

那么 \(g(S, z) = 0\) 的解记为 \(S^*(z)\)。我们有 \(G(x, z) \ge G^*(x, z)\)。

## 12.2.3. 遍历理论。

我们现在转向 \(\alpha \to 1\) 的情况。我们写 \(u_\alpha(x, z)\) 以满足

(12.2.26) 
$$u_\alpha(x, z) = \begin{cases} (h - c)x + cS_\alpha(z) + pE[(S_\alpha(z) - z_2)^-|z_1 = z] + \alpha E[u_\alpha((S_\alpha(z) - z_2)^+, z_2)|z_1 = z], & \text{若 } x \le S_\alpha(z) \\ hx + pE[(x - z_2)^-|z_1 = z] + \alpha E[u_\alpha((x - z_2)^+, z_2)|z_1 = z], & \text{若 } x \ge S_\alpha(z) \end{cases}$$

我们将做出以下假设

(12.2.27) 
$$c_0 = 0, \text{ 且 } \inf_{0 \le \zeta \le a} f(\zeta|z) \ge \gamma(a) > 0, \forall a$$

(12.2.28) 
$$f(\zeta|z) \text{ 是遍历的}$$

(12.2.29) 
$$\int |f(\zeta|z) - f(\zeta|z')| d\zeta \le \delta|z - z'| \quad \sup_z F(x|z) = \delta_0(x) < 1, \forall x$$

我们用 \(\varpi(z)\) 表示与马尔可夫链 \(f(\zeta|z)\) 对应的不变概率密度。

我们陈述

### **定理 12.3.** 我们假设 (12.2.1)、(12.2.2)（其中 \(c_0 = 0\)）、(12.2.6)（其中 \(p > c\)）以及 (12.2.27)、(12.2.28)、(12.2.29)。那么，对于收敛到 1 的一个子序列（仍记为 \(\alpha\)），我们有，对于 \(R^+\) 的任何紧集 \(K\)

(12.2.30) 
$$\sup_{z \in K} |S_\alpha(z) - S(z)| \le \epsilon(\alpha, K), \quad \epsilon(\alpha, K) \to 0, \text{ as } \alpha \uparrow 1$$

(12.2.31) 
$$\sup_{\substack{x \le M \\ z \le N}} \left| u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} - u(x, z) \right| \to 0, \forall M, N,$$

其中 \(\rho_\alpha \to \rho\) 并且

(12.2.32) 
$$u(x, z) + \rho = \begin{cases} (h - c)x + cS(z) + pE[(S(z) - z_2)^-|z_1 = z] + E[u((S(z) - z_2)^+, z_2)|z_1 = z] & \text{若 } x \le S(z) \\ hx + pE[(x - z_2)^-|z_1 = z] + E[u((x - z_2)^+, z_2)|z_1 = z] & \text{若 } x \ge S(z) \end{cases}$$

函数 \(u(x, z)\) 满足增长条件

(12.2.33) 
$$\sup_{\substack{\xi \le x \\ z}} |u(\xi, z)| \le C_0 + \frac{C_1 x}{1 - \delta_0(x)}.$$




它在 $x$ 上是 $C^1$ 的，在 $z$ 上是 Lipschitz 连续的。以下估计成立

(12.2.34)
\[
\begin{aligned}
\sup_{\xi \le x} \frac{|u(\xi, z)|}{z} &\le \frac{C}{1 - \delta_0(x)}, \\
|u(x,z) - u(x,z')| &\le \left[ C_0(m_0) + \frac{C_1(m_0)x}{1 - \delta_0(x)} \right] |z - z'|.
\end{aligned}
\]

(12.2.35)
\[
\begin{aligned}
(1 - \delta_0(x)) \sup_{\xi \le x} \frac{|u_{xx}(\xi, z)|}{z} &\le C, \\
(1 - \delta_0(x)) \sup_{\xi \le x} \frac{|u_{xz}(\xi, z)|}{z} &\le C, \quad \text{a.e.}
\end{aligned}
\]

给定 $S(z)$，满足上述条件且 $\int u(0,z)\varpi(z)dz = 0$ 的对 $u(x,z)$、$\rho$ 是唯一确定的。

另外

(12.2.36)
\[
u(x,z) + \rho = \inf_{v \ge 0} [l(x, z+v) + \Phi'' u(x,z)].
\]

### 证明

我们从 (12.2.30) 开始。首先注意到，由于 $c_0 = 0$，我们有

(12.2.37)
\[
S_\alpha(z) \le \frac{c_1(p+h)}{\min(h,c)} = m_0.
\]

我们继续使用定理 12.2 中获得的估计。首先，我们有

\[
(S_\alpha(z) - S_\alpha(z'))(G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z'), z)) \ge 2 \min(h,c)\gamma(m_0)(S_\alpha(z) - S_\alpha(z'))^2
\]

我们知道 $u_\alpha(x,z)$ 在 $x$ 上是 $C^1$ 的。然后，根据 (12.2.26)，我们有（记 $u'_\alpha(x,z)$）

\[
u'_\alpha(x,z) = h - c \quad \text{if } x < S_\alpha(z), \qquad
u'_\alpha(x,z) = h - p\bar{F}(x) + \alpha E[u'_\alpha(x-z_2, z_2) \mathbb{1}_{x>z_2} \mid z_1 = z] \quad \text{if } x > S_\alpha(z)
\]

由此我们可以断言

(12.2.38)
\[
\sup_{\xi \le x} \frac{|u'_\alpha(\xi, z)|}{z} \le \frac{\max(h,p)}{1 - \delta_0(x)}.
\]

因此

\[
|G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z), z)| = \left( p + \frac{\max(h,p)}{1 - \sup_z F(m_0 z)} \right) \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta,
\]

\[
|G'_\alpha(S_\alpha(z'), z') - G'_\alpha(S_\alpha(z'), z)| = \left( p + \frac{\max(h,p)}{1 - \sup_z F(m_0 z)} \right) \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta.
\]

汇总结果，我们得到估计

(12.2.39)
\[
|S_\alpha(z) - S_\alpha(z')| \le \frac{p + \max(h,p)}{\min(h,c)\gamma(m_0)} \frac{1}{1 - \delta_0(m_0)} \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta,
\]

并且根据第一个假设 (12.2.29)，我们最终得到

(12.2.40)
\[
|S_\alpha(z) - S_\alpha(z')| \le \frac{p + \max(h, p)}{\min(h, c)\gamma(m_0)} \delta |z - z'|.
\]

因此，序列 $S_\alpha(z)$ 是一致 Lipschitz 连续的。可以提取一个子序列，它在紧集上的连续函数空间中收敛到一个函数 $S(z)$，这是标准的（参见附录 A.4），对于任何紧集 $K$ 都成立。因此 (12.2.30) 得到满足。

定义 $\chi_\alpha(x, z) = u'_\alpha(x, z) - h + c$。我们有

(12.2.41)
\[
\begin{aligned}
\chi_\alpha(x, z) &= g_\alpha(x, z) \\
&\quad + \alpha E[\chi_\alpha(x - 2z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \quad x > S_\alpha(z) \\
&= 0, \qquad x \le S_\alpha(z)
\end{aligned}
\]

其中

(12.2.42)
\[
g_\alpha(x, z) = (c + \alpha(h - c) - (p + \alpha(h - c))F(x|z).
\]

如同对 $u'_\alpha(x, z)$ 所做的那样，我们可以断言

(12.2.43)
\[
\sup_{0 \le \xi \le z} |\chi_\alpha(\xi, z)| \le \frac{\max(h, p)}{1 - \delta_0(x)}.
\]

如果我们考虑 $\psi_\alpha(x, z) = \chi'_\alpha(x, z) = u''_\alpha(x, z)$，那么利用 $\chi_\alpha(0, z) = 0$ 这一事实，我们看到

(12.2.44)
\[
\begin{aligned}
\psi_\alpha(x, z) &= (p + \alpha(h - c))f(x|z) \\
&\quad + \alpha E[\psi_\alpha(x - 2z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \quad x > S_\alpha(z) \\
&= 0, \qquad x < S_\alpha(z)
\end{aligned}
\]

函数 $\psi_\alpha(x, z)$ 不是连续的，但它是可测且有界的。我们有

(12.2.45)
\[
\sup_{0 \le \xi \le x} |\psi_\alpha(\xi, z)| \le \frac{((h - c)^+ + p)\|f\|}{1 - \delta_0(x)},
\]

其中 $\|f\| = \sup_{x,z} f(x|z)$。

接下来，我们对 $\chi_\alpha(x, z) - \chi_\alpha(x, z')$ 进行估计。首先假设 $x > S_\alpha(z), x > S_\alpha(z')$。那么，根据 (12.2.41)，我们有

\[
\begin{aligned}
\chi_\alpha(x, z) - \chi_\alpha(x, z') &= g_\alpha(x, z) - g_\alpha(x, z') \\
&\quad + \alpha \int_0^x \chi_\alpha(x - \zeta, \zeta)(f(\zeta|z) - f(\zeta|z')) \, d\zeta.
\end{aligned}
\]

根据估计 (12.2.43) 和第一个假设 (12.2.29)，我们推断

\[
|\chi_\alpha(x, z) - \chi_\alpha(x, z')| \le \left(p + (h - c)^+ + \frac{\max(h, p)}{1 - \delta_0(x)}\right) \delta |z - z'|,
\qquad x > S_\alpha(z), \; x > S_\alpha(z').
\]

现在，为了明确起见，假设 $S_\alpha(z') > x > S_\alpha(z)$。那么 $\chi_\alpha(x, z') = 0$ 且

\[
0 = g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(S_\alpha(z) - 2z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z].
\]

因此

\[
\begin{aligned}
\chi_\alpha(x, z) - \chi_\alpha(x, z')
&= g_\alpha(x, z) - g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \\
&\quad - \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] \\
&= (p + \alpha(h - c))(F(x|z) - F(S_\alpha(z)|z)) \\
&\quad + \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2 > S_\alpha(z)} \mid z_1 = z] \\
&\quad + \alpha E[(\chi_\alpha(x - z_2, z_2) - \chi_\alpha(S_\alpha(z) - z_2, z_2)) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z].
\end{aligned}
\]

由此可得

\[
\begin{aligned}
|\chi_\alpha(x, z) - \chi_\alpha(x, z')|
&\le \left[ p + (h - c)^+ + \frac{\max(h, p)}{1 - \delta_0(x)} + \frac{(h - c)^+ + p}{1 - \delta_0(x)} \right] f(\|x - S_\alpha(z)\|).
\end{aligned}
\]

最后，我们可以给出估计

(12.2.46)
\[
|\chi_\alpha(x, z) - \chi_\alpha(x, z')| \le \frac{C(m_0)}{1 - \delta_0(x)} \delta |z - z'|,
\]

其中 $C(m_0)$ 仅依赖于常数和 $m_0$。因此，考虑 $\chi_\alpha$ 在两个变量上的梯度，我们得到了估计

(12.2.47)
\[
|D\chi_\alpha(x, z)| \le \frac{C}{1 - \delta_0(x)}.
\]

根据这个估计，我们可以断言，对于一个子序列（仍记为 $\alpha$）

(12.2.48)
\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le N}} |\chi_\alpha(x, z) - \chi(x, z)| \to 0, \qquad \text{as } \alpha \to 0, \; \forall M, N.
\end{aligned}
\]

因此也

\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le M}} \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
\le \sup_{\substack{x \le M \\ z \le M}} \left| E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
+ (1 - \alpha) \frac{\max(h, p)}{1 - \delta_0(M)},
\end{aligned}
\]

并且

\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le M}} \left| E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
\le \sup_{\substack{x \le M \\ z \le N}} |\chi_\alpha(x, z) - \chi(x, z)| + 2 \frac{\max(h, p)}{1 - \delta_0(M)} \frac{c_1}{N},
\end{aligned}
\]

由此我们很容易推断

\[
\sup_{x \le M} \sup_z \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \to 0, \qquad \forall M.
\]

根据 (12.2.41)，可得

\[
\chi(x, z) = g(x, z) + E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \qquad \forall x > S(z),
\]

其中

(12.2.49)
\[
g(x, z) = h - (p - h + c)\bar{F}(x|z).
\]

另外，如果 $x < S(z)$，则 $\chi(x,z)=0$。而且，根据

\[
0 = g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z]
\]

和

\[
\begin{aligned}
&\left| \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] - E[\chi(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] \right| \\
&\quad \le \sup_{x \le M} \sup_z \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right|
\end{aligned}
\]

\[
\begin{aligned}
&\left| E[\chi(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] - E[\chi(S(z) - z_2, z_2) \mathbb{1}_{S(z) > z_2} \mid z_1 = z] \right| \\
&\quad \le \frac{(h - c + p)\|f\|_1}{1 - \delta_0(m_0)} |S_\alpha(z) - S(z)| + \frac{2 \max(h, p)}{1 - \delta_0(m_0)} |F(S_\alpha(z)|z) - F(S(z)|z)|
\end{aligned}
\]

我们很容易得到

\[
0 = g(S(z), z) + E[\chi((S(z) - z_2)^+, z_2) \mid z_1 = z],
\]

并且函数 $\chi(x, z)$ 在 $x$ 上是连续的。

接下来，我们设

\[
\Gamma_\alpha(z) = u_\alpha(0, z), \qquad G_\alpha(z) = E[(S_\alpha(z) - z_2)^- \mid z_1 = z],
\]

然后，从第一个方程 (12.2.26) 可以验证

\[
\Gamma_\alpha(z) = cS_\alpha(z) + pG_\alpha(z) + \alpha E[u_\alpha(S_\alpha(z) - z_2, z_2)^+ \mid z_1 = z] = \Psi_\alpha(z) + \alpha E[\Gamma_\alpha(z_2) \mid z_1 = z].
\]

其中

\[
\Psi_\alpha(z) = cS_\alpha(z) + pG_\alpha(z) + \alpha E\left[\int_0^{(S_\alpha(z) - z_2)^+} (h - c + \chi(\xi, z_2)) \, d\xi \,\middle|\, z_1 = z\right],
\]

并且

\[
0 \le \Psi_\alpha(z) \le \left[\max(h, c) + \frac{\max(h, p)}{1 - \delta_0(m_0)}\right] m_0 + pc_1.
\]

这个估计对于极限也成立

\[
\Psi(z) = cS(z) + pG(z) + E\left[\int_0^{(S(z) - z_2)^+} (h - c + \chi(\xi, z_2)) \, d\xi \,\middle|\, z_1 = z\right]
\]

其中

\[
G(z) = E[(S(z) - z_2)^- \mid z_1 = z].
\]


定义

$$\rho = \int \Psi(z) \varpi(z) dz.$$

现在考虑方程

$$\Gamma(z) + \rho = \Psi(z) + E[\Gamma(z_2)|z_1 = z], \quad \int \Gamma(z) \varpi(z) dz = 0.$$

根据遍历理论，参见第3章，定理3.3，我们可以断言

$$\sup_z |\Gamma(z)| \le \sup_z |\Psi(z) - \rho| \frac{3-\beta}{1-\beta},$$

其中 \(0 < \beta < 1\)，仅取决于马尔可夫链。同样，如果我们设置

$$\rho_\alpha = \int \Psi_\alpha(z) \varpi(z) dz, \quad \bar{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha},$$

我们可以写成

$$\bar{\Gamma}_\alpha(z) + \rho_\alpha = \Psi_\alpha(z) + \alpha E[\bar{\Gamma}_\alpha(z_2)|z_1 = z],$$

我们也可以断言

$$\sup_z |\bar{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3-\beta}{1-\beta} \le 2 \left[ \left( \max(h, c) + \frac{\max(h, p)}{1-\delta(m_0)} \right) m_0 + pc_1 \right] \frac{3-\beta}{1-\beta}$$

此外

$$\bar{\Gamma}_\alpha(z) - \bar{\Gamma}_\alpha(z') = \Psi_\alpha(z) - \Psi_\alpha(z') + \alpha \int \bar{\Gamma}_\alpha(\zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta.$$

使用性质 (12.2.40)、(12.2.43) 和假设 (12.2.29)，我们可以验证

$$|\Psi_\alpha(z) - \Psi_\alpha(z')| \le C(m_0) \delta |z - z'|,$$

因此也有

$$|\bar{\Gamma}_\alpha(z) - \bar{\Gamma}_\alpha(z')| \le C_1(m_0) \delta |z - z'|.$$

因此函数 \(\bar{\Gamma}_\alpha(z)\) 是一致 Lipschitz 连续且有界的。因此对于一个子序列我们得到

(12.2.50) $$\sup_{0 \le z \le N} \left| \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha} - \Gamma(z) \right| \to 0, \forall M$$

因此，也有

(12.2.51) $$\sup_{\substack{0 \le x \le M \\ 0 \le z \le N}} \left| u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha} - u(x, z) \right| \to 0, \forall x, \forall M, N$$

其中

(12.2.52) $$u(x, z) = (h - c)x + \int_0^x \chi(\xi, z) d\xi + \Gamma(z).$$

我们推导出

(12.2.53) $$u(x, z) = (h - c)x + \Gamma(z), \forall x \le S(z).$$

从 (12.2.50)、(12.2.51) 可以清楚地看出

(12.2.54) $$\Gamma(z) = u(0, z).$$

然而

$$E[u((S(z)-z_2)^+, z_2)|z_1 = z]$$
$$= E[u(0, z_2)|z_1 = z] + E \left[ \int_0^{(S(z)-z_2)^+} (h - c + \chi(\xi, z_2)) d\xi | z_1 = z \right],$$

因此

$$\Gamma(z) = -\rho + cS(z) + \rho G(z) + E[u((S(z)-z_2)^+, z_2)|z_1 = z],$$

因此第一个关系 (12.2.32) 得证。

现在考虑 \(x \ge S(z)\) 的情况。定义函数

$$\tilde{u}(x, z) = hx + pE[(x - z_2)^-|z_1 = z] + E[u((x - z_2)^+, z_2)|z_1 = z].$$

我们得到

$$\tilde{u}'(x, z) = h - p\bar{F}(x) + E[u'(x - z_2, z_2) 1_{x > z_2}|z_1 = z]$$
$$= h - c + \chi(x, z), \quad x \ge S(z).$$

同样

$$\tilde{u}(S(z), z) = hS(z) + pE[(S(z) - z_2)^-|z_1 = z] + \Gamma(z)$$
$$= u(S(z), z) + \rho.$$

从这两个关系我们得到 \(\tilde{u}(x, z) = u(x, z) + \rho, \forall x \ge S(z)\)。

这完成了 (12.2.32) 的第二部分。还要注意

$$u_\alpha(x, z) - u_\alpha(x, z') = \Gamma_\alpha(z) - \Gamma_\alpha(z') + \int_0^x (\chi_\alpha(\xi, z) - \chi_\alpha(\xi, z')) d\xi.$$

使用已证明的估计我们得到

$$|u_\alpha(x, z) - u_\alpha(x, z')| \le \left[ C_0(m_0) + \frac{C_1(m_0)x}{1 - \delta_0(x)} \right] |z - z'|$$

极限 \(u(x, z)\) 满足所有估计 (12.2.34)、(12.2.35)。

为了证明 (12.2.36)，我们首先检查

$$u_\alpha(x, z) \le l(x, z, v) + \alpha E[u_\alpha(x + v - z_2)^+, z_2)|z_1 = z], \forall x, z, v$$

因此，很容易得出

$$u(x, z) + \rho \le l(x, z, v) + E[u((x + v - z_2)^+, z_2)|z_1 = z], \forall x, z, v$$

然而 (12.2.36) 可以读作

$$u(x, z) + \rho = l(x, z, \hat{v}(x, z)) + E[u((x + \hat{v}(x, z) - z_2)^+, z_2)|z_1 = z], \forall x, z$$

其中

$$\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{if } x \le S(z) \\ 0, & \text{if } x > S(z) \end{cases}$$

结合我们得到方程 (12.2.36)。

让我们证明唯一性，对于给定的 \(S(z)\)。我们首先证明 \(\chi(x, z)\) 是唯一确定的。要证明这一点，只需证明如果

$$\chi(x, z) = \begin{cases} E[\chi(x - z_2, z_2) 1_{x > z_2}|z_1 = z], & \forall x > S(z) \\ 0, & \forall x \le S(z) \end{cases}$$

并且

$$(1 - \delta_0(x)) \sup_{0 \le \xi \le z} |\chi(\xi, z)| < \infty,$$

那么 \(\chi(x, z) = 0\)。这很明显。因此函数 \(\Psi(z)\) 是唯一确定的。因此对 \(\rho, \Gamma(z) = u(0, z)\) 也是唯一确定的，条件是 \(\int \Gamma(z) \varpi(z) dz = 0\)。因此 \(u(x, z)\) 也是唯一确定的。定理的证明已完成。

**示例 12.1。** 考虑独立需求的情况，那么 \(f(x|z) = f(x)\)。在这种情况下 \(\varpi(x) = S\)，并且

$$\rho = (p + h - c)E(S - D)^+ - (p - c)S + p\bar{D}$$

我们恢复了第6章的公式 (6.2.4)。我们还看到 \(\Psi(z) = \rho\)，因此 \(\Gamma(z) = 0\)。

接下来考虑情况

$$f(x|z) = \lambda(z) \exp(-\lambda(z)x),$$

在假设 \(0 < \lambda_0 \le \lambda(z) \le \lambda_1\) 下。我们还假设 \(\lambda(z)\) 是 Lipschitz 连续的。那么定理 12.3 的所有假设都满足。

我们转向对数 \(\rho\) 的解释。考虑与基础库存 \(S(z)\) 相关的反馈 \(\hat{v}(x, z)\)。定义受控过程

$$\hat{y}_{n+1} = (\hat{y}_n + \hat{v}_n - z_{n+1})^+, \hat{v}_n = \hat{v}(\hat{y}_n, z_n),$$

其中 \(\hat{y}_1 = x, z_1 = z\)。我们定义策略 \(\hat{V} = (\hat{v}_1, \cdots, \hat{v}_n, \cdots)\)。我们考虑平均成本

$$J_{x,z}^n(\hat{V}) = \frac{\sum_{j=1}^n E[l(\hat{y}_j, z_j, \hat{v}_j)]}{n}.$$

同样，对于任何策略 \(V = (v_1, \cdots, v_n \cdots)\) 我们定义平均成本

$$J_{x,z}^n(V) = \frac{\sum_{j=1}^n E[l(y_j, z_j, v_j)]}{n},$$

其中

$$y_{n+1} = (y_n + v_n - z_{n+1})^+, y_1 = x, z_1 = z.$$

我们陈述

**命题 12.1。** 我们具有性质

$$\rho = \lim_{n \to \infty} J_{x,z}^n(\hat{V}). \tag{12.2.55}$$

此外，考虑策略集

$$\mathcal{U} = \{V \in \mathbb{V} | E|u(y_n, z_n)| \le C_x\},$$

那么我们有

$$\rho = \inf_{V \in \mathcal{U}} \lim_{n \to \infty} J_{x,z}^n(V). \tag{12.2.56}$$

**证明。** 我们首先注意到

\(\hat{y}_n \le \max(x, m_0).\)

因此，从估计 (12.2.33) 我们得到

\(|u(\hat{y}_n, z_n)| \le C_0 + \frac{C_1 \max(x, m_0)}{1 - \delta_0(\max(x, m_0))}.\)

因此 \(\hat{V}\) 属于 \(\mathcal{U}\)。从 (12.2.36) 我们可以写成

\(u(\hat{y}_n, z_n) + \rho = l(\hat{y}_n, z_n, v_n) + E[u(\hat{y}_{n+1}, z_{n+1})|\hat{y}_n, z_n].\)

取期望并求和我们得到

\(\rho = J_{x,z}^n(\hat{V}) + \frac{E u(\hat{y}_{n+1}, z_{n+1}) - u(x, z)}{n},\)

因此性质 (12.2.55) 立即得出。同样，对于任何策略我们可以写成

\(\rho \le J_{x,z}^n(V) + \frac{E u(y_{n+1}, z_{n+1}) - u(x, z)}{n}.\)

因此，如果 \(V \in \mathcal{U}\)，我们有 \(\rho \le J_{x,z}^n(V)\)。这意味着 (12.2.56)。证明已完成。

**注 12.2。** 我们不能断言过程 \(\hat{y}_n, z_n\) 是遍历的。我们确实不能应用第3章定理3.3的性质 (3.5.5)。因此，我们无法对函数 \(u(x, z)\) 本身给出解释。

## 12.3. 积压和无设置成本

### 12.3.1. 模型。

我们在这里考虑允许积压的情况。这相当于第5章，第5.2节。表示需求的马尔可夫链保持不变。转移概率是 \(f(\zeta|z)\)。我们回顾

(12.3.1) \(f(\zeta|z)\) 在两个变量中一致连续且有界

(12.3.2) \(\int_0^{+\infty} \zeta f(\zeta|z) d\zeta \le c_0 z + c_1.\)

我们定义过滤

\(\mathcal{F}^n = \sigma(z_1, \cdots, z_n).\)

一个控制策略，记为 \(V\)，是随机变量序列 \(v_n\)，使得 \(v_n\) 是 \(\mathcal{F}^n\) 可测的。当 \(z_1 = z\) 时，\(v_1\) 是确定的。同样，我们像往常一样假设 \(v_n \ge 0\)。接下来我们将库存定义为序列，

(12.3.3) \(y_{n+1} = y_n + v_n - z_{n+1}, \quad y_1 = x.\)

过程 \(y_n\) 关于过滤 \(\mathcal{F}^n\) 是自适应的。联合过程 \(y_n, z_n\) 也是一个马尔可夫链。

我们可以写，对于测试函数 \(\varphi(x, z)\)（在 \(R \times R^+\) 上有界连续）

\(E[\varphi(y_2, z_2)|y_1 = x, z_1 = z, v_1 = v] = E[\varphi(x + v - z_2, z_2)|z_1 = z]\)
\(= \int_0^{\infty} \varphi(x + v - \zeta, \zeta) f(\zeta|z) d\zeta\)




这定义了一个与以下算子相关的马尔可夫链

(12.3.4) 
\(\Phi^v \varphi(x, z) = \int_0^\infty \varphi(x + v - \zeta, c) f(\zeta | z) d\zeta,\)

因此过渡概率由以下给出

(12.3.5) 
\(\pi(x, z, v; d\xi, d\zeta) = \delta(\xi - (x + v - \zeta)) \otimes f(\zeta | z) d\zeta.\)

接下来我们定义函数

(12.3.6) 
\(l(x, v) = cv + hx^+ + px^-,\)

它将用于建模单期成本。成本函数则为

(12.3.7) 
\(J_{x,z}(V) = E \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n).\)

我们关心的值函数为

(12.3.8) 
\(u(x, z) = \inf_V J_{x,z}(V).\)

我们再次注意到性质 (4.31)、(4.32) 得到满足。为继续，我们需要指定一个上限函数。它对应于恒等为 0 的控制。令 \(l_v(x) = l(x, v)\)。请注意不等式

\(\Phi^{x+} u^+(x, z) \le x^+, \quad \Phi^{x-} u^-(x, z) \le x^- + c_0 z + c_1.\)

很容易验证

(12.3.9) 
\((\Phi^0)^n x^+(x, z) \le x^+,\)

(12.3.10) 
\((\Phi^0)^n x^-(x, z) \le x^- + c_0 z \frac{1-c_0^n}{1-c_0} + (n - c_0(n+1) + c_0^{n+1}) \frac{c_1}{(1-c_0)^2}.\)

接下来考虑函数

(12.3.11) 
\(w_0(x, z) = \sum_{n=1}^\infty \alpha^{n-1} (\Phi^0)^{n-1} l_0(x)\)

### 引理 12.2.

我们假设

(12.3.12) 
\(\alpha c_0 < 1,\)

则级数 \(w_0(x, z) < \infty\)，更精确地说

(12.3.13) 
\(u_0(x, z) \le \frac{hx^+ + px^-}{1 - \alpha} + \frac{p c_0 z \alpha}{(1 - c_0 \alpha)(1 - \alpha)} + \frac{p c_1}{(1 - c_0)^2} \left( \frac{\alpha - c_0}{(1 - \alpha)^2} + \frac{c_0}{1 - \alpha c_0} \right).\)

证明. 这是公式 (13.2.10) 和 (12.3.9) 的直接结果。\(\square\)

接下来我们写出贝尔曼方程

(12.3.14) 
\(u(x, z) = \inf_{v \ge 0} [l(x, v) + \alpha \Phi^v u(x, z)].\)

我们陈述如下

### 定理 12.4.

我们假设 (13.2.1)、(12.3.2)、(12.3.6)、(13.2.11)。那么方程 (13.2.15) 存在唯一解，满足 \(0 \le u \le w_0\)。它是连续的，并与值函数 (12.3.8) 重合。存在一个最优反馈 \(v(x, z)\) 和一个最优控制策略 \(\bar{V}\)。

证明. 我们首先注意到定理 4.4 和 4.3 的条件得到满足。因此方程 (13.2.15) 的解集非空。它存在最小解和最大解。最小解是下半连续的，最大解是上半连续的。最小解与值函数重合。存在一个最优反馈 \(\hat{v}(x, z)\) 和一个最优控制策略 \(\hat{V}\)。为证明唯一性，我们需要证明最小解和最大解重合。我们首先从对 \(\hat{v}(x, z)\) 的界限开始证明。由 (13.2.15)，考虑 \(\underline{w}\)，即最小解，我们可以断言

(12.3.15) 
\(\underline{w}(x, z) \ge \frac{hx^+}{1-\alpha} + px^- - \frac{\alpha h c_0 z}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha h c_1}{(1-\alpha)^2},\)

这由 \(l(x, v) \ge hx^+ + px^-\) 得出，并且

(12.3.16) 
\(\Phi^{l,v}(x, z) \ge \Phi^{0,v}(x, z), \forall v \ge 0, \forall \varphi \text{ increasing in } x,\)

这意味着

\(\alpha E[\underline{w}(x+v-z_2, z_2)|z_1=z]\)
\(\ge \frac{\alpha h}{1-\alpha} E[(x-z_2)^+|z_1=z] - \frac{\alpha^2 h c_0 (c_0 z + c_1)}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha^2 h c_1}{(1-\alpha)^2}\)
\(\ge \frac{\alpha h}{1-\alpha} (x^+ - c_0 z - c_1) - \frac{\alpha^2 h c_0 (c_0 z + c_1)}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha^2 h c_1}{(1-\alpha)^2}\)

并且 (13.2.40) 得出，再次使用 (13.2.15)。因此也

(12.3.17) 
\(l(x, v) + \alpha \Phi^{\underline{w}}(x, z) \ge cv + \frac{hx^+}{1-\alpha} + px^- - \frac{\alpha h c_0 z}{(1-\alpha)(1-\alpha c_0)} - \frac{\alpha h c_1}{(1-\alpha)^2}.\)

接下来我们引入函数 \(w(x, z)\)，它是以下方程的解

(12.3.18) 
\(w(x, z) = hx^+ + (c+p)x^- + \alpha E[w(x^+-z_2, z_2)|z_1=z],\)

它对应于反馈 \(v(x) = x^-\)。我们注意到 \(\underline{w}(x, z) \le w(x, z)\)。我们可以断言

(12.3.19) 
\(w(x, z) \le (c+p)x^- + \frac{hx^+}{1-\alpha} + L_0 z + L_1,\)

其中

\(L_0 = \frac{\alpha(c+p)c_0}{1-\alpha c_0}, \quad L_1 = \frac{\alpha c_1(c+p)}{(1-\alpha)(1-\alpha c_0)}\)

因此，在对 \(v\) 求最小值时，我们可以从上方界定 \(v\) 的范围。更精确地说，我们得到

(12.3.20) 
\(\hat{v}(x, z) \le x^- + \frac{\alpha c_0 z}{c(1-c_0 \alpha)} \left( c+p + \frac{h}{1-\alpha} \right) + c \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right).\)

我们考虑从最优反馈得到的最优轨迹 \(\hat{y}_n, z_n\)，即

\(\hat{y}_{n+1} = \hat{y}_n + \hat{v}_n - z_{n+1}, \hat{v}_n = \hat{v}(\hat{y}_n, z_n)\)

其中 \(\hat{y}_1 = x, z_1 = z\)。

为证明唯一性，只需证明

(12.3.21) 
\(\alpha^n E[\hat{y}_{n+1}] \to 0, \text{ as } n \to \infty.\)

我们有

\(\hat{y}_{n+1} \le \hat{y}_n + \hat{v}_n\)
\(\le \hat{y}_n^+ + \frac{\alpha c_0 z_n}{c(1-c_0 \alpha)} \left( c+p+\frac{h}{1-\alpha} \right) + \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right)\)

因此

\(E\hat{y}_{n+1}^+ \le E\hat{y}_n^+ + \frac{\alpha \left( c_0^2 z + c_1 \frac{c_0 - c_0^2}{1-c_0} \right)}{c(1-c_0 \alpha)} \left( c+p+\frac{h}{1-\alpha} \right)\)
\(+ \frac{\alpha c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right)\)

我们推导出估计

\(E\hat{y}_{n+1}^+ \le x^+ + \frac{\alpha c_0}{c(1-c_0 \alpha)} \left( z \frac{1-c_0^n}{1-c_0} + c_1 \frac{n}{1-c_0 \alpha} - c_1 \frac{1-c_0^n}{(1-c_0)^2} \right) \left( c+p+\frac{h}{1-\alpha} \right)\)
\(+ \frac{n c_1}{c(1-\alpha)} \left( \frac{h}{1-\alpha} + \frac{c+p}{1-c_0 \alpha} \right),\)

因此 \(\alpha^n E\hat{y}_{n+1}^+ \to 0\)，当 \(n \to +\infty\)。接下来

\(\hat{y}_{n+1} \ge \hat{y}_n - z_{n+1},\)

很容易得出

\(E\hat{y}_{n+1}^- \le x^- + c_0 z \frac{1-c_0^n}{1-c_0} + \frac{c_1}{1-c_0} \left( n - c_0 \frac{1-c_0^n}{1-c_0} \right),\)

我们得到 \(\alpha^n E\hat{y}_{n+1}^- \le x^- \to 0\)，当 \(n \to +\infty\)。证明完成。

## 12.3.2. 基准库存策略.

我们现在想验证最优反馈 \(\hat{v}(x, z)\) 可以通过基准库存策略得到，其中基准库存取决于 \(z\) 的值。我们有

### 定理 12.5.

我们做出定理 12.4 的假设，且 \(p\alpha > c(1 - \alpha)\)、\(h + p - c > 0\)。还假设

(12.3.22) \(f(x)z \ge a_0(M) > 0, \forall x, z \le M.\)

那么函数 \(u(x, z)\) 在自变量 \(x\) 上是凸的且为 \(C^1\)，除了 \(x = 0\) 处，那里存在左导数和右导数。此外，最优反馈由以下给出

(12.3.23) \(\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{if } x \le S(z) \\ 0, & \text{if } x \ge S(z) \end{cases}\)

其中 \(S(z) > 0\) 是一致连续的。

证明. 我们考虑递增过程

\(u_{n+1}(x, z) = \inf_{v \ge 0} [(f, v) + \alpha \Phi^n u_n(x, z)], \quad u_0(x) = 0\)

也可写成

\(u_{n+1}(x, z) = hx^+ + px^- - cx + \inf_{\eta \ge x} \{ c\eta + \alpha E[u_n(\eta - z_2, z_2)|z_1 = z] \}\)

我们递归地证明序列 \(u_n(x, z)\) 在 \(x\) 上是凸的且为 \(C^1\)，除了 \(x=0\)。我们首先有

(12.3.24) 
\(u_{n+1}(x, z) = hx^+ + px^- + \alpha E[u_n(x - z_2, z_2)|z_1 = z]\)

对于 \(0 \le n \le n_0\)，其中

\(\frac{\alpha p}{1 - \alpha}(1 - \alpha^{n_0+1}) > c > \frac{\alpha p}{1 - \alpha}(1 - \alpha^{n_0}).\)

确实，考虑由 (13.2.24) 定义的序列，我们有

\(u'_n(x, z) = -p \frac{1 - \alpha^n}{1 - \alpha}, \forall n \le n_0 + 1, \forall x < 0\)

因此 \(c - \alpha p \frac{1 - \alpha^n}{1 - \alpha} > 0\)，对所有 \(n \le n_0\) 成立，且函数 \(\alpha \eta + \alpha E[u_n(\eta - z_2, z_2)|z_1 = z]\) 是单调递增的，对所有 \(n \le n_0\) 成立。

定义

\(G_n(x, z) = cx + \alpha E[u_n(x - z_2, z_2)|z_1 = z],\)

那么函数 \(G_n(x, z)\) 对 \(n \le n_0\) 是单调递增的，并且对于 \(n = n_0 + 1\) 在 \(S_n(z) > 0\) 处取得其最小值，可以通过取最小的最小值来唯一确定。它是 \(C^1\) 且凸的（导数在 0 处连续，由数学期望的正则化效应）。

那么，对于 \(n \le n_0 + 1\)，我们有

\(u_{n+1}(x, z) = \left\{ \begin{array}{ll} hx^+ + px^- - cx + G_n(S_n(z), z) & \text{if } x \le S_n(z) \\ hx^+ + px^- - cx + G_n(x, z) & \text{if } x \ge S_n(z) \end{array} \right.\)

其中 \(S_n(z) = -\infty\)，对所有 \(n \le n_0\)。因此 \(u_n(x, z)\) 是 \(C^1\)，除了 \(x=0\)，且是凸的，对于 \(n \le n_0 + 2\)。通过递归，该性质对任何 \(n\) 都成立。

由此可知极限 \(u(x, z)\) 在 \(x\) 上是凸的。显然 \(u(x, z) \to +\infty\)，当 \(|x| \to +\infty\)。另外 \(S_n(z) > 0\)，对所有 \(n \ge n_0 + 1\)。而且

\(u'_n(x, z) = -p - c, \forall x < 0, \forall n \ge n_0 + 2\)

且 \(u'_n(x, z) \le \frac{h}{1 - \alpha}\)。因此极限 \(u(x, z)\) 在 \(x\) 上是 Lipschitz 连续的，并且

\(u'(x, z) = -p - c, \forall x < 0, \quad u'(x, z) \le \frac{h}{1 - \alpha}.\)

还

(12.3.25) 
\(-p - c \le u'(x, z) \le \frac{h}{1 - \alpha}.\)

函数

\(G(x, z) = cx + \alpha E[u(x - z_2, z_2)|z_1 = z],\)

是凸的，并且当 \(x \to +\infty\) 时趋向于 \(+\infty\)。对于 \(x < 0\)，我们有 \(G'(x, z) = c(1 - \alpha) - \alpha p < 0\)。因此 \(G(x, z)\) 的最小值在 \(S(z) > 0\) 处取得，可以通过取最小的最小值来唯一确定。

然后，由凸性

\(u(x, z) = \left\{ \begin{array}{ll} hx^+ + px^- - cx + G(S(z), z) & \text{if } x \le S(z) \\ hx^+ + px^- - cx + G(x, z) & \text{if } x \ge S(z) \end{array} \right.\)




事实上，我们可以写出比(12.3.25)左边更好的估计。

(12.3.26) \( u'(x, z) \ge h - c, \quad \text{if } x \ge 0. \)

因此也

\( G'(x, z) \ge c(1-\alpha) + \alpha h - \alpha(p+h)\bar{F}(x|z), \)

并且由于 \( S(z) \) 是最小值，我们得到

\( \bar{F}(S(z)|z) \ge \frac{c(1-\alpha) + \alpha h}{\alpha(p+h)} \)

这意味着

(12.3.27) \( 0 < S(z) < \frac{(c_0 z + c_1)\alpha(p+h)}{c(1-\alpha) + \alpha h}. \)

另外，函数 \( S(z) \) 是连续的，因此反馈 \( \hat{v}(x, z) \) 也是连续的。

如果我们定义

\( \chi(x, z) = u'(x, z) - h\mathbf{I}_{x>0} + p\mathbf{I}_{x<0} + c, \)

作为 \( B \)（\( R \times R^+ \) 上可测有界函数空间）的一个元素，那么 \( \chi \) 是方程在 \( B \) 中的唯一解

\( \chi(x, z) = g(x + \hat{v}(x, z), z) + \alpha E[\chi(x + \hat{v}(x, z) - z_2, z_2)|z_1 = z], \quad x \in R, z \in R^+ \)

其中

\( g(x, z) = c(1-\alpha) + \alpha h - \alpha(p+h)\bar{F}(x|z). \)

由于函数 \( g(x + \hat{v}(x, z), z) \) 在 \( x, z \) 对中是连续的，解 \( \chi(x, z) \) 也是连续的。

接下来我们证明 \( S(z) \) 是一致连续的。考虑 \( G'(x_1, z) - G'(x_2, z) \)，其中 \( x_1 \ge x_2 \ge 0 \)。我们有

G'(x_1, z) - G'(x_2, z)
= \alpha E[u'(x_1 - z_2, z_2) - u'(x_2 - z_2, z_2)|z_1 = z]
= \alpha E[u'(x_1 - z_2, z_2) \mathbf{I}_{x_1 - z_2 > 0} + u'(x_1 - z_2, z_2) \mathbf{I}_{x_1 - z_2 \le 0}
- u'(x_2 - z_2, z_2) \mathbf{I}_{x_2 - z_2 > 0} - u'(x_2 - z_2, z_2) \mathbf{I}_{x_2 - z_2 \le 0}|z_1 = z]
= \alpha E[(u'(x_1 - z_2, z_2) - u'(x_2 - z_2, z_2)) \mathbf{I}_{x_1 - z_2 > 0} + (u'(x_1 - z_2, z_2) - u'(x_2 - z_2, z_2)) \mathbf{I}_{x_1 - z_2 \le 0}
+ u'(x_1 - z_2, z_2) \mathbf{I}_{x_2 < z_2 \le x_1} |z_1 = z] + \alpha E[u'(x_1 - z_2, z_2) - u'(x_2 - z_2, z_2)) \mathbf{I}_{x_2 < z_2 \le x_1} |z_1 = z]
- u'(x_2 - z_2, z_2) \mathbf{I}_{x_1 - z_2 \le 0} - u'(x_2 - z_2, z_2) \mathbf{I}_{x_2 < z_2 \le x_1} |z_1 = z]
\ge \alpha(h+p)(F(x_1|z) - F(x_2|z)).

因此

(12.3.28) \( (G'(x_1, z) - G'(x_2, z))(x_1 - x_2) \ge \alpha(h+p)(F(x_1|z) - F(x_2|z))(x_1 - x_2). \)

我们可以轻易验证该公式对任意 \( x_1, x_2 \) 对成立。如同在定理 12.2 中推导的那样，对于 \( z, z' < m \) 且 \( S(z), S(z') < M_m \)（其中 \( M_m > m \)），以下关系成立

\( (G'(S(z), z') - G'(S(z'), z))(S(z) - S(z')) \ge 2\alpha(h+p)a_0(M_m)(S(z) - S(z'))^2. \)

接下来

G'(x, z) - G'(x, z')
= \alpha E[u'(x - z_2, z_2)|z_1 = z] - E[u'(x - z_2, z_2)|z_1 = z']
= (p + c)(F(x|z) - F(x|z')) + \int_0^{x^+} u'(x - \zeta, \zeta)(f(\zeta|z) - f(\zeta|z'))d\zeta,

因此

|G'(x, z) - G'(x, z')| \le Cx^+ \sup_{0 < \zeta < x^+} |f(\zeta|z) - f(\zeta|z')|

分别对 \(x = S(z)\) 和 \(x = S(z')\) 应用此不等式，并结合估计，我们推断出 \(S(z)\) 是一致连续的。证明完成。

## 12.3.3. Ergodic theory

我们现在转向 \(\alpha \to 1\) 的情况。我们将 \(u_\alpha(x, z)\) 写作如下

(12.3.29) \( u_\alpha(x, z) = \left\{ \begin{array}{ll} hx^+ + px^- - cx + cS_\alpha(z) & \text{if } x \le S_\alpha(z) \\ + \alpha E[u_\alpha(S_\alpha(z) - z_2, z_2)|z_1 = z] & \\ hx^+ + px^- & \text{if } x \ge S_\alpha(z) \\ + \alpha E[u_\alpha(x - z_2, z_2)|z_1 = z] & \end{array} \right. \)

我们做如下假设

(12.3.30) \(\begin{aligned} c_0 &= 0 \\ \inf_{0 \le \zeta \le a} f(\zeta|z) \ge \gamma(a) > 0, \forall a \end{aligned}\)

(12.3.31) \( f(\zeta|z) \text{ is ergodic} \)

(12.3.32) \(\begin{aligned} \int |f(\zeta|z) - f(\zeta|z')|d\zeta \le \delta|z - z'| \\ F(x|z) \le \delta_0(x) < 1, \forall x \end{aligned}\)

我们用 \(\varpi(z)\) 表示与马尔可夫链 \(f(\zeta|z)\) 对应的不变概率密度。

我们陈述

### 定理 12.6.

我们假设 (13.2.1)、(13.2.2)（其中 \(c_0 = 0\)）、(12.3.6)、(12.3.22) 以及 (12.3.30)、(12.3.31)、(12.3.32)。那么，对于收敛于 1 的一个子序列（仍记为 \(\alpha\)），我们有，对于 \(R^+\) 的任意紧集 \(K\)

(12.3.33) \(\sup_{z \in K} |S_\alpha(z) - S(z)| \le \epsilon(\alpha, K), \epsilon(\alpha, K) \to 0, \text{ as } \alpha \uparrow 1\)

(12.3.34) \(\sup_{x \le M, z \le N} | u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} - u(x, z) | \to 0, \forall M, N,\)

其中 \(\rho_\alpha \to \rho\) 且

(12.3.35)
$$
u(x, z) + \rho = \begin{cases} hx^+ + px^- - cx + cS(z) & \text{if } x \le S(z) \\ hx^+ + px^- + E[u(S(z) - z_2, z_2) | z_1 = z] & \text{if } x \ge S(z) \end{cases}
$$

函数 \(u(x, z)\) 满足增长条件

(12.3.36)
$$
\sup_{\xi \le x} |u(\xi, z)| \le C_0 + \frac{C_1 x}{1 - \delta_0(x)}.
$$

它在 \(x\) 中是 \(C^1\) 的，在 \(z\) 中是 Lipschitz 连续的。以下估计成立

(12.3.37)
$$
\sup_{\xi \le z} |u_x(\xi, z)| \le \frac{C}{(1 - \delta_0(x))},
$$

(12.3.38)
$$
|u(x, z) - u(x, z')| \le \left[ C_0(m_0) + \frac{C_1(m_0)x}{1 - \delta_0(x)} \right] |z - z'|
$$

(12.3.39)
$$
(1 - \delta_0(x)) \sup_{\xi \le z} |u_{xx}(\xi, z)| \le C, (1 - \delta_0(x)) \\
\sup_{\xi \le z} |u_{xz}(\xi, z)| \le C, a.e.
$$

给定 \(S(z)\)，满足上述条件且 \(\int u(0, z)\varpi(z)dz = 0\) 的对 \(u(x, z), \rho\) 是唯一确定的。

另外

(12.3.40)
$$
u(x, z) + \rho = \inf_{v \ge 0} [(x, z, v) + \Phi u(x, z)].
$$

证明。我们从 (12.3.33) 开始。我们首先注意到

(12.3.41)
$$
0 \le S_\alpha - \frac{c_1(p+h)}{\min(c, h)} = m_0.
$$

此外，根据 (12.3.28) 和 (12.3.30) 我们有

$$(G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z'), z))(S_\alpha(z) - S_\alpha(z')) \\
\ge 2\alpha(h+p)\gamma(m_0)(S_\alpha(z) - S_\alpha(z'))^2$$

现在

$$(G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z'), z))(S_\alpha(z) - S_\alpha(z')) \\
= \alpha \int (u'_\alpha(S_\alpha(z) - \zeta, z) + u'_\alpha(S_\alpha(z') - \zeta, z))(f(\zeta|z') - f(\zeta|z)) d\zeta$$

根据 (13.2.25)，我们还有

(12.3.42)
$$
\sup_{\xi \le x} |u'_\alpha(\xi, z)| \le \frac{\max(h, p+c)}{1 - \delta_0(x)}.
$$

因此

$$
|G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z'), z)| \le \frac{2 \max(h, p+c)}{1 - \delta_0(m_0)} \int |f(\zeta|z) - f(\zeta|z')| d\zeta
$$

汇总结果，我们可以给出如下估计

$$
|S_\alpha(z) - S_\alpha(z')| \le \frac{\max(h, p+c)}{(h+p)\gamma(m_0)(1-\delta_0(m_0))} \int |f(\zeta|z) - f(\zeta|z')| d\zeta
$$

并且使用假设 (12.3.32) 我们得到

(12.3.43) $$|S_\alpha(z) - S_\alpha(z')| \le \frac{\delta \max(h, p+c)}{(h+p)\gamma(m_0)(1-\delta_0(m_0))} |z' - z|.$$

因此序列 \(S_\alpha(z)\) 是一致 Lipschitz 连续的，从中得出性质 (12.3.33)。

考虑 \(\chi_\alpha(x,z) = u'_\alpha(x,z) - h \mathbb{I}_{x>0} + p \mathbb{I}_{x<0} + c\)。我们有

(12.3.44) $$\chi_\alpha(x,z) = g_\alpha(x,z) + \alpha E[\chi_\alpha(x-z_2, z_2)|z_1=z], \text{ if } x \ge S_\alpha(z)$$ $$= 0 \text{ if } x \le S_\alpha(z)$$

其中

(12.3.45) $$g_\alpha(x,z) = c + \alpha(h-c) - \alpha(h+p)\bar{F}(x|z),$$

我们轻易推断出

(12.3.46) $$\sup_{\xi \le z} |\chi_\alpha(x,z)| \le \frac{\max(h,c)}{1 - \delta_0(x)}.$$

接下来考虑 \(\psi_\alpha(x,z) = \chi'_\alpha(x,z)\)。我们得到

(12.3.47) $$\psi_\alpha(x,z) = \begin{cases} \alpha(h+p)f(x|z) + \alpha E[\psi_\alpha(x-z_2, z_2)|z_1=z], & \text{if } x > S_\alpha(z) \\ 0, & \text{if } x < S_\alpha(z) \end{cases}$$

该函数不连续，但是有界的（在 \(\alpha\) 中不一致有界），我们可以断言

(12.3.48) $$\sup_{\xi \le z} |\psi_\alpha(\xi, z)| \le \frac{(h+p)\|f\|}{1 - \delta_0(x)}.$$

接下来，考虑 \(\chi_\alpha(x,z) - \chi_\alpha(x,z')\)。对于 \(x > S_\alpha(z), x > S_\alpha(z')\)，我们轻易检查出

$$|\chi_\alpha(x,z) - \chi_\alpha(x,z')| \le \left| h+p + \frac{\max(h,c)}{1-\delta_0(x)} \right| \delta |z-z'|.$$

接下来，如同在定理 12.3 中操作的那样，我们可以断言对于 \(S_\alpha(z') > x > S_\alpha(z)\)

$$|\chi_\alpha(x,z) - \chi_\alpha(x,z')| \le h \left| p + \frac{\max(h,c)}{1-\delta_0(x)} + \frac{h+p}{1-\delta_0(x)} \right| |f|(x-S_\alpha(z)).$$

结合估计我们得到

(12.3.49) $$|\chi_\alpha(x,z) - \chi_\alpha(x,z')| \le \frac{C(m_0)\delta}{1-\delta_0(x)} |z-z'|.$$




考虑到 \(\chi\) 在两个变量中的梯度，我们有

\[
\sup_{\xi \le x, z} |D\chi_a(x, z)| \le \frac{C}{1 - \delta_0(x)}.
\]

从这个估计出发，并利用 \(\chi_a(x, z) = 0, \forall x < 0\) 这一事实，我们可以断言，对于一个子序列（仍记为 \(\alpha\)）

\[
\sup_{x \le M, z \le N} |\chi_a(x, z) - \chi(x, z)| \to 0, \text{ as } \alpha \to 0, \forall M, N.
\]

我们如同在定理 12.3 中所做的那样，来证明

\[
\sup_{x \le M, z} |aE[\chi_a(x-x_2, z_2)|z_1=z] - E[\chi(x-x_2, z_2)|z_1=z]| \to 0, \forall M
\]

由 (13.2.34) 可知

\[
\chi(x, z) = g(x, z) + E[\chi(x-x_2, z_2)|z_1=z], \forall x > S(z),
\]

其中

\[
g(x, z) = h - (p+h)F(x|z).
\]

另外，若 \(x < S(z)\)，则 \(\chi(x,x)=0\)。而且，由

\[
0 = g_a(S_a(z), z) + aE[\chi_a(S_a(z)-x_2, z_2)|z_1=z],
\]

和

\[
\sup_{z \le N} |aE[\chi_a(S_a(z)-x_2, z_2)|z_1=z] - E[\chi(S(z)-x_2, z_2)1_{S(z)>z_2}|z_1=z]| \to 0
\]

我们容易得到

\[
0 = g(S(z), z) + E[\chi((S(z)-z_2)^+, z_2)|z_1=z],
\]

且函数 \(\chi(x,z)\) 在 \(x\) 中是连续的。

我们设

\[
\Gamma_a(z) = E[u_a(0, z_2)|z_1=z],
\]

则由第一个方程 (13.2.25) 可验证

\[
\Gamma_a(z) = \Psi_a(z) + aE[\Gamma_a(z_2)|z_1=z],
\]

其中

\[
\Psi_a(z) = c(1-a)S_a(z) + ahE[(S_a(z)-z_2)^+|z_1=z] + a\rho E[(S_a(z)-z_2)^+|z_1=z] + acE[z_2|z_1=z] + aE\left[\int_0^{(S_a(z)-z_2)^+} \chi_a(\xi, z_2)d\xi | z_1=z \right]
\]

我们有

\[
0 \le \Psi_a(z) \le m_0 \max(h, c) \left(1 + \frac{1}{1 - \delta_0(m_0)}\right) + (p+c)c_1
\]

考虑

\[
\Psi(z) = hE[(S(z) - z_2)^+ | z_1 = z] + pE[(S(z) - z_2)^- | z_1 = z] + cE[z_2 | z_1 = z] + E \left[ \int_0^{(S(z)-z_2)^+} \chi(\xi, z_2) d\xi | z_1 = z \right]
\]

以及 \(\Gamma(z)\) 为以下方程的解

\[
\Gamma(z) + \rho = \Psi(z) + E[\Gamma(z_2) | z_1 = z],
\]

其中

\[
\rho = \int \Psi(z) \varpi(z) dz.
$$

根据遍历理论，参见第 3 章，定理 3.3，我们可以断言

\[
\sup_z |\Gamma(z)| \le \sup_z |\Psi(z) - \rho| \frac{3 - \beta}{1 - \beta},
$$

其中 \(0 < \beta < 1\)，仅取决于马尔可夫链。

同样，若设

\[
\rho_\alpha = \int \Psi_\alpha(z) \varpi(z) dz, \quad \tilde{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1 - \alpha}
$$

则可写成

\[
\tilde{\Gamma}_\alpha(z) + \rho_\alpha = \Psi_\alpha(z) + \alpha E[\tilde{\Gamma}_\alpha(z_2) | z_1 = z],
$$

我们也可以断言

\[
\sup_z |\tilde{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3 - \beta}{1 - \beta} \le \left[ m_0 \max(h, c) \left( 1 + \frac{1}{1 - \delta_0(m_0)} \right) + (p + c)c_1 \right] \frac{3 - \beta}{1 - \beta}.
$$

而且

\[
\tilde{\Gamma}_\alpha(z) - \tilde{\Gamma}_\alpha(z') = \Psi_\alpha(z) - \Psi_\alpha(z') + \alpha \int \tilde{\Gamma}_\alpha(\zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta.
$$

由于，利用 (13.2.33)

\[
|\Psi_\alpha(z) - \Psi_\alpha(z')| \le C(m_0) \delta |z - z'|,
$$

并且由 (12.3.32) 可断言

\[
|\tilde{\Gamma}_\alpha(z) - \tilde{\Gamma}_\alpha(z')| \le C_1(m_0) \delta |z - z'|.
$$

因此函数 \(\tilde{\Gamma}_\alpha(z)\) 一致 Lipschitz 连续且有界。由此可知，对于一个子序列我们得到

\[
\sup_{0 \le z \le N} \left| \Gamma_\alpha(z) - \frac{\rho_\alpha}{1 - \alpha} - \Gamma(z) \right| \to 0, \forall N
$$

因此

\[
\sup_{x \le M, 0 \le z \le N} \left| u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} - u(x, z) \right| \to 0, \forall x, \forall M, N
$$

其中

\[
u(x, z) = hx^+ + px^- - cx + \int_0^x \chi(\xi, z) d\xi + \Gamma(z).
$$

我们推导出 \(u(0,z) = \Gamma(z)\)。而且，容易验证

\[
\Gamma(z) = \rho + cS(z) + E[u(S(z) - z_2, z_2)|z_1 = z].
$$

因此第一个关系 (13.2.28) 得证。

现在考虑 \(x \ge S(z)\) 的情况。定义函数

\[
\bar{u}(x,z) = hx^+ + px^- + E[u(x - z_2, z_2)|z_1 = z].
$$

我们得到

\[
\begin{aligned}
\bar{u}'(x,z) &= h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + E[u'(x-z_2, z_2)|z_1 = z] \\
&= h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + c + \chi(x,z), \quad x \ge S(z) \\
&= u'(x,z), \quad x \ge S(z).
\end{aligned}
$$

又

\[
\begin{aligned}
\bar{u}(S(z), z) &= hS(z) + E[u(S(z) - z_2, z_2)|z_1 = z] \\
&= (h - c)S(z) + \rho + \Gamma(z) \\
&= u(S(z), z) + \rho
\end{aligned}
$$

由这两个关系可得 \(\bar{u}(x,z) = u(x,z) + \rho, \forall x \ge S(z)\)。

这就完成了 (13.2.28) 的第二部分。

(12.3.40) 的证明与定理 12.3 的证明类似。

我们接下来有

\[
u_\alpha(x,z) - u_\alpha(x,z') = \Gamma_\alpha(z) - \Gamma_\alpha(z') + \int_0^x (\chi_\alpha(\xi,z) - \chi_\alpha(\xi,z')) d\xi
$$

利用已证明的估计我们得到

\[
|u_\alpha(x,z) - u_\alpha(x,z')| \le \left[ C_1(m_0) + \frac{C(m_0)x^+}{1 - \delta_0(x)} \right] \delta|z - z'|
$$

极限 \(u(x,z)\) 满足所有估计 (12.3.37), (12.3.39)。唯一性的证明与定理 12.3 的证明类似。

证明已完成 \(\square\)

## 12.4. 无积压和设置成本

### 12.4.1. 模型.

我们现在研究设置成本的情况，并从无短缺模型开始。我们需要研究 Bellman 方程

\[
u(x,z) = \inf_{v \ge 0} \{K \mathbb{I}_{v > 0} + l(x,z,v) + \alpha \Phi^v u(x,z)\},
$$

其中

\[
\begin{aligned}
\Phi^v \varphi(x,z) &= E[\varphi((x+v-z_2)^+, z_2)|z_1 = z] \\
&= \int_0^{x+v} \varphi(x+v-\zeta, \zeta) f(\zeta|z) d\zeta + \int_{x+v}^\infty \varphi(0, \zeta) f(\zeta|z) d\zeta
\end{aligned}
$$

并且

\[
f(\zeta|z) \text{ 在两个变量中一致连续且有界}
\]

\[
\int_0^{+\infty} \zeta f(\zeta|z) d\zeta \le c_0 z + c_1
$$

\[
l(x,z,v) = cv + hx + pE[(x+v-z_2)^-|z_1 = z].
$$

我们在区间 \([0, w_0(x,z)]\) 中寻找 (12.4.1) 的解，其中

\[
u_0(x,z) = l_0(x,z) + \alpha E[u_0(x-z_2, z_2)|z_1=z].
$$

在引理 12.1 中，我们已证明估计

\[
u_0(x,z) \le \frac{hx}{1-\alpha} + \frac{pc_0z}{1-c_0\alpha} + \frac{pc_1}{(1-\alpha)(1-c_0\alpha)},
$$

并假设

\[
c_0\alpha < 1.
$$

如常，我们考虑收益函数

\[
J_{x,z}(V) = E \sum_{n=1}^\infty \alpha^{n-1} [K \mathbb{I}_{v_n > 0} + l(y_n, z_n, v_n)],
$$

其中 \(V = (v_1, \cdots, v_n, \cdots)\) 为取正值的自适应过程，且

\[
y_{n+1} = (y_n + v_n - z_{n+1})^+, y_1 = x.
$$

我们定义值函数

\[
u(x,z) = \inf_V J_{x,z}(V).
$$

我们陈述

**定理 12.7.** 我们假设 (12.4.2), (12.4.3), (12.4.4), (12.4.5), (12.4.8)。在 (12.4.11) 中定义的值函数是区间 \([0, w_0]\) 上 Bellman 方程 (12.4.1) 的唯一下半连续解。存在一个最优反馈 \(\hat{v}(x,z)\)。

### 12.4.2. s(z), S(z) 策略.

我们现在证明以下结果

**定理 12.8.** 我们做出定理 12.7 的假设且 \(p > c\)。那么函数 \(u(x,z)\) 是 \(K\)-凸且连续的。当 \(x \to +\infty\) 时，它趋向于 \(+\infty\)。函数

\[
G(x,z) = cx + pE[(x-z_2)^-|z_1=z] + \alpha E[u((x-z_2)^+, z_2)|z_1=z],
$$

也是 \(K\)-凸且连续的。当 \(x \to +\infty\) 时，它趋向于 \(+\infty\)。考虑与 \(G(x,z)\) 相关的数 \(s(z)\)、\(S(z)\)，最优反馈由

\[
\hat{v}(x,z) = \begin{cases} S(z) - x, & \text{如果 } x \le s(z) \\ 0, & \text{如果 } x > s(z) \end{cases}
$$

给出。

函数 \(s(z)\)、\(S(z)\) 是连续的。

证明. 我们考虑递增序列

\[
u_{n+1}(x,z) = \inf_{v \ge 0} \{ K \mathbb{I}_{v > 0} + cv + hx + pE[(x+v-z_2)^-|z_1=z] + \alpha E[u_n((x+v-z_2)^+, z_2)|z_1=z] \},
$$

其中 \(u_0(x,z) = 0\)。定义

\[
G_n(x,z) = cx + pE[(x-z_2)^-|z_1=z] + \alpha E[u_n((x-z_2)^+, z_2)|z_1=z].
$$

我们可以写成

\[
u_{n+1}(x,z) = (h-c)x + \inf_{\eta \ge z} \{ K \mathbb{I}_{\eta \ge z} + G_n(\eta, z) \}.
$$

我们将通过归纳法证明，对于 \(n \ge 1\)，\(u_n(x,z)\) 和 \(G_n(x,z)\) 在 \(x\) 中均为 \(K\)-凸、连续，并且当 \(x \to +\infty\) 时趋向于 \(+\infty\)。对于


n = 1. 我们假设它们对 n 成立，并证明对 n + 1 成立。由于 \( G_n(x, z) \) 在 x 中是 K-凸的，连续，并且当 \( x \to +\infty \) 时趋于 \( +\infty \)，我们可以定义 \( s_n(z), S_n(z) \) 如下

(12.4.16) \( G_n(S_n(z), z) = \inf_\eta G_n(\eta, z) \)

(12.4.17) \( s_n(z) = \begin{cases} 0, & \text{如果 } G_n(0, z) \le K + \inf_\eta G_n(\eta, z) \\ G_n(s_n(z), z) = K + \inf_\eta G_n(\eta, z), & \text{如果 } G_n(0, z) > K + \inf_\eta G_n(\eta, z) \end{cases} \)

通常，我们取最小的最小化点以唯一地定义 \( S_n(z) \)。由于 \( G_n(\eta, z) \) 是连续的，很容易检查 \( S_n(z) \) 是连续的。同样，\( s_n(z) \) 也是连续的。

我们可以写

\( u_{n+1}(x, z) = (h - c)x + G_n(\max(x, s_n(z)), z), \)

这立即表明 \( u_{n+1}(x, z) \) 是 K-凸且连续的。此外，当 \( x \to +\infty \) 时，\( u_{n+1}(x, z) \to +\infty \)。于是我们有

\( G_{n+1}(x, z) = cx + pE[(x - z_2)^+ | z_1 = z] + \alpha(h - c)E[(x - z_2)^+ | z_1 = z] + \alpha E[G_n(\max(x - z_2, s_n(z_2)), z_2) | z_1 = z] \)

它是一个凸函数和一个 K-凸函数的和，因此是 K-凸的。它是连续的，并且当 \( x \to +\infty \) 时趋于 \( +\infty \)。因此递归关系已证明。如果我们写（形式上）

\( u'_n(x, z) = h - c + \chi_n(x, z), \)

则有递推关系

\( \chi_{n+1}(x, z) = \begin{cases} 0 & \text{如果 } x < s_n(z) \\ = \mu(x, z) + \alpha E[\chi_n(x - z_2, z_2) | z_1 = z] \end{cases} \)

其中

(12.4.18) \( \mu(x, z) = c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x|z). \)

函数 \( \chi_{n+1}(x, z) \) 在 \( s_n(z) \) 处不连续。然而，有界限

\( -\frac{(p - c)}{1 - \alpha} \le \chi_{n+1}(x, z) \le \frac{c + \alpha(h - c)}{1 - \alpha} \quad \text{几乎处处} \)

因此极限 \( u(x, z) \) 是 K-凸的，并满足

\( u'(x, z) = h - c + \chi(x, z), \)

其中

\( -\frac{(p - c)}{1 - \alpha} \le \chi(x, z) \le \frac{c + \alpha(h - c)}{1 - \alpha} \quad \text{几乎处处} \)

因此 \( u(x, z) \) 在 x 中是连续的，并且当 \( x \to +\infty \) 时趋于 \( +\infty \)。于是唯一地定义 \( s(z), S(z) \)，且 \( S(z) \) 在 x 中最小化函数

\( G(x, z) = cx + pE[(x - z_2)^+ | z_1 = z] + \alpha E[u((x - z_2)^+, z_2) | z_1 = z] \)

从该公式和 u 在 x 中的 Lipschitz 连续性出发，利用假设 (12.4.3) 可以看出 \( G(x, z) \) 在两个参数中都是连续的。因此 \( S(z) \) 和 \( s(z) \) 是连续的。证明已完成。\(\square\)

## 12.4.3. 遍历理论.

我们现在研究当 $\alpha \to +\infty$ 时 $u(x, z)$ 的行为。我们将其记为 $u_\alpha(x, z)$ 并写出关系

(12.4.19) 
$u_\alpha(x, z) = (h - c)x + G_\alpha(\max(x, s_\alpha(z)), z)$

(12.4.20) 
$G_\alpha(x, z) = g_\alpha(x, z) + \alpha E[G_\alpha(\max((x - z_2)^+, s_\alpha(z_2)), z_2)|z_1 = z],$

其中

(12.4.21) 
$g_\alpha(x, z) = cx + pE[(x - z_2)^-|z_1 = z] + \alpha(h - c)E[(x - z_2)^+|z_1 = z].$

我们将采用与基准库存情况不同的方法，因为我们无法证明函数 $s_\alpha(z)$ 具有一致 Lipschitz 性质。当前方法将使用较少的假设。我们将假设 $c_0 = 0$ 并且

(12.4.22) 
$z_n \text{ 是遍历的.}$

我们用 $\varpi(z)$ 表示不变量度。我们还假设

(12.4.23) 
$\int |f(\zeta|z) - f(\zeta|z')| d\zeta \le \delta|z - z'|, 
\int \zeta |f(\zeta|z) - f(\zeta|z')| d\zeta \le \delta|z - z'|$

(12.4.24) 
$\sup_z F(x|z) = \delta_0(x) < 1, \forall x$

(12.4.25) 
$\sup_z \bar{F}(x|z) \to 0 \text{ 当 } x \to +\infty$

我们从下面开始

### 引理 12.3. 如果 $s(z) > 0$，则

$S(z) \le \frac{p + \alpha(h - c)}{c + \alpha(h - c)} E[z_2|z]$

证明. 如果 $s(z) > 0$，则我们有

$u(0, z) = K + G(S(z), z).$

设

$\dot{y}_2 = (S(z) - z_2)^+, \quad \dot{v}_2 = \dot{u}(\dot{y}_2, z_2),$

则

$G(S(z), z) = cS(z) + pE[(S(z) - z_2)^-|z_1 = z] + \alpha E[u(\dot{y}_2, z_2)|z_1 = z]$

同样，我们可以写

$u(\dot{y}_2, z_2) = (h - c)\dot{y}_2 + K\mathbb{1}_{\dot{y}_2 > 0} + G(\dot{y}_2 + \dot{v}_2, z_2) 
= h\dot{y}_2 + K\mathbb{1}_{\dot{y}_2 > 0} + c\dot{v}_2 + pE[(\dot{y}_2 + \dot{v}_2 - z_3)^-|z_2] 
+ \alpha E[u((\dot{y}_2 + \dot{v}_2 - z_3)^+, z_3)|z_2]$

因此，我们可以写

(12.4.26) 
$u(0, z) = K + cS(z) + pE[(S(z) - z_2)^-|z_1 = z] 
+ \alpha E[h\dot{y}_2 + K\mathbb{1}_{\dot{y}_2 > 0} + c\dot{v}_2 + p(\dot{y}_2 + \dot{v}_2 - z_3)^- 
+ \alpha u((\dot{y}_2 + \dot{v}_2 - z_3)^+, z_3)|z_1 = z].$

接下来我们有

$u(0, z) \le G(0, z) = E[pz_2 + \alpha u(0, z_2)|z_1 = z]$

此外

$u(0, z_2) \le K + G(\hat{y}_2 + \hat{v}_2, z_2)$

替换 $G$ 并结合两个不等式，我们得到

$u(0, z) \le pE[z_2|z_1 = z] + \alpha K + \alpha E[(y_2 + \hat{v}_2) + p(y_2 + \hat{v}_2 - z_3)^- + \alpha u((y_2 + \hat{v}_2 - z_3)^+, z_3)|z_1 = z]$

与 (12.4.26) 比较，我们很容易得到所需的不等式。

从该引理推断，每当 $c_0 = 0$ 时

(12.4.27) $$s_\alpha(z) \le \frac{p + (h - c)^+}{\min(c, h)} c_1.$$

我们现在陈述

### 定理 12.9. 我们假设 (12.4.3), (12.4.4)，其中 $c_0 = 0$，(12.4.22), (12.4.23), (12.4.24), (12.4.25)。那么存在一个数 $\rho_\alpha$ 使得，对于一个子序列，仍记为 $\alpha \to 1$

(12.4.28) $$\sup_{x \le M} \frac{u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} - u(x, z)}{z} \to 0, \forall M,$$

并且 $\rho_\alpha \to \rho$。函数 $u(x, z)$ 是 Lipschitz 连续的，$K$-凸的，并满足

(12.4.29) $$|u(x, z)| \le C_0 + \frac{C_1 x}{1 - \delta_0(x)}$$

(12.4.30) $$|u_x(x, z)| \le \frac{C}{1 - \delta_0(x)}, \quad |u_z(x, z)| \le C_0 + \frac{C_1 x}{1 - \delta_0(x)} \quad \text{几乎处处}$$

对子 $u(x, z), \rho$ 是

(12.4.31) $$u(x, z) + \rho = \inf_{v \ge 0} [K \mathbb{I}_{v > 0} + l(x, z, v) + \Phi^v u(x, z)].$$

证明. 我们设

$\chi_\alpha(x, z) = u'_\alpha(x, z) - h + c,$

则我们可以写

(12.4.32) $$\chi_\alpha(x, z) = \mathbb{I}_{x > z_\alpha(h)} \mu_\alpha(x, z) + \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{I}_{x - z_2 > 0} | z_1 = z],$$

其中

$\mu_\alpha(x, z) = g'_\alpha(x, z) = c + \alpha(h - c) - (p + \alpha(h - c))\bar{F}(x|z)$

函数 $\chi_\alpha(x, z)$ 不是连续的，但满足

(12.4.33) $$\sup_{0 \le \xi \le x} \frac{|\chi_\alpha(\xi, z)|}{z} \le \frac{\max(h, p)}{1 - \delta_0(x)}.$$

接下来我们定义 \(\Gamma_\alpha(z) = u_\alpha(0, z)\)。我们有
\(\begin{aligned}
\Gamma_\alpha(z) &= G_\alpha(s_\alpha(z), z) \\
&= c s_\alpha(z) + p E[(s_\alpha(z) - z_2)^- | z_1 = z] + \alpha E[u_\alpha((s_\alpha(z) - z_2)^+, z_2) | z_1 = z] \\
&= g_\alpha(s_\alpha(z), z) + \alpha E \left[ \int_0^{(s_\alpha(z) - z_2)^+} \chi_\alpha(\xi, z_2) d\xi | z_1 = z \right] + \alpha E[\Gamma_\alpha(z_2) | z_1 = z]
\end{aligned}$

因此我们可以写
(12.4.34) \(\Gamma_\alpha(z) = \Psi_\alpha(z) + \alpha E[\Gamma_\alpha(z_2) | z_1 = z],\)

其中
\(\Psi_\alpha(z) = g_\alpha(s_\alpha(z), z) + \alpha E \left[ \int_0^{(s_\alpha(z) - z_2)^+} \chi_\alpha(\xi, z_2) d\xi | z_1 = z \right].\)

得益于引理 12.3，我们有估计 (12.4.27)，因此 \(s_\alpha(z) \le m_0$。使用估计 (12.4.33)，我们看到 \(|\Psi_\alpha(z)| \le C$。然后我们定义
\(\rho_\alpha = \int \Psi_\alpha(z) \varpi(z) dz,\)

和 \(\bar{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1 - \alpha}$。根据遍历理论，我们可以断言
\(\sup_z |\bar{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3 - \beta}{1 - \beta} \le C,$

并且我们可以陈述估计
\(\left| u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} \right| \le C + \frac{Cx}{1 - \delta_0(x)}.$

定义 \(\tilde{u}_\alpha(x, z) = u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha}$。我们将方程 (12.4.1) 写为
(12.4.35) \(\tilde{u}_\alpha(x, z) + \rho_\alpha = \inf_{v \ge 0} [K \mathbf{1}_{v>0} + l(x, z, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)].$

从引理 12.3 我们可以断言最优反馈满足 \(x + \tilde{u}_\alpha(x, z) \le \max(x, m_0)$。因此我们可以用以下内容替换 (12.4.35)
\(\begin{aligned}
\tilde{u}_\alpha(x, z) + \rho_\alpha &= \inf_{x+v \le \max(x, m_0)} [K \mathbf{1}_{v>0} + l(x, z, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)] \\
&= \inf_{0 \le v \le \max(x, m_0) - x} L_\alpha(x, z, v).
\end{aligned}$

接下来
\(L_\alpha(x, z, v) - L_\alpha(x, z', v) = \int [p(x+v-\zeta)^+ - \alpha \tilde{u}_\alpha((x+v-\zeta)^+, \zeta)] (f(z|\zeta) - f(z'|\zeta)) d\zeta$

对于 \(v \le \max(x, m_0) - x$ 我们可以写
\(\begin{aligned}
|\tilde{u}_\alpha((x+v-\zeta)^+, \zeta)| \le C + \frac{C \max(x, m_0)}{1 - \delta_0(\max(x, m_0))} \\
\le C'_1 + \frac{C_2 x}{1 - \delta_0(x)}
\end{aligned}$

使用假设 (12.4.23) 我们很容易得到
\(|\tilde{u}_\alpha(x, z) - \tilde{u}_\alpha(x, z')| \le \left( C_1 + \frac{C_2 x}{1 - \delta_0(x)} \right) |z - z'|.$



从所得估计可以断言，\(\bar{u}_\alpha(x, z)\) 有一个收敛子序列（仍记作 \(\alpha\)），其意义为

(12.4.36)
\(\sup_{x \le M \\ z \le N} |\bar{u}_\alpha(x, z) - u(x, z)| \to 0, \text{ as } \alpha \to 0.\)

由于 \(\rho_\alpha\) 有界，我们总可以假设 \(\rho_\alpha \to \rho\)。记

\(L(x, z, v) = K \mathbb{I}_{v>0} + l(x, z, v) + \Phi^e u(x, z)\)

则

\(L_\alpha(x, z, v) - L(x, z, v) = \alpha \Phi^e(\bar{u}_\alpha - u)(x, z) - (1 - \alpha) \Phi^e u(x, z)\)

对于 \(v \le \max(x, m_0) - x\)，在假设 \(M > m_0\) 下，我们有

\(\sup_{x \le M \\ z} |\Phi^e u(x, z)| \le C + \frac{CM}{1 - \delta_0(M)}\)

我们还有

\(\sup_{x \le M \\ z} |\Phi^e(\bar{u}_\alpha - u)(x, z)| \le \sup_{x \le M \\ z} |\bar{u}_\alpha - u|(x, z) \sup_z \bar{F}(N, z)\)
\(+ \sup_{x \le M \\ z \le N} |\bar{u}_\alpha - u|(x, z)\)

利用假设 (12.4.25) 和 (12.4.36)，先令 \(\alpha \to 0\)，再令 \(N \to \infty$，可得

\(\sup_{v \le \max(x, m_0) - x \\ z \le M} |L_\alpha(x, z, v) - L(x, z, v)| \to 0, \text{ as } \alpha \to 0.\)

因此我们容易推出 (12.4.28)，并且对 \(u(x, z), \rho\) 满足 (12.4.31)。估计 (12.4.29)、(12.4.31) 立即从 \(\bar{u}_\alpha(x, z)\) 上的相应估计得出。\(u\) 的 \(K\)-凸性由 \(\bar{u}_\alpha\) 的 \(K\)-凸性得证。证明已完成。

## 12.5. 积压与设置成本

### 12.5.1. 模型.

我们最后考虑有积压的设置成本情况。Bellman 方程为

(12.5.1) \(u(x, z) = \inf_{v \ge 0} [K \mathbb{I}_{v>0} + l(x, v) + \alpha \Phi^e u(x, z)],\)

其中

(12.5.2) \(\Phi^e \varphi(x, z) = E[\varphi(x + v - z_2, z_2) | z_1 = z]\)
\(= \int_0^\infty \varphi(x + v - \zeta, \zeta) f(\zeta | z) d\zeta,\)

以及

(12.5.3) \(f(\zeta | z)\) 对两个变量一致连续且有界

(12.5.4) \(\int_0^{+\infty} c(|z|) d\zeta \le c_0 z + c_1,\)

(12.5.5) \(l(x, v) = cv + hx^+ + px^- .\)

我们在区间 [0, w_0(x, z)] 内寻求 (12.5.1) 的解，其中

(12.5.6) \(w_0(x, z) = l_0(x) + \alpha E[w_0(x - z_2, z_2) | z_1 = z],\)

且 \(l_0(x) = l(x, 0).\)

在引理 12.2 中，我们已证明估计

(12.5.7) \(w_0(x, z) \le \frac{hx^+ + px^-}{1 - \alpha} + \frac{pc_0 \alpha}{(1 - c_0 \alpha)(1 - \alpha)} + \frac{pc_1}{(1 - c_0)^2} \left( \frac{\alpha - c_0}{(1 - \alpha)^2} + \frac{c_0}{1 - \alpha c_0} \right),\)

并假设

(12.5.8) \(c_0 \alpha < 1.\)

如常，我们考虑收益函数

(12.5.9) \(J_{x,z}(V) = E \sum_{n=1}^{\infty} \alpha^{n-1} [K \mathbf{I}_{v_n > 0} + l(y_n, v_n)],\)

其中 \(V = (v_1, \cdots, v_n, \cdots)\) 为取正值的自适应过程，且

(12.5.10) \(y_{n+1} = y_n + v_n - z_{n+1}, y_1 = x.\)

我们定义值函数

(12.5.11) \(u(x, z) = \inf_V J_{x,z}(V).\)

我们陈述

### 定理 12.10.
我们假设 (12.5.2), (12.5.3), (12.5.4), (12.5.5), (12.5.8). 在区间 [0, w_0] 上，由 (12.5.11) 定义的值函数是 Bellman 方程 (12.5.1) 的唯一下半连续解。存在一个最优反馈 \(\hat{v}(x, z).\)

### 12.5.2. s(z), S(z) 策略.
我们现在证明以下结果

### 定理 12.11.
我们做定理 12.10 的假设且 \(\alpha p > c\). 那么函数 \(u(x, z)\) 是 \(K\)-凸且连续的。当 \(|x| \to +\infty\) 时，它趋于 \(+\infty\). 考虑与 \(u(x, z)\) 相关的数 \(s(z), S(z)\)，最优反馈由

(12.5.12) \(\hat{v}(x, z) = \begin{cases} S(z) - x, & \text{if } x \le s(z) \\ 0, & \text{if } x > s(z) \end{cases}\)

给出。函数 \(s(z), S(z)\) 是连续的，且 \(S(z) > 0.\)

### 证明.
我们考虑递增序列

(12.5.13) \(u_{n+1}(x, z) = hx^+ + px^- + \inf_{v \ge 0} \{ K \mathbf{I}_{v > 0} + c v + \alpha E[u_n(x + v - z_2, z_2) | z_1 = z] \},\)

其中 \(u_0(x, z) = 0.\) 定义

(12.5.14) \(G_n(x, z) = cx + \alpha E[u_n(x - z_2, z_2) | z_1 = z].\)

我们可以写成

(12.5.15) \(u_{n+1}(x, z) = hx^+ + px^- - cx + \inf_{\eta \ge x} [K \mathbf{I}_{\eta > x} + G_n(\eta, z)].\)

我们将通过归纳法证明，对于 \(n \ge 2\)，\(u_n(x,z)\) 和 \(G_n(x,z)\) 在 \(x\) 中都是 \(K\)-凸的、连续的，并且当 \(|x| \to +\infty\) 时趋于 \(+\infty\). 此外

(12.5.16) \(u'_n(x,z) \le -p - c, G'_n(x,z) \le c(1-\alpha) - \alpha p, \text{ if } x < 0.\)

这些关系对于 \(n \ge 2\) 成立。我们有 \(G'_0(x,z) = c\) 且当 \(x < 0\) 时 \(u'_1(x,z) = -p\). 那么

\(G'_n(x,z) = c - \alpha p < 0, \text{ if } x < 0\)

一旦 \(G'_n(x,z) \le 0\) 对 \(x < 0\) 成立，那么 \(u'_{n+1}(x,z)\) 满足 (12.5.16)，且 \(G'_{n+1}(x,z)\) 也满足 (12.5.16).

由于 \(G_n(x,z)\) 在 \(x\) 中是 \(K\)-凸的、连续的，并且当 \(|x| \to +\infty\) 时趋于 \(+\infty\)，我们可以定义 \(s_n(z), S_n(z)\) 使得

(12.5.17) \(G_n(S_n(z), z) = \inf_\eta G_n(\eta, z),\)

并且 \(s_n(z)\) 由

(12.5.18) \(G_n(s_n(z), z) = K + \inf_\eta G_n(\eta, z).\)

定义。

如常，我们取最小极小值，以唯一方式定义 \(S_n(z)\). 由于 \(G_n(\eta, z)\) 是连续的，容易检查 \(S_n(z)\) 是连续的。同样 \(s_n(z)\) 是连续的。

我们可以写成

\(u_{n+1}(x,z) = hx^+ + px^- - cx + G_n(\max(x, s_n(z)), z)\)

这立即表明 \(u_{n+1}(x,z)\) 进而 \(G_{n+1}(x,z)\) 是 \(K\)-凸且连续的。此外，当 \(x \to +\infty\) 时，\(u_{n+1}(x,z), G_{n+1}(x,z) \rightarrow +\infty\).

由于当 \(x < 0\) 时

\(u'_{n+1}(x,z) = -p + c + G'_n(x) 1_{x > s_n(z)},\)

我们看到 (12.5.16) 对 \(u_{n+1}, G_{n+1}\) 满足。因此当 \(x \to -\infty\) 时，\(u_{n+1}(x,z), G_{n+1}(x,z) \rightarrow +\infty\).

所以递归已证。还要注意 \(S_n(z) > 0\).

如果我们（形式地）写成

\(u'_n(x,z) = h 1_{x > 0} - p 1_{x < 0} - c + \chi_n(x,z),\)

那么有递推关系

\(X_{n+1}(x,z) = \begin{cases} 0 & \text{if } x < s_n(z) \\ = \mu(x,z) + \alpha E[\chi_n(x - z_2, z_2) | z_1 = z] \end{cases}\)

其中

(12.5.19) \(\mu(x,z) = c(1-\alpha) + \alpha h - \alpha(p+h)\bar{F}(x|z).\)

函数 \(X_{n+1}(x,z)\) 在 \(s_n(z)\) 处不连续。然而有界

\(\frac{c(1-\alpha) - \alpha p}{1-\alpha} \le X_{n+1}(x,z) \le \frac{c(1-\alpha) + \alpha h}{1-\alpha} \quad \text{a.e.}\)

还要注意，若 \(x < 0\) 则 \(X_n(x,z) \le 0\)，且

\(X_{n+1}(x,z) \le c(1-\alpha) - \alpha p, \text{ if } s_n(z) < x < 0\)

因此极限 \(u(x,z)\) 是 \(K\)-凸的并满足

\(u'(x,z) = h 1_{x > 0} - p 1_{x < 0} - c + \chi(x,z),\)

其中

\(\frac{c(1-\alpha)-\alpha p}{1-\alpha} \le \chi(x,z) \le \frac{c(1-\alpha)+\alpha h}{1-\alpha} \quad \text{a.e.}\)

因此 \(u(x,z)\) 在 \(x\) 中是连续的，且当 \(x \to +\infty\) 时趋于 \(+\infty\). 对于 \(x < 0\)，还有一个

\(u'(x,z) \le -c - p\)

因此当 \(x \to -\infty\) 时，\(u(x,z) \to +\infty\). 另外

\(\chi(x,z) \le 0 \text{ if } x < 0, \quad \chi(x,z) \le c(1-\alpha) - \alpha p, \ s(z) < x < 0\)

因此唯一地定义 \(s(z), S(z)\)，且 \(S(z)\) 在 \(x\) 中使函数

\(G(x,z) = cx + \alpha E[u(x-z_2, z_2)|z_1 = z]\)

取得最小值。

从这个公式和 \(u\) 在 \(x\) 中的 Lipschitz 连续性出发，利用假设 (12.5.3) 可以看出 \(G(x,z)\) 在两个参数中都是连续的。

另外，当 \(x \to -\infty\) 时，\(G(x,z) \to +\infty\). 因此 \(S(z)\) 和 \(s(z)\) 定义良好，且是连续的。而且 \(S(z) > 0\). 证明已完成。

### 12.5.3. 遍历理论.

我们现在研究当 \(\alpha \to +\infty\) 时 \(u(x,z)\) 的行为。我们将其记为 \(u_\alpha(x,z)\) 并写出关系

(12.5.20) \(u_\alpha(x,z) = hx^+ + px^- - cx + G_\alpha(\max(x, s_\alpha(z)), z)\)

(12.5.21) \(G_\alpha(x,z) = cx + \alpha E[u_\alpha(x-z_2, z_2)|z_1 = z].\)

我们将假设 \(c_0 = 0\) 并且

(12.5.22) \(z_n \text{ is ergodic.}\)

我们用 \(\varpi(z)\) 表示不变量度。我们还假设

(12.5.23) \(\int |f(\zeta|z) - f(\zeta|z')| d\zeta \le \delta |z - z'|,\)

(12.5.24) \(\int \zeta |f(\zeta|z) - f(\zeta|z')| d\zeta \le \delta |z - z'|,\)

(12.5.25) \(\sup_z F(x|z) = \delta_0(x) < 1, \forall x\)

(12.5.26) \(\sup_z \bar{F}(x|z) \to 0 \text{ as } x \to +\infty\)

我们从以下开始

### 引理 12.4.
我们有估计

(12.5.27) \(s_\alpha^-(z) \le \frac{K}{\alpha p - c(1-\alpha)} = m_\alpha\)

还有

(12.5.28) \(0 \le S_\alpha(z) \le \frac{\alpha(p+h)E[z_2|z_1=z] + \alpha p m_\alpha}{c + \alpha(h-c)}\)




证明。我们回顾一下

$$0 = K + \inf_{\eta > \alpha(z)} \int_{s(z)}^\eta \chi(\xi, z) d\xi.$$

因此，如果 $s(z) < 0$，我们可以写成

$$0 \le K + \int_{s(z)}^0 \chi(\xi, z) d\xi$$

然而，对于 $s(z) < \xi < 0$，我们有 $\chi(\xi, z) \le c(1-\alpha) - \alpha p$，这立即蕴含 (12.5.27)。

由于 $s_\alpha(z) > -m_\alpha$，我们依次得到

$$u(-m_\alpha, z) = (p+c)m_\alpha + K + G(S(z), z).$$

设

$$\hat{y}_2 = S(z) - z_2, \quad \hat{v}_2 = \hat{v}(\hat{y}_2, z_2),$$

则

$$G(S(z), z) = cS(z) + \alpha E[u(\hat{y}_2, z_2)|z_1 = z].$$

同样，我们可以写成

$$u(\hat{y}_2, z_2) = h\hat{y}_2^+ + p\hat{y}_2^- + K \mathbf{1}_{\hat{v}_2 > 0} + c\hat{v}_2 + \alpha E[u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_2].$$

因此，我们可以写成

(12.5.29) $$u(-m_\alpha, z) = (p+c)m_\alpha + K + cS(z) + \alpha E[h\hat{y}_2^+ + p\hat{y}_2^- + K \mathbf{1}_{\hat{v}_2 > 0} + c\hat{v}_2 + \alpha u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_1 = z].$$

接下来，我们有

$$u(-m_\alpha, z) \le p m_\alpha + \alpha E[u(-m_\alpha - z_2, z_2)|z_1 = z].$$

此外，

$$u(-m_\alpha - z_2, z_2) \le K + p(z_2 + m_\alpha) + c(\hat{y}_2 + \hat{v}_2 + z_2 + m_\alpha) + \alpha E[u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_2].$$

结合这两个不等式，我们得到

$$u(-m_\alpha, z) \le p m_\alpha + \alpha K + \alpha(p+c)m_\alpha + \alpha E[(p+c)z_2 + c(\hat{y}_2 + \hat{v}_2) + \alpha u(\hat{y}_2 + \hat{v}_2 - z_3, z_3)|z_1 = z].$$

与 (12.5.29) 比较，我们得到不等式

$$cS(z) + \alpha(h-\alpha)E[(S(z)-z_2)^+|z_1 = z] + \alpha(p+c)E[(S(z)-z_2)^+|z_1 = z] \le \alpha p m_\alpha + \alpha(p+c)E[z_2|z_1 = z],$$

由此我们很容易推导出 (12.5.28)，从而完成证明。

根据引理，如果 $\alpha p > c + \alpha(h-c)$，则还有

(12.5.30) $$|s_\alpha(z)| \le \frac{\alpha(p+h)E[z_2|z_1=z] + \alpha p m_\alpha}{c + \alpha(h-c)}.$$

由于 $\alpha \to 1$，我们可以假设 $\alpha > \frac{1}{2}$，因此如果 $c_0 = 0$

$$|s_\alpha(z)|, S_\alpha(z) \le m_0 = \frac{(p+h)c_1 + \frac{2Kp}{p-c}}{\min(c,h)}$$

我们现在陈述

## 定理 12.12. 我们假设 (12.5.3), (12.5.4)，其中 \(c_0=0\)，(12.5.22), (12.5.23), (12.5.25), (12.5.26)。那么存在一个数 \(\rho_\alpha\)，使得对于一个子序列，仍记为 \(\alpha \to 1\)

(12.5.31)
$$
\sup_{|x| \le M} \left| u_\alpha(x,z) - \frac{\rho_\alpha}{1-\alpha} - u(x,z) \right| \to 0, \forall M,
$$

并且 \(\rho_\alpha \to \rho$。函数 \(u(x,z)$ 是 Lipschitz 连续的，\(K\)-凸的，并满足

(12.5.32)
$$
|u(x,z)| \le C + \frac{C(x+m_0)^+}{1-\delta_0((x+m_0)^+)} + C(x+m_0)^-
$$

(12.5.33)
$$
\begin{aligned}
|u_x(x,z)| &\le \frac{C}{1-\delta_0((x+m_0)^+)}; \\
|u_z(x,z)| &\le C + \frac{C(\max(x^+,m_0)+m_0)}{1-\delta_0(\max(x^+,m_0)+m_0)} \text{ 几乎处处}
\end{aligned}
$$

\((u(x,z), \rho)\) 是 ... 的解

(12.5.34)
$$
u(x,z) + \rho = \inf_{v \ge 1} [K \mathbb{I}_{v>0} + l(x,v) + \Phi^v u(x,z)].
$$

证明。我们设

$$
\chi_\alpha(x,z) = u'_\alpha(x,z) - h \mathbb{I}_{x>0} + p \mathbb{I}_{x<0} + c,
$$

然后我们可以写成

(12.5.35)
$$
\chi_\alpha(x,z) = \mathbb{I}_{x>s_\alpha(z)} \{ \mu_\alpha(x,z) + \alpha E[\chi_\alpha(x-s_2,z_2)|z_1=z] \},
$$

其中

$$
\mu_\alpha(x,z) = c + \alpha(h-c) - \alpha(h+p)\bar{F}(x|z)
$$

函数 \(\chi_\alpha(x,z)$ 不是连续的，但满足（因为 \(s_\alpha(z) \ge -m_0\)）

(12.5.36)
$$
\sup_{\xi \le x} |\chi_\alpha(\xi,z)| \le \frac{\max(h,p)}{1-\delta_0(x^++m_0)}.
$$

接下来，我们定义 \(\Gamma_\alpha(z) = u_\alpha(-m_0, z)$。我们有

$$
\begin{aligned}
\Gamma_\alpha(z) &= G_\alpha(s_\alpha(z), z) + (p+c)m_0 \\
&= c s_\alpha(z) + \alpha E[u_\alpha(s_\alpha(z)-z_2, z_2)|z_1=z] + (p+c)m_0 \\
&= g_\alpha(s_\alpha(z), z) + \alpha E[\Gamma_\alpha(z_2)|z_1=z] \\
&\quad + \alpha E \left[ \int_{-m_0}^{s_\alpha(z)-z_2} \chi_\alpha(\xi, z_2) d\xi \mid z_1=z \right]
\end{aligned}
$$

其中

(12.5.37)
$$
\begin{aligned}
g_\alpha(x,z) &= c(1-\alpha)x + \alpha E[h(x-z_2)^+ + p(x-z_2)^-] \\
&\quad + c E[z_2|z_1=z] + (p+c)m_0(1-\alpha)
\end{aligned}
$$

因此，我们可以写成

(12.5.38)
$$
\Gamma_\alpha(z) = \Psi_\alpha(z) + \alpha E[\Gamma_\alpha(z_2)|z_1=z],
$$

其中
\[
\Psi_\alpha(z) = g_\alpha(s_\alpha(z), z) + \alpha E \left[ \int_{-m_0}^{s_\alpha(z)-z_2} \chi_\alpha(\xi, z_2) d\xi \mid z_1 = z \right].
\]

我们注意到 \(|s_\alpha(z)| \le m_0$。使用估计 (12.5.36)，我们看到 \(|\Psi_\alpha(z)| \le C$。然后我们定义
\[
\rho_\alpha = \int \Psi_\alpha(z) \varpi(2) dz,
\]

以及 \(\bar{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1-\alpha}$。根据遍历理论，我们可以断言
\[
\sup_z |\bar{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3-\beta}{1-\beta} \le C,
\]

并且我们可以陈述估计
\[
\left| u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha} \right| \le C + \frac{C(x+m_0)^+}{1-\delta_0((x+m_0)^+)} + C(x+m_0)^-.
\]

定义 \(\tilde{u}_\alpha(x, z) = u_\alpha(x, z) - \frac{\rho_\alpha}{1-\alpha}$。我们将方程 (12.5.1) 写为
(12.5.39) $$\tilde{u}_\alpha(x, z) + \rho_\alpha = \inf_{v \ge 0} [K \mathbf{1}_{v>0} + l(x, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)].$$

根据引理 12.4，我们可以断言最优反馈满足
\[
\max(-m_0, x) \le x + \hat{v}(x, z) \le \max(x^+, m_0).
\]

因此，我们可以用以下内容替换 (12.5.39)
\[
\begin{aligned}
\tilde{u}_\alpha(x, z) + \rho_\alpha &= \inf_{\max(-m_0, x) \le x+v \le \max(x^+, m_0)} [K \mathbf{1}_{v>0} + l(x, v) + \alpha \Phi^v \tilde{u}_\alpha(x, z)] \\
&= \inf_{\max(-m_0, x) \le x+v \le \max(x^+, m_0)} L_\alpha(x, z, v).
\end{aligned}
\]

接下来
\[
L_\alpha(x, z, v) - L_\alpha(x, z', v) = \alpha \int \tilde{u}_\alpha(x+v-\zeta, \zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta
\]

对于 \(\max(-m_0, x) \le x \le v \le \max(x^+, m_0)$，我们可以写成
\[
|\tilde{u}_\alpha(x+v-\zeta, \zeta)| \le C + \frac{C(\max(x^+, m_0)+m_0)}{1-\delta_0(\max(x^+, m_0)+m_0)} + C\zeta
\]

使用假设 (12.5.23) 和 (12.5.24)，我们很容易得到
\[
|\tilde{u}_\alpha(x, z) - \tilde{u}_\alpha(x, z')| \le \left( C + \frac{C(\max(x^+, m_0)+m_0)}{1-\delta_0(\max(x^+, m_0)+m_0)} \right) \delta|z-z'|.
\]

从所得估计中，我们可以断言 \(\tilde{u}_\alpha(x, z)$ 有一个收敛子序列（仍记为 \(\alpha\)），意义为
(12.5.40) $$\sup_{|x| \le M, |z| \le N} |\tilde{u}_\alpha(x, z) - u(x, z)| \to 0, \text{ as } \alpha \to 1.$$

由于 \(\rho_\alpha$ 有界，我们总可以假设 \(\rho_\alpha \to \rho$。记
\[
L(x, z, v) = K \mathbf{1}_{v>0} + l(x, v) + \Phi^v u(x, z)
\]

则
\[
L_\alpha(x, z, v) - L(x, z, v) = \alpha \Phi^v (\tilde{u}_\alpha - u)(x, z) - (1-\alpha) \Phi^v u(x, z)
\]

对于 \(\max(-m_0, x) \le x + v \le \max(x^+, m_0)$，我们有，假设 \(M > m_0\)

$$
\sup_{|x| \le M, z} |\Phi^v u(x, z)| \le C + \frac{CM}{1 - \delta_0(2M)}
$$

我们还有

$$
\begin{aligned}
\sup_{|x| \le M, z} |\Phi^v (\bar{u}_\alpha - u)(x, z)| &\le \sup_{|x| \le M, z} |\bar{u}_\alpha - u(x, z)| \sup F(N, z) \\
&\quad + \sup_{|x| \le M, z} |\bar{u}_\alpha - u(x, z)|
\end{aligned}
$$

使用假设 (12.5.26) 和 (12.5.40)，先令 $\alpha \to 1$，再令 $N \to \infty$，我们推导出

$$
\sup_{|x| \le M} |L_\alpha(x, z, v) - L(x, z, v)| \to 0, \text{ as } \alpha \to 1.
$$

因此，我们很容易推导出 (12.5.31)，并且对 \(u(x, z), \rho$ 满足 (12.5.34)。估计 (12.5.32), (12.5.33) 立即从 \(\bar{u}_\alpha(x, z)$ 上的相应估计得出。\(u$ 的 \(K\)-凸性来自 \(\bar{u}_\alpha$ 的 \(K\)-凸性。证明已完成。

## 12.6. 学习过程

### 12.6.1. 模型. 在本节中，我们遵循 [33]。我们已经在 12.2 节的示例 12.1 中考虑过马尔可夫需求的一个例子，其中马尔可夫依赖是通过需求的概率定律的一个参数获得的。需求 $z_{n+1}$ 的概率定律取决于一个参数，即 $f(x, \lambda)$，但 \(\lambda\) 不是固定的。它是 \(z_n, \lambda(z_n)$ 的函数。我们在这里展示，当参数并不真正已知，而是根据可用信息进行更新时，常见的学习程序（这相当自然）会导致类似的情况。我们只考虑有积压的库存模型，以明确概念。因此，我们有

(12.6.1) $$y_{n+1} = y_n + v_n - z_{n+1}, y_1 = x.$$

$z_{n+1}$ 的概率密度是 $f(z, \lambda_n)$，其中 \(\lambda_n$ 是在时间 \(n\) 赋予参数 \(\lambda$ 的值。与其写 \(\lambda_n = \lambda(z_n)$，不如表达一个演化

(12.6.2) $$\lambda_{n+1} = \rho(\lambda_n, z_{n+1}), \lambda_1 = \lambda.$$

对 \(y_n, \lambda_n$ 是一个受控马尔可夫链，其算子由

(12.6.3)
$$
\begin{aligned}
\Phi^v \varphi(x, \lambda) &= E[\varphi(x+v-z_2, \rho(\lambda, z_2))] \\
&= \int \varphi(x+v-\zeta, \rho(\lambda, \zeta)) f(\zeta, \lambda) d\zeta
\end{aligned}
$$

给出。

观测过程是需求。因此，我们定义滤流

$$
\begin{aligned}
\mathcal{F}^n &= \sigma(z_2, \cdots, z_n), n \ge 2 \\
\mathcal{F}^1 &= \{\emptyset, \Omega\}
\end{aligned}
$$


且控制过程 \(v_n\) 相对于滤流 \(\mathcal{F}^n\) 是自适应的。我们定义每期的成本函数

(12.6.4) \( l(x, v) = hx^+ + px^- + cv. \)

令 \(V = \{v_1, \cdots, v_n, \cdots\}\) 为一种控制策略，我们定义成本泛函

(12.6.5) \( J_{x, \lambda}(V) = E \left[ \sum_{n=1}^\infty \alpha^{n-1} l(y_n, v_n) | y_1 = x, \lambda_1 = \lambda \right]. \)

我们考虑值函数

(12.6.6) \( u(x, \lambda) = \inf_V J_{x, \lambda}(V), \)

以及贝尔曼方程

(12.6.7) \( u(x, \lambda) = hx^+ + px^- - cx + \inf_{y \ge x} [\alpha y + \alpha \Phi^u(u, \eta, \lambda)]. \)

### 12.6.2. 可缩性。

如预期，贝尔曼方程 (12.6.7) 是一个二维问题。我们在此仅描述一种情况：通过一个有趣的性质——*可缩性*，问题可以降维到一维。我们说，若存在如下关系，则称函数 \(g(\lambda)\) 具有可缩性

(12.6.8) \( f(x, \lambda) = \frac{f(x/q(\lambda))}{q(\lambda)}, \quad q(\rho(\lambda, x)) = q(\lambda) U\left(\frac{x}{q(\lambda)}\right). \)

下面给出几个例子。第一个是函数

(12.6.9) \( f(x, \lambda) = \frac{k \alpha x^{k-1}}{(\lambda + x^k)^{\alpha+1}}. \)

这个概率密度称为韦布尔-伽马分布。其原因是它由韦布尔分布与伽马分布组合而成。假设我们考虑一个韦布尔分布

\(\psi(y, x) = k y x^{k-1} \exp - y x^k,\)

它依赖于参数 \(y\)。然而，参数 \(y\) 是未知的。人们认为它是随机的，其密度为

\(g(y, \lambda) = \frac{\lambda^\alpha y^{\alpha-1} \exp - y \lambda}{\Gamma(a)},\)

这里回顾，当 \(a > 0\) 时

\(\Gamma(a) = \int_0^{+\infty} x^{a-1} \exp - x \, dx.\)

我们立即看到

\(f(x, \lambda) = \int_0^{+\infty} \psi(y, x) g(y, \lambda) \, dy.\)

若 \(\rho(\lambda, x) = \lambda + x^k\)，则由 (12.6.9) 定义的函数 \(f(x, \lambda)\) 具有可缩性。函数 \(g(\lambda)\)、\(f(x)\)、\(U(x)\) 定义如下

(12.6.10) \( q(\lambda) = \lambda \bar{k}, \quad f(x) = \frac{k \alpha x^{k-1}}{(1+x^k)^{\alpha+1}}, \quad U(x) = (1+x^k) \bar{k}. \)

第二个例子是伽马-伽马模型，其中

(12.6.11) $$f(x, \lambda) = \frac{\lambda^x x^{k-1} \Gamma(k+a)}{(x+\lambda)^{k+a} \Gamma(a) \Gamma(k)}.$$

这个概率密度可以通过组合一个伽马概率密度得到

$$\psi(x, y) = \frac{y^x x^{k-1} \exp^{-y}}{\Gamma(k)},$$

与另一个伽马概率密度

$$g(y, \lambda) = \frac{\lambda^a y^{a-1} \exp^{-y\lambda}}{\Gamma(a)}.$$

若 \(\rho(\lambda, x) = \lambda + x\)，则概率密度 (12.6.11) 具有可缩性。函数 \(q(\lambda)\)、\(f(x)\)、\(U(x)\) 定义如下

(12.6.12) $$q(\lambda) = \lambda, \quad f(x) = \frac{x^{k-1} \Gamma(k+a)}{(1+x)^{k+a} \Gamma(a) \Gamma(k)}, \quad U(x) = 1+x.$$

下面展示如何利用可缩性性质将贝尔曼方程的维度降至 1。

方程 (12.6.7) 写作

(12.6.13) $$u(x, \lambda) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int u(\eta - \zeta, \rho(\lambda, \zeta)) f(\zeta, \lambda) d\zeta \right].$$

将 \(f(\zeta, \lambda)\) 替换后，我们得到

$$u(x, \lambda) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int u(\eta - \zeta, \rho(\lambda, \zeta)) \frac{f\left(\frac{\zeta}{q(\lambda)}\right)}{q(\lambda)} d\zeta \right].$$

我们可以找到如下形式的解

$$u(x, \lambda) = v\left(\frac{x}{q(\lambda)}\right) q(\lambda),$$

其中 \(v(x)\) 是以下方程的解

(12.6.14) $$v(x) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int v\left(\frac{\eta - \zeta}{U(\zeta)}\right) U(\zeta) f(\zeta) d\zeta \right],$$

这是一个一维问题。

本页故意留空

## 提前量与延误

### 13.1. 引言

在迄今考虑的所有模型中，我们都假设在时间 \(n\) 下达的订单 \(v_n\) 将在时间 \(n+1\) 交付。另一种等价的方式是：将 \(n\) 视为第 \(n\) 期的初始时间，交付在期末完成，这也是第 \((n+1)\) 期的开始。交付时间，称为*提前量*，为 1。在本章中，我们将考虑更复杂的情况，其中提前量大于 1。可能出现多种情况，最简单的是提前量是一个固定的确定性数 \(L\)。它也可以是一个随机变量，甚至是一个随机过程。在提前量期间，订单可能存在限制，例如提前量期间无法下订单，或者可以无限制地下订单。

关于延误，我们将考虑信息接收中的延误。在前面的章节中，延误为 0。事实上，需求在实现时被观察到；第 \(n\) 期的需求在第 \(n\) 期末实现，这也是时间 \(n+1\)，此时订单 \(v_{n+1}\) 被决定。

在这些问题中，动态并非无关紧要。积压情况（库存演变为线性的情况）可以带来重要的简化，其中一个有趣的概念——*库存位置*——起着主要作用。

### 13.2. 带库存位置的模型

### 13.2.1. 确定性提前量。

我们在此假设提前量 \(L \ge 1\)。当然，\(L=1\) 是标准情况。需求是一系列独立同分布的随机变量 \(D_1, \cdots, D_n, \cdots\)。我们定义滤流

$\mathcal{F}^n = \sigma(D_1, \cdots, D_n), \quad \mathcal{F}^0 = (\emptyset, \Omega).$

控制 \(V = (v_1, \cdots, v_n, \cdots)\) 相对于滤流 \(\mathcal{F}^{n-1}\) 是自适应的。若用 \((y_1, \cdots, y_n, \cdots)\) 表示库存序列，初始库存为 \(y_1 = x\)，则有关系式

(13.2.1) \( y_{n+L} = y_{n+L-1} + v_n - D_{n+L-1}, \quad y_1 = x. \)

我们注意到，我们允许积压的可能性。此外，库存 \(y_1, \cdots, y_L\) 不依赖于控制，而不仅仅是 \(y_1\)。如果 \(L \ge 2\)，引入待收订单 \(x_1, \cdots, x_{L-1}\) 将在时间 \(2, \cdots, L\) 收到，这很方便。它们是给定值，就像初始值 \(x\) 一样。因此我们有关系式

(13.2.2) \( y_j = x + x_1 + \cdots + x_{j-1} - D_1 - \cdots - D_{j-1}, 2 \le j \le L, \)

其中 \(L \ge 2\)。接下来我们定义每期成本

(13.2.3) \( C(v) = K \mathbf{1}_{v>0} + cv, \quad l(x) = hx^+ + px^-. \)

引入向量 \(X = (x, x_1, \cdots, x_{L-1}) \in R^L\)。我们可以定义目标泛函

(13.2.4) 
$$J_X(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{j=1}^{L-1} \alpha^{j-1} El(y_j) + \sum_{n=1}^\infty \alpha^{n-2+L} El(y_{n+L-1}).$$

如果 \(L=1\)，中间求和消失，我们恢复标准成本目标。这个中间求和是 \(X\) 的给定函数，不依赖于控制。其余部分通过 \(y_L\) 依赖于 \(X\)，因此实际上仅通过以下数字依赖于 \(X\)

(13.2.5) 
$$z = x + x_1 + \cdots + x_{L-1}.$$

因此我们可以写成

$$J_X(V) = \sum_{j=1}^{L-1} \alpha^{j-1} El(y_j) + \bar{J}_z(V),$$

其中

(13.2.6) 
$$\bar{J}_z(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{n=1}^\infty \alpha^{n-2+L} El(y_{n+L-1}).$$

注意，\(z\) 表示初始库存加上待交付量之和。它被称为*库存位置*。类似地，对于 \(L \ge 2\)，我们使用

$$y_{n+L-1} = y_n + v_{n-1} + \cdots + v_{n-L+1} - (D_n + \cdots + D_{n+L-2}),$$

采用记号

$$v_0 = x_{L-1}; v_{-1} = x_{L-2} \cdots; v_{2-L} = x_1,$$

以定义

$$\begin{aligned} z_n &= y_{n+L-1} + D_n + \cdots + D_{n+L-2} \\ &= y_n + v_{n-1} + \cdots + v_{n-L+1}, \end{aligned}$$

这是时间 \(n\) 的库存位置。我们有 \(z_1 = z\)。然后我们有演化

(13.2.7) 
$$z_{n+1} = z_n + v_n - D_n.$$

这证明了过程 \(z_n\) 相对于滤流 \(\mathcal{F}^{n-1}\) 是自适应的。接下来

$$l(y_{n+L-1}) = l(z_n - (D_n + \cdots + D_{n+L-2})).$$

但是 \(D_n, \cdots, D_{n+L-2}\) 与 \(z_n\) 独立。因此

$$\alpha^{L-1} El(y_{n+L-1}) = E\bar{l}(z_n),$$

其中

(13.2.8) 
$$\bar{l}(x) = \alpha^{L-1} El\left(x - \sum_{j=1}^{L-1} D_j\right).$$

然后我们可以写成

(13.2.9) 
$$\bar{J}_z(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{n=1}^\infty \alpha^{n-1} E\bar{l}(z_n).$$

问题已被简化为一个标准问题，用库存位置替换库存，并用 \(\bar{l}(x)\) 替换函数 \(l(x)\)。




**备注 13.1.** 当不允许积压时，前述变换失效。动态规划仍然可行，但我们需要在 \(R^L\) 中工作。

### 13.2.2. 分析证明。

在前面的分析中，我们基于控制本身进行了推理，并展示如何将其归约为库存位置的一维问题。我们在此给出一个分析证明，遵循 Karlin 和 Scarf，参见 [1]。思路是遵循备注 13.1 并在空间 \(R^L\) 中写出 Bellman 方程。时刻 \(n\) 的状态是一个向量

\[
Y_n = (y_n^1, y_n^2, \cdots, y_n^{L-1}).
\]

解释很简单。第一个分量 \(y_n\) 是现有库存，\(y_n^1, \cdots, y_n^{L-1}\) 表示按到达顺序排列的待处理订单；\(y_n^1\) 将在时刻 \(n+1\) 到达，\(y_n^{L-1}\) 将在时刻 \(n+L-1\) 到达。我们有初始条件

\[
Y_1 = (x, x_1, \cdots, x_{L-1}).
\]

演化方程如下

\[
\begin{aligned}
y_{n+1} &= y_n + y_n^1 - D_n; \\
y_{n+1}^1 &= y_n^2; \\
\cdots \\
y_{n+1}^{L-2} &= y_n^{L-1}; \\
y_{n+1}^{L-1} &= v_n.
\end{aligned}
\tag{13.2.10}
\]

在时刻 \(n\) 决定的 \(v_n\) 将在时刻 \(n+L\) 到达。由 (13.2.10) 容易推导出 (13.2.1)。成本泛函定义为

\[
J_X(V) = \sum_{n=1}^{\infty} \alpha^{n-1} (C(v_n) + l(y_n)).
\tag{13.2.11}
\]

记

\[
w(X) = w(x, x_1, \cdots, x_{L-1}) = \inf_V J_X(V).
\tag{13.2.12}
\]

Bellman 方程为

\[
w(x, x_1, \cdots, x_{L-1}) = l(x) + \inf_{v \ge 0} [C(v) + \alpha E w(x + x_1 - D_1, x_2, \cdots, x_{L-1}, v)].
\tag{13.2.13}
\]

如果考虑相对于库存位置的 Bellman 方程，对于值函数 \(\bar{J}_z(V)\)，

\[
u(z) = \inf_V \bar{J}_z(V),
\tag{13.2.14}
\]

则有

\[
u(z) = \bar{l}(z) + \inf_{v \ge 0} [C(v) + \alpha E u(z + v - D)].
\tag{13.2.15}
\]

### 提议 13.1.

有公式

\[
w(x, x_1, \cdots, x_{L-1}) = u(x + x_1 + \cdots + x_{L-1}) + G(x, x_1, \cdots, x_{L-2}),
\tag{13.2.16}
\]

其中

\[
G(x, x_1, \cdots, x_{L-2}) = l(x) + \sum_{j=1}^{L-2} \alpha^j E l(x + x_1 + \cdots + x_j - (D_1 + \cdots + D_{L-1})).
\tag{13.2.17}
\]

证明. 将 (13.2.16) 代入 (13.2.13)，其中 u(z) 是 (13.2.15) 的解，则得到 G 的函数关系，即

\[
\bar{l}(x) + G(x, x_1, \cdots, x_{L-2}) = l(x) + \alpha E G(x + x_1 - D, x_2, \cdots, x_{L-1}),
\]

通过直接验证，我们看到由 (13.2.17) 定义的 G 满足所需关系。

### 13.2.3. 多级库存问题。

该问题由 Clark 和 Scarf 的开创性论文引入，参见 [16]。我们将考虑 $L=2$。因此有

\[
y_{n+1} = y_n + y_n^1 - D_n; \qquad y_{n+1}^1 = v_n.
\tag{13.2.18}
\]

然而，订单 $v_n` 并非简单地在市场上下达。它是从一个上层设施获得的，称为设施 2，而直接与客户接触的设施称为设施 1。只有设施 2 在市场上购买。因此我们引入设施 2 的库存，记为 \(\eta_n\)，其演化定义为

\[
\eta_{n+1} = \eta_n + \bar{v}_n - v_n,
\tag{13.2.19}
\]

其中 \(\bar{v}_n\) 是外部购买的。我们需要施加约束

\[
0 \le v_n \le \eta_n,
\tag{13.2.20}
\]

这表示数量 \(v_n\) 必须在设施 2 上可用，以便由设施 1 订购。注意库存 \(\eta_n \ge 0\)。引入量很方便

\[
\xi_n = \eta_n + y_n + y_n^1,
\]

Clark-Scarf 称之为系统库存。它显然满足演化方程

\[
\xi_{n+1} = \xi_n + \bar{v}_n - D_n.
\tag{13.2.21}
\]

每期成本涉及 $C(v_n)$、$C_1(\bar{v}_n)$ 以及成本 $l(y_n)$、$l_1(\xi_n)$。当然，人们可能期望与 \(\eta_n\) 以及可能与 \(y_n^1\) 相关的成本。这些成本被汇总为仅取决于系统库存的成本，这是一种限制。当 \(y_n, y_n^1, \eta_n\) 的持有成本相同且为线性时，此假设将得到满足。这要归功于 \(y_n^1, \eta_n \ge 0\) 的事实。定义控制策略

\[
V = \{v_1, \bar{v}_1, \cdots, v_n, \bar{v}_n, \cdots \},
\]

控制策略相对于滤流 $\mathcal{F}^{n-1}$ 是自适应的。回顾约束 (13.2.20)，它可以表示为

\[
0 \le v_n \le \xi_n - y_n - y_n^1.
\tag{13.2.22}
\]

用 \(\{x, x_1, \xi\}\) 表示初始状态。我们可以定义成本目标

\[
J_{x, x_1, \xi}(V) = \sum_{n=1}^\infty \alpha^{n-1} [C(v_n) + C_1(\bar{v}_n) + l(y_n) + l_1(\xi_n)],
\tag{13.2.23}
\]

以及值函数

\[
\Psi(x, x_1, \xi) = \inf_V J_{x, x_1, \xi}(V),
\tag{13.2.24}
\]

则值函数是 Bellman 方程的解

\[
\Psi(x, x_1, \xi) = l(x) + l_1(\xi) + \inf_{\substack{0 \le v \le \xi - (x + x_1) \\ \bar{v} \ge 0}} [C(v) + C_1(\bar{v}) + \alpha E \Psi(x + x_1 - D, v, \xi + \bar{v} - D)]
\tag{13.2.25}
\]

参数满足 \(x_1 \ge 0, x + x_1 \le \xi - D\)。接下来我们考虑前一节中 \(L=2\) 的问题，即方程 (13.2.13)，也就是 \(w(x, x_1)\) 满足

\[
w(x, x_1) = l(x) + \inf_{v \ge 0} [C(v) + \alpha E w(x + x_1 - D, v)]
\tag{13.2.26}
\]

根据提议 13.1 可知

\[
w(x, x_1) = l(x) + u(x + x_1)
\tag{13.2.27}
\]

其中

\[
u(z) = \tilde{l}(z) + \inf_{v \ge 0} [(C(v) + \alpha E u(z + v - D))]
\tag{13.2.28}
\]

以及 \(\tilde{l}(z) = \alpha E l(z - D)\)。我们将假设

\[
C(v) = cv
\tag{13.2.29}
\]

因此我们排除了设置成本的情况。在这种情况下，函数 \(u(z)\) 是凸的，最优反馈由基准库存策略 \(S\) 给出。定义

\[
G(\eta) = c\eta + \alpha E u(\eta - D)
\]

则有

\[
\inf_{\eta \ge z} G(\eta) = \left\{ \begin{array}{ll} G(S), & \text{if } z \le S \\ G(z), & \text{if } z \ge S \end{array} \right.
\tag{13.2.30}
\]

由 (13.2.28) 可写出

\[
u(z) = \tilde{l}(z) - cz + \left\{ \begin{array}{ll} G(S), & \text{if } z \le S \\ G(z), & \text{if } z \ge S \end{array} \right.
\tag{13.2.31}
\]

我们可以给出

### 定理 13.1.

对于问题 (13.2.18)、(13.2.21)、(13.2.22)、(13.2.23) 并在假设 (13.2.29) 下，Bellman 方程 (13.2.25) 的解 \(\Psi(x, x_1, \xi)\) 由以下给出

\[
\Psi(x, x_1, \xi) = l(x) + u(x + x_1) + \Phi(\xi)
\tag{13.2.32}
\]

其中 \(\Phi(\xi)\) 是 Bellman 方程的解

\[
\Phi(\xi) = l_1(\xi) + (G(\xi) - G(S)) 1_{\xi \le S} + \inf_{\bar{v} \ge 0} [C_1(\bar{v}) + \alpha E \Phi(\xi + \bar{v} - D)]
\tag{13.2.33}
\]

如果用 \(\hat{v}(\xi)\) 表示方程 (13.2.33) 定义的最优反馈，则完整 Bellman 方程 (13.2.25) 定义的最优反馈由以下给出

\[
\hat{v}(x, x_1, \xi) = \left\{ \begin{array}{ll} \xi - (x + x_1), & \text{if } x + x_1 \le \xi \le S \\ S - (x + x_1), & \text{if } x + x_1 \le S \le \xi \\ 0, & \text{if } S \le x + x_1 \le \xi \end{array} \right.
\tag{13.2.34}
\]

以及

\[
\hat{\bar{v}}(x, x_1, \xi) = \hat{v}(\xi)
\tag{13.2.35}
\]

证明. 通过直接检查，我们看到形式为 (13.2.32) 的函数将满足 (13.2.25)，如果

\[
\Phi(\xi) + \inf_{x+x_1 \le \eta} G(\eta) = l_1(\xi) + \inf_{x+x_1 \le \eta \le \xi} G(\eta) + \inf_{\tilde{v} \ge 0} [C_1(\tilde{v}) + \alpha E \Phi(\xi + \tilde{v} - D)].
\]

然而，很容易检查

\[
\inf_{x+x_1 \le \eta \le \xi} G(\eta) - \inf_{x+x_1 \le \eta} G(\eta) = \begin{cases} 0, & \text{if } \xi \ge S \\ G(\xi) - G(S), & \text{if } \xi \le S \end{cases}
\]

重要的性质是这个表达式不依赖于 \(x+x_1\)。因此 \(\Phi(\xi)\) 必须是 (13.2.33) 的解。这也意味着 (13.2.32) 右边的表达式是 (13.2.25) 的解，并且由 (13.2.34)、(13.2.35) 定义的反馈是最优的。证明完成。

### 13.2.4. 随机提前期。

我们现在假设，在时刻 \(n\) 决定订单 \(v_n\) 时的提前期是一个随机变量 \(L_n\)。我们假设限制性假设

\[
\begin{aligned}
L_{n+1} &= L_n + \epsilon_n, \quad \epsilon_n \ge 0, \quad \text{i.i.d} \\
L_1 \ge 1 \quad \text{independent of } \epsilon_n
\end{aligned}
\tag{13.2.36}
\]

因此，提前期不能随时间改善。它当然包含确定性情况，更一般地包含提前期恒定但随机的情况。这可以被视为对提前期的风险规避态度，但当然排除了任何改善的可能性。

我们还假设

\[
L_n \quad \text{independent of the demand process.}
\tag{13.2.37}
\]

\(L_n\) 与需求过程独立。

然后我们写

\[
y_{n+L_n} = y_{n+L_n-1} + v_n - D_{n+L_n-1}, \quad y_1 = x,
\tag{13.2.38}
\]

并且 \(n+L_n\) 是一个随机时间。我们再次定义库存位置

\[
z_{n+1} = y_{n+L_n} + D_{n+1} + \cdots + D_{n+L_n-1}.
\tag{13.2.39}
\]

如果 \(L_n = 1\)，我们将公式解释为 \(z_{n+1} = y_{n+1}\)。我们注意到

\[
y_{n+L_n} = y_{n+1-L_{n-1}} + v_n - (D_{n+1-L_{n-1}} + \cdots + D_{n+L_n-1}),
\]

因为只有 \(v_n\) 在时间 \(n-1+L_{n-1}\)（不包括）和 \(n+L_n\) 之间到达。因此我们又有

\[
z_{n+1} = z_n + v_n - D_n.
\tag{13.2.40}
\]

过程 \(z_n\) 相对于 \(\mathcal{F}^{n-1}\) 是自适应的。要定义 \(z_1\)，我们必须考虑时刻 1 的待处理订单。这意味着我们必须考虑 \(n \le 0\) 的 \(v_n\)。我们写 \(v_{-k}, k \ge 0\)。由于必须有

\[
L_{-k} - k \ge 2,
\]

为了使订单 \(v_{-k}\) 在时刻 1 处于待处理状态，这样的订单只能有有限个，尽管这个数量 \(k^*\) 可以是随机的。我们有

\[
z_1 = x + \sum_{k=0}^{k^*} v_{-k},



并且必须有

$$L_{-k+1} \ge L_{-k} \ge L_{-k^*} \ge k^* + 2.$$

由此可得

$$z_n = y_n + \sum_{-k^* \le k \le n-1 \\ k+L_k \ge n+1} v_k.$$

当然，订单 $v_{-k}$ 是已知的。因此，只需给出时刻 1 的库存位置，即 $z_1 = z$。考虑成本目标

$$J(V) = \sum_{j=1}^\infty \alpha^{j-1} EC(v_j) + \sum_{j=1}^\infty \alpha^{j-1} El(y_j).$$

基于我们对提前期的假设，函数 $n + L_n$ 关于 $k$ 严格单调递增。因此我们可以写成

$$J(V) = \sum_{j=1}^\infty \alpha^{j-1} EC(v_j) + E \sum_{j=1}^\infty \alpha^{j-1} El(y_j) + \sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j)$$

接下来

$$E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = E \alpha^{n+L_{n-1}-2} \sum_{k=0}^{L_n-L_{n-1}-1} \alpha^k l(y_{n-1+L_{n-1}+k}).$$

然而

$$y_{n-1+L_{n-1}+k} = y_{n-1+L_{n-1}} - (D_{n-1+L_{n-1}} + \cdots + D_{n-2+L_{n-1}+k}), \quad 0 \le k \le L_n - L_{n-1},$$ 其中当 $k=0$ 时求和省略。这是因为在时刻 $n-1+L_{n-1}+k$（$1 \le k \le L_n - L_{n-1}$）没有订单到达。考虑到 $y_{n-1+L_{n-1}+1}$ 的值，我们得到

$$y_{n-1+L_{n-1}+k} = z_n - (D_n + \cdots + D_{n-2+L_{n-1}+k}), \quad 0 \le k \le L_n - L_{n-1}.$$

因此

$$\sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^\infty E \alpha^{n+L_{n-1}-2} \cdot L_n - L_{n-1} \sum_{k=0}^{L_n-L_{n-1}} \alpha^k l(z_n - (D_n + \cdots + D_{n+L_{n-1}+k-2})).$$

定义函数

(13.2.41) $$\lambda(i, x) = El(x - (D_1 + \cdots + D_i)), \quad i \ge 0,$$ 其中当 $i=0$ 时求和省略。因此，$\lambda(0, x) = l(x)$。

从独立性性质出发，可以写成

$$\sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^\infty \alpha^{n-1} E \alpha^{L_{n-1}-1} \sum_{k=0}^{L_{n-1}-1} \alpha^k \lambda(L_{n-1}-1+k; z_n)$$

接下来定义

(13.2.42) $$\bar{I}_n(x) = E \alpha^{L_{n-1}-1} \sum_{k=0}^{\epsilon_{n-1}} \alpha^k \lambda(L_{n-1} + 1 + k, x).$$

从需求和提前期的独立性出发，我们得到

$$\sum_{n=1}^{\infty} E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^{\infty} \alpha^{n-1} E \bar{I}_n(z_n).$$

接下来，量 \(E \sum_{j=1}^{L_n-1} \alpha^{j-1} El(y_j)\) 是固定的，与控制无关。因此我们最终得到以下优化问题

(13.2.43) $$J_\epsilon(V) = \sum_{n=1}^{\infty} \alpha^{n-1} E C(v_n) + \sum_{n=1}^{\infty} \alpha^{n-1} E \bar{I}_n(z_n),$$

伴随演化 (13.2.40)。这个问题不是标准的，因为它是非平稳的。每个周期 \(n\) 的成本取决于 \(n\)。为了简化记号，本书未处理非平稳问题。然而，动态规划的技术可以适应无限时域的非平稳问题。与有限时域情况不同，它不会归约为一个序列。它仍然是一个函数方程，因为无法启动该序列。

如果 \(L_n = L$（随机），则 \(\epsilon_n = 0$。在这种情况下

$$\bar{I}_n(x) = \bar{I}(x) = E \alpha^{L-1} \lambda(L-1, x),$$

如果 $L$ 是确定的，我们恢复 (13.2.8)。

## 13.3. 没有库存位置的模型

### 13.3.1. 订购约束

我们考虑第 13.2.1 节的模型，其中提前期 $L$ 是确定的。然而，我们将在订购过程中引入一个约束。当有未决订单时，不能下单。因此，未决订单的数量最多为一个。订购策略 \(V\) 由一系列订购时刻组成

$$\tau_1, \cdots, \tau_j, \cdots,$$

它们是 \(\mathcal{F}^{n-1}$ 停时。对每个订购时刻 \(\tau_j\)，关联一个数量 \(v_{\tau_j}\)，它是 \(\mathcal{F}^{\tau_j-1}$ 可测的，即订购量。新的元素是通常条件 \(\tau_j \le \tau_{j+1}$ 被约束所取代

$$\tau_{j+1} \ge \tau_j + L.$$

库存演化如下

$$y_{n+1} = y_n + v_n - D_n, \quad y_1 = x,$$

其中

$$v_n = 0, \quad \text{if } n \neq \tau_j, \text{ for some } j.$$

目标函数与通常相同

$$J_\epsilon(V) = \sum_{n=1}^{\infty} \alpha^{n-1} (l(y_n) + C(v_n)),$$

价值函数是

$$u(x) = \inf_V J_\epsilon(V).$$

### 13.3.2. 动态规划

考虑到初始时刻的可能性，很容易推导出 Bellman 方程。如果时刻 0 没有订单，那么可以达到的最佳结果是

$$l(x) + \alpha E u(x - D).$$

另一方面，如果在时刻 0 下一个大小为 $v$ 的订单，由于没有未决订单，这是可能的，那么库存演化如下

$$y_1 = x;$$
$$y_2 = x - D_1;$$
$$\dots$$
$$y_{L+1} = x - (D_1 + \dots + D_L) + v,$$

可以达到的最佳结果是

$$K + c v + l(x) + E \sum_{j=2}^L \alpha^{j-1} l(-(D_1 + \dots + D_{j-1})) + \alpha^L E u(x + v - (D_1 + \dots + D_L)).$$

从这些考虑中，我们可以轻松推导出 Bellman 方程

(13.3.1) $$u(x) = \min \left\{ \begin{array}{l} l(x) + \alpha E u(x - D), \\ K - c x + E \sum_{j=0}^{L-1} \alpha^j l(x - D^{(j)}) + \inf_{\eta \ge x} \{ c \eta + \alpha^L E u(\eta - D^{(L)}) \} \end{array} \right\}$$

其中我们使用记号

$$D^{(j)} = D_1 + \dots + D_j \text{ if } j \ge 1, \text{ if } j = 0$$

### 13.3.3. (s, S) 策略

首先，通过引入常数 $s \in R$，并将 $u(x)$ 变换为 $H_s(x)$，使用公式来变换 (13.3.1)

(13.3.2) $$u(x) = -c x + E \sum_{j=0}^{L-1} \alpha^j l(x - D^{(j)}) + C_s + H_s(x),$$

其中 $C_s$ 将在下面定义。事实上，令

$$g(x) = (1 - \alpha) c x + \alpha^L E l(x - D^{(L)}),$$

然后取

$$C_s = \frac{g(s) + \alpha c \bar{D}}{1 - \alpha},$$

其中 \(\bar{D}\) 是 \(D\) 的期望值。

我们然后注意公式

$$E \sum_{j=0}^{L-1} \alpha^j g(x - D^{(j)}) = c x (1 - \alpha^L) - \alpha c \bar{D} \frac{1 - \alpha^L}{1 - \alpha} + \alpha^L c D L + E \sum_{j=0}^{L-1} \alpha^{j+L} l(x - D^{(j+L)})$$

我们然后检查 \(H_s(x)\) 是以下方程的解

(13.3.3) $$H_s(x) = \min \left\{ \begin{array}{l} g(x) - g(s) + \alpha E H_s(x - D), \\ K + \inf_{\eta \ge x} \left[ E \sum_{j=0}^{L-1} \alpha^j (g(\eta - D^{(j)}) - g(s)) + \alpha^L E H_s(\eta - D^{(L)}) \right] \end{array} \right\}.$$

另一方面，对于任何 \(s\)，我们以唯一的方式定义以下方程的解

(13.3.4) $$H_s(x) = g(x) - g(s) + \alpha E H_s(x - D), \quad x \ge s$$
$$= 0, \quad x \le s$$

我们在 (13.3.3) 和 (13.3.4) 之间使用了相同的记号 \( H_s(x) $，因为我们想要找到 \(s\)，使得 (13.3.4) 的解也是 (13.3.3) 的解。记 \( \mu(x) = g'(x) $，(13.3.4) 的解明确给出为

(13.3.5) $$H_s(x) = \int_s^x \Gamma(x - \eta) f(\eta) d\eta, x > s,$$

其中我们回顾 \( \Gamma(x) $ 是以下方程的解

(13.3.6) $$\Gamma(x) = 1 + \alpha \int_0^x \Gamma(x - \eta) f(\eta) d\eta, x > 0.$$

令

$$g_s(x) = (g(x) - g(s)) \mathbb{I}_{x \ge s},$$

那么 (13.3.4) 的解满足

(13.3.7) $$H_s(x) = g_s(x) + \alpha E H_s(x - D), \forall x.$$

从这个关系出发，经过迭代我们推导出

$$H_s(x) = E \sum_{j=0}^{L-1} \alpha^j g_s(x - D^{(j)}) + \alpha^L E H_s(x - D^{(L)}),$$

因此还有

$$E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) + \alpha^L E H_s(x - D^{(L)}) = H_s(x) + E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) \mathbb{I}_{x - D^{(j)} < s},$$

定义

(13.3.8) $$\Psi_s(x) = H_s(x) + E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) \mathbb{I}_{x - D^{(j)} < s},$$

那么如果我们希望 \( H_s(x) $ 满足 (13.3.3)，我们必须有

(13.3.9) $$H_s(x) = \min \left\{ g(x) - g(s) + \alpha E H_s(x - D), K + \inf_{\eta > x} \Psi_s(\eta) \right\}.$$

这个关系激励了 \(s\) 的选择。我们想要找到 \(s\)，使得

(13.3.10) $$K + \inf_{\eta > s} \Psi_s(\eta) = 0.$$

如果这样的 \(s\) 存在，我们定义 \( S = S(s) $ 为取得下确点的点。

(13.3.11) $$\inf_{\eta > s} \Psi_s(\eta) = \Psi_s(S(s)).$$

注意，当 \( L = 1 \) 时，对于 \( x > s \)，\( \Psi_s(x) $ 与 \( H_s(x) $ 重合。





## 13.3.4. 双 s, S 的存在与刻画

我们回顾一下

(13.3.12) \(\mu(x) = (1-\alpha)c + \alpha^L h - \alpha^L(h+p)\bar{F}^{(L)}(x),\)

其中 \(F^{(L)}(x)\) 是 \(D^{(L)}\) 的累积分布函数，且 \(\bar{F}^{(L)}(x) = 1 - F^{(L)}(x)\)。我们假设

(13.3.13) \((1-\alpha)c - \alpha^L p < 0.\)

存在唯一的 \(\bar{s} > 0\)，使得

\(\mu(x) \le 0, \text{ if } x \le \bar{s}, \mu(x) \ge 0, \text{ if } x \ge \bar{s}.\)

接下来我们对函数 \(\Psi(x)\) 进行进一步计算。我们有

\(E[(g(x-D^{(j)}) - g(s)) \mathbb{1}_{x-D^{(j)} < s}]\)
\(= -E[D^{(j)} > x-s] \left( \int_{x-D^{(j)}}^s \mu(\xi) d\xi \right)\)
\(= -\int_{-s}^{+\infty} dF^{(j)}(\zeta) \int_{x-\zeta}^s \mu(\xi) d\xi\)
\(= -\int_{-s}^{+\infty} \bar{F}^{(j)}(\zeta) \mu(x-\zeta) d\zeta\)
\(= -\int_{-\infty}^x F^{(j)}(x-\xi) \mu(\xi) d\xi\)
\(= -\int_{-\infty}^x F^{(j)}(x-\xi) \mu(\xi) d\xi + \int_s^x \bar{F}^{(j)}(x-\xi) \mu(\xi) d\xi.\)

我们接着验证

\(H_s(x) \sum_{j=0}^{L-1} \alpha^j \int_s^x \bar{F}^{(j)}(x-\xi) \mu(\xi) d\xi\)
\(= \frac{1-\alpha^L}{1-\alpha} (g(x) - g(s)) + \sum_{j=L}^{\infty} \alpha^j \int_s^x F^{(j)}(x-\xi) \mu(\xi) d\xi.\)

该公式对任意 \(x\) 成立，且当 \(x < s$ 时积分项消失。汇总结果，可得公式

(13.3.14) \(\Psi_s(x) = \frac{1-\alpha^L}{1-\alpha} (g(x) - g(s)) + \sum_{j=L}^{\infty} \alpha^j \int_s^x F^{(j)}(x-\xi) \mu(\xi) d\xi\)
\(-((1-\alpha)c + \alpha^L h) D \sum_{j=1}^{L-1} j \alpha^j\)
\(+ \alpha^L (h+p) \sum_{j=1}^{L-1} \alpha^j \int_0^{+\infty} \bar{F}^{(j)}(\zeta) \bar{F}^{(L)}(x-\zeta) d\zeta.\)

由此可见，\(\Psi_s(x)\) 下有界，且当 \(x \to +\infty$ 时趋于 \(+\infty$。因此，对 \(x \ge s$ 的下确界可达，我们可以定义 \(S(s)\) 为最小下确界。

### 提议 13.2. 我们假设 (13.3.13)。则有

(13.3.15) \(\max_s \Psi_s(S(s)) = \Psi_s(S(\bar{s})) \ge 0,\)

(13.3.16)

\(\Psi_s(S(s)) \to -\infty, \text{ as } s \to -\infty\)

(13.3.17)

\(\Psi_s(S(s)) \to -((1-\alpha)c + \alpha^L h)D \sum_{j=1}^{L-1} j \alpha^j, \text{ as } s \to +\infty.\)

存在且仅存在 (13.3.10) 的一个解，满足 \(s \le \bar{s}\)。

证明. 我们计算

\(\Psi'_s(x) = \frac{1-\alpha^L}{1-\alpha}\mu(x) + \sum_{j=L}^\infty \alpha^j \int_s^x f^{(j)}(x-\xi)\mu(\xi)d\xi\)
\(-\alpha^L(h+p) \sum_{j=1}^{L-1} \alpha^j \int_0^x F^{(j)}(\xi)f^{(L)}(x-\xi)d\xi\)

也可以写成

(13.3.18)

\(\Psi'_s(x) = \gamma(x) + \sum_{j=L}^\infty \alpha^j \int_s^x f^{(j)}(x-\xi)\mu(\xi)d\xi,\)

与

(13.3.19)

\(\gamma(x) = \frac{1-\alpha^L}{1-\alpha}((1-\alpha)c - \alpha^L p) + \alpha^L(h+p) \sum_{j=0}^{L-1} \alpha^j \int_0^x F^{(j)}(x-\xi)f^{(L)}(\xi)d\xi.\)

函数 \(\gamma(x)\) 是递增的，且

\(\gamma(x) = \frac{1-\alpha^L}{1-\alpha}((1-\alpha)c - \alpha^L p) < 0, \forall x \le 0, \gamma(+\infty) = \frac{1-\alpha^L}{1-\alpha}((1-\alpha)c + \alpha^L h),\)

因此存在唯一的 \(s^*\)，使得

\(\gamma(x) < 0, \forall x < s^*, \gamma(x) > 0, \forall x > s^*, \gamma(s^*) = 0, s^* > 0.\)

注意

\(\mu(x) \frac{1-\alpha^L}{1-\alpha} - \gamma(x) = \alpha^L(h+p) \sum_{j=0}^{L-1} \alpha^j \int_0^x \bar{F}^{(j)}(x-\xi)f^{(L)}(\xi)d\xi.\)

当 \(x \le 0$ 或 \(L=1$ 时，该量消失。否则

\(\mu(x) \frac{1-\alpha^L}{1-\alpha} - \gamma(x) > 0, \forall x > 0, L \ge 2\)

由于 \(\gamma(s^*)=0$，我们有 \(\mu(s^*) > 0\)，故 \(0 < \bar{s} < s^*\)。

接下来，若 \(s \ge s^*\)，则对所有 \(x \ge s$ 有 \(\Psi'_s(x) \ge 0\)，故 \(S(s) = s\)。因此

\(\Psi_s(S(s)) = -((1-\alpha)c + \alpha^L h)D \sum_{j=1}^{L-1} j \alpha^j\)
\(+ \alpha^L(h+p) \sum_{j=1}^{L-1} \alpha^j \int_0^{+\infty} \bar{F}^{(j)}(\xi)\bar{F}^{(L)}(s-\xi)d\xi\)

该函数关于 \(s$ 单调递减，且当 \(s \to +\infty$ 时收敛于 \(-((1-\alpha)c+\alpha^L h)D \sum_{j=1}^{L-1} j \alpha^j\)。现在考虑 \(\bar{s} < s < s^*\)。我们注意到

\(\Psi'_s(s) = \gamma(s) < 0,\)

\(\Psi'_s(s^*) = \sum_{j=L}^\infty \int_s^{s^*} f^{(j)}(s^* - \xi) \mu(\xi) d\xi > 0,\)

因此在此情况下

\(\bar{s} < S < S(s) < s^*.\)

若 \(s < \bar{s}$，则我们可以断言

\(s < \bar{s} < S(s).\)

确实，对于 \(s < x < \bar{s}$，由公式 (13.3.18) 可见 \(\Psi'_s(x) < 0\)。然而，在此情况下我们无法比较 \(S(s)\) 与 \(s^*\)。

接下来我们研究 \(\Psi_s(S(s))$ 的行为。我们已经看到，对于 \(s > s^*$，函数 \(\Psi_s(S(s))$ 单调递减至负常数

\(-((1-\alpha)c+\alpha^L h)D \sum_{j=1}^{L-1} j \alpha^j.\)

此情形下

(13.3.20) \(\frac{d}{ds}\Psi_s(S(s)) = -\alpha^L(h+p) \sum_{j=1}^{L-1} \alpha^j \int_0^{\bar{s}} \bar{F}^{(j)}(\zeta) f^{(L)}(s - \zeta) d\zeta, s > s^*.\)

注意 \(s > 0$。若 \(s < s^*$，则 \(s < S(s)$，因此

\(\frac{d}{ds}\Psi_s(S(s)) = \frac{\partial \Psi_s}{\partial s}(S(s)),\)

故

(13.3.21) \(\frac{d}{ds}\Psi_s(S(s)) = -\mu(s) \left[ \frac{1-\alpha^L}{1-\alpha} + \sum_{j=L}^\infty \alpha^j F^{(j)}(S(s) - s) \right].\)

注意在 \(s = s^*$ 处两个公式一致，因为

\(-\mu(s^*) \frac{1-\alpha^L}{1-\alpha} = -\alpha^L(h+p) \sum_{j=1}^{L-1} \alpha^j \int_0^{\bar{s}} \bar{F}^{(j)}(\zeta) f^{(L)}(s^* - \zeta) d\zeta,\)

这很容易验证，只需回忆 \(s^*$ 的定义（\(\gamma(s^*) = 0\)）并进行简单计算即可。由此可见，\(\Psi_s(S(s))$ 在 \((s, s^*)$ 上单调递减，在 \((-\infty, \bar{s}]$ 上单调递增。最后，\(\Psi_s(S(s))$ 在 \((\bar{s}, +\infty)$ 上单调递减，在 \((-\infty, \infty)$ 上单调递增。因此它在 \(\bar{s}$ 处取得最大值。由 \(\Psi_s(x)$、\(H_s(x)$（\(x > \bar{s}$）的公式以及 \(s$ 是 \(g$ 的最小值这一事实，我们立即得到 \(\Psi_s(S(s)) \ge 0$。

最后，对于 \(s < 0$，我们有

\(\Psi_s(S(s)) \le \Psi_s(0)\)

\(= ((1-\alpha)c-\alpha^L p) \left[ \frac{1-\alpha^L}{1-\alpha} (-\bar{s}) + \sum_{j=L}^\infty \alpha^j \int_s^0 F^{(j)}(-\xi) d\xi - D \sum_{j=1}^{L-1} j \alpha^j \right],\)

当 \(s \to -\infty$ 时，该表达式趋于 \(-\infty$。因此，随着 \(s$ 从 \(-\infty$ 增长到 \(\bar{s}$，\(\Psi_s(S(s))$ 从 \(-\infty$ 单调递增至一个正数。因此，存在且仅存在一个 \(s < \bar{s}$ 满足 (13.3.10)。证明完成。

## 13.3.5. 作为 s, S 策略的解

还需看看由 (13.3.5) 定义的函数 \(H_s(x)$（其中 \(s$ 是 (13.3.10) 的解）是否确实是方程 (13.3.9) 的解。与其使用 \(\Psi_s(x)$，不如使用另一个函数，即

(13.3.22)

\(\Phi_s(x) = H_s(x) + E \sum_{j=1}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) \mathbb{I}_{-x - D^{(j)} < s},\)

它与 \(\Psi_s(x)$ 的区别仅在于删除了对应 \(j=0$ 的项。显然

\(\Phi_s(x) = \Psi_s(x), \forall x \ge s.\)

然而，当 \(x < s$ 时，两个函数相差一项

\(\Psi_s(x) = \Phi_s(x) + g(x) - g(s), \forall x < s.\)

注意，在求解 \(S$ 时，使用哪个函数都无所谓。另请注意，当 \(L=1$ 时，对所有 \(x$ 有 \(\Phi_s(x) = H_s(x)$。现在我们有

\(\inf_{\eta > x} \Psi_s(\eta) = \inf_{\eta > x} \Phi_s(\eta).\)

当 \(x > s$ 时，该等式显而易见，因为两个函数相同。若 \(x < s$，我们有

\(\inf_{\eta > x} \Psi_s(\eta) = \inf_{\eta > x} \Phi_s(\eta) = \inf_{\eta > x} \Phi_s(\eta) = -K.\)

例如

\(\inf_{\eta > x} \Psi_s(\eta) = \min \left[ \inf_{\eta > x} \Psi_s(\eta), \inf_{x < \eta < \bar{s}} \Psi_s(\eta) \right],\)

且 \(\inf_{\eta > x} \Psi_s(\eta) = -K\)，而

\(\inf_{x < \eta < \bar{s}} \Psi_s(\eta) = \inf_{x < \eta < \bar{s}} E \sum_{j=0}^{L-1} \alpha^j (g(\eta - D^{(j)}) - g(s)) \mathbb{I}_{-x - D^{(j)} < s} > 0,\)

故得结果。因此 (13.3.9) 变为

(13.3.23)

\(H_s(x) = \min \left\{ g(x) - g(s) + \alpha E H_s(x - D), K + \inf_{\eta > x} \Phi_s(\eta) \right\}.\)

对于 \(x < s$，该关系简化为

\(0 = \min[g(x) - g(s), 0]\)

这成立，因为 \(g(x)$ 在 \(x < s$ 时单调递减。接下来我们考虑 \(x > s$。由于 \(H_s(x)$ 等于括号中的第一项。因此，我们需要证明的是

(13.3.24)

\(H_s(x) \le K + \inf_{\eta > x} \Phi_s(\eta), \forall x > s.\)

事实上，我们无法对所有 \(L$ 的值都证明 (13.3.24)。我们知道当 \(L=1$ 时它成立。我们将稍后对泊松需求进行证明。对于一般需求分布，我们有



### **提议 13.3.** 我们假设

\[
(13.3.25) \quad \alpha^L((1-\alpha)c - \alpha^L p)(L-1)D + K(1-\alpha) \ge 0,
\]

则性质 (13.3.24) 得到满足。

证明。我们注意到，此结果包含 L = 1 的情况，此时条件自动满足。证明与 L = 1 的情况类似。

我们回顾

\[
(13.3.26) \quad H_s(x) - \alpha E H_s(x - D) = g_s(x), \forall x.
\]

我们接着为 \(\Phi_s(x)\) 找到一个类似方程。这里重要的是要考虑 \(\Phi_s(x)\) 而不是 \(\Psi_s(x)\)，因为我们为任何 x 写出方程，而不仅仅是 x > s。很容易验证 \(\Phi_s(x)\) 是

\[
(13.3.27) \quad \Phi_s(x) - \alpha E \Phi_s(x - D) = g_s(x) + \alpha E(g(x - D) - g(s)) \mathbb{I}_{s-D < s} - \alpha^L E(g(x - D^{(L)}) - g(s)) \mathbb{I}_{s-D^{(L)} < s},
\]

的解，并且我们再次检查，当 L = 1 时，该方程与 (13.3.26) 重合。回到 (13.3.24) 我们回顾

\[
K + \inf_{\eta \ge x} \Phi_s(\eta) \ge K + \inf_{\eta > s} \Phi_s(\eta) = 0, \forall x > s.
\]

所以只需对 \(x > x_0 > s\) 证明 (13.3.24)，其中 \(x_0\) 是大于 s 的第一个值，使得 \(H_s(x) \ge 0\)。我们必然有 \(H_s(x_0) = 0\)。我们有 \(s < \xi < x_0\)。让我们固定 \(\xi > 0\)。我们考虑区域 \(x \ge x_0 - \xi\)。我们可以写

\[
(13.3.28) \quad H_s(x) - \alpha E H_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \le g_s(x), \forall x,
\]

利用事实

\[
E H_s(x - D) \mathbb{I}_{x-D < x_0 - \xi} \le 0.
\]

接下来定义

\[
M_s(x) = \Phi_s(x + \xi) + K.
\]

我们注意到 \(M_s(x) > 0, \forall x\)。

\[
M_s(x) - \alpha E M_s(x - D) = g_s(x + \xi) + \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{x + \xi - D < s} - \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{x + \xi - D^{(L)} < s} + K(1 - \alpha)
\]

并且利用 M 的正性我们可以断言

\[
(13.3.29) \quad M_s(x) - \alpha E M_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \ge g_s(x + \xi) + \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{x + \xi - D < s} - \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{x + \xi - D^{(L)} < s} + K(1 - \alpha)
\]

我们现在考虑区域 \(x \ge x_0 - \xi\) 中的差值 \(Y_s(x) = H_s(x) - M_s(x)\)。

我们有

\[
(13.3.30) \quad Y_s(x) - \alpha E Y_s(x - D) \mathbb{I}_{x-D \ge x_0 - \xi} \le g_s(x) - g_s(x + \xi) - \alpha E(g(x + \xi - D) - g(s)) \mathbb{I}_{x + \xi - D < s} + \alpha^L E(g(x + \xi - D^{(L)}) - g(s)) \mathbb{I}_{x + \xi - D^{(L)} < s} - K(1 - \alpha)
\]

我们从 L = 1 的情况，定理 9.11 中看到

\[
g_s(x + \xi) - g_s(x) \ge 0, \forall x \ge x_0 - \xi.
\]

接下来考虑函数

\[
\chi_s(y) = \alpha E(g(y - D) - g(s)) \mathbb{I}_{y-D < s} - \alpha^L E(g(y - D^{(L)}) - g(s)) \mathbb{I}_{y-D^{(L)} < s},
\]

对于 \( y \ge x_0 \)。我们检查

\[
X_s(y) = \int_{-\infty}^s d\zeta \mu(\zeta) \int_{y-\zeta}^{\infty} (-\alpha f(\eta) + \alpha^L f^{(L)}(\eta)) d\eta,
\]

所以事实上

\[
X_s(y) = \int_{-\infty}^s \mu(\zeta)(-\alpha \bar{F}(y-\zeta) + \alpha^L \bar{F}^{(L)}(y-\zeta)) d\zeta.
\]

注意在积分中，\( \mu(\zeta) < 0 \)，因为 \( s < \bar{s} \)。我们推导

\[
X_s(y) \ge \alpha^L \int_{-\infty}^s \mu(\zeta)(\bar{F}^{(L)}(y-\zeta) - \bar{F}(y-\zeta)) d\zeta.
\]

注意 \( \bar{F}^{(L)}(y-\zeta) - \bar{F}(y-\zeta) \ge 0 \)，并且 \( \mu(\zeta) \ge ((1-\alpha)c - \alpha^L p) \)。因此

\[
X_s(y) \ge \alpha^L((1-\alpha)c - \alpha^L p) \int_{-\infty}^s (\bar{F}^{(L)}(y-\zeta) - \bar{F}(y-\zeta)) d\zeta,
\]

并且由于 \( y \ge s \),

\[
\begin{aligned}
X_s(y) &\ge \alpha^L((1-\alpha)c - \alpha^L p) \int_{-\infty}^y (\bar{F}^{(L)}(y-\zeta) - \bar{F}(y-\zeta)) d\zeta \\
&= \alpha^L((1-\alpha)c - \alpha^L p) \int_0^\infty (\bar{F}^{(L)}(u) - \bar{F}(u)) du \\
&= \alpha^L((1-\alpha)c - \alpha^L p)(L-1)\bar{D}
\end{aligned}
\]

由于假设 (13.3.25) 我们可以断言

\[
Y_s(x) - \alpha E Y_s(x - D) \mathbb{I}_{x - D \ge x_0 - \xi} \le 0, \forall x \ge x_0 - \xi.
\]

另外

\[
Y_s(x_0 - \xi) \le -\Phi_s(x_0) - K \le -K,
\]

因为 \( \Phi_s(x_0) \ge H_s(x_0) = 0 \)。由此可得

\[
Y_s(x) \le 0, \forall x \ge x_0 - \xi,
\]

这是所期望的结果。

### 13.3.6. 泊松需求

我们给出

### **提议 13.4.** 我们假设需求服从泊松分布，那么 (13.3.24) 成立。

证明。我们将证明

\[
(13.3.31) \quad H'_s(x) \ge 0, \text{if } x \ge x_0,
\]

那么 (13.3.24) 将立即得出，因为对于 \( x \ge x_0 \)

\[
H_s(x) \le H_s(x+\xi) \le \Phi_s(x+\xi) \le \Phi_s(x+\xi) + K, \forall \xi \ge 0
\]

假设

\[
f(x) = \beta \exp -\beta x,
\]

那么，我们知道（参见第 9.3.5 节）：

\[
\Gamma(x) = \frac{1}{1-\alpha} - \frac{\alpha}{1-\alpha} \exp -\beta(1-\alpha)x, x > 0,
\]

并且

\[
\mu(x) = c(1-\alpha) + \alpha h - \alpha(p+h) \exp -\beta x^+.
\]

我们有

\[
H'_s(x) = \mu(x) + \int_s^x \Gamma(x-\xi)\mu(\xi)d\xi,
\]

因此

\[
H'_s(x) = \mu(x) + \alpha\beta \exp-\beta(1-\alpha)x \int_s^x \exp \beta(1-\alpha)\xi \mu(\xi)d\xi,
\]

并且

\[
H_s(x) = \int_s^x \frac{\mu(\xi)}{1-\alpha}d\xi - \frac{\alpha}{1-\alpha} \exp-\beta(1-\alpha)x \int_s^x \exp \beta(1-\alpha)\xi \mu(\xi)d\xi.
\]

我们回顾

\[
H_s(x) \le 0, \forall x < x_0, H_s(x_0) = 0.
\]

现在令 \(x_1\) 使得

\[
\int_s^{x_1} \exp \beta(1-\alpha)\xi \mu(\xi)d\xi = 0.
\]

如果 \(x_1 \le x_0\)，则从 \(H'_s(x)\) 的公式、\(H'_s(x_0) > 0\) 以及 \(\mu(x)\) 单调递增的事实来看，我们立即看到 \(H'_s(x) \ge 0\) 当 \(x \ge x_0\)。所以假设 \(s < x_0 < x_1\)。对于 \(x \ge x_1\)

\[
H'_s(x) \ge H'_s(x_1) \ge H'_s(x_0) > 0.
\]

剩下区间 \((x_0, x_1)\)。我们知道 \(H'_s(x_1) \ge H'_s(x_0) \ge 0\)。如果区间中存在一点使得 \(H'_s(x) < 0\)，必然存在一点 \(\xi\) 使得

\[
x_0 < \xi < x_1, H'_s(\xi) = 0.
\]

如果我们引入

\[
\lambda(x) = \mu(x) \exp \beta(1-\alpha)x, \rho(x) = \frac{\lambda(x)}{\int_s^x \lambda(u)du},
\]

那么 \(\xi\) 满足 \(\rho(\xi) = -\alpha\beta\)。根据 \(x_1\) 的定义，

\[
\int_s^x \lambda(u)du < 0, \forall s < x < x_1,
\]

并且 \(\lambda'(x) > 0\)。因此

\[
\rho'(x) = \frac{\lambda(x) \int_s^x \lambda(u)du - \lambda^2(x)}{(\int_s^x \lambda(u)du)^2} < 0.
\]

此外

\[
H'_s(x_0) > 0 \Rightarrow \lambda(x_0) + \alpha\beta \int_s^{x_0} \lambda(u)du > 0,
\]

因此

\[
\rho(x_0) + \alpha\beta < 0.
\]

所以 \(\rho(x) < -\alpha\beta, \forall x \in [x_0, x_1]\)。点 \(\xi\) 不能存在。所以 \(H'_s(x) > 0, \forall x \in [x_0, x_1]\)。结果已被证明。\(\square\)

## 13.4. 信息延迟

我们将在此研究以下情况：信息不是立即获得，而是在某个延迟后获得。这是部分信息的一个特例，但更简单。给定可用信息的库存条件分布可以用某些充分统计量替代，因此问题仍然是有限维的。我们将依赖文献 [6], [7]。

### 13.4.1. 模型与预备知识。

设 $\Omega, \mathcal{A}, P$ 为概率空间。时间是离散的，并且存在一个过程 $D_t, t = 1, 2, \cdots$，即独立同分布随机变量。一般变量 $D$ 的累积分布函数是 $F(x)$，概率密度是 $f(x)$。对每个时刻 $t$ 关联一个随机变量 $\theta_t$，表示在时刻 $t$ 接收信息的延迟。特别是，时刻 $t - \theta_t$ 的库存将在时刻 $t$ 已知，前提是该数严格为正。然而 $t - \theta_t$ 不一定是时刻 $t$ 可用信息的最新时刻。时刻 $t$ 的最新信息时间称为 *年份*。如果用 $\beta_t$ 表示它，那么该过程由演化定义

\[
(13.4.1) \quad \beta_t = \max(t - \theta_t, \beta_{t-1}), t \ge 2 \quad \beta_1 = 1.
\]

$\beta_1 = 1$ 的事实意味着我们知道初始库存。库存演化如下

\[
(13.4.2) \quad y_{t+1} = y_t + v_t - D_t, \quad y_1 = x.
\]

我们可以引入滤流

\[
\mathcal{F}^t = \sigma(D_1 \cdots D_{t-1}),
\]

在之前研究的情况下，订单 $v_t$ 是 $\mathcal{F}^{t-1}$ 可测的。这不再是这种情况。令

\[
(13.4.3) \quad z_t = y_{\theta_t}.
\]

时刻 $t$ 可用的信息是对 $z_t, \beta_t$ 和该对的先前值。我们因此定义观测的滤流

\[
(13.4.4) \quad \mathcal{Z}^t = (\sigma(z_2, \beta_2) \cdots \sigma(z_t, \beta_t)), t \ge 2.
\]

当 $\theta_t = 0$ 时，我们有 $\beta_t = t$ 和 $\mathcal{Z}^t = \mathcal{F}^t$。订单 $v_t$ 适应于 $\mathcal{Z}^t$。对于 $t = 1$ 我们有 $\mathcal{Z}^1 = \{\Omega, \emptyset\}$ 和 $z_1 = y_1 = x$。我们还注意到

\[
(13.4.5) \quad \beta_{t-1} \le \beta_t \le t.
\]

为了继续构建模型，我们需要对延迟过程做出假设。首先我们假设 $\theta_t$ 取值于有限状态空间 $\mathcal{M} = \{0, 1, \cdots, M\}$。此外 $\theta_t$ 是具有转移概率矩阵 $P = (p_{ij})$ 的马尔可夫链，其中

\[
p_{ij} = P(\theta_{t+1} = j | \theta_t = i).
\]

我们还假设两个过程 $\theta_t$ 和 $D_t$ 相互独立。

### 13.4.2. 库存位置。

我们引入 *库存位置*

\[
(13.4.6) \quad x_t = \begin{cases} z_t, & \text{if } \beta_t = t \\ z_t + \sum_{j=\beta_t}^{t-1} v_j, & \text{if } \beta_t < t \end{cases}
\]

我们可以证明

### **引理 13.1.** 以下关系成立

\[
(13.4.7) \quad x_{t+1} = x_t + v_t - \mathbb{I}_{\beta_{t+1} > \theta_t} \sum_{j=\beta_t}^{\beta_{t+1}-1} D_j, \quad x_1 = z_1 = y_1 = x
\]

\[
(13.4.8) \quad y_t = x_t - \sum_{j=\beta_t}^{t-1} D_j, \text{ if } \beta_t < t





过程 $x_t$ 是可观测的。

证明。库存位置可观测的事实直接从其定义得出。第二个关系来自

$x_t = y_{\beta_t} + \sum_{j=\beta_t}^{t-1} v_j$

$y_t = y_{\beta_t} + \sum_{j=\beta_t}^{t-1} v_j - \sum_{j=\beta_t}^{t-1} D_j$

要证明第一个，首先注意

$z_{t+1} - z_t = y_{\beta_{t+1}} - y_{\beta_t}$

$= \sum_{j=\beta_t}^{\beta_{t+1}-1} (v_j - D_j), \text{if } \beta_t < \beta_{t+1}$

通过考虑所有情况，(13.4.7) 很容易得出。

现在考虑一期成本

$c(x, v) = C(v) + l(x),$

其中

$C(v) = K \mathbf{1}_{v>0} + cv, l(x) = hx^+ + px^-,$

以及一个控制

$V = (v_1, \cdots, v_t, \cdots), v_t \text{ is } \mathcal{Z}^t \text{ measurable.}$

目标函数是

$J(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} c(y_t, v_t),$

从 (13.4.8) 得到

$c(y_t, v_t) = c \left( x_t - \sum_{j=\beta_t}^t D_j, v_t \right) = C(v_t) + l \left( x_t - \sum_{j=\beta_t}^t D_j \right),$

其中当 $\beta_t = t$ 时求和消失。过程 $\beta_t$ 与需求过程独立。由于需求是独立随机变量，很容易检查 $D_{\beta_t}, \cdots, D_t$ 与 $\mathcal{Z}^t$ 独立。因此，如果我们引入如下记号

$l^{(i)}(x) = E l \left( x - \sum_{j=1}^i D_j \right), i \ge 1, l^{(0)}(x) = l(x),$

那么我们可以将目标函数重写为

(13.4.9) \( J(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} (C(v_t) + l^{(t-\beta_t)}(x_t)). \)

这种写法的重要属性在于三个过程 $x_t, v_t, \beta_t$ 都是 $\mathcal{Z}^t$ 可测的。然而 $\beta_t$ 不是马尔可夫链，因此用这个过程不方便。我们将引入一个新的马尔可夫链，从中可以轻松推导出 $\beta_t$。

### 13.4.3. 新马尔可夫链。

我们引入日历时间，即在 $t$ 之前观察到延迟的最大时间。因此

$\tau_t = \max_{1 \le j \le t} \{j : \beta_{j-1} < \beta_j\},$

因此

$\beta_{\tau_t} = \tau_t - \theta_{\tau_t};$  
$\beta_{\tau_t+1} = \dots = \beta_t = \beta_{\tau_t}.$

我们然后设置

$\sigma_t = t - \tau_t, \quad \eta_t = \theta_{\tau_t},$

因此，对 $\beta_t, \tau_t$ 可以通过公式从对 $\sigma_t, \eta_t$ 轻松推导

(13.4.10)  
$\beta_t = t - \sigma_t - \eta_t, \quad \tau_t = t - \sigma_t.$

由于 $\beta_t \ge t - \theta_t$，我们得到 $\sigma_t + \eta_t \le \theta_t, \sigma_t \ge 0, \eta_t \ge 0$。因此过程 $\sigma_t, \eta_t$ 取值于 $\mathcal{M} \times \mathcal{M}$。而且

$\sigma_t + \eta_t \le M, \quad \sigma_t \le t - 1.$

重要结果是

**提议 13.5。** 对 $\sigma_t, \eta_t$ 是在状态空间 $\mathcal{M} \times \mathcal{M}$ 上的马尔可夫链，具有性质 $\sigma_t + \eta_t \le M$。它是相对于滤流 $\mathcal{Z}^t$ 的过程。

证明。我们首先定义转移。假设 $\sigma_t = \sigma, \eta_t = \eta$，其中 $\sigma, \eta$ 是两个满足 $\sigma \ge 0, \eta \ge 0, \sigma + \eta \le M$ 的数。假设 $\sigma + \eta = M$。那么如果 $\beta_{t+1} = \beta_t$，我们有

$\tau_{t+1} = \tau_t = t - \sigma, \quad \sigma_{t+1} = t + 1 - \tau_{t+1} = \sigma + 1.$

另一方面 $\eta_{t+1} = \eta$ 且我们得到 $\sigma_{t+1} + \eta_{t+1} = M + 1$，这是不可能的。因此 $\beta_{t+1} > \beta_t$，这意味着 $\tau_{t+1} = t + 1$，因此 $\sigma_{t+1} = 0$。变量 $\eta_{t+1}$ 可以取值 $0, \cdots, M$。接下来假设 $\sigma + \eta < M$。我们可能有 $\beta_{t+1} = \beta_t$，在这种情况下 $\sigma_{t+1} = \sigma + 1$ 且 $\eta_{t+1} = \eta$。否则 $\beta_{t+1} > \beta_t$，这意味着 $\sigma_{t+1} = 0$。但此时

$\eta_{t+1} = t + 1 - \beta_{t+1} < t + 1 - \beta_t = \sigma + \eta + 1.$

因此 $\eta_{t+1}$ 可以取值 $0, \cdots, \sigma + \eta$。转移总结如下：

如果 $\sigma + \eta < M$

(13.4.11)  
$\sigma, \eta \Rightarrow \begin{cases} \sigma' = \sigma + 1, \eta' = \eta \\ \sigma' = 0, \eta' = k, \quad 0 \le k \le \sigma + \eta \end{cases}$

如果 $\sigma + \eta = M$

(13.4.12)  
$\sigma, \eta \Rightarrow \sigma' = 0, \eta' = k, \quad 0 \le k \le M$

我们现在可以定义转移概率矩阵。我们首先注意到 $\theta_{t-\sigma} = \eta$，且

$\beta_{\tau_t+1} = t - \sigma - \eta = \max(t - \sigma + 1 - \theta_{\tau_t+1}, \beta_{\tau_t})$  
$= \max(t - \sigma + 1 - \theta_{t-\sigma+1}, t - \sigma - \eta),$

由此可得 $\theta_{t-\sigma+1} \ge \eta + 1$。类似地

$\theta_{t-\sigma+2} \ge \eta + 2, \cdots, \theta_t \ge \eta + \sigma.$

因此如果 \(\sigma + \eta < M\)，我们有

\(P(\sigma_{t+1} = \sigma + 1, \eta_{t+1} = \eta | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\beta_t \ge t + 1 - \theta_{t+1} | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\theta_{t+1} \ge \sigma + \eta + 1 | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

接下来对于 \(0 \le k \le \sigma + \eta\)

\(P(\sigma_{t+1} = 0, \eta_{t+1} = k | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\beta_{t+1} = t + 1 - \theta_{t+1}, \theta_{t+1} = k | \sigma_t = \sigma, \eta_t = \eta)\)
\(= P(\theta_{t+1} = k | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

我们然后定义函数 \(\gamma(k; \sigma, \eta)\)，其参数为 \(0 \le k \le M, \sigma + \eta \le M, \sigma \ge 0, \eta \ge 0, \sigma \le t-1\)

(13.4.13) \(\gamma(k; \sigma, \eta) = P(\theta_{t+1} = k | \theta_{t-\sigma} = \eta, \theta_{t-\sigma+1} \ge \eta + 1, \cdots, \theta_t \ge \eta + \sigma)\)

该函数由马尔可夫链 \(\theta_t\) 及其转移概率函数唯一确定。事实上，它可以通过递归定义

(13.4.14) \(\gamma(k; \sigma, \eta) = \frac{\sum_{j=\sigma+\eta}^M p_{jk}(j; \sigma-1, \eta)}{\sum_{j=\sigma+\eta}^M \gamma(j; \sigma-1, \eta)}, \sigma \ge 1; \gamma(k; 0, \eta) = p_{\eta k}\)

马尔可夫链 $\sigma_t, \eta_t$ 的转移概率矩阵由以下给出：

如果 $\sigma + \eta < M$

(13.4.15) \(\pi(\sigma, \eta; \sigma', \eta') = \begin{cases} \gamma(k; \sigma, \eta), & \text{if } \sigma' = 0, \eta' = k, 0 \le k \le \sigma + \eta \\ \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta), & \text{if } \sigma' = \sigma + 1, \eta' = \eta \\ 0, & \text{otherwise} \end{cases}\)

如果 $\sigma + \eta = M$

(13.4.16) \(\pi(\sigma, \eta; \sigma', \eta') = \begin{cases} \gamma(k; \sigma, \eta), & \text{if } \sigma' = 0, \eta' = k, 0 \le k \le M \\ 0, & \text{otherwise} \end{cases}\)

$\sigma_t, \eta_t$ 相对于 $\mathcal{Z}^t$ 可适应的事实源于过程的定义。

事实上，马尔可夫链 $\sigma_t, \eta_t$ 从 $t=1$ 开始不是平稳的，因为约束 $\sigma_t \le t-1$。它从 $t \ge M+1$ 开始变得平稳。在后续内容中，我们将舍弃这个暂态阶段，并认为从一开始就处于平稳情况。从 (13.4.7) 和 (13.4.9) 我们可以写出

(13.4.17) \(J(V) = E \sum_{t=1}^\infty \alpha^{t-1} (C(v_t) + [l^{\sigma_t, \eta_t}(x_t)]),\)

以及

(13.4.18) \(x_{t+1} = x_t + v_t - \mathbb{I}_{\sigma_{t+1} + \eta_{t+1} \le \sigma_t + \eta_t} \sum_{j=\sigma_t + \eta_t + 1}^{\sigma_t + \eta_t} D_{t,j}\)

其中我们设置 $D_{t,j} = D_{t-j}$。存在一个暂态期，其中 $\sigma_t + \eta_t < t$。当 $t \ge M+1$ 时结束。在 (13.4.18) 中，随机变量 $D_{t,j}$ 同分布，独立于 $\mathcal{Z}^t$ 且相互独立。我们舍弃暂态期，并在 (13.4.17)、(13.4.18) 中从 $t=1$ 考虑马尔可夫链 $\sigma_t, \eta_t$，并通过以下方式固定初始条件

(13.4.19) \(x_1 = x, \sigma_1 = \sigma, \eta_1 = \eta, \sigma, \eta \ge 0, \sigma + \eta \le M\)

我们然后将函数 \( J(V) \) 称为 \( J_{x,\sigma,\eta}(V) \)，以强调初始条件。我们定义

(13.4.20) \( u(x, \sigma, \eta) = \inf_V J_{x,\sigma,\eta}(V) \).

如果 \( M=0 \)，则 \( \sigma_t = 0, \eta_t = 0\)，问题退化为第 9 章第 9.3 节中研究的无信息延迟的标准问题。

### 13.4.4. 动态规划。

与值函数 (13.4.20) 相关的贝尔曼方程很容易写出。我们将按以下方式写出

(13.4.21) \( u(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbf{1}_{y > x} + cy \right. \left. + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u^{(\sigma+\eta+1-k)}(y, 0, k) + \sum_{k=\sigma+\eta+1}^{M} \gamma(k; \sigma, \eta) u(y; \sigma+1, \eta) \right\} \)

其中当 \( \sigma + \eta = M \) 时最后一项求和被舍去。以等价且方便的方式写出此方程为

(13.4.22) \( u(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbf{1}_{y \ge x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\} \)

其中括号中的期望是指随机变量 \( \sigma', \eta'\)，其概率分布为 \( \pi(\sigma, \eta; \sigma', \eta')\)，其中 \( \sigma, \eta\) 固定。

### 定理 13.2。我们假设

(13.4.23) \( c(1 - \alpha) - \alpha p < 0, \)

那么 (13.5.9) 的解在空间 \( B_1 \) 中是唯一的，连续，当 \( |x| \to \infty \) 时趋于 \( +\infty\)，并且是 \( K\)-凸的。最优反馈由 \( s(\sigma, \eta)\)、\( S(\sigma, \eta)\) 策略定义。

证明。证明使用第 9 章的方法，此处不再重复。

## 13.5. 带信息延迟的遍历控制

我们想在这里研究 \( \alpha \to 1\) 的情况。我们遵循文献 [7]。

### 13.5.1. 遍历性质

马尔可夫链 \( \theta_t \) 我们对以下内容做出假设

(13.5.1) \( \varpi_0 = \min_{j \in M} p_{j0} > 0. \)

该假设保证马尔可夫链 \( \theta_t \) 是遍历的，参见第 3 章，公式 (3.6.8)。我们将推导出

### 提议 13.6。假设 (13.5.1)，则马尔可夫链 \( \sigma_t, \eta_t \) 是遍历的。

证明。只需证明

(13.5.2) \( \min_{\sigma, \eta} \pi(\sigma, \eta; 0,0) > 0. \)

但是

\( \pi(\sigma, \eta; 0,0) = \gamma(0; \sigma, \eta), \)



根据 (13.4.14)
$$\gamma(0; \sigma, \eta) \ge \varpi_0 > 0,$$
故性质 (13.5.2) 成立。让我们定义相应的不变测度 \(\mu(\sigma, \eta)\)。它是下列方程组的解，

(13.5.3) $$\sum_{\substack{\sigma \ge 0 \\ \eta \ge 0 \\ \sigma + \eta \le M}} \mu(\sigma, \eta) \pi(\sigma; \eta, \sigma', \eta') = \mu(\sigma', \eta'),$$

利用公式 (13.4.15), (13.4.16) 我们写出

(13.5.4) $$\sum_{\substack{\sigma \ge 0 \\ \eta \ge 0 \\ \eta' \le \sigma + \eta \le M}} \mu(\sigma, \eta) \gamma(\eta'; \sigma, \eta) = \mu(0, \eta'), \text{ if } \sigma' = 0, 0 \le \eta' \le M$$

(13.5.5) $$\mu(\sigma' - 1, \eta') \sum_{k=\sigma'+\eta}^{M} \gamma(k; \sigma' - 1, \eta') = \mu(\sigma', \eta'), \text{ if } 1 \le \sigma' \le M, 0 \le \eta' \le M - \sigma'.$$

由 (13.5.5) 得

(13.5.6) $$\mu(\sigma, \eta) = \mu(0, \eta) \prod_{h=1, \cdots}^{\sigma} \sum_{k=h+\eta}^{M} \gamma(k; h-1, \eta), 1 \le \sigma \le M, 0 \le \eta \le M - \sigma,$$

且 \(\mu(0, \eta)\) 由 (13.5.4) 作为解得到

(13.5.7) $$\mu(0, \eta') = \sum_{\eta=\eta'}^{M} \mu(0, \eta) \left[ \gamma(\eta'; 0, \eta) + \sum_{\sigma=1}^{M-\eta} \gamma(\eta'; \sigma, \eta) \right.$$ \
$$\left. \cdot \prod_{h=1, \cdots}^{\sigma} \sum_{k=h+\eta}^{M} \gamma(k; h-1, \eta) \right] + \sum_{\eta=0}^{\eta'-1} \mu(0, \eta) \sum_{\sigma=1}^{M-\eta} \gamma(\eta'; \sigma, \eta) \cdot \prod_{h=1, \cdots}^{\sigma} \sum_{k=h+\eta}^{M} \gamma(k; h-1, \eta), 0 \le \eta' \le M$$

其中当 \(\eta' = 0\) 时最后一项消失。这个由 \(M + 1\) 个关系组成的系统实际上只有 \(M\) 个独立关系。我们有恒等式

$$\sum_{\eta=0}^{M} \mu(0, \eta') + \sum_{\eta=0}^{M-1} \mu(0, \eta') \sum_{\sigma=1}^{M-\eta'} \prod_{h=1, \cdots}^{\sigma} \sum_{k=h+\eta'}^{M} \gamma(k; h-1, \eta')$$ \
$$= \sum_{\eta=0}^{M} \mu(0, \eta) + \sum_{\eta=0}^{M-1} \mu(0, \eta) \sum_{\sigma=1}^{M-\eta} \prod_{h=1, \cdots}^{\sigma} \sum_{k=h+\eta}^{M} \gamma(k; h-1, \eta)$$

且该表达式必须等于 1。根据 ergodic 理论，该系统有唯一解，使得 \(\mu(\sigma, \eta); \sigma \ge 0, \sigma + \eta \le 1\) 是一个概率。\(\square\)

## 13.5.2. \( K=0 \) 情况的估计。

我们考虑 Bellman 方程

$$
u_\alpha(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x)
+ \inf_{y \ge x} \left\{ cy + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}
$$

其中我们强调了对 \(\alpha\) 的依赖。由于 \(K=0\)，最优策略是一种基准库存策略，由基准库存 \(S_\alpha(\sigma, \eta)\) 定义。关于 \(x\) 的函数 \(u_\alpha(x; \sigma, \eta)\) 是连续的、凸的，并且当 \(|x| \to +\infty\) 时趋向于 \(+\infty\)。它还可如下描述

$$
u_\alpha(x; \sigma, \eta) = -cx + l^{(\sigma+\eta)}(x) + c S_\alpha
+ \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(S_\alpha; \sigma', \eta'), \forall x \le S_\alpha(\sigma, \eta)
$$

和

$$
u_\alpha(x; \sigma, \eta) = l^{(\sigma+\eta)}(x) + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), \forall x \ge S_\alpha(\sigma, \eta)
$$

该函数由于凸性而可微。让我们检查它在 \(S_\alpha(\sigma, \eta)\) 处是否连续可微。确实

$$
u'_\alpha(x; \sigma, \eta) = -c + (l')^{(\sigma+\eta)}(x), \forall x < S_\alpha(\sigma, \eta)
$$
$$
u'_\alpha(x; \sigma, \eta) = (l')^{(\sigma+\eta)}(x) + \alpha E (u'_\alpha)^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), \forall x > S_\alpha(\sigma, \eta)
$$

因为在 \(S_\alpha\) 处有

$$
-c = \alpha E (u'_\alpha)^{(\sigma+\eta+1-(\sigma'+\eta'))}(S_\alpha; \sigma', \eta'),
$$

根据基准库存的定义，导数在 \(S_\alpha\) 处的连续性得到了。

我们现在推导基准库存的一些有用性质。首先我们将澄清一些记号滥用。将 \(l^{[x]}\) 的定义应用于 Heaviside 函数 \(\mathbb{1}_{x>0}\)，我们得到 \(D_1 + \cdots + D_t\) 的累积分布函数（CDF），它在第 9 章中已被表示为 \(F^{(t)}(x)\)，参见方程 (9.2.19)。为了方便，我们将保留此记号，仅当 \(F(x)\) 表示变量 \(D\) 的 CDF 时。我们然后给出

### 命题 13.7. 我们有估计

$$
0 < S_\alpha(\sigma, \eta) < \bar{S}_\alpha(\sigma, \eta),
$$

其中 \(S_\alpha(\sigma, \eta)\) 是下式的解

$$
F^{(\sigma+\eta+1)}(S_\alpha) = \frac{\alpha(p+c)-c}{\alpha(h+p)}.
$$

### 证明. 我们首先证明性质

$$
u'_\alpha(x; \sigma, \eta) \ge (l')^{(\sigma+\eta)}(x) - c.
$$

我们知道它对 \(x \le S_\alpha(\sigma, \eta)\) 成立。因此我们可以假设 \(x > S_\alpha(\sigma, \eta)\)。根据导数的单调性，我们有

$$
(u'_\alpha)^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta') \ge (u'_\alpha)^{(\sigma+\eta+1-(\sigma'+\eta'))}(S_\alpha(\sigma, \eta); \sigma', \eta'),
$$

因此

$$
u'_\alpha(x; \sigma, \eta) \ge (l')^{(\sigma+\eta)}(x) + \alpha E (u'_\alpha)^{(\sigma+\eta+1-(\sigma'+\eta'))}(S_\alpha(\sigma, \eta); \sigma', \eta')
$$
$$
= (l')^{(\sigma+\eta)}(x) - c,
$$

从而得到 (13.5.13)。接下来，从关系式

$$
-c = \alpha E(u'_{\alpha})^{(\sigma+\eta+1-(\sigma'+\eta'))}(S_\alpha(\sigma, \eta); \sigma', \eta'),
$$

我们利用不等式

$$
-c \ge -\alpha c + \alpha E((l')^{(\sigma'+\eta')}(\sigma+\eta+1-(\sigma'+\eta'))(S_\alpha(\sigma, \eta)))
$$
$$
= -\alpha c + \alpha (l')^{(\sigma+\eta+1)}(S_\alpha(\sigma, \eta)).
$$

但根据我们的记号

$$
(l')^{(\beta)}(x) = -p + (h+p)F^{(\beta)}(x),
$$

从而我们得到

$$
0 \ge c(1-\alpha) - \alpha p + \alpha(h+p)F^{(\sigma+\eta+1)}(S_\alpha(\sigma, \eta)),
$$

故

$$
F^{(\sigma+\eta+1)}(S_\alpha(\sigma, \eta)) \le \frac{\alpha(p+c)-c}{\alpha(h+p)} = F^{(\sigma+\eta+1)}(S_\alpha),
$$

从而得到 (13.5.11) 右侧的不等式。

为了证明正性，考虑

$$
\underline{S}_\alpha = \min_{\sigma, \eta} S_\alpha(\sigma, \eta) = S_\alpha(\sigma_\alpha, \eta_\alpha)
$$

数字 \(\sigma_\alpha, \eta_\alpha\) 是定义明确的，因为只有有限个可能性。我们可以写出

$$
-c = \alpha E(u'_{\alpha})^{(\sigma+\eta+1-(\sigma'+\eta'))}(\underline{S}_\alpha, \sigma', \eta').
$$

因为 \(\underline{S}_\alpha < S_\alpha(\sigma', \eta')\)，我们有

$$
(u'_{\alpha})^{(\sigma+\eta+1-(\sigma'+\eta'))}(\underline{S}_\alpha, \sigma', \eta') = -c + (l')^{(\sigma'+\eta')}(\sigma+\eta+1-(\sigma'+\eta'))(S_\alpha)
$$
$$
= -c + (l')^{(\sigma+\eta+1)}(\underline{S}_\alpha),
$$

故

$$
-c = -\alpha c + \alpha (l')^{(\sigma+\eta+1)}(\underline{S}_\alpha),
$$

因此也

$$
F^{(\sigma_\alpha+\eta_\alpha+1)}(\underline{S}_\alpha) = \frac{\alpha(p+c)-c}{\alpha(h+p)},
$$

这意味着 \(\underline{S}_\alpha > 0\)。这证明了 (13.5.11) 的左侧不等式。

接下来使用

$$
F^{(M+1)}(S_\alpha(\sigma, \eta)) \le F^{(\sigma+\eta+1)}(S_\alpha(\sigma, \eta)) \le \frac{\alpha(p+c)-c}{\alpha(h+p)} \le \frac{p}{h+p},
$$

我们推导出

(13.5.14) \(0 < S_\alpha(\sigma, \eta) \le \bar{S},\)

其中

$$
F^{(M+1)}(\bar{S}) = \frac{p}{h+p}.
$$

我们接下来对 \(u'_\alpha(x; \sigma, \eta)\) 进行估计。我们将证明

### 命题 13.8. 以下估计成立

(13.5.15)
$$
-c - p \le u'_\alpha(x; \sigma, \eta) \le h \left(1 + \frac{1}{\varpi_0}\right) \frac{1}{F(x)}.
$$

所以如果 \(x < X\)，则可以断言

(13.5.16)
$$
-c - p \le u'_\alpha(x; \sigma, \eta) \le L_X, \quad L_X = h \left(1 + \frac{1}{\varpi_0}\right) \overline{F(X)}.
$$

### 证明. 左侧估计直接由 (13.5.13) 和 \( (l')^{(\sigma+\eta)}(x) \ge -p \) 得出。我们接下来断言

$$
u'_\alpha(x; \sigma, \eta) \le -c + h, \text{ 对所有 } x \le S_\alpha(\sigma, \eta)
$$
$$
\le h + \alpha E(u'_\alpha)^{(+)}(\sigma+\eta+1-(\sigma'+\eta'))(x; \sigma', \eta'), \text{ 对所有 } x > S_\alpha(\sigma, \eta)
$$

因此也

$$
(u'_\alpha)^+(x; \sigma, \eta) \le h + \alpha E((u'_\alpha)^+)(\sigma+\eta+1-(\sigma'+\eta'))(x; \sigma', \eta'), \text{ 对所有 } x
$$

这意味着，展开数学期望

$$
(u'_\alpha)^+(x; \sigma, \eta) \le h + (u'_\alpha)^+(x; \sigma + 1, \eta) \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta)
$$
$$
+ \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta)((u'_\alpha)^+)(\sigma+\eta+1-k)(x; 0, k).
$$

然而，对于 \(k \le \sigma + \eta\)，根据 \((u'_\alpha)^+\) 的单调性，我们有

$$
((u'_\alpha)^+)(\sigma+\eta+1-k)(x; 0, k) \le E(u'_\alpha)^+(x - D; 0, k),
$$

因此

$$
(u'_\alpha)^+(x; \sigma, \eta) \le h + (u'_\alpha)^+(x; \sigma + 1, \eta) \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta)
$$
$$
+ \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) E(u'_\alpha)^+(x - D; 0, k).
$$

设

$$
w_\alpha(x) = \sup_{\sigma, \eta} (u'_\alpha)^+(x; \sigma, \eta),
$$

我们推导出

$$
(u'_\alpha)^+(x; \sigma, \eta) \le h + w_\alpha(x) \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) + E w_\alpha(x - D) \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta)
$$
$$
= h + w_\alpha(x) - \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta)(w_\alpha(x) - E w_\alpha(x - D))
$$

我们使用

$$
\sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) \ge \varpi_0, \quad w_\alpha(x) - E w_\alpha(x - D) \ge 0,
$$

从而推导出

$$
(u'_\alpha)^+(x; \sigma, \eta) \le h + w_\alpha(x) - \varpi_0(w_\alpha(x) - E w_\alpha(x - D)),
$$





## 13.5.3. 情况 $K=0$ 的极限行为

现在可以给出 (13.5.39) 的极限。

### 定理 13.3. 假设 (13.5.1) 且

$$
(13.5.17) \quad \bar{F}(x) > 0, \forall x < \infty, \quad p > c.
$$

存在一个序列 \(\rho_\alpha\)，使得当 \(\alpha \to 1$ 时，对于一个子序列

$$
(13.5.18) \quad u_\alpha(x;\sigma,\eta) - \frac{\rho_\alpha}{1-\alpha} \to u(x;\sigma,\eta),
$$

在 \(R$ 的任何紧集上一致收敛。我们还有 \(\rho_\alpha \to \rho$。函数 \(u(x;\sigma,\eta)$ 是局部利普希茨连续的，并满足

$$
|u'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

对 \(u(x;\sigma,\eta), \rho$ 满足

$$
(13.5.19) \quad u(x;\sigma,\eta) + \rho = -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ cy + \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta) u^{(\sigma+\eta+1-k)}(y,0,k) + \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) u(y;\sigma+1,\eta) \right\}.
$$

### 证明

考虑 \(u_\alpha(0; \sigma, \eta)$。由于 \(S_\alpha(\sigma, \eta) > 0$，我们可以写出，注意到 \(\ell^{(\sigma+\eta)}(0) = p\bar{D}(\sigma + \eta)\)

$$
\begin{aligned}
u_\alpha(0; \sigma, \eta) &= p\bar{D}(\sigma + \eta) + cS_\alpha(\sigma, \eta) \\
&\quad + \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u_\alpha(S_\alpha(\sigma, \eta); \sigma + 1, \eta) \\
&\quad + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) E u_\alpha(S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-k, 0; k)}).
\end{aligned}
$$

令

$$
\begin{aligned}
G_\alpha(\sigma, \eta) &= u_\alpha(0; \sigma, \eta) - \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u_\alpha(0; \sigma + 1, \eta) \\
&\quad - \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u_\alpha(0; 0, k).
\end{aligned}
$$

利用 \(u_\alpha(0; \sigma, \eta)$ 的值，我们可以得出

$$
\begin{aligned}
G_\alpha(\sigma, \eta) &= p\bar{D}(\sigma + \eta) + cS_\alpha(\sigma, \eta) \\
&\quad + \alpha \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) (u_\alpha(S_\alpha(\sigma, \eta); \sigma + 1, \eta) - u_\alpha(0; \sigma + 1, \eta)) \\
&\quad + \alpha \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) E (u_\alpha(S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-k, 0; k)}) - u_\alpha(0; 0, k)).
\end{aligned}
$$

利用估计 (13.5.14) 和 (13.5.15)，我们很容易推导出 \(|G_\alpha(\sigma, \eta)| \le C$。\(G_\alpha(\sigma, \eta)$ 的定义也可以写成

$$
(13.5.20) \quad u_\alpha(0; \sigma, \eta) - \alpha \sum_{\sigma', \eta'} \pi(\sigma, \eta; \sigma', \eta') u_\alpha(0; \sigma', \eta') = G_\alpha(\sigma, \eta)
$$

链 \(\pi(\sigma, \eta; \sigma', \eta')$ 是遍历的，其不变测度为 \(\mu(\sigma, \eta)$。定义

$$
\rho_\alpha = \sum_{\sigma, \eta} \mu(\sigma, \eta) G_\alpha(\sigma, \eta).
$$

由于 \(\mu(\sigma, \eta)$ 是不变的，我们还有

$$
\sum_{\sigma, \eta} \mu(\sigma, \eta) u_\alpha(0; \sigma, \eta) = \frac{\rho_\alpha}{1 - \alpha}.
$$

根据遍历理论，我们还可以断言

$$
(13.5.21) \quad \left| u_\alpha(0; \sigma, \eta) - \frac{\rho_\alpha}{1 - \alpha} \right| \le C,
$$

其中常数与 \(\alpha, \sigma, \eta$ 无关。接下来定义

$$
\bar{u}_\alpha(x; \sigma, \eta) = u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1 - \alpha}.
$$

结合 (13.5.21) 和 (13.5.15)，我们可以给出以下估计

$$
(13.5.22) \quad |\bar{u}_\alpha(x; \sigma, \eta)| \le C + C \frac{|x|}{F(x)};
$$

$$
(13.5.23) \quad |(\tilde{u}_\alpha)'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

更一般地

$$
(13.5.24) \quad |(\tilde{u}_\alpha)^{(\beta)}(x;\sigma,\eta)| \le C + C \frac{|x| + \beta D}{F(x)};
$$

$$
(13.5.25) \quad |((\tilde{u}_\alpha)^{(\beta)})'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

根据 Ascoli-Arzelà 定理，我们可以找到一个子序列，使得

$$
\begin{aligned}
\rho_\alpha &\to \rho, \\
\sup_{|x| \le X} |\tilde{u}_\alpha(x;\sigma,\eta) - u(x;\sigma,\eta)| &\to 0, \\
\sup_{|x| \le X} |(\tilde{u}_\alpha)^{(\beta)}(x;\sigma,\eta) - u^{(\beta)}(x;\sigma,\eta)| &\to 0 \\
&\forall \ \sigma, \eta, \beta, X \text{ as } \alpha \to 1.
\end{aligned}
$$

根据估计 (13.5.25)，极限满足

$$
|u'(x;\sigma,\eta)| \le \frac{C}{F(x)}.
$$

回到 (13.5.27) 并回顾 \(y$ 中的下确界在 \(\max(x, S_\alpha(\sigma,\eta))$ 处取得，只要 \(x < X$，我们可以将 \(y$ 限制为 \(y \le L_X$。因此我们可以使用 \(\tilde{u}_\alpha(x;\sigma,\eta)$ 写出

$$
\begin{aligned}
\tilde{u}_\alpha(x;\sigma,\eta) + \rho_\alpha &= -cx + \ell^{(\sigma+\eta)}(x) \\
&\quad + \inf_{L_X \ge y \ge x} \left\{ cy + \alpha E \tilde{u}_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\},
\end{aligned}
$$

因此利用 \(R$ 紧集上的一致收敛，我们得到

$$
\begin{aligned}
u(x;\sigma,\eta) + \rho &= -cx + \ell^{(\sigma+\eta)}(x) \\
&\quad + \inf_{L_X \ge y \ge x} \left\{ cy + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\} \\
&\ge -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ cy + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta') \right\}.
\end{aligned}
$$

另一方面，对于任何 \(y > x$，我们还有

$$
u(x;\sigma,\eta) + \rho \le -cx + \ell^{(\sigma+\eta)}(x) + E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y;\sigma',\eta'),
$$

因此得到了 (13.5.19)。证明完成。

考虑成本函数

$$
J^\alpha_{\sigma,\eta}(V) = E \sum_{t=1}^\infty \alpha^{t-1} (c v_t + \ell^{(\sigma+\eta_t)}(x_t)),
$$

那么我们将有

$$
(13.5.26) \quad \rho = \inf_V \lim_{\alpha \to 1} (1-\alpha) J^\alpha_{\sigma,\eta}(V),
$$

仅考虑使极限存在的控制策略 \(V$。然后下确界在由基准库存特征的 \(V$ 处取得

$$
S(\sigma,\eta) = \lim_{\alpha \to 1} S_\alpha(\sigma,\eta).
$$

## 13.5.4. 情况 \(K > 0\)。

方程写作如下

$$
(13.5.27) \quad u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
$$

解由 \(s_\alpha(\sigma, \eta)$、\(S_\alpha(\sigma, \eta)$ 策略控制。因此

$$
x \le s_\alpha(\sigma, \eta) \Rightarrow u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + K + C_{\alpha, \sigma, \eta},
$$

且

$$
x \ge s_\alpha(\sigma, \eta) \Rightarrow u_\alpha(x; \sigma, \eta) = \ell^{(\sigma+\eta)}(x) + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta').
$$

我们还有连续性条件

$$
C_{\alpha, \sigma, \eta} = \inf_{y > s_\alpha(\sigma, \eta)} \left\{ cy + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
$$

函数 \(u_\alpha(x; \sigma, \eta)$ 是连续的但不是连续可微的。导数的唯一不连续点是 \(s_\alpha(\sigma, \eta)$。然而我们可以考虑不连续函数 \(u_\alpha(x; \sigma, \eta)$ 并写出

$$
u'_\alpha(x; \sigma, \eta) = -c + \ell^{(\sigma+\eta)}(x) + \chi_\alpha(x; \sigma, \eta).
$$

经过一些计算，我们可以写出方程

$$
(13.5.28) \quad \chi_\alpha(x; \sigma, \eta) = \begin{cases} \mu_\alpha^{(\sigma+\eta)}(x) + \alpha E \chi_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), & x \ge s_\alpha(\sigma, \eta) \\ 0, & x \le s_\alpha(\sigma, \eta) \end{cases}
$$

且

$$
(13.5.29) \quad \mu_\alpha(x) = c(1 - \alpha) + \alpha h - \alpha(h + p)\bar{F}(x).
$$

连续性条件则表示如下

$$
(13.5.30) \quad 0 = K + \inf_{y > s_\alpha(\sigma, \eta)} \int_{s_\alpha(\sigma, \eta)}^y \chi_\alpha(\xi; \sigma, \eta) d\xi
$$

如果定义

$$
(13.5.31) \quad G_\alpha(x; \sigma, \eta) = cx + \alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'),
$$

那么我们可以写出

$$
(13.5.32) \quad u_\alpha(x; \sigma, \eta) = -cx + \ell^{(\sigma+\eta)}(x) + G_\alpha(\max(x, s_\alpha(\sigma, \eta)); \sigma, \eta),
$$

因此

$$
(13.5.33) \quad \chi_\alpha(x; \sigma, \eta) = G'_\alpha(x; \sigma, \eta) \mathbb{1}_{x > s_\alpha(\sigma, \eta)}.
$$

我们现在陈述一个重要性质

### 引理 13.2. 假设 \(\alpha p > c$。我们有以下性质

$$
\begin{aligned}
u'_\alpha(x; \sigma, \eta) &\le -(c+p)\lambda, \quad \chi'_\alpha(x; \sigma, \eta) \le 0 \quad \forall x < 0, \\
G'_\alpha(x; \sigma, \eta) &\le c(1-\alpha) - \alpha p \quad \forall x < 0.
\end{aligned}
$$





证明. 注意，如果我们知道 \( G_{0\alpha}(x; \sigma, \eta) < 0 \)，当 \( x < 0 \) 时，则结果立即从公式 (13.5.31)、(13.5.32) 在 \( x \) 上求导后得出。为了完整性，我们考虑方程 (13.5.31)、(13.5.32) 的迭代过程，起始于 \( u_{0\alpha}(x; \sigma, \eta) = 0 \)。我们有

\( G_{0\alpha}(x; \sigma, \eta) = cx, s_{0\alpha}(\sigma, \eta) = -\infty; \)
\( u_{1\alpha}(x; \sigma, \eta) = l^{(\sigma+\eta)}(x). \)

因此，当 \( x < 0 \) 时，

\( G_{1\alpha}(x; \sigma, \eta) = cx - \alpha px + p\bar{D}(\sigma + \eta + 1), \)

这意味着 \( G_{1\alpha}^*(x; \sigma, \eta) < 0 \)，当 \( x < 0 \) 时。迭代保持这些性质。证明完成。

我们接着进行估计。

## 提议 13.9. 我们有如下估计

\( s_\alpha^-(\sigma, \eta) \le \frac{K}{\alpha p - c(1-\alpha)} = m_\alpha, \)
\( 0 \le S_\alpha(\sigma, \eta) \le \frac{\alpha p m_\alpha + \alpha(p+h)\bar{D}(\sigma + \eta + 1)}{c(1-\alpha) + \alpha h}. \)

**证明.** 我们从第一个不等式开始。只需假设 \( s_\alpha(\sigma, \eta) < 0 \)。注意，由 (13.5.33) 和引理 13.2 可得

\( \chi_\alpha(x; \sigma, \eta) \le c(1-\alpha) - \alpha p, \forall s_\alpha(\sigma, \eta) < x < 0 \)

接下来，由 (13.5.30)，因为 \( s_\alpha(\sigma, \eta) < 0 \),

\( 0 \le K + \int_{s_\alpha(\sigma, \eta)}^0 \chi_\alpha(\xi; \sigma, \eta) d\xi, \)

第一个估计立即得出。让我们继续处理第二个不等式。

回顾以下等价关系很有用：

\( Eu_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta') = E[u_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

我们还回顾最优反馈

\( \hat{v}_\alpha(x; \sigma, \eta) = \begin{cases} S_\alpha(\sigma, \eta) - x, & \text{if } x \le s_\alpha(\sigma, \eta) \\ 0, & \text{if } x > s_\alpha(\sigma, \eta) \end{cases} \)

贝尔曼方程如下

\( u_\alpha(x; \sigma, \eta) = l^{(\sigma+\eta)}(x) + K \mathbb{I}_{\hat{v}_\alpha(x; \sigma, \eta) > 0} + c \hat{v}_\alpha(x; \sigma, \eta) \)
\( + E[u_\alpha(x + \hat{v}_\alpha(x; \sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') | \sigma, \eta] \)

令

\( \breve{y}_2 = S_\alpha(\sigma, \eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \quad \hat{v}_2 = \hat{v}_\alpha(x; \sigma', \eta'). \)

在 \( \breve{y}_2, \hat{v}_2 \) 中，随机性来自需求和 \( \sigma', \eta' \)，而 \( \sigma, \eta \) 是已知的。由于 \( s_\alpha(\sigma, \eta) > -m_\alpha \)，我们可以写出

\( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma+\eta)D + K \)
\( + c S_\alpha(\sigma, \eta) + \alpha E[u_\alpha(\breve{y}_2; \sigma', \eta') | \sigma, \eta]. \)

另一方面

\( u_\alpha(\hat{y}_2; \sigma', \eta') = l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta']. \)

结合这两个关系并利用期望的运算法则，我们得到

(13.5.34) \( u_\alpha(-m_\alpha; \sigma, \eta) = (p+c)m_\alpha + p(\sigma + \eta)D + K + cE_\delta(\sigma, \eta) \)

\( + \alpha E\{l^{(\sigma' + \eta')}(\hat{y}_2) + K \mathbb{I}_{\hat{y}_2 > 0} + c\hat{v}_2 \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

另一方面，我们可以从贝尔曼方程写出以下两个不等式

\( u_\alpha(-m_\alpha; \sigma, \eta) \le p m_\alpha + p(\sigma + \eta)\tilde{D} \)

\( + \alpha E\left[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta\right] \)

\( u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') \le l^{(\sigma' + \eta')}(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + K + c(\hat{v}_2 + \hat{y}_2 + m_\alpha + D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma', \eta'], \)

因此，条件下

\( E[u_\alpha(-m_\alpha - D^{(\sigma + \eta + 1 - (\sigma' + \eta'))}, \sigma', \eta') | \sigma, \eta] \le K + p\tilde{D}(\sigma + \eta + 1) + (p+c)m_\alpha \)

\( + cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] + cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta] \)

汇总结果，我们得到不等式

(13.5.35) \( u_\alpha(-m_\alpha; \sigma, \eta) \le p(m_\alpha + (\sigma + \eta)D) + \alpha K \)

\( + \alpha p\tilde{D}(\sigma + \eta + 1) + \alpha(p+c)m_\alpha + \alpha cE[\hat{v}_2 + \hat{y}_2 | \sigma, \eta] \)

\( + \alpha cD(\sigma + \eta + 1 - E(\sigma' + \eta' | \sigma, \eta)) \)

\( + \alpha^2 E[u_\alpha(\hat{y}_2 + \hat{v}_2 - D^{(\sigma' + \eta' + 1 - (\sigma' + \eta'))}, \sigma'', \eta'') | \sigma, \eta]. \)

比较方程 (13.5.34) 和不等式 (13.5.35) 并消去项，我们得到

\( c(1-\alpha)S_\alpha(\sigma, \eta) + K(1-\alpha) + \alpha K E[\mathbb{I}_{\hat{y}_2 > 0} | \sigma, \eta] + c(1-\alpha)E[\hat{v}_2 | \sigma, \eta] \)

\( + \alpha h E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^+ + \alpha p E[S_\alpha(\sigma, \eta) - D^{(\sigma + \eta + 1)}]^- \)

\( \le (\alpha p - c(1-\alpha))m_\alpha + \alpha p\tilde{D}(\sigma + \eta + 1), \)

因此也有

\( (c(1-\alpha) + \alpha h)S_\alpha(\sigma, \eta) \le (\alpha p - c(1-\alpha))m_\alpha + \alpha(p+\tilde{h})\tilde{D}(\sigma + \eta + 1), \)

第二个不等式已证得。\(\square\)

我们可以推导出不依赖于 \(\alpha\) 的估计。由于 \(\alpha \to 1\)，我们可以假设 \(\alpha > \frac{1}{2}\)。我们陈述

## **推论 13.1.** 对于 $\alpha > \frac{1}{2}$，我们有

$|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0$

其中

$m_0 = \frac{\frac{2pK}{p-c} + (p+h)D(M+1)}{\min(c,h)}$

**证明.** 这是提议 13.9 的直接结果。

我们现在证明关于 \( u'_\alpha(x; \sigma, \eta) \) 的估计。

## **引理 13.3.** 我们将证明估计

(13.5.36) 
\(\sup_{\xi < x, \sigma, \eta} |u'_\alpha(x; \sigma, \eta)| \le \frac{C}{\bar{F}((x+m_0)^+)}.\)

**证明.** 我们回顾

\(\chi_\alpha(x; \sigma, \eta) = \mu_\alpha^{(\sigma+\eta)}(x) + \alpha E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta'), \forall x > s_\alpha(\sigma, \eta)
= 0, \quad \forall x \le s_\alpha(\sigma, \eta)\)

其中

\(\mu_\alpha^{(\sigma+\eta)}(x) = c(1-\alpha) + \alpha h - \alpha(h+p)\bar{F}(x),\)

并且

\(|s_\alpha(\sigma, \eta)|, |S_\alpha(\sigma, \eta)| \le m_0\)

我们使用

\(E X_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(x; \sigma', \eta')
= E[\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta') \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')}].\)

由于

\(\mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > s_\alpha(\sigma', \eta')} \le \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0},\)

我们推断

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le |\mu_\alpha^{(\sigma+\eta)}(x)|
+ \alpha E[|\chi_\alpha(x - D^{(\sigma+\eta+1-(\sigma'+\eta'))}, \sigma', \eta')| \mathbb{I}_{x - D^{(\sigma+\eta+1-(\sigma'+\eta'))} > -m_0}],\)

利用 \(|\mu_\alpha^{(\sigma+\eta)}(x)| \le \max(h,p)\) 并展开期望，我们得到

\(|\chi_\alpha(x; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}} \le \max(h,p) + \alpha |\chi_\alpha(x; \sigma+1, \eta)|_{\mathbb{I}_{x > -m_0}}
+ \alpha \sum_{k=\sigma+\eta}^M \gamma(k; \alpha, \eta)
+ \alpha \sum_{k=0}^{\sigma+\eta} E|\chi_\alpha(x - D^{(\sigma+\eta+1-k)}, 0, k)| \mathbb{I}_{x - D^{(\sigma+\eta+1-k)} > -m_0} \gamma(k; \sigma, \eta).\)

令

\(w_\alpha(x) = \sup_{\xi < x, \sigma, \eta} |\chi_\alpha(\xi; \sigma, \eta)|_{\mathbb{I}_{x > -m_0}}.\)

由前面的不等式得到

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}}\)
\(\le \max(h,p) + w_\alpha(x) \sum_{k=\sigma+\eta+1}^M \gamma(k;\sigma,\eta) + E w_\alpha(x-D) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta)\)
\(= \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D)) \sum_{k=0}^{\sigma+\eta} \gamma(k;\sigma,\eta),\)

并利用 \(w_\alpha(x) - E w_\alpha(x-D) \ge 0\)，\(\sum_{k=\sigma+\eta}^{\sigma+\eta} \gamma(k;\sigma,\eta) \ge \varpi_0\)，我们得到

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x) - (w_\alpha(x) - E w_\alpha(x-D))\varpi_0\)

令 \(x_0\) 固定。对于 \(x < x_0\)，我们也可以写出

\(|\chi_\alpha(x;\sigma,\eta)|_{\mathbb{I}_{x>-m_0}} \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

因此

\(w_\alpha(x_0) \le \max(h,p) + w_\alpha(x_0) - (w_\alpha(x_0) - E w_\alpha(x_0-D))\varpi_0,\)

这意味着

\(w_\alpha(x) - E w_\alpha(x-D) \le \frac{\max(h,p)}{\varpi_0}\)

\(w_\alpha(x) - E w_\alpha(x-D)_{\mathbb{I}_{x>D-m_0}} \le \frac{\max(h,p)}{\varpi_0}.\)

最后

\(w_\alpha(x) \le \frac{\max(h,p)}{\varpi_0} \frac{1}{\bar{F}((x+m_0)^+)}.\)

由此估计，结果立即得出。

定义

\(\Gamma_\alpha(\sigma,\eta) = u_\alpha(-m_0;\sigma,\eta).\)

由于 \(-m_0 < s_\alpha(\sigma,\eta)\)，我们可以写出

\(u_\alpha(-m_0;\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E u_\alpha^{(\sigma+\eta+1-(\sigma'+\eta'))}(s_\alpha(\sigma,\eta);\sigma',\eta'),\)

因此我们得到

\(\Gamma_\alpha(\sigma,\eta) = \alpha E \Gamma_\alpha(\sigma',\eta') + \Psi_\alpha(\sigma,\eta),\)

其中

\(\Psi_\alpha(\sigma,\eta) = (p+c)m_0 + pD(\sigma+\eta) + cs_\alpha(\sigma,\eta)\)
\(+\alpha E[u_\alpha(s_\alpha(\sigma,\eta) - D^{(\sigma+\eta+1-(\sigma'+\eta'))};\sigma',\eta') - u_\alpha(-m_0;\sigma,\eta)].\)

由提议 13.9 和引理 13.3 的估计可立即看出

\(|\Psi_\alpha(\sigma,\eta)| \le C, \forall \alpha, \sigma, \eta.\)

利用不变测度 \(\mu(\sigma,\eta)\)，我们定义

\(\rho_\alpha = \sum_{\sigma,\eta} \Psi_\alpha(\sigma,\eta)\mu(\sigma,\eta),\)



因此，来自遍历理论

(13.5.37)
\[
\left| \Gamma_\alpha(\sigma, \eta) - \frac{\rho_\alpha}{1-\alpha} \right|.
\]

我们可以陈述如下

### 定理 13.4.
我们采用定理 13.3 的假设。存在一个序列 \(\rho_\alpha\)，使得当 \(\alpha \to 1\) 时，对于一个子序列

(13.5.38)
\[
u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1-\alpha} \to u(x; \sigma, \eta),
\]

在 \(R\) 的任何紧集上一致收敛。我们还有 \(\rho_\alpha \to \rho\)。函数 \(u(x; \sigma, \eta)\) 是局部 Lipschitz 连续的，并满足

\[
|u'(x; \sigma, \eta)| \le \frac{C}{F((x+m_0)^+)}
\]

对 \(u(x; \sigma, \eta), \rho\) 满足

(13.5.39)
\[
u(x; \sigma, \eta) + \rho = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \sum_{k=0}^{\sigma+\eta} \gamma(k; \sigma, \eta) u^{(\sigma+\eta+1-k)}(y; 0, k) + \sum_{k=\sigma+\eta+1}^M \gamma(k; \sigma, \eta) u(y; \sigma+1, \eta) \right\}
\]

### 证明.
我们再次定义

\[
\bar{u}_\alpha(x; \sigma, \eta) = u_\alpha(x; \sigma, \eta) - \frac{\rho_\alpha}{1-\alpha},
\]

然后我们得到方程

\[
\bar{u}_\alpha(x; \sigma, \eta) + \rho_\alpha = -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E \bar{u}^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}
\]

由于下确界在 \(\max(x, S A_\alpha(\sigma, \eta))\) 处取得，我们可以认为若 \(x < X\) 则 \(y < L_X\)。因此我们还有

(13.5.40)
\[
\bar{u}_\alpha(x; \sigma, \eta) + \rho_\alpha = -cx + l^{(\sigma+\eta)}(x) + \inf_{L_X \ge y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E \bar{u}^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
\]

假设 \(|x| < X\)，利用提议 13.9 和引理 13.3 的估计，并应用 Ascoli-Arzelà 定理，我们可以提取一个子序列，使得

\[
\sup_{|x|<X} |\bar{u}_\alpha(x; \sigma, \eta) - u(x; \sigma, \eta)| \to 0
\]

并且我们可以对 (13.5.40) 取极限以得到

\[
\begin{aligned}
u(x; \sigma, \eta) + \rho &= -cx + l^{(\sigma+\eta)}(x) + \inf_{L_X \ge y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\} \\
&\ge -cx + l^{(\sigma+\eta)}(x) + \inf_{y \ge x} \left\{ K \mathbb{1}_{y > x} + cy + \alpha E u^{(\sigma+\eta+1-(\sigma'+\eta'))}(y; \sigma', \eta') \right\}.
\end{aligned}
\]

但相反的不等式可以轻易验证。结果随之得出。

考虑成本泛函

\[
J_{x, \alpha, \eta}^s(V) = E \sum_{t=1}^{\infty} \alpha^{t-1} (C(v_t) + l^{(\sigma_t + \eta_t)}(x_t)),
\]

那么我们将有

(13.5.41)
\[
\rho = \inf_V \lim_{\alpha \to 1} (1 - \alpha) J_{x, \alpha, \eta}^s(V)
\]

仅考虑极限存在的控制策略 \(V\)。然后下确界在由 \(s(\sigma, \eta)\)、\(S(\sigma, \eta)\) 策略表征的 \(V\) 处取得，其中

\[
s(\sigma, \eta) = \lim_{\alpha \to 1} s_\alpha(\sigma, \eta), \quad S(\sigma, \eta) = \lim_{\alpha \to 1} S_\alpha(\sigma, \eta)
\]

# 连续时间库存控制

## 14.1. 确定性模型

### 14.1.1. 连续时间冲动控制

我们描述一个连续时间模型。冲动控制是一系列时刻

\[
\theta_1 < \theta_2 < \cdots < \theta_n \cdots,
\]

在此时刻我们做出决策

\[
v_1 < v_2 < \cdots v_n \cdots .
\]

时刻 \(\theta_n\) 将是我们决定补充库存的时刻，而 \(v_n\) 将是补充水平。在这个确定性框架中，这些数字是确定性的。我们用 \(V\) 表示时刻和水平的序列，并称 \(V\) 为冲动控制。

设 \(y(t) = y_x(t; V)\) 为时刻 \(t\) 的库存状态，初始时刻 0 的初始状态为 \(x\)，并受冲动控制 \(V\) 约束。

我们有

\[
y(t) = x - \lambda t + M(t),
\]

其中

\[
M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n.
\]

这些关系的含义很明确：\(x > 0\) 是初始库存，\(\lambda t\) 是截至时刻 \(t\) 的需求，\(M(t)\) 表示截至时刻 \(t\) 的总补充量。由于不允许短缺，我们施加状态约束 \(y(t) \ge 0\)。我们定义成本函数如下

\[
J_x(V) = \sum_{n=0}^\infty (K + c v_n) \exp -a\theta_n + \int_0^\infty hy(t) \exp -\alpha t dt.
\]

像往常一样，我们通过以下方式定义值函数

\[
u(x) = \inf_V J_x(V).
\]

反馈是一种决策规则，它在任何时刻 \(t\) 定义作为该时刻系统状态函数的待采取决策。在我们的情况中，在任何时刻 \(t\)，查看库存值 \(y(t)\) 后，我们决定下订单并决定订购数量。

### 14.1.2. s, S 策略

s, S 策略是一对数字，满足

\[
s \le S,
\]

这样从这两个数字可以得到如下反馈：

\[
v(x) = v_{s,S}(x) = \begin{cases} S - x, & \text{if } x \le s \\ 0, & \text{if } x > s \end{cases}
\]

反馈用于按如下方式计算冲动控制 \(V = V_{s,S}\)：在任何时刻 \(t\)，如果 \(x(t) \le s\)，则订购数量

\[
v(t) = S - x(t).
\]

如果

\[
x(t) > s,
\]

则在时刻 \(t\) 不下订单。我们称

\[
u_{s,S}(x).
\]

与一对 \(s, S\) 相关的值函数。即

\[
u_{s,S}(x) = J_x(V_{s,S}).
\]

### 14.1.3. 不等式

很容易验证 \(u(x)\) 满足的不等式。回顾 \(x\) 表示初始时刻的状态（库存水平）。如果我们强制在初始时刻做出订购数量 \(v\) 的决策，那么我们支付 \(K + cv\)，状态变为 \(x + v\)。如果从现在开始最优进行，我们能达到的最佳结果是

\[
K + cv + u(x + v).
\]

因此我们可以断言

(14.1.1)
\[
u(x) \le K + \inf_{v>0} (cv + u(x + v)).
\]

下一个不等式在于检查初始时刻不订购的决策。因此我们将决策推迟一小段时间 \(\delta\)。在此期间，我们首先支付持有成本 \(\delta h x\)，然后在时刻 \(\delta\) 时库存为

\[
x - \delta \lambda.
\]

对于小 \(\delta\)，这个数为正。假设从现在开始我们表现最优。对于寿命期 \((\delta, \infty)\)，我们能获得的最佳结果是

\[
u(x - \delta \lambda).
\]

我们对该数量进行贴现以得到时刻 0 的值。由于 \(\delta\) 很小，我们有近似值

\[
(1 - \delta \alpha) u(x - \delta \lambda).
\]

因此我们声称

\[
u(x) \le (1 - \delta \alpha) u(x - \delta \lambda) + \delta h x
\]

在 \(\delta\) 中展开我们得到

(14.1.2)
\[
\alpha u + \lambda u' \le h x, \quad x > 0
\]

下一点是声称对于任何初始库存 \(x\)，(14.1.1) 或 (14.1.2) 中至少一个成立，因为要么我们决定订购，要么我们让系统自由演化一小段时间。我们可以通过写出互补松弛条件来表达这一点

(14.1.3)
\[
(\alpha u + \lambda u' - h x)(u(x) - K - \inf_{v>0} (cv + u(x + v))) = 0 \quad \forall x > 0
\]

我们必须通过对边界和光滑性的考虑来完善条件。边界是 \(x=0\)。我们显然必须在边界处订购，否则库存将保持在 0，因为它不能为负。最终我们订购，并可以认为问题从这时开始。因此，我们可以写

(14.1.4)
\[
u(0) = K + \inf_{v>0} (cv + u(v)).
\]

关于光滑性，如果

(14.1.5)
\[
u \in C^1(0, \infty).
\]

不等式集合和互补松弛方程 (14.1.1)、(14.1.2)、(14.1.3) 以及相关的边界和光滑性条件称为 *准变分不等式*。

### 注释 14.1.
值函数 \(u(x)\) 的定义并不保证光滑性。这是一种可取的性质，远非自动成立，特别是在切换点。

现在让我们写出由 \(s, S\) 策略定义的值函数所满足的条件。注意

\[
0 \le s \le S.
\]

我们首先有

(14.1.6)
\[
u_{s,S}(x) = K + c(S - x) + u_{s,S}(S), \quad \forall x \le s.
\]

接下来

(14.1.7)
\[
\alpha u_{s,S} + \lambda u'_{s,S} - hx = 0, \quad \forall x > s.
\]

这些关系表达了 \(s, S\) 策略下的决策过程。

与定义值函数 \(u\) 的关系相比，这暗示了一种从 \(s\) 得到 \(S\) 的自然方法。让我们首先选择一个单一的正数 \(s\)，并通过以下方式定义 \(u_s(x)\)

(14.1.8)
\[
u_s(x) + cx = K + \inf_{y>s} (cy + u_y(y)), \quad x \le s
\]

(14.1.9)
\[
\alpha u_s + \lambda u'_s - hx = 0, \quad \forall x > s.
\]

那么 \(S(s)\) 简单地通过以下方式得到

(14.1.10)
\[
\inf_{y>s} (cy + u_y(y)) = cS + u_s(S)
\]

### 14.1.4. \(u_s\) 的定义

对于任何固定的 \(s\)，我们可以将微分方程 (14.1.9) 的解写成如下形式

\[
u_s(x) = u_s(s) \exp -\frac{\alpha}{\lambda}(x-s) + \frac{h}{\lambda} \int_s^x y \exp -\frac{\alpha}{\lambda}(x-y) dy,
\]

因此

(14.1.11)
\[
u_s(x) = \frac{h}{\alpha} \left( x - \frac{\lambda}{\alpha} \right) + \left( u_s(s) - \frac{h}{\alpha} s + \frac{\lambda h}{\alpha^2} \right) \exp -\frac{\alpha}{\lambda}(x-s).
\]

为了定义 \(S = S(s)\)，我们写

\[
u'_s(S) = -c,
\]

因此

\[
\alpha u_s(S) = hS + \lambda c.
\]





我们可以为 $S$ 写出以下方程

$$ \exp^{-\frac{\alpha}{\lambda}(S-s)} = \frac{1 + \frac{\alpha c}{h}}{1 + (\frac{\alpha}{h}(\frac{cK}{u_s(s)} + s) - S)}. $$

为了定义 $u_s(s)$ 的值，我们使用方程 (14.1.8) 和 (14.1.10) 得到

$$ u_s(s) = K + c(S - s) + \frac{hS + \lambda c}{\alpha}. $$

我们推导出右导数

$$ u'_{s+0}(s) = -c - \frac{\alpha K + (\alpha c + h)(S - s)}{\lambda}. $$

因为

$$ u'_{s-0}(s) = -c. $$

在点 s 处无法使导数匹配，而这是我们要求 $u_s(x)$ 与值函数 $u(x)$ 重合所必需的。

避免这一困难的唯一方法是取 s = 0，因为在边界上不存在匹配。然后考虑 $u_0(x)$。$S = S(0)$ 的值通过求解方程得到

(14.1.12)

$$ (1 + \frac{\alpha c}{h}) \exp^{\frac{\alpha}{\lambda}S} S - (\frac{\alpha}{\lambda} + \frac{\alpha^2 c}{\lambda h}) - 1 - \frac{\alpha c}{h} - \frac{\alpha^2 K}{\lambda h} = 0. $$

可以轻松验证该方程有一个唯一的正解 S。

现在的重要问题是检查 $u_0(x)$ 是否为值函数 $u(x)$。我们必须验证它是否满足 u 的条件，即关系 (14.1.1)、(14.1.2)、(14.1.3)。唯一非平凡的验证是 (14.1.1)，我们将其重写为

(14.1.13)

$$ u_0(x) + cx \le K + \inf_{y > x} (u_0(y) + cy). $$

因为

$$ u_0(x) = \frac{h}{\alpha}x - \frac{\lambda h}{\alpha} + (u_0(0) + \frac{\lambda h}{\alpha}) \exp^{-\frac{\alpha c}{\lambda}x}, $$

我们很容易看出它是一个凸函数。因此 $u_0(x) + cx$ 也是凸的。其最小值在 S 处。因此对于 $x \ge S$ 它是递增的。故对于 $x \ge S$ 我们有

$$ \inf_{y > x} (u_0(y) + cy) = u_0(x) + cx, $$

属性 (14.1.13) 平凡地得到验证。

对于 x < S 我们可以写出

$$ u_0(x) + cx \le u_0(0). $$

同样

$$ \inf_{y > x} (u_0(y) + cy) = u_0(S) + cS. $$

注意到

$$ u_0(0) = K + u_0(S) + cS, $$

属性 (14.1.13) 再次得到。

## 14.2. 遍历问题

遍历问题在于让折扣率趋于 0。我们对所有感兴趣的量都指明其对 \(\alpha\) 的依赖性。特别是，用 \(u_\alpha(x)\) 表示值函数，回顾有

\(u_\alpha(x) = u_{\alpha 0}(x)\)。

我们省略不再必要的索引 0。通过直接检查

\(u_\alpha(x) \to \infty, \text{ as } \alpha \to 0\)

### 14.2.1. 恢复 EOQ 公式。

**练习 14.1.** 证明

\(S_\alpha \to \hat{S} = \sqrt{\frac{2K\lambda}{h}} = \hat{q}\)

当 \(\alpha \to 0\) 时，其中 \(\hat{q}\) 被称为 EOQ 公式，参见第 2 章，2.2 节。

我们推导出

\(\alpha u_\alpha(0) \to h\hat{S} + \lambda c\),

这是由 EOQ 公式推导出的最优平均成本。同样

\(\alpha u_\alpha(x) \to h\hat{S} + \lambda c\),

我们看到初始库存不起任何作用。

接下来设

\(\bar{u}_\alpha(x) = u_\alpha(x) - u_\alpha(0)\)。

它满足微分方程

\(\alpha u_\alpha(0) + \alpha \bar{u}_\alpha(x) + \lambda \bar{u}'_\alpha(x) = hx\),

具有初始条件

\(\bar{u}_\alpha(0) = 0\)。

我们知道

\(\alpha u_\alpha(0) \to h\hat{S} + \lambda c = \beta\),

因此我们可以推测

\(\bar{u}_\alpha(x) \to u(x)\),

其中 \(u\) 满足

\(\beta + \lambda u' = hx, u(0) = 0\),

即

\(u(x) = -\frac{\beta x}{\lambda} + \frac{x^2 h}{2\lambda}\)

**练习 14.2.** 直接验证上述极限性质。

### 14.2.2. 极限等价。

练习 14.3. 考虑一个 0, q 策略并设 \( q = \lambda T \)。

我们从初始库存 0 开始，因此立即下单。库存定义为

\( y(t) = q - \lambda(t - nT), \forall t \in [nT, (n+1)T]. \)

考虑平均成本

\( C(q) + c\lambda = \frac{hq}{2} + \frac{K\lambda}{q} + c\lambda. \)

定义折扣成本

\( J_\alpha(q) = h \int_0^\infty y(t) \exp -\alpha t dt + \sum_{n=0}^\infty (K + cq) \exp -n\alpha T. \)

练习 14.4. 证明

\( \alpha J_\alpha(q) \to C(q) + c\lambda, \)

当 \( \alpha \to 0 \) 时

练习 14.5. 计算使 \( J_\alpha(q) \) 最小的量 \( \hat{q}_\alpha \)。证明它与通过求解方程 (14.1.12) 得到的相同。

## 14.3. 连续速率交付

### 14.3.1. 变换后的 EOQ 公式。

假设现在没有即时交付。相反，交付以连续速率 \( r \) 提供。由于没有短缺的可能性，我们必须有 \( r \ge \lambda \)。我们回顾 EOQ 公式必须更改（参见 14.3.1）为

\( \hat{q} = \sqrt{\frac{2K\lambda}{h(r-\lambda)}}. \)

当 \( r = \lambda \) 时，该公式趋于 \( \infty \)。必须将其理解为：将在需求水平进行连续交付。库存保持为 0，单位时间成本等于 \( c\lambda \)。在这种情况下没有优化。

### 14.3.2. 变换后的不等式。

我们可以尝试推导控制连续交付问题的值函数的不等式。我们决定在交付处理期间不下单。值函数 \( u(x) \) 被考虑为具有初始库存 \( r \) 且没有正在进行的交付。不等式 (14.1.2) 保持不变。然而，不等式 (14.1.1) 必须更改以表达以下事实：当我们订购数量 \( q \) 时，我们必须等待直到交付完成，即直到 \( \frac{q}{r} \)。我们必须在此期间覆盖持有成本，当交付完成后，可用库存为

\( x + q - \frac{\lambda}{r}q. \)

因此我们必须写出

(14.3.1) \( u(x) \le K + \inf_{q \ge 0} \left[ cq + h \int_0^{\frac{q}{r}} (x + (r - \lambda)t) \exp -\alpha t dt + \exp -\alpha \frac{q}{r} u \left( x + q - \frac{\lambda}{r}q \right) \right] \)

进行计算我们得到

(14.3.2) \( u(x) \leq K + \inf_{q \geq 0} \left[ cq + \frac{h}{\alpha} \left( x \left( 1 - \exp -\alpha \frac{q}{r} \right) + \frac{r - \lambda}{\alpha} \right. \right. \\
\left. \left. \cdot \left( 1 - \exp -\alpha \frac{q}{r} - \alpha \frac{q}{r} \exp -\alpha \frac{q}{r} \right) \right) + \exp -\alpha \frac{q}{r} u \left( x + q - \frac{\lambda}{r}q \right) \right] \).

我们如同在 EOQ 情况中一样进行，考虑 \( s = 0 \) 且方程对 \( x > 0 \) 成立，并使用边界条件

(14.3.3) \( u(0) = K + \inf_{q \geq 0} \left[ cq + \frac{h(r - \lambda)}{\alpha^2} \left( 1 - \exp -\alpha \frac{q}{r} - \alpha \frac{q}{r} \exp -\alpha \frac{q}{r} \right) \right. \\
\left. + \exp -\alpha \frac{q}{r} u(q - \frac{\lambda}{r} q) \right] \).

**练习 14.6.** 我们通过对右侧求导并将其等于 0 来计算最优 \(\hat{S} = \hat{q}\)。我们得到

(14.3.4) \( c + \frac{r - \lambda}{r} \exp -\alpha \frac{S}{r} \frac{S}{r} \left( S + u' \left( S \frac{r - \lambda}{r} \right) \right) - \frac{\alpha}{r} \exp -\alpha \frac{S}{r} u \left( S \frac{r - \lambda}{r} \right) = 0 \).

**练习 14.7.** 证明 \(\hat{S}\) 是下式的解

(14.3.5) \( \left( \exp -\alpha \frac{S}{r} + \frac{\alpha c}{h} \right) \left( \exp \frac{\alpha}{\lambda} S - 1 \right) - \frac{r}{\lambda} \left( 1 - \exp -\frac{S\alpha}{r} \right) - S \frac{\alpha^2 c}{\lambda h} - \frac{\alpha^2 K}{\lambda h} = 0 \).

**练习 14.8.** 检查方程 (14.3.5) 当 \( r \to \infty \) 时归约为 (14.1.12)，当 \( \alpha \to 0 \) 时归约为第 14.3.1 节的变换后的 EOQ 公式。

## 14.4. 前置时间

### 14.4.1. 不允许短缺。

我们现在考虑一种带有折扣率的情况。我们补充第 2.6.1 节。如果我们实施一个 \( s, q \) 策略且 \( s = \lambda L \)，则最优 \( q \) 将不同于 EOQ 公式。确实，我们回顾 \( s = \lambda L \) 时 \( u_s(x) \) 的微分函数，为了简化记法我们将其写作 \( u(x) \)，尽管它不是值函数。我们有

\( u(x) = \frac{h}{\alpha} \left( x - \frac{\lambda}{\alpha} \right) + \left( u(\lambda L) - \frac{L \lambda h}{\alpha} + \frac{\lambda h}{\alpha^2} \right) \exp -\frac{\alpha}{\lambda} (x - L \lambda) \).

那么我们必须写出

\( u'(q) = -c \exp \alpha L \).

其中我们期望 \(\hat{q} > \lambda L\)。然后我们可以应用方程得到

\( u(q) \exp -\alpha L = \frac{\lambda c + h \hat{q} \exp -\alpha L}{\alpha} \).

我们推导出

\( u(\lambda L) = K + c\hat{q} + \frac{L \lambda h}{\alpha} - \frac{\lambda h}{\alpha} + \frac{h \lambda}{\alpha} \exp -\alpha L + \frac{\lambda c + h \hat{q} \exp -\alpha L}{\alpha} \).

汇总结果，我们得到 \(\hat{q}\) 是方程的解

(14.4.1) \( \left( \exp -\alpha L + \frac{\alpha c}{h} \right) \frac{\exp \alpha \hat{q}}{\lambda} \frac{\alpha}{q} \hat{q} \left( \exp -\alpha L + \frac{\alpha c}{h} \right) - \exp -\alpha L - \frac{\alpha c}{h} - \frac{\alpha^2 K}{\lambda h} = 0 \).

**练习 14.9.** 检查当 \(\alpha\) 较小时，方程 (14.4.1) 的解趋于 EOQ 公式，与 \( L \) 无关，前提是它大于 \(\lambda L\)。





## 14.5. 新闻商问题

我们在此考虑一个周期 T。周期开始时，库存为 S，即采购量。周期内的总需求量为 D，假设其服从概率密度函数 f(x)。该需求在周期内以均匀速率 \(\frac{D}{T}\) 实现。因此，时刻 t 的库存为

\(S - \frac{D}{T}t.\)

该随机变量可以为正或负。当其为正时，产生持有成本；当其为负时，产生短缺成本。

平均库存盈余为

\(I_+(S) = E[\frac{\int_0^T (S - D\frac{t}{T})^+ dt}{T}] = E\left[ \mathbb{I}_{S>D}(S - \frac{D}{2}) + \mathbb{I}_{S \le D} \frac{S^2}{2D} \right]\)
\(= SF(S) - \frac{1}{2} \int_0^S x f(x) dx + \frac{S^2}{2} \int_S^{+\infty} \frac{f(x)}{x} dx.\)

对于短缺库存，我们有

\(I_-(S) = E[\frac{\int_0^T (S - D\frac{t}{T})^- dt}{T}] = E[\frac{((S - D)^-)^2}{2D}],\)

即

\(I_-(S) = I_+(S) - S + \frac{1}{2} \int_0^{+\infty} x f(x) dx.\)

令 h 为单位时间的持有成本，p 为单位时间的短缺成本，则总成本为

\(C(S) = hI_+(S) + pI_-(S),\)

或

\(C(S) = (h+p) \left[ SF(S) - \frac{1}{2} \int_0^S x f(x) dx + \frac{S^2}{2} \int_S^{+\infty} \frac{f(x)}{x} dx \right]\)
\(+ p \left( -S + \frac{1}{2} \int_0^{+\infty} x f(x) dx \right).\)

我们可以进而计算最优 \(S = \hat{S}\)。我们有

\(C'(S) = (h+p) \left( F(S) + S \int_S^{+\infty} \frac{f(x)}{x} dx \right) - p,\)

且

\(C''(S) = (h+p) \int_S^{+\infty} \frac{f(x)}{x} dx > 0.\)

因此唯一的 \(\hat{S}\) 由以下给出

\(F(\hat{S}) + \hat{S} \int_{\hat{S}}^{+\infty} \frac{f(x)}{x} dx = \frac{p}{h+p}\)

### 注释 14.2. 通常新闻商问题的解给出为

\(F(\hat{S}) = \frac{p}{h+p}.\)

这是因为假设需求一次性实现。

## 14.6. 泊松需求

### 14.6.1. 泊松过程。与其通过随机速率 \(\lambda\) 来建模需求的随机性，不如将需求 \(D(t)\) 视为一个马可夫过程。在确定性情况下，它仅为 \(\lambda t\)。最自然的随机过程是参数为 \(\lambda\) 的泊松过程。我们回顾泊松过程的定义。我们有

\(D(0) = 0; D(t_2) - D(t_1) \text{ and } D(s_2) - D(s_1) \text{ are independent } \forall s_1 \le s_2 \le t_1 \le t_2\)

\(D(t_2) - D(t_1) \text{ is integer valued; } P(D(t_2) - D(t_1) = k) = \exp(-\lambda(t_2 - t_1)) \frac{(\lambda(t_2 - t_1))^k}{k!}\)

以下公式表达了马可夫性质

\(P(D(t + \epsilon) = D(t)|D(s), s \le t) \sim 1 - \lambda \epsilon \quad P(D(t + \epsilon) = D(t) + 1|D(s), s \le t) \sim \lambda \epsilon\)

泊松过程模拟了排队中客户的到达，平均到达率为 \(\lambda\)。请注意

\(ED(t) = \lambda t.\)

这一最后属性解释了为什么泊松过程是具有恒定需求速率 \(\lambda\) 的确定性模型的自然扩展。

马可夫过程 \(D(t)\) 的无穷小生成元是实变量 \(x\) 上光滑函数上的线性算子，定义为

\(A\phi(x) = \lim_{\epsilon \to 0} \frac{\phi(x + D(\epsilon)) - \phi(x)}{\epsilon} = \lambda(\phi(x + 1) - \phi(x))\)

### 14.6.2. 模型描述。冲动控制是一个序列

\(\theta_n, v_n,\)

其中 \(\theta_n\) 是相对于滤流的停止时间

\(\mathcal{F}^t = \sigma(D(s), s \le t),\)

且 \(v_n\) 是 \(\mathcal{F}^{\theta_n}\) 可测的随机变量。令 \(V\) 为一个冲动控制，相应的库存由以下公式描述

\(y_x(t; V) = x - D(t) + M(t; V),\)

其中

\(M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n\)

请注意库存可能变为负值。令

\(f(x) = hx^+ + px^-,\)

待最小化的成本函数由以下给出

\(J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp(-\alpha \theta_n) \right.\)

\(\left. + \int_0^\infty f(y(t)) \exp(-\alpha t) \, dt \right]\)

### 14.6.3. 值函数的不等式。

考虑值函数
\( u(x) = \inf_V J_V(V). \)

我们可以为函数 \( u(x) \) 推导不等式和互补松弛条件，该条件将再次被称为 *准变分不等式*。我们首先有

(14.6.1) \( u(x) \le K \inf_{v>0} (cv + u(x+v)), \)

然后

(14.6.2) \( -\lambda(u(x-1) - u(x)) + \alpha u(x) \le f(x). \)

互补松弛条件表示

(14.6.3) \( [((\alpha + \lambda)u(x) - \lambda u(x-1)) - f(x)](u(x) - K \inf_{v>0} (cv + u(x+v))) = 0. \)

### 14.6.4. 对应于 \( s, S \) 策略的值函数。

注意 \( x \in R \)。没有显式边界条件。然而 \( u(x) \) 的增长不应快于 \( f(x) \)（即线性增长）。以类似于确定性情况中讨论的方式，对应于 \( s, S \) 策略的值函数定义如下。我们写

(14.6.4) \( u_s(x) + cx = u_s(s) + cs = K + \inf_{\eta > s} (c\eta + u(\eta)) = K + cS + u(S), \forall x \le s \)

(14.6.5) \( (\alpha + \lambda)u(x) - \lambda u(x-1) - f(x) = 0, \forall x \ge s \)

### 定理 14.1. 假设

\( p > \alpha c. \)

存在唯一的一对 \( s, S \) 和一个具有线性增长的唯一连续函数 \( u_s(x) \)，使得方程 (14.6.4)、(14.6.5) 得到满足。

### 证明。注意到

\( u_s(s-1) + c(s-1) = u_s(s) + cs, \)

且

\( (\alpha + \lambda)u_s(s) - \lambda u_s(s-1) = f(s), \)

我们得到

\( u_s(x) + cx = cs + \frac{f(s) + \lambda c}{\alpha}, \forall x \le s. \)

定义

\( H_s(x) = u_s(x) + cx - cs - \frac{f(s) + \lambda c}{\alpha} \)

我们得到关于 \( H_s(x) \) 的以下关系

(14.6.6) \( (\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = g(x) - g(s), \forall x \ge s; H_s(x) = 0, \forall x \le s, \)

其中我们设定

\( g(x) = f(x) + \alpha cx. \)

我们有

\( g(x) - g(s) = \begin{cases} -(p - \alpha c)(x - s), & \forall x < 0 \\ (h + \alpha c)x + (p - \alpha c)s, & \forall x \ge 0 \end{cases} \)

当 \( s < 0 \) 时，特别是，得益于该假设，我们看到

\( g(x) - g(s) \le 0, \forall s < x < 0. \)

事实上，注意到存在唯一的 \( \nu > 0 \) 使得 \( g(\nu) = g(s) \)。我们有

\( s < x < \nu \Rightarrow g(x) - g(s) < 0. \)

定义

\( g_s(x) = (g(x) - g(s)) \mathbf{1}_{x > s}. \)

我们得到

(14.6.7) \( H_s(x) = \sum_{j=0}^{\lfloor x-s \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}}, \forall x \ge s; H_s(x) = 0, \forall x \le s, \)

其中 \( \lfloor x \rfloor \) 是 x 的整数部分，即唯一满足以下条件的整数

\( \lfloor x \rfloor \le x < \lfloor x \rfloor + 1. \)

得益于 \( g_s(s) = 0 \) 这一事实，我们可以验证 \( H_s(x) \) 是一个连续函数。量 \( S = S(s) \) 由以下给出

\( H_s(S) = \inf_{\eta > s} H_s(\eta). \)

回顾 \( f(x) \) 的定义，我们立即得到

\( S(s) = s, \forall s \ge 0 \)

接下来考虑 \( s < 0 \) 的情况。从公式 (14.6.7) 可以立即得出

\( s < x < \nu \Rightarrow H_s(x) < 0. \)

接下来对于 \( x > \nu \) 我们可以写成

\( H_s(x) = \sum_{j=0}^{\lfloor x-\nu \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}} + \sum_{j=\lfloor x-\nu \rfloor+1}^{\lfloor x-s \rfloor} \frac{g_s(x-j)\lambda^j}{(\alpha+\lambda)^{j+1}}. \)

第一个求和由正项组成，第二个由负项组成。我们很容易推导出以下估计

\( H_s(x) \ge \frac{g_s(x)}{\alpha+\lambda} + \frac{g_s(0)}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{\lfloor x-s \rfloor}, \)

由此可得

\( H_s(x) \to +\infty \text{ as } x \to +\infty. \)

回顾 \( H_s(x) \) 的连续性，可知其在 \( (s, \infty) \) 上达到最小值。选取最小的最小值 \( S(s) \)，我们为 \( s < 0 \) 定义函数 \( S(s) \)。必然有

\( S(s) \ge 0, \)

因为 \( H_s(x) \) 在 \( s < x < 0 \) 上递减。这可通过直接检查公式 (14.6.7) 得到。

剩下的就是找到 \( s \)。它必须满足关于 \( s \) 的方程

\( \inf_{\eta > s} H_s(\eta) = -K. \)

我们有

\( \inf_{\eta > s} H_s(\eta) = 0, \forall s \ge 0. \)





因此我们可以假设 $s < 0$。考虑 $s < x_0 < 0$。我们可以断言

$$
H_s(x_0) \le \frac{g_s(x_0)}{\alpha + \lambda}.
$$

因此

$$
\inf_{\eta > s} H_s(\eta) \le H_s(x_0) \le \frac{g_s(x_0)}{\alpha + \lambda}.
$$

令 $s$ 趋向于 $-\infty$，我们得到

$$
\inf_{\eta > s} H_s(\eta) \to -\infty, \text{ as } s \to -\infty.
$$

最后我们证明 $\inf_{\eta > s} H_s(\eta)$ 是 $s$ 在 $(-\infty, 0)$ 上的增函数。这将证明存在且仅存在一个 $s$ 的值，使得该函数等于 $-K$。考虑 $s' < s < 0$。我们将证明

$$
H_{s'}(x) < H_s(x), \forall s' < s < x.
$$

这将蕴含所需的结果。我们注意到

$$
g_{s'}(x) < g_s(x), \forall x.
$$

写成

$$
H_{s'}(x) - H_s(x) = \sum_{j=0}^{[x-s]} \frac{(g_{s'}(x-j) - g_s(x-j))\lambda^j}{(\alpha + \lambda)^{j+1}} + \sum_{j=[x-s]+1}^{[x-s']} \frac{g_s(x-j)\lambda^j}{(\alpha + \lambda)^{j+1}}.
$$

根据刚才提到的性质，第一项为负。在第二项中我们注意到

$$
[x - s] + 1 \le j \le [x - s'] \Rightarrow s' \le s' + x - j < s < 0,
$$

且第二项也为负。该性质已证得，$s$ 被唯一确定。

## 14.6.5. s, S 策略的最优性。

我们现在转向证明，上面用选定的 $s$ 定义的函数 $u_s(x)$ 确实是最优策略，即 $u_s(x) = u(x)$。

### 定理 14.2。

我们假设 $ca - p < 0$。那么，s, S 策略是最优的。

### 证明。

我们需要验证不等式，互补松弛条件平凡满足。

$$
(\alpha + \lambda)u(x) - \lambda u(x - 1) \le f(x), \forall x \le s,
$$

相当于 $g(x) - g(s) \ge 0, \forall x \le s$。由于 $s < 0$，该性质满足。第二个不等式归约为

$$
H_s(x) \le K + \inf_{\eta > x} H_s(\eta), \forall x \ge s
$$

由于 $K = -\inf_{\eta > s} H_s(\eta)$，右边肯定为正。因此，每当 $H_s(x) \le 0$ 时，不等式显而易见。这在 $s < x < \nu$ 时尤其成立。函数 $H_s(x)$ 在 $\nu$ 之后可以为负，并且存在第一个点 $x_0$，使得 $\nu < x_0$ 且 $H_s(x_0) = 0$。因此，只需对 $x \ge x_0$ 证明该不等式。我们还注意到

$$
g_s(x_0) = -\lambda H_s(x_0 - 1) \ge 0.
$$

令 \(\xi \ge 0\)。我们将考虑 \(x > x_0 - \xi\)。由于 \(\xi\) 是任意的，我们可以有 \(x < s\)。我们可以以对任何 \(x\) 都有效的方式写出 \(H_s(x)\) 的方程，如下（回顾 \(g_s(x)\) 的定义。

$$
(\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = g_s(x).
$$

接下来我们可以写出以下不等式

$$
(\alpha + \lambda)H_s(x) - \lambda H_s(x-1) \mathbb{1}_{-1 \le x_0 - \xi} \le g_s(x), \quad H_s(x_0 - \xi) \le 0.
$$

截断的原因是为了能够在域 \(x \ge x_0 - \xi$ 上工作。需要付出的代价是我们只能写出一个不等式。请注意，确实

$$
H_s(x-1)\mathbb{1}_{x-1 < x_0 - \xi} \le 0,
$$

由 \(x_0$ 的定义可知。接下来定义

$$
M_s(x) = H_s(x + \xi) + K \ge 0.
$$

我们可以写出

$$
(\alpha + \lambda)M_s(x) - \lambda M_s(x-1) \mathbb{1}_{x-1 \ge x_0 - \xi} \le g_s(x + \xi) + \alpha K, \quad M_s(x_0 - \xi) = K.
$$

我们声称

$$
g_s(x + \xi) \ge g_s(x).
$$

请注意

$$
g_s(x + \xi) \ge g_s(x_0) > 0.
$$

因此，如果 \(x < s$，该主张显而易见。如果 \(x > s$，则我们需要证明 \(g(s + \xi) \ge g(x)$。

如果 \(x > 0$，这由凸性得出。如果 \(s < x < 0\)，则

$$
g(x + \xi) - g(x) \ge g(x_0) - g(s) > 0.
$$

因此，令

$$
Y_s(x) = H_s(x) - M_s(x),
$$

我们推断出 \(Y_s(x) \le 0$。该结果对 \(x > x_0 - \xi$ 有效，因此也对 \(x > x_0$ 有效。

定理 14.2 的证明已完成。\(\square\)

## 14.6.6. 导数的计算。

我们将计算导数 \(H'_s(x + 0)$ 和 \(H'_s(x - 0)$。对于 \(x \ge s$，我们有

$$
H'_s(x + 0) = \sum_{j=0}^{[x-s]} \frac{g'_s(x - j + 0)\lambda^j}{(\alpha + \lambda)^{j+1}}.
$$

我们也可以通过公式计算 \(H'_s(x - 0)$

$$
H'_s(x - 0) = \begin{cases} \sum_{j=0}^{[x-s]} \frac{g'_s(x - j - 0)\lambda^j}{(\alpha + \lambda)^{j+1}}, & \text{if } [x-s] < x - s \\ \sum_{j=0}^{[x-s]-1} \frac{g'_s(x - j - 0)\lambda^j}{(\alpha + \lambda)^{j+1}}, & \text{if } [x-s] = x - s \end{cases}
$$

其中 \(H'_s(s - 0) = 0$。

由此可知，对于 \(x < 0$

(14.6.8)
$$
H'_s(x + 0) = -\frac{p - \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{[x-s]+1} \right),
$$

(14.6.9)
$$
H'_s(x-0) = \begin{cases} H'_s(x+0), & \text{if } [x-s] < x-s \\ -\frac{p-\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{x-s} \right), & \text{if } [x-s] = x-s \end{cases}
$$

由此可知，对于 \(x < 0$，\(H'_s(x)$ 仅在 \(x - s$ 为负整数的点 \(x$ 处不连续。不连续点为

$$
H'_s(x+0) - H'_s(x-0) = -\frac{p-\alpha c}{\lambda+\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{x-s}.
$$

如果 \(s = [s]$，则不连续点为负整数 \(-n$，其中 \(1 \le n \le -s$。我们有

$$
H'_s(-n+0) = -\frac{p-\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{-n-s+1} \right),
$$

$$
H'_s(-n-0) = -\frac{p-\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{-n-s} \right),
$$

且对于 \(-n < x < -n + 1$

$$
H'_s(x) = H'_s(-n+0).
$$

因此，对于 \(s$ 为负整数、\(x < 0$，\(H'_s(x)$ 是分段常数、负且递减的，不连续点位于 \(x = -n$，其中 \(0 \le n \le -s$。

接下来假设 \([s] < s$，注意 \([s] + 1 = -[-s]$。我们考虑区间

$$
(s, s+1), (s+1, s+2), \dots, (s+[-s], 0).
$$

一个区间的形式为 \((s+n-1, s+n)$，其中 \(n$ 从 \(1$ 运行到 \([-s]+1$。对于最后一个区间，末端 \(s+[-s]+1$ 被替换为 \(0$。我们有

$$
s + n - 1 < x < s + n \Rightarrow [x-s] = n - 1,
$$

且

$$
H'_s(x) = H'_s(s+n-1+0) = -\frac{p-\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^n \right).
$$

我们得到，对于 \([s] < s < 0$，\(H'_s(x)$ 是分段常数、负且递减的，不连续点位于 \(s+n-1$，其中 \(n$ 从 \(1$ 到 \([-s]+1$。

现在考虑 \(x \ge 0\)，故 \([x] \ge 0$。我们有 \([x-s] \ge [x]$。我们容易计算得出

(14.6.10)
$$
H'_s(x+0) = \frac{h+\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]+1} \right) - \frac{p-\alpha c}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]+1} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]-[x]} \right).
$$

对于 \(H'_s(x-0)$，情况更复杂。有 4 种情况，取决于 \(x$ 和 \(x-s$ 是否为整数。如果 \([x-s] < x-s$ 且 \([x] < x$，则

(14.6.11)
$$
H'_s(x-0) = H'_s(x+0).
$$

如果 $[x-s] < x-s$ 且 $[x] = x$（这意味着 $[x-s] = x + [-s]$），则

(14.6.12)
$$
H'_s(x-0) = \frac{h+\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^x \right) - \frac{p-\alpha c}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^x \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{[-s]+1} \right).
$$

与 (14.6.10) 比较，我们观察到一个不连续点

(14.6.13)
$$
H'_s(x+0) - H'_s(x-0) = \frac{1}{\lambda+\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^x (h+p).
$$

如果 $[x-s] = x-s$，则 $[x] = x-s+[s]$。请注意，在这种情况下，$x = [x]$ 仅当 $s = [s]$ 时成立。如果 $[s] < s$，我们得到

(14.6.14)
$$
H'_s(x-0) = \frac{h+\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]+1} \right) - \frac{p-\alpha c}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]+1} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{[-s]} \right).
$$

且如果 $[s] = s$，我们得到

(14.6.15)
$$
H'_s(x-0) = \frac{h+\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^x \right) - \frac{p-\alpha c}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^x \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{-s} \right).
$$

我们再次得到一个不连续点：当 $[x-s] = x-s$ 且 $[s] < s$ 时

$$
H'_s(x+0) - H'_s(x-0) = - \frac{p-\alpha c}{\lambda+\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^{[x]-[s]}.
$$

当 $[x] = x$ 且 $[s] = s$ 时，我们得到

$$
H'_s(x+0) - H'_s(x-0) = \frac{1}{\lambda+\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^x \left[ h+\alpha c + (p-\alpha c) \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{-s} \right) \right].
$$

我们从 $s = [s]$ 的情况开始，其中 $s$ 是整数。我们有 $[x-s] = [x]-s$。唯一可能的不连续点是正整数。因此我们考虑区间 $(0, 1), \cdots (n-1, n), \cdots$ 。

如果 $n-1 < x < n$，则 $[x-s] = n-1-s < x-s$，

因此

$$
H'_s(x) = H'_s(n-1+0) = \frac{h+\alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^n \right) - \frac{p-\alpha c}{\alpha} \left( \frac{\lambda}{\lambda+\alpha} \right)^n \left( 1 - \left( \frac{\lambda}{\lambda+\alpha} \right)^{-s} \right).
$$

因此，对于 $x \ge 0$ 和 $s$ 为负整数，函数 $H'_s(x)$ 是分段常数的，在 $x$ 为正整数的值处有不连续点。函数 $H'_s(x)$ 是递增的。





考虑现在 $x \ge 0$ 且 $[s] < s$。考虑 $n - 1 < x < n$，则 $[x] = n - 1$ 且

$$H'_s(n-1+0) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^n \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^n \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]} \right),$$

$$H'_s(n-1-0) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{n-1} \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n-1} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]+1} \right).$$

那么对于 $n - 1 < x < n + [-s] + s$ 我们有

$[x - s] = n - 1 + [-s], \quad H'_s(x) = H'_s(n - 1 + 0),$

并且对于 $n + [-s] + s < x < n$ 我们有

$[x - s] = n + [-s], \quad [x - s] - [x] = [-s] + 1$

并且

$$H'_s(x) = \frac{h + \alpha c}{\alpha} \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^n \right) - \frac{p - \alpha c}{\alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^n \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]+1} \right) = H'_s(n - 0).$$

我们在 $n + [-s] + s$ 处有一个不连续点，由以下给出

$$H'_s(n + [-s] + s + 0) - H'_s(n + [-s] + s - 0) = H'_s(n - 0) - H'_s(n - 1 + 0) = - \frac{p - \alpha c}{\alpha + \lambda} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n - [s]}. $$

所以对于 $x \ge 0, [s] < s$，$H'_s(x)$ 在 $x = n$ 和 $x = n + [-s] + s$ ($n > 0$) 处有不连续点。它是分段常数的，但不是递增的。它在 $n$ 处增加，在 $n + [-s] + s$ 处减少。但是

$$H'_s(n+1+0) - H'_s(n+0) = \frac{1}{\lambda + \alpha} \left( \frac{\lambda}{\lambda + \alpha} \right)^{n+1} \left[ h + \alpha c + (p - \alpha c) \left( 1 - \left( \frac{\lambda}{\lambda + \alpha} \right)^{-[s]} \right) \right]$$

最小值 $S(s)$ 必须满足 $H'_s(S + 0) \ge 0$。因此 $S$ 必然是整数。如果 $s$ 是整数，我们推断出

$H'_s(x + 0) \ge 0, \forall x > S.$

因此

$H_s(x) = \inf_{y > x} H_s(y), \forall x \ge S.$

现在对于 $s \le x \le S$ 我们有

$H_s(x) \le 0,$

并且

$\inf_{\eta > s} H_s(\eta) = H_s(S) = -K$

如果 $s$ 不是整数，我们只能推断出

$H'_s(n + 1 + 0) \ge H'_s(n + 0) \ge 0, \forall n > S.$

导数可能有一些负值。这可能发生在区间 $(n + [-s] + s, n)$ 上。但是，我们知道对于 $x \ge s$

$H_s(x) \le K + H_s(x + \xi), \forall \xi \ge 0$

### 14.6.7. 求解 S.

数 S 的特征是它是严格大于 s 的第一个数，使得

$H'_s(S-0) \le 0, H'_s(S+0) \ge 0.$

由于 $H'_s(x)$ 是分段常数的，它是第一个整数 n，使得

$$H'_s(n+0) = \frac{1}{\alpha} \left[ (\alpha c + h) \left( 1 - \left( \frac{\lambda}{\alpha + \lambda} \right)^{n+1} \right) - (p - \alpha c) \left( \frac{\lambda}{\alpha + \lambda} \right)^{n+1} \left( 1 - \left( \frac{\lambda}{\alpha + \lambda} \right)^{[-s]} \right) \right] \ge 0,$$

和

$$H'_s(n-1+0) = \frac{1}{\alpha} \left[ (\alpha c + h) \left( 1 - \left( \frac{\lambda}{\alpha + \lambda} \right)^n \right) - (p - \alpha c) \left( \frac{\lambda}{\alpha + \lambda} \right)^n \left( 1 - \left( \frac{\lambda}{\alpha + \lambda} \right)^{[-s]} \right) \right] < 0.$$

## 14.7. 泊松需求的遍历情况

现在的目标是让 $\alpha$ 趋向于 0。在这种情况下 $g_s(x) = (f(x) - f(s)) \mathbb{1}_{x>s}$。

接下来函数 $H_s(x)$ 变为

(14.7.1) $$H_s(x) = \sum_{j=0}^{[x-s]} \frac{g_s(x-j)}{\lambda}, \forall x \ge s; H_s(x) = 0, \forall x \le s$$

数 S(s) 是通过计算左导数和右导数得到的

$$H'_s(x+0) = \sum_{j=0}^{[x-s]} \frac{g'_s(x-j+0)}{\lambda}$$

$$H'_s(x-0) = \begin{cases} \sum_{j=0}^{[x-s]-0} \frac{g'_s(x-j-0)}{\lambda}, & \text{if } [x-s] < x-s \\ \sum_{j=0}^{[x-s]-1} \frac{g'_s(x-j-0)}{\lambda}, & \text{if } [x-s] = x-s \end{cases}$$

并且我们写

$H'_s(S+0) \ge 0; H'_s(S-0) \le 0$

### Lemma 14.1.

假设 -s 为整数且 $\frac{ps}{h}$ 不是整数，则

$S(s) = \left[ -\frac{ps}{h} \right].$

证明. 注意

$[S-s] = [S] - s.$

回顾

$$g'_s(x+0) = \begin{cases} h, & \text{if } x \ge 0 \\ -p, & \text{if } x < 0 \end{cases}$$

和

$$g'_s(x-0) = \begin{cases} h, & \text{if } x > 0 \\ -p, & \text{if } x \le 0 \end{cases}$$

第一个条件意味着

$[S] + 1 \ge -\frac{ps}{h}.$

等号不可能成立，由于假设，因此

$[S] + 1 > -\frac{ps}{h}.$

对于第二个条件，我们需要考虑 $S - s$ 是整数还是非整数的情况。如果它不是整数，那么 $S$ 不能是整数，但此时 $H'_s(S-0) = H'_s(S+0) = 0$，这是不可能的。如果 $S$ 是整数，那么第二个条件相当于

$hS + ps \le 0,$

因此得出结果。

我们可以通过公式计算 $H'_s(S)$

$$H'_s(S) = \frac{1}{\lambda} \left[ -p \frac{s^2}{2} + p \frac{s}{p} + S \left( ps + h \frac{S+1}{2} \right) \right].$$

为了定义最优 $s$，我们必须写出方程

$$K \lambda = p \frac{s^2}{2} - p \frac{s}{p} - S \left( ps + h \frac{S+1}{2} \right).$$

如果我们用 $-p \frac{s}{h}$ 近似 $S$，我们很容易推断出 $s$ 由以下定义

(14.7.2) $$s = - \sqrt{\frac{2hK\lambda}{p(h+p)}},$$

和订购数量 $S - s$ 由以下给出

(14.7.3) $$S - s = \sqrt{\frac{2K\lambda(p+h)}{ph}}.$$

我们看到当 $p \to \infty$ 时，我们得到精确的 EOQ 公式。

## Little 法则：

由于我们有积压和等待时间，一个自然的问题是 Little 法则是否适用于此模型。等待从库存为零的时刻开始，直到它变为 $s < 0$ 的时间。如果 $\tau$ 表示这个随机时间，我们有

$\tau = \inf \{ t | D(t) = -s \}.$

为了简化，我们假设 $s$ 为整数。那么

$D(\tau) = -s.$

因为在 $0, \tau$ 上我们有

$x(t) = -D(t),$

平均积压为

$\frac{1}{\tau} \int_0^\tau D(t) dt,$

平均等待时间是

$E \frac{1}{\tau} \int_0^\tau (\tau - t) dt = \frac{1}{2} E \tau.$

Little 法则是以下关系

$E \frac{1}{\tau} \int_0^\tau D(t) dt = \lambda \frac{1}{2} E \tau.$

左边可以写成

$E \int_0^1 D(\rho \tau) d\rho.$

结果来自以下性质：

### **练习 14.10.** 验证公式

$ED(\tau) = \lambda E \tau,$

对于由过程 $D(t)$ 生成的滤流 $\mathcal{F}^t$ 相对于的任何停时。

性质的证明如下。假设

$\tau = \nu h,$

其中 $\nu$ 是随机整数，$h$ 是确定的实数。那么

$D(\nu h) = \sum_{j \ge 0} (D((j+1)h) - D(jh)) \mathbf{1}_{j < \nu h}.$

注意

$\mathbf{1}_{j < \nu h} \text{ is } \mathcal{F}^{jh} \text{ measurable},$

并且 $D((j+1)h) - D(jh)$ 与 $\mathcal{F}^{jh}$ 独立，我们很容易推断出

$ED(\nu h) = \sum_{j \ge 0} h E \mathbf{1}_{j < \nu} = \lambda h E \nu.$

所以结果对形式为 $\nu h$ 的停时成立。现在写

$ED\left( \left[ \frac{\tau}{h} \right] h \right) \le ED(\tau) \le ED\left( \left[ \frac{\tau}{h} \right] h + h \right),$

由此可得

$\lambda E\left( \left[ \frac{\tau}{h} \right] h \right) \le ED(\tau) \le \lambda E\left( \left[ \frac{\tau}{h} \right] + 1 \right) h,$

结果随之得出。

## 14.8. 带前置时间的泊松需求

### 14.8.1. 模型描述.

我们引入确定性前置时间 $L$，并假设在等待交货时不下订单。这可以由物流和安全原因来证明。因此模型转换如下：

$y_\varepsilon(t; V) = x - D(t) + M(t - L; V),$

其中

$M(t; V) = \sum_{\{n | \theta_n < t\}} v_n,$

并且冲击时刻 $\theta_n$ 满足 $\theta_{n+1} > \theta_n + L$。

成本函数由 $J_s(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp -\alpha \theta_n + \int_0^\infty f(y(t; V)) \exp -\alpha t dt \right]$ 给出。

在时刻 0 我们假设管道中没有交货。

### 14.8.2. 值函数的不等式.

值函数 $u(x) = \inf_V J_s(V)$ 满足以下不等式和互补松弛条件（变分不等式）

(14.8.1)
$$u(x) \le K + E \int_0^L f(x - D(t)) \exp -\alpha t dt + \inf_{v \ge 0} [cv + Eu(x + v - D(L)) \exp -\alpha L] = M(u)(x),$$

和

(14.8.2) $-\lambda(u(x-1) - u(x)) + \alpha u(x) \le f(x).$

互补松弛条件表示

(14.8.3) $[((\alpha + \lambda)u(x) - \lambda u(x-1)) - f(x)][u(x) - M(u)(x)] = 0$

### 14.8.3. 最优 s, S 策略.

s, S 策略的概念易于扩展。引入函数很方便

$g(x) = f(x) + \alpha c x + \lambda E \int_0^L (f(x - 1 - D(t)) - f(x - D(t))) \exp -\alpha t dt - \alpha E \int_0^L f(x - D(t)) \exp -\alpha t dt$

并且我们设

$g_s(x) = (g(x) - g(s)) \mathbb{I}_{x > s}.$

如前所述，对于给定的 s，我们求解

(14.8.4) $(\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = g_s(x), \forall x \ge s; H_s(x) = 0, \forall x \le s$

接下来我们定义对应于 s 的值函数

$u_s(x) = H_s(x) - cx + E \int_0^L f(x - D(t)) \exp -\alpha t dt + C(s),$

其中 $C(s)$ 仅依赖于 s。我们希望

$(\alpha + \lambda)u_s(x) - \lambda u_s(x-1) = f(x), \forall x \ge s.$

我们很容易检查常数 $C(s)$ 必须满足

$\alpha C(s) = g(s) + \lambda c.$

另一方面

$C(s) = K + \inf_{\eta \ge s} [c\eta + Eu_s(\eta - D(L)) \exp -\alpha L].$




我们最终推导出获得 s 值的方程

```
(14.8.5) \frac{(g(s) + \lambda c)(1 - \exp(-\alpha L))}{\alpha} = K + c \lambda L \exp(-\alpha L) + \{ \inf_{n \ge s} c \lambda n (1 - \exp(-\alpha L)) + \exp(-\alpha L) E[H_s(\eta - D(L))] + \int_0^L f(y - D(t + L)) \exp(-\alpha t) dt \}
```

利用前面的关系，通过使用一个重要的恒等式，即

```
(14.8.6) \exp(-\alpha L) E f(x - D(L)) - f(x) + (\alpha + \lambda) \int_0^L f(x - D(t)) \exp(-\alpha t) dt - \lambda \int_0^L f(x - 1 - D(t)) \exp(-\alpha t) dt = 0, \forall x
```

### 练习 14.11.

验证恒等式 (14.8.6)。检查它是否归约为恒等式
-x^+ + \exp(-\alpha L) E(x - D(L))^+ + (\alpha + \lambda) E \int_0^L (x - D(t))^+ \exp(-\alpha t) dt - \lambda E \int_0^L (x - 1 - D(t))^+ \exp(-\alpha t) dt = 0.

最简单的方法是证明该表达式关于 x 的导数为零。由于当 x \le 0 时它为 0，因此对所有 x 都为零。

利用这个表达式，我们可以断言

```
(14.8.7) g(x) = \alpha c x + \exp(-\alpha L) E f(x - D(L)),
```

因此我们得到

### 引理 14.2. 函数 g(x) 是凸的且连续。

**证明。** 这直接来自 f 的凸性。

函数 g 不是连续可微的，而是分段线性的。

### 引理 14.3. 假设

```
\alpha c - p \exp(-\alpha L) < 0,
```

则函数 g(x) 满足

```
g(x) \to +\infty, as |x| \to +\infty.
```

它有一个唯一的最小值，记为 \hat{n}，是正整数。

**证明。** 注意

```
g'(x) = \alpha c - p \exp(-\alpha L), if x < 0,
```

且假设意味着 g(x) 在 x < 0 时单调递减。此外，它保证了

```
g(x) \to +\infty, as x \to -\infty.
```

当 x \to +\infty 时，同样的性质平凡地成立。由于该函数是分段线性的，在正整数处有不连续点，因此最小值是整数。它是正数，因为函数在 x < 0 时单调递减。

显式写出

\( g(x) = (\alpha c - p \exp(-\alpha L))x + \lambda L p \exp(-\alpha L) + (h + p) \exp(-(\alpha + \lambda)L) \sum_{j=0}^{[x]} (x - j) \frac{(\lambda L)^j}{j!} . \)

我们推导出

\( g'(n+0) = \alpha c - p \exp(-\alpha L) + (h + p) \exp(-(\alpha + \lambda)L) \sum_{j=0}^{n} \frac{(\lambda L)^j}{j!} . \)

这在 n 中是严格递增的。因此最小值是唯一的。

接下来我们转换 s 为解的方程，即方程 (14.8.5)。我们使用一个新的恒等式

(14.8.8) \( E \int_0^L g(x - D(t)) \exp(-\alpha t) dt = \alpha L (1 - \exp(-\alpha L)) + \lambda c L \exp(-\alpha L) - \lambda c \frac{1 - \exp(-\alpha L)}{\alpha} + \exp(-\alpha L) E \int_0^L f(x - D(t+L)) \exp(-\alpha t) dt \)

利用这个恒等式，我们可以将方程 (14.8.5) 写为

(14.8.9) \( 0 = K + \inf_{\eta \ge x} E \left[ \exp(-\alpha L) H_s(\eta - D(L)) + \int_0^L (g(\eta - D(t)) - g(s)) \exp(-\alpha t) dt \right] \)

定义

\( \psi_s(x) = E \left[ \exp(-\alpha L) H_s(x - D(L)) + \int_0^L (g(x - D(t)) - g(s)) \exp(-\alpha t) dt \right] , \)

然后我们得到方程

\( 0 = K + \inf_{\eta \ge x} \psi_s(\eta) . \)

我们可以证明 \psi_s(x) 的一个新表达式。我们有

### 引理 14.4.

(14.8.10) \( \psi_s(x) = H_s(x) + \exp(-(\alpha + \lambda)L) \sum_{j=[x-s]+1}^{\infty} \frac{(g(x-j) - g(s)) \lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^{\infty} \frac{((\alpha + \lambda)L)^k}{k!} \)

**证明。** 我们使用公式

\( \int_0^L (g(x - D(t)) - g(s)) \exp(-\alpha t) dt = \exp(-(\alpha + \lambda)L) \sum_{j=0}^{\infty} \frac{(g(x-j) - g(s)) \lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^{\infty} \frac{((\alpha + \lambda)L)^k}{k!} , \)

且对于 x \ge s

\( \exp(-\alpha L) E H_s(x - D(L)) = \exp(-(\alpha + \lambda)L) \sum_{j=0}^{[x-s]} \frac{(g(x-j) - g(s)) \lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=0}^{j} \frac{((\alpha + \lambda)L)^k}{k!} . \)

为了得到第一个，需要计算积分

```
\( A_j = \int_0^L \frac{L(\lambda t)^j}{j!} \exp(-(\alpha + \lambda)t) dt. \)
```

可以通过归纳法验证

```
\( A_j = \frac{\lambda^j \exp(-(\alpha + \lambda)L)}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^\infty \frac{((\alpha + \lambda)L)^k}{k!}. \)
```

结果通过使用 H_s(x) 的定义得到。

汇总结果，我们可以写出，对于 x \ge s

```
(14.8.11) \( \psi_s(x) = \sum_{j=0}^{[x-s]} \frac{(g(x-j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} \quad + \exp(-(\alpha + \lambda)L) \sum_{j=[x-s]+1}^\infty \frac{(g(x-j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^\infty \frac{((\alpha + \lambda)L)^k}{k!}, \)
```

且对于 x \le s

```
(14.8.12) \( \psi_s(x) = \exp(-(\alpha + \lambda)L) \sum_{j=0}^\infty \frac{(g(x-j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^\infty \frac{((\alpha + \lambda)L)^k}{k!} \)
```

## 14.8.4. S(s) 的存在性。

固定 s。我们将证明 \psi_s(x) 有下界，并且当 x \to +\infty 时趋于 +\infty。从公式 (14.8.11) 出发，回顾 \bar{n} 的定义，我们有

```
\( \psi_s(x) \ge \frac{g(\bar{n}) - g(s)}{\alpha}. \)
```

还有

```
\( \psi_s(x) \ge \frac{g(x) - g(s)}{\alpha + \lambda} + \frac{\lambda}{\alpha} \frac{g(\bar{n}) - g(s)}{\alpha + \lambda}. \)
```

因此 \psi_s(x) 的最小值可达，我们定义 S(s) 为最小的最小值。

## 14.8.5. s 的存在性。

还剩下求解方程 (14.8.9)。

### 定理 14.3. 存在 (14.8.9) 的一个解，使得 s < \bar{n}。它在区间 (-\infty, \bar{n}] 上是唯一的。

**证明。** 定义

```
\( z(s) = \inf_{\eta \ge s} \psi_s(\eta). \)
```

方程 (14.8.9) 意味着

```
\( z(s) + K = 0. \)
```

注意

```
\( z(\bar{n}) \ge 0, \)
```

这直接来自 \psi_s(\eta) 的定义。我们将证明 z(s) 在 s < \bar{n} 时是递增的。取

```
\( s' < s < \eta. \)
```

我们有公式

$$\psi_{s'}(\eta) - \psi_s(\eta) = \sum_{j=0}^{\lfloor \eta - s \rfloor} \frac{(g(s) - g(s'))\lambda^j}{(\alpha + \lambda)^{j+1}} + \sum_{j=\lfloor \eta - s \rfloor + 1}^{\lfloor \eta - s' \rfloor} \frac{(g(\eta - j) - g(s'))\lambda^j}{(\alpha + \lambda)^{j+1}} - \exp(-(\alpha + \lambda)L) \sum_{j=\lfloor \eta - s \rfloor + 1}^{\lfloor \eta - s' \rfloor} \frac{(g(\eta - j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^{\infty} \frac{((\alpha + \lambda)L)^k}{k!} + \exp(-(\alpha + \lambda)L) \sum_{j=\lfloor \eta - s' \rfloor + 1}^{\infty} \frac{(g(s) - g(s'))\lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^{\infty} \frac{((\alpha + \lambda)L)^k}{k!}.$$

因此

$g(s) - g(s') < 0$

此外，当 \lfloor \eta - s \rfloor + 1 \le j \le \lfloor \eta - s' \rfloor 时，我们有

s \ge \eta - j \ge s'

汇总结果，我们可以断言

s' < s < \bar{n}, s' < s < \eta \Rightarrow \psi_{s'}(\eta) < \psi_s(\eta)

因此，对于 s' < s < \bar{n}，我们可以断言

z(s') \le \inf_{\eta \ge s} \psi_{s'}(\eta) \le \inf_{\eta \ge s} \psi_s(y) = z(s).

接下来我们检查

z(s) \to -\infty \text{ as } s \to -\infty.

只需证明

\psi_s(x) \to -\infty \text{ as } s \to -\infty, \forall x \text{ fixed.}

回顾对于 x < 0, s < 0

g(x) - g(s) = (\alpha c - p \exp(-\alpha L))(x - s),

我们可以轻易推导出不等式

$$\exp(-(\alpha + \lambda)L) \sum_{j=\lfloor x - s \rfloor + 1}^{\infty} \frac{(g(x - j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} \sum_{k=j+1}^{\infty} \frac{((\alpha + \lambda)L)^k}{k!} \le (p \exp(-\alpha L) - \alpha c) \sum_{j=\lfloor x - s \rfloor + 1}^{\infty} \frac{j\lambda^j}{(\alpha + \lambda)^{j+1}} \to 0 \text{ as } s \to -\infty$$

接下来考虑

$$\sum_{j=0}^{\lfloor x - s \rfloor} \frac{(g(x - j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} = \sum_{j=0}^{\lfloor x - s \rfloor} \frac{(g(x - j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}} + \sum_{j=\lfloor x - s \rfloor + 1}^{\lfloor x - s \rfloor} \frac{(g(x - j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}}$$

第二项是正的。我们使用这样一个事实：对于 s < 0

g(x) - g(s) = (\alpha c - p \exp(-\alpha L))(x - s) + (h + p) \exp(-\alpha L) E(x - D(L))^+,

且对于 x > s

g(x) - g(s) \le (h + p) \exp(-\alpha L) E(x - D(L))^+ \le (h + p) \exp(-\alpha L) x^+

因此

\(\sum_{j=[x-\hat{n}]+1}^{[x-s]} \frac{(g(x-j)-g(s))\lambda^j}{(\alpha+\lambda)^{j+1}} \le \frac{(h+p)\exp-\alpha L x^+}{\alpha}.\)

所以我们可以断言

\(\limsup_{s \to -\infty} \psi_s(x) \le \sum_{j=0}^{[x-\hat{n}]} \frac{(g(x-j)-g(s))\lambda^j}{(\alpha+\lambda)^{j+1}} + \frac{(h+p)\exp-\alpha L x^+}{\alpha}.\)

第一个求和式由若干项组成，每一项当 \(s \to -\infty\) 时都趋于 \(-\infty\)。这就完成了定理 14.3 的证明。

### 14.8.6. s, S 策略的最优性。

我们需要检查一组不等式和互补松弛条件。互补松弛性质显然得到满足。当 \(x < s\) 时，我们有

\(u_s(x) = -cx + E \int_0^L f(x-D(t)) \exp-\alpha t dt + \frac{g(s)+\lambda c}{\alpha},\)

并且我们必须检查

\((\alpha+\lambda)u_s(x) - \lambda u_s(x-1) \le f(x).\)

利用 \(u_s(x)\) 的值，这等价于 \(g(x) \ge g(s)\)，由于 \(s \le \hat{n}\)，这显然得到满足。

困难部分在于 \(x \ge s\) 的情况，此时必须满足不等式 (14.8.1)。代入 \(H_s(x)\) 后，这等价于

\(H_s(x) + (g(s)+\alpha c) \frac{1-\exp-\alpha L}{\alpha} \le K + c\alpha L \exp-\alpha L + \inf_{\eta \ge x} \left\{ cp(1-\exp-\alpha L) \right.\)
\(\left. + \exp-\alpha L E H_s(\eta-D(L)) + \int_0^L f(\eta-D(t+L)) \exp-\alpha t dt \right\}.\)

这可解释为

(14.8.13) \(H_s(x) \le K + \inf_{\eta \ge x} \psi_s(\eta).\)

由于右边为正，只有在 \(x > x_0\) 时才需要检查，其中 \(x_0\) 是 \(H_s(x)\) 首次为正或等于 0 的值。

回顾公式

\(H'_s(x+0) = \sum_{j=0}^{[x-s]} \frac{g'(x-j+0)\lambda^j}{(\alpha+\lambda)^{j+1}},\)

我们注意到 \(x_0 \ge \hat{n}\)。

对于整数 \(x\)，我们还可以写出公式

\(\left( \frac{\alpha+\lambda}{\lambda} \right)^x H'_s(x+0) = \sum_{k=-[x-s]}^x \frac{g'(k+0)}{\alpha+\lambda} \left( \frac{\alpha+\lambda}{\lambda} \right)^k .\)

然后考虑整数 \(x \ge x_0\)。我们可以假设 \(H'_s(x_0+0) \ge 0\)，这相当于假设在 \(x_0\) 稍后 \(H_s(x) > 0\)，否则我们要证明的性质在 \(x_0\) 之后成立。

因此

$$ \sum_{k=-\lceil s \rceil}^{x_0} \frac{g'(k+0)}{\alpha + \lambda} \left( \frac{\alpha + \lambda}{\lambda} \right)^k \ge 0. $$

由于对于 \( k \ge \tilde{n}, g'(k+0) \ge 0 \)，我们推导出

$$ \sum_{k=-\lceil s \rceil}^{x} \frac{g'(k+0)}{\alpha + \lambda} \left( \frac{\alpha + \lambda}{\lambda} \right)^k \ge 0, \forall x \ge x_0. $$

由此可见 \( H'_s(x+0) \ge 0, \forall x \ge x_0 \)。因此

$$ H_s(x) \le H_s(y), \forall y \ge x \ge x_0. $$

注意到 \( H_s(y) \le \psi_s(y), \forall y \ge s \)，我们轻易推导出

$$ H_s(x) \le K + \psi_s(y), \forall y \ge x \ge x_0, $$

证明已完成。

## 14.9. 带前置时间的泊松需求的遍历方法

### 14.9.1. 函数 \( \psi_s(x) \) 的研究。

我们现在考虑 \(\alpha = 0\) 的情况。首先得到

\( g(x) = E f(x - D(L)), \)

所以

\( g(x) = \begin{cases} -px + \lambda p L, & \text{if } x \le 0 \\ -p \sum_{k=\lceil x \rceil + 1}^{[x] + 1} (x - k) \frac{(\lambda L)^k}{k!} \exp -\lambda L + h \sum_{k=0}^{[x]} (x - k) \frac{(\lambda L)^k}{k!} \exp -\lambda L, & \text{if } x \ge 0 \end{cases} \)

接下来我们计算函数 \(\psi_s(x)\)。对于 \(x \ge s\)，我们有

\( \psi_s(x) = \frac{1}{\lambda} \left\{ \sum_{j=0}^{[x-s]} (g(x-j) - g(s)) + \exp -\lambda L \sum_{j=[x-s]+1}^{\infty} (g(x-j) - g(s)) \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \right\}, \)

而对于 \(x \le s\)

\( \psi_s(x) = \frac{1}{\lambda} \sum_{j=0}^{\infty} (g(x-j) - g(s)) \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}. \)

在后续内容中，为稍作简化，我们假设 \(s\) 为整数。我们可以给出 \(\psi_s(x)\) 的显式公式，具体取决于 \(s\) 的符号。计算过程繁琐但并不困难。只需考虑 \(x \ge s\)。

假设 \(s \le x \le 0\) 为整数，我们有

(14.9.1) \( \psi_s(x) = pL(s - x) + \frac{1}{2} \lambda L^2 p - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x-s]} \frac{(\lambda L)^j}{j!} \cdot \left[ \left( x - \frac{1}{2} [x] - \frac{1}{2} j \right) ([x] - j + 1) - s(x - j) + \frac{s^2}{2} - \frac{s}{2} \right]. \)

我们利用以下事实

\( g(x) - g(s) = p(s - x), \)

当 \(s < x < 0\) 时。

接下来的情况是 \(s < 0 < x\)。注意，在这种情况下，

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+,\)

可以轻易验证，给出 \(\psi_s(x)\) 的公式是公式 (14.9.1) 加上一个额外项

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x]} E(x - j - D(L))^+.\)

该项等于

\(\frac{h+p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1).\)

汇总结果，我们得到，对于 \(s < 0 < x\)

(14.9.2) \(\psi_s(x) = -pL(x - s) + \frac{1}{2}\lambda L^2 p + \frac{h}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) - \frac{p}{\lambda} \exp - \lambda L \sum_{j=s+[x]+1}^{[x] - s} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) + \frac{p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x] - s} \frac{(\lambda L)^j}{j!} \left((x - j)s + \frac{s}{2} - \frac{s^2}{2}\right).\)

现在考虑 \(0 < s\) 的情况。我们回顾一下

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+ - (s - D(L))^+].\)

同样，我们需要向表达式 (14.9.1) 添加一个由以下给出的额外项

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x] - s} E([(x - j - D(L))^+ - (s - D(L))^+] \\ + \exp - \lambda L \left[ \sum_{j=[x] - s + 1}^{\infty} E[(x - j - D(L))^+ - (s - D(L))^+] \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \right]\)

我们可以将乘以 \(\frac{h+p}{\lambda}\) 的额外项表示如下

\(\exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - s) \frac{(\lambda L)^k}{k!} + \exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - k) \frac{(\lambda L)^k}{k!} \\ + \exp - 2\lambda L \lfloor_{j=[x] - s + 1}^{[x]} \sum_{m=0}^{k-j} \left( \sum_{m=0}^{[x] - j - s} (x - j - s) \frac{(\lambda L)^m}{m!} - \sum_{m=[x] - j + 1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \right) \\ \cdot \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \rfloor - \exp - 2\lambda L \sum_{j=[x] + 1}^{\infty} \sum_{m=0}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}\)

变换后我们得到

$$
\begin{aligned}
&\exp -\lambda L \sum_{k=0}^{s-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1) \left( x - \frac{[x]}{2} - \frac{s}{2} \right) \\
&+ \exp -\lambda L \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) \left( x - \frac{[x]}{2} - \frac{k}{2} \right) \\
&+ \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=s+1}^{[x]-j} \sum_{k=j+1}^{\infty} (x - j - s) \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \\
&- \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=[x]-j+1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \\
&- \sum_{j=[x]+1}^{\infty} \sum_{m=s+1}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}.
\end{aligned}
$$

### 14.9.2. 局部最小值。

我们首先得到导数 \(\psi'_s(x + 0)\)。

对于 \(s < x < 0\)

(14.9.3) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!}.\)

接下来我们考虑 \(s < 0 < x\) 的情况。我们有

(14.9.4) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=[x]+1}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{\exp -\lambda L}{\lambda} \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} (h([x] - j + 1) + ps).\)

最后，对于 \(0 < s < x\)，我们有

(14.9.5) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=0}^{s-1} \frac{(\lambda L)^j}{j!} ([x] - s + 1) + \sum_{j=s}^{[x]} \frac{(\lambda L)^j}{j!} ([x] - j + 1) - \exp -\lambda L \sum_{j=[x]+1}^{[x]+s} \sum_{l=j+1-s}^{\infty} \frac{(\lambda L)^l}{l!} \sum_{k=[x]+1}^{j} C_l^{j-k} \right].\)

我们可以验证对于 \(s < 0 < x\) 的公式

\(\psi'_s(x + 1 + 0) - \psi'_s(x + 0) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{[x]+1-s} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=[x]+2}^{[x]+1-s} \frac{(\lambda L)^j}{j!} \right].\)




定义对于 $n \ge 0$ 的整数

$$\xi(n) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} \right].$$

我们有

$$\xi(n+1) - \xi(n) = \frac{(\lambda L)^{n+2}}{(n+2)!} \frac{\exp -\lambda L}{\lambda} \left[ h + p - p \frac{(\lambda L)^{-s}}{(n+3)\cdots(n+2-s)} \right].$$

定义 $n_0 = n_0(s)$ 为使得

$$(n+3)\cdots(n+2-s) \ge \frac{p(L\lambda)^{-s}}{h+p}$$

成立的第一个正整数。

### 引理 14.5.
对于 $s \le 0$，存在且仅存在一个值 $S$ 是局部最小值。即满足

$$\psi'_s(S+0) \ge 0, \psi'_s(S-1+0) < 0.$$

最小值 $S$ 是满足此条件的唯一值

**证明。** $n_0$ 是 $\xi(n)$ 的最小值。我们首先检查

(14.9.6) $$\xi(0) \ge 0 \Rightarrow \xi(n) \ge 0, \forall n.$$

因此

$$\psi'_s(n+0) \text{ 是递增的.}$$

如果 $\psi'_s(0+) \ge 0$，则 $\psi'_s(n+0) \ge 0, \forall n$。因此 $S=0$。如果 $\psi'_s(0+) < 0$，注意到对于足够大的 $n$，$\psi'_s(n+0) > 0$，存在且仅存在一个满足局部最小值性质的 $S$。

让我们证明性质 (14.9.6)。注意

$$\xi(0) \ge 0 \Rightarrow h(1+\lambda L) \ge p \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!}.$$

因此

$$\xi(n) \ge \frac{p \exp -\lambda L}{\lambda(1+\lambda L)} \left[ \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} (1+\lambda L) \right].$$

令

$$b_j = \frac{(\lambda L)^j}{j!}, \nu = 1+s \ge 1.$$

$\xi(n)$ 的正性将是以下不等式的结果

$$\sum_{j=0}^\nu b_j \sum_{k=0}^{n+1} b_k - \sum_{j=0}^{n+\nu} b_j \sum_{k=0}^{n+1} b_k$$

要证明该不等式，只需证明

$$\frac{\sum_{j=0}^{n+\nu} b_j}{\sum_{k=0}^{n+1} b_k}$$

关于 $n$ 是递减的。

比较 $n$ 和 $n+1$ 中的项，这等同于证明

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=0}^{n+\nu} b_j,$$

并且只需证明

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=\nu-1}^{n+\nu} b_j = b_{n+2} \sum_{k=0}^{n+1} b_{\nu-1+k}$$

因此只需检查

$$\frac{b_k}{b_{n+2}} \le \frac{b_{\nu-1+k}}{b_{n+1+\nu}} \forall k \le n+1.$$

这归结为检查性质

$$(k+1)\cdots(n+2) \le (k+\nu)\cdots(n+1+\nu), \forall k \le n+1,$$

该性质成立。

仍需考虑 $\xi(0) < 0$ 的情况，此时 $\xi(n_0) < 0$。

由于对于足够大的 $n$，$\xi(n) > 0$，存在 $S_1 > n_0$ 使得

$$\xi(S_1) \ge 0, \xi(S_1 - 1) < 0.$$

则

$$\xi(n) \ge 0 \forall n \ge S_1; \xi(n) < 0 \forall 0 \le n < S_1.$$

因此 $S_1$ 是唯一确定的。

故

$$\psi'_s(n+1+0) - \psi'_s(n+0) \ge 0, \forall n \ge S_1,$$

$$\psi'_s(n+1+0) - \psi'_s(n+0) < 0, \forall 0 \le n < S_1.$$

因此 $S_1$ 是 $\psi'_s(n+0)$ 的最小值。如果该最小值为正，我们可以得出 $S=0$。否则，很容易检查出存在唯一的局部最小值 $S > S_1$。证明完毕。

我们现在考虑 $s > 0$ 的情况，此时自然 $S(s) \ge s > 0$。我们首先计算导数

$$\psi'_s(x+0) = R_s([x]) = -pL + \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} \frac{(\lambda L)^j}{j!} ([x] - s - j + 1)$$

$$+ \frac{h+p}{\lambda} \exp -\lambda L \sum_{k=0}^{[x]-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1)$$

$$+ \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) - \sum_{k=0}^{[x]-s} \frac{(\lambda L)^k}{k!} ([x] - k + 1 - s)$$

$$+ \exp -\lambda L \sum_{j=[x]+1-s}^{[x]} \sum_{m=0}^{[x]-j} \sum_{k=j+1}^{\infty} \left[ \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].$$

函数 \(R_s(n), n \ge s\) 关于 \(n\) 是递增的。我们确实可以检查

\(R_s(n+1) - R_s(n) = \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{n+1-s} \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=n+2-s}^{n+1} \frac{(\lambda L)^j}{j!} - \exp -\lambda L \sum_{m=0}^{s-1} \sum_{j=n+2-s}^{n+2-m} \frac{(\lambda L)^j}{j!} \frac{(\lambda L)^m}{m!} \right],\)

和

\(R_s(n+1) - R_s(n) \ge 0, \forall n \ge s\)

我们接下来考虑 \(R_s(s), s \ge 0\)。我们首先检查

\(R_s(s) = -pL + \frac{h}{\lambda} \exp -\lambda L + \frac{h+p}{\lambda} \exp -\lambda L \left[ - \sum_{j=s+1}^{\infty} \frac{(\lambda L)^j}{j!} + \exp -\lambda L \sum_{j=0}^{s} \sum_{m=0}^{s-j} \sum_{k=1}^{\infty} \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].\)

很容易检查 \(R_s(s)\) 是一个递增函数。我们可以继续以唯一方式定义 \(S(s)\)。我们需要 \(\hat{s}\) 为使得 \(R_s(s) \ge 0\) 的第一个正整数。该数是唯一确定的。

### 引理 14.6.
对于 \(s > \hat{s}\) 我们有 \(S(s) = s\)，而对于 \(0 \le s \le \hat{s}\)，$S(s)$ 是使得 \(R_s(s) \ge 0\) 的第一个整数。

**证明。** 证明直接来自 \(R_s(x)\) 的单调性性质。

## 提前期情况下的小定律.
我们考虑正提前期 \(L\) 的小定律。假设在起始时刻初始库存为 \(x\)。依次定义

\(\theta = \inf\{t|x - D(t) \le 0\}; \quad \tau = \inf\{t|x - D(t) \le s\}.\)

注意

\(D(\tau) - D(\theta) = -s, \text{ 如果 } \tau \neq \theta, \tau \neq 0.\)

在时刻 \(\tau\)，如果 \(\tau > 0$ 下订单大小为 \(S - s$，如果 \(\tau = 0$ 下订单大小为 \(S - x\)。它在时刻 \(\tau + L$ 交付。因此交付后库存为 \(S - D(\tau + L) + D(\tau)\)。注意我们假设 \(s$ 为整数（正或负）。

缺货的可能性仅在 \(\theta < \tau + L$ 时存在。否则没有缺货和等待时间。如果 \(S - D(\tau + L) + D(\tau) > 0$，则缺货在时刻 \(\tau + L$ 被吸收。如果不是正数，人口 \(D(\tau + L) - D(\tau) - S$ 必须等到下一次交付。定义

\(\tau_1 = \inf\{t \ge \tau + L|S - D(t) + D(\tau) \le s\} - \tau - L,\)

则该部分人口将在时刻 \(\tau + L + \tau_1 + L$ 被服务。注意

\(S - D(\tau + L) + D(\tau) < s \Rightarrow \tau_1 = 0.\)

而且

\(S - D(\tau + L) + D(\tau) > s \Rightarrow S - D(\tau + L + \tau_1) + D(\tau) = s.\)

### 练习 14.12.
验证公式

\(\lambda E \tau_1 = E(S - s - D(\tau + L) + D(\tau))^+.\)

一个周期是区间 \(\min(\theta, \tau), \tau + L$。我们考虑在周期内到达的需求，它们在被服务前构成的缺货以及相应的等待时间。如果 \(\theta > \tau + L$，则没有缺货和等待时间。在时刻 \(\tau + L$ 被服务的人口为

- \(-s + \min(S, D(\tau + L) - D(\tau))$ 如果 \(\tau > 0\)，
- \(-x + \min(S, D(L))$ 如果 \(\tau = 0\)。

如果在 \(\tau + L$ 时库存为负，则周期内的所有需求无法在时刻 \(\tau + L$ 时得到满足。剩余部分将在时刻 \(\tau + L + \tau_1$ 被服务。其水平为 \((S - D(\tau + L) + D(\tau))^-\)。因此平均缺货可以表示为

$$B = \int_0^1 (D(\theta) + \rho(\tau + L - \theta)^+ - D(\theta))\,d\rho + (S - D(\tau + L) + D(\tau))^- \frac{L}{\tau + L - \theta} + (S - D(\tau + L) + D(\tau))^- \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}}$$

则预期缺货为

$$EB = \frac{\lambda}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} \right].$$

我们现在可以考虑等待时间。首先我们注意到，整个人口在周期内平均等待时间为 \(\frac{1}{2}(\tau + L - \theta)^+$。此外，结转部分需要额外等待时间 \(L + \tau_1$，其中 \(\tau_1$ 可以为 0。按人口比例加权，我们得到预期平均等待时间

$$EWT = \frac{1}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} \right]$$

小定律：

$$EB = \lambda EWT,$$

不成立。如果忽略结转的概率，它近似成立。即我们假设

$$\text{Prob } \{D(\tau + L) - D(\tau) > S\} \sim 0,$$

这意味着

$$\sum_{j=S+1}^\infty \frac{(\lambda L)^j}{j!} \sim 0.$$

另一种近似是将总人口 \(D(\tau + L) - D(\theta)$ 在 \((S - D(\tau + L) + D(\tau))^-\) 的系数中替换为 \(\lambda(\tau + L - \theta)$。这两个随机变量具有相同的期望值。使用这些近似，小定律仍然有效。这些近似要求提前期不能太大。




## 14.10. 带提前期的泊松需求：使用库存位置

### 14.10.1. 问题的表述。

考虑前一节定义的问题，我们稍微改变一下符号，因为系统的状态将不再是库存，而是一个新概念，称为_库存位置_。冲动控制仍将用

\( M(t; V) = \sum_{\{n|\theta_n < t\}} v_n, \)

表示，这次停止时间 \(\theta_n\) 没有约束。库存将用 \(\bar{y}_x(t; V)\) 表示。然而，\(x\) 并不代表初始库存，而是初始库存位置。

相对于实际库存，库存位置加上所有尚未交付的订单。因此，库存位置 \(y_x(t; V)\) 的演化由

\( y_x(t; V) = x - D(t) + M(t; V), \)

描述，其中 \(x\) 是其初始值，将在时间 \(L\) 成为库存的一部分。显然我们有关系

\(\bar{y}_x(t + L; V) = y_x(t; V) - D(t + L) + D(t).\)

该关系定义了大于 \(L\) 时刻的库存。在 \(L\) 之前，库存不受提前期区间内决策的影响。如果我们没有 0 之前订单的记录，那么 \(L\) 之前的库存就是时间 0 时的库存扣除需求后的结果。无论如何，相应的成本是固定的，没有优化的可能性。

对应于冲动控制 \(V\) 的成本由

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + \int_L^\infty f(\bar{y}_x(t; V)) e^{-\alpha t} dt \right] . \)

给出。在此表述中，我们没有包括区间 \(0, L\) 上的成本，它是一个常数。该成本可以立即写为

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + e^{-\alpha L} \int_0^\infty f(y_x(t; V) - D(t + L) + D(t)) e^{-\alpha t} dt \right] \)

我们注意到 \(D(t+L)-D(t)\) 与 \(y_x(t; V)\) 无关。因此，我们可以引入函数

\(\phi(x) = e^{-\alpha L} E f(x - D(L)),\)

成本由

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + \int_0^\infty \phi(y_x(t; V)) e^{-\alpha t} dt \right] . \)

给出。对于库存位置，我们得到与没有提前期的库存问题相同的问题，但积分成本 \(\phi(x)\) 代替 \(f(x)\)。相应的函数 \( g(x) \) 与前一节所考虑问题中进入的函数相同，见方程 (14.87)。

### 14.10.2. 值函数问题。

值函数

\( u(x) = \inf_V J_x(V), \)

满足一组不等式和互补条件

\( u(x) + cx \le K + \inf_{\eta \ge x} (c\eta + u(\eta)); \)

\( (\alpha + \lambda)u(x) - \lambda u(x-1) \le \phi(x); \)

\( [(\alpha + \lambda)u(x) - \lambda u(x-1) - \phi(x)][u(x) + cx - K - \inf_{\eta \ge x} (c\eta + u(\eta))] = 0. \)

### 14.10.3. s, S 策略。

与我们在无延迟情况下所做的一样，我们寻找一个函数 \( u_s(x) \)，使得

\( u_s(x) + cx = u_s(s) + cs, \forall x \le s \)

\( (\alpha + \lambda)u_s(x) - \lambda u_s(x-1) = \phi(x), \forall x \ge s \)

\( u_s(s) + cs = K + \inf_{\eta \ge s} (c\eta + u_s(\eta)). \)

最后一个表达式是关于 s 的方程，一旦函数 \( u_s(x) \) 唯一确定。为了定义任何 s 的 \( u_s(x) \)，我们需要 \( u_s(s) \) 的值。这个数由

\( u_s(s) = \frac{\phi(s) + \lambda c}{\alpha}. \)

给出。这促使引入函数 \( H_s(x) \)，它是以下方程的解

\( H_s(x) = 0, \forall x \le s \)

\( (\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = \lambda g(x) - g(x), \forall x \ge s \)

\( 0 = K + \inf_{\eta \ge s} H_s(\eta), \)

函数 \( g(x) \) 由

\( g(x) = \phi(x) + \rho cx, \)

定义，这是上一节（14.8.7）中已引入的函数。我们有关系

\( H_s(x) = u_s(x) + cx - cs - \frac{\lambda c + \phi(s)}{\alpha}. \)

我们回顾 \( H_s(x) \) 的公式。

(14.10.1)
\( H_s(x) = \sum_{j=0}^{\lfloor x-s \rfloor} \frac{(g(x-j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}}, \forall x \ge s; H_s(x) = 0, \forall x \le s. \)

14.6 节发展的理论适用，其中 \( g(x) \) 的最小值是 \(\hat{n}\)，它是一个正整数，而不是 0。

首先考虑 \( S(s) \)，它使 \( H_s(\eta), \eta \ge s \) 最小。我们有

\( S(s) = s, \text{ if } s > \hat{n}. \)

接下来考虑 \( s < \hat{n} \) 的情况。如同在 14.6 节中，我们证明 \( H_s(x) \) 在 \( (s, \infty) \) 上达到其最小值。选取最小的最小值 \( S(s) \)，我们为 \( s < \hat{n} \) 定义函数 \( S(s) \)。必然有

\( S(s) \ge \hat{n}. \)

剩下的就是找到 s。它必须满足关于 s 的方程

\[ \min_{n \ge s} H_n(s) = -K. \]

再次，14.6 节的理论证明了解 s 的存在性和唯一性。接下来我们可以陈述定理 14.2 的等价定理

定理 14.4。我们假设 \( c\alpha - p e^{-\alpha L} < 0 \)。那么，s, S 策略是最优的。

## 14.11. 带提前期的库存位置的遍历理论

### 14.11.1. 问题的表述。

我们现在考虑 \(\alpha = 0\)。问题归结为以下内容。首先

\[ g(x) = E f(x - D(L)), \]

和 \(\phi(x) = g(x)\)。

函数 \(H_s(x)\) 满足

\[ H_s(x) - H_s(x-1) = \frac{g(x) - g(s)}{\lambda}, \forall x \ge s; H_s(x) = 0, \forall x \le s. \]

对 s, S 由

\[ H_s(S) = \inf_{n \ge s} H_n(s) = -K. \]

定义。我们得到

\[ H_s(x) = \frac{1}{\lambda} \left[ \sum_{j=0}^{\lfloor x-s \rfloor} (g(x-j) - g(s)) \right]. \]

右导数满足

\[ H'_s(x+0) = \frac{1}{\lambda} \sum_{j=0}^{\lfloor x-s \rfloor} g'(x-j+0). \]

由于函数 \(H_s(x)\) 是分段线性的，\(H_s(x)\) 的计算归结为使用公式的 x 为整数的情况

\[ H_s(x) = H_s(\lfloor x \rfloor) + H'_s(\lfloor x \rfloor+0)(x-\lfloor x \rfloor). \]

因此我们可以考虑 x 为整数。那么

\[ H_s(x) = \frac{1}{\lambda} \sum_{j=0}^{x+\lfloor -s \rfloor} (g(x-j) - g(s)) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{x} (g(k) - g(s)), \]

和

\[ H'_s(x+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{x} g'(k+0). \]

为了得到整数 s, S，我们按以下步骤进行：我们写出条件

\[ H'_s(S+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S} g'(k+0) \ge 0; \]

\[ H'_s(S-1+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S-1} g'(k+0) < 0, \]

和

\[ H_s(S) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S} (g(k) - g(s)) = -K. \]

接下来我们使用恒等式

\[ g(k+1) = g(-\lfloor -s \rfloor) + \sum_{j=-\lfloor -s \rfloor}^{k} g'(j+0). \]

第二个关系写为

\[ -K\lambda = (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1) + \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)(S-j). \]

使用第一个条件，我们可以写出

(14.11.1)
\[ \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)j < K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1); \]
\[ \sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0)j \ge K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1). \]

我们还加上

(14.11.2)
\[ \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0) < 0; \]
\[ \sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0) \ge 0. \]

### 14.11.2. 近似。

如果我们用 s 的整数值近似 s，我们得到以下系统

(14.11.3)
\[ \sum_{j=s}^{S-1} g'(j+0)j < K\lambda; \]
\[ \sum_{j=s}^{S} g'(j+0)j \ge K\lambda. \]

(14.11.4)
\[ \sum_{j=s}^{S-1} g'(j+0) < 0; \]
\[ \sum_{j=s}^{S} g'(j+0) \ge 0. \]

首先我们注意到，如果忽略 \(K\)，我们得到基础库存策略

\( s = S = \bar{n}. \)

接下来我们用方程近似这些条件

\[ \sum_{j=s}^{S} g'(j+0) = 0, \]

和

\[ \sum_{j=s}^S jg'(j+0) = K\lambda. \]

我们对这些关系进行连续近似

(14.11.5)
\[ g(s) = g(S) \]
\[ \int_s^S xg'(x+0)dx = K\lambda \]

### 14.11.3. 解释。

我们可以通过对成本函数进行直接推理来恢复系统 (14.11.5)。我们考虑一对 s, S，假设它们是整数。应用 s, S 策略，库存的演化描述如下。设 Q = S - s，并依次定义停止时间序列

\[ T_{n+1} = T_n + \tau_n, T_0 = 0, \]

其中

\[ \tau_n = \inf\{t > 0 | D(T_n + t) - D(T_n) \ge Q\}, \]

并设 \(\tau_0 = \tau\)。

停止时间 \(\tau_n\) 是独立同分布的随机变量，分布与随机变量 \(\tau\) 相同。考虑从 S 开始的库存演化，记为 \(y_S(t)\)。我们有

\[ y_S(t) = S - D(t) + D(T_n), T_n \le t < T_{n+1}, \]

并且我们可以将 \(T_n\) 解释为

\[ T_{n+1} = \inf\{t \ge T_n | y_S(t-0) \le s\}, \]

和

\[ y_S(T_n) = S, y_S(T_n - 0) \le s. \]

定义

\[ C_\alpha(s, Q) = E \int_0^\infty e^{-\alpha t} \phi(y_S(t)) dt. \]

我们计算

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E \int_{T_n}^{T_{n+1}} e^{-\alpha t} \phi(S - D(t) + D(T_n)) dt, \]

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E e^{-\alpha T_n} \int_0^{\tau_n} e^{-\alpha t} \phi(S - D(T_n + t) + D(T_n)) dt, \]

并且根据独立性考虑

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E(e^{-\alpha \tau})^n E \int_0^\tau e^{-\alpha t} \phi(S - D(t)) dt. \]

最后我们得到

(14.11.6)
\[ C_\alpha(s, Q) = \frac{E \int_0^\tau e^{-\alpha t} \phi(S - D(t)) dt}{1 - E(e^{-\alpha \tau})} \]

现在考虑从任意值 x 开始的库存演化。我们首先定义

\[ \tau_x = \inf\{t > 0 | D(t) \ge x - s\}. \]




我们接下来依次定义 \( T_{n,x} \) 如下：

\( T_{0,x} = \tau_x; \quad T_{n+1,x} = T_{n,x} + \tau_{n,x} \)

\( \tau_{n,x} = \inf \{t > 0 | D(T_{n,x} + t) - D(T_{n,x}) \ge Q \} \)

我们通过如下关系定义 \( y_x(t) \)：

\( y_x(t) = x - D(t), t < \tau_x, \)
\( y_x(t) = S - D(t) + \tau(T_{n,x}), T_{n,x} \le t < T_{n+1,x} \)
\( y_x(T_{n,x}) = S; y_x(T_{n,x} - 0) \le s \)

我们考虑

\( u_\alpha(x) = E \int_0^\infty \exp -\alpha t \phi(y_x(t)) dt. \)

在上述记法中，我们不显式写出 \( s, S \)。另一方面，我们显式标注 \( \alpha \)，因为我们将令 \( \alpha \) 趋于 0。还要注意

\( u_\alpha(S) = C_\alpha(s, Q) = C_\alpha. \)

以同样的方式获得 \( C_\alpha \) 的公式后，我们可以验证以下公式

\( u_\alpha(x) = E \int_0^{\tau_x} \exp -\alpha t \phi(x - D(t)) dt + C_\alpha E \exp -\alpha \tau_x \)

从前面的公式我们注意到

\( x \le s \Rightarrow \tau_x = 0 \Rightarrow u_\alpha(x) = C_\alpha. \)

现在的关键点是求得 \( \tau_x \) 的概率分布。为了稍作简化，我们假设 \( x, s \) 为整数。我们有

\( P(\tau_x \le t) = P(D(t) \ge x - s) = \exp -\lambda t \sum_{j=x-s}^\infty \frac{(\lambda t)^j}{j!}. \)

这个概率分布的密度由以下给出

\( \frac{d}{dt} P(\tau_x \le t) = \lambda \exp -\lambda t \frac{(\lambda t)^{x-s-1}}{(x-s-1)!}. \)

当 \( x - s \ge 1 \) 时这有意义。如果 \( x = s \)，则

\( \frac{d}{dt} P(\tau_x \le t) = \lambda \exp -\lambda t, \)

且对于 \( x < s \) 密度为 0。

然后可以计算函数 \( E \exp -\alpha \tau_x \)。我们留作练习来证明

\( E \exp -\alpha \tau_x = \left( \frac{\lambda}{\alpha + \lambda} \right)^{x-s}. \)

接下来我们可以写

\( E \int_0^{\tau_x} \exp -\alpha t \phi(x - D(t)) dt = E \int_0^\infty \exp -\alpha t \mathbb{I}_{\{\tau_x > t\}} \phi(x - D(t)) dt \)

\( E \int_0^{\tau_x} \exp -\alpha t \phi(x - D(t)) dt = E \int_0^\infty \exp -\alpha t \mathbb{I}_{\{D(t) < x - s\}} \phi(x - D(t)) dt. \)

引入记法

\( \tilde{\phi}_s(x) = \phi(x) \mathbb{I}_{x > s}, \)

我们有

$$ E \int_0^{\tau_x} \exp -\alpha t \phi(x - D(t))dt = E \int_0^\infty \exp -\alpha t \tilde{\phi}_s(x - D(t))dt $$

汇总结果，我们得到公式

$$ u_\alpha(x) = E \int_0^\infty \exp -\alpha t \tilde{\phi}_s(x - D(t))dt + C_\alpha \left( \frac{\lambda}{\alpha + \lambda} \right)^{x-s} $$

在 ergodic theory 中，人们关心当 \(\alpha \to 0\) 时 \(\alpha u_\alpha(x)\) 的行为，对于任何固定的 \(x\)。从上面的公式可以清楚地看出

$$ \lim_{\alpha \to 0} \alpha u_\alpha(x) = \lim_{\alpha \to 0} \alpha C_\alpha $$

很容易验证

$$ \lim_{\alpha \to 0} \alpha C_\alpha = \frac{\lambda H_s(S)}{Q} $$

其中

$$ H_s(S) = E \int_0^\infty \tilde{\phi}_s(S - D(t))dt $$

很容易验证关系

$$ H_s(S) - H_s(S - 1) = \frac{\tilde{\phi}_s(S)}{\lambda} = \frac{\phi(S)}{\lambda} $$

通过归纳，可以验证公式

$$ H_s(S) = \sum_{j=0}^{Q-1} \frac{\phi(S - j)}{\lambda} $$

最后我们得到了

$$ \lim_{\alpha \to 0} \alpha u_\alpha(x) = \lim_{\alpha \to 0} \alpha C_\alpha = \sum_{k=s+1}^S \frac{\phi(k)}{Q} $$

回顾一下，根据标准的 ergodic theory 论证

$$ \lim_{T \to \infty} \alpha u_\alpha(x) = \lim_{T \to \infty} \frac{1}{T} \int_0^T \phi(y_x(t))dt = \sum_{k=s+1}^S \frac{\phi(k)}{Q} $$

右边可以解释为 \(E\phi(X)\)，其中 \(X\) 是分布在 \(s+1, \cdots, S\) 上的均匀随机变量。我们现在可以继续对参数 \(s, S\) 进行优化。我们优化 ergodic cost

$$ \lim_{\alpha \to 0} \alpha E \left[ (K + cQ) \sum_{n=0}^\infty \exp -\alpha T_n + \int_0^\infty \exp -\alpha t \phi(y_x(t))dt \right] $$

根据前面的结果，这相当于

$$ L(s, Q) = \frac{\lambda K}{Q} + \sum_{k=1}^Q \frac{g(s + k)}{Q} $$

回顾

$$ g(x) = E f(x - D(L)) $$

为了写出必要条件，我们考虑连续近似，其写作

\( L(s, Q) = \frac{\Lambda K}{Q} + \frac{1}{Q} \int_0^Q g(s + x) dx. \)

很容易恢复条件 (14.11.5)。

## 带扩散需求的库存控制

## 15.1. 引言

我们继续研究连续时间的库存控制。我们希望考虑一个相当一般的需求过程，结合确定速率和第14章中的泊松跳跃，加上一个扩散项。我们遵循文献[9]和补充文献[4]的工作。我们将使用Q.V.I（准变分不等式）的全部力量来解决与冲动控制问题相关的动态规划问题。然后我们检查最优反馈是通过 *s, S* 策略获得的。

## 15.2. 问题表述

### 15.2.1. 需求过程。

需求过程由三部分组成：一个恒定速率 \(\nu\) 的确定性部分。在第14章中它被称为 \(\lambda\)，但 \(\lambda\) 将用于复合泊松部分。我们考虑一个概率空间 \(\Omega, \mathcal{A}, P\)，在其上定义了一个强度为 \(\Lambda\) 的泊松过程 \(n(t)\)，一个维纳过程 \(w(t)\) 以及一组独立同分布的随机变量 \(\xi_1, \cdots, \xi_i, \cdots\)。所有这些随机变量和随机过程相互独立。随机变量 \(\xi_i\) 在 \(R^+\) 上具有概率密度 \(\mu\)。我们通过以下定义复合泊松过程

\(N(t) = \sum_{i \le n(t)} \xi_i.\)

那么在区间 \((0, t)\) 上的需求由以下给出

\(D(t) = \nu t + N(t) + \sigma w(t),\)

其中 \(\sigma\) 是正系数。令 \(\mathcal{F}^t = \sigma(D(s), s \le t)\)

一个冲动控制是一个序列

\(\theta_n, v_n,\)

其中 \(\theta_n\) 是相对于滤流 \(\mathcal{F}^t\) 的停时，\(v_n\) 是 \(\mathcal{F}^{\theta_n}\) 可测的随机变量。用 *V* 表示一个冲动控制，相应的库存由公式描述

\(y_\sigma(t; V) = x - D(t) + M(t; V),\)

与

\(M(t) = M(t; V) = \sum_{\{n \mid \theta_n < t\}} v_n\)

### 15.2.2. 控制问题。

再次令

$f(x) = hx^+ + px^-$.

我们定义成本泛函

(15.2.1) \( J_\sigma(V) = E \left[ \sum_{n=0}^\infty (K + cv_n) \exp -\alpha \theta_n + \int_0^\infty f(y_\sigma(t; V)) \exp -\alpha t dt \right] \)

以及值函数

\( u(x) = \inf J_\sigma(V) \)

为了获得动态规划关系，我们可以假设足够的光滑性并写出最优性原理。如果在一小段时间 \(\delta\) 内不下订单，则我们可以写

\( u(x) \le \delta f(x) + (1 - \alpha \delta) Eu(x - D(\delta)), \)

和

\( Eu(x - D(\delta)) = Eu(x - \delta v - N(\delta) - \sigma w(\delta)). \)

形式上

\( N(\delta) = \begin{cases} 0, & \text{w.p. } 1 - \lambda \delta \\ \in (\xi, \xi + d\xi), & \text{w.p. } \lambda \delta \mu(\xi) d\xi \end{cases} \)

且 \(w(\delta)\) 是均值为0、方差为 \(\delta\) 的高斯变量。因此

\( Eu(x - D(\delta)) \simeq (1 - \lambda \delta) Eu(x - \delta v - \sigma w(\delta)) + \lambda \delta \int_0^\infty u(x - \xi) \mu(\xi) d\xi \)

在假设 \(u\) 二阶光滑的情况下，对 \(\delta\) 进行一阶展开，我们得到不等式

\( Au(x) + \alpha u(x) \le f(x), \)

其中 \(A\) 是积分微分算子

(15.2.2) \( Au(x) = -\frac{1}{2} \sigma^2 u''(x) + \nu u'(x) - \lambda \int_0^\infty (u(x - \xi) - u(x)) \mu(\xi) d\xi. \)

如果我们下一个大小为 \(v\) 的订单，则库存立即变为 \(x + v\)，我们写出不等式

\( u(x) \le K + cv + u(x + v), \forall v \ge 0 \)

所以

\( u(x) \le M(u)(x), \)

与

(15.2.3) \( M(u)(x) = K + \inf_{v > 0} [cv + u(x + v)] \)

并且由于必须做出两个决定之一，我们有互补松弛条件

\( (Au(x) + \alpha u(x) - f(x))(u(x) - M(u)(x)) = 0. \)

### 15.2.3. 准变分不等式。

我们假设存在 \(\bar{\pi} > 0\)，使得 \(\int_0^\infty \exp \pi \bar{\pi} \mu(d\xi) = +\infty\)

(15.2.4) 
$$ \int_0^\infty \exp \pi \xi \mu(d\xi) < +\infty, \forall \pi < \bar{\pi} $$

我们寻找一个函数 \(u(x)\)，它是 \(C^1\)，几乎处处二次可微且具有线性增长，使得

(15.2.5) 
$$ \begin{aligned} Au(x) + \alpha u(x) &\le f(x) \\ u(x) &\le M(u(x)) \\ (Au(x) + \alpha u(x) - f(x))(u(x) - M(u(x))) &= 0 \end{aligned} $$

我们称这组关系为Q.V.I.（准变分不等式）

## 15.3. *s, S* 策略

### 15.3.1. 记法。

令

$$ \begin{aligned} G(x) &= u(x) + cx; \\ g(x) &= f(x) + \alpha cx, \end{aligned} $$

那么Q.V.I被略微修改为

(15.3.1) 
$$ \begin{aligned} AG(x) + \alpha G(x) &\le g(x) + cv + c\lambda\tilde{\xi} \\ G(x) &\le K + \inf_{\eta > x} G(\eta) \end{aligned} $$

(15.3.2) 
$$ (AG(x) + \alpha G(x) - (g(x) + cv + c\lambda\tilde{\xi})) \left( G(x) - K - \inf_{\eta > x} G(\eta) \right) = 0, $$

其中 \(\tilde{\xi}\) 表示概率为 \(\mu\) 的随机变量的均值

$$ \tilde{\xi} = \int_0^{+\infty} \xi \mu(d\xi). $$

如果 \(s\) 是实数，我们通过求解以下问题定义 \(G_s(x)\)

(15.3.3) 
$$ \begin{aligned} AG_s(x) + \alpha G_s(x) &= g(x) + cv + c\lambda\tilde{\xi} & x > s \\ G_s(x) &= K + \inf_{\eta > s} G_s(\eta) & x \le s \end{aligned} $$

由于我们希望解是 \(C^1\)，我们必须施加条件

(15.3.4) 
$$ G'_s(s) = 0 $$

### 15.3.2. 函数 \(H_s(x)\)。

自然地寻找导数 $$ H_s(x) = G'_s(x) $$

它是以下问题的解

(15.3.5) 
$$ \begin{aligned} AH_s(x) + \alpha H_s(x) &= g'(x) & x > s \\ H_s(x) &= 0 & x \le s \end{aligned} $$

由于 \(g'(x)\) 有界，我们寻找有界解

**提议 15.1.** 我们假设(15.2.4)。那么，对于任何 \(s\)，存在一个唯一的连续有界函数解 (15.3.5)。该解在 \((s, +\infty)\) 上是 \(C^2\)。





证明。让我们证明唯一性。这意味着
$AH_s(x) + \alpha H_s(x) = 0 \quad x > s$
$H_s(x) = 0 \quad x \le s$
的有界解为 0。这由最大原理考虑得出。我们有
$AH_s(x) + \alpha H_s(x) = -\frac{1}{2}\sigma^2 H_s''(x) + \nu H_s'(x) + (\lambda + \alpha)H_s(x) - \lambda \int_0^{x-s} H_s(x-\xi)\mu(\xi)d\xi.$

假设 $H_s(x)$ 变为严格正。让我们证明它不可能有局部最大值。如果它有一个局部最大值 $x^* > s$，则我们可以假设它是最小的一个。在这样的点
$H_s'(x^*) = 0, \quad H_s''(x^*) < 0,$
和
$\int_0^{x^*-s} H_s(x^* - \xi)\mu(\xi)d\xi \le H_s(x^*) \int_0^{x^*-s} \mu(\xi)d\xi \le H_s(x^*).$
因此 $AH_s(x^*) > 0$，这与假设矛盾。因此 $H_s'(x) > 0$。由于 $H_s(x)$ 是有界的，我们必须有当 $x \to +\infty$ 时 $H_s'(x) \to 0$。因此存在一点 $x^*$ 使得 $H_s'(x^*) < 0$。在这样的点，必然有 $AH_s(x^*) > 0$，我们再次得到矛盾。因此 $H_s(x) \le 0$，类似的推理表明它不能变为严格负。

为了证明存在性，我们将构造一个显式解。然而，我们需要一些预备知识。让我们记
$\hat{\mu}(\pi) = \int_0^{+\infty} \exp \pi \xi \mu(\xi)d\xi, \quad \pi < \bar{\pi}$

我们考虑函数
$\chi(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda + \alpha - \lambda\hat{\mu}(\pi),$
其中 $\pi \le \bar{\pi}$。我们首先注意到
$\chi(\bar{\pi}) = \chi(-\infty) = -\infty;$
$\chi'(\pi) = -\sigma^2\pi - \nu - \lambda \int_0^{+\infty} \xi \exp \pi \xi \mu(\xi)d\xi;$
$\chi''(\pi) = -\sigma^2 - \lambda \int_0^{+\infty} \xi^2 \exp \pi \xi \mu(\xi)d\xi < 0;$
$\chi'(\bar{\pi}) = -\infty, \quad \chi'(-\infty) = +\infty, \quad \chi'(0) < 0.$

因此 $\chi'(\pi)$ 从 $+\infty$ 严格递减到 $-\infty$。存在唯一的 $\pi_0 < 0$ 使得 $\chi'(\pi_0) = 0$。因此 $\pi_0$ 是 $\chi(\pi)$ 的极大值点。由于 $\chi(0) = \alpha$，我们得到 $\chi(\pi_0) > 0$。因此 $\chi(\pi)$ 只有两个零点 $\beta_1$ 和 $\beta_2$，满足
$\beta_2 < \pi_0 < 0 < \beta_1 < \bar{\pi}.$

还记
$\chi_0(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda + \alpha,$

并令 $\beta_0$ 为 $\chi_0(\pi) = 0$ 的正根。由于 $\chi(\pi) < \chi_0(\pi)$，我们有 $\chi(\beta_0) < 0$，因此
$\beta_1 < \beta_0 < \bar{\pi}.$

为了继续，我们引入以下问题：

\(-\frac{1}{2}\sigma^2 \Gamma''(x) + \nu \Gamma'(x) + (\lambda + \alpha)\Gamma(x) - \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi = 0, \quad \forall x > 0\)
\(\Gamma(0) = 1, \quad \Gamma(+\infty) = 0\)
(15.3.6)

我们将在下面的引理 15.1 中证明，(15.3.6) 存在且仅存在一个满足以下条件的解：

\(\exp -\beta_0 x < \Gamma(x) < \exp -\beta_1 x\)
(15.3.7)

我们还将证明性质

\(\Gamma'(0) = \frac{2\nu}{\sigma^2} + \beta_2.\)
(15.3.8)

我们现在可以给出 (15.3.5) 的解，即

\(H_s(x) = \int_s^x \Gamma(x-\xi)Q(\xi)d\xi,\)
(15.3.9)

其中

\(Q(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \exp \beta_2(\eta-x) g'(\eta)d\eta,\)
(15.3.10)

根据估计 (15.3.7)，我们可以检查 $H_s(x)$ 保持有界，直接计算表明它确实是方程 (15.3.5) 的解。

让我们陈述

**引理 15.1.** _方程_ (15.3.6) _存在且仅存在一个满足_ (15.3.7) _的解。_

**证明。** 唯一性通过最大原理考虑得出，如同命题 15.1 中的 \(H_s(x)\)。为了证明存在性，我们首先检查

\(\underline{\Gamma}(x) = \exp -\beta_0 x \quad \overline{\Gamma}(x) = \exp -\beta_1 x,\)

满足

\(-\frac{1}{2}\sigma^2 \overline{\Gamma}''(x) + \nu \overline{\Gamma}'(x) + (\lambda + \alpha)\overline{\Gamma}(x) - \lambda \int_0^x \overline{\Gamma}(x-\xi)\mu(\xi)d\xi \ge 0;\)
(15.3.11)

\(-\frac{1}{2}\sigma^2 \underline{\Gamma}''(x) + \nu \underline{\Gamma}'(x) + (\lambda + \alpha)\underline{\Gamma}(x) - \lambda \int_0^x \underline{\Gamma}(x-\xi)\mu(\xi)d\xi \le 0.\)
(15.3.12)

然后我们考虑序列

\(-\frac{1}{2}\sigma^2 \Gamma_{n+1}''(x) + \nu \Gamma_{n+1}'(x) + (\lambda + \alpha)\Gamma_{n+1}(x) = \lambda \int_0^x \Gamma_n(x-\xi)\mu(\xi)d\xi;\)
\(\Gamma_0(x) = \underline{\Gamma}(x),\)

边界条件为

\(\Gamma_n(0) = 1, \quad \Gamma_n(+\infty) = 0.\)

假设

\(\underline{\Gamma}(x) \le \Gamma_n(x) \le \overline{\Gamma}(x),\)

则 $\Gamma_{n+1}(x)$ 可通过求解一个二阶微分方程容易得到，关键性质是检查

\(\Gamma_n(x) \le \Gamma_{n+1}(x) \le \overline{\Gamma}(x).\)

让我们对 $n = 0$ 进行证明。这等价于

$\underline{\Gamma}(x) \le \Gamma_1(x) \le \overline{\Gamma}(x)$

根据 (15.3.11)、(15.3.12) 和 $\Gamma_1(x)$ 的方程，这很容易检查。

假设该性质在 n 处成立，可以立即检查它在 n + 1 处也成立。因此序列 $\Gamma_n(x)$ 是一个单调递增序列。极限 $\Gamma(x)$ 是 (15.3.6) 的解，并按构造满足 (15.3.7)。让我们检查 (15.3.8)。

我们首先检查 $\Gamma'(+\infty) = 0$。确实，我们将方程 (15.3.6) 写为

$-\frac{1}{2}\sigma^2\Gamma''(x) + \nu\Gamma'(x) + (\lambda + \alpha)\Gamma(x) = \theta(x)$

其中

$\theta(x) = \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi$

并且我们可以给出估计

$0 \le \theta(x) \le \lambda\hat{\mu}(\beta_1) \exp-\beta_1 x$

现在我们可以将 (15.3.13) 的解作为带有右项的二阶微分方程求得。注意

$\bar{\beta}_0 = -\beta_0 - \frac{2\nu}{\sigma^2}$

它是 $\chi_0(x) = 0$ 的负根，我们容易得到

$\Gamma(x) = C \exp-\beta_0 x + \frac{2}{\sigma^2(\beta_0 - \bar{\beta}_0)} \left[ \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi + \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \right]$

和

$\Gamma'(x) = -\beta_0 C \exp-\beta_0 x - \frac{2}{\sigma^2(\beta_0 - \bar{\beta}_0)} \cdot \left[ \bar{\beta}_0 \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi + \bar{\beta}_0 \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \right]$

但是

$0 \le \int_0^x \exp-\beta_0(x-\xi)\theta(\xi)d\xi \le \frac{\lambda\hat{\mu}(\beta_1)}{\beta_0 - \beta_1}(\exp-\beta_1 x - \exp-\beta_0 x)$

$0 \le \int_x^{+\infty} \exp\bar{\beta}_0(\xi-x)\theta(\xi)d\xi \le \frac{\lambda\hat{\mu}(\beta_1)}{\beta_1 - \bar{\beta}_0} \exp-\beta_1 x$

这意味着 $\Gamma'(+\infty) = 0$。我们可以用 $\exp \pi x$（其中 $\pi < 0$）来检验 (15.3.6)。我们设

$\hat{\Gamma}(\pi) = \int_0^{+\infty} \exp \pi x \Gamma(x) dx$

它定义良好。

利用边界条件，我们容易计算得

$\frac{\sigma^2}{2}(\Gamma''(0) - \pi) - \nu + \hat{\Gamma}(\pi)(\pi) = 0$

并将此关系应用于 $\pi = \beta_2$，我们得到关系 (15.3.8)。

我们必须有 $\Gamma'(0) < 0$。让我们确实检查这个性质：

让我们证明性质

(15.3.14) 
 \(\frac{2\nu}{\sigma^2} + \beta_2 < -\beta_1\)

这将意味着 $\Gamma'(0) < 0$。这首先源于注意到 \(\chi(-\frac{\nu}{\sigma^2}) < 0\)。因此

\(-\frac{\nu}{\sigma^2} > \pi_0 \Rightarrow -2\frac{\nu}{\sigma^2} - \beta_2 > \beta_2.\)

接下来

\(\chi(-\frac{\nu}{\sigma^2} - \beta_2) = \lambda \hat{\mu}(\beta_2) - \lambda \hat{\mu} (-\frac{\nu}{\sigma^2} - \beta_2) < 0.\)

综合结果，不等式 (15.3.14) 立即得出。

### 15.3.3. 获取 s, S 策略。

我们现在来寻找 s 和 $G_s(x)$ 满足 (15.3.3)、(15.3.4) 的解。我们首先为任意 s 构造 $G_s(x)$ 满足 (15.3.3) 的第一个方程和 (15.3.4)。对于固定的 s，我们简单地定义

(15.3.15) 
 \(G_s(x) = G_s(s) + \int_s^x H_s(\xi) d\xi, \, x > s\) 
 \(= G_s(s), \, x \le s\)

这样定义了一个 $C^1$ 函数，且 (15.3.4) 显然满足。让我们检查，对于 $G_s(s)$ 的适当选择，第一个方程 (15.3.3) 是否满足。该函数在 $x > s$ 处也是 $C^2$。我们利用 $G_s(x)$ 的定义重新解释第一个方程 (15.3.3)。经过整理，对于 $x > s$ 我们得到

\(-\frac{\sigma^2}{2} H''_s(x) + \nu H'_s(x) + \alpha G_s(s) + (\lambda + \alpha) \int_s^x H_s(\xi) d\xi\) 
 \(-\lambda \int_0^{x-s} \mu(\xi) \left( \int_s^{x-\xi} H_s(\eta) d\eta \right) d\xi = g(x) + c\nu + c\lambda \tilde{\xi}.\)

另一方面，从 (15.3.3) 出发，对 s 到 x 进行积分，我们得到

\(-\frac{\sigma^2}{2} H'_s(x) + \frac{\sigma^2}{2} H'_s(s) + \nu H_s(x) + (\lambda + \alpha) \int_s^x H_s(\xi) d\xi -\) 
 \(\lambda \int_0^{x-s} \mu(\xi) \left( \int_s^{x-\xi} H_s(\eta) d\eta \right) d\xi = g(x) - g(s).\)

注意到 $H'_s(s) = Q(s)$ 并比较两个关系，我们得到 $G_s(s)$ 的值，即

(15.3.16) 
 \(G_s(s) = \frac{\frac{c^2}{2} Q(s) + g(s) + c\nu + c\lambda \tilde{\xi}}{\alpha}.\)

为了继续，我们做标准假设

(15.3.17) 
 \(p - ac > 0.\)

我们可以给出 $Q(x)$ 的显式公式，即

(15.3.18) 
 \(Q(x) = \frac{2}{\beta_2 \sigma^2} (p - ac - (h + p) \exp \beta_2 x^{-}),\)

因此我们有

\(Q'(x) = \frac{2(h+p)}{\sigma^2} \exp -\beta_2 x \mathbb{I}_{x<0},\)



因此 Q(x) 是一个递增函数，且

$$Q(-\infty) = \frac{2}{\beta \sigma_2^2}(p - \alpha c), Q(x) = -\frac{2}{\beta \sigma_2^2}(h + \alpha c), \forall x \ge 0$$

### 命题 15.2.
假设 (15.3.17)，由 (15.3.15) 定义的函数 G_s(x) 在 x > s 处取得其下确界。取最小极小点，我们唯一地定义一个函数 S(s)，使得

$$(15.3.19) \quad G_s(S(s)) = \inf_{\eta \ge s} G_s(\eta).$$

**证明。** 令 x_0 < 0 为使得 Q(x_0) = 0 的唯一点。它由以下明确给出

$$\exp -\beta_2 x_0 = \frac{p - \alpha c}{h + p}.$$

那么对于 s > x_0，我们有 H_s(x) > 0。因此 G_s(x) 在 x > s 时递增，且极小值在 s 处取得。所以在这种情况下，S(s) = s。接下来我们假设 s < x_0。对于 s < x < x_0，我们有 H_s(x) < 0，因此 G_s(x) 在 (s, x_0) 上递减。考虑 x > 0，我们可以写出

$$H_s(x) = \int_s^x \Gamma(x - \xi) Q(\xi) d\xi = -\frac{2}{\sigma^2 \beta_2}(h + \alpha c) \int_0^x \Gamma(\xi) d\xi.$$

利用 \Gamma(x) 的估计和 Q(x) 的最小值，我们可以轻易证明不等式

$$H_s(x) \ge \frac{2}{\sigma^2 \beta_2}(p - \alpha c) \frac{1 - \exp -\beta_1 s}{\beta_1} \exp -\beta_1 x - \frac{2}{\sigma^2 \beta_2}(h + \alpha c) \frac{1 - \exp -\beta_0 x}{\beta_0}, \forall x \ge 0.$$

因此也有

$$\liminf_{x \to +\infty} H_s(x) \ge -\frac{2}{\sigma^2 \beta_2 \beta_0}(h + \alpha c),$$

这也意味着当 x \to +\infty 时 G_s(x) \to +\infty。综合结果我们看到 G_s(x) 在 x > s 处取得其下确界。取最小下确界，我们唯一地定义 S(s)。必然 S(s) 使 G_s(x) 最小化，因此

$$G'_s(S(s)) = H_s(S(s)) = 0; G''_s(S(s)) = H'_s(S(s)) > 0.$$

另外

$$S'(s) H'_s(S(s)) + \frac{\partial H_s}{\partial s}(S(s)) = 0.$$

因为

$$\frac{\partial H_s}{\partial s}(S(s)) = -\Gamma(S(s) - s) Q(s) > 0,$$

我们得到

$$(15.3.20) \quad S'(s) < 0, \text{ 当 } s < x_0 \quad S'(s) = 1, \text{ 当 } s > x_0 .$$

让我们验证

$$(15.3.21) \quad S'(x_0 - 0) = -1.$$

确实，因为 s < x_0 < S(s)，我们可以写出

$$\int_s^{x_0} \Gamma(S(s) - \xi) Q(\xi) d\xi + \int_{x_0}^{S(s)} \Gamma(S(s) - \xi) Q(\xi) d\xi = 0.$$

当 \( s \uparrow x_0 \) 时，我们有 \( S(s) \downarrow x_0 \)。在两个积分中

\(\Gamma(S(s) - \xi) \simeq 1, \quad Q(\xi) \simeq Q'(x_0)(\xi - x_0),\)

这意味着

\((s - x_0)^2 \simeq (S(s) - x_0)^2,\)

考虑符号后，我们得到

\(x_0 - s \simeq S(s) - x_0,\)

因此

\(\frac{S(s) - x_0}{s - x_0} \to -1,\)

这意味着结果成立。

我们可以转向寻找使第二个方程 (15.3.3) 得到满足的 \( s \) 的问题。因为我们要找一个单一数，所以需要一个方程。我们写出

\(G_*(s) = K + \inf_{\eta > s} G_*(\eta),\)

这等价于

(15.3.22) \(0 = K + \int_s^{S(s)} H_s(\eta) d\eta.\)

那么研究函数是自然的

\(\gamma(s) = \int_s^{S(s)} H_s(\eta) d\eta,\)

我们有当 \( s \ge x_0 \) 时 \(\gamma(s) = 0\)，而当 \( s < x_0 \) 时

\(\gamma'(s) = \int_s^{S(s)} \frac{\partial H_s}{\partial s}(\eta) d\eta = -Q(s) \int_s^{S(s)} \Gamma(\eta - s) d\eta > 0.\)

还要注意的是 \(\gamma(s)\) 是 \(C^1\)。回顾 \(\Gamma(x)\) 的估计，我们得到估计

\(\gamma'(s) \ge -\frac{Q(s)}{\beta_0}(1 - \exp -\beta_0(S(s) - s)) \ge -\frac{Q(s)}{\beta_0}(1 - \exp -\beta_0(x_0 - s)).\)

让我们取 \( s < s_1 < x_0 \)，因为 \( Q(s) \) 递增，我们轻易得到

\(\gamma'(s) \ge -\frac{Q(s_1)}{\beta_0}(1 - \exp -\beta_0(x_0 - s_1)) > 0.\)

这意味着当 \( s \to -\infty \) 时 \(\gamma(s) \to -\infty\)。因此，当 \( s \) 从 \(-\infty\) 增加到 \( x_0 \) 时，它从 \(-\infty\) 到 0 严格单调递增。由此可得，存在唯一的 \( s < x_0 \) 使得 \(\gamma(s) = -K\)。我们现在可以陈述

### 定理 15.1.
我们假设 (15.2.4) (15.3.17)。那么存在唯一一对 \( s, G_*(s) \)，使得 \( G_* \in C^1 \) 且 (15.3.3), (15.3.4) 得到满足。

**证明。** 我们已经证明了使得 \(\gamma(s) = -K\) 的数 \( s \) 以及由 (15.3.15), (15.3.16) 定义的对应函数 \( G_*(x) \) 满足 (15.3.3), (15.3.4)。它是唯一的，因为其导数必须与由 (15.3.5) 唯一确定的 \( H_s(x) \) 重合，且值 \( G_*(s) \) 由 (15.3.16) 唯一确定。此外，由于第二个关系 (15.3.3)，数 \( s \) 必须满足 \(\gamma(s) = -K\)，这有唯一解。 \(\square\)

将定理 15.1 中定义的唯一值 \( s \) 的 \( S(s) = S \) 设定，我们得到 \( s,S \) 策略。

## 15.4. 求解 Q.V.I

还剩下要证明 s,S 策略解决问题。这等同于证明由 (15.3.3), (15.3.4) 定义的函数 G_s(x) 解决 Q.V.I. (15.3.1), (15.3.2)。

### 定理 15.2.
与定理 15.1 相同的假设。由 (15.3.3), (15.3.4) 定义的函数 G_s(x) 解决 Q.V.I. (15.3.1), (15.3.2)。

**证明。** 我们首先注意到

$$ \inf_{\eta > x} G_s(\eta) = \inf_{\eta > s} G_s(\eta), \quad \forall x \le s. $$

确实，我们注意到对于 x < \eta < s，我们有

$$ G_s(\eta) = G_s(s) > \inf_{\eta > s} G_s(\eta). $$

因此函数 G_s(x) 满足互补松弛条件 (15.3.2)。还剩下要证明它满足不等式 (15.3.1)。这等同于

(15.4.1) \( A G_s(x) + \alpha G_s(x) \le g(x) + c\nu + c\lambda\xi \quad x \le s; \)

(15.4.2) \( G_s(x) \le K + \inf_{\eta > x} G_s(\eta) \quad x \ge s. \)

我们从 (15.4.1) 开始。由于对于 x \le s 有 G_s(x) = G_s(s)，不等式 (15.4.1) 等同于

$$ \alpha G_s(s) \le g(x) + c\nu + c\lambda\xi \quad x \le s, $$

并且从 G_s(s) 的定义我们得到

$$ \frac{\sigma^2}{2} Q(s) + g(s) \le g(x) \quad x \le s, $$

这成立，因为 Q(s) \le 0 且 g(s) \le g(x) 当 x \le s \le 0。

我们现在转向 (15.4.2)。定义

$$ B_s(x) = G_s(x) - \inf_{\eta > x} G_s(\eta). $$

我们想要证明

(15.4.3) \( B_s(x) \le K, \quad \forall x \ge s. \)

我们从 s \le x \le x_0 开始。函数 G_s(x) 在 (s, x_0) 上递减，因此

$$ \begin{aligned} G_s(x) &\le G_s(s) = K + \inf_{\eta > s} G_s(\eta) \\ &\le K + \inf_{\eta > x} G_s(\eta), \end{aligned} $$

并且 (15.4.3) 得到满足。我们可以假设 x > x_0。假设存在一个点 x' > x_0 使得 B_s(x') \ge K。我们可以假设它是第一个发生这种情况的点。必然

$$ B_s(x') = K, \quad B_s(x) < K, \forall s < x < x' $$

考虑 G_s(\eta)，\eta > x'。其下确界被取得，因为当 x \to +\infty 时 G_s(x) \to +\infty。取最小极小值，我们唯一地定义一个点 x_3，使得

(15.4.4) \( G_s(x_3) = \inf_{\eta \ge x'} G_s(\eta). \)

我们可以声称 \(x_3 \neq x'\)，因为

\(B_s(x') = G_s(x') - G_s(x_3) = K,\)

因此 \(x_3\) 是一个局部极小值点，这意味着

(15.4.5) \(G'_s(x_3) = 0, \quad G''_s(x_3) > 0\)

接下来定义 \(x_2\) 为 \(G_s(\eta), \eta \le x_3\) 的最小极大值点

(15.4.6) \(G_s(x_2) = \sup_{\eta \le x_3} G_s(\eta)\)

极大值被取得，因为

\(\sup_{\eta \le x_3} G_s(\eta) = \sup_{s \le \eta \le x_3} G_s(\eta),\)

并且函数 \(G_s(x)\) 是连续的。让我们检查 \(x_2 \ge x'\)。确实，假设 \(x_2 < x'\)。那么

\(\inf_{\eta \ge x_2} G_s(\eta) \le \inf_{\eta \ge x'} G_s(\eta),\)

并且

\(G_s(x_2) - \inf_{\eta \ge x_2} G_s(\eta) \ge G_s(x') - \inf_{\eta \ge x'} G_s(\eta) = K\)

这与 \(x'\) 的定义矛盾。而且 \(x_2 \neq x_3\)，因为

\(G_s(x_2) - G_s(x_3) \ge G_s(x') - G_s(x_3) = K.\)

因此 \(x_2\) 也是一个局部极大值点，我们有

(15.4.7) \(G'_s(x_2) = 0 \quad G''_s(x_2) < 0.\)

所以我们有 \(x' \le x_2 < x_3\)。让我们证明性质

(15.4.8) \(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3), \quad \forall x \le y \le x_3.\)

确实，如果 \(x < x'\) 那么

\(G_s(x) - G_s(y) \le G_s(x) - \inf_{\eta \ge x} G_s(\eta) < K \le G_s(x_2) - G_s(x_3),\)

如果 \(x \ge x'\) 那么 \(x' \le x \le y \le x_3\) 并且

\(G_s(x) - G_s(y) \le G_s(x_2) - G_s(x_3),\)

从 \(x_2\) 和 \(x_3\) 的定义得出。

最后，让我们定义 \(x_1\) 使得

(15.4.9) \(G_s(x_1) = \inf_{\eta \le x'} G_s(\eta).\)

出于与定义 \(x_2\) 中相同的原因，点 \(x_1\) 被定义为最小极小值点。而且 \(x_1 \neq x'\)。确实

\(G_s(x') = K + \inf_{\eta \ge x'} G_s(\eta),\)

并且回顾 \(x' > x_0 > s\) 且 \(G_s(x)\) 在 \((s, x_0)\) 上递减

\(G_s(x') \ge K + \inf_{\eta \ge x_2} G_s(\eta) = G_s(s) > G_s(x_0) \ge \inf_{\eta \le x'} G_s(\eta) = G_s(x_1),\)

因此 \(x_1\) 是一个局部极小值点，因此

(15.4.10) \(G'_s(x_1) = 0, \quad G''_s(x_1) > 0.\)

注意序列

(15.4.11) \(s < x_0 \le x_1 < x' \le x_2 < x_3.\)




我们现在可以采用矛盾论证，以证明不存在类似 \(x'\) 的点。我们回顾，对于 \(x > s\)，函数 \(G_s(x)\) 满足

\[
-\frac{1}{2}\sigma^2 G_s''(x) + \nu G_s'(x) + (\alpha + \lambda)G_s(x) - \lambda \int_0^\infty G_s(x-\xi)\mu(\xi)d\xi = l(x),
\]

其中

\[
l(x) = g(x) + cv + cx\tilde{\xi}.
\]

回顾 \(x_0 < 0\)，我们考虑两种可能性：

- 如果 \(x_2 < 0\)，则在点 \(x_1\) 和 \(x_2\) 处写出 (15.4.12)。我们有

\[
-\frac{1}{2}\sigma^2 G_s''(x_1) + \nu G_s'(x_1) + (\alpha + \lambda)G_s(x_1) - \lambda \int_0^\infty G_s(x_1-\xi)\mu(\xi)d\xi = l(x_1);
\]

\[
-\frac{1}{2}\sigma^2 G_s''(x_2) + \nu G_s'(x_2) + (\alpha + \lambda)G_s(x_2) - \lambda \int_0^\infty G_s(x_2-\xi)\mu(\xi)d\xi = l(x_2),
\]

并且我们使用

\[
G_s'(x_1) = G_s'(x_2) = 0;
\]

\[
G_s''(x_1) > 0, \quad G_s''(x_2) < 0;
\]

\[
G_s(x_2) - G_s(x_2-\xi) > 0, \quad G_s(x_1) - G_s(x_1-\xi) < 0;
\]

\[
l(x_1) > l(x_2),
\]

因此必然 \(G_s(x_1) > G_s(x_2)\)，这是不可能的。

- 如果 \(x_2 \ge 0\)，则在点 \(x_2\) 和 \(x_3\) 处写出 (15.4.12)。我们有

\[
-\frac{1}{2}\sigma^2 G_s''(x_3) + \nu G_s'(x_3) + (\alpha + \lambda)G_s(x_3) - \lambda \int_0^\infty G_s(x_3-\xi)\mu(\xi)d\xi = l(x_3)
\]

我们于是有

\[
G_s'(x_3) = G_s'(x_2) = 0
\]

\[
G_s''(x_3) > 0 \quad G_s''(x_2) < 0
\]

\[
G_s(x_2-\xi) - G_s(x_3-\xi) \le G_s(x_2) - G_s(x_3)
\]

\[
l(x_2) < l(x_3),
\]

由此可得 \(G_s(x_2) - G_s(x_3) < 0\)，这也是一个矛盾。因此不存在类似 \(x'\) 的点，这证明 (15.4.3) 得到满足，并完成了函数 \(G_s(x)\) 求解 Q.V.I. 的证明。

## 15.5. ERGODIC THEORY

### 15.5.1. 记号与模型.

我们现在令 \(\alpha \to 0\)。我们将用 \(\alpha\) 为函数建立索引。因此我们有准变分不等式

\[
\alpha G_\alpha(x) + \alpha G_\alpha(x) \le g_\alpha(x)
\]

\[
G_\alpha(x) \le K + \inf_{\eta > x} G_\alpha(\eta)
\]

\[
(\alpha G_\alpha(x) + \alpha G_\alpha(x) - g_\alpha(x)) \left( G_\alpha(x) - K + \inf_{\eta > x} G_\alpha(\eta) \right) = 0,
\]

其中

\[
g_\alpha(x) = f(x) + \alpha cx + cv + c\lambda\tilde{\xi},
\]

函数 \(G_\alpha(x)\) 由一个 \(s, S\) 策略得到。我们依次通过如下方式定义 \(\Gamma_\alpha(x)\)

\[
-\frac{1}{2}\sigma^2 \Gamma_\alpha''(x) + \nu \Gamma_\alpha'(x) + \lambda \Gamma_\alpha(x) - \lambda \int_0^x \Gamma_\alpha(x-\xi)\mu(\xi)d\xi + \alpha \Gamma_\alpha(x) = 0, \quad \forall x > 0
\]

\[
\Gamma_\alpha(0) = 1, \quad \Gamma_\alpha(+\infty) = 0
\]

对于 \(\pi < \bar{\pi}\)，令 \(\chi_\alpha(\pi)\) 为函数

\[
\chi_\alpha(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu \pi + \lambda - \lambda \hat{\mu}(\pi) + \alpha
\]

最大值在一点 \(\pi_0 < 0\) 处取得，该点不依赖于 \(\alpha\)。我们知道 \(\chi_\alpha(x)\) 有两个零点 \(\beta_{2\alpha} < \pi_0\) 和 \(0 < \beta_{1\alpha} < \bar{\pi}\)。我们接下来定义

\[
Q_\alpha(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \exp(\beta_{2\alpha} (\eta - x)) g'_\alpha(\eta) d\eta
\]

并且对于任意 \(s\) 和 \(x \ge s\)

\[
H_{\alpha,s}(x) = \int_s^x \Gamma_\alpha(x-\xi) Q_\alpha(\xi) d\xi
\]

函数 \(H_{\alpha,s}(x)\) 在 \(x < s\) 时由 0 扩展。我们然后定义函数 \(G_{\alpha,s}(x)\) 如下

\[
G'_{\alpha,s}(x) = H_{\alpha,s}(x) \quad G_{\alpha,s}(s) = \frac{\frac{\sigma^2}{2} Q_\alpha(s) + g_\alpha(s)}{\alpha}
\]

我们还需要

\[
\chi_{0\alpha}(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu \pi + \lambda + \alpha
\]

它有两个零点，\(\beta_{0\alpha} > 0\) 和 \(\bar{\beta}_{0\alpha} < 0\)。

我们知道

\[
\exp(-\beta_{0\alpha} x) \le \Gamma_\alpha(x) \le \exp(-\beta_{1\alpha} x)
\]

令 \(x_{0\alpha}\) 为 \(Q_\alpha(x)\) 的唯一零点。我们知道存在唯一的 \(s_\alpha < x_{0\alpha}\) 使得

\[
0 = K + \inf_{x \ge s_\alpha} \int_{s_\alpha}^x H_{\alpha,s_\alpha}(\xi) d\xi.
\]

函数

\[
G_\alpha(x) = G_{\alpha,s_\alpha}(x)
\]

是 Q.V.I (15.5.1) 的解。我们还定义数 \(S_\alpha > x_{0\alpha}\) 使得

\[
0 = K + \int_{s_\alpha}^{S_\alpha} H_{\alpha,s_\alpha}(\xi) d\xi \quad H_{\alpha,s_\alpha}(S_\alpha) = 0
\]

### 15.5.2. 极限过程.

我们现在可以令 \(\alpha \to 0\)。我们设

\[
\chi(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda - \lambda\hat{\mu}(\pi) = \lim_{\alpha \to 0} \chi_\alpha(\pi)
\]

\[
\chi_0(\pi) = -\frac{\sigma^2}{2}\pi^2 - \nu\pi + \lambda = \lim_{\alpha \to 0} \chi_{0\alpha}(\pi)
$$

根收敛

\[
\beta_{0\alpha} \to \beta_0 > 0 \quad \tilde{\beta}_{0\alpha} \to \tilde{\beta}_0 < 0
$$

\[
\beta_{2\alpha} \to \beta_2 < 0 \quad \beta_{1\alpha} \to \beta_1 = 0.
$$

第二个性质 \(\beta_1 = 0\) 而非一个严格正数，对 \(\Gamma_\alpha(x)\) 的极限有影响。\(\Gamma_\alpha(x)\) 在 \(x \to +\infty\) 时趋于 0 的性质无法保持，因此 \(\Gamma_\alpha(x)\) 的极限问题如下

\[
-\frac{1}{2}\sigma^2\Gamma''(x) + \nu\Gamma'(x) + \lambda\Gamma(x) - \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi = 0
$$

和

\[
\exp(-\beta_0 x) \le \Gamma(x) \le 1, \quad \Gamma(0) = 1, \quad \Gamma'(x) \text{ bounded},
$$

\[
\Gamma_\alpha(x) \uparrow \Gamma(x), \quad \text{as } \alpha \downarrow 0.
$$

定义

\[
\theta(x) = \lambda \int_0^x \Gamma(x-\xi)\mu(\xi)d\xi,
$$

那么我们可以写出公式

\[
\Gamma(x) = C \exp(-\beta_0 x) + \frac{2}{\sigma^2(\beta_0 - \tilde{\beta}_0)}
\left[ \int_0^x \exp(-\beta_0(x-\xi))\theta(\xi)d\xi + \int_x^{+\infty} \exp(\tilde{\beta}_0(\xi-x))\theta(\xi)d\xi \right],
$$

其中

\[
1 = C + \frac{2}{\sigma^2(\beta_0 - \tilde{\beta}_0)} \int_0^{+\infty} \exp(\beta_0 \xi) \theta(\xi)d\xi,
$$

还设定

\[
\theta_\alpha(x) = -\alpha \Gamma_\alpha(x) + \lambda \int_0^x \Gamma_\alpha(x-\xi)\mu(\xi)d\xi,
$$

我们也可以写出

\[
\Gamma_\alpha(x) = C_\alpha \exp(-\beta_0 x) + \frac{2}{\sigma^2(\beta_0 - \tilde{\beta}_0)}
\cdot \left[ \int_0^x \exp(-\beta_0(x-\xi))\theta_\alpha(\xi)d\xi + \int_x^{+\infty} \exp(\tilde{\beta}_0(\xi-x))\theta_\alpha(\xi)d\xi \right],
$$

其中

\[
1 = C_\alpha + \frac{2}{\sigma^2(\beta_0 - \tilde{\beta}_0)} \int_0^{+\infty} \exp(\beta_0 \xi) \theta_\alpha(\xi)d\xi.
$$

从这些公式以及 \(\Gamma_\alpha(x)\) 向 \(\Gamma(x)\) 的单调收敛来看，很容易验证 \(\Gamma_\alpha(x)\) 在 \(R^+\) 的任何紧集上一致收敛到 \(\Gamma(x)\)。同样，\(Q_\alpha(x) \to Q(x)\) 一致收敛，其中

\[
Q(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \exp(\beta_2 (\eta - x)) f'(\eta) d\eta = \frac{2}{\beta_2 \sigma^2} (p - (h + p) \exp(\beta_2 x^-))
$$

我们称

\[
x_0 = \lim_{\alpha \to 0} x_{0\alpha} \qquad \exp(-\beta_2 x_0) = \frac{p}{h + p}.
$$

对于任意 s，我们有

\[
H_{\alpha,s}(x) \to H_s(x),
$$

在 R 的紧集上一致收敛，其中

\[
H_s(x) = \int_s^x \Gamma(x - \xi) Q(\xi) d\xi.
$$

现在考虑函数

\[
\gamma_\alpha(s) = \inf_{x \ge s} \int_s^x H_{\alpha,s}(\xi) d\xi = \int_s^{S_\alpha(s)} H_{\alpha,s}(\xi) d\xi.
$$

我们首先检查

\[
0 > s > \bar{s} \Rightarrow \limsup_{\alpha \to 0} S_\alpha(s) \le B(\bar{s}),
$$

其中 \(B(\bar{s}) > 0\) 是某个下面将明确给出的界。

不失一般性，我们可以假设 \(S_\alpha(s) > 0\)。那么我们有 \(H_{\alpha,s}(S_\alpha(s)) = 0\)。因此

\[
\int_s^{x_{0\alpha}} \Gamma_\alpha(S_\alpha(s) - \xi) Q_\alpha(\xi) d\xi = \int_{x_{0\alpha}}^{S_\alpha(s)} \Gamma_\alpha(S_\alpha(s) - \xi) Q_\alpha(\xi) d\xi,
$$

因此

\[
\int_0^{S_\alpha(s)} \Gamma_\alpha(S_\alpha(s) - \xi) Q_\alpha(\xi) d\xi \le - \int_s^{x_{0\alpha}} \Gamma_\alpha(S_\alpha(s) - \xi) Q_\alpha(\xi) d\xi,
$$

使用

\[
Q_\alpha(\xi) = - \frac{2}{\beta_{2\alpha} \sigma^2} (h + \alpha c), \quad \xi \ge 0 ; \quad Q_\alpha(\xi) \ge \frac{2}{\beta_{2\alpha} \sigma^2} (p - \alpha c),
$$

我们推导出

\[
(h + \alpha c) \int_0^{S_\alpha(s)} \Gamma_\alpha(\xi) d\xi \le (p - \alpha c) \int_s^{x_{0\alpha}} \Gamma_\alpha(S_\alpha(s) - \xi) d\xi \le (p - \alpha c)(x_{0\alpha} - s)
$$

令 \(M > 0\) 并设定 \(S_\alpha^M(s) = \min(M, S_\alpha(s))\)。我们有

\[
(h + \alpha c) \int_0^{S_\alpha^M(s)} \Gamma_\alpha(\xi) d\xi \le (p - \alpha c)(x_{0\alpha} - \bar{s}).
$$

令 \(S^M(s) = \limsup_{\alpha \to 0} S_\alpha^M(s)\)。通过对前面的不等式取上极限，我们得到

\[
h \int_0^{S^M(s)} \Gamma(\xi) d\xi \le p(x_0 - \bar{s}).
$$



然而我们具有性质

$$ \int_0^{ +\infty } \Gamma (\xi ) d\xi = +\infty . $$

确实，若考虑 \(\pi < 0\)

$$ \hat{\Gamma} (\pi ) = \int_0^{ +\infty } \exp \xi \pi \Gamma (\xi ) d\xi , $$

由方程 (15.5.14) 推得

$$ \hat{\Gamma} (\pi ) = \frac{\sigma ^2 \pi - \beta _2}{2 - \chi (\pi )}. $$

当 \(\pi \uparrow 0\) 时，我们知道 \(\chi (\pi ) \to 0\)，故 \(\hat{\Gamma} (\pi ) \uparrow +\infty\)，这蕴含 (15.5.17)。我们可以定义唯一的 \(B(\bar{s})\) 使得

$$ \int_0^{B(\bar{s})} \Gamma (\xi ) d\xi = \frac{p(x_0 - \bar{s})}{h}, $$

故

$$ S^M(\bar{s}) \le B(\bar{s}), $$

并令 \(M \uparrow +\infty\)，我们得到性质 (15.5.16)。

取 \(s < x_0\)。对于足够小的 \(\alpha\)，我们还可假设 \(s < x_{0\alpha}\)。因此 \(H_\alpha (s, S_\alpha (s)) = 0\)。由估计 (15.5.16)，对于足够小的 \(\alpha\)，我们可假设 \(S_\alpha (s)\) 被 \(2B(\bar{s})\) 所界定。通过提取满足 \(S_\alpha (s) \to S^*\) 的子序列，我们容易得到 \(H_1(S^*) = 0\) 且

$$ \gamma_\alpha (s) \to \gamma (s) = \inf_{\eta > s} \int_s^\eta H_s (\xi ) d\xi = \int_s^{S^*} H_s (\xi ) d\xi $$

我们再次令 \(S(s)\) 为使得 \(H_1(S(s)) = 0\) 的第一个点。

我们在上面，定理 15.1 的证明中已经表明

$$ \gamma'_\alpha (s) \ge - \frac{Q_\alpha (s_1)}{\beta_{0\alpha }} (1 - \exp -\beta_{0\alpha } (x_{0\alpha } - s_1)) > 0, $$

只要 \(s < s_1 < x_{0\alpha}\)。固定 \(s_1 < x_0\)。对于足够小的 \(\alpha\)，我们可假设 \(s_1 < x_{0\alpha}\)，且对 \(s < s_1\)

$$ \gamma'_\alpha (s) \ge - \frac{Q(s_1)}{2\beta _0} (1 - \exp -\beta _0 (x_0 - s_1)) = a(s_1) > 0, $$

故

$$ \gamma_\alpha (s_1) - \gamma_\alpha (s) \ge (s_1 - s)a(s_1). $$

由于 \(\gamma_\alpha (s_1) < 0\)，事实上

$$ -\gamma_\alpha (s) \ge (s_1 - s)a(s_1). $$

现在考虑 \(s_\alpha\)。要么 \(s_\alpha \ge s_1\)，要么 \(s_\alpha < s_1\)，在此情况下由上述不等式

$$ K \ge (s_1 - s_\alpha )a(s_1). $$

因此在所有情况下

(15.5.18) 
$$ s_\alpha \ge s_1 - \frac{K}{a(s_1)} = \bar{s}, $$

但随后由 (15.5.16) 我们还可断言

(15.5.19) 
$$ S_\alpha = S_\alpha (s_\alpha ) \le 2B(\bar{s}), $$

对于足够小的 \(\alpha\)。因此我们可以提取一个子序列使得 \(s_\alpha \to s, S_\alpha \to S\)。另外 \(\gamma(s) = -K\)。然而，出于与 \(s_\alpha\) 相同的理由，存在唯一的 \(s\) 满足此关系。故整个序列 \(s_\alpha \to s\)。定义

(15.5.20) 
$$ \rho_\alpha = \alpha G_{\sigma_\alpha}(s_\alpha) \to \rho = \frac{\sigma^2}{2} Q(s) + f(s) + c\nu + c\lambda \tilde{\xi}, $$

我们可以设

$$ \tilde{G}_\alpha(x) = G_\alpha(x) - \frac{\rho_\alpha}{\alpha}, $$

并声称以下遍历结果

**定理 15.3。** 我们假设 (15.2.4)。函数 \(G_\alpha(x)\)，（及其导数）在紧集上一致收敛到 \(G(x)\)，（及其导数），且对 \(G(x), \rho\) 是 Q.V.I. 的解。

(15.5.21) 
$$ \begin{aligned} AG(x) + \rho \le l(x) \\ G(x) \le K + \inf_{\eta > x} G(\eta) \\ (AG(x) + \rho - l(x))(G(x) - K + \inf_{\eta > x} G(\eta)) = 0, \end{aligned} $$

其中

\(l(x) = f(x) + cv + c\lambda \tilde{\xi}.\)

函数 \(G(x)\) 是 \(C^1\)，其导数具有线性增长。它由一个 \(s, S\) 策略给出

(15.5.22) 
$$ \begin{aligned} AG(x) + \rho = l(x), \quad x > s \\ G(x) = K + \inf_{\eta > x} G(\eta), \quad x \le s \end{aligned} $$

## 15.6. 概率诠释

本节将发展前几节 Q.V.I 方法的概率对偶。我们将 [32] 的方法扩展到扩散和泊松情况。其思想是在 \(s, S\) 策略类中进行优化，并表明我们以这种方式求解 Q.V.I。

### 15.6.1. 带有 \(s, S\) 控制的过程研究

设 \(s < S\) 为两个给定数。我们将定义在 \(s, S\) 策略下、初始值为 \(x\) 的过程 \(y_x^{s,S}(t)\)。回顾需求

$$ D(t) = \nu t + N(t) + \sigma \omega(t), $$

在区间 \(0, t\) 中我们定义

$$ \tau_x^s = \inf \{t \ge 0 \mid x - D(t) \le s\}, $$

且若 \(x > s\)

$$ y_x^{s,S}(t) = x - D(t), \forall t < \tau_x^s. $$

接下来设

$$ y_x^{s,S}(\tau_x^s) = S. $$

设

$$ \tau_{x,n}^{s,S} = \tau_x^s, $$

并假设我们已定义 \(\tau_{x,n}^{s,S}\) 且 \(y_x^{s,S}(\tau_{x,n}^{s,S}) = S\)。我们接着定义

$$ \tau_{x,n+1}^{s,S} = \tau_{x,n}^{s,S} + \inf \{t \ge 0 \mid S - D(\tau_{x,n}^{s,S} + t) + D(\tau_{x,n}^{s,S}) \le s\}. $$

显然 \(\tau_{x,n+1}^{s,S} > \tau_{x,n}^{s,S}\)。我们接下来设

$$ y_x^{s,S}(\tau_{x,n}^{s,S} + t) = S - D(\tau_{x,n}^{s,S} + t) + D(\tau_{x,n}^{s,S}), \forall t < \tau_{x,n+1}^{s,S} - \tau_{x,n}^{s,S}, $$

并再次 \(y_x^{s,S}(\tau_{x,n+1}^{s,S}) = S\)。我们以这种方式定义了由 s, S 策略控制的过程：它在时刻 \(\tau_{x,n}^{s,S}\) 处有跳跃，即冲击时刻，在时刻 \(\tau_{x,n}^{s,S}\) 处的冲击大小为 \(S - y_x^{s,S}(\tau_{x,n}^{s,S}, 0)\)。注意该冲击大于或等于 \(S - s\)。过程 \(y_x^{s,S}(t)\) 还由于需求的复合泊松部分而有跳跃。这是一个马可夫过程，我们将描述其无穷小生成元。

回顾，无穷小生成元是定义在函数 \(\varphi(x)\) 集合上的线性算子，使得极限

$$ \lim_{\epsilon \to 0} \frac{E\varphi(y_x^{s,S}(\epsilon)) - \varphi(x)}{\epsilon} = \mathcal{A}^{s,S}\varphi(x), $$

存在。

由于

$$ y_x^{s,S}(s) = y_S^{s,S}(\epsilon), \forall x \le s, $$

我们需要有

(15.6.1) \(\quad \varphi(x) = \varphi(S), \forall x \le s.\)

执行与第 15.2 节中相同的近似推理，我们容易得到

$$ \mathcal{A}^{s,S}\varphi(x) = \begin{cases} -A\varphi(x), & \text{if } x > s \\ -A\varphi(s), & \text{if } x \le s \end{cases} $$

其中 \(A\) 是方程 (17.2.4) 中定义的二阶微分算子。其定义域是一阶和二阶导数有界且满足 (15.6.1) 的有界函数集合。只需假设函数 \(\varphi\) 和 \(A\varphi\) 有界且 (15.6.1) 满足即可。尽管我们提到 \(\mathcal{A}\) 的定义域，但谈论 \(A\) 的定义域会更方便。

### 15.6.2. 不变量度

我们将表明以下结论

**定理 15.4。** 过程 \(y_x^{s,S}(t)\) 具有如下定义的唯一不变量度

$$ m^{s,S}(x) = \frac{\tilde{m}^{s,S}(x)}{\int_s^{+\infty} \tilde{m}^{s,S}(\xi) d\xi}, $$

其中

(15.6.2) \(\quad \tilde{m}^{s,S}(x) = \begin{cases} 0, & \text{if } x \le s \\ \exp \beta_2 x \int_x^S \exp -\beta_2 \xi \Gamma(S-\xi) d\xi, & \text{if } s \le x \le S \\ \exp \beta_2 x \int_s^S \exp -\beta_2 \xi \Gamma(S-\xi) d\xi, & \text{if } S \le x \end{cases}\)

其中 \(\Gamma(x)\) 是下式的唯一解

(15.6.3) \(\quad -\frac{\sigma^2}{2} \Gamma''(x) + \mu \Gamma'(x) + \lambda \Gamma(x) - \lambda \int_0^x \Gamma(x-\xi) \mu(\xi) d\xi = 0\)

\(\Gamma(0) = 1 \quad 0 \le \Gamma(x) \le 1\)

且 \(\beta_2\) 是下式的唯一负根

\(-\frac{\sigma^2}{2} \beta_2^2 - \nu \beta_2 - \lambda - \lambda \hat{\mu}(\beta_2) = 0.\)

此外，对任何有界的 \(\varphi(x)\)

(15.6.4) 
$$ \Phi_\alpha^{s,S}(x) = E \int_0^{+\infty} \exp - \alpha t \varphi(y_x^{s,S}(t))dt, $$

满足

(15.6.5) 
$$ \alpha \Phi_\alpha^{s,S}(x) \to \int_s^{+\infty} \varphi(x) m^{s,S}(x) dx. $$

证明。我们注意到公式 (15.6.2) 中的 \(\tilde{m}^{s,S}(x)\) 是连续的但不是 \(C^1\)。导数在 \(S\) 处不连续。我们开始证明 \(m^{s,S}(x)\) 是一个不变量度且是唯一的，它是连续的且在 \(S\) 处除外是 \(C^1\)。我们首先证明 \(m^{s,S}(x)\) 必须在区间 \((-\infty, s)\) 上消失。确实，不变量度必须满足

$$ \int m^{s,S}(x)\varphi(x)dx = \int m^{s,S}(x)E\varphi(y_x^{s,S}(\varepsilon))dx, \forall \varepsilon $$

取一个在 \(s, +\infty\) 上消失的测试函数 \(\varphi(x)\)。由前述关系得到

$$ \int_{-\infty}^s m^{s,S}(x)\varphi(x)dx = E\varphi(y_S^{s,S}(\varepsilon)) \int_{-\infty}^s m^{s,S}(x)dx + \int_s^{+\infty} m^{s,S}(x)E\varphi(y_x^{s,S}(\varepsilon))dx $$

令右边 \(\epsilon \to 0\)，我们得到

$$ \varphi(S) \int_{-\infty}^s m^{s,S}(x)dx + \int_s^{+\infty} m^{s,S}(x)\varphi(x)dx = 0, $$

由 \(\varphi\) 的选取得出。现在取 \(\varphi(x)\) 在无穷小生成元的定义域中。不变量度必须满足

$$ \int_s^{+\infty} m^{s,S}(x)A\varphi(x)dx = 0. $$

为简化记号，我们将 \(m(x)\) 写作 \(m^{s,S}(x)\)。我们回顾 \(m\) 的正则性性质并进行分部积分。我们得到

$$
\begin{aligned}
&-\frac{\sigma^2}{2} [\varphi(S)(m'(S+0) - m'(S-0)) + \varphi(s)m'(s)] \\
&\quad -\lambda \varphi(S) \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx + \int_s^{+\infty} \varphi(x) \left( \frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) \right) dx \\
&\quad -\lambda \int_s^{+\infty} m(x) \left( \int_0^{x-s} \varphi(x - \xi) \mu(\xi)d\xi \right) dx = 0.
\end{aligned}
$$

利用 \(\varphi\) 满足 \(\varphi(s) = \varphi(S)\) 并整理后，我们得到

$$
\begin{aligned}
&-\varphi(S) \left[ \frac{\sigma^2}{2} (m'(S+0) - m'(S-0) + m'(s)) \right. \\
&\quad \left. + \lambda \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx \right] + \int_s^{+\infty} \varphi(x) \left( \frac{\sigma^2}{2}m''(x) - \nu m'(x) \right. \\
&\quad \left. + \lambda m(x) - \lambda \int_0^{+\infty} m(x + \xi) \mu(\xi)d\xi \right) dx = 0.
\end{aligned}



这意味着

\(-\frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) - \lambda \int_0^{+\infty} m(x+\xi)\mu(\xi)d\xi = 0, x \in (s, +\infty)\)
\(m(x) = 0, x \le s \quad m'' \text{ 在 } S \text{ 处不连续}\)

并且我们必须有 \(m \ge 0\) 并满足归一化性质 \(\int_s^{+\infty} m(x)dx = 1\)。请注意，条件

\(\frac{\sigma^2}{2}(m'(S+0) - m'(S-0) + m'(S) + \lambda) \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx = 0,\)

这不是一个额外条件。它由(15.6.6)和归一化性质推导而来。因此，(15.6.6)和归一化性质构成了不变量度的方程。让我们证明(15.6.2)是一个解且是唯一的。我们可以验证\(\exp \beta_2 x\)满足积分微分方程(15.6.6)。当\(x \to +\infty\)时，它趋于0。它不能是\((s, +\infty)\)上的解，但如果我们在\(S\)处强制其值等于\(\exp \beta_2 S\)，那么它就是\((S, +\infty)\)上的唯一解。请注意，强制归一化条件或某点的值是等价的。因此，我们可以固定\(S\)处的值等于\(\exp \beta_2 S\)。那么，(15.6.6)在\((s, +\infty)\)上为\(C^2\)且在无穷处消失的解只能有一个。这由最大原理考虑得出。

我们可以在\((s, S)\)上将方程写成如下形式

\(-\frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) - \lambda \int_0^{S-x} m(x+\xi)\mu(\xi)d\xi\)
\(= \lambda \exp \beta_2 x \int_{S-x}^{+\infty} \exp \beta_2 \xi \mu(\xi)d\xi, \quad s < x < S\)
\(m(s) = 0; \quad m(S) = \exp \beta_2 S\)

根据最大原理考虑，该方程只能有一个解。如果我们进行未知函数的变换。

\(m(x) = v(x) \exp \beta_2 x,\)

那么我们得到关于\(v(x)\)的方程，即

\(-\frac{\sigma^2}{2}v''(x) - (\nu + \beta_2 \sigma^2)v'(x) + \lambda v(x)\tilde{\mu}(\beta_2)\)
\(-\lambda \int_0^{S-x} v(x+\xi) \exp \beta_2 \xi \mu(\xi)d\xi = \lambda \int_{S-x}^{+\infty} \exp \beta_2 \xi \mu(\xi)d\xi,\)
\(v(s) = 0, \quad v(S) = 1\)

考虑\(w(x) = v'(x)\)，并考虑到\(v(S) = 1\)的值，我们得到

\(-\frac{\sigma^2}{2}w''(x) - (\nu + \beta_2 \sigma^2)w'(x) + \lambda w(x)\tilde{\mu}(\beta_2) - \lambda \int_0^{S-x} w(x+\xi) \exp \beta_2 \xi \mu(\xi)d\xi = 0,\)

如果我们写

\(w(x) = \exp -\beta_2 x z(S-x),\)

我们看到\(z(x) = \Gamma(x)\)。汇总结果，我们得到\(\tilde{m}^{n,s}(x)\)是(15.6.6)的一个解，所有条件均满足，当然在\(S\)处的值不同。因此，\(m^{n,s}(x)\)是满足正则性性质、边界条件和归一化性质的唯一不变量度。

现在让我们证明(15.6.5)。我们有

\(\Phi_\alpha^{*,S}(x) = E \int_t^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(+ \sum_{n=1}^{n+1} E \int_{\tau_{x,n}^{S,S}}^{\tau_{x,n+1}^{S,S}} \exp - \alpha t \varphi(y_x^S(S)(t)) dt.\)

然后利用条件化和独立性性质，对于\(n \ge 1\)

\(E \int_{\tau_{x,n}^{S,S}}^{\tau_{x,n+1}^{S,S}} \exp - \alpha t \varphi(y_x^S(S)(t)) dt\)
\(= E \exp - \alpha \tau_{x,n}^{S,S} \int_0^{\tau_{x,n+1}^{S,S} - \tau_{x,n}^{S,S}} \exp - \alpha t \varphi(y_x^S(\tau_{x,n}^{S,S} + t)) dt\)
\(= E \exp - \alpha \tau_{x,n}^{S,S} E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(= E \exp - \alpha \tau_S^x (E \exp - \alpha \tau_S^x)^{n-1} E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt.\)

我们得到公式

(15.6.8) \(\Phi_\alpha^{*,S}(x) = E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt\)
\(+ E \exp - \alpha \tau_S^x \frac{E \int_0^{\tau_S^x} \exp - \alpha t \varphi(y_S^{*,S}(t)) dt}{1 - E \exp - \alpha \tau_S^x}.\)

然后

(15.6.9) \(\alpha \Phi_\alpha^{*,S}(x) \rightarrow \frac{E \int_0^{\tau_S^x} \varphi(y_S^{*,S}(t)) dt}{E \tau_S^x}.\)

如果我们定义

\(\zeta_s(x; \varphi) = E \int_0^{\tau_S^x} \varphi(y_S^{*,S}(t)) dt,\)

那么我们已经证明了

\(\alpha \Phi_\alpha^{*,S}(x) \rightarrow \frac{\zeta_S(S; \varphi)}{\zeta_S(S; 1)}.\)

然而，\(\zeta_s(x; \varphi)\)是以下问题的解

(15.6.10) \(A \zeta_s(x) = \varphi(x) \quad x > s\)
\(\zeta_s(x) = 0 \quad x \le s\)

并且它具有显式解

(15.6.11) \(\zeta_s(x; \varphi) = \frac{2}{\sigma^2 s} \int_s^x \Gamma(x - \xi) \int_\xi^{+\infty} \exp \beta_2(\eta - \xi) \varphi(\eta) d\eta.\)

经过一些简单的积分变换，我们推导出

\(\zeta_S(S; \varphi) = \frac{2}{\sigma^2 s} \int_S^S \varphi(\eta) \exp \beta_2 \eta \left( \int_S^\eta \exp - \beta_2 \xi \Gamma(S - \xi) d\xi \right) d\eta\)
\(+ \frac{2}{\sigma^2} \int_S^{+\infty} \varphi(\eta) \exp \beta_2 \eta \left( \int_S^\eta \exp - \beta_2 \xi \Gamma(S - \xi) d\xi \right) d\eta\)

并且我们按预期识别出

$$\zeta_S(S; \varphi) = \frac{2}{\sigma^2} \int_s^{+\infty} \varphi(x)\bar{m}^{s,S}(x)dx.$$

结果得证。

我们现在介绍一个有用的结果

## 引理 15.2. 对于\(A\)定义域中的任何\(z\)，我们有等式

$$(15.6.12) \quad \int_s^{+\infty} m(x)z(x)Az(x)dx = \frac{1}{2} \int_s^{+\infty} \sigma^2 m z'^2 dx + \frac{\lambda}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(\xi) dx d\xi .$$

证明。我们考虑左边的量。由于我们将进行两次分部积分，必须小心\(m'\)在\(S\)处不连续。另一方面，\(z'\)在\(S\)处是连续的。

进行一次分部积分后，我们可以写成

$$\int_s^{+\infty} m(x)z(x)Az(x)dx = \frac{1}{2} \int_s^S \sigma^2 m z'^2 dx + \int_s^S zz' \left( \frac{\sigma^2}{2} m' + \nu m \right) dx + \lambda \int_s^{+\infty} \int_0^{+\infty} m(x)z(x)(z(x) - z(x - \xi)) \mu(\xi) dx d\xi .$$

注意到

$$zz' = \frac{1}{2}(z^2)' ,$$

我们可以进行第二次分部积分，从而得到

$$\int_s^S zz' \left( \frac{\sigma^2}{2} m' + \nu m \right) dx = -\frac{1}{2} \int_s^{+\infty} z^2 \left( \frac{\sigma^2}{2} m' + \nu m \right) dx + \frac{\sigma^2}{4} z^2(S)(m'(S-0) - m'(S+0) - m'(s)) .$$

下一步是考虑

$$\int_s^{+\infty} \int_0^{+\infty} m(x)z(x)(z(x) - z(x - \xi)) \mu(\xi) dx d\xi = \frac{1}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(\xi) dx d\xi + \frac{1}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(z^2(x) - z^2(x - \xi)) \mu(\xi) dx d\xi .$$

我们还使用

$$\int_s^{+\infty} \int_0^{+\infty} m(x)z^2(x - \xi) \mu(\xi) dx d\xi = \int_s^{+\infty} \int_0^{+\infty} m(x + \xi) z^2(x) \mu(\xi) dx d\xi + z^2(S) \int_s^{+\infty} \int_0^{+\infty} m(x + \xi) \mu(\xi) dx d\xi .$$

汇总结果并利用不变量度的方程，参见(15.6.6)、(15.6.7)，我们得到许多简化。最终我们得到(15.6.14)

在(15.6.4)中定义的函数\(\Phi_\alpha^{s,S}(x)\)（我们省略记号\(s,S\)）是以下方程的解

$$
A\Phi_\alpha(x) + \alpha\Phi_\alpha(x) = \varphi(x), \quad \forall x > s
\Phi_\alpha(x) = \Phi_\alpha(S), \quad \forall x \le s
$$

解\(\Phi_\alpha(x)\)属于\(A\)的定义域。证明稠密性结果将很有用。

## 引理 15.3. 对于任何有界函数\(\varphi\)，我们可以构造一个属于\(A\)定义域的序列\(\varphi_\epsilon\)，使得

\(\|\varphi_\epsilon\| = \sup_x |\varphi_\epsilon(x)| \le \|\varphi\|\)

(15.6.13) \(\int_s^{+\infty} m(x)|\varphi_\epsilon(x) - \varphi(x)|^2 dx \to 0, \quad \text{当 } \epsilon \to 0\)

证明。我们考虑以下问题的解

$$
A\varphi_\epsilon(x) + \frac{\varphi_\epsilon(x)}{\epsilon} = \frac{\varphi(x)}{\epsilon}, \quad \forall x > s
\varphi_\epsilon(x) = \varphi_\epsilon(S), \quad \forall x \le s
$$

令

\(\tilde{\varphi}_\epsilon(x) = \varphi_\epsilon(x) - \|\varphi\|,\)

那么

$$
A\tilde{\varphi}_\epsilon(x) + \frac{\tilde{\varphi}_\epsilon(x) - \|\varphi\|}{\epsilon} = \frac{\varphi(x) - \|\varphi\|}{\epsilon}, \quad \forall x > s
\tilde{\varphi}_\epsilon(x) = \tilde{\varphi}_\epsilon(S), \quad \forall x \le s
$$

因此\(\tilde{\varphi}_\epsilon(x) \le 0\)。同样地

\(\varphi_\epsilon(x) + \|\varphi\| \ge 0,\)

并且第一个性质(15.6.22)随之得出。根据引理15.2，我们可以断言

$$
\frac{1}{2} \int_s^{+\infty} \sigma^2 m(\varphi_\epsilon)^2 dx + \frac{\lambda}{2} \int_s^{+\infty} \int_0^{+\infty} m(x)(\varphi_\epsilon(x) - \varphi_\epsilon(x - \xi))^2 \mu(\xi) dx d\xi
+ \int_s^{+\infty} m \frac{\varphi_\epsilon^2}{\epsilon} dx = \int_s^{+\infty} m \frac{\varphi \varphi_\epsilon}{\epsilon} dx.
$$

由此可得

\(\int_s^{+\infty} m \varphi_\epsilon^2 dx \le \int_s^{+\infty} m \varphi_\epsilon \varphi dx.\)

考虑希尔伯特空间\(L_m^2(R)\)，由函数\(z\)组成，使得

\(\int_s^{+\infty} m z^2 dx < +\infty.\)

序列\(\varphi_\epsilon\)在此希尔伯特空间中保持有界。如果我们考虑一个收敛于\(\varphi^*\)的弱收敛子序列，那么

$$
\int_s^{+\infty} m(\varphi^*)^2 dx \le \lim \sup \int_s^{+\infty} m \varphi_\epsilon^2 dx \le \lim \int_s^{+\infty} m \varphi_\epsilon \varphi dx = \int_s^{+\infty} m \varphi^* \varphi dx.
$$

现在

$$
\int_s^{+\infty} m(\varphi_\epsilon - \varphi^*)^2 dx \le \int_s^{+\infty} m \varphi_\epsilon \varphi dx + \int_s^{+\infty} m(\varphi^*)^2 dx - 2 \int_s^{+\infty} m \varphi_\epsilon \varphi^* dx,



故

\[
\limsup \int_s^{+\infty} m(\varphi_s - \varphi^o)^2 dx \le \int_s^{+\infty} m \varphi^o \varphi dx - \int_s^{+\infty} m(\varphi^o)^2 dx.
\]

注意到 \(\sqrt{\epsilon}\varphi_\epsilon\) 在 \(L^2_n(R)\) 中保持有界，由 \(\varphi_\epsilon\) 的方程可知

\[
\epsilon \int_s^{+\infty} A \varphi_\epsilon z dx \to 0, \forall z \text{ 在 } (s, +\infty) \text{ 中光滑且具有紧支集},
\]

因此我们立即推断出 \(\varphi^o = \varphi\)，并由 (15.6.14) 得到性质 (15.6.22)，这完成了证明。

## 15.6.3. 遍历性.

定理 15.4 的结果，虽然足以研究遍历控制和 Bellman 方程的极限，如我们在下一节将看到的，但并未证明完全遍历性。为了完备，我们需要证明

### 定理 15.5. 我们有性质

\[
E \varphi(y_s^{x,S}(t)) \to \int_s^{+\infty} E \varphi(\xi) m^{s,S}(d\xi), \text{ 当 } t \to +\infty, \forall x, \forall \varphi \text{ 有界.}
\]

### 证明.

我们将利用以下事实

\[
z^{s,S}(x,t) = E \varphi(y_s^{x,S}(t)),
\]

是柯西问题的解

(15.6.16)
\[
\begin{align*}
\frac{\partial z}{\partial t} + Az &= 0, \quad x > s \\
z(x,t) &= z(S,t), \quad x \le s, t > 0 \\
z(x,0) &= \varphi(x)
\end{align*}
\]

我们进行估计。我们首先推导一个能量等式。通过用 \(mz\) 对 (15.6.16) 进行试验并利用引理 15.5.2，我们可以得出

(15.6.17)
\[
\begin{align*}
\frac{1}{2} \frac{d}{dt} \int_s^{+\infty} m(x) z^2(x,t) dx + \frac{1}{2} \int_s^{+\infty} \sigma^2 m \left( \frac{\partial z}{\partial x} \right)^2 dx \\
+ \frac{\lambda}{2} \int_s^{+\infty} \int_0^{+\infty} m(x) (z(x) - z(x - \xi))^2 \mu(d\xi) dx d\xi = 0
\end{align*}
\]

我们推导出以下估计

(15.6.18)
\[
\int_0^{+\infty} \int_s^{+\infty} \sigma^2 m \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx dt \le \int_s^{+\infty} m(x) \varphi^2(x) dx
\]

(15.6.19)
\[
\lambda \int_0^{+\infty} \int_s^{+\infty} \int_0^{+\infty} m(x) (z(x) - z(x - \xi))^2 \mu(d\xi) dx d\xi dt \le \int_s^{+\infty} m(x) \varphi^2(x) dx.
\]

另外

(15.6.20)
\[
\int_s^{+\infty} m(x) z^2(x,t) dx \le \int_s^{+\infty} m(x) \varphi^2(x) dx, \forall t.
\]

该不等式意味着，不失一般性我们可以假设 \(\varphi\) 在 \(A\) 的定义域内。确实，考虑到引理 15.3 中定义的近似 \(\varphi_\epsilon\)，并记 \(z_c(x,t)\) 为相应的柯西问题解，由估计 (15.6.20) 推出

\[
\int_s^{+\infty} m(x)(z_c(x,t) - z(x,t))^2 dx \le \int_s^{+\infty} m(x)(\varphi_c - \varphi)^2 dx.
\]

假设我们已经证明了

\[
z_c(x,t) \to \int_s^{+\infty} m(x)\varphi_c(x) dx, \quad \text{当 } t \to +\infty, \forall c > 0
\]

然后记

\[
\bar{\varphi} = \int_s^{+\infty} m(x)\varphi(x) dx, \quad \bar{\varphi}_c = \int_s^{+\infty} m(x)\varphi_c(x) dx
\]

\[
\begin{aligned}
\int_s^{+\infty} m(x)(z(x,t) - \bar{\varphi})^2 dx &\le 3 \left[ \int_s^{+\infty} m(x)(z_c(x,t) - z(x,t))^2 dx + \int_s^{+\infty} m(x)(z_c(x,t) - \bar{\varphi}_c)^2 dx + (\bar{\varphi}_c - \bar{\varphi})^2 \right] \\
&\le 3 \left[ \int_s^{+\infty} m(x)(\varphi_c - \varphi)^2(x) dx + \int_s^{+\infty} m(x)(z_c(x,t) - \bar{\varphi}_c)^2 dx + (\bar{\varphi}_c - \bar{\varphi})^2 \right]
\end{aligned}
\]

但随后

\[
\limsup_{t \to +\infty} \int_s^{+\infty} m(x)(z(x,t) - \bar{\varphi})^2 dx \le 3 \left[ \int_s^{+\infty} m(x)(\varphi_c - \varphi)^2(x) dx + (\bar{\varphi}_c - \bar{\varphi})^2 \right],
\]

并令 \(\epsilon \to 0\) 我们得到

\[
\int_s^{+\infty} m(x)(z(x,t) - \bar{\varphi})^2 dx \to 0, \text{ 当 } t \to +\infty
\]

我们还推出

\[
z(x,t) \to \bar{\varphi} \quad \text{几乎处处 } x > s
\]

因此我们假设 \(\varphi\) 属于 \(A\) 的定义域。我们可以进一步得到估计。

我们定义函数

\[
u(x,t) = \frac{\partial z}{\partial t}(x,t),
\]

它是下式的解

(15.6.21)
\[
\begin{aligned}
\frac{\partial u}{\partial t} + Au &= 0, \quad x > s \\
u(x,t) &= u(S,t), \quad x \le s, t > 0 \\
u(x,0) &= -A\varphi
\end{aligned}
\]

对于 \(z\) 我们可以写出

(15.6.22)
\[
\int_0^{+\infty} \int_s^{+\infty} \sigma^2 m \left( \frac{\partial u}{\partial x} \right)^2 (x,t) dx dt \le \int_s^{+\infty} m(x)(A\varphi)^2(x) dx
\]

(15.6.23)
\[
\begin{aligned}
\lambda \int_0^{+\infty} \int_s^{+\infty} \int_0^{+\infty} m(x)(u(x) - u(x-\xi))^2 \mu(d\xi) dx dt \le \int_s^{+\infty} m(x)(A\varphi)^2(x) dx
\end{aligned}
\]

(15.6.24)
\[
\int_s^{+\infty} m(x)u^2(x,t)dx \le \int_s^{+\infty} m(x)(A\varphi)^2(x)dx, \forall t.
\]

特别是，我们已经证明了

\[
\int_0^{+\infty} \int_s^{+\infty} m \left( \frac{\partial^2 z}{\partial x \partial t} \right)^2 (x,t) dx dt \le \frac{1}{\sigma^2} \int_s^{+\infty} m(x)(A\varphi)^2(x)dx
\]

注意到

\[
\int_s^{+\infty} m \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx = \int_s^{+\infty} m(\varphi')^2(x)dx + 2 \int_0^t \int_s^{+\infty} m \frac{\partial z}{\partial x}(x, \tau) \frac{\partial^2 z}{\partial x \partial t}(x, \tau) dx d\tau
\]

右边在 \(t \to +\infty\) 时有极限，得益于上述估计。所以 \(\int_s^{+\infty} m \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx\) 在 \(t \to +\infty\) 时有极限。这个极限必须为 0，得益于估计 (15.6.18)。回顾 \(z\) 是有界的，我们可以断言，对于 \([s, +\infty)\) 的任何紧子集，我们可以找到 \(z(x,t)\) 的一个一致收敛子序列。极限必然是一个常数，并且由于

\[
\int_s^{+\infty} m(x)z(x,t)dx = \int_s^{+\infty} m(x)\varphi(x)dx,
\]

这个极限必然是 \(\int_s^{+\infty} m(x)\varphi(x)dx\)。由极限的唯一性，整个序列在任何紧集上一致收敛。所以我们已经得到了 \(\varphi\) 在 \(A\) 的定义域内的结果，也通过上述近似得到了一般结果。然而我们只在几乎处处 \(x\) 上证明了结果 (15.6.15)。我们现在想证明它对任何初始值 \(x\) 都成立。我们需要两个重要的中间结果。第一个是

(15.6.25)
\[
z(x,t) \text{ 在 } x \text{ 中连续}, \quad \forall t > 0
\]

这个性质允许我们不失一般性地假设 \(\varphi(x)\) 连续且有界。确实，显然

\[
\lim_{t \to +\infty} z(x,t) = \lim_{t \to +\infty} z(x,t+1),
\]

并且 \(z(x, t + 1)\) 满足与 \(z(x,t)\) 相同的方程，除了初始条件是 \(z(x,1)\) 而非 \(\varphi(x)\)。但那么 \(z(x,1)\) 是连续且有界的。第二个重要结果是，当 \(\varphi(x)\) 连续且有界时，我们可以如下改进引理 15.3 的近似结果：引理 15.3 中定义的近似 \(\varphi_\epsilon(x)\) 满足

(15.6.26)
\[
\sup_{s \le x \le M} |\varphi(x) - \varphi_\epsilon(x)| \to 0, \text{ 当 } \epsilon \to 0, \forall M \ge s.
\]

我们还将证明 \(z(x,t)\) 的以下正则性性质

(15.6.27)
\[
\int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx \le C \frac{t+1}{t} ||\varphi||^2, \forall t > 0.
\]

注意这里 \(\varphi\) 仅可测且有界。当 \(\varphi\) 属于 \(A\) 的定义域时，我们上面已经看到更好的估计成立。作为结果，我们将有，记 \(y_x(t)\) 为过程 \(y_x^S(t)\)

(15.6.28)
\[
\sup_{t \ge \delta} \sup_{s_0 \le x \le M} E \mathbf{1}_{y_x(t) \ge R} \to 0, \text{ 当 } R \to +\infty, \forall \delta > 0, s < s_0 \le M.
\]

中间结果 (15.6.25), (15.6.26), (15.6.27), (15.6.28) 将在后面证明。我们现在假设 \(\varphi(x)\) 连续且有界。我们想证明

(15.6.29)
\[
z(x, t) \to \int_s^{+\infty} m(x)\varphi(x)dx \text{ 当 } t \to +\infty, \forall x.
\]

只需假设 \(x > s\)。所以让我们选取 \(x_0 > s\)。利用 \(z(x, t) = E\varphi(y_x(t))\) 我们可以写出

\[
E\varphi(y_{x_0}(t)) - \int m\varphi dx = E\varphi(y_{x_0}(t)) - E\varphi_\epsilon(y_{x_0}(t)) + E\varphi_\epsilon(y_{x_0}(t)) - \int m\varphi_\epsilon dx + \int m\varphi_\epsilon dx - \int m\varphi dx.
\]

现在对于 \(R > x_0\) 我们有

\[
|E\varphi(y_{x_0}(t)) - E\varphi_\epsilon(y_{x_0}(t))| \le 2||\varphi|| E\mathbf{I}_{y_{x_0}(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)|,
\]

故

\[
\left| E\varphi(y_{x_0}(t)) - \int m\varphi dx \right| \le 2||\varphi|| E\mathbf{I}_{y_{x_0}(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)| + \left| E\varphi_\epsilon(y_{x_0}(t)) - \int m\varphi_\epsilon dx \right| + \left| \int m\varphi_\epsilon dx - \int m\varphi dx \right|.
\]

由于 \(\varphi\) 属于 \(A\) 的定义域，固定 \(\epsilon\) 和 \(R\)，我们可以令 \(t \to +\infty\) 并推断

\[
\limsup_{t \to +\infty} \left| E\varphi(y_{x_0}(t)) - \int m\varphi dx \right| \le 2||\varphi|| \sup_{t \ge \delta} E\mathbf{I}_{y_x(t) \ge R} + \sup_{s \le x \le R} |\varphi_\epsilon(x) - \varphi(x)| + \left| \int m\varphi_\epsilon dx - \int m\varphi dx \right|.
\]

但随后令 \(\epsilon \to 0\)，然后 \(R \to +\infty\) 并利用性质 (15.6.26), (15.6.28) 右边趋于 0。所以性质 (15.6.15) 已完全证明。

## 中间结果的证明：

## 正则性的证明：

我们知道

(15.6.30)
\[
\begin{aligned}
|z(x, t)| &\le ||\varphi||, \\
\int_0^{+\infty} \int_s^{+\infty} m(x) \left( \frac{\partial z}{\partial x} \right)^2 (x, t) dx dt &\le \frac{1}{\sigma^2} ||\varphi||^2, \\
\int_0^{+\infty} \int_s^{+\infty} \int_0^{+\infty} m(x)(z(x) - z(x - \xi))^2 \mu(d\xi) dx dt &\le \frac{1}{\lambda} ||\varphi||^2.
\end{aligned}
\]





我们现在用 \(m^3(x)\frac{\partial z}{\partial t}\frac{t}{t+1}\) 来检验方程 (15.6.16)，并获得
\[\frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx\]

\[+ \frac{t}{t+1} \int_s^{+\infty} m^{\frac{3}{2}}(x) \frac{\partial z}{\partial t} \left[ \frac{3}{2} \sigma^2 m' m^{\frac{1}{2}} \frac{\partial z}{\partial x} + \nu m^{\frac{3}{2}} \frac{\partial z}{\partial x} \right] (x,t) dx\]

\[- \lambda \frac{t}{t+1} \int_s^{+\infty} m^3(x) \frac{\partial z}{\partial t} \left[ \int_0^{+\infty} (z(x-\xi, t) - z(x,t)) \mu(\xi) d\xi \right] dx\]

\[+ \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx = 0\]

因此
\[\frac{1}{2} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx + \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx\]

\[\le \int_s^{+\infty} m \left( \frac{\partial z}{\partial x} \right)^2 \left( \frac{3}{2} \sigma^2 m' + \nu m \right)^2 (x,t) dx\]

\[+ \lambda^2 \int_s^{+\infty} m^3 \int_0^{+\infty} (z(x-\xi, t) - z(x,t))^2 \mu(\xi) d\xi.\]

从已经获得的估计 (15.6.30) 我们推导出 (15.6.27)，并且还有
(15.6.31) \(\int_s^{+\infty} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx dt \le C ||\varphi||^2.\)

## (15.6.27) 的证明：

令 \(x_0 \in [s_0, M]\)。取 \(\rho\) 使得
\(0 < \rho \le \frac{s_0 - s}{2}.\)

我们记
\(z_R(x,t) = E \mathbb{1}_{Y_x(t) \ge R}.\)

我们使用估计
\(\int_s^{+\infty} m^3(x) \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C \frac{t+1}{t},\)
且常数不依赖于 R。特别是我们推导出
(15.6.32) \(\int_s^{M + \frac{s_0 - s}{2}} \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C_{s_0, M} \left( 1 + \frac{1}{t} \right),\)

这里我们使用了 \(m(x)\) 在区间 \([\frac{s+s_0}{2}, M + \frac{s_0-s}{2}]\) 上有正下确界的事实。现在我们有
\[\int_s^{+\infty} m(x) z_R(x,t) dx = \int_s^{+\infty} m(x) \mathbb{1}_R(x) dx = \int_R^{+\infty} m(x) dx\]
\[\ge \int_{x_0 - \rho}^{+\infty} m(x) z_R(x,t) dx\]

现在对于 \(x \in [x_0 - \rho, x_0 + \rho]\) 我们有
\(|z_R(x,t) - z_R(x_0,t)| \le \rho^{\frac{1}{2}} \left( \int_{\frac{x+x_0}{2}}^{M + \frac{x_0-x}{2}} \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \right)^{\frac{1}{2}} \le \rho^{\frac{1}{2}} (C_{s_0, M})^{\frac{1}{2}} \left( 1 + \frac{1}{t} \right)^{\frac{1}{2}} .\)

现在假设 \(t \ge \delta\) 并设
\(C_{s_0, M, \delta} = (C_{s_0, M})^{\frac{1}{2}} \left( 1 + \frac{1}{\delta} \right)^{\frac{1}{2}} ,\)

我们可以写，使用先前的估计
\(\int_R^{+\infty} m(x) dx \ge (z_R(x_0, t) - \rho^{\frac{1}{2}} C_{s_0, M, \delta}) \int_{x_0 - \rho}^{x_0 + \rho} m(x) dx ,\)

从而
\(z_R(x_0, t) \le \rho^{\frac{1}{2}} C_{s_0, M, \delta} + \frac{\int_R^{+\infty} m(x) dx}{\int_{x_0 - \rho}^{x_0 + \rho} m(x) dx} ,\)

因此也
\(\sup_{x \in [s_0, M]} \sup_{t \ge \delta} z_R(x_0, t) \le \rho^{\frac{1}{2}} C_{s_0, M, \delta} + \frac{\int_R^{+\infty} m(x) dx}{\inf_{x \in [s_0, M]} \int_{x - \frac{\rho}{2}}^{x + \frac{\rho}{2}} m(\xi) d\xi} .\)

令 \(R \to +\infty\)，然后 \(\rho \to 0\)，我们得到性质 (15.6.27)。这个论证是

## 连续性证明 (15.6.43)：

我们首先证明在固定正 \(t\) 时，\(z(x,t)\) 在 \((s, +\infty)\) 内关于 \(x\) 的连续性。这是估计 (15.6.27) 的直接结果。确实，对于任何固定的正 \(t\) 和任何紧集 \([s_0, M]\)，\(z(x,t)\) 在 \(x\) 上的偏导数在 \(L^2(s_0, M)\) 中有界。因此它在 \([s_0, M]\) 上是 \(x\) 的连续函数。所以剩下的是证明在 \(s\) 处的右连续性，即

(15.6.33) \(z(s + \epsilon, t) \to z(S, t) \forall t > 0, \text{ as } \epsilon \to 0 .\)

由于在 \(s\) 的左侧，\(z(x,t) = z(S,t)\)，性质 (15.6.33) 将意味着在任何点处关于 \(x\) 的连续性。回顾在 15.6.1 节中引入的记号 \(\tau_{x,n}\) 以表征轨迹 \(y_x(t)\)，其中 \(\tau_{x,0} = 0, \tau_{x,1} = \tau_x^S\) 且

与
\(\tau_{x,n+1} = \tau_{x,n} + X_{x,n}, \quad n \ge 1 ,\)
\(X_{x,n} = \inf \{ u \ge 0 | S - D(\tau_{x,n} + u) + D(\tau_{x,n}) \} .\)

变量 \(X_{x,n}\) 是独立的且具有相同的概率分布，即 \(\tau_x^S\) 的分布。如果我们定义
\(F_x(t) = \mathbb{E}[\mathbb{I}_{\tau_x^S < t}] ,\)

那么 \(X_{x,n}\) 的概率分布是 \(F_S(t)\)。注意
\(y_x(t) = \begin{cases} x - D(t), & \text{if } t < \tau_x^S \\ S - D(t) + D(\tau_{x,n}), & \text{if } \tau_{x,n} \le t < \tau_{x,n+1} \end{cases}\)

我们可以然后得到 \(z(x,t), t > 0\) 的公式。我们有
\(z(x,t) = E\varphi(x - D(t)) \mathbb{I}_{t < \tau_x^S} + \sum_{n=1}^{+\infty} E\varphi(S - D(t) + D(\tau_{x,n})) \mathbb{I}_{\tau_{x,n} \le t < \tau_{x,n+1}}\)

定义

\(\Psi(x,t) = E\varphi(x - D(t)) \mathbb{1}_{t < \tau_x^S},\)

然后，回顾 \(\mathcal{F}^t = \sigma(D(s), s \le t)\)，通过相对于 \(\mathcal{F}^{\tau_{x,n}}\) 条件化并使用独立性性质，可以检查

\(E\varphi(S - D(t) + D(\tau_{x,n})) \mathbb{1}_{\tau_{x,n} \le t < \tau_{x,n+1}} = E\mathbb{1}_{\tau_{x,n} \le t} \Psi(S, t - \tau_{x,n}), n \ge 1.\)

由于

\(\tau_{x,n} = \tau_x^S + \sum_{j=1}^{n-1} X_{n,j}, n \ge 2,\)

使用独立性性质，我们容易检查

\(E\mathbb{1}_{\tau_{x,n} \le t} = F_x \otimes F_S^{(n-1)}(t),\)

其中 \(F_S^{(n-1)}\) 表示概率分布 \(F_S\) 的 \(n-1\) 次卷积。累积分布函数 \(F_S(t)\) 具有密度 \(f_S(t)\) 且

\(dF_S^{(n-1)}(t) = f_S^{(n-1)}(t)dt.\)

注意对于 \(n=1\) 没有密度且 \(f_S^{(0)}(t) = 1, \forall t > 0\)。在这种情况下 \(f_S^{(0)}(t)dt\) 必须被 0 处的 Dirac 测度所取代。汇总结果我们可以最终写出公式

(15.6.34) \(z(x,t) = \Psi(x,t) + \sum_{n=1}^\infty \int_0^t f_x(t-\eta) \left( \int_0^\eta \Psi(S, \xi) f_S^{(n-1)}(\eta - \xi) d\xi \right) d\eta\)

所以我们必须考虑

(15.6.35) \(z(s+c, t) = \Psi(s+c, t) + \int_0^t f_{s+c}(t-\eta) \Psi(S, \eta) d\eta + \sum_{n=2}^\infty \int_0^t f_{s+c}(t-\eta) \left( \int_0^\eta \Psi(S, \xi) f_S^{(n-1)}(\eta - \xi) d\xi \right) d\eta\)

然而 \(\Psi(x,t)\) 是柯西问题的解

(15.6.36) \(\frac{\partial \Psi}{\partial t} + A\Psi = 0, \quad x > s\)
\(\Psi(x,t) = 0, \quad x \le s\)
\(\Psi(x,0) = \varphi(x)\)

这是一个具有 Dirichlet 边界条件的经典柯西问题。注意解不依赖于 \(x \le s\) 时 \(\varphi(x)\) 的值。然后可以标准地检查

\(\Psi(s+c, t) \to 0, \text{ as } \epsilon \to 0, \forall t > 0.\)

现在如果我们在 (15.6.35) 中取 \(\varphi(x) = 1\)，那么我们看到

\(E\mathbb{1}_{t < \tau_x^{++}} \to 0, \text{ as } \epsilon \to 0, \forall t > 0.\)

这意味着

\(\mathbb{1}_{t < \tau_x^{++}} \to 0 \text{ a.s. as } \epsilon \to 0, \forall t > 0.\)

然后很容易检查

\(E \frac{\tau_x^{s+\epsilon}}{1 + \tau_x^{s+\epsilon}} \to 0,\)

并且也 \(\sigma_t^{r++} \to 0\)，几乎必然。但然后我们可以在公式 (15.6.35) 中取极限并得到

\(z(s + \epsilon, t) \to \Psi(S,t) + \sum_{m=2}^\infty \int_0^t \Psi(S, \xi) f_S^{(m-1)}(t - \xi) d\xi\)
\(= z(S,t)\)

最后的等式通过与 (15.6.34) 比较来检查。

## (15.6.26) 的证明：

我们首先证明一个较弱的结果。令 \(0 < a_0 \le \frac{M}{2}\)，那么我们有

(15.6.37) \(\sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| \to 0, \text{ as } \epsilon \to 0.\)

这个结果需要 \(\varphi\) 的连续性（但不一定是 \(\varphi(s) = \varphi(S)\)）。我们使用

\(\varphi_\epsilon(x) = \frac{1}{\epsilon} E \int_0^{+\infty} \exp\left(-\frac{t}{\epsilon}\right) \varphi(y_\epsilon(t)) dt\)
\(= E \int_0^{+\infty} \exp(-u) \varphi(y_\epsilon(\epsilon u)) du\)

对于固定的 \(T\) 设置

\(\varphi_\epsilon^T(x) = E \int_0^T \exp(-u) \varphi(y_\epsilon(\epsilon u)) du,\)

并且

(15.6.38) \(|\varphi_\epsilon(x) - \varphi_\epsilon^T(x)| \le ||\varphi|| \exp(-T).\)

接下来我们断言对于 \(u \le T\)

\(E\varphi(y_\epsilon(\epsilon u)) = E\varphi(x - D(\epsilon u)) + E(\varphi(y_\epsilon(\epsilon u)) - \varphi(x - D(\epsilon u))) \mathbf{I}_{\tau_\epsilon^z \le T},\)

因此对于 \(u \le T\)

(15.6.39) \(|E\varphi(y_\epsilon(\epsilon u)) - E\varphi(x - D(\epsilon u))| \le 2||\varphi|| E \mathbf{I}_{\tau_\epsilon^z \le T}.\)

很容易看出

\(E \mathbf{I}_{\tau_\epsilon^z \le T} \le P \left( \nu \epsilon T + \sigma \sup_{0 \le u \le T} w(u) + N(\epsilon T) \ge a_0 \right) = \Theta_{a_0}(\epsilon T).\)

这个量当然在 \(\nu \epsilon T \ge a_0\) 时等于 1。为了在 \(\nu \epsilon T < a_0\) 时评估这个量，我们将回顾以下概率分布

\(P \left( \sup_{0 \le u \le T} w(u) \le y \right) = \frac{2}{\sqrt{2\pi T}} \int_0^y \exp\left(-\frac{\xi^2}{2T}\right) d\xi\)

（参见 I. Karatzas, S. Shreve [27]），并且

\(P(N(\epsilon T) \le y) = 1 - \lambda \epsilon T \int_y^{+\infty} \mu(\eta) d\eta + o(\epsilon)\)

但然后

\(P \left( N(\epsilon T) + \sigma \sup_{0 \le u \le T} w(u) \ge y \right) \le \lambda \epsilon T + P \left( \sigma \sup_{0 \le u \le T} w(u) \ge y \right).\)





汇总结果可得

(15.6.40) \(\Theta_{a_\epsilon}(T\epsilon) \le \lambda \epsilon T + \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} \frac{a_0 - \nu \epsilon T}{\sigma \sqrt{\epsilon T}} \exp -\frac{\xi^2}{2} d\xi.\)

接下来，若 \(|D(\epsilon u)| < a_0\)，则有 \(x - D(\epsilon u) \in [s, M]\)。由于 \(\varphi(x)\) 在 \([s, M]\) 上一致连续，存在一个函数 \(\gamma_M(\delta)\)，它单调递增，且当 \(\delta\) 趋于 0 时趋于 0，并且

\(|\varphi(x') - \varphi(x'')| \le \gamma_M(\delta) \text{ if } |x' - x''| \le \delta.\)

因此

\(|\varphi(x - D(\epsilon u)) - \varphi(x)| \le \gamma_M(|D(\epsilon u)|) + 4||\varphi|| \mathbb{I}_{|D(\epsilon u)| \ge a_0}.\)

由于

\(|D(\epsilon u)| \le \nu \epsilon T + \sigma \sup_{0 \le u \le \epsilon T} w(u) + N(\epsilon T),\)

我们得到

\(E|\varphi(x - D(\epsilon u)) - \varphi(x)| \le E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right) + 4||\varphi|| \Theta_{a_\epsilon}(T\epsilon).\)

最后，对于 \(s + a_0 \le x \le M\)，我们得到估计

\(|\varphi_\epsilon(x) - \varphi(x)| \le 2||\varphi|| \exp -T + 6||\varphi|| \Theta_{a_\epsilon}(T\epsilon) + E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right),\)

以及

\(E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right) \le \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} \gamma_M(\nu \epsilon T + \sigma \sqrt{\epsilon T} \xi) \exp -\frac{\xi^2}{2} d\xi + \frac{2}{\sqrt{2\pi}} \lambda \epsilon T \int_0^{+\infty} \exp -\frac{\xi^2}{2} \left( \int_0^{+\infty} \gamma_M(\nu \epsilon T + \sigma \sqrt{\epsilon T} \xi + v) \mu(v) dv \right) d\xi.\)

我们可以汇总估计并写出

\(|\varphi_\epsilon(x) - \varphi(x)| \le 2||\varphi|| \exp -T + C_M(\epsilon T),\)

以及

\(C_M(\epsilon T) \to 0, \text{ as } \epsilon T \to 0.\)

结果 (15.6.37) 易得。

我们现在完成 (15.6.26) 的证明。我们假设 \(\varphi(s) = \varphi(S)\)。首先，利用此假设并假设

\(s + a_0 < S < M, \quad s + 2a_0 < M\)

（\(a_0\) 将取很小值，因此这不是限制），然后应用 (15.6.37)

\(\sup_{s \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| \le \max \left[ \sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)|, \sup_{s \le x \le s+a_0} |\varphi_\epsilon(x) - \varphi(x)| \right]\)

\(\le \sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| + \sup_{s \le x \le s+a_0} |\varphi_\epsilon(x) - \varphi(x)| + \sup_{s \le x \le s+a_0} |\varphi(x) - \varphi(s)|.\)

第一项由 (15.6.37) 得出，第三项将通过 \(\varphi(x)\) 在 \([s, M]\) 上的一致连续性来处理。因此我们专注于第二项。我们可以写出

\[
\varphi_t(x) - \varphi(s) = \int_0^T \exp -u \, E(\varphi(y_\epsilon(\epsilon u)) - \varphi(s)) du + \int_T^{+\infty} \exp -u \, E(\varphi(y_\epsilon(\epsilon u)) - \varphi(s)) \exp -T.
\]

考虑 \(u \le T\)，然后在考虑可能的情况后，人们可以确信以下关系

\[
E\varphi(y_\epsilon(\epsilon u)) - \varphi(s) = -\varphi(s) E\mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| \ge a_0} + E\mathbb{I}_{\tau_T^s > \epsilon u} \mathbb{I}_{|D(\epsilon u)| \ge a_0})
\]
\[
+ E(\varphi(x - D(\epsilon u)) - \varphi(s)) \mathbb{I}_{\tau_T^s > \epsilon u} \mathbb{I}_{|D(\epsilon u)| < a_0}
\]
\[
+ E\varphi(S - D(\epsilon u) + D(\tau_T^s)) \mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| \ge a_0}
\]
\[
+ E(\varphi(S - D(\epsilon u) + D(\tau_T^s)) - \varphi(S)) \mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| < a_0}
\]
\[
+ E\varphi(y_\epsilon(\epsilon u)) \mathbb{I}_{\tau_{a_1, s} \le \epsilon u}.
\]

我们然后考虑以下估计

\(\mathbb{I}_{|D(u)| \ge a_0} \le \nu_{cT+N(T)} + s \mathbb{I}_{\sup_{0 \le u \le T} w(u)} + \mathbb{I}_{\nu_{cT} + N(\epsilon T) + \sigma \sup_{0 \le u \le \epsilon T} w(u)}\)

因此

\(E\mathbb{I}_{|D(u)| \ge a_0} \le 2\Theta_{a_0}(\epsilon T).\)

经过一些额外的努力，我们还可以验证

\(E\mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(u) - D(\tau_T^s)| \ge a_0} \le 2\Theta_{a_0}(\epsilon T);\)

\(E\mathbb{I}_{\tau_{a_1, s} \le u} \le \Theta_{S-s}(\epsilon T).\)

另外

\(E|\varphi(x - D(\epsilon u)) - \varphi(s)| \mathbb{I}_{|D(\epsilon u)| < a_0} \le \gamma_M(2a_0);\)

\(E|\varphi(S - D(\epsilon u) + D(\tau_T^s)) - \varphi(S)| \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| < a_0} \le \gamma_M(a_0),\)

其中 \(\gamma_M(\delta)\) 是 \(\varphi(x)\) 在 \([s, M]\) 上的连续性模量。汇总结果，我们可以断言对于 \(u \le T\)

\(|E\varphi(y_\epsilon(u)) - \varphi(s)| \le ||\varphi|| (4\Theta_{a_*}(\epsilon T) + \Theta_{S-s}(\epsilon T)) + \gamma_M(2a_0) + \gamma_M(a_0),\)

因此

\(\sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le ||\varphi|| (4\Theta_{a_*}(\epsilon T) + \Theta_{S-s}(\epsilon T) + 2 \exp -T) + \gamma_M(2a_0) + \gamma_M(a_0),\)

这意味着

\(\limsup_{\epsilon \to 0} \sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le 2 ||\varphi|| \exp -T + \gamma_M(2a_0) + \gamma_M(a_0).\)

因此也

\(\limsup_{\epsilon \to 0} \sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le 2 ||\varphi|| \exp -T + \gamma_M(2a_0) + \gamma_M(a_0)\)
\(+ \sup_{s \le u \le s+a_0} |\varphi(x) - \varphi(s)|.\)

令 \(a_0\) 趋于 0，然后 \(T\) 趋于 \(+\infty\)，我们看到右边为 0。这完成了中间结果的证明，从而也完成了定理 15.5 的证明。

### 15.6.4. 查普曼-科尔莫戈罗夫方程。

从公式 (15.6.34) 可以看出，对于任何 \(t > 0\)，\(y_\tau(t)\) 都有一个密度。这直接源于 \(x - D(t)\) 在 \(t > 0\) 时有一个密度这一事实。因此，对于 \(\varphi(x) \ge 0\),

\[
\Psi(x, t) \le E\varphi(x - D(t)) = \int \varpi(\xi, t)\varphi(\xi)d\xi,
\]

其中 \(\varpi(\xi, t)\) 是 \(x - D(t)\) 的密度。因此我们可以写出

\[
z(x, t) = E\varphi(y_\tau(t)) = \int p(\xi, t)\varphi(\xi)d\xi,
\]

并且 \(p(\xi, t)\) 是变量 \(y_\tau(t)\) 的密度。形式上我们可以写出

\[
p(\xi, 0) = \delta(\xi - x).
\]

由于当 \(\varphi = 0\) 在 \((s, +\infty)\) 上时 \(z(x, t) = 0\)（再次参见公式 (15.6.34)），我们有对于 \(\xi \le s\) 的 \(p(\xi, t) = 0\)。查普曼-科尔莫戈罗夫方程描述了 \(p(\xi, t)\) 的演化。通过与不变量度类似的考虑，我们可以推导这个方程并得到

\[
\frac{\partial p}{\partial t} - \frac{\sigma^2}{2} \frac{\partial^2 p}{\partial \xi^2} - \nu \frac{\partial p}{\partial \xi} - \lambda \int_0^{+\infty} (p(\xi + \eta, t) - p(\xi, t)) \mu(\eta) d\eta = 0, \quad \text{if } \xi > s
\]
\[
p(\xi, t) = 0, \quad \text{if } \xi \le s
\]
\[
p(\xi, 0) = \delta(\xi - x)
\]

我们已经证明了弱收敛

\[
\int p(\xi, t)\varphi(\xi)d\xi \to \int m(\xi)\varphi(\xi)d\xi, \quad \text{as } t \to +\infty.
\]

注意 \(\frac{\partial p}{\partial \xi}\) 在 \(S\) 处有不连续点，关系为

\[
\frac{\sigma^2}{2} \left( \frac{\partial p}{\partial \xi}(S+0, t) - \frac{\partial p}{\partial \xi}(S-0, t) + \frac{\partial p}{\partial \xi}(s+0, t) \right) + \lambda \int_s^{+\infty} p(x, t) \int_{x-s}^{+\infty} \mu(\xi) d\xi = 0.
\]

我们不展开查普曼-科尔莫戈罗夫方程的细节，因为它没有显式解，且所有关于遍历理论的结果都可以绕过这个方程。

### 15.6.5. 与 s, S 策略相关的成本。

我们现在可以计算与由 (17.2.2) 定义的 s, S 策略相关的成本，适用于一般冲动控制。冲动时间是随机时间 \(\tau_n^s\)，冲动（订单）是 \(S - y_{\tau_n^s}^s(\tau_n^s - 0), \quad n \ge 1\)。回顾公式 (15.6.8)，并使用类似的推理，人们可以确信相关成本由以下给出

\[
u_\alpha^{s,S}(x) = E \int_0^{\tau^s} \exp - \alpha t f(y_{\tau^s}^s(t)) dt + E [\exp - \alpha \tau_s^s (K + c(S - y_{\tau^s}^s(\tau_s^s - 0)))] + E \exp - \alpha \tau_s^s \frac{E \int_0^{\tau^s} \exp - \alpha t f(y_{\tau^s}^s(t)) dt}{1 - E \exp - \alpha \tau_s^s} + E \exp - \alpha \tau_s^s \left[ \frac{\exp - \alpha \tau_s^s (K + c(S - y_{\tau^s}^s(\tau_s^s - 0)))}{1 - E \exp - \alpha \tau_s^s} \right].





我们也可以将此公式写为

(15.6.43) \( u_\alpha^{*,S}(x) = E \int_0^{\tau_x^S} \exp - \alpha t f(y_x^{*,S}(t)) dt + c E [\exp - \alpha \tau_x^S (s - y_x^{*,S}(\tau_x^S - 0))] + \frac{E \exp - \alpha \tau_x^S}{1 - E \exp - \alpha \tau_x^S} [ E \int_0^{\tau_x^S} \exp - \alpha t f(y_x^{*,S}(t)) dt + K + c(S - s) + c E [\exp - \alpha \tau_x^S (s - y_x^{*,S}(\tau_x^S - 0))] ], \)

因此

(15.6.44) \( u_\alpha^{*,S}(S) = -(K + c(S - s)) + \frac{1}{1 - E \exp - \alpha \tau_x^S} [ E \int_0^{\tau_x^S} \exp - \alpha t f(y_x^{*,S}(t)) dt + K + c(S - s) + c E [\exp - \alpha \tau_x^S (s - y_x^{*,S}(\tau_x^S - 0))] ]. \)

因此我们可以写

(15.6.45) \( u_\alpha^{*,S}(x) = E \int_0^{\tau_x^S} \exp - \alpha t f(y_x^{*,S}(t)) dt + c E [\exp - \alpha \tau_x^S (s - y_x^{*,S}(\tau_x^S - 0))] + E \exp - \alpha \tau_x^S (u_\alpha^{*,S}(S) + K + c(S - s)). \)

如果我们引入

\( G_\alpha^{*,S}(x) = u_\alpha^{*,S}(x) + cx, \)

那么我们得到

\( G_\alpha^{*,S}(x) = E \int_0^{\tau_x^S} \exp - \alpha t f(y_x^{*,S}(t)) dt + c(x - E [\exp - \alpha \tau_x^S y_x^{*,S}(\tau_x^S - 0)]) + E \exp - \alpha \tau_x^S (K + G_\alpha^{*,S}(S)). \)

我们使用关系

\( x - E[\exp - \alpha \tau_x^S y_x^{*,S}(\tau_x^S - 0)] = E \int_0^{\tau_x^S} \exp - \alpha t (\nu + \lambda \xi + \alpha y_x^{*,S}(t)) dt, \)

这意味着

(15.6.46) \( G_\alpha^{*,S}(x) = E \int_0^{\tau_x^S} \exp - \alpha t g_\alpha(y_x^{*,S}(t)) dt + E \exp - \alpha \tau_x^S (K + G_\alpha^{*,S}(S)), \)

其中

\( g_\alpha(x) = f(x) + c\nu + c\lambda\xi + \alpha c x; \)

(15.6.47) \( G_\alpha^{*,S}(S) = \frac{E \int_0^{\tau_x^S} \exp - \alpha t g_\alpha(y_x^{*,S}(t)) dt + K E \exp - \alpha \tau_x^S}{1 - E \exp - \alpha \tau_x^S}, \)

并且我们恢复 \( G_\alpha^{*,S}(x) \) 是下列问题的解

(15.6.48) \( \alpha G_\alpha^{*,S}(x) + \alpha G_\alpha^{*,S}(x) = g_\alpha(x) \quad \forall x > s \quad G_\alpha^{*,S}(x) = K + G_\alpha^{*,S}(S) \quad \forall x \le s \)

### 15.6.6. 优化.

我们能否在 s, S 值中进行优化？根据 Q.V.I. 方法，我们知道存在一对唯一的 s, S，它对任意 x 最小化 \(G_\alpha^{*,S}(x)\)。我们回顾，它是下列代数方程组的解。设

\(H_\alpha^{*,S}(x) = (G_\alpha^{*,S})'(x),\)

它在 x = s 处不连续。条件是

(15.6.49) 
\(H_\alpha^{*,S}(s) = 0 \quad H_\alpha^{*,S}(S) = 0,\)

相应的函数变为 C^1。第二个条件从通用公式 (15.6.26) 很明显。确实，S 仅通过项 \(G_\alpha^{*,S}(S)\) 进入，该项应被最小化。请注意，在停止时间 \(\tau_x^s\) 之前的过程 \(y_S^{*,S}(t)\) 的积分部分不依赖于 S。

第二个条件不那么明显。从公式 (15.6.26) 来看，找到一个对任意 x 最小化 \(G_\alpha^{*,S}(x)$ 的唯一 s 似乎并不明显。特别是，它应最小化 \(G_\alpha^{*,S}(S)$。我们随后陈述

**命题 15.3.** 存在一对 s, S 最小化 \(G_\alpha^{*,S}(S)$。它满足条件 (15.6.29) 并对任意 x 最小化 \(G_\alpha^{*,S}(x)$。

证明。由于我们有显式公式，将进行直接验证。我们从 (15.6.27) 注意到

\(G_\alpha^{*,S}(S) = -K + \frac{E \int_0^{\tau_S^y} \exp -\alpha t g_\alpha(y_S^{*,S}(t)) dt + K}{1 - E \exp -\alpha \tau_S^y},\)

因此我们需要最小化表达式

\(G_\alpha^{*,S}(s) = \frac{E \int_0^{\tau_s^y} \exp -\alpha t g_\alpha(y_s^{*,S}(t)) dt + K}{1 - E \exp -\alpha \tau_s^S}.\)

我们随后回顾

\(z_{\alpha,s}(x) = E \int_0^{\tau_x^s} \exp -\alpha t g_\alpha(y(t)) dt,\)

其中 \(y(t) = x - D(t)$ 是下式的解

\(Az_{\alpha,s}(x) + \alpha z_{\alpha,s}(x) = g_\alpha(x), \quad x > s \quad z_{\alpha,s}(x) = 0, \quad x \le s\)

并由公式给出

\(z_{\alpha,s}(x) = \frac{2}{\sigma^2} \int_x^\infty \Gamma_\alpha(x - \xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta - \xi) g_\alpha(\eta) d\eta \right) d\xi,\)

以及

\(E \int_0^{\tau_x^s} \exp -\alpha t g_\alpha(y_S^{*,S}(t)) dt = z_{\alpha,S}(s).\)

重新整理待优化量后变为

\(\Theta_\alpha(s, S) = \frac{\int_s^S \Gamma_\alpha(S - \xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta - \xi) g_\alpha(\eta) d\eta \right) d\xi + K \frac{\sigma^2}{2}}{\int_0^{S-s} \Gamma_\alpha(x) dx}.\)

来自 Q.V.I. 的代数方程，回顾 $H_{\alpha,s}(x)$ 的表达式，参见 (15.5.5) 和 (15.5.6)，归约为

$$ \int_s^S \Gamma_\alpha(S-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g'_\alpha(\eta) d\eta \right) d\xi = 0, $$

和

$$ \int_s^S \left[ \int_s^x \Gamma_\alpha(x-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g'_\alpha(\eta) d\eta \right) d\xi \right] dx + K \frac{\sigma^2}{2} = 0. $$

因此我们需要做的归结为检查：将 $\Theta_\alpha(s,S)$ 对 $s$ 和 $S$ 的导数置零，确实得到 (15.6.30) 和 (15.6.31)。这是纯代数等价。首先有用的是检查

$$ \int_s^x \Gamma_\alpha(x-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g'_\alpha(\eta) d\eta \right) d\xi - \int_s^x \Gamma_\alpha(x-\xi) g_\alpha(\xi) d\xi - \beta_{2\alpha} \int_s^x \Gamma_\alpha(x-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g_\alpha(\eta) d\eta \right) d\xi. $$

因此 (15.6.30) 和 (15.6.31) 变为

$$ \int_s^S \Gamma_\alpha(S-\xi) g_\alpha(\xi) d\xi + \beta_{2\alpha} \int_s^S \Gamma_\alpha(S-\xi) \cdot \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g_\alpha(\eta) d\eta \right) d\xi = 0, $$

和

$$ K \frac{\sigma^2}{2} - \int_s^S \left( \int_s^x \Gamma_\alpha(x-\xi) g_\alpha(\xi) d\xi \right) dx - \beta_{2\alpha} \cdot \int_s^S \left[ \int_s^x \Gamma_\alpha(x-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g_\alpha(\eta) d\eta \right) d\xi \right] dx = 0. $$

但最后这个关系等价于

$$ K \frac{\sigma^2}{2} - \int_s^{+\infty} \exp \beta_{2\alpha}(\eta-s) g_\alpha(\eta) d\eta \int_0^{S-s} \Gamma_\alpha(y) dy + \int_s^S \Gamma_\alpha(S-\xi) \left( \int_\xi^{+\infty} \exp \beta_{2\alpha}(\eta-\xi) g_\alpha(\eta) d\eta \right) d\xi = 0. $$

如果我们现在对 $\Theta_\alpha(s,S)$ 分别对 $s$ 和 $S$ 求导，经过重新整理和联立方程后，可以轻松验证我们确实得到关系 (15.6.52) 和 (15.6.54)。

由于我们恢复了允许求解 Q.V.I. 的值，我们知道 $s$ 的值是唯一确定的，$S$ 也是唯一确定的，前提是我们取最小极小值。由于我们已求解 Q.V.I.，$G_\alpha^{*,S}(x)$ 对任意 $x$ 都被最小化。这结束了证明。$\square$

### 15.6.7. 遍历情况.

我们现在可以轻松处理遍历情况，当 $\alpha \to 0$ 时。我们可以立即检查

$$ \lim_{\alpha \to 0} \alpha u_\alpha^{*,S}(x) = \lim_{\alpha \to 0} \alpha G_\alpha^{*,S}(x) = \lim_{\alpha \to 0} \alpha G_\alpha^{*,S}(s) \\ = c\nu + c\lambda\xi + \frac{K + E \int_0^\tau f(y_s(t)) dt}{E \tau_x^s} = \rho^{*,S}. $$

此外，$G_\alpha^{s,S}(x) - G_\alpha^{s,S}(s) \to G^{s,S}(x)$ 在紧集上一致收敛，且 $G^{s,S}(x)$ 是下式的解

(15.6.56) 
\(AG^{s,S}(x) + \rho^{*,S} = cv + c\lambda\xi + f(x), \quad x > s\)
\(G^{s,S}(x) = 0, \quad x \le s\)
\(0 = K + G^{s,S}(S)\)

从这个方程我们可以验证

(15.6.57) 
\(\rho^{*,S} = cv + c\lambda\xi + \int_s^{+\infty} f(x)m^{s,S}(x)dx\)
\(+ K\frac{\sigma^2}{2}((m^{s,S})'(S-0) - (m^{s,S})'(S+0)),\)

这也是表达式 (15.6.55)。对 $s, S$ 最小化 $\rho^{*,S}$ 导致条件

\((G^{s,S})'(S) = 0 \quad (G^{s,S})(s) = 0,\)

并且我们恢复了遍历情况的 Q.V.I.，参见第 15.5 节。

# 均值回归库存控制

## 16.1. 引言

本章中，我们考虑一种情况：库存控制部分通过冲动控制（如上一章所述）进行，部分通过一种称为均值回归的平滑程序进行。均值回归程序是一个给定的连续反馈，当库存低于或高于某个给定水平时，它会连续增加或减少库存。此动作未经优化，且其成本固定，因此被省略。冲动控制作为决策保留，因此是一种补充。我们将验证 s, S 策略仍然有效，只是 r, s, S 的数量值自然不同。需求是连续扩散，没有跳跃。跳跃情况引发数学困难。均值回归库存模型已在 [13] 和 [14] 中考虑，采用不同技术。事实上，在这些论文中考虑了一个两带冲动控制问题。出人意料的是，这种情况反而更简单，因为需要在有界域中求解微分方程，而不是像本例中那样在无界域中求解微分方程。成本函数也与这些论文不同，后者考虑二次成本，而这里我们考虑传统的持有成本和短缺成本。二次成本的合理性在于，人们试图保持接近目标库存，从而最小化到目标的距离。

### 16.2. 问题描述

### 16.2.1. 模型

需求过程由两部分组成：首先是一个恒定速率 \(\nu$ 的确定性部分。接下来我们考虑一个概率空间 \(\Omega, \mathcal{A}, P$，在其上定义了一个维纳过程 \(w(t)$。区间 \((0, t)$ 上的需求则由以下给出

\(D(t) = \nu t + \sigma w(t)\)

其中 \(\sigma$ 是正系数。令 \(\mathcal{F}^t = \sigma(D(s), s \le t)$。冲动控制是一个序列

\(\theta_n, \upsilon_n\)

其中 \(\theta_n$ 是相对于滤流 \(\mathcal{F}^t$ 的停止时间，\(\upsilon_n$ 是 \(\mathcal{F}^{\theta_n}$ 可测的随机变量。用 \(V$ 表示一个冲动控制，相应的库存由公式描述

\(y_x(t; V) = x + k \left( \gamma t - \int_0^t y_x(s; V) ds \right) - D(t) + M(t; V),\)



with

M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n.

方程 (16.2.1) 中的新项是

k \left( \gamma t - \int_0^t y_s(s; V) ds \right),

该项描述了均值回归过程。库存的增加或减少以连续方式进行。因此，在时间间隔 dt 内，如果库存 y(t) 小于目标 \gamma \ge 0（且 k > 0），则库存增加 k(\gamma - y(t))dt。如果库存大于 \gamma，则库存相应减少相同数量。如果 k = 0，均值回归部分消失，我们恢复上一章的模型，只是没有跳跃。请注意，项 k\gamma t 可以与需求的确定性部分 -\nu t 合并，这在数学分析中会很明显。然而，这些项具有不同的经济解释，因此我们不将它们合并。因此，我们不对 k\gamma - \nu 的符号做任何假设。

成本泛函将与没有均值回归部分的情况相同。令

f(x) = hx^+ + px^-.

我们按如下定义成本泛函

(16.2.2) \quad J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp -\alpha \theta_n + \int_0^\infty f(y_s(t; V)) \exp -\alpha t dt \right],

以及值函数

u(x) = \inf J_x(V).

### 16.2.2. Q.V.I.

然后可以写出源自动态规划的Q.V.I。我们引入算子

(16.2.3) \quad Au(x) = -\frac{1}{2} \sigma^2 u''(x) + (\nu + k(x - \gamma)) u'(x),

其中可以看到源自均值回归部分的项。算子 A 不再具有常系数。

Q.V.I. 由以下给出

(16.2.4)
Au(x) + \alpha u(x) \le f(x)
u(x) \le M(u)(x)
(Au(x) + \alpha u(x) - f(x))(u(x) - M(u)(x)) = 0

其中

M(u)(x) = K + \inf_{v > 0} [cv + u(x + v)].

像往常一样，我们寻找一个具有线性增长的 C^1 函数。标准论证表明，Q.V.I 的解即为值函数。

### 16.2.3. 变换

如同上一章所做的那样，考虑如下变换很方便

$$G(x) = u(x) + cx,$$

因此问题变为：寻找一个 \(x \in R\)、\(C^1\) 且具有线性增长的函数 \(G(x)\)，使其满足

$$(16.2.5) \quad \begin{aligned} AG(x) + \alpha G(x) \le g(x) + c(v - k\gamma) \\ G(x) \le K + \inf_{\eta \ge x} G(\eta) \\ (AG(x) + \alpha G(x) - g(x) - c(v - k\gamma))(G(x) - K - \inf_{\eta \ge x} G(\eta)) = 0 \end{aligned}$$

函数 \(g\) 由以下给出

$$(16.2.6) \quad g(x) = f(x) + c(\alpha + k)x.$$

## 16.3. s, S 策略

### 16.3.1. 阈值 s

给定一个数 s，我们按如下方式寻找 (16.2.5) 的解：

$$(16.3.1) \quad \begin{aligned} AG_s(x) + \alpha G_s(x) = g(x) + c(v - k\gamma), & \quad x > s \\ G_s(x) = K + \inf_{\eta \ge x} G_s(\eta), & \quad x \le s \end{aligned}$$

为了得到一个全局 \(C^1\) 的函数，我们施加条件

$$(16.3.2) \quad G'_s(s) = 0.$$

这是定义 s 的关系式。我们通过考虑

$$H_s(x) = G'_s(x),$$

它是以下问题的解

$$(16.3.3) \quad \begin{aligned} AH_s(x) + (\alpha + k)H_s(x) = g'(x), & \quad x > s \\ H_s(x) = 0, & \quad x \le s \end{aligned}$$

对于给定的 s，我们寻找狄里克莱问题 (16.3.3) 的一个有界连续解 \(H_s(x)\)。为了定义 s，我们使用第二个关系式 (16.3.1)，它可以写成如下形式

$$(16.3.4) \quad 0 = K + \inf_{\eta \ge s} \int_s^\eta H_s(\eta) d\eta.$$

请注意

$$(16.3.5) \quad g'(x) = \left\{ \begin{array}{ll} h + c(\alpha + k), & \text{if } x > 0 \\ -p + c(\alpha + k), & \text{if } x < 0 \end{array} \right.$$

我们做如下假设

$$(16.3.6) \quad -p + c(\alpha + k) < 0.$$

### 16.3.2. 格林函数

虽然可以通过近似程序证明 (16.3.3) 解的存在，但像在标准情况下所做的那样，获得显式公式很重要。为此，我们需要一个格林函数，即全空间内无右项的微分方程的解。我们引入以下问题

$$
\begin{aligned}
-\frac{1}{2}\sigma^2\Phi''(x) + (\nu + k(x - \gamma))\Phi'(x) + (\alpha + k)\Phi(x) &= 0, \forall x \in R \\
\Phi(0) &= 1, \quad \Phi(+\infty) = 0
\end{aligned}
$$

我们要证明

### 定理 16.1.

我们假设 (16.3.6)。(16.3.7) 存在唯一解，使得

(16.3.8) \Phi(x) > 0, \Phi'(x) < 0, \Phi''(x) > 0.

当 \(x \to -\infty\) 时，\(\Phi(x) \to +\infty\)，\(\Phi'(x) \to -\infty\)。考虑方程的根 \(\beta_k < 0, \beta_k^* > 0\) 
\(-\frac{1}{2}\sigma^2\beta^2 + \nu\beta + \alpha + k = 0,\)

我们有增长条件

$$
0 > \Phi'(x) \ge \frac{k}{\sigma^2} \frac{(x - \gamma)^2}{\beta_k^* - \beta_k} \left[ \beta_k \left( \beta_k^* - \Phi(0) \exp - \frac{k\gamma^2}{\sigma^2} \right) \exp \beta_k x + \beta_k^* \left( \Phi(0) \exp - \frac{k\gamma^2}{\sigma^2} - \beta_k \right) \exp \beta_k^* x \right], x \le 0
$$

### 证明。

我们首先在 \([0, +\infty)\) 上求解 (16.3.7)。这是一个狄里克莱类型的边值问题。它有唯一解，并且

0 \le \Phi(x) \le 1, x \ge 0,

并且我们有能量关系

(16.3.10) \frac{\sigma^2}{2} \int_0^{+\infty} \Phi'^2 dx + \left( \alpha + \frac{k}{2} \right) \int_0^{+\infty} \Phi^2 dx = -\frac{\sigma^2}{2} \Phi'(0) + \frac{1}{2} (\nu - k\gamma).

接下来，我们用 \(\Phi'(x)\) 对方程 (16.3.7) 进行试验，并在 0 到 \(x > 0\) 之间积分。我们得到

-\frac{\sigma^2}{4} \Phi'^2(x) + \frac{\sigma^2}{4} \Phi'^2(0) + \int_0^x (\nu + k(\xi - \gamma)) \Phi'^2(\xi) d\xi + \frac{\alpha + k}{2} (\Phi^2(x) - 1) = 0,

从这个公式中，可以很容易地看出 \(\Phi''(x)\) 在 \(x \to +\infty\) 时有一个极限，但由于 \(\Phi'^2(x)\) 也是一个 \(L^1\) 函数，这个极限必然为 0。因此，我们得到一个额外的能量关系

(16.3.11) \frac{\sigma^2}{4} \Phi'^2(0) + \int_0^{+\infty} (\nu + k(x - \gamma)) \Phi'^2(x) dx = \frac{\alpha + k}{2}.

由于 \(\Phi(\epsilon) < 1 = \Phi(0)\)，我们看到 \(\Phi'(0) \le 0\)。事实上，\(\Phi'(0) < 0\)。确实，如果令 \(\Psi(x) = \Phi'(x)\)，则 \(\Psi(x)\) 满足

(16.3.12) -\frac{1}{2} \sigma^2 \Psi''(x) + (\nu + k(x - \gamma)) \Psi'(x) + (\alpha + 2k) \Psi(x) = 0, x > 0,

并且我们已经知道 \(\Psi(+\infty) = 0\)。因此 \(\Psi(0)\) 不能为 0，否则 \(\Psi(x)\) 将恒为 0，从而 \(\Phi(x)\) 在 \([0, \infty)\) 上为常数，这是不可能的。由于 \(\Psi(0) \le 0\)，事实上 \(\Psi(0) < 0\)。必然 \(\Psi(x) \le 0\) 且在任何点都不能为 0，否则该点将是一个极大值，这也是不可能的。因此 \(\Psi(x) < 0, \forall x \ge 0\)。此外，\(\Psi'(x)\) 在任何点都不能为负或零。否则，\(\Psi(x)\) 将有一个负的局部最小值，这也是不可能的。因此 \(\Psi(x) = \Phi'(x) < 0, \forall x \in (0, \infty)\)。

我们因此证明了 \(x \in [0, \infty)\) 时的性质 (16.3.8)。

接下来，我们在 \((-\infty, 0]\) 上将方程 (16.3.7) 求解为一个给定 0 处初值的二维线性微分方程组。为方便起见，我们将改变 \(x\) 的符号，以在 \([0, \infty)\) 上求解一个系统。定义

\(y(x) = \Phi(-x), z(x) = \Phi'(-x), x > 0\)

那么对 \(y(x), z(x)\) 是以下问题的解

(16.3.13)
\[
\begin{aligned}
y' &= -z; \\
z' &= \frac{2}{\sigma^2}((kx - (\nu - k\gamma))z - (\alpha + k)y),
\end{aligned}
\]
在 \([0, \infty)\) 上，初始条件为 \(y(0) = 1, z(0) = z_0 = \Phi'(0) < 0\)。考虑矩阵

\(\mathcal{A}(x) = \left( \begin{array}{ c c }
0 & -1 \\
-\frac{2}{\sigma^2}(\alpha + k) & \frac{2}{\sigma^2}(kx - (\nu - k\gamma)) 
\end{array} \right),\)

然后我们将其与一组矩阵关联，称为 \(\Sigma(x, x_0), x \ge x_0\)，即满足微分方程的*基本矩阵*

\[
\begin{aligned}
\frac{d}{dx}\Sigma(x, x_0) &= \mathcal{A}(x)\Sigma(x, x_0); \\
\Sigma(x_0, x_0) &= I,
\end{aligned}
\]

其中 \(I\) 是单位矩阵。根据线性微分方程理论，矩阵 \(\Sigma(x, x_0)\) 对于任何 \(x \ge x_0\) 的对都定义良好。此外，(16.3.13) 的解由以下给出

\(\begin{pmatrix} y(x) \\ z(x) \end{pmatrix} = \Sigma(x, 0) \begin{pmatrix} 1 \\ z_0 \end{pmatrix},\)

因此它对任何 \(x > 0\) 都唯一确定。令

\(\varpi(x) = \exp -\frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right],\)

以及

\(\bar{z}(x) = z(x)\varpi(x),\)

那么对 \(y(x), \bar{z}(x)\) 是以下问题的解

(16.3.14)
\[
\begin{aligned}
y' &= -\frac{\bar{z}}{\varpi} \\
\bar{z}' &= -\frac{2}{\sigma^2}(\alpha + k)\varpi y
\end{aligned}
\]

初始条件为 \(y(0) = 1, \bar{z}(0) = z_0 \exp - \frac{k\gamma^2}{\sigma^2}\)。很容易看出 \(y(x) > 0, \bar{z}(x) < 0\)。经过简单变形后，我们得到 \(\bar{z}(x)\) 的以下积分方程

(16.3.15)
\[
\begin{aligned}
\bar{z}(x) &= \bar{z}(0) - \frac{2}{\sigma^2}(\alpha + k)y(0) \int_0^x \varpi(\xi) d\xi \\
&+ \frac{2}{\sigma^2}(\alpha + k) \int_0^x G(x, \eta) \bar{z}(\eta) d\eta,
\end{aligned}
\]



与

$$G(x, \eta) = \int_{\eta}^{x} \frac{\varpi(\xi)}{\varpi(\eta)} d\xi,$$

以及

$$
\frac{\varpi(\xi)}{\varpi(\eta)} = \exp - \frac{2}{\sigma^2} \left[ \frac{k}{2} (\xi - \eta)(\xi + \eta + 2\nu) - \nu(\xi - \eta) \right].
$$

对于 \(\xi \ge \eta \ge 0\)，有

$$
\frac{\varpi(\xi)}{\varpi(\eta)} \le \exp \frac{2\nu}{\sigma^2} (\xi - \eta),
$$

因此对于 \(x \ge \eta \ge 0\)

$$
G(x, \eta) \le \frac{\exp \frac{2\nu}{\sigma^2}(x - \eta) - 1}{\frac{2\nu}{\sigma^2}}.
$$

另外

$$
\varpi(x) \le \exp \frac{2\nu}{\sigma^2} x.
$$

我们在 (16.3.15) 中使用这些不等式，并注意到 \(y(0) = 1\) 且 \(\tilde{z}(\eta) \le 0\)。经过整理后，我们得到不等式

(16.3.16) $$
\tilde{z}(x) \ge \tilde{z}(0) + \frac{\alpha + k}{\nu} y(0) - \frac{\alpha + k}{\nu} \cdot \exp \frac{2\nu}{\sigma^2} x \left( y(0) - \int_0^x \tilde{z}(\eta) \exp - \frac{2\nu}{\sigma^2} \eta d\eta \right) - \frac{\alpha + k}{\nu} \int_0^x \tilde{z}(\eta) d\eta.
$$

我们接着引入函数 \(u(x)\)，它是以下方程的解

(16.3.17) $$
\begin{aligned}
u(x) = \tilde{z}(0) + \frac{\alpha + k}{\nu} y(0) - \frac{\alpha + k}{\nu} \cdot \exp \frac{2\nu}{\sigma^2} x \Bigg( y(0) - \int_0^x u(\eta) \exp - \frac{2\nu}{\sigma^2} \eta d\eta \Bigg) - \frac{\alpha + k}{\nu} \int_0^x u(\eta) d\eta.
\end{aligned}
$$

可以轻易验证 \(u(x)\) 满足

$$-\frac{\sigma^2}{2} u''(x) + \nu u'(x) + (\alpha + k)u(x) = 0,$$

并且还有

$$u(0) = \tilde{z}(0), \quad u'(0) = -\frac{2}{\sigma^2}(\alpha + k)y(0).$$

考虑方程

$$-\frac{\sigma^2}{2} \beta^2 + \nu \beta + (\alpha + k) = 0,$$

的根，记为 \(\beta_k < 0, \beta_k^* > 0\)，我们可以用公式表示函数 \(u(x)\)

(16.3.18) $$
\begin{aligned}
u(x) = \frac{\tilde{z}(0)}{\beta_k^* - \beta_k} (-\beta_k \exp \beta_k^* x + \beta_k^* \exp \beta_k x) - \frac{2}{\sigma^2} (\alpha + k)y(0) \frac{1}{\beta_k^* - \beta_k} (\exp \beta_k^* x - \exp \beta_k x).
\end{aligned}
$$

让我们验证 \(\tilde{z}(x) \ge u(x)\)。确实，如果令 \(w(x) = \tilde{z}(x) - u(x)\)，则有不等式

$$w(x) \ge \frac{\alpha + k}{\nu} k \int_0^x \left( \exp \frac{2\nu}{\sigma^2}(x - \eta) - 1 \right) w(\eta) d\eta,$$

因此

\( w(x) \ge - \frac{\alpha + k}{\nu} \int_0^x \left( \exp \frac{2\nu}{\sigma^2}(x - \eta) - 1 \right) w(\eta) d\eta; \)

\( w(x) \exp - \frac{2\nu}{\sigma^2} x \le \frac{\alpha + k}{\nu} \int_0^x \exp - \frac{2\nu}{\sigma^2} \eta \ w(\eta) d\eta. \)

根据 Gronwall 不等式，我们断言

\( w(x) - \exp \frac{2\nu}{\sigma^2} x = 0, \)

这意味着结果成立。回顾一下

\( \tilde{z}(0) = -y'(0) \exp -\frac{k\gamma^2}{\sigma^2} = \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}; \)

\( y(0) = \Phi(0) = 1; \quad \beta_k \beta_k^* = -\frac{2}{\sigma^2}(\alpha + k); \quad \beta_k^* + \beta_k = \frac{2\nu}{\sigma^2}, \)

并重新整理后，我们可以写成

\( z(x) \exp \frac{k}{\sigma^2}(x+\gamma)^2 \ge \beta_k \exp -\beta_k x \frac{\beta_k^* - \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}}{\beta_k^* - \beta_k} + \beta_k^* \exp -\beta_k^* x \frac{-\beta_k + \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}}{\beta_k^* - \beta_k}. \)

最后，回顾 \( z(x) = \Phi'(x) - x \ge 0 \)，我们很容易推导出估计 (16.3.9)。我们有 \( \Phi(x) > 0, \Phi'(x) < 0 \)。让我们验证

(16.3.19) \( \quad \Phi'(x) \to -\infty, \text{ as } x \to -\infty. \)

确实，根据 (16.3.14)，\(\tilde{z}(x)\) 是严格递减的。因此

\( z(x) = \tilde{z}(x) \exp \frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right] \le \tilde{z}(0) \exp \frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right] \to -\infty, \text{ as } x \to +\infty \)

故 (16.3.19)。考虑 \(\Psi(x) = \Phi'(x)\)。它是 (16.3.12) 的一个解，且 \(\Psi(x) < 0, \forall x \le 0\)。此外

\( \Psi(x) \to -\infty, \text{ as } x \to -\infty \)

我们还知道 \(\Psi'(0) = \Phi''(0) > 0\)。必然有

\( \Psi'(x) = \Phi''(x) > 0, \forall x < 0 \)

否则将存在一点 \(x_0\)，使得 \(\Psi'(x_0) = 0\)。我们可以取最大的负数这样的点。它是 \(\Psi(x)\) 的一个局部最小值。但根据方程 (16.3.12)，\(\Psi(x)\) 在 \(x < 0\) 时不能有负的局部最小值。证明完成。\(\square\)

我们称 \(\Phi(x)\) 为问题 (16.3.3) 的 Green 函数，类比于线性 P.D.E. 的解。注意当 \(k=0\) 时，

\( \Phi(x) = \exp \beta x, \)

其中 \(\beta\) 是方程

\( -\frac{\sigma^2}{2} \beta^2 + \nu \beta + \alpha = 0. \)

的负根。

## 16.3.3. (16.3.3) 的解

得益于 Green 函数，我们可以给出 (16.3.3) 解的显式公式。令

(16.3.20)
$$
\vartheta(x) = \varpi(-x)
= \exp -\frac{2}{\sigma^2} \left[ k \frac{(x-\gamma)^2}{2} + \nu x \right].
$$

我们先考虑函数

(16.3.21)
$$
\chi(x) = \vartheta(x)\Phi(x), x \in R,
$$

它满足微分方程

(16.3.22)
$$
-\frac{\sigma^2}{2}\chi''(x) - (k(x-\gamma) + \nu)\chi'(x) + \alpha\chi(x) = 0
$$

$$
\chi(0) = \exp -\frac{k}{\sigma^2}\gamma^2, \chi(+\infty) = 0
$$

### Lemma 16.1

(16.3.22) 存在且仅存在一个解。此外

(16.3.23)
$$
\chi'(x) < 0, \chi(x) \to +\infty, \text{as } x \to -\infty.
$$

**Proof.** 由 (16.3.22) 定义的函数是一个解，通过直接检查可得。唯一性来自线性微分方程理论，与 \(\Phi(x)\) 的情况相同。我们只需证明 \(\chi'(x) < 0\)。必然有 \(\chi'(0) < 0\)，否则 \(\chi(x)\) 在 \(x > 0\) 且接近 0 时会增加。但随后，由于它在 \(x \to +\infty\) 时趋于 0，\(\chi(x)\) 将在 \((0, +\infty)\) 上有一个正的最大值，这是不可能的。然后我们有 \(\chi'(x) = \vartheta(x)\Phi'(x) - \frac{2}{\sigma^2}(k(x-\gamma) + \nu)\)。由于 \(\Phi'(x) < 0\)，对于 \(x \ge \gamma\)，有 \(\chi'(x) < 0\)。如果 \(\chi'(x)\) 在 \((0, \gamma)\) 的某点 \(x^*\) 处消失，则第一个这样的点必须是局部最小值。但随后 \(\chi(x)\) 在 \(x^*\) 之后，靠近 \(x^*\) 处会增加。但随后将有一个正的局部最大值，这是不可能的。因此，对于 \(x \ge 0\)，有 \(\chi'(x) < 0\)。当 \(x < 0\) 时，同样 \(\chi'(x)\) 不能消失并改变符号，否则 \(\chi(x)\) 将有一个正的局部最大值。它不能有拐点，因为二阶导数将为 0，而根据二阶方程 (16.3.22) 这是不可能的。\(\chi(x) \to +\infty\) 当 \(x \to -\infty\) 这一事实立即从 \(\chi'(x) < 0\) 且对于足够小的 \(x\) 有 \(\chi'(x) > 0\) 得出。

然后我们陈述

### Theorem 16.2

(16.3.3) 的解是唯一的，并由公式给出

(16.3.24)
$$
H_s(x) = \frac{2}{\sigma^2} \int_s^x \frac{\Phi(x)}{\Phi(\xi)} \left( \int_\xi^{+\infty} g(\eta) \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, x \ge s.
$$

**Proof.** 首先要证明的是，由 (16.3.24) 定义的函数，为简洁起见称为 \(H_s(x)\)，是有界的。由于 \(g'(x)\) 是有界的，只需证明函数

$$
Z_s(x) = \frac{2}{\sigma^2} \int_s^x \frac{\Phi(x)}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, x \ge s
$$

是有界的。从函数 \(\Phi(x)\) 和 \(\chi(x)\) 的性质可以轻易验证，只需证明 \(Z_0(x)\) 是有界的。但我们将证明

(16.3.25)
$$
Z_0(x) = \frac{1 - \Phi(x)}{\alpha + k}.
$$

确实，让我们按 (16.3.25) 定义 \(Z_0(x)\)。它是下式的一个有界解

(16.3.26) 
$$
-\frac{\sigma^2}{2} Z_0'' + (\nu + k(x - \gamma))Z_0' + (\alpha + k)Z_0 = 1, \quad x > 0
$$
$$
Z_0(0) = 0
$$

接着定义

$$
A(x) = \frac{Z_0(x)}{\Phi(x)} = - \frac{1}{\alpha + k} + \frac{1}{\alpha + k} \frac{1}{\Phi(x)}
$$

然后，通过直接计算，我们有

$$
A''(x) + A'(x) \left[ 2 \frac{\Phi'(x)}{\Phi(x)} - \frac{2}{\sigma^2}(\nu + k(x - \gamma)) \right] = - \frac{2}{\sigma^2 \Phi(x)},
$$

因此也有

$$
\frac{d}{dx} (A'(x) \Phi^2(x) \vartheta(x)) = - \frac{2}{\sigma^2} \Phi(x) \vartheta(x).
$$

但也从 \(A(x)\) 的定义可得

$$
A'(x) \Phi^2(x) \vartheta(x) = - \frac{1}{\alpha + k} \Phi'(x) \vartheta(x).
$$

由于在 \(x > 0\) 时，\(\Phi'(x)\) 是有界的，右边在 \(x \to +\infty\) 时趋于 0。因此，必然有

$$
A'(x) \Phi^2(x) \vartheta(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \chi(\eta) d\eta.
$$

现在，由于 \(A(0) = 0\)，我们得到

$$
A(x) = \frac{2}{\sigma^2} \int_0^x \frac{1}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi,
$$

因此，\(Z_0(x)\) 也由公式给出

$$
Z_0(x) = \frac{2}{\sigma^2} \int_0^x \frac{\Phi(\eta)}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, \quad x \ge 0,
$$

这证明了右边也是有界的。接下来，由 (16.3.24) 定义的函数是 (16.3.3) 的解。

让我们证明有界解的唯一性。当然，只需证明

$$
AH_s(x) + (\alpha + k)H_s(x) = 0, \quad x > s
$$
$$
H_s(s) = 0
$$

的有界解为 0。假设 \(H_s(x)\) 变为严格正。它不能有正的局部最大值。否则，如果 \(x^*\) 是严格大于 \(s\) 的最小局部最大值，则

$$
H_s'(x^*) = 0, \quad H_s''(x^*) < 0,
$$

这会导致矛盾。因此 \(H_s(x) > 0\)。由于 \(H_s(x)\) 是有界的，我们必须有 \(H_s'(x) \to 0\)，当 \(x \to +\infty\)。考虑一点 \(x_0\)，使得 \(\nu + k(x_0 - \gamma) > 0\)。存在一点 \(x^*\)，使得 \(H_s''(x^*) < 0\)。在这一点上，再次出现矛盾。因此 \(H_s(x) \le 0\)。通过类似的推理，我们很容易看出 \(H_s(x)\) 不能变为严格负。因此它为 0。证明已完成。\(\square\)





## 16.3.4. 函数 $G_s(x)$

首先定义

(16.3.27)
$$
Q(x) = \frac{2}{\sigma^2} \int_x^{+\infty} g(\eta) \frac{\chi(\eta)}{\chi(x)} d\eta.
$$

因此函数 $H_s(x)$ 是 (16.3.3) 的解（$s$ 为固定参数），可以写成如下形式

(16.3.28)
$$
H_s(x) = \int_s^x \frac{\Phi(\eta)}{\Phi(\xi)} Q(\xi) d\xi.
$$

从函数 $H_s(x)$ 我们通过公式定义函数 $G_s(x)$

(16.3.29)
$$
G_s(x) = \begin{cases} G_s(s) + \int_s^x H_s(\xi) d\xi, & x > s \\ G_s(s), & x \le s \end{cases}
$$

选取

(16.3.30)
$$
G_s(s) = \frac{g(s) + \frac{\sigma^2}{2} Q(s) + c(\nu - k\gamma)}{\alpha}.
$$

进而有

### **引理 16.2.** 函数 $G_s(x)$ 是 $C^1$ 且满足

$$
AG_s(x) + \alpha G_s(x) = g(x) + c(\nu - k\gamma), \quad x > s
$$

### **证明.** 其 $C^1$ 性质是 $H_s(s) = 0$ 的结果。接下来函数 $H_s(x)$ 的方程 (16.3.3) 可以写成如下形式

$$
-\frac{\sigma^2}{2} H_s''(x) + \frac{d}{dx}[(\nu + k(x - \gamma)) H_s(x)] + \alpha H_s(x) = g'(x).
$$

在 $s$ 和 $x$ 之间积分并整理后，我们对 $x > s$ 得到

$$
-\frac{\sigma^2}{2} G_s''(x) + \frac{\sigma^2}{2} H_s'(x) + (\nu + k(x - \gamma)) G_s'(x) + \alpha G_s(x) - \alpha G_s(s) = g(x) - g(s),
$$

并且从 $G_s(s)$ 的定义可得结果，注意 $H'_s(s) = Q(s)$。

### **引理 16.3.** 函数 $G_s(x)$ 在 $x \ge s$ 处取得其下确界。

### **证明.** 从 $Q(x)$ 的定义 (16.3.27) 和 $g'(x)$ 的值可得 $Q(x) > 0$ 对 $x \ge 0$ 成立。对于 $x < 0$ 我们有公式

$$
\frac{\sigma^2}{2} Q(x) \chi(x) = (-p + c(\alpha + k)) \int_x^0 \chi(\eta) d\eta + (h + c(\alpha + k)) \int_0^\infty \chi(\eta) d\eta,
$$

这显然是一个递增函数。我们回顾，参见引理 16.1，$\chi(x) \to +\infty$ 当 $x \to -\infty$。因此

$$
Q(x) \chi(x) \to -\infty, \quad \text{as } x \to -\infty
$$

由此可知存在唯一点 $x_0 < 0$ 使得

$$
Q(x_0) = 0, \quad Q(x) > 0, \forall x > x_0, \quad Q(x) < 0, \forall x < x_0 < 0
$$

对于 $s \ge x_0$，$H_s(x) > 0$，因此 $G_s(x)$ 递增。故其最小值在 $s$ 处取得。

接下来假设 $s < x_0 < 0$。

我们此时可以写成

$$
AH_s(x) + (\alpha + k) H_s(x) = h + c(\alpha + k),
$$

因此我们也可以写成

$$
H_s(x) = \frac{h+c(\alpha+k)}{\alpha+k} + \Phi(x) \left( H_s(0) - \frac{h+c(\alpha+k)}{\alpha+k} \right), \quad \forall x \ge 0.
$$

这意味着

$$
H_s(x) \to \frac{h+c(\alpha+k)}{\alpha+k}, \quad \text{as } x \to +\infty
$$

从而

$$
G_s(x) \to +\infty, \quad \text{as } x \to +\infty
$$

由于 $H'_s(s) = Q(s) < 0$，$(H_s)$ 在 $x$ 接近 $s$ 且大于 $s$ 时保持严格负值。因此 $G_s(x)$ 在 $x$ 接近 $s$ 且大于 $s$ 时递减。

由于当 $x \to +\infty$ 时它趋向 $+\infty$，它在 $x \ge s$ 处取得其最小值，在点 $\neq s$ 处。

我们可以定义 $S(s)$ 为 $G_s(x)$ 在 $x \ge s$ 上的最小最小值。从引理 16.3 的证明中我们看到

(16.3.31)
$$
S(s) = s, \forall s \ge x_0, \quad S(s) > x_0 \quad \forall s < x_0
$$

## 16.3.5. 求解 $s$

点 $s$ 是 (16.3.4) 的解，这也意味着

(16.3.32)
$$
0 = K + \int_s^{S(s)} H_s(\eta) d\eta.
$$

### **命题 16.1.** 存在唯一 $s < x_0$ 是 (16.3.32) 的解。

### **证明.** 我们研究函数

$$
\gamma(s) = \int_s^{S(s)} H_s(\eta) d\eta.
$$

显然

$$
\gamma(s) = 0, \quad \forall s \ge x_0.
$$

对于 $s < x_0$，我们有，注意到 $H_s(s) = H_s(S(s)) = 0$，

$$
\gamma'(s) = \int_s^{S(s)} \frac{\partial}{\partial s} H_s(\eta) d\eta
$$

并且从公式 (16.3.28) 我们得到

(16.3.33)
$$
\gamma'(s) = -\frac{Q(s)}{\Phi(s)} \int_s^{S(s)} \Phi(x) dx,
$$

并且由于 $Q(s) < 0$，我们立即看到 $\gamma'(s) > 0$。关键步骤是证明

(16.3.34)
$$
\liminf_{s \to -\infty} \gamma'(s) \ge \frac{p - c(\alpha + k)}{\alpha + k}.
$$

这将在下一个引理中完成。如果 (16.3.34) 成立，则

(16.3.35)
$$
\gamma(s) \to -\infty, \quad \text{as } s \to -\infty.
$$

由于然后，$\gamma(s)$ 从 $-\infty$ 增加到 $0$，当 $s$ 从 $-\infty$ 增加到 $0$。因此存在唯一 $s < x_0$ 使得 $\gamma(s) = -K$。这结束了证明。

由 (16.3.29) 和 (16.3.30) 定义的函数 $G_s(x)$ 满足 (16.3.1) 和 (16.3.2)。仍需证明

### **引理 16.4.** 属性 (16.3.34) 得到满足。

### **证明.** 我们首先注意到

$$
\gamma'(s) \ge -\frac{Q(s)}{\Phi(s)} \int_s^\infty \Phi(\eta) d\eta.
$$

另外

(16.3.36)
$$
\gamma'(s) \ge \frac{Q(s)}{\Phi(s)} \int_s^0 \Phi(\eta) d\eta \left( 1 - \frac{\int_{-\infty}^0 \Phi(\eta) d\eta}{\int_s^\infty \Phi(\eta) d\eta} \right).
$$

由于

$$
\int_s^\infty \Phi(\eta) d\eta \to +\infty, \text{ as } s \to -\infty
$$

括号中的第二项当 $s \to -\infty$ 时趋于 0。因此我们关注函数

$$
Z(x) = -\frac{Q(x)}{\Phi(x)} \int_x^0 \Phi(\eta) d\eta, x \le 0
$$

接下来我们注意到

$$
Q(x) = \frac{2}{\sigma^2}(-p + c(\alpha + k)) \int_x^\infty \frac{\chi(\eta)}{\chi(x)} d\eta + \frac{2}{\sigma^2}(h + c(\alpha + k)) \int_0^{+\infty} \frac{\chi(\eta)}{\chi(x)} d\eta,
$$

并且由于 $\chi(x) \to +\infty$，当 $x \to -\infty$，第二项当 $x \to -\infty$ 时趋于 0。接下来考虑 $x < 0$ 时 $\chi(x)$ 的方程 (16.3.22)。我们在 $x$ 和 $0$ 之间积分并除以 $\chi(x)$。我们容易得到

$$
\int_x^0 \frac{\chi(\eta)}{\chi(x)} d\eta = -\frac{\sigma^2}{2(\alpha+k)} \frac{\Phi'(x)}{\Phi(x)} + \frac{2}{(\alpha+k)\chi(x)} (\chi'(0) + \chi(0)(\nu - k\gamma)),
$$

同样，考虑 $x < 0$ 时 $\Phi(x)$ 的方程，参见 (17.2.1)，我们在 $x$ 和 $0$ 之间积分并得到

$$
\int_x^0 \frac{\Phi(\eta)}{\Phi(x)} d\eta = -\frac{\sigma^2}{2\alpha} \frac{\Phi'(x)}{\Phi(x)} + \frac{\nu + k(x - \gamma)}{\alpha} + \frac{\sigma^2}{2} \frac{\Phi'(0) - \Phi(0)(\nu - k\gamma)}{\alpha \Phi(x)},
$$

并且第三项当 $x \to -\infty$ 时趋于 0。

我们将证明以下两个性质

(16.3.37)
$$
-\frac{\Phi'(x)}{\Phi(x)} \to +\infty, \text{ as } x \to -\infty
$$

(16.3.38)
$$
\nu + k(x - \gamma) - \frac{\alpha^2}{2} \frac{\Phi'(x)}{\Phi(x)} \ge \frac{1}{2} B(x), \forall x < \bar{x},
$$

对于某些 $\bar{x} < 0$ 和

$$
B(x) = \frac{\nu + k(x - \gamma) + \sqrt{(\nu + k(x - \gamma))^2 + 2\alpha \sigma^2}}{2}.
$$

显然

(16.3.39)
$$
-B(x)(\nu + k(x - \gamma)) \to \frac{\alpha \sigma^2}{2}, \text{ as } x \to -\infty.
$$

假设我们已经获得了性质 (16.3.37) 和 (16.3.38)。在考虑 $Z(x)$ 当 $x \to -\infty$ 时的行为时，我们寻找主导项。从上述考虑中，我们可以写成

$$
Z(x) = \frac{1}{\alpha} \left[ \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha + k} \left( -\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} + \frac{\sigma^2}{2} \frac{\chi'(0) + \chi(0)(\nu - k\gamma)}{\chi(x)} \right) - \frac{\sigma^2}{2} \frac{\chi'(0) + \chi(0)(\nu - k\gamma)}{\chi(x)} \right] \left[ \frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} + \nu + k(x - \gamma) + \frac{\sigma^2}{2} \frac{\Phi'(0) - \Phi(0)(\nu - k\gamma)}{\Phi(x)} \right].
$$

在第一个括号中，从 (16.3.37) 可以清楚地看出主导项是

$$
\frac{p - c(\alpha + k)}{\alpha + k} \left( - \frac{\Phi'(x)}{\Phi(x)} \right).
$$

在第二个括号中主导项不明显。然而

$$
\frac{\sigma^2}{2} \frac{\Phi'(0) - (\nu - k\gamma)}{\Phi(x)} = \frac{\sigma^2}{2} \frac{\Phi'(0) - (\nu - k\gamma)}{\chi(x)} \vartheta(x).
$$

回顾

$$
\vartheta(x) = \exp -\frac{2}{\sigma^2} \left[ k \frac{(x - \gamma)^2}{2} + \nu x \right],
$$

那么

$$
\frac{\sigma^2}{2} \frac{\Phi'(0) - (\nu - k\gamma)}{\Phi(x)} = B(x) \left[ \frac{\frac{\sigma^2}{2} \Phi'(0) - (\nu - k\gamma) - \vartheta(x)(\nu + k(x - \gamma))}{\chi(x)} \right].
$$

从 (16.3.39)、$\chi(x)$ 的性质和 $\vartheta(x)$ 的值可知括号中的函数当 $x \to -\infty$ 时趋于 0。从 (16.3.38) 很容易得出主导项是

$$
-\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} + \nu + k(x - \gamma),
$$

因此，汇总结果我们可以断言 $Z(x)$ 中的主导项是

$$
\tilde{Z}(x) = \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} \left( - \frac{\Phi'(x)}{\Phi(x)} \right) \left( -\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} + \nu + k(x - \gamma) \right).
$$

定义

$$
u(x) = -\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} + \nu + k(x - \gamma),
$$

那么

(16.3.40)
$$
\tilde{Z}(x) = \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} u(x - (\nu + k(x - \gamma))u).
$$




我们现在通过更精确地研究 $u$ 来证明 (16.3.37) 和 (16.3.38)。首先，由关系式

$$\frac{\sigma^2}{2}\Phi'(0) - (\nu - k\gamma) + \alpha \int_0^{+\infty} \Phi(x) dx = 0$$

我们推导出（回顾 $\Phi(0) = 1$）

$$u(0) > 0.$$

而且，很容易验证 $u(x)$ 是微分方程的解

$$(16.3.41) \quad u' = \frac{2u^2}{\sigma^2} - \frac{2u}{\sigma^2}(\nu + k(x - \gamma)) - \alpha, \quad u(0) > 0.$$

我们首先检验当 $x < 0$ 时 $u(x) > 0$。确实，对于 $x < 0$ 我们可以写出

$$-\frac{\sigma^2}{2}\Phi'(0) + \frac{\sigma^2}{2}\Phi'(x) + \nu - k\gamma - (\nu + k(x - \gamma))\Phi(x) + \alpha \int_x^0 \Phi(y) dy = 0,$$

因此

$$\frac{-\frac{\sigma^2}{2}\Phi'(0) + (\nu - k\gamma)}{\Phi(x)} = u(x) + \alpha \int_x^0 \Phi(y) dy = 0,$$

这意味着当 $x < 0$ 时 $u(x) > 0$。接下来，我们将 (16.3.41) 写为

$$(16.3.42) \quad u' = \frac{2}{\sigma^2}(u(x) - B(x))(u(x) + C(x)),$$

其中

$$C(x) = B(x) - (\nu + k(x - \gamma)).$$

注意

$$B(x)C(x) = \frac{\alpha \sigma^2}{2}.$$

现在考虑

$$v(x) = \frac{u(x)}{B(x)} > 0,$$

它满足微分方程

$$(16.3.43) \quad v' = \frac{2}{\sigma^2}(v - 1)\left(Bv + \frac{\alpha \sigma^2}{2B}\right) - v \frac{k}{\sqrt{(\nu + k(x - \gamma))^2 + 2\alpha \sigma^2}}, \quad x < 0.$$

我们推导出

$$-\frac{1}{2} \frac{d}{dx} ((1 - v)^+)^2 = v'(1 - v)^+ < 0,$$

因此函数 $((1 - v)^+)^2$ 在 $(-\infty, 0)$ 上单调递增。由此可知，如果存在 $\bar{x} < 0$ 使得 $(1 - v)^+(\bar{x}) = 0$，则必然有

$$(1 - v)^+(x) = 0, \quad \forall x < \bar{x}$$

因此，如果 $v(\bar{x}) \ge 1$，则必然有 $v(x) \ge 1$，对所有 $x < \bar{x}$ 成立。现在假设对所有 $x < 0$ 都有 $v(x) < 1$，则由方程 (16.3.43) 可知 $v'(x) < 0$。因此，当 $x \to -\infty$ 时，$v(x)$ 单调递增。它必然收敛到某个 $v^* \le 1$。如果 $v^* < 1$，则由方程可知，当 $x \to -\infty$ 时，$v'(x) \to -\infty$。这产生了矛盾。总结，我们有以下两种情况：要么

$$v(x) \ge 1, \quad \forall x < \bar{x}$$

或

$$v(x) \uparrow 1, \quad \text{as } x \downarrow -\infty$$

由于 \(u(x) = v(x)B(x)\)，我们有以下两种情况：要么

$$u(x) \ge B(x), \quad \forall x < \bar{x}$$

或

$$u(x) - B(x) = (v(x) - 1)B(x) \to 0, \text{ as } x \to -\infty$$

因此，在两种情况下我们都可以断言性质 (16.3.38)。接下来，要么

$$-\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} \ge -(\nu + k(x - \gamma)) + B(x), \forall x \le \bar{x}$$

或

$$-\frac{\sigma^2}{2} \frac{\Phi'(x)}{\Phi(x)} = B(x) + u(x) - B(x) - (\nu + k(x - \gamma)) \to \infty, \text{ as } x \to -\infty.$$

在两种情况下我们都得到性质 (16.3.37)。因此，由 (16.3.40) 给出的 \(\tilde{Z}(x)\) 是 \(Z(x)\) 表达式中的主导项。现在我们可以写出

$$\tilde{Z}(x) = \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} Bu(Bv - (\nu + k(x - \gamma)\nu)$$
$$= \frac{2}{\sigma^2} \frac{p - c(\alpha + k)}{\alpha(\alpha + k)} \left( B^2(x)v(x)(v(x) - 1) + v(x) \frac{\alpha a^2}{2} \right).$$

现在，由于

$$\liminf_{x \to -\infty} v(x) \ge 1,$$

我们可以断言

$$\liminf_{x \to -\infty} \tilde{Z}(x) = \frac{p - c(\alpha + k)}{\alpha + k},$$

因此也有

$$\liminf_{x \to -\infty} Z(x) = \frac{p - c(\alpha + k)}{\alpha + k}$$

这证明了 (16.3.34)，并结束了证明。

## 16.4. Q.V.I 的解

还需证明由 (16.3.1) 和 (16.3.2) 定义的函数 \(G_s(x)\) 是 Q.V.I. (16.2.5) 的解。我们可以陈述

### 定理 16.3. 由 (16.3.1) 和 (16.3.2) 定义的函数 \(G_s(x)\) 是 Q.V.I. (16.2.5) 的解。

证明。我们首先检验互补松弛条件（即 (16.2.5) 的第三个条件）。对于 \(x \le s$，我们有

$$G_s(x) = G_s(s)$$
$$= K + G_s(S(s))$$
$$= K + \inf_{\eta > s} G_s(\eta).$$

但是

$$\inf_{\eta > s} G_s(\eta) = \inf_{\eta > x} G_s(\eta) \quad \forall x \le s.$$

确实，对于 \(x < \eta < s$，有

$$G_s(\eta) = G_s(s) > \inf_{\eta > s} G_s(\eta).$$

因此，我们可以断言

$$G_s(x) = K + \inf_{\eta > x} G_s(\eta) \quad \forall x \le s.$$

显然，互补松弛条件已满足。还需证明

(16.4.1) $$ AG_s(x) + \alpha G_s(x) \le g(x) + c(\nu - k\tau), \quad x < s $$

(16.4.2) $$ G_s(x) \le K + \inf_{\eta > x} G_s(\eta) \quad \forall x \ge s. $$

但是 (16.4.1) 意味着

$$ G_s(s) \le g(x) + c(\nu - k\tau), \quad x < s, $$

并且由公式 (16.3.30) 我们需要证明

$$ g(s) + \frac{\sigma^2}{2} Q(s) \le g(x), \quad x \le s, $$

这成立，因为 \( Q(s) < 0 \) 且 \( x \le s \le 0 \)。

(16.4.2) 的证明与第 15 章定理 15.2 中 (15.3.20) 的证明相同。至此证明结束。\(\square\)

# 双带冲动控制问题

## 17.1. 引言

在前几章中考虑的库存控制问题里，冲动控制是一种补货类型的订购控制。被需求耗尽的库存需要不时地（在冲动时刻）进行补货。存在一些希望减少库存的情况。当存在额外的供给来源时（均值回归规则就是一个例子），就会出现这种情况。此时，积累库存可能不是最优的。一个典型的例子是 Constantinides 和 Richard [17] 引入的现金管理问题。关于另一个应用，参见 Cadenillas 和 Zapatero [15]。本章基于 Bensoussan、Liu 和 Yuan [10]。

### 17.2. 问题

#### 17.2.1. 模型

我们考虑一个概率空间 \(\Omega, \mathcal{A}, P\)，其上定义了一个维纳过程 \(w(t)\)。令 \(\mathcal{F}^t = \sigma(w(s), s \le t)\)。一个冲动控制是一个序列

$$
\theta_n, v_n,
$$

其中 \(\theta_n\) 是相对于滤流 \(\mathcal{F}^t\) 的停时，而 \(v_n\) 是 \(\mathcal{F}^{\theta_n}\) 可测的随机变量。用 \(V\) 表示一个冲动控制，相应的库存由公式描述

$$
(17.2.1) \quad y_t(t; V) = x + \mu t + \sigma w(t) + M(t; V),
$$

其中

$$
M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n
$$

在这个模型中，漂移项 \(\mu t\) 结合了平均需求和固定的再补货政策。数 \(\mu\) 可以是任意实数。

令

$$
f(x) = hx^+ + px^-.
$$

我们通过以下方式定义成本泛函

$$
(17.2.2) \quad J_x(V) = E \left[ \sum_{k=0}^{\infty} C(v_k) \exp -a\theta_n + \int_0^{\infty} f(y_x(t; V)) \exp -adt \right],
$$

其中

$$
(17.2.3) \quad C(v) = K^+ \mathbb{I}_{v>0} + K^- \mathbb{I}_{v<0} + c^+ v^+ + c^- v^-,
$$

其中 \(v^+ = \max(v, 0)\)，\(v^- = -\min(v, 0)\)，且 \(K^+, K^-, c^+, c^-\) 为正常数。注意，上标符号 + 和 - 含义不同。

与之前的模型相反，冲动可以是正的或负的，并且它们受到不同的固定成本和变动成本的约束。

值函数定义为

$$
u(x) = \inf J_x(V).
$$

#### 17.2.2. Q.V.I.

我们写出由动态规划产生的 Q.V.I。我们考虑算子

$$
(17.2.4) \quad Au(x) = -\frac{1}{2}\sigma^2 u''(x) - \mu u'(x).
$$

Q.V.I. 由以下给出

$$
(17.2.5) \quad \begin{aligned} Au(x) + \alpha u(x) \le f(x); \\ u(x) \le M(u)(x); \\ (Au(x) + \alpha u(x) - f(x))(u(x) - M(u)(x)) = 0, \end{aligned}
$$

其中

$$
M(u)(x) = \inf_{v \neq 0} [C(v) + u(x+v)].
$$

我们寻找一个线性增长的 $C^1$ 函数。标准论证表明，Q.V.I. 的解即为值函数。

#### 17.2.3. 变换

定义

$$
\begin{aligned}
M^+ u(x) &= \inf_{v \ge 0} (K^+ \mathbf{1}_{v>0} + c^+ v + u(x+v)); \\
M^- u(x) &= \inf_{v \le 0} (K^- \mathbf{1}_{v<0} - c^- v + u(x+v)),
\end{aligned}
$$

那么

$$
Mu(x) = \min(M^+ u(x), M^- u(x)),
$$

并且 Q.V.I. 可以写成如下形式

$$
(17.2.6) \quad \begin{aligned} Au(x) + \alpha u(x) \le f(x); \\ u(x) \le M^+ u(x); \\ u(x) \le M^- u(x); \\ (Au(x) + \alpha u(x) - f(x))(u(x) - M^+ u(x))(u(x) - M^- u(x)) = 0. \end{aligned}
$$

引入函数

$$
(17.2.7) \quad G^+(x) = u(x) + c^+ x;
$$

$$
(17.2.8) \quad G^-(x) = u(x) - c^- x;
$$

$$
(17.2.9) \quad g^+(x) = f(x) + \alpha c^+ x;
$$

$$
(17.2.10) \quad g^-(x) = f(x) - \alpha c^- x,
$$

那么我们可以将 Q.V.I. 写成两部分

$$
(17.2.11) \quad \begin{aligned} AG^+ + \alpha G^+ \le g^+(x) - c^+ \mu \\ G^+(x) \le K^+ + \inf_{\eta > y} G^+(\eta) \\ (AG^+ + \alpha G^+ - g^+(x) + c^+ \mu)(G^+(x) - K^+ - \inf_{\eta > y} G^+(\eta)) = 0 \\ \text{if } G^-(x) < K^- + \inf_{\eta < y} G^-(\eta) \end{aligned}


$AG^- + \alpha G^- \le g^-(x) + c^- \mu$
$G^-(x) \le K^- + \inf_{\eta < x} G^-(\eta)$
(17.2.12) $(AG^- + \alpha G^- - g^-(x)) \le - \inf_{\eta < x} G^-(\eta)$
if $G^+(x) < K^+ + \inf_{\eta < x} G^+(\eta)$

(17.2.13) $G^+(x) - G^-(x) = (c^+ + c^-)x$

## 17.3. a, A, b, B 策略.

### 17.3.1. 函数 $G_{ab}^+(x)$ 和 $G_{ab}^-(x)$.

推广 (s, S) 策略的思想，我们引入 (a, A, b, B) 策略的概念。首先设 \( a < b \) 为两个实数。我们通过以下准变分不等式（Q.V.I）定义函数 \( G_{ab}^+(x) \) 和 \( G_{ab}^-(x) \)（注意它们是解耦的）

$$(17.3.1) \begin{aligned} AG_{ab}^+ + \alpha G_{ab}^+ &= g^+(x) + c^+ \mu(\eta), \quad \forall a < x < b \\ G_{ab}^+(x) &= K^+ + \inf_{a < \eta < x} c^+(G_{ab}^+(\eta)), \quad \forall x \le a \\ G_{ab}^+(b) &= K^+ + (c^+ + c^-)b + \inf_{a < \eta < b} c^+(G_{ab}^+(\eta) - (c^+ + c^-)\eta) \end{aligned}$$

$$(17.3.2) \begin{aligned} AG_{ab}^- + \alpha G_{ab}^- &= g^-(x) + c^- \mu, \quad \forall a < x < b \\ G_{ab}^-(x) &= K^- + (c^+ + c^-)a + \inf_{a < \eta < x} c^-(G_{ab}^-(\eta)), \quad \forall x \ge b \\ G_{ab}^-(a) &= K^- + (c^+ + c^-)a + \inf_{a < \eta < b} c^-(G_{ab}^-(\eta) + (c^+ + c^-)\eta) \end{aligned}$$

第一个问题定义在域 \((-\infty, b]\) 上，第二个问题定义在域 \([a, +\infty)\) 上。考虑到公共域 \([a, b]\) 上的条件，我们得到带有非局部 Dirichlet 条件的两点边值问题。在这个域上，有关系

(17.3.3) \( G_{ab}^+(x) - G_{ab}^-(x) = (c^+ + c^-)x. \)

从第二个关系 (17.3.1) 我们得到 \( G_{ab}^+(x) \) 在 \( a\) 以下的扩展，从第二个方程 (17.3.2) 我们得到 \( G_{ab}^-(x) \) 在 \( b\) 以外的扩展。利用 (17.3.3) 我们在整条直线上定义 \( G_{ab}^+(x) \) 和 \( G_{ab}^-(x) \)，且关系 (17.3.3) 成立。当 \( a < b\) 为任意数时，我们只能断言 \( G_{ab}^+(x) \) 和 \( G_{ab}^-(x) \) 是连续的。要在整条直线上得到 \( C^1\) 函数，我们需要施加条件

(17.3.4) \( (G_{ab}^+)'(a) = 0, \quad (G_{ab}^-)'(b) = 0, \)

这可以被视为定义 \( a \) 和 \( b \) 的方程。

### 17.3.2. 函数 \( H_{ab}^+(x) \) 和 \( H_{ab}^-(x) \).

下一步是考虑函数

(17.3.5) \( H_{ab}^+(x) = (G_{ab}^+)'(x), \quad H_{ab}^-(x) = (G_{ab}^-)'(x). \)

这些函数是两点边值问题的解

(17.3.6) \( AH_{ab}^+ + \alpha H_{ab}^+ = f' + \alpha c^+, \quad a < x < b, \quad H_{ab}^+(a) = 0, \quad H_{ab}^+(b) = c^+ + c^- \)

(17.3.7) \( AH_{ab}^- + \alpha H_{ab}^- = f' - \alpha c^-, \quad a < x < b, \quad H_{ab}^-(a) = -(c^+ + c^-), \quad H_{ab}^-(b) = 0, \)

并且当然

(17.3.8) \( H_{ab}^+(x) - H_{ab}^-(x) = c^+ + c^- \).

我们通过常数值将 \( H_{ab}^+(x) \) 和 \( H_{ab}^-(x) \) 扩展到区间 \((a, b)\) 之外，使得 (17.3.8) 在整条直线上成立。函数 \( H_{ab}^+(x) \) 和 \( H_{ab}^-(x) \) 在整条直线上是连续的，对于任意一对 $a < b$。定义对 $(a, b)$ 的方程组变为

(17.3.9) 
$$F(a,b) = K^+ + \inf_{a \le x \le b} \int_x^b H_{ab}^+(\xi) d\xi = 0$$

(17.3.10) 
$$G(a,b) = -K^- + \sup_{a \le x \le b} \int_x^b H_{ab}^-(\xi) d\xi = 0.$$

在后续中我们将做如下假设

(17.3.11) 
$$p - \alpha c^+ > 0, \quad h - \alpha c^- > 0.$$

给出 $H_{ab}^+(x)$ 和 $H_{ab}^-(x)$ 的解析公式相当容易。让我们考虑二阶方程

$$-\frac{1}{2}\sigma^2 \beta^2 - \mu\beta + \alpha = 0,$$

及其根

$$\beta_1 = -\frac{\mu - \sqrt{\mu^2 + 2\sigma^2\alpha}}{\sigma^2} > 0, \quad \beta_2 = -\frac{\mu + \sqrt{\mu^2 + 2\sigma^2\alpha}}{\sigma^2} < 0,$$

那么我们有公式

$$H_{ab}^+(x) = Z^+(a,b) \frac{\exp \beta_1(x-a) - \exp \beta_2(x-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} - \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_a^b (f'(\xi) + \alpha c^+) (\exp \beta_1(x-\xi) - \exp \beta_2(x-\xi)) d\xi,$$

其中

$$Z^+(a,b) = c^+ + c^- + \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_a^b (f'(\xi) + \alpha c^+) (\exp \beta_1(b-\xi) - \exp \beta_2(b-\xi)) d\xi;$$

$$H_{ab}^-(x) = -Z^-(a,b) \frac{\exp \beta_1(x-b) - \exp \beta_2(x-b)}{\exp \beta_1(a-b) - \exp \beta_2(a-b)} + \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_x^b (f'(\xi) - \alpha c^-) (\exp \beta_1(x-\xi) - \exp \beta_2(x-\xi)) d\xi,$$

其中

$$Z^-(a,b) = -(c^+ + c^-) + \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_a^b (f'(\xi) - \alpha c^-) (\exp \beta_1(a-\xi) - \exp \beta_2(a-\xi)) d\xi.$$

### 17.3.3. 函数 A(a, b) 和 B(a, b). 我们从

**引理 17.1.** 我们假设 $a < 0 < b$。在第一个假设 (17.3.11) 下，函数 $Z^+(a,b)$ 关于 $a$ 单调递增。而且 $Z^+(0,b) > 0, Z^+(-\infty,b) = -\infty$。类似地，在第二个假设 (17.3.11) 下，函数 $Z^-(a,b)$ 关于 $b$ 单调递增。而且 $Z^-(a,0) < 0$ 且 $Z^-(a,+\infty) = +\infty$。

**证明.** 我们有

$$Z^+(a,b) = -\frac{h-\alpha c^-}{\alpha} + \frac{1}{\alpha(\beta_1 - \beta_2)} [(p+h)(\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b) - (p-\alpha c^+)(\beta_1 \exp \beta_2 (b-a) - \beta_2 \exp \beta_1 (b-a))],$$

因此

\(\frac{\partial Z^+}{\partial a} = \frac{2}{\sigma^2(\beta_1 - \beta_2)}(p - \alpha c^+)(\exp \beta_1(b - a) - \exp \beta_2(b - a)) > 0.\)

显然 \(Z^+(0, b) > 0\)。此外，由此我们推断 \(Z^+(-\infty, b) = -\infty\)。类似地

(17.3.12) \(Z^-(a, b) = \frac{p - \alpha c^+}{\alpha} + \frac{1}{\alpha(\beta_1 - \beta_2)}[-(p + h)(\beta_1 \exp \beta_2 a - \beta_2 \exp \beta_1 a) - (h - \alpha c^-)(\beta_1 \exp \beta_2(a - b) - \beta_2 \exp \beta_1(a - b))],\)

因此

\(\frac{\partial Z^-}{\partial b} = -\frac{2}{\sigma^2(\beta_1 - \beta_2)}(h - \alpha c^-)(\exp \beta_1(a - b) - \exp \beta_2(a - b)) > 0,\)

并且 \(Z^-(a, 0) < 0, Z^-(a, +\infty) = +\infty\)。

### **命题 17.3.1.** 我们假设 (17.3.11) 和 \(a < 0 < b\)。存在唯一的数 \(A(a, b), B(a, b)\) 使得

\(a \le A(a, b) < B(a, b) \le b,\)

且满足

\(H_{ab}^+(x) > 0, \forall x > A(a, b); H_{ab}^+(x) < 0, \forall a < x < A(a, b); H_{ab}^+(A) = 0\)
\(H_{ab}^-(x) > 0, \forall x > B(a, b); H_{ab}^-(x) < 0, \forall x < B(a, b); H_{ab}^-(B) = 0.\)

情况 \(A(a, b) = a\) 或 \(B(a, b) = b\) 是可能的，在这种情况下 \(H_{ab}^+(x) > 0, \forall x > a\) 或 \(H_{ab}^-(x) < 0, \forall x < b\)。

**证明.** 由引理 17.1 可知，存在唯一确定的数 \(a_0(b) < 0\) 和 \(b_0(a) > 0\) 使得

(17.3.13) \(Z^+(a, b) < 0, \forall a < a_0(b); Z^+(a, b) > 0, \forall a_0(b) < a < 0\)

(17.3.14) \(Z^-(a, b) > 0, \forall b > b_0(a); Z^-(a, b) < 0, \forall 0 < b < b_0(a).\)

接下来，从 \(H_{ab}^+(x)\) 的公式中我们得到

\((H_{ab}^+)'(a) = \frac{Z^+(a, b)(\beta_1 - \beta_2)}{\exp \beta_1(b - a) - \exp \beta_2(b - a)},\)

因此 \((H_{ab}^+)'(a)\) 和 \(Z^+(a, b)\) 符号相同。我们推断

\(a_0(b) \le a \Longrightarrow (H_{ab}^+)'(a) \ge 0,\)

我们随后断言 \(H_{ab}^+(x) > 0, \forall x \in (a, b]\). 确实存在一个小区间 \((a, a + \epsilon)\)，其中 \(H_{ab}^+(x) > 0\)。当 \(a > a_0(b)\) 时这很明显，因为 \((H_{ab}^+)'(a) > 0\)。当 \(a = a_0(b)\) 时这也成立，因为 \((H_{ab}^+)'(a) = 0\) 且

\(-\frac{1}{2}\sigma^2(H_{ab}^+)''(a) = -(p - \alpha c^+) < 0.\)

不存在一点 \(\bar{x}\) 满足 \(a < \bar{x} < b\) 且 \(H_{ab}^+(\bar{x}) = 0\)。确实，如果存在这样的点，我们可以考虑最小的这样的点，因此有

\(H_{ab}^+(x) > 0, \forall x \in (a, \bar{x}).\)

必然 \(\bar{x} > 0\)。否则，由于在 \((a, \bar{x})\) 中存在正最大值，在 \((a, 0)\) 中将存在一个局部正最大值，根据最大原理考虑这是不可能的。而且 \((H_{ab}^+)'(\bar{x}) < 0\)。由于 \(H_{ab}^+(b) > 0\)，函数 \(H_{ab}^+(x)\) 在 $(0, b)$ 中有一个负最小值，根据最大原理考虑这也是不可能的。因此我们已经证明了 $H_{ab}^+(x) > 0, \forall x \in (a, b]$. 定义

$A(a, b) = a, \forall a > a_0(b),$

则 $H_{ab}^+(x)$ 的结果得到。我们可以假设 $a < a_0(b)$。那么我们有 $(H_{ab}^+)'(a) < 0$。这意味着对于小区间 $(a, a+\epsilon)$，有 $H_{ab}^+(x) < 0$。由于 $H_{ab}^+(b) > 0$，函数 $H_{ab}^+(x)$ 必须在 $(a, b)$ 中消失。我们可以定义 $A(a, b)$ 为 $(a, b)$ 中最小的点，使得 $H_{ab}^+(A) = 0$。事实上，我们将证明这个点是唯一的，且 $H_{ab}^+(x) > 0, \forall x \in (A, b]$. 我们有 $(H_{ab}^+)'(A) > 0$。因此对于小区间 $(A, A+\epsilon)$，有 $H_{ab}^+(x) > 0$。考虑 $H_{ab}^+(x)$ 在 $[A + \epsilon, b]$ 上的最小值。假设这个最小值 $\le 0$，并令 $x^*$ 为这个最小值。那么根据最大原理考虑，$x^* \le 0$。但这样 $A < 0$ 并且在开区间 $(A, 0)$ 中存在 $H_{ab}^+(x)$ 的一个局部最大值。根据最大原理考虑这是不可能的。因此，对于 $a < a_0(b)$，存在唯一的 $A(a, b)$ 使得 $a < A(a, b) < b$ 且

$H_{ab}^+(x) > 0, \forall x > A(a, b); H_{ab}^+(x) < 0, \forall x < A(a, b); H_{ab}^+(A) = 0.$

类似地，我们可以检查

$b \le b_0(a) \implies H_{ab}^-(x) < 0, \forall x \in [a, b].$

在这种情况下，我们设置 $B(a, b) = b$。否则，如果 $b > b_0(a)$，存在唯一的 $B(a, b)$ 使得 $a < B(a, b) < b$ 且

$H_{ab}^-(x) > 0, \forall x > B(a, b); H_{ab}^-(x) < 0, \forall x < B(a, b); H_{ab}^-(B) = 0.$

根据 (17.3.8) 我们显然有

$A(a, b) < B(a, b).$

证明完成。

### 17.3.4. 函数 $a(b)$ 和 $b(a)$.

我们回顾函数 $F(a, b), G(a, b)$ 的定义，参见 (17.3.9), (17.3.10)。我们将证明

### **命题 17.2.** 我们假设 (17.3.11) 和 $a < 0 < b$。存在唯一的 $a(b) < a_0(b)$ 使得

(17.3.15) $F(a(b), b) = 0,$

以及唯一的 $b(a) > b_0(a)$ 使得

(17.3.16) $G(a, b(a)) = 0.$

为了证明该命题，我们将依赖一些本身也很有趣的中间性质

### **引理 17.2.** 对于 $a \le x \le b$，我们有以下性质

(17.3.17) $\frac{\partial H_{ab}^+(x)}{\partial a} > 0, \forall a < a_0(b); \frac{\partial H_{ab}^+(x)}{\partial a} < 0, \forall a > a_0(b); \frac{\partial H_{ab}^+(x)}{\partial a}|_{a=a_0(b)} = 0$

(17.3.18) $\frac{\partial H_{ab}^-(x)}{\partial b} > 0, \forall b > b_0(a); \frac{\partial H_{ab}^-(x)}{\partial b} < 0, \forall b < b_0(a); \frac{\partial H_{ab}^-(x)}{\partial b}|_{b=b_0(a)} = 0.$





证明。由 \( H_{ab}^+(x) \) 的公式可知，经过虽繁琐但直接的计算得

(17.3.19)

\frac{\partial H_{ab}^+(x)}{\partial a} = Z^+(a,b) \frac{\exp \beta_1(x-b) - \exp \beta_2(x-b)}{(\exp \beta_1(a-b) - \exp \beta_2(a-b))^2 (\beta_1 - \beta_2)} \cdot \exp(\beta_1 + \beta_2)(a-b),

同样地

(17.3.20)

\frac{\partial H_{ab}^-(x)}{\partial b} = Z^-(a,b) \frac{\exp \beta_1(x-a) - \exp \beta_2(x-a)}{(\exp \beta_1(b-a) - \exp \beta_2(b-a))^2 (\beta_1 - \beta_2)} \cdot \exp(\beta_1 + \beta_2)(b-a).

因此，由 (17.3.13) 和 (17.3.14) 可断言

(17.3.21)

\frac{\partial H_{ab}^+(x)}{\partial a} > 0, \text{ if } a < a_0(b); \frac{\partial H_{ab}^+(x)}{\partial a} < 0, \text{ if } a > a_0(b); \frac{\partial H_{ab}^+(x)}{\partial a}|_{a=a_0(b)}

(17.3.22)

\frac{\partial H_{ab}^+(x)}{\partial b} > 0, \text{ if } b > b_0(a); \frac{\partial H_{ab}^-(x)}{\partial b} < 0, \text{ if } b < b_0(a); \frac{\partial H_{ab}^-(x)}{\partial b}|_{b=b_0(a)}

### 命题 17.2 的证明：

接下来考虑由 (17.3.9) 和 (17.3.10) 定义的 \( F(a,b) \) 和 \( G(a,b) \)。我们首先注意到

(17.3.23)

F(a,b) = K^+, \text{ if } a \ge a_0(b); G(a,b) = -K^-, \text{ if } b \le b_0(a).

接下来，对于 \( a < a_0(b) \)

\frac{\partial F(a,b)}{\partial a} = \int_a^{A(a,b)} \frac{\partial H_{ab}^+(x)}{\partial a} dx > 0,

由 (17.3.21) 得。同样地，对于 \( b > b_0(a) \) 有人

\frac{\partial G(a,b)}{\partial b} = \int_{B(a,b)}^b \frac{\partial H_{ab}^-(x)}{\partial b} dx > 0.

因此 \( F(a,b) \) 在 \( (-\infty, a_0(b)) \) 上关于 \( a \) 严格单调递增，在 \( [a_0(b), 0] \) 上为常数。同样地 \( G(a,b) \) 在 \( [0, b_0(a)] \) 上为常数，在 \( (b_0(a), +\infty) \) 上关于 \( b \) 严格单调递增。接下来通过证明

(17.3.24)

F(-\infty, b) = -\infty, G(a, +\infty) = +\infty.

单调性性质和 (17.3.23)、(17.3.24) 立即蕴含 \( a(b) \) 和 \( b(a) \) 的存在性和唯一性，使得 (17.3.15) 和 (17.3.16) 成立。尚需证明 (17.3.24)。我们仅证明第一部分。第二部分类似。给出 \( H_{ab}^+(x) \) 和 \( H_{ab}^-(x) \) 的显式公式很有用。可得

当 \( x > 0 \) 时，

\( H_{ab}^+(x) = (c^+ + c^-) \frac{\exp \beta_1(x-a) - \exp \beta_2(x-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \frac{h + \alpha c^+}{\alpha} \frac{\exp \beta_1(x-a) - \exp \beta_2(x-a) - \exp \beta_1(b-a) + \exp \beta_2(b-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \frac{p+h}{\alpha(\beta_1 - \beta_2)} \frac{(\exp(\beta_2 x + \beta_1 b) - \exp(\beta_1 x + \beta_2 b))(\beta_1 \exp \beta_1 a - \beta_1 a - \beta_2 \exp -\beta_2 a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \frac{p - \alpha c^-}{\alpha} \exp -(\beta_1 + \beta_2)a \frac{\exp(\beta_2 x + \beta_1 b) - \exp(\beta_1 x + \beta_2 b)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \)

而当 \( x < 0 \) 时，

\( H_{ab}^+(x) = \frac{\exp \beta_1(x-a) - \exp \beta_2(x-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \left[ \frac{h - \alpha c^-}{\alpha} \right. \left. + \frac{p+h}{\alpha} \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\beta_1 - \beta_2} \right] + \frac{p - \alpha c^+}{\alpha} \frac{\exp \beta_1(b-a)(\exp \beta_2(x-a) - 1) - \exp \beta_2(b-a)(\exp \beta_1(x-a) - 1)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \)

同样地，我们陈述：
当 \( x > 0 \) 时，

\( H_{ab}^-(x) = \frac{\exp \beta_1(x-b) - \exp \beta_2(x-b)}{\exp \beta_1(a-b) - \exp \beta_2(a-b)} \left[ \frac{p - \alpha c^+}{\alpha} \right. \left. - \frac{p+h}{\alpha} \frac{\beta_1 \exp \beta_2 a - \beta_2 \exp \beta_1 a}{\beta_1 - \beta_2} \right] + \frac{h - \alpha c^-}{\alpha} \frac{\exp \beta_2(a-b)(\exp \beta_1(x-b) - 1) - \exp \beta_1(a-b)(\exp \beta_2(x-b) - 1)}{\exp \beta_1(a-b) - \exp \beta_2(a-b)} \)

而当 \( x < 0 \) 时，

\( H_{ab}^-(x) = -(c^+ + c^-) \frac{\exp \beta_1(b-x) - \exp \beta_2(b-x)}{\exp \beta_1(a-b) - \exp \beta_2(a-b)} + \frac{p + \alpha c^-}{\alpha} \frac{\exp \beta_1(x-b) - \exp \beta_2(x-b) - \exp \beta_1(a-b) + \exp \beta_2(a-b)}{\exp \beta_1(a-b) - \exp \beta_2(b-a)} + \frac{p+h}{\alpha(\beta_1 - \beta_2)} \frac{(\exp(\beta_2 x + \beta_1 a) - \exp(\beta_1 x + \beta_2 a))(\beta_1 \exp \beta_1 b - \beta_1 b - \beta_2 \exp -\beta_2 b)}{\exp \beta_1(a-b) - \exp \beta_2(b-a)} \frac{h - \alpha c^-}{\alpha} \exp -(\beta_1 + \beta_2)b \frac{\exp(\beta_2 x + \beta_1 a) - \exp(\beta_1 x + \beta_2 a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} \)

由此立即可推出：
当 \( x \le 0 \) 时，

\( H_{-\infty b}^+(x) = -\frac{h - \alpha c^-}{\alpha} \exp \beta_1(x-b) - \frac{p - \alpha c^+}{\alpha} + \frac{h+p}{\alpha(\beta_1 - \beta_2)} \exp \beta_1(x-b)(\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b), \)

故

\( H_{-\infty b}^+(x) \to -\frac{p - \alpha c^+}{\alpha} \quad \text{as} \quad x \to -\infty, \)

且 $H^+_{-\infty}(b) = c^+ + c^-$。因此点 $A(-\infty, b)$ 定义良好且有限。由此可知
$$
\int_{-\infty}^{A(-\infty, b)} H^+_{-\infty}(\xi) d\xi = -\infty,
$$
故 (17.3.24) 的第一部分已得证。第二部分以类似方式证明。命题的证明已完成。

## 17.3.5. 求 a 和 b。

我们寻找点 $a \le 0$ 和 $b \ge 0$ 使得 (17.3.9)、(17.3.10) 成立。我们首先给出 $F(a, b)$、$G(a, b)$ 的完整表达式。当然，我们知道 (17.3.23)。因此我们考虑 $a < a_0(b)$ 和 $b > b_0(a)$。有人
$$
F(a, b) = K^+ + \int_a^A H^+_{ab}(x) dx.
$$

由方程 (17.3.6) 得
$$
-\frac{\sigma^2}{2}((H^+_{ab})'(A) - (H^+_{ab})'(a)) + \alpha \int_a^A H^+_{ab}(x) dx = \int_a^A (f'(x) + \alpha c^+) dx.
$$

利用 $\beta_1 \beta_2 = -\frac{2\alpha}{\sigma^2}$ 还得
$$
\int_a^A H^+_{ab}(x) dx = \frac{1}{\alpha} \int_a^A (f'(x) + \alpha c^+) dx - \frac{1}{\beta_1 \beta_2} ((H^+_{ab})'(A) - (H^+_{ab})'(a)).
$$

接下来，由 $H^+_{ab}(x)$ 的公式可断言
(17.3.25)
$$
(H^+_{ab})'(x) = Z^+(a, b) \frac{\beta_1 \exp \beta_1(x-a) - \beta_2 \exp \beta_2(x-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} - \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_x^A (f'(\xi) + \alpha c^+) (\beta_1 \exp \beta_1(x-\xi) - \beta_2 \exp \beta_2(x-\xi)) d\xi
$$

故
$$
(H^+_{ab})'(A) - (H^+_{ab})'(a) = Z^+(a, b) \frac{(\beta_1 \exp \beta_1(A-a) - 1) - \beta_2 (\exp \beta_2(A-a) - 1)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} - \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_a^A (f'(\xi) + \alpha c^+) (\beta_1 \exp \beta_1(A-\xi) - \beta_2 \exp \beta_2(A-\xi)) d\xi.
$$

另一方面，由于 $H^+_{ab}(A) = 0$，也可写成
$$
Z^+(a, b) \frac{\exp \beta_1(A-a) - \exp \beta_2(A-a)}{\exp \beta_1(b-a) - \exp \beta_2(b-a)} = \frac{2}{\sigma^2(\beta_1 - \beta_2)} \int_a^A (f'(\xi) + \alpha c^+) (\exp \beta_1(A-\xi) - \exp \beta_2(A-\xi)) d\xi.
$$

综合得
$$
(H^+_{ab})'(A) - (H^+_{ab})'(a) = \frac{2}{\sigma^2} \int_a^A (f'(x) + \alpha c^+) \frac{\exp \beta_1(A-x)(\exp \beta_2(A-a) - 1) - \exp \beta_2(A-x)(\exp \beta_1(A-a) - 1)}{\exp \beta_1(A-a) - \exp \beta_2(A-a)} dx.
$$

因此

\( F(a,b) = K^+ + \frac{1}{\alpha} \int_a^A (f'(x) + \alpha c^+) dx + \frac{1}{\alpha} \int_a^A (f'(x) + \alpha c^+) \frac{\exp \beta_1(A-x)(\exp \beta_2(A-a) - 1) - \exp \beta_2(A-x)(\exp \beta_1(A-a) - 1)}{\exp \beta_1(A-a) - \exp \beta_2(A-a)} dx. \)

计算积分，最终得

\( F(a,b) = K^+ + \frac{1}{\alpha}((-p + \alpha c^+)(A - a) + (h + p)A^+) + \frac{1}{\alpha} \frac{p - \alpha c^+}{\beta_1 \beta_2} (\beta_1 - \beta_2) \frac{(\exp \beta_1(A - a) - 1)(\exp \beta_2(A - a) - 1)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)} + \frac{1}{\alpha} \frac{p + h}{\alpha} \frac{\beta_1 (\exp \beta_1(A - a) - 1)(1 - \exp \beta_2 A^+) - \beta_2 (\exp \beta_2 A^+) - \beta_2 (\exp \beta_2(A - a) - 1)(1 - \exp \beta_1 A^+)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)}. \)

同样地，我们可以给出 \( G(a, b) \) 的公式

\( G(a,b) = -K^- + \frac{1}{\alpha}((h\alpha - c^-)(B - b) - (h + p)B^-) + \frac{1}{\alpha} \frac{h - \alpha c^-}{\beta_1 \beta_2} (\beta_1 - \beta_2) \frac{(\exp \beta_1(B - b) - 1)(\exp \beta_2(B - b) - 1)}{\exp \beta_1(B - b) - \exp \beta_2(B - b)} + \frac{1}{\alpha} \frac{p + h}{\alpha} \frac{\beta_1 (\exp \beta_1(B - b) - 1)(1 - \exp \beta_2 B^-) - \beta_2 (\exp \beta_2 B^-) - \beta_2 (\exp \beta_2(B - b) - 1)(1 - \exp \beta_1 B^-)}{\exp \beta_1(B - b) - \exp \beta_2(B - b)}. \)

我们可以陈述

### 命题 17.3. 我们假设 (17.3.11)。系统 (17.3.9)、(17.3.10) 存在一个解 \( a < 0 < b \)。

### 证明。函数 \( A(a,b), B(a,b) \) 和 \( F(a,b), G(a,b) \) 是连续的。而且我们有 (17.3.24)。由此可知函数 \( a(b) \) 和 \( b(a) \) 是连续的。确实，如果 \( b_n \to b \) 且 \( a_n = a(b_n) \)，则序列 \( a_n \) 必须有界。否则将存在一个收敛于 \( -\infty \) 的子序列，但对于该子序列 \( F(a_n, b_n) \to F(-\infty, b) = -\infty \)，这是不可能的，因为 \( F(a_n, b_n) = 0 \)。由此容易看出序列 \( a_n, b_n \) 的唯一聚点是 \( a(b), b \)。因此 \( a(b_n) \to a(b) \)，这证明了映射 \( b \to a(b) \) 的连续性。类似的证明适用于映射 \( a \to b(a) \)。现在，系统 (17.3.9)、(17.3.10) 的一个解满足 \( u(a) = u(b(a)) = 0 \)。

函数 \( u(a) \) 是连续的且 \( u(0) = a(b(0)) < 0 \)。让我们验证

(17.3.26) \( u(-\infty) = +\infty. \)

如果这是真的，那么函数 \( u(a) \) 穿过直线 0 且存在 \( \hat{a} \) 使得 \( u(\hat{a}) = 0 \)。那么 \( \hat{a} \) 和 \( b = b(\hat{a}) \) 是 (17.3.9)、(17.3.10) 的一个解。为了证明 (17.3.26)，只需检查 \( b(-\infty) \) 是有限的。然而如果 \( b(-\infty) = +\infty \) 则 \( G(-\infty, +\infty) = 0 \)。这从 (17.3.24) 看来是不可能的。证明已完成。

### 注释 17.1. 我们不声称点 \( a, b \) 的唯一性，尽管这很可能。





## 17.4. Q.V.I. 的解

从 $(a, A, B, b)$ 策略出发，我们将构造满足 (17.2.11)、(17.2.12)、(17.2.13) 的 $G^+(x), G^-(x)$。我们定义

(17.4.1)
$$
G^+_{ab}(x) = G^+_{ab}(a), \forall x \le a; \quad G^+_{ab}(x) = G^+_{ab}(a) + \int_a^x H^+_{ab}(\xi) d\xi, \forall x \ge a
$$

(17.4.2)
$$
G^-_{ab}(x) = G^-_{ab}(b), \forall x \ge b; \quad G^-_{ab}(x) = G^-_{ab}(b) - \int_x^b H^-_{ab}(\xi) d\xi, \forall x \le b,
$$

其中

(17.4.3)
$$
G^+_{ab}(a) = \frac{g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a)}{\alpha};
$$

(17.4.4)
$$
G^-_{ab}(b) = \frac{g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b)}{\alpha}.
$$

我们首先验证

(17.4.5)
$$
G^+_{ab}(x) - G^-_{ab}(x) = (c^+ + c^-)x.
$$

由于

$(G^+_{ab})'(x) - (G^-_{ab})'(x) = H^+_{ab}(x) - H^-_{ab}(x) = c^+ + c^-$，

只需验证

(17.4.6)
$$
G^+_{ab}(a) - G^-_{ab}(a) = (c^+ + c^-)a.
$$

使用

$$
\begin{aligned}
G^-_{ab}(a) &= G^-_{ab}(b) - \int_a^b H^-_{ab}(\xi) d\xi \\
&= G^-_{ab}(b) - \int_a^b H^+_{ab}(\xi) d\xi + (c^+ + c^-)(b - a),
\end{aligned}
$$

以及公式 (17.4.3)、(17.4.4)，我们必须验证关系

$$
\begin{aligned}
g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a) \\
= g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b) - a \int_a^b H^+_{ab}(\xi) d\xi + \alpha(c^+ + c^-)b,
\end{aligned}
$$

或

$$
-\frac{\sigma^2}{2}((H^-_{ab})'(b) - (H^+_{ab})'(a)) + \alpha \int_a^b H^+_{ab}(\xi) d\xi - (c^+ + c^-) \mu = f(b) - f(a) + \alpha c^+(b - a),
$$

这直接由 (17.3.6) 在 $a$ 和 $b$ 之间积分后得出。函数 $G^+_{ab}(x)$ 和 $G^-_{ab}(x)$ 满足 (17.3.1)、(17.3.2)、(17.3.3)。我们然后定义

我们注意到

$$
\begin{aligned}
AG^+(x) + \alpha G^+(x) &= g^+(x) - c^+ \mu, & \forall a < x < b \\
G^+(x) &= G^+_{ab}(a), & \forall x \le a \\
G^+(x) &= G^-_{ab}(b) + (c^+ + c^-)x, & \forall x \ge b
\end{aligned}
$$

因此，对于 \( x < a \)

\( AG^+(x) + \alpha G^+(x) = g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H_{ab}^+)'(a) \)。

接下来我们使用 \( (H_{ab}^+)'(a) < 0 \) 和

\( g^+(x) = f(x) + \alpha c^+ x = (-p + \alpha c^+)x \)
\( \ge (-p + \alpha c^+)a = g^+(a) \)

从而得出

\( AG^+(x) + \alpha G^+(x) \le g^+(x) - c^+ \mu, \quad \forall x < a \)。

对于 \( x > b \)，我们有

\( AG^+(x) + \alpha G^+(x) = -\mu(c^+ + c^-) + \alpha(c^+ + c^-)x \)
\( + g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H_{ab}^+)'(b) \)。

然后我们使用 \( (H_{ab}^+)'(b) < 0 \) 和

\( g^-(b) = f(b) - \alpha c^- b = (h - \alpha c^-)b \le (h - \alpha c^-)b \)
\( = g^-(x) = g^+(x) - \alpha(c^+ + c^-)x \),

同样得出

\( AG^+(x) + \alpha G^+(x) \le g^+(x) - c^+ \mu, \quad \forall x > b \)。

接下来我们注意到，由于 $a, b$ 的选择，我们有

\( G_{ab}^+(a) = K^+ + \inf_{a < \eta < b} G_{ab}^+(\eta) \)

对于 \( x \le a \),

\( G^+(x) = G_{ab}^+(a) = K^+ + \inf_{a < \eta < b} G^+(\eta) \)
\( = K^+ + \inf_{x < \eta < b} G^+(\eta) = K^+ + \inf_{x < \eta} G^+(\eta) \)。

对于 \( x > a \)，要证明同样的不等式，我们需要验证

(17.4.7)
$$
0 \le K^+ + \inf_{x < \eta} \int_x^\eta H_{ab}^+(\xi) d\xi.
$$

对于 \( x > A $，这很明显，因为积分为正。因此我们可以考虑 $a \le x \le A$ 的情况。但此时

\( K^+ + \inf_{x < \eta} \int_x^\eta H_{ab}^+(\xi) d\xi = K^+ + \int_x^A H_{ab}^+(\xi) d\xi \)
\( \ge K^+ + \int_A^A H_{ab}^+(\xi) d\xi = 0 \)。

因此得到 (17.4.7)。考虑到 (17.2.11)，我们看到前两个不等式已满足。以同样的方式，我们验证 (17.2.12) 的前两个不等式也满足。最后，考虑三个区间 $(-\infty, a)$、$(a, b)$、$(b, +\infty)$，我们看到 (17.4.7) 和 (17.2.12) 中的第三个关系也满足。因此，我们通过 $(a, A, B, b)$ 策略找到了 Q.V.I. (17.2.11)、(17.2.12)、(17.2.13) 的一个解，从而也找到了 (17.2.6) 的解。

## 17.5. 计算方面

本节我们关注与求得四个数 $a, A, B, b$ 相关的计算方面。

### 17.5.1. A 和 B 的符号

我们知道 $A < B$ 且 $a < 0, b > 0$，但无法保证 $A, B$ 的符号。进一步研究这个问题很有意思。这也会在计算四个数时带来简化。考虑固定 $b$ 时求 $a(b)$。我们需要求解 $F(a(b), b) = 0$。但观察公式 (17.5.13) 可知，$F(a(b))$ 对 $b$ 的依赖仅通过 $A(a, b)$ 体现。因此，对于固定的 $b$，对子 $a(b), A(a(b), b)$ 可通过以下方程组求得

(17.5.1)
$$
F(a, b) = 0, H_{\alpha}^{+}(a) = 0.
$$

在求解该方程组时，计算过程取决于所求解 $A$ 的符号。若假设 $A < 0$，则对子 $a, A$ 成为下列方程组的解（回顾，在此框架下我们省略了写出固定正参数 $b$）

$$
K^{+} - \frac{1}{\alpha}(p - \alpha c^{+})(A - a) + \frac{1}{\alpha} \frac{p - \alpha c^{+}}{\beta_1 \beta_2} (\beta_1 - \beta_2) \frac{(\exp \beta_1(A - a) - 1)(\exp \beta_2(A - a) - 1)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)} = 0
$$

$$
h - \alpha c^{+} - (p + h) \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\beta_1 - \beta_2} = (p - \alpha c^{+}) \frac{\exp \beta_1(b - a)(\exp \beta_2(A - a) - 1) - \exp \beta_2(b - a)(\exp \beta_1(A - a) - 1)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)}.
$$

此外，该方程组是逐次求解的。第一个方程定义 $A - a$ 且与 $b$ 无关。第二个方程将 $a$ 定义为 $b$ 的函数以及由第一个方程得到的 $A - a$ 的值。若定义函数

(17.5.2)
$$
Z(x) = -x + \frac{\beta_1 - \beta_2}{\beta_1 \beta_2} \frac{(\exp \beta_1 x - 1)(\exp \beta_2 x - 1)}{\exp \beta_1 x - \exp \beta_2 x},
$$

则第一个条件等价于

(17.5.3)
$$
Z(A - a) = \frac{-K^{+}\alpha}{p - \alpha c^{+}}.
$$

我们有

**引理 17.3.3.** 存在唯一的数 $\varpi > 0$，使得

(17.5.4)
$$
Z(\varpi) = \frac{-K^{+}\alpha}{p - \alpha c^{+}}.
$$

证明。我们计算

$$
Z'(x) = -1 + \frac{\beta_1 - \beta_2}{\beta_1 \beta_2} \frac{\beta_2 \exp \beta_2 x (\exp \beta_1 x - 1)^2 - \beta_1 \exp \beta_1 x (\exp \beta_2 x - 1)^2}{(\exp \beta_1 x - \exp \beta_2 x)^2}
$$
$$
= \frac{[\beta_2 (\exp \beta_1 x - 1) - \beta_1 (\exp \beta_2 x - 1)]}{\beta_1 \beta_2 (\exp \beta_1 x - \exp \beta_2 x)^2} \frac{[\beta_1 \exp \beta_1 x (\exp \beta_2 x - 1) - \beta_2 \exp \beta_2 x (\exp \beta_1 x - 1)]}{\beta_1 \beta_2 (\exp \beta_1 x - \exp \beta_2 x)^2}
$$

我们容易验证，对于 $x > 0$
$$
\beta_2(\exp \beta_1 x - 1) - \beta_1(\exp \beta_2 x - 1) < 0
$$
$$
\beta_1 \exp \beta_1 x (\exp \beta_2 x - 1) - \beta_2 \exp \beta_2 x (\exp \beta_1 x - 1) < 0
$$
因此 $Z'(x) \le 0$。此外，$Z(0) = 0$ 且 $Z(+\infty) = -\infty$。这蕴含了结果。

由 (17.5.3) 可断言
(17.5.5)
$$
A(a(b), b) - a(b) = \varpi \quad \text{if } A(a(b), b) \le 0.
$$

回到第二个条件，我们可以写出
(17.5.6)
$$
\begin{aligned}
h - \alpha c^- - (p+h) \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\exp \beta_1 b - \exp \beta_2 b} &= (p - \alpha c^+) \ \frac{\exp \beta_1 b (a-b) (\exp \beta_2 \varpi - 1) - \exp \beta_2 b (a-b) (\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}
\end{aligned}
$$

这将 $a$ 定义为 $b$ 的函数。让我们引入数
(17.5.7)
$$
\varphi(\varpi) = \frac{\beta_1(\exp \beta_2 \varpi - 1) - \beta_2(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi},
$$

则有
$$
\varphi(\varpi) + \beta_1 = \frac{(\beta_1 - \beta_2)(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}; \quad \varphi(\varpi) + \beta_2 = \frac{(\beta_1 - \beta_2)(\exp \beta_2 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi},
$$

且 (17.5.6) 变形后变为
(17.5.8)
$$
L_\varpi(b-a) = \frac{\alpha(c^+ + c^-)(\beta_2 - \beta_1) + (p+h)[\beta_2(\exp \beta_1 b - 1) - \beta_1(\exp \beta_2 b - 1)]}{p - \alpha c^+},
$$

其中
(17.5.9)
$$
L_\varpi(x) = (\exp \beta_1 x - 1)(\varphi(\varpi) + \beta_2) - (\exp \beta_2 x - 1)(\varphi(\varpi) + \beta_1), \quad x \ge 0.
$$

我们也可以给出方程 (17.5.8) 的另一种表述。回顾 $Z^+(a, b)$ 的定义，我们容易验证 (17.5.8) 等价于

(17.5.10)
$$
\frac{Z^+(a, b)}{\exp \beta_1 b (a - b) - \exp \beta_2 b (a - b)} = \frac{\varphi(\varpi) - \alpha c^+}{\alpha(\beta_2 - \beta_1)}.
$$

现在，我们容易验证 $\varphi(0) = 0$。由 (17.3.13) 可知，当 $\varpi = 0$ 时，$a_0(b)$ 是 (17.5.10) 的唯一解。更一般地，我们提出

**引理 17.4.** 对于任何 $\varpi \ge 0$，存在唯一的 $a_\varpi(b)$ 解满足 (17.5.10)。

证明。当然，考虑方程 (17.5.8) 是等价的。函数 $L_\varpi(x)$ 满足

$$
\begin{aligned}
L'_\varpi(x) &= \beta_1(\varphi(\varpi) + \beta_2) \exp \beta_1 x - \beta_2(\varphi(\varpi) + \beta_1) \exp \beta_2 x; \\
L''_\varpi(x) &= (\beta_1)^2(\varphi(\varpi) + \beta_2) \exp \beta_1 x - (\beta_2)^2(\varphi(\varpi) + \beta_1) \exp \beta_2 x.
\end{aligned}
$$

我们注意到

(17.5.11)
$$
\varphi(\varpi) > 0, \quad \varphi(\varpi) + \beta_2 < 0,
$$

因此 $L''_\varpi(x)$ 是递减的，且

$$
L'_\varpi(0) = (\beta_1 - \beta_2)\varphi(\varpi), \quad L'_\varpi( +\infty ) = -\infty.
$$




由此可见，\( L'_{\varpi}(x) \) 在正点 \( \tilde{x} \) 处消失，且

\( L'_{\varpi}(x) > 0, \forall 0 \le x < \tilde{x}, \quad L'_{\varpi}(x) < 0, \forall x > \tilde{x} \)

由于 \( L_{\varpi}(0) = 0 \) 且 \( L_{\varpi}(+\infty) = -\infty \)，函数 \( L_{\varpi}(x) \) 在 \( \tilde{x} \) 处取得最大值，并在点 \( x^* > \tilde{x} \) 处有唯一的0。当 \( x > x^* \) 时，它严格为负；当 \( 0 < x < x^* \) 时，它为正。我们容易验证(17.5.8)右边为负且小于 \( L_{\varpi}(b) \)。因此，存在且仅存在一个 \( a_{\varpi}(b) \) 是(17.5.8)的解。

类似地，对于给定的 \( a \)，对 \( b(a) \) 和 \( B(a,b(a)) \) 是以下方程的解：

(17.5.12) \( G(a,b) = 0, \quad H_{\varpi b}(B) = 0, \)

并且当 \( B > 0 \) 时，我们得到类似于上述 \( A < 0 \) 情况的简化。从 \( G(a,b) \) 的公式中，我们可以写出

(17.5.13) \( -K^- + \frac{1}{\alpha}(h-ac^-)(-B) + \frac{1}{\alpha} \frac{h-ac^-}{\beta_1 \beta_2}(\beta_1 - \beta_2) \frac{(\exp \beta_1(B-b) - 1)(\exp \beta_2(B-b) - 1)}{\exp \beta_1(B-b) - \exp \beta_2(B-b)} = 0 \)

这导出 \( b - B = \pi \)，其中 \( \pi > 0 \) 是以下方程的解：

(17.5.14) \( Z(\pi) = \frac{-K^-}{h - ac^-} . \)

同样，从 \( H_{\varpi b}(B) \) 的公式中，利用函数 \( \varphi \) 的定义（参见(17.5.7)），我们得到

(17.5.15) \( L_{-\pi}(a-b) = \frac{a(c^+ + c^-)(\beta_2 - \beta_1) + (p + h)[\beta_2(\exp \beta_1 a - 1) - \beta_1(\exp \beta_2 a - 1)]}{h - ac^-} . \)

我们注意到

(17.5.16) \( \varphi(-\pi) < 0, \quad \varphi(-\pi) + \beta_1 > 0 . \)

我们看到 \( L'_{-\pi}(x) \) 在 \( x < \tilde{x} < 0 \) 时为正，在 \( x > \tilde{x} \) 时为负。我们有 \( L_{-\pi}(0) = 0 \) 且 \( L_{-\pi}(-\infty) = -\infty \)。注意到(17.5.15)右边为负且小于 \( L_{-\pi}(a) \)，方程(17.5.15)对任意 \( \pi \ge 0 \) 唯一地定义了一个正数 \( b_{\pi}(a) \)。汇总结果，我们可以给出

### 提议 17.4. 我们假设(17.3.11)。那么，对于(17.5.4)的解 \( \varpi \)，有

(17.5.17) \( a_{\varpi}(b) + \varpi < 0 \implies a(b) = a_{\varpi}(b), A(a(b), b) = a_{\varpi}(b) + \varpi , \)

并且对于(17.5.14)的解 \( \pi \)，有

(17.5.18) \( b_{\pi}(a) - \pi > 0 \implies b(a) = b_{\pi}(a), A(a, b(a)) = b_{\pi}(a) - \pi . \)

**证明。** 在假设下，\( a_{\varpi}(b), a_{\varpi}(b) + \varpi \) 和 \( b_{\pi}(a), b_{\pi}(a) - \pi \) 分别是(17.5.1)和(17.5.12)的唯一解。

### 17.5.2. \(a_{\varpi}(b)\) 和 \(b_{\pi}(a)\) 的性质。

我们将证明提议17.5。我们假设(17.3.11)。那么 \(a'_{\varpi}(b) = b'_{\pi}(0) = 1\)。存在唯一点 \(b^*_{\varpi} > 0\) 和 \(a^*_{\pi} < 0\)，使得 \(a'_{\varpi}(b^*_{\varpi}) = b'_{\pi}(a^*_{\pi}) = 0\)。

函数 \(a_{\varpi}(b)\) 在 \((0, b^*_{\varpi})\) 上递增，在 \((b^*_{\varpi}, +\infty)\) 上递减。函数 \(b_{\pi}(a)\) 在 \((-\infty, a^*_{\pi})\) 上递减，在 \((a^*_{\pi}, 0)\) 上递增。而且，

(17.5.19) \(a_{\varpi}(b) < a_0(b), \forall b > 0, b_{\pi}(a) > b_0(a), \forall a < 0.\)

**证明。** 我们可以从(17.5.8)计算 \(a'_{\varpi}(b)\)。我们也使用(17.5.8)来合并项。重排后我们得到

(17.5.20) \(a'_{\varpi}(b) = \frac{\beta_1 - \beta_2}{p - ac^+} \frac{(p - ac^+) \exp \beta_2(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_1) - (p + h)\beta_1 \exp \beta_2 b + \beta_1(h - ac^-)}{p \beta_1 \exp \beta_1(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_2) - \beta_2 \exp \beta_2(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_1)}.\)

还要注意

\(1 - a'_{\varpi}(b) = \frac{p + h}{p - ac^+} \frac{\beta_1 \beta_2(\exp \beta_1 b - \exp \beta_2 b)}{\beta_1 \exp \beta_1(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_2) - \beta_2 \exp \beta_2(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_1)},\)

由此我们得到 \(a'_{\varpi}(0) = 1\)，并且对于足够大的 \(b\)，有 \(a'_{\varpi}(b) < 0\)。

让我们检查是否存在唯一点 \(b\) 使得 \(a'_{\varpi}(b) = 0\)。为简化记号，我们称其为 \(b\)。从(17.5.20)我们得到

(17.5.21) \(\exp -\beta_2 a_{\varpi}(b) = \frac{\beta_1}{\varphi(\varpi) + \beta_1} \frac{p + h - (h - ac^-) \exp -\beta_2 b}{p - ac^+}.\)

但结合(17.5.8)（重写为）

\((p - ac^+) \exp \beta_2(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_1) - (p + h)\beta_1 \exp \beta_2 b = (p - ac^+) \exp \beta_1(b - a_{\varpi}(b))((\varphi(\varpi) + \beta_2) - (p + h)\beta_2 \exp \beta_1 b + (h - ac^-)(\beta_2 - \beta_1)),\)

我们还有

(17.5.22) \(\exp -\beta_1 a_{\varpi}(b) = \frac{\beta_2}{\varphi(\varpi) + \beta_2} \frac{p + h - (h - ac^-) \exp -\beta_1 b}{p - ac^+}.\)

然后我们可以消去 \(a_{\varpi}(b)\) 并得到关于 \(b\) 值的方程。我们有

\((p + h - (h - ac^-) \exp -\beta_2 b)(p + h - (h - ac^-) \exp -\beta_1 b)^{\frac{\beta_2}{\beta_1}} = \frac{\varphi(\varpi) + \beta_1}{\beta_1} \left( \frac{\varphi(\varpi) + \beta_2}{\beta_2} \right)^{-\frac{\beta_2}{\beta_1}} (p - ac^+)^{-1 + \frac{\beta_2}{\beta_1}}\)

让我们检查(17.5.23)是否定义了唯一的正值 \(b\)。首先，右边是0和 \((p - ac^+)^{-1} \frac{\beta_2}{\beta_1}\) 之间的一个数。这源于性质

\(0 < \left(1 + \frac{x}{\beta_1}\right) \left(1 + \frac{x}{\beta_2}\right)^{-\frac{\beta_2}{\beta_1}} < 1, \forall 0 < x < -\beta_2.\)

另一方面，(17.5.23)左边在参数 \(b\) 在 \([0, \infty)\) 上从 \((p + ac^-)^{-1} \frac{\beta_2}{\beta_1}\) 减少到 \(-\infty\)。由于

\((p + ac^-)^{-1} \frac{\beta_2}{\beta_1} > (p + ac^+)^{-1} \frac{\beta_2}{\beta_1},\)

数 \(b\) 是唯一确定的。我们称这个数为 \(b^*_{\varpi}\)。我们证明这个点是正极大值。首先我们知道 \(a'_{\varpi}(0) = 1\)。由于 \(b^*_{\varpi}\) 是使得 \(a'_{\varpi}(b) = 0\) 的唯一点，我们必然有 \(a'_{\varpi}(b) > 0, \forall 0 < b < b^*_{\varpi}\)。必然 \(a''_{\varpi}(b^*_{\varpi}) \le 0\)。我们不能有 \(a''_{\varpi}(b^*_{\varpi}) = 0\)。确实，该点将是拐点，并且对于接近 \(b^*_{\varpi}\) 的 \(b > b^*_{\varpi}\)，我们将有 \(a'_{\varpi}(b) = 0\)。因为我们将有另一个不同于 \(b^*_{\varpi}\) 的驻点。这是不可能的，基于驻点的唯一性。这证明了 \(a_{\varpi}(b)\) 的性质。性质(17.5.19)源于 \(Z^+(a_{\varpi}(b), b) < 0\) 的事实，参见(17.5.10)以及函数在 \(a\) 上的单调递增性。\(a_{\varpi}(b)\) 的所有性质都已证明。\(b^*_{\pi}(a)\) 的性质以类似方式证明。这结束了证明。

我们推导出

### 推论 17.1. 如果

(17.5.24) \( a_{\varpi}(b^*_{\varpi}) + \varpi \le 0,\)

那么 \(a(b) = a_{\varpi}(b), \forall b > 0.\) 类似地，如果

(17.5.25) \( b_{\pi}(a^*_{\pi}) - \pi \ge 0,\)

那么 \(b(a) = b_{\pi}(a), \forall a < 0.\) 如果(17.5.24)不满足，则存在且仅存在两个值 \(b^1_{\varpi}\) 和 \(b^2_{\varpi}\)，使得

(17.5.26) \( b^1_{\varpi} < b^*_{\varpi} < b^2_{\varpi}, \quad a_{\varpi}(b^1_{\varpi}) + \varpi = a_{\varpi}(b^2_{\varpi}) + \varpi = 0,\)

其中 \(b^2_{\varpi} = +\infty\)，如果 \(a_{\varpi}(+\infty) + \varpi \ge 0\)。那么

(17.5.27) \( a(b) = a_{\varpi}(b), \forall b < b^1_{\varpi} \text{ and } b > b^2_{\varpi}.\)

类似地，如果(17.5.25)不满足，则存在且仅存在两个值 \(a^1_{\pi}\) 和 \(a^2_{\pi}\)，使得

(17.5.28) \( a^1_{\pi} < a^2_{\pi}, \quad b_{\pi}(a^1_{\pi}) - \pi = b_{\pi}(a^2_{\pi}) - \pi = 0\)

其中 \(a^1_{\pi} = -\infty\)，如果 \(b_{\pi}(-\infty) - \pi \le 0\)。那么

(17.5.29) \( b(a) = b_{\pi}(a), \forall a < a^1_{\pi} \text{ and } a > a^2_{\pi}.\)

**证明。** 显然 \(a_{\varpi}(b) + \varpi < 0, \forall b > 0\) 和 \(b_{\pi}(a) - \pi > 0, \forall a < 0.\) 结果源于提议17.4。我们还注意到

\(a_{\varpi}(0) + \varpi < 0, \quad b_{\pi}(0) - \pi > 0.\)

其余讨论容易得出。

标准(17.5.24)和(17.5.25)容易检查，因为它们涉及单个数值的值。

### 17.5.3. 搜索程序。

我们首先注意到 \(a_{\varpi}(+\infty)\) 和 \(b_{\pi}(-\infty)\) 是有限的。确实

(17.5.30) \(\exp -\beta_1 a_{\varpi}(+\infty) = \frac{p+h}{p - ac^- + \varpi + \beta_2}.\)

(17.5.31) \(\exp -\beta_2 b_{\pi}(-\infty) = \frac{p+h}{h - ac^- - \varpi + \beta_1}.\)

因此，曲线 \(a_{\varpi}(b)\) 和 \(b_{\pi}(a)\) 因为，设定

\(u(a) = a_{\varpi}(b_{\pi}(a)) - a,\)

它在 \(u(0) = a_\varpi(b_\varpi(0)) < 0\) 和 \(u(-\infty) = +\infty\) 之间连续变化，因此穿过值 0。

考虑系统的一个解 \(\hat{a}, \hat{b}\)。

```
\(\dot{a} = a(\hat{b}); \dot{b} = b(\hat{a}),\)
```

和

```
\(\dot{A} = A(\hat{a}, \hat{b}); \dot{B} = B(\hat{a}, \hat{b}).\)
```

如果 \(\hat{A} < 0, \hat{B} > 0\)，则

```
\(\hat{A} = \hat{a} + \varpi, \hat{B} = \hat{b} - \pi,\)
```

并且

```
\(\hat{a} = a_\varpi(\hat{b}), \hat{b} = b_\pi(\hat{a}).\)
```

如果 \(\hat{A} > 0\)，则 \(\hat{B} > 0\)。因此

```
\(\hat{B} = \hat{b} - \pi, \hat{b} = b_\pi(\hat{a}).\)
```

由于 \(\hat{a} \neq a_\varpi(\hat{b})\)，则 \(\hat{a} + \varpi > 0\)。我们还必须有 \(a_\varpi(b_\pi^+) + \varpi > 0\)，因此区间 \((b_\pi^1, b_\pi^2)\) 定义良好（可能 \(b_\pi^2 = +\infty\)），且

```
\(b_\pi^1 < \hat{b} < b_\pi^2.\)
```

由于 \(\hat{b} = b_\pi(\hat{a})\)，\(b_\pi(a_\pi^+) - \pi\) 的符号未指定。但是如果 \(b_\pi(a_\pi^+) - \pi < 0\)，则区间 \((a_\pi^1, a_\pi^2)\) 定义良好（可能 \(a_\pi^1 = -\infty\)），且我们有

```
\(\hat{a} < a_\pi^1 \text{ or } \hat{a} > a_\pi^2.\)
```

如果 \(a_\pi^1 + \varpi < 0\)，则第一种情况消失（特别是如果 \(a_\pi^1 = -\infty\)）。

类似地，如果 \(\hat{B} < 0\)，则 \(\hat{A} < 0\)。因此我们有

```
\(\hat{A} = \hat{a} + \varpi, \hat{a} = a_\varpi(\hat{b}).\)
```

由于 \(\hat{b} \neq b_\pi(\hat{a})\)，则 \(\hat{b} - \pi < 0\)。我们还必须有 \(b_\pi(a_\pi^+) - \pi < 0\)，因此区间 \((a_\pi^1, a_\pi^2)\) 定义良好（可能 \(a_\pi^1 = -\infty\)），且

```
\(a_\pi^1 < \hat{a} < a_\pi^2.\)
```

由于 \(\hat{a} = a_\varpi(\hat{b})\)，\(a_\varpi(b_\varpi^+) + \varpi\) 的符号未指定。但是如果 \(a_\varpi(b_\varpi^+) + \varpi > 0\)，则区间 \((b_\varpi^1, b_\varpi^2)\) 定义良好（可能 \(b_\varpi^2 = +\infty\)），且我们有

```
\(\hat{b} < b_\varpi^1 \text{ or } \hat{b} > b_\varpi^2.\)
```

如果 \(b_\varpi^2 > \pi\)，则第二种情况消失，特别是如果 \(b_\varpi^2 = +\infty\)。

根据前面的讨论，我们可以定义以下过程来搜索对 \(\hat{a}, \hat{b}\)。我们考虑曲线 \(a_\varpi(b)\) 和 \(b_\pi(a)\) 的一个交叉点，记为 \(a_0, b_0\)。

- (1) 如果 \(a_0 + \varpi \le 0\) 且 \(b_0 - \pi \ge 0\)，则 \(\hat{a} = a_0, \hat{b} = b_0\)
- (2) 如果 \(a_\varpi(b_0^+) + \varpi \le 0\) 且 \(b_\pi(a_\varpi^+) - \pi \ge 0\)，则 \(\hat{a} = a_0, \hat{b} = b_0\)
- (3) 如果步骤 1 和 2 中的一个条件不满足，则我们考虑两种可能的场景：

### 场景 1

如果 \(a_\pi(b_\varpi^+) > 0\) 且 \(b_\pi(a_\pi^+) - \pi \ge 0\)，则 \(\hat{b} = b_\pi(a_\pi^+)\hat{b}_\varpi^- < b_\pi(a_\pi^+) < b_{\pi \varpi}^+\)，\(\hat{B} = -\hat{b} = \hat{b} - \pi\) 且 \(-\infty \le \hat{a} \le 0, 0 < \hat{A} < b_\pi(a_\pi^+) - \pi\) 并且

\(K^+ + \frac{1}{\alpha}((h - ac^+)\hat{A} + \hat{a}(p - ac^-)) + \frac{1}{\alpha} \frac{p - ac^+}{\beta_1 \beta_2} (\beta_1 - \beta_2)\)
\(\frac{(\exp \beta_1(\hat{A} - \hat{a}) - 1)(\exp \beta_2(\hat{A} - \hat{a}) - 1)}{\exp \beta_1(\hat{A} - \hat{a}) - \exp \beta_2(\hat{A} - \hat{a})} + \frac{1}{\alpha} \frac{p + h}{\beta_1 \beta_2}\)
\(\frac{\beta_1 (\exp \beta_1(\hat{A} - \hat{a}) - 1)(1 - \exp \beta_2(\hat{A} - \hat{a})) - \beta_2 (\exp \beta_2(\hat{A} - \hat{a}) - 1)(1 - \exp \beta_1 \hat{A})}{\exp \beta_1(\hat{A} - \hat{a}) - \exp \beta_2(\hat{A} - \hat{a})} + \frac{1}{\alpha} \frac{p + h}{\beta_1 \beta_2}\)
\(\frac{\beta_1 (\exp \beta_1(\hat{A} - \hat{a}) - 1)(1 - \exp \beta_2(\hat{A} - \hat{a})) - \beta_2 (\exp \beta_2(\hat{A} - \hat{a}) - 1)(1 - \exp \beta_1 \hat{A})}{\exp \beta_1(\hat{A} - \hat{a}) - \exp \beta_2(\hat{A} - \hat{a})} = 0;\)
\((c^+ + c^-)(\exp \beta_1(\hat{A} - \hat{a}) - \exp \beta_2(\hat{A} - \hat{a})) - \frac{h + ac^+}{\alpha}\)
\(\cdot (\exp \beta_1(\hat{A} - \hat{a}) - \exp \beta_2(\hat{A} - \hat{a}) - \exp \beta_1(b_\pi(a_\pi^+) - \hat{a}) + \exp \beta_2(b_\pi(a_\pi^+) - \hat{a}))\)
\(- \frac{p + h}{\alpha(\beta_1 - \beta_2)} (\exp \beta_2 \hat{A} + \beta_1 b_\pi(a_\pi^+)) - \exp(\beta_1 \hat{A} + \beta_2 b_\pi(a_\pi^+)))\)
\(\cdot (\beta_1 \exp -\beta_1 \hat{a} - \beta_2 \exp -\beta_2 \hat{a}) + \frac{p - ac^+}{\alpha} \exp -(\beta_1 + \beta_2)\hat{a}\)
\(\cdot (\exp(\beta_2 \hat{A} + \beta_1 b_\pi(a_\pi^+)) - \exp(\beta_1 \hat{A} + \beta_2 b_\pi(a_\pi^+))) = 0.\)

### 场景 2

如果 \(a_\varpi(b_\pi^+) + \varpi \le 0\) 且 \(b_\pi(a_\pi^+) - \pi < 0\)，则 \(\hat{a} = a_\varpi(\hat{b})\)，\(a_\pi^+ < a_\varpi(\hat{b}) < a_\pi^+\)，\(\hat{A} = \hat{a} + \varpi, 0 < \hat{b} < \pi, a_\varpi(\hat{b}) + \varpi < \hat{B} < 0\) 且

\(-K^- + \frac{1}{\alpha}((h - ac^-)\hat{b} + (p + ac^-)\hat{B})\)
\(+ \frac{1}{\alpha} \frac{h - ac^-}{\beta_1 \beta_2} (\beta_1 - \beta_2) \frac{(\exp \beta_1(\hat{B} - \hat{b}) - 1)(\exp \beta_2(\hat{B} - \hat{b}) - 1)}{\exp \beta_1(\hat{B} - \hat{b}) - \exp \beta_2(\hat{B} - \hat{b})} + \frac{1}{\alpha} \frac{p + h}{\beta_1 \beta_2}\)
\(\frac{\beta_1 (\exp \beta_1(\hat{B} - \hat{b}) - 1)(1 - \exp \beta_2 \hat{B}) - \beta_2 (\exp \beta_2(\hat{B} - \hat{b}) - 1)(1 - \exp \beta_1 \hat{B})}{\exp \beta_1(\hat{B} - \hat{b}) - \exp \beta_2(\hat{B} - \hat{b})} = 0;\)
\(-(c^+ + c^-)(\exp \beta_1(\hat{B} - \hat{b}) - \exp \beta_2(\hat{B} - \hat{b})) + \frac{p + ac^-}{\alpha}\)
\(\cdot (\exp \beta_1(\hat{B} - \hat{b}) - \exp \beta_2(\hat{B} - \hat{b}) - \exp \beta_1(a_\pi(a_\pi^+) - \hat{b}) + \exp \beta_2(a_\pi(a_\pi^+) - \hat{b}))\)
\(+ \frac{p + h}{\alpha(\beta_1 - \beta_2)} (\exp \beta_2 \hat{B} + \beta_1 a_\pi(\hat{a})) - \exp(\beta_1 \hat{B} + \beta_2 a_\pi(\hat{a})))\)
\(\cdot (\beta_1 \exp -\beta_1 \hat{b} - \beta_2 \exp -\beta_2 \hat{b}) - \frac{h - ac^-}{\alpha} \exp -(\beta_1 + \beta_2)\hat{b}\)
\(\cdot (\exp(\beta_2 \hat{B} + \beta_1 a_\pi(\hat{a})) - \exp(\beta_1 \hat{B} + \beta_2 a_\pi(\hat{a}))) = 0.\)

如果 \(a_\varpi(b_\pi^+) + \varpi > 0\) 且 \(b_\pi(a_\pi^+) - \pi < 0\)，则可能出现场景 1 或场景 2。如果发生场景 1，则对 \(a\) 有额外限制：\(\hat{a} < a_\pi^+\) 或 \(\hat{a} > a_\pi^+\)。如果 \(a_\pi^+ + \varpi < 0\)，则第一种情况消失（特别是如果 \(a_\pi^+ = -\infty\)）；如果发生场景 2，则对 \(\hat{b}\) 有额外限制：\(\hat{b} < b_{\pi \varpi}^+\) 或 \(\hat{b} > b_{\pi \varpi}^+\)。如果 \(b_{\pi \varpi}^+ > \pi\)，则第二种情况消失，特别是如果 \(b_{\pi \varpi}^+ = +\infty\)。

本页故意留空

# 参考文献

- [1] Arrow K.J., Karlin S., Scarf H. 库存与生产数学理论研究, Stanford University Press, (1958).
- [2] Bellman R. 动态规划, Princeton University Press, (1957).
- [3] Benkherouf L. 关于 s-S 库存策略最优性的研究：一种准变分方法, 应用数学与随机分析杂志, Vol 2008, Hindawi Publishing Corporation, (2008).
- [4] Benkherouf L., Bensoussan A. 复合泊松和扩散需求下 (s, S) 策略的最优性：一种准变分不等式方法, SIAM 控制杂志, Vol. 48, No 2, p.756-762, (2009).
- [5] Bensoussan A. 最优控制中的扰动方法, Dunod-Gauthier-Villars, (1988).
- [6] Bensoussan A., Cakanyildirim M., Sethi S.P. 带有信息延迟的库存问题中基础库存和 s-S 策略的最优性, 优化理论与应用杂志, Vol 130, No 2, p. 153-172, (2006).
- [7] Bensoussan A., Çakanyıldırım M., Sethi S.P., Wang M., Zhang H. 带有动态信息延迟的库存模型中平均成本最优性, 待出版.
- [8] Bensoussan A., Lions J.L. 冲动控制与准变分不等式, Dunod, (1982).
- [9] Bensoussan A., Liu R.H., Sethi S.P. 复合泊松和扩散需求下 (s-S) 策略的最优性：一种准变分不等式方法, SIAM 控制杂志, Vol 44, No 5, p. 1650-1676, (2005).
- [10] Bensoussan A., Liu J., Yuan J. 奇异控制与冲动控制：一种共同方法, 离散与连续动力系统-B 系列 (DCDS-B), 13, 27-57, (2010).
- [11] Bertsekas D. P. 动态规划与最优控制 (第 2 版), Athena Scientific, (2000). 共两卷.
- [12] Heyman D., Cheng F., Sethi S. P., Taksar M. 马尔可夫需求库存模型, Springer, 2009.
- [13] Cadenillas A., Lakner P., Pinedo M. 均值回归库存的最优控制, 运筹学, Vol 58, No. 6, (2010).
- [14] Cadenillas A., Sarkar S., Zapatero F. 均值回归现金水库下的最优股利政策, 数学金融, Vol 17, No 1, (2007).
- [15] Cadenillas A., Zapatero F. 外汇市场中中央银行干预的最优性, 经济理论杂志, 87(1):218-242, (1999).
- [16] Clark A. J., Scarf H. 多级库存问题的最优策略, 管理科学, Vol 50, No 12 Supplement, 2004.
- [17] Constantinides G.M., Richard S.F. 连续时间折扣成本库存和现金管理中最优简单策略的存在性, 运筹学, 26(4): 620-636, (1978).
- [18] Doob J.L. 随机过程, Wiley, (1953).
- [19] Gallego G., Sethi S.P. R^n 中的 K-凸性, 优化理论与应用杂志, 127(1), 71-88, (2005).
- [20] Girard V. 生产与流量管理, 第 3 版, Economica, (2003).
- [21] Guo X., Hernández-Lerma O. 连续时间马尔可夫决策过程, Springer, (2009).
- [22] Hadley G., Whitin T. 库存系统分析, Prentice-Hall, Englewood Cliffs, (1963).
- [23] Harris F.W. “一次制造多少零件”, Factory, 管理杂志, 10(2), 135-136, 152, (1913).




- [24] Harris F.W., 《运营成本（工厂管理丛书）》，芝加哥：Shaw (1915).
- [25] Hernández-Lerma O., Lasserre J.B., 《离散时间马尔可夫控制过程》，Springer，数学应用，第 30 卷，(1996).
- [26] Iglehart D.L., 《无限时域动态库存问题中 (s, S) 策略的最优性》，《管理科学》，第 9 卷，第 2 期，第 259-267 页，(1963).
- [27] Karlin S., Shreve S.E., 《布朗运动与随机微积分》，Springer，第 2 版，(1991).
- [28] Karlin S., 《具有变动和随机需求的动态库存策略》，《管理科学》，6(3)，231-258，(1960).
- [29] Khas’minskii R.Z., 《微分方程的随机稳定性》，Kluwer，(1980).
- [30] Kuratowski K., 《拓扑学（第 I 和 II 卷）》，Academic Press，纽约，(1966).
- [31] Loève M., 《概率论》，第 I 卷，第 4 版，Springer Verlag 数学研究生教材，第 45 卷，(1977).
- [32] Presman E., Sethi S.P., 《具有连续和泊松需求以及折扣和平均成本的随机库存模型》，《生产与运营管理》，15(2)，279-293，(2006).
- [33] Porteus E.L., 《随机库存理论基础》，斯坦福大学出版社，斯坦福，(2002).
- [34] Ross S.M., 《概率模型导论》，圣地亚哥，CA：Academic Press，(1989).
- [35] Scarf H., 《动态库存问题中 (s, S) 策略的最优性》，《社会科学中的数学方法》，K. Arrow, S. Karlin 和 P. Suppes 编，第 13 章，第 196-202 页，斯坦福大学出版社，斯坦福，(1960).
- [36] Sethi S.P., Zhang H., Zhang Q., 《随机制造系统的平均成本控制》，Springer New York，NY (2005).
- [37] Sulem A., 《扩散库存系统的一维可求解模型》，《数学运筹学》，11，第 125-133 页，(1986).
- [38] Veinott A.F., 《关于 (s, S) 库存策略的最优性：新条件与新证明》，《工业与应用数学杂志》，第 14 卷，第 5 期，第 1067-1083 页，(1966).
- [39] Wagner H., 《应用研究原理》，Prentice-Hall，恩格尔伍德克利夫斯，(1969).
- [40] Wilson R.H., 《库存控制的科学常规》，《哈佛商业评论》，13，116-128，(1934).
- [41] Zipkin P., 《库存管理基础》，McGraw-Hill，(2000).

# A.1. 引理证明

## A.1.1. 引理 4.1 证明

证明. 令 d(x, y) 表示 X 上的距离。我们可以假设 \( f \neq +\infty \)，否则 f_n(x) = n 具有所需性质。我们定义

(A.1.1) 
\( g_n(x) = \inf_{y \in X} [f(y) + nd(x, y)], \)

则 g_n(x) 一致连续。确实

\( |g_n(x) - g_n(x')| \le nd(x, x'). \)

接下来令

\( f_n(x) = \min(n, g_n(x)), \)

则 f_n = \min(n, g_n) 属于 C(X)。而且，它是一个递增序列。我们有 f_n(x) \le f(x)。假设 f(x) < \infty，则由于 g_n(x) \le f(x)，我们可以断言对于足够大的 n 有 f_n(x) = g_n(x)。而且由于 f 是下半连续且下有界，存在 y_n = y_n(x) 使得

\( g_n(x) = f(y_n) + nd(x, y_n). \)

由于该表达式上有界且 f 下有界，很容易得到 y_n \to x，当 n \uparrow \infty 时。由于 f 是下半连续，我们有

\( f(x) \le \liminf f(y_n) \le \liminf g_n(x). \)

但也有 \limsup g_n(x) \le f(x)。因此 g_n(x) \uparrow f(x)。因此也有 f_n(x) \uparrow f(x)。现在假设 f(x) = +\infty。必然有 g_n(x) \uparrow +\infty。否则 g_n(x) 保持被某个常数 A_x 上界，这是不可能的。确实，按上述考虑 y_n，我们有 y_n \to x，并且由于 f 的下半连续性，可得 f(x) \le A_x，这与假设矛盾。最后，如果 g_n(x) \uparrow +\infty，则也有 f_n(x) \uparrow +\infty，从而完成证明。

### A.1.2. 引理 4.2 证明

证明. 无损一般性，我们可以假设 l_v(x) = l(x, v) \ge 0。存在一个序列 l_n^v = l^n(x, v) \uparrow l(x, v)，且 l^n(x, v) 是一致连续且有界的。根据假设 (4.3.1)，序列 \Phi^l l_n^v(x) 是一致连续且有界的。现在我们可以写成

\(\Phi^l l_n^v(x) = \int P(x, v; d\xi) l^v(\xi, v) = \iint P(x, v; d\xi) \otimes \delta_v(\xi') l^v(\xi, \xi),\)

因此我们可以应用凸性单调定理来断言

\(\Phi^l l_n^v(x) \uparrow \Phi^l l_v(x),\)

从而完成证明。

### A.1.3. 引理 4.3 证明

证明. 首先，对于任意固定的 x，存在 v(x) \in U 使得

G(x) = F(x, v(x)).

确实，让我们考虑一个序列 v_n，使得 F(x, v_n) \to G(x)。由于 v_n 在 U 中，而 U 是紧集，我们可以提取一个收敛子序列 v_{n_k} \to v^*。由于 F 是下半连续的，我们可以写成

F(x, v^*) \le G(x).

由于逆不等式也成立，我们有相等。因此下确界可达。现在让我们考虑一个序列 x_n \to x 并令 v_n = v(x_n)。我们可以从序列 x_n, v_n 中提取一个收敛子序列 x_{n_k} \to x, v_{n_k} \to v^*。由于 F 关于两个参数 x, v 是下半连续的，我们可以断言

F(x, v^*) \le \liminf F(x_{n_k}, v_{n_k}) = \liminf G(x_{n_k}).

因此

G(x) \le F(x, v^*) \le \liminf G(x_{n_k}).

我们总是可以假设 x_{n_k} 本身是从一个初步子序列中提取的，使得 G(x_{n_k}) \to \liminf G(x_n)。因此，G 是下半连续的。

# A.2. 可测选择证明

我们现在证明定理 4.1。请注意，在引理 4.3 的证明中定义的 v(x) 关于 x 的依赖关系尚未定义。能够选择一个可测选择对于获得最优反馈以求解最优随机控制问题至关重要。该结果需要多值函数理论。我们需要一些概念和初步结果。首先我们有

## 引理 A.1. 如果 f 是下半连续的，则对于任何实数 c，{x|f(x) \le c} 是闭集。

证明. 确实，考虑一个序列 x_n，使得 x_n \to x 且 f(x_n) \le c。由于

f(x) \le \liminf f(x_n),

我们有 f(x) \le c，闭集性质已证。请注意，逆命题也成立。确实，假设 x_n \to x。令 L 为序列 f(x_n) 的一个累积点。存在一个子序列 x_{n_k} 使得 f(x_{n_k}) \to L。令 \epsilon > 0 并定义

L(\epsilon) = \begin{cases} L + \epsilon, & \text{if } L > -\infty \\ -\frac{1}{\epsilon}, & \text{if } L = -\infty \end{cases}

那么对于足够大的 k \ge k(\epsilon)，我们有 f(x_{n_k}) \le L(\epsilon)，因此根据闭集性质 f(x) \le L(\epsilon)，从而也有 f(x) \le L。由于 L 是任意累积点，必然有 f(x) \le \liminf f(x_n)。

定义 \mathcal{F}(U) 为 U 的闭集子集的集合（包括空集）。这些子集是紧集。我们在 \mathcal{F}(U) 上配备一个度量，即豪斯多夫度量，定义如下（集合之间的距离）。首先，如果 A \neq \emptyset, A \in \mathcal{F}(U)，且 u \in U，我们定义 u 到 A 的距离为

d(u, A) = \min_{a \in A} d(u, a).

请注意

|d(u, A) - d(v, A)| \le d(u, v).

如果 \( A = \mathcal{O} \)，则定义

\( d(u, \mathcal{O}) = \max_{v, w \in U} d(v, w) = \text{diam} \, (U). \)

接下来，对于 \( A, B \in \mathcal{F}(U) \)，我们定义

\(\begin{aligned} \varrho(A, B) &= \max \left\{ \max_{a \in A} d(a, B), \max_{b \in B} d(b, A) \right\}, \quad \text{if } A, B \neq \mathcal{O} \\ \varrho(A, \mathcal{O}) = \varrho(\mathcal{O}, A) &= \text{diam } (U), \quad \text{if } A \neq \mathcal{O} \\ \varrho(\mathcal{O}, \mathcal{O}) &= \varrho(\mathcal{O}, \mathcal{O}) = 0. \end{aligned}\)

这在 \(\mathcal{F}(U)\) 上定义了一个度量，\(\mathcal{F}(U)\) 成为一个 *紧度量空间*。

考虑 \(\mathcal{F}(U)\) 元素的一个序列 \( A_n \)。定义

\(\begin{aligned} \liminf A_n &= \{ u \in U \mid \liminf d(u, A_n) = 0 \} \\ \limsup A_n &= \{ u \in U \mid \lim d(u, A_n) = 0 \} \end{aligned}\)

显然 \(\liminf A_n \subset \limsup A_n\)。而且，它们是属于 \(\mathcal{F}(U)\) 的闭集。可以验证有用的性质

\( \liminf A_n = \limsup A_n = A \Leftrightarrow \varrho(A_n, A) \to 0. \)

在这种情况下，人们使用定义 \( A = \lim A_n \)。

如果 \( X \) 是一个度量空间，则映射 \( \Psi : X \to \mathcal{F}(U) \) 称为一个 *多值映射*。由于 \( X \) 和 \(\mathcal{F}(U)\) 都是度量空间，我们自然地拥有连续、下半连续、上半连续和博雷尔函数的概念。然而，可以定义两个额外的概念。这些额外的概念由 K. Kuratowski 引入，参见 [30]。这就是它们被称为 (K) 上半连续或 (K) 下半连续的原因。我们说 \( \Psi \) 是 (K) 上半连续的，如果

\( x_n \to x \Rightarrow \limsup \Psi(x_n) \subset \Psi(x). \)

同样，当

\( x_n \to x \Rightarrow \liminf \Psi(x_n) \supset \Psi(x). \)

时，我们说 \( \Psi \) 是 (K) 下半连续的。

可以证明，如果 \( \Psi \) 既是 (K) 上半连续的又是 (K) 下半连续的，那么它是连续的。事实上，最有用的概念是 (K) 上半连续性。原因在于以下两个基本性质：

(A.2.1) \( \Psi \text{ (K) u.s.c} \Rightarrow \Psi \text{ 是博雷尔的} \)

接下来 (A.2.2)

如果 \( \Psi \) 是 (K) 上半连续的，且 G 是 U 的开子集，则 \( \{x \in X | \Psi(x) \subset G\} \) 是开集。

第二个性质表明，(K) 上半连续性的概念对于普通函数归结为连续性。

### 引理 A.2. 设 \( U \) 为紧度量空间，\( g : U \to ]-\infty, +\infty[ \) 为下半连续函数。定义 \( g^* : \mathcal{F}(U) \to ]-\infty, +\infty[ \) 为

(A.2.3) \( g^*(A) = \begin{cases} \min_{u \in A} g(u), & \text{if } A \neq \mathcal{O} \\ +\infty, & \text{if } A = \mathcal{O} \end{cases} \)

则 \( g^* \) 是下半连续的。





证明。集合 $\emptyset$ 是 $\mathcal{F}(U)$ 的一个孤立点。因此，只需证明 $g^*$ 在 $\mathcal{F}(U) - \emptyset$ 上是下半连续（l.s.c.）的。对于 $A \in \mathcal{F}(U) - \emptyset$，存在 $a \in A$ 使得 $g(a) = g^*(A)$。现在考虑一个序列 $A_n \in \mathcal{F}(U) - \emptyset$，且 $A_n \to A$。令 $a_n \in A_n$，使得 $g(a_n) = g^*(A_n)$。让我们考虑一个子序列 $a_{n_k}$，使得 $g(a_{n_k}) \to \liminf g(a_n) = \liminf g^*(A_n)$。

我们可以假设 $a_{n_k} \to \bar{a}$（否则取一个收敛子序列）。由下半连续性可得 $g(\bar{a}) \le \liminf g(a_n) = \liminf g^*(A_n)$。

由于 $d(\bar{a}, A_{n_k}) \le d(\bar{a}, a_{n_k})$，可知 $d(\bar{a}, A_{n_k}) \to 0$。故 $\bar{a} \in \liminf A_{n_k}$。但 $A_{n_k} \to A$，故 $\liminf A_{n_k} = A$。因此 $\bar{a} \in A$。由此可得 $g^*(A) \le g(\bar{a}) \le \liminf g^*(A_n)$，从而该性质已被证明。$\square$

### Lemma A.3.
设 $U$ 为度量紧集，$g : U \to ]-\infty, +\infty]$ 为下半连续函数。对 $A \in \mathcal{F}(U)$ 和 $c \in ]-\infty, +\infty[$，定义函数

$G(A, c) = \{u \in A | g(u) \le c\}$

则 $G$ 从 $\mathcal{F}(U) \times ]-\infty, +\infty]$ 到 $\mathcal{F}(U)$ 是 (K) 上半连续（u.s.c.）的。

证明。设 $A_n \to A$ 且 $c_n \to c$，我们必须证明

(A.2.4) $\limsup_{n \to \infty} G(A_n, c_n) \subset G(A, c)$。

令 $y \in \limsup_{n \to \infty} G(A_n, c_n)$。由定义可知，$\liminf_{n \to \infty} d(y, G(A_n, c_n)) = 0$。

由此可知存在 $y_{n_k} \in G(A_{n_k}, c_{n_k})$ 使得 $y_{n_k} \to y$。注意 $y_{n_k} \in A_{n_k}$。因此 $y \in \liminf A_{n_k} = A$。又 $g(y_{n_k}) \le c_{n_k}$，且由于 $g$ 是下半连续的，可得 $g(y) \le c$。故 $y \in G(A, c)$。这证明了 (A.2.4) 及所需结果。$\square$

### Lemma A.4.
设 $U$ 为度量紧集，$g : U \to ]-\infty, +\infty]$ 为下半连续函数。令 $g^*$ 由 (A.2.3) 定义。我们定义

$G^*(A) = G(A, g^*(A))$，

则 $G^*$ 是从 $\mathcal{F}(U)$ 到 $\mathcal{F}(U)$ 的 Borel 映射。

证明。根据 Lemma A.3，$G$ 是 Borel 映射，且由 Lemma A.2 可知 $g^*$ 也是 Borel 映射。由复合可知 $G^*$ 也是 Borel 映射，从而证明了该结果。$\square$

### Lemma A.5.
设 $U$ 为度量紧集。存在一个映射 $\sigma : \mathcal{F}(U) - \emptyset \to U$，它是 Borel 映射且满足

$\sigma(A) \in A, \forall A \in \mathcal{F}(U) - \emptyset$。

证明。让我们考虑一组在 $U$ 上一致连续且有限且能区分 $U$ 点的函数序列 $g_n$。这意味着如果 $u \neq v$，则存在 $g_n$ 使得 $g_n(u) \neq g_n(v)$。这样的序列存在。事实上，选取在 $U$ 中稠密的序列 $u_k$。定义

$F_{kn} = \left\{v \in U | d(u_k, v) \le \frac{1}{n} \right\}$。

考虑两个集合 $F_k$ 和 $F_{k'n'}$。我们定义一个从 $U$ 到 $[0, 1]$ 的函数 $g_{k,k:n'}$，它是连续的（因此是一致连续的，因为 $U$ 是紧集）且满足：
如果 $F_k \cap F_{k'n'} \neq \emptyset$ 则 $g_{k,k:n'} = 1$
如果 $F_k \cap F_{k'n'} = \emptyset$ 则 $g_{k,k:n'}(F_k) = 0, g_{k,k:n'}(F_{k'n'}) = 1$

函数集 $g_{k,k:n'}$ 是一个区分序列。事实上，如果 $u \neq v$，则存在 $F_{k,n}$ 和 $F_{k'n'}$ 使得 $u \in F_{k,n}, v \in F_{k'n'}$。

对于函数 $g_n$，我们如同在 Lemma A.2 中关联 $g^*_n$，如同在 Lemma A.4 中关联 $G^*_n$。

接下来定义序列 $H_n : \mathcal{F}(U) - \emptyset \to \mathcal{F}(U) - \emptyset$ 如下公式
$H_n(A) = G^*_n(H_{n-1}(A)); H_0(A) = A$

由于 $A \neq \emptyset$，有
$A = H_0(A) \supset H_1(A) \cdots \supset H_n(A)$。

由于
$H_n(A) = \left\{ u \in H_{n-1}(A) \mid g_n(u) = \min_{a \in H_{n-1}(A)} g_n(a) \right\}$，

集合 $H_n(A)$ 非空且紧。我们可以断言
\(\cap^\infty_{n=0} H_n(A) \neq \emptyset.\)

事实上，存在序列 $a_n \in H_n(A)$。我们可以提取一个子序列 $a_{n_k} \to a$。必然有 $a \in \cap^\infty_{n=0} H_{n_k}(A) = \cap^\infty_{n=0} H_n(A)$。

如果 $u, u' \in \cap^\infty_{n=0} H_n(A)$，则由构造可知
$g_n(u) = g_n(u') = g^*_n(H_{n-1}(A)),$

且由于函数 $g_n$ 能区分 $U$ 的点，故 $u = u'$。因此 $\cap^\infty_{n=0} H_n(A)$ 只包含一个点，记为 $\sigma(A)$。让我们验证

(A.2.5) \(H_n(A) \to \{\sigma(A)\}.\)

事实上，由于序列 $H_n(A)$ 是递减的，我们可以断言
\(u \in \cap^\infty_{n=0} H_n(A) \implies d(u, H_n(A)) = 0, \forall n\)

因此

(A.2.6) \(\cap^\infty_{n=0} H_n(A) \subset \liminf_n H_n(A) \subset \limsup_n H_n(A).\)

另一方面，如果考虑元素 \(u \in \limsup_n H_n(A)\)，则存在序列 \(u_{n_k} \in H_{n_k}(A)\) 使得 \(d(u, u_{n_k}) \to 0\)。我们有 \(n_k \le n_{k+1}\)，因此对于固定的 \(k\)，\(u_{n_k} \in H_{n_k}\)。这意味着 \(u \in H_{n_k}\)，故 \(u \in \cap^\infty_{n=0} H_n(A)\)，这与 (A.2.6) 一起蕴含结果 (A.2.5)。

现在，函数 \(G^*_n\) 是 Borel 的，函数 \(H_n\) 也是 Borel 的，\(\forall n\)。因此由 \(\nu(A) = \{\sigma(A)\}\) 定义的函数 \(\nu : \mathcal{F}(U) - \emptyset \to \mathcal{F}(U) - \emptyset\) 是 Borel 的。要断言 $\sigma$ 是 Borel 的，我们注意到 $\sigma = \tau^{-1} \circ \nu$，其中 $\tau : U \to \mathcal{F}(U) - \emptyset$ 简单地由 $\tau(u) = \{u\}$ 定义。映射 $\tau$ 是点对点且连续的。由于 $U$ 是紧集，$\tau(U)$ 也是紧集，因此在 $\mathcal{F}(U) - \emptyset$ 中是闭集。其逆是 Borel 的，故 $\sigma$ 是 Borel 的，从而证明结束。

我们现在证明定理 4.1：

证明。考虑由以下公式定义的映射 \( F^*: X \times [-\infty, +\infty] \to \mathcal{F}(U) \)
\[ F^*(x, c) = \{u \in U | F(x, u) \le c\}, \]
则 \( F^* \) 是 (K) 上半连续的。确实，如果 \( x_n \to x, c_n \to c \)，我们必须证明
\[ \limsup F^*(x_n, c_n) \subset F^*(x, c). \]
令 \( u \in \limsup F^*(x_n, c_n) \)，由定义可知 \( \liminf d(u, F^*(x_n, c_n)) = 0 \)。存在子序列 \( u_{n_k} \in F^*(x_{n_k}, c_{n_k}) \)，使得 \( u_{n_k} \to u \)。这意味着
\[ F(x_{n_k}, u_{n_k}) \le c_{n_k}. \]
由于 \( F \) 是下半连续的，我们得到 \( F(x, u) \le c \)，故 \( u \in F^*(x, c) \)。接下来定义
\[ F^*(x) = F^*\left(x, \inf_{u \in U} F(x, u)\right): X \to \mathcal{F}(U). \]
由于 \( F^*(x, c) \) 是 Borel 的且 \( x \to \inf_{u \in U} F(x, u) \) 是下半连续的，映射 \( F^*(x) \) 是 Borel 的。注意
\[ F^*(x) = \left\{u \in U | F(x, u) = \inf_{v \in U} F(x, v)\right\}. \]
而且 \( F^*(x) \neq \emptyset, \forall x \)，故 \( F^*: X \to \mathcal{F}(U) - \emptyset \)。映射 \( \hat{v}(x) = \sigma(F^*(x)) \) 从 $X$ 到 $U$ 是 Borel 的且满足 \( \hat{v}(x) \in F^*(x) \)。因此我们有
\[ F(x, \hat{v}(x)) = \inf_{v \in U} F(x, v) \forall x, \]
从而证明完成。\(\square\)

# A.3. 扩展到 U 非紧的情况

我们现在证明定理 4.2

证明。对于每个固定的 \( x \)，我们可以将控制集限制为 \( U \cap \{|v| \le \gamma(x)\} \)，它是紧集，因此最小值可达。要证明 \( G(x) \) 是下半连续的，取序列 \( x_n \to x \) 并令 \( v_n \) 为相应的最小值。我们有
\[ |v_n| \le \gamma(x_n), \]
根据假设，它保持有界。因此序列 \( v_n \) 保持在一个紧集中。我们可以提取一个收敛于 \( x, v^* \) 的子序列 \( x_{n_k}, v_{n_k} \)。由于 \( F \) 在两个参数上都是下半连续的，我们有
\[ F(x, v^*) \le \liminf F(x_{n_k}, v_{n_k}) = \liminf G(x_{n_k}). \]
事先可以假设
\[ G(x_n) \to \liminf G(x_n), \]
故
\[ G(x) \le \liminf G(x_n), \]
这证明了 \( G(x) \) 是下半连续的。接下来，考虑子集 \( X_N = \{x \in X | d(x_0, x) \le N\} \)，其中 \( d \) 是 $X$ 上的距离。对于 \( x \in X_N \)，我们可以将控制集限制为
\[ U_N = U \cap \{|v| \le \sup_{x \in X_N} \gamma(x)\}, \]
它是紧集。
因此，根据定理 4.1，存在 Borel 映射 \( \hat{v}_N(x): X_N \to U_N \) 使得
\[ G(x) = F(x, \hat{v}_N(x)), \forall x \in X_N. \]





我们接下来定义

\(\hat{v}(x) = \left\{ \begin{array}{ll} \hat{v}_1(x), & \text{if } x \in X_1 \\ \dots \\ \hat{v}_N(x), & \text{if } x \in X_N - X_{N-1} \end{array} \right.\)

映射 \(\hat{v}(x)\) 是博雷尔可测的，并满足 \(G(x) = F(x, \hat{v}(x)), \forall x\)。证明已完成。

# A.4. 紧性性质

让我们考虑一组函数 \(u_\alpha(x)\)，其中 \(x \in R^n\)。我们假设（当 \(\alpha \to 1\) 时）

\(|u_\alpha(x)| \le C_M, |Du_\alpha(x)| \le C_M, \forall x \text{ such that } |x| \le M,\)

那么存在一个子序列，仍记作 \(u_\alpha(x)\)，它在半径为 \(M\) 的球上一致收敛到一个函数 \(u(x)\)，使得

\(|u(x)| \le C_M, |Du(x)| \le C_M, \forall x \text{ such that } |x| \le M\)

且

\(\sup_{|x| \le M} |u_\alpha(x) - u(x)| \to 0, \text{ as } \alpha \to 1.\)

\(\alpha\) 到 1 的收敛可以替换为收敛到任何固定数。当 \(n = 1\) 时，这就是 Ascoli-Arzelà 定理。一般来说，这个结果表达了一组函数的紧性性质。

