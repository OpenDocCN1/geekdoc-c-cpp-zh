
```sage
sage: alpha, m, x = var('alpha, m, x'); q = function('q')(x)
sage: p = (x - alpha)^m * q
sage: p.derivative(x)
(-alpha + x)^(m - 1)*m*q(x) + (-alpha + x)^m*diff(q(x), x)
sage: simplify(p.derivative(x)/(x-alpha))
0
```

因此，$p$ 与 $p'$ 的最大公因式（gcd）是乘积 $\prod_{\alpha\in\Gamma}(x-\alpha)^{m_\alpha-1}$，其中 $\Gamma$ 是 $p$ 的重数严格大于 1 的根组成的集合，$m_\alpha$ 是根 $\alpha$ 的重数。若用 $d$ 表示这个最大公因式，则商 $p/d$ 具有所需性质。

注意，$p$ 除以 $d$ 所得商的次数严格小于 $p$ 的次数。特别地，如果这个次数严格小于 5，就可以用根式表示这些根。下面的例子用一个次数为 13 的有理系数多项式说明了这一点。

```sage
sage: R.<x> = PolynomialRing(QQ, 'x')
sage: p = 128 * x^13 - 1344 * x^12 + 6048 * x^11 - 15632 * x^10 \
.....: + 28056 * x^9 - 44604 * x^8 + 71198 * x^7 - 98283 * x^6 \
.....: + 105840 * x^5 - 101304 * x^4 + 99468 * x^3 - 81648 * x^2 \
.....: + 40824 * x - 8748
sage: d = gcd(p, p.derivative())
sage: (p // d).degree()
4
sage: roots = SR(p // d).roots(multiplicities=False)
sage: roots
[1/2*I*sqrt(3)*2^(1/3) - 1/2*2^(1/3),
 -1/2*I*sqrt(3)*2^(1/3) - 1/2*2^(1/3),
 2^(1/3),
 3/2]
sage: [QQbar(p(alpha)).is_zero() for alpha in roots]
[True, True, True, True]
```

## 12.2 数值解

数学中传统上存在*离散*与*连续*的二分法。数值分析在一定程度上弥合了这一鸿沟：数值分析的一个主要方面，是通过实验性视角研究关于实数（实数明确属于连续领域）的问题，而这一过程常常借助计算机，计算机则属于离散领域。

关于非线性方程的求解，除了计算近似值之外，还会产生许多自然的问题：给定方程有多少个实根？有多少个虚根、正根或负根？

本节开始针对代数方程这一特殊情形回答此类问题。然后，我们描述一些计算非线性方程近似解的方法。

```sage
sage: def sturm(p, a, b):
....:     assert p.degree() > 2
....:     assert not (p(a) == 0)
....:     assert not (p(b) == 0)
....:     assert a <= b
....:     remains = [p, p.derivative()]
....:     for i in range(p.degree() - 1):
....:         remains.append(-(remains[i] % remains[i + 1]))
....:     evals = [[], []]
....:     for q in remains:
....:         evals[0].append(q(a))
....:         evals[1].append(q(b))
....:     return count_sign_changes(evals[0]) \
....:         - count_sign_changes(evals[1])
```

下面是函数 `sturm()` 的一个使用示例。

```sage
sage: R.<x> = PolynomialRing(QQ, 'x')
sage: p = (x - 34) * (x - 5) * (x - 3) * (x - 2) * (x - 2/3)
sage: sturm(p, 1, 4)
2
sage: sturm(p, 1, 10)
3
sage: sturm(p, 1, 200)
4
sage: p.roots(multiplicities=False)
[34, 5, 3, 2, 2/3]
sage: sturm(p, 1/2, 35)
5
```

### 12.2.2 迭代逼近方法

本节说明逼近非线性方程 $f(x) = 0$ 的解的各种方法。此类逼近本质上主要有两种途径。最高效的算法会混合使用这两种途径。

第一种途径构造一系列嵌套区间，其中包含方程的一个解。我们可以控制精度，并且收敛性有保证，但收敛速度并不总是很好。

第二种途径从方程某个解的一个给定近似值开始。如果函数 $f$ 的局部性态足够规则，我们可以计算出一个新的、更精确的解的近似值。通过递推，我们得到近似值序列。这种方法假定已知目标数的一个初步近似值。此外，其性能取决于函数 $f$ 良好的局部性态：我们无法*先验地*规定答案的精度；更糟的是，近似值序列的收敛性也不一定有保证。

本节始终考虑非线性方程 $f(x)=0$，其中 $f$ 是定义在区间 $[a,b]$ 上并在该区间上连续的数值函数。我们假定 $f$ 在区间 $[a,b]$ 端点处的值非零且符号相反：换言之，乘积 $f(a)f(b)$ 严格为负。$f$ 的连续性保证方程 $f(x)=0$ 在区间 $[a,b]$ 内至少存在一个解。

对于所讨论的每种方法，我们都用以下函数进行实验。

```sage
sage: f(x) = 4 * sin(x) - exp(x) / 2 + 1
sage: a, b = RR(-pi), RR(pi)
sage: bool(f(a) * f(b) < 0)
True
```

需要注意，对于这个函数，命令 `solve` 没有用处。

```sage
sage: solve(f(x) == 0, x)
[sin(x) == 1/8*e^x - 1/4]
```

```sage
sage: f.roots()
Traceback (most recent call last):
...
RuntimeError: no explicit roots found
```

求解非线性方程的算法可能非常耗时：在继续之前，最好采取某些预防措施。特别地，我们应当通过研究所涉函数的连续性、可微性以及其符号变化来确保解存在；在此绘制函数图像可能很有用（见第 4 章）。

**二分法。** 该方法基于第一种途径：构造一系列嵌套区间，其中每个区间都包含方程 $f(x)=0$ 的一个解。

我们找到区间 $[a,b]$ 的中点 $c$。假定 $f(c) \ne 0$（否则我们已经找到一个解）。要么 $f(a)f(c)$ 为负，因此区间 $[a,c]$ 必定包含方程的一个解；要么 $f(c)f(b)$ 为负，因此区间 $[c,b]$ 包含方程的一个解。因此，我们可以构造一个包含解且长度为区间 $[a,b]$ 长度一半的区间。通过迭代这一构造，我们得到一个具有所需性质的区间序列。为实现这一途径，我们如下定义一个 Python 函数 `intervalgen`。

```sage
sage: def phi(s, t): return (s + t) / 2
sage: def intervalgen(f, phi, s, t):
....:     msg = '{0} wrong arguments: f({0})*f({1})>=0'.format(s, t)
....:     assert (f(s) * f(t) < 0), msg
....:     yield s
....:     yield t
....:     while True:
....:         u = phi(s, t)
....:         yield u
....:         if f(u) * f(s) < 0:
....:             t = u
....:         else:
....:             s = u
```

![](img/99840d73c45ee58b635c4eedc727fd9a_280_0.png)

图 12.2 – 函数 $f$ 的图像。

这个函数的定义值得解释。`intervalgen` 定义中的关键字 `yield` 会把它变成一个*生成器*（见 §15.2.4）。当调用生成器的 `next()` 方法时，如果解释器看到关键字 `yield`，所有局部数据都会被保存，执行被中断，并立即返回该关键字右侧的表达式。下一次调用 `next()` 方法时，会恢复中断前保存的局部数据，并从关键字 `yield` 的下一行继续执行。在无限循环（`while True:`）中使用关键字 `yield`，可以通过一种与数学定义非常相似的语法来实现递归序列。使用关键字 `return` 可以完全停止执行。

参数 `phi` 是一个指定逼近方法的函数。对于二分法，该函数计算区间的中点。为了测试其他同样使用嵌套区间的迭代逼近方法，我们需要给出函数 `phi` 的新定义，然后可以使用函数 `intervalgen` 构造相应的生成器。

该函数的参数 `s` 和 `t` 指定第一个
