
求解器对象使我们能够注册待求解系统的定义和参数；它提供了来自 GSL 库的微分方程数值求解工具，这些工具在数值积分部分已经提到过。

系统方程以函数的形式给出：

```python
sage: def f_1(t,y,params): return [y[1],params[0]*(1-y[0]^2)*y[1]-y[0]]
sage: T.function = f_1
```

参数 y 表示未知函数向量，我们应返回系统的右端向量，其以 t 和一个可选参数表示（这里的 params[0] 表示 $\mu$）。

一些 GSL 算法还要求系统的雅可比矩阵（其第 $(i, j)$ 项为 $\frac{\partial f_i}{\partial y_j}$，最后一行包含 $\frac{\partial f_i}{\partial t}$）：

```python
sage: def j_1(t,y,params):
....:     return [[0, 1],
....:             [-2*params[0]*y[0]*y[1]-1, params[0]*(1-y[0]^2)],
....:             [0,0]]
sage: T.jacobian = j_1
```

现在可以请求数值解。我们选择算法、希望求解的区间以及步数，步数决定 $h$：

```python
sage: T.algorithm = "rk8pd"
sage: T.ode_solve(y_0=[1,0], t_span=[0,100], params=[10],
....:           num_points=1000)
sage: f = T.interpolate_solution()
```

这里，我们选择 Runge-Kutta Dormand-Prince 算法在 $[0,100]$ 上计算解；初始条件和参数值（这里只有一个参数）也已给出：$y_0=[1,0]$ 表示 $y_0(0) = 1, y_1(0) = 0$，即 $x(0) = 1, x'(0) = 0$。

为了显示解的图形（我们可以尝试 `plot(f, 0, 2)` 来更清楚地看到 $t = 0$ 处的零导数）：

```python
sage: plot(f, 0, 100)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_333_0.png)

### 14.2.2 可用函数

我们已经在 GSL 的求解器对象中提到了 `rk8pd` 方法。其他可用方法包括：

- `rkf45`：Runge-Kutta-Fehlberg，一种 5 阶和 4 阶自适应方法；
- `rk2`：3 阶和 2 阶自适应 Runge-Kutta 方法；
- `rk4`：经典的 4 阶 Runge-Kutta 方法；
- `rk2imp`：一种隐式 2 阶 Runge-Kutta 方法，在区间中点处求值；
- `rk4imp`：一种隐式 4 阶 Runge-Kutta 方法，在“高斯点”⁴处求值；
- `bsimp`：隐式 Bulirsch-Stoer 方法；
- `gear1`：隐式单步 Gear 方法；
- `gear2`：隐式两步 Gear 方法。

关于所有这些方法的更多细节，请读者参阅 [AP98]。

应当注意，我们为数值积分提到的 GSL 对机器浮点数的限制——因而是固定精度——同样适用于求解微分方程。

Maxima 也提供了用其自身语法数值求解微分方程的程序：

```sage
sage: t, y = var('t, y')
sage: desolve_rk4(t*y*(2-y), y, ics=[0,1], end_points=[0, 1], step=0.5)
[[0, 1], [0.5, 1.12419127424558], [1.0, 1.461590162288825]]
```

`desolve_rk4` 函数使用 4 阶 Runge-Kutta 方法（与 GSL 的 `rk4` 相同），其参数包括：

- 方程的右端 \(y'(t) = f(t,y(t))\)，这里为 \(y' = ty(2-y)\)；
- 未知函数的名称，这里为 \(y\)；
- 初始条件 `ics`，这里为 \(t = 0\) 且 \(y = 1\)；
- 求解区间 `end_points`，这里为 \([0,1]\)；
- 求解步长，这里为 0.5。

我们省略类似的命令 `desolve_system_rk4`，它已在第 4 章提到，适用于微分方程组。Maxima 同样受限于机器精度。

如果我们想要任意精度解，可以使用 `mpmath` 包中的 `odefun`：

⁴二次 Legendre 多项式的根，它们被平移到区间 \([t, t + h]\) 上，其名称源自 Gauss-Legendre 求积规则。

```sage
sage: import mpmath
sage: mpmath.mp.prec = 53
sage: sol = mpmath.odefun(lambda t, y: y, 0, 1)
sage: sol(1)
mpf('2.7182818284590451')
sage: mpmath.mp.prec = 100
sage: sol(1)
mpf('2.7182818284590452353602874802307')
sage: N(exp(1), 100)
2.7182818284590452353602874714
```

`mpmath.odefun` 函数的参数如下：

- 方程组的右端，以函数 \((t,y) \mapsto f(t,y(t))\) 的形式给出，这里为 \(y'=y\)，与 `ode_solver` 函数类似。系统的维数由函数返回值的维数自动推断；
- 初始条件 \(t_0\) 和 \(y(t_0)\)，这里为 \(y(0)=1\)。

例如，对于这个二维系统

$$\begin{cases} y_1' &= -y_2 \\ y_2' &= y_1 \end{cases}$$

其解为 \((\cos(t),\sin(t))\)，初始条件为 \(y_1(0)=1\) 和 \(y_2(0)=0\)：

```sage
sage: mpmath.mp.prec = 53
sage: f = mpmath.odefun(lambda t, y: [-y[1], y[0]], 0, [1, 0])
sage: f(3)
[mpf('-0.98999249660044542'), mpf('0.14112000805986721')]
sage: (cos(3.), sin(3.))
(-0.98999249660044505, 0.141120008059867)
```

`mpmath.odefun` 函数依赖 Taylor 方法。对于次数 \(p\)，它使用：

$$y(t_{n+1}) = y(t_n) + h\frac{dy}{dt}(t_n) + \frac{h^2}{2!}\frac{d^2y}{dt^2}(t_n) + \ldots + \frac{h^p}{p!}\frac{d^py}{dt^p}(t_n) + O(h^{p+1}).$$

主要问题在于计算 \(y\) 的导数。为此，`odefun` 计算近似值

$$[\widetilde y(t_n+h),\ldots,\widetilde y(t_n+ph)] \approx [y(t_n+h),\ldots,y(t_n+ph)]$$

使用较不精确的 Euler 方法的 \(p\) 步。然后我们计算

$$\frac{dy}{dt}(t_n) \approx \frac{\widetilde y(t_n+h)-\widetilde y(t_n)}{h}, \qquad \frac{dy}{dt}(t_n+h) \approx \frac{\widetilde y(t_n+2h)-\widetilde y(t_n+h)}{h}$$

然后

$$\frac{d^2y}{dt^2}(t_n) \approx \frac{\frac{dy}{dt}(t_n+h)-\frac{dy}{dt}(t_n)}{h},$$

## 15 枚举与组合数学

本章主要介绍 Sage 中处理以下组合问题的内容：枚举（集合 $S$ 中有多少个元素？）、列出（生成 $S$ 的所有元素，或遍历它们）以及随机选择（根据给定分布，例如均匀分布，从集合 $S$ 中随机选择一个元素）。这些问题自然地出现在概率计算中（在扑克中获得顺子或四个 A 的概率是多少？）、统计物理中，也出现在计算机代数中（有限域中元素的数量），或算法分析中。组合数学涵盖的领域要广泛得多（偏序、表示论……），我们只给出一些指向 Sage 所提供可能性的线索。图在第 16 章讨论。

计算组合数学的一个特点是需要操作的对象和集合种类繁多。不可能将它们全部描述出来，更不用说全部实现。在一些示例（§15.1）之后，本章说明其基本方法：提供用于描述常见组合集合的基本构件 §15.2，用于组合它们以构造新示例的工具 §15.3，以及用于统一解决一大类问题的通用算法 §15.4。初读时，本章可以快速跳过，在 §15.1.2 和 §15.3 节的总结处稍作停留。

在这个领域中，Sage 的能力比大多数计算机代数系统都要广泛得多，并且正在快速扩展；与此同时，它仍然相当新，并且存在许多不必要的限制和不一致之处。

### 15.1 初始示例

### 15.1.1 扑克与概率

我们首先解决一个经典问题：枚举扑克游戏中某些牌的组合，以推导其概率。

扑克牌中的一张牌由花色（红桃、方块、黑桃或梅花）和点数（2、3、……、10、J、Q、K、A）确定。游戏使用一副完整的牌，即花色集合与点数集合的笛卡尔积：

Cards = Suits × Values = {(s,v) | s ∈ Suits 且 v ∈ Values}。

我们在 Sage 中构造这些示例：

```sage
sage: Suits = Set(["Hearts", "Diamonds", "Spades", "Clubs"])
sage: Values = Set([2, 3, 4, 5, 6, 7, 8, 9, 10,
....:               "Jack", "Queen", "King", "Ace"])
sage: Cards = cartesian_product([Values, Suits])
```

有 4 种花色和 13 个可能点数，因此扑克牌中有 4 × 13 = 52 张牌：

```sage
sage: Suits.cardinality()
4
sage: Values.cardinality()
13
sage: Cards.cardinality()
52
```

随机抽取一张牌：

```sage
sage: Cards.random_element()
(6, 'Clubs')
```

随机抽取两张牌：

```sage
sage: Set([Cards.random_element(), Cards.random_element()])
{(2, 'Hearts'), (4, 'Spades')}
```

回到我们的主题，我们将考虑一种简化版扑克，其中每位玩家直接抽取五张牌，组成其手牌。所有牌互不相同，且抽取顺序无关紧要；因此，一手牌是牌集合中大小为 5 的子集。为了随机抽取一手牌，我们首先构造所有可能手牌的集合，然后请求随机选择一个元素：

```sage
sage: Hands = Subsets(Cards, 5)
sage: Hands.random_element()
{(4, 'Hearts'), (9, 'Diamonds'), (8, 'Spades'),
 (9, 'Clubs'), (7, 'Hearts')}
```
