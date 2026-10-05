

```
(c:magnitudes<->distance Vega-apparent-magnitude
Vega-absolute-magnitude
Vega-magnitude-distance)
```

我们现在提供一些测量数据。天织星非常亮；它的视等非常接近零。（使用哈勃空间望远镜完成了这项非常精确的测量。Bohlin 和 Gillilland [14]）。

```
(tell! Vega-apparent-magnitude
(->interval 0.026 0.008
'Bohlin-Gillilland2004)
```

此外，天织星的绝对等也以相当精度已知 [44]：

```
(tell! Vega-absolute-magnitude
(->interval 0.582 0.014
'Gatewood2008)
```

结果，我们对天织星的距离得到了一个相当不错的估计，它仅取决于这些测量值：

```
(inquire Vega-magnitude-distance
((vega-magnitude-distance)
(has-value interval 7.663 7.8199)
(depends-on gatewood2008 bohlingillilland2004))
```

遗憾的是，我们在两个不同的单元中拥有距离，让我们用一个传播器将它们连接起来：

```
(c:same Vega-magnitude-distance Vega-parallax-distance)
```

此时我们得到了一个更佳的天织星距离值——一个区间，其上限与之前相同（在第 336 页），但下限稍高一点：

```
(inquire Vega-parallax-distance
((vega-parallax-distance)
(has-value interval 7.663 7.6787))
(depends-on fvanleeuwen2007 gatewood-dejonge1995
gatewood2008 bohlingillilland2004))
```

Gatewood 和 de Jonge 1995 年的测量在这里真的重要吗？让我们来一下：

```
(retract; 'Gatewood-deJonge1995)

(inquire Vega-parallax-distance
(vega-parallax-distance)
(has-value (interval 7.663 7.7))
(depends-on fvanleeuwen2007nov
gatewood2008
bohlinggillillilland2004))
```

确实重要。1995 年的测量值拉低了区间的上限。

# 测量改进了！

我们有两种计算天织星距离的方法——通过视差和通过等等。这里有一个非同寻常之处：视差和等等的测量区间都分别通过来自另一方的信息得到了改进。为了保持系统的一致性，这是必须的。

看天织星的视等等。由 Bohlin 和 Gilliland 提供的原始测量结果为 $m = 0.026 \pm 0.008$。这转化为区间：

```
-->interval 0.026 0.008
(interval .018 .034)
```

但现在这个值稍微更好——[0.018, 0.028456]：

```
(inquire Vega-apparent-magnitude
(vega-apparent-magnitude)
(has-value (interval 1.8e-2 2.8456e-2))
(depends-on fvanleeuwen2007nov
bohlin-gilliland2004))
```

上限必须被拉低以与视差测量信息保持一致。对于每个测量量都是如此。Gatewood 2008（第 338 页）提供的绝对等等为：

```
-->interval 0.582 0.014
(interval .568 .596)
```

但现在下限被拉高了：

```
(inquire Vega-absolute-magnitude)
((vega-absolute-magnitude)
(has-value interval 5.8554e-1 5.96e-1)
(depends-on gatewood2000
  fvanleeuwen2007nov
  bohlin-gilliland2004))
```

视差也通过等等测量信息得到了改进：

```
(inquire Vega-parallax)
((vega-parallax)
(has-value interval 6.2963e-7 6.3267e-7)
(depends-on fvanleeuwen2007nov
  gatewood2008
  bohlin-gilliland2004))
```

计算在所有方向传播的这一事实为我们理解任何新信息的含义提供了一个强大的工具。

# 练习 7.1：让编写传播网络变得更简单

在我们的传播系统中，编写构建即使是简单的网络的代码是非常痛苦的，因为所有内部节点必须命名。例如，一个转换摄氏和华氏温度的约束传播器看起来如下：

```
(define-c:prop (celsius fahrenheit)
(let-cells (u (nine 9) (five 5) (thirty-two u))
  (c:* celsius u)
  (c:* five u)
  (c:* thirty-two fahrenheit))
```

如果能对某些传播器使用表达式语法将好得多，我们可以写成：

```
(define-c:prop (celsius fahrenheit)
(c:+ (ce:* (ce:/ constant 9) (constant 5))
  celsius))

(constant thirty-two)
```

如果能对某些传播器使用表达式语法将好得多，我们可以写成：

```
(define-c:prop (celsius fahrenheit)
(c:+ (ce:* (ce:/ constant 9) (constant 5))
  celsius))

(constant thirty-two)
```
（注：此处原文示例存在重复，在翻译时已遵循“不要重复输出原文”原则进行逻辑处理，但为保持代码结构完整，此处保留了代码块逻辑。修正：原文翻译如下：）

$ce:*$ 和 $ce+$ 是创建单元格的构造函数。

除了约束传播器，还有如 $p+$ 这样的方向传播器。编写一个程序，从这些测量名称中选择 $R_1$ 的值。

# 练习 7.2：电路设计问题

注意：做这个问题不需要了解电子学。Anna 正在设计一个晶体管偏置。电压分压器由两个电阻 $R_1$ 和 $R_2$ 组成 $\rho$ 是输出电压与电源电压的比值。$Z$ 是分压器的电阻。

![](img/2e770736573f9ba6300d828c1_390.png)

这里是相关的方程：

$$\rho = \frac{V_{out}}{V_{in}}$$
$$\rho = \frac{R_1}{R_2}$$
$$Z = R_1$$

由于 Anna 有许多这样的问题，她制作了一个传播网络来帮助她：

![](img/2e770736573f9ba6300d828c1_391.png)

- **a.** 实现此图的传播网络。
- **b.** Anna 有一个电压在 14.5 到 15.5 伏之间的电源，她需要分压器的输出电压在 3.5 到 4.0 伏之间：$V_{in} \in [14.5, 15.5]$。她有一个 $R_2$ 为 47000 欧姆的电阻。可以从哪些值范围选择 $R_1$？她能选择出一个符合规格的 $R_1$ 值吗？
- **c.** Anna 还需要分压器的电阻在 20000 到 30000 欧姆之间：$Z \in [20000, 30000]$。所以她的真实问题是在给定 $\rho$ 和 $Z$ 规格的情况下，找到合适的数值范围。

如果不是选择 $R_2$（记住撤销该值的支持！），而是断言 $Z$ 规格，这将决定 $R_1$ 和 $R_2$；但是……
- **d.** 如果我们现在告诉 $R_2$ 它在 1000 到 500000 欧姆之间的范围内，传播网络将收敛并给出一个 $R_2$ 的有效答案。

# 练习 7.3：局部一致性——一个项目

传播是攻击局部一致性问题的方法。例如，Waltz 算法是解释多面体线条图的传播方法。

- **a.** 对于这些实验，你需要一个离散集合的“算术”。你需要并集、交集以及一个相对于另一个的补。构建这样的算术。
- **b.** 节点的可能集是关于实际状态的部分信息：可能集越小，我们关于节点的信息就越多。如果我们把状态的知识表示为传播单元格，那么合并就是它们的交集。让交集离散集合成为通用合并的处理程序。

