
对应于约化为唯一平凡方程 $0=0$ 的系统，而任何多项式都是它的解。显然，这并不是求解线性方程组的推荐方式：第 8 章讨论的具体工具要高效得多！

再看一个稍微不那么平凡的例子：让我们回到第 9.2.3 节的系统 $(S_1)$（见图 9.1a）：

```text
sage: R.<x,y> = QQ[]
sage: J1 = ideal(x^2 + y^2 - 1, 16*x^2*y^2 - 1)
```

消去 $y$ 得到 $\mathbb{Q}[x]$ 的一个理想——因此是主理想——它由多项式 $g$ 生成，而 $g$ 的根是

$$\frac{\pm\sqrt{2\pm\sqrt{3}}}{2}$$

即 $(S_1)$ 的八个解的横坐标：

```text
sage: g = J1.elimination_ideal(y).gens(); g
[16*x^4 - 16*x^2 + 1]
sage: SR(g[0]).solve(SR(x)) # solves by radicals
[x == -1/2*sqrt(sqrt(3) + 2), x == 1/2*sqrt(sqrt(3) + 2),
 x == -1/2*sqrt(2 - sqrt(3)), x == 1/2*sqrt(2 - sqrt(3))]
```

将求得的每个 $x$ 值重新代入 $(S_1)$，我们得到一个仅含 $y$ 的（冗余）方程组，由此可以计算相应的 $y$ 值。

## 消元 = 投影。

上述例子表明，在系统中消去 $y$ 在几何上对应于将解簇投影到方程为 $y = \text{constant}$ 的超平面上（投影记为 $\pi$）。然而，现在让我们分别考虑理想 $C = \langle x^2 + y^2 - 1\rangle$ 和 $H = \langle 16x^2y^2 - 1\rangle$，它们的和为 $J_1$，并再次消去 $y$：

```text
sage: C.elimination_ideal(y).gens()
[0]
sage: H.elimination_ideal(y).gens()
[0]
```

就 $C$ 而言，这并不奇怪。圆 $\{(x,y)\in\mathbb{R}^2\mid x^2+y^2=1\}$ 投影到 $[-1,1]$ 上；然而很明显，任何 $x$ 值都可以被“重新代入”唯一方程 $x^2+y^2-1=0$，而所得关于 $y$ 的方程有复数解。在 $C$ 中消去 $y$ 对应于将复圆 $\{(x,y)\in\mathbb{C}^2\mid x^2+y^2=1\}$ 投影到第一坐标上，而该投影整体就是 $\mathbb{C}$。

$H$ 的情形稍微更复杂一些。方程 $16x^2y^2=1$ 在 $x=0$ 时没有解，即使是复数解也没有。于是我们有

$$V_{\mathbb{C}}(H\cap\mathbb{Q}[x])=\mathbb{C}\subseteq\pi(V_{\mathbb{C}}(H))=\mathbb{C}\setminus\{0\}.$$

事实上，双曲线的投影 $\mathbb{C}\setminus\{0\}$ 不是代数子簇。结论：消元确实对应于（代数闭域上的）投影，但它计算的并不是精确投影，而只是其扎里斯基闭包。

![](img/99840d73c45ee58b635c4eedc727fd9a_208_0.png)

图 9.2 – 由 (9.6) 定义的 $(x,y,t)$ 中曲线的一部分及其在平面 $t=0$ 上的投影。

## 应用：平面几何。

如果 $X\subset\mathbb{C}^k$ 由有理参数化给出

$$X=\{(f_1(t),f_2(t),\ldots,f_k(t))\},\qquad f_1,\ldots,f_k\in\mathbb{Q}(t_1,\ldots,t_n),$$

那么求 $X$ 的隐式方程，就是将由方程 $x_i=f_i(t)$ 定义的 $\mathbb{C}^{k+n}$ 的部分投影到子空间 $(x_1,\ldots,x_k)\cong\mathbb{C}^k$ 上。这是一个消元问题。让我们考虑圆的经典参数化

$$x=\frac{1-t^2}{1+t^2}\qquad y=\frac{2t}{1+t^2} \tag{9.6}$$

它与用 $\tan(\theta/2)$ 表示 $(\cos\theta,\sin\theta)$ 的表达式相关。它转化为定义 $\mathbb{Q}[x,y,t]$ 的一个理想的多项式关系：

```text
sage: R.<x,y,t> = QQ[]
sage: Param = R.ideal((1-t^2)-(1+t^2)*x, 2*t-(1+t^2)*y)
```

让我们消去 $t$：

```text
sage: Param.elimination_ideal(t).gens()
[x^2 + y^2 - 1]
```

我们得到圆的一个方程。我们可以注意到，该方程在 $(x,y)=(-1,0)$ 处为零，尽管参数化 (9.6) 并不经过该点，因为圆去掉一个点不是代数子簇。

另一个例子：让我们画出方程

$$C_t:\qquad x^2+(y-t)^2=\frac{t^2+1}{2} \tag{9.7}$$

的几个圆 $(C_t)$，使用 Sage 命令（见图 9.3）：

```text
sage: R.<x,y,t> = QQ[]
sage: eq = x^2 + (y-t)^2 - 1/2*(t^2+1)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_209_0.png)

![](img/99840d73c45ee58b635c4eedc727fd9a_209_1.png)

图 9.3 一族圆及其包络。

```text
sage: fig = add((eq(t=k/5)*QQ[x,y]).plot() for k in (-15..15))
sage: fig.show(aspect_ratio=1, xmin=-2, xmax=2, ymin=-3, ymax=3)
```

我们看到，圆族 $\mathcal{C}_t$ 的*包络*出现了，它是一条与所有 $\mathcal{C}_t$ 相切的“极限曲线”；我们可以非正式地把它描述为与该族“无限接近的圆”的“交点”集合。

更准确地说，如果 $f$ 是可微函数，且曲线 $\mathcal{C}_t$ 对任意 $t$ 都由 $f(x,y,t)=0$ 定义，那么 $\{\mathcal{C}_t\}$ 的包络是满足下式的点 $(x,y)$ 的集合

$$\forall t,\quad f(x,y,t)=0 \qquad\text{and}\qquad \frac{\partial f}{\partial t}(x,y,t)=0. \tag{9.8}$$

在圆 (9.7) 的情形中，函数 $f(x,y,t)$ 是多项式。它们的包络是 (9.8) 的解在 $(x,y)$ 平面上的投影，因此我们可以通过如下消元计算确定其方程：

```text
sage: env = ideal(eq, eq.derivative(t)).elimination_ideal(t)
sage: env.gens()
[2*x^2 - 2*y^2 - 1]
```

剩下的只需画出所得到的曲线：

```text
sage: env.change_ring(QQ[x,y]).plot((x,-2,2), (y,-3,3))
```

## 结式与消元。

前面例子中执行的消元隐含地基于 Sage 自动计算的 Gröbner 基。然而，我们在本书中已经遇到过另一种消元工具：结式。

让我们考虑两个非常数多项式 $p,q \in K[x_1,\ldots,x_n,y]$。记 $\operatorname{Res}_y(p,q)$ 为 $p$ 和 $q$ 的结式，这里把它们视为单变量 $y$ 的多项式，系数在 $K[x_1,\ldots,x_n]$ 中。我们在 §7.3.3 中已经看到，它是 $K[x_1,\ldots,x_n]$ 中的一个多项式；它在 $u\in K^n$ 处为零，当且仅当 $p(u_1,\ldots,u_n)$ 和 $q(u_1,\ldots,u_n)$（它们是 $K[y]$ 中的两个多项式）有公共零点，除非 $p$ 和 $q$ 的（关于 $y$ 的）首项系数本身在 $u$ 处为零。

我们一些只涉及两个多项式的消元计算可以用结式代替。例如，圆 (9.7) 的包络方程是

```text
sage: eq.derivative(t).resultant(eq, t)
x^2 - y^2 - 1/2
```

结式 $\operatorname{Res}_y(p,q)$ 是消元理想 $(p,q)\cap K[x_1,\ldots,x_n]$ 中的一个元素。然而，即使在 $n=1$ 的情形（此时消元理想是主理想），并且即使 $p$ 和 $q$ 关于 $y$ 的首项系数互素，结式也不一定生成消元理想：

```text
sage: R.<x,y> = QQ[]
```

## 不等式

让我们考虑顶点为 $A=(0,0)$、$B=(1,0)$ 和 $C=(x,y)$ 的三角形。假设角 $\widehat{BAC}$ 和 $\widehat{CBA}$ 相等，并尝试通过计算证明该三角形是等腰三角形。通过引入参数 $t=\tan\widehat{A}=\tan\widehat{B}$，该问题可由方程 $y=tx=t(1-x)$ 编码，并且我们需要证明它们蕴含

$$x^2+y^2=(1-x)^2+y^2.$$

使用 Sage，我们得到：

```text
sage: R.<x,y,t> = QQ[]
sage: J = (y-t*x, y-t*(1-x))*R
sage: (x^2+y^2) - ((1-x)^2+y^2) in J
False
```

这是可以预料到的：当 $x=y=t=0$ 时，假设条件成立，但结论为假！从几何上看，我们必须排除退化三角形的情形，这种三角形可以有两个相等的角却不是等腰三角形。

如何编码约束 $t\ne 0$？技巧是引入辅助变量 $u$，并强制 $tu=1$。计算变为：

```text
sage: R.<x,y,t,u> = QQ[]
sage: J = (y-t*x, y-t*(1-x), t*u-1)*R
sage: (x^2+y^2) - ((1-x)^2+y^2) in J
True
```

现在我们得到了预期的结果。顺便指出，我们可以只用一个辅助变量，借助形如 $t_1t_2\cdots t_nu=1$ 的方程，同时迫使若干个表达式为零。

