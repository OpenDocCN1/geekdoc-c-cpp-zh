

```cpp
// Create basic structure for plain options
Lattice<double, TYPEB> lattice(N, 0.0); // init
LatticeMechanisms::ForwardInduction<double>(lattice, algorithm, S0);

// 2.
// Price a plain option
double V0 = LatticeMechanisms::BackwardInduction<double>
            (lattice, algorithm, basePayoff);

// 3.
// a. Find lattice index corresponding to t = T1.
// b. Backtrack from that T1 index.

// a. Find index at t = T1
std::size_t indexT1 = static_cast<std::size_t>(T1/dt);

// b.
double CV0 = LatticeMechanisms::BackwardInduction<double>
              (lattice, algorithm, compoundPayoff, indexT1);

return CV0;
}
```

我们现在以 Haug (2007, p. 136) 中的示例为例（买入看涨期权）。输入为：

```cpp
// Option data for 'base' option
OptionData opt;

// Haug 2007 page 136
opt.K = 520.0;
opt.T = 0.5;
opt.r = 0.08;
opt.q = 0.03;
opt.sig = 0.35;
double S0 = 500.0;
std::size_t N = 13000;

// Payoff as a lambda function
double K2 = opt.K;
auto baseCallPayoff = [&K2] (double S) -> double
  {return std::max<double>(S - K2, 0.0);};

double K1 = 50.0;
auto compoundPutPayoff = [&K1] (double V) -> double
  {return std::max<double>(K1 - V, 0.0);};
double T1 = 0.25;

double compoundOptionValue = CompoundOption
            (compoundPutPayoff, T1, // Compound option
```

```
baseCallPayoff, opt,       // Equity option
N,                          // Lattice size
S0);                        // Underlying value
```

我们得到的答案是 21.1959。

回答以下问题：

+   a) 根据以下数据为看涨期权上的看涨期权定价（Mun, 2002, p. 187）：

```
opt.K = 900.0; // Mun 2002 page 187
opt.T = 3.0;
opt.r = 0.077;
opt.q = 0.0;
opt.sig = 0.30;
double S0 = 1000.0;
double K1 = 500.0;
```

我们得到的答案是 165.174。

+   b) 修改函数 `CompoundOption()` 的代码以包含除 **Tian 方法** 之外的其他前向归纳算法（见第 11 章和第 12 章讨论）。测试这些方案。

# 9. （复合期权，PDE 方法）

本练习的目的是使用有限差分法对复合期权进行定价。我们已在练习 8 中解释了背景。基础期权和复合期权收益的 PDE 已由公式 (25.33)、(25.34) 和 (25.35) 定义。

回答以下问题：

+   a) 将系统 (25.33)、(25.34) 和 (25.35) 写成如第 20 章至第 23 章中所示的初边值问题。

+   b) 使用 MOL 为此问题创建一个软件框架。你需要处理基础期权计算的离散收益。将结果与练习 8 中产生的结果进行比较。

+   c) 使用 ADE 方法求解系统 (25.33)、(25.34) 和 (25.35)。

# 10. （选择期权）

*选择期权* 允许购买者决定衍生品将是欧式看涨期权还是看跌期权。这些期权类型可以使用 Mun (2002) 和练习 8 中讨论的格子方法通过二叉树方法进行定价，但在本次练习中我们使用 PDE 模型。两个基础期权的底层 PDE 给出为：

$$\frac{\partial V_j}{\partial t}+\frac{1}{2}\sigma^2S^2\frac{\partial^2 V_j}{\partial S^2}+rS\frac{\partial V_j}{\partial S}-rV_j=0,\quad j=1,2$$  (25.36)

其执行价分别为 $K_1$ 和 $K_2$（这称为 *复杂选择期权*）。选择期权的 PDE 为：

$$\frac{\partial C_h}{\partial t}+\frac{1}{2}\sigma^2S^2\frac{\partial^2 C_h}{\partial S^2}+rS\frac{\partial C_h}{\partial S}-rC_h=0$$  (25.37)

其收益定义为：

$$C_h(S,T_2)=\max\left(V_1(S,T_2)-K_1,\ V_2(S,T_2)-K_2,\ 0\right). \tag{25.38}$$

回答以下问题：

+   a) 使用 MOL 求解此系统。使用以下数据（Haug, 2007, p. 130）进行代码测试，使用下划线表示看涨和看跌：
+   
+   $$S=50$$
+   $$K_c=55;\ K_p=48$$
+   $$T_c=0.5;\ T_p=0.5833$$
+   $$T=0.25\ \text{(chooser)}$$
+   $$r=0.1;\ b=0.1-0.05;\ \sigma=0.35.$$

+   b) *复杂选择期权* 的价格具有解析解，可以用双变量正态累积分布函数表示（Haug, 2007；Mun, 2002；Rubinstein, 1991），我们在第 16 章中讨论过。实现该公式并将结果与 a) 部分产生的结果进行比较。

+   c) *简单选择期权* 给予持有人在时间 $t_1$ 后选择期权是标准看涨还是看跌的权利，执行价为 $K$，到期时间为 $T_2$（$t_1<T_2$）。按照 Haug (2007) 和 Rubinstein (1991) 中的方法实现该公式。

# 11. （粘性 Burgers 方程）

在本练习中我们研究了练习 21.4 中引入的粘性 Burgers 方程。它是一个带有扩散项的非线性波动方程。它模拟流体流动，是数值实验的简单非线性方案。

本练习的目的是将 MOL 应用于此问题。将结果与基于 ADE 方法的结果进行比较。

## 26.2 什么是随机数生成器？

我们介绍多种生成随机数的方法。给出我们引入的 C++ 代码的一些数学背景是有用的。

### 26.2.1 均匀随机数生成

我们的起点是生成具有 *均匀分布* 的数。为此，假设 $X$ 是一个连续随机变量，取闭区间 $[a,b]$ 内的所有值，其中 $a$ 和 $b$ 为有限。若 $X$ 的 *概率密度函数*（pdf）由以下给出：

$$f(x)=\begin{cases}\dfrac{1}{b-a}, & a\le x\le b\\0, & \text{otherwise}\end{cases} \tag{26.1}$$

则我们说 $X$ 在区间 $[a,b]$ 上 *均匀分布*。简写记号为 $X$ 为 $U(a,b)$。我们通过使用已在 C 或 C++ 中编程的算法来生成均匀分布的随机数。

我们现在介绍两种几年前流行的两种方法。我们在这里出于历史原因包含它们。我们还在第 31 章和第 32 章中随机微分方程（SDE）的数值求解的背景下介绍它们。

### 26.2.2 极坐标 Marsaglia 方法

该方法利用了如果随机变量 $U$ 为 $U(0,1)$，则随机变量 $V$ 定义为 $V=2U-1$ 为 $U(-1,1)$ 的事实。我们现在选择两个变量定义为：

$$V_j=2U_j-1 \quad \text{where}\quad U_j\sim U(0,1),\quad j=1,2.$$

然后我们定义：

$$W=V_1^2+V_2^2\le 1,\quad W\sim U(0,1).$$

我们不断尝试不同的值直到该不等式成立，即直到 $W>0.0$ 且 $W^2\le 1$。继续，我们定义中间值：

$$Y=\sqrt{-2\log(W)/W}.$$

最后，由以下定义的成对值：

$$N_j=V_jY,\quad j=1,2 \tag{26.2}$$

构成两个标准正态（高斯）分布的随机变量。

生成随机变量。设 X 为具有累积概率分布函数 F_X(x) 的随机变量。由于 F_X(x) 是一个非递减函数，逆函数 F_X^{-1}(y) 对 0 到 1 之间的任何值都有定义：

F_X^{-1}(y) = inf {x : F_X(x) ≥ y},      0 ≤ y ≤ 1.

在这种情况下变量 y 给出。

为了从给定分布创建随机变量，设 U 在 (0, 1) 上均匀分布。然后：

X = F_X^{-1}(U) (26.6)

是给定分布的随机变量。

通常，我们需要使用数值方法（例如 Newton–Raphson 方法或不动点迭代）来计算方程 (26.6) 中的随机变量 X。在特殊情况下，可能给出解析解，但这更像是例外而不是规则。为完整起见，我们给出一些例子。

# 26.3.1 随机变量计算的解析解

我们考察区间 (a, b) 上的单维均匀分布，其 pdf 由以下给出：

f_X(x) = { 1/(b - a),  a < x < b ; 0, otherwise } (26.7)

相应的 cdf 为：

F_X(x) = ∫_0^x f_X(y) dy = { 0, x < a ; (x - a)/(b - a), a ≤ x < b ; 1, x ≥ b. } (26.8)

那么，区间 (a, b) 上均匀分布的随机变量由方程给出：

X = F_X^{-1}(U) = a + (b - a)U. (26.9)

参数 β > 0 的指数变量 X 具有密度（pdf）：

f(x) = f_X(x) = { (1/β) e^{-x/β}, 0 ≤ x < ∞, β > 0 ; 0, otherwise } (26.10)

并表示为 exp(β)。

