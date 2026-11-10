

**递推关系与闭式公式。** 现在我们回到 $C(z)$ 的闭式形式：

```sage
sage: z = var('z'); C = s0; C
-1/2*sqrt(-4*z + 1) + 1/2
```

$C(z)$ 的泰勒级数中的第 $n$ 个系数由 $\frac{1}{n!}C(z)^{(n)}(0)$ 给出，我们考察其逐次导数 $C(z)^{(n)}(z)$：

```sage
sage: derivative(C, z, 1)
1/sqrt(-4*z + 1)
sage: derivative(C, z, 2)
2/(-4*z + 1)^(3/2)
sage: derivative(C, z, 3)
12/(-4*z + 1)^(5/2)
```

这表明存在一个简单的显式公式，我们现在就来寻找。下面这个小函数返回 $d_n = n!c_n$：

```sage
sage: def d(n): return derivative(C, n).subs(z=0)
```

取逐次商：

```sage
sage: [ (d(n+1) / d(n)) for n in range(1,17) ]
[2, 6, 10, 14, 18, 22, 26, 30, 34, 38, 42, 46, 50, 54, 58, 62]
```

我们观察到 $d_n$ 满足递推关系 $d_{n+1} = (4n-2)d_n$，由此我们推断出 $c_n$ 满足递推关系 $c_{n+1} = \frac{(4n-2)}{n+1}c_n$。化简后，我们发现 $c_n$ 是第 $(n-1)$ 个卡特兰数：

$$c_n = \mathrm{Catalan}(n-1) = \frac{1}{n}\binom{2(n-1)}{n-1}.$$

我们来验证一下：

```sage
sage: def c(n): return 1/n*binomial(2*(n-1),n-1)
sage: [c(k) for k in range(1, 11)]
[1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862]
sage: [catalan_number(k-1) for k in range(1, 11)]
[1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862]
```

现在我们可以计算更大规模的系数；这里我们计算 $c_{100000}$，它有超过 60000 位数字：

```sage
sage: %time cc = c(100000)
CPU times: user 2.34 s, sys: 0.00 s, total: 2.34 s
Wall time: 2.34 s
sage: ZZ(cc).ndigits()
60198
```

## 代数-微分方程的系统处理

我们使用的方法可以推广到所有递归定义的对象：集合论方程组可以转化为生成函数上的方程组，从而能够递归计算其系数。如果集合论方程足够简单（例如，只涉及笛卡尔积和不相交并），则 $C(z)$ 的方程是代数的。这个方程一般没有闭式解。然而，利用*限定*（confinement），我们可以推导出 $C(z)$ 满足的一个*线性*微分方程。这个微分方程又可以转化为其系数 $c_n$ 上的固定长度递推关系。在这种情况下，该级数称为 *D-有限*（D-finite）的。在初步计算出这个递推关系之后，系数的计算就非常快了。所有这些步骤都是纯算法的，并且计划将 Maple（gfun 和 combstruct 包）或 MuPAD-Combinat（decomposableObjects 库）中已有的实现移植到 Sage 中。

目前，我们以完全二叉树为例来说明这一通用过程。生成函数 $C(z)$ 是代数方程 $P(z,C(z))=0$ 的一个解，其中 $P=P(x,y)$ 是系数在 $\mathbb{Q}$ 中的多项式。在当前情况下，$P=y^2-y+x$。我们对这个方程关于 $z$ 进行形式微分：

```sage
sage: x, y, z = var('x, y, z')
sage: P = function('P')(x, y); C = function('C')(z)
sage: equation = P(x=z, y=C) == 0
sage: diff(equation, z)
diff(C(z), z)*D[1](P)(z, C(z)) + D[0](P)(z, C(z)) == 0
```

或者，以更可读的格式，

$$\frac{dC(z)}{dz}\frac{\partial P}{\partial y}(z,C(z)) + \frac{\partial P}{\partial x}(z,C(z)) = 0.$$

由此我们推导出：

$$\frac{dC(z)}{dz}=-\frac{\frac{\partial P}{\partial x}(z,C(z))}{\frac{\partial P}{\partial y}(z,C(z))}.$$

在完全二叉树的情况下，这给出：

```sage
sage: P = y^2 - y + x; Px = diff(P, x); Py = diff(P, y)
sage: - Px / Py
-1/(2*y - 1)
```

回想一下 $P(z,C(z))=0$。因此，我们可以计算这个分式模 $P$，从而将 $C(z)$ 的导数表示为*系数在 $\mathbb{Q}(z)$ 中的关于 $C(z)$ 的多项式*。为了实现这一点，我们构造商环 $R=\mathbb{Q}(x)[y]/(P)$：

```sage
sage: Qx = QQ['x'].fraction_field(); Qxy = Qx['y']
sage: R = Qxy.quo(P); R
Univariate Quotient Polynomial Ring in ybar
 over Fraction Field of Univariate Polynomial Ring in x
 over Rational Field with modulus y^2 - y + x
```

注意：ybar 是商环中变量 $y$ 的名字；关于商环的更多信息，参见 §7.2.2。我们继续在 $R$ 中计算这个分式：

```sage
sage: fraction = - R(Px) / R(Py); fraction
(1/2*(x - 1/4))*ybar - 1/4/(x - 1/4)
```

我们将结果提升到 $\mathbb{Q}(x)[y]$，然后代入 $z$ 和 $C(z)$，得到 $\frac{\partial}{\partial z}C(z)$ 的表达式：

```sage
sage: fraction = fraction.lift(); fraction
(1/2*(x - 1/4))*y - 1/4/(x - 1/4)
sage: fraction(x=z, y=C)
2*C(z)/(4*z - 1) - 1/(4*z - 1)
```

或者，更清晰地，

$$\frac{\partial C(z)}{\partial z} = \frac{1}{1-4z} - \frac{2}{1-4z}C(z).$$

在这个简单情形中，我们可以直接从该表达式推导出系数在 $\mathbb{Q}[z]$ 中的线性微分方程：

```sage
sage: eqdiff = diff(C,z) == fraction(x=z, y=C); eqdiff
diff(C(z), z) == 2*C(z)/(4*z - 1) - 1/(4*z - 1)
sage: eqdiff = eqdiff.simplify_rational()
sage: eqdiff = eqdiff * eqdiff.rhs().denominator()
sage: eqdiff = eqdiff - eqdiff.rhs()
sage: eqdiff
(4*z - 1)*diff(C(z), z) - 2*C(z) + 1 == 0
```

或者，更清晰地，

$$\left(1-4z\right)\frac{\partial C(z)}{\partial z} + 2C(z) - 1 = 0.$$

在闭式形式上验证这个方程是平凡的：

```sage
sage: Cf = sage.symbolic.function_factory.function('C')
sage: bool(eqdiff.substitute_function(Cf, lambda z: s0(z=z)))
True
```

在一般情况下，我们继续计算 $C(z)$ 的逐次导数。这些导数被*限定*在商环 $\mathbb{Q}(z)[C]/(P)$ 中，该商环在 $\mathbb{Q}(z)$ 上的维数为 $\deg P$。因此，我们最终会在 $C(z)$ 的前 $\deg P$ 个导数之间找到一个线性关系。将其放到一个公分母上，我们得到阶数 $\leq \deg P$ 且系数在 $\mathbb{Q}[z]$ 中的线性微分方程。通过提取微分方程中 $z^n$ 的系数，我们得到所需的系数递推关系；在这个情形中，我们恢复了之前基于闭式形式已经找到的关系：

$$c_{n+1} = \frac{4n-2}{n+1}c_n.$$

在确定正确的初始条件后，就可以递归地计算 $C(z)$ 的系数：

```sage
sage: def C(n): return n if n <= 1 else (4*n-6)/n * C(n-1)
sage: [ C(i) for i in range(10) ]
[0, 1, 1, 2, 5, 14, 42, 132, 429, 1430]
```

如果 $n$ 太大，无法显式计算 $c_n$，则可以寻找与系数序列 $c_n$ 渐近等价的序列。这里同样有通用技术。核心工具是复分析，特别是研究生成函数在其奇点附近的行为。在目前的例子中，奇点位于 $z_0 = 1/4$，我们将得到 $c_n \sim \frac{4^{n-1}}{n^{3/2}\sqrt{\pi}}$。

**小结。** 我们在这里看到计算机代数的一个普遍现象：描述复杂数学对象（实数、序列、形式幂级数、函数、集合）的最佳*数据结构*通常是定义该对象的方程（或方程组，通常带有一些初始条件）。试图寻找这个方程的闭式解并不一定有意义：一方面，这种闭式很少存在（例如，用根式求解多项式的问题），另一方面，方程本身包含了所有必要信息，足以通过算法计算所考虑对象的性质（例如数值近似、初始项或元素、渐近等价），或者与对象本身进行计算（例如对幂级数进行算术运算）。因此，与其解方程，我们不如寻找描述该对象且最适合我们想要解决的问题的方程；另见 §2.2.2。

正如我们在例子中所看到的，限定（例如在有限维向量空间中）是研究此类方程的基本工具。这种限定的概念在消元技术（线性代数、Gröbner 基及其代数-微分推广）中有着广泛的应用。同样的工具在自动求和与恒等式自动验证算法（Gosper 算法、Zeilberger 算法及其推广 [PWZ96]；另见 §2.3.1 中的例子和练习 56）中也是核心。

所有这些技术及其众多推广是当前非常活跃的研究主题的核心：自动组合学和分析组合学，它们在算法分析中有重要应用 [FS09]。它们有望逐步在 Sage 中实现，这也是我们所期望的。

## 15.2 常见枚举集合

### 15.2.1 第一个例子：集合的子集

固定一个大小为 $n$ 的集合 $E$，并考虑 $E$ 的大小为 $k$ 的子集。我们知道这些子集由二项式系数 $\binom{n}{k}$ 计数。因此，我们可以用函数 binomial 计算 $E = \{1, 2, 3, 4\}$ 的大小为 $k = 2$ 的子集个数：

```sage
sage: binomial(4, 2)
6
```

