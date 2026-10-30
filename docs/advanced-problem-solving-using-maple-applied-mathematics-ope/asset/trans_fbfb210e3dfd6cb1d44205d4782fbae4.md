

# diff 或 Diff – *微分或偏微分*

调用序列
`diff(f, x1, ..., xj)`

\[
\frac{d^j}{dx_1\cdots dx_j}f
\]

`diff(f, [x1$])`

\[
\frac{d^n}{dx_1^n}f
\]

**Remark:** these calling sequences are also valid with the inert *Diff* command

**Parameters**

- `f` — 代数表达式或方程
- `x1, x2, ..., xj` — 表示微分变量的名称
- `n` — 代数表达式进入微分构造如 x$n，代表 n 阶导数，假定为整数阶微分

# solve – *求解一个或多个方程*

调用序列
`solve(equations, variables)`

**Parameters**

- `equations` — 方程或不等式，或方程或不等式的集合或列表
- `variables` — （可选）名称或名称的集合或列表；求解的未知数

# fsolve – *使用浮点算术求解一个或多个方程*

调用序列
`fsolve(equations, variables, complex)`

**Parameters**

- `equations` — 方程，set(equation)，表达式，set(expression)，list(equation)
- `variables` — （可选）名称或名称的集合或列表；求解的未知数
- `complex` — （可选）文字；搜索复数解

> Note: For simple functions *f(x)*, Maple can use *f′(x)*, *f″(x)*, etc., for derivatives.

# Basic Applications Calculus Max-Min Theory

# Example 3.2. Chemical Manufacturing Company.

一家化工制造公司以每吨 200 美元的价格出售硫酸。*x* 吨的日总生产成本为美元

$$C(x)=150000+145.5x+0.0025x^2,$$

日产量最多为 7,500 吨。制造商应生产多少吨硫酸才能使日利润最大化？

*Solution.* 利润函数为

$$\begin{aligned}
Profit &= Revenue-Cost \\
&=(200x)-(150000+145.5x+0.0025x^2) \\
&=-150000+54.5x-0.0025x^2 \qquad \text{for }0\le x\le 7000
\end{aligned}$$

*Profit* 是二阶可微的，因此使用 Maple 进行二阶导数检验。我们将 Maple 的 *D* 运算符应用于 *Profit* 函数以计算导数函数。

```
〉 Profit := x → −150000 + 54.5 · x − 0.0025 · x²;
dProfit := D(Profit);
d2Profit := D(dProfit);
        Profit := x → −150000 + 54.5 · x + (−1)0.0025 · x²
        dProfit := x → 54.5 − 0.0050 x
        d2Profit := x → −0.0050
```

```
〉 c := solve(dProfit(x) = 0, x);
        c := 10900.
```

```
〉 Profit(c);
        147025.0000
```

我们必须检查端点，因为 *Profit* 定义在区间 [0, 7500] 上。

```
〉 [0, Profit(0)], [7500, Profit(7500)];
        [0, −150000.], [7500, 118125.0000]
```

即使 *Profit(c)* 最大，*c* = 10,900 吨也大于最大产量 7,500 吨。因此公司应尽可能多地生产，7,500 吨，最大 *Profit*(7500) = $118,125.00。

通过绘制 *Profit* 在 [0, 7500] 和 [0, 12000] 上的图形来验证分析，显示端点解被选中是因为临界点在 *Profit* 的定义域之外。

# Example 3.3. Computer Production.

*Bell Computers* 生产一台 SP6 计算机的 *可变成本* 为 250 美元。他们在工厂运营并生产计算机时有 5,500 美元的 *固定成本*。如果 *Bell* 在其新 SP6 上花费 *x* 美元用于广告，他们

可以以每台 50 美元的价格出售 $\sqrt{x}$ 台 SP6。公司应生产多少台 SP6 计算机才能使利润最大化？

**Solution.** 由于收入是价格乘以数量，总成本是固定成本加上可变成本乘以数量，Bell 的利润函数由下式给出

```
```text
> varcost, fixedcost, price := 250, 5500, 550:

> Revenue := x → price · √x:
  Cost := x → fixedcost + x · varcost + √x:
> Profit := Revenue − Cost:  # Note this is an equation of functions!
  Profit(x);

                    300√x − 5500 − x
```
```

Profit 是二阶可微的，因此再次使用 Maple 进行二阶导数检验。

```
```text
> dProfit := D(Profit):
  dProfit(x);

  c := solve(dProfit(x) = 0, x);

                    150
                    ─── − 1
                    √x
  c := 22500

> d2Profit := D(dProfit):
  d2Profit(c);

                    √22500
                    ───────
                    6750000
```
```

由于 $Profit''(c)$ 为负，我们得到最大值 $Profit(22500) = \$17,000$。图形将验证我们的分析。

```
```text
> plot(Profit, 0..30000, thickness = 2, title = “Bell Computer Profit”);
```
```

![](img/0f04050177d82aebd17d3383d7334896_115_0.png)

返回本节开头介绍的抽水站示例。

# **Example 3.4. Oil Pumping Station Location.**

Rigs-R-Us 的一座石油钻井平台位于离岸 9.5 英里处。钻井平台将通过一条水下管道连接到一座抽水站，然后通过一条陆上管道连接到炼油厂。炼油厂距离钻井平台沿海岸线向下 15.7 英里。见图 3.2。水下管道安装成本为每英里 32,575 美元

![](img/0f04050177d82aebd17d3383d7334896_116_0.png)

陆上管道成本为每英里 14,442 美元。确定抽水站的位置以最小化管道总成本。

*Problem.*

找出抽水站位置与管道安装成本之间的关系，然后最小化成本。

*Assumptions.*

首先，我们假设如果以更大批量购买管道则没有成本节约。我们进一步假设铺设管道的准备地形成本，无论是海上还是陆上，都包含在给定的每英里成本数字中。

*Variables.*

$x$ = 抽水站沿水平距离的位置，从 $x = 0$ 到 $x = 15.7$ 英里

$TC$ = 水下和陆上管道的管道总成本

*Model Construction.*

使用毕达哥拉斯定理计算水下管道距离；即高度为 9.5 英里、沿海岸线基数为 $x$ 英里的直角三角形的斜边。斜边的长度为 $\sqrt{9.5^2 + x^2}$。岸上管道的长度为 $15.7 - x$。因此总成本为

```
$$TC = 32575\cdot\sqrt{9.5^2+x^2}+14442\cdot(15.7-x).$$
```

我们转向 Maple 进行二阶导数检验以确定最小成本抽水站位置。

```
> TC := x → 32575 · √(9.5² + x²) + 14442 · (15.7 − x) :
> dTC := D(TC);

\[
dTC := x \to \frac{32575x}{\sqrt{90.25+x^2}} - 14442
\]

> c := solve(dTC(x) = 0, x);

\[
c := 4.698818368
\]

> d2TC := D(dTC);

\[
d2TC := x \to \frac{32575}{\sqrt{90.25+x^2}} - \frac{32575x^2}{(90.25+x^2)^{3/2}}
\]

> d2TC(c);

\[
2469.416868
\]
```

由于 c = 4.6988 时二阶导数为正，我们得到最小总成本。因此，如果抽水站位于距离炼油厂 15.7 − 4.6988 ≈ 11.0 英里处，我们将使管道总成本最小化，TC(c) = $50,4126.27。

再次，我们绘制总成本函数以验证我们的结果。

```
> plot(TC, 0..8, thickness = 2, title = “Pipeline Cost”);
```

![](img/0f04050177d82aebd17d3383d7334896_117_0.png)

如何修改 plot 命令以在曲线上显示最小值处的点？

# Exercises

+   1. 每天早上高峰时段，10,000 人从新泽西州前往纽约。乘坐地铁需要 40 分钟。如果有 $x$ 千人驾车前往纽约市，行程需要 $20+5x$ 分钟。
+   
+   (a) 制定问题以最小化人均平均出行时间。
+   
+   (b) 找到使人均平均时间最小化的驾车人数。

+   2. 设 $f(x)=2x^3-1$。使用微积分求
+   
+   $$\max_{-1\le x\le 1} f(x)$$

的最优解

+   3. 求 $f(x)=\sin(2+\pi x)/x$ 在区间 $1\le x\le 4$ 上的所有极值。

+   4. 考虑函数 $f(x)=0.5x^3-8x^2$。
+   
+   (a) 使用图形找到并分类 $f$ 的所有极值。
+   
+   (b) 使用分析技术（即微积分）找到并分类 $f$ 的所有极值。
+   
+   (c) 定义：可微函数
+   
+   - **凸或上凸** 在区间 $[a,b]$ 上 iff $f$ 位于其所有切线之上；即对于 $[a,b]$ 中所有 $x_1<x<x_2$，
+     $$f'(x)\le\frac{f(x_2)-f(x_1)}{x_2-x_1}$$
+   
+   - **凹或下凸** 在区间 $[a,b]$ 上 iff $f$ 位于其所有切线之下；即对于 $[a,b]$ 中所有 $x_1<x<x_2$，
+     $$f'(x)\ge\frac{f(x_2)-f(x_1)}{x_2-x_1}$$
+   
+   二次可微函数
+   
+   - 在 $[a,b]$ 上 **凸** iff 其二阶导数非负。
+   - 在 $[a,b]$ 上 **凹** iff 其二阶导数非正。
+   
+   应用 **凹**（下凸）的定义来证明 $f$ 在区间 $[-6,5]$ 上是凹的。
+   
+   (d) $f$ 凸的最大区间？凹的？
+   
+   (e) 为什么在优化中知道凹凸性很重要？

