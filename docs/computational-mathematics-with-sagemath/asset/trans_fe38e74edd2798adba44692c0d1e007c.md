

```
x^3 - 6*I*x^2 - 12*x + 8*I
```

这里，我们也可以写 `p.map_coefficients(conjugate)`，因为对于 \(z \in \mathbb{Q}[i]\)，`conjugate(z)` 与 `z.conjugate` 效果相同。显式调用对象 `z` 的方法更稳健：这样代码适用于所有具有 `conjugate()` 方法的对象，并且只适用于这些对象。

## 多项式环上的运算

多项式对象的父结构，即环 \(A[x]\)，本身就是一等 Sage 对象。让我们简要看看如何使用它们。

第一类方法使我们能够构造特定多项式、随机抽取多项式或枚举族，这里是 \(\mathbb{F}_2\) 上次数恰好为 2 的多项式族：

```sage
sage: list(GF(2)['x'].polynomials(of_degree=2))
[x^2, x^2 + 1, x^2 + x, x^2 + x + 1]
```

我们将在后续章节的示例中调用其中一些方法，以构建我们要在其上工作的对象。第 15 章更一般地解释如何用 Sage 枚举有限集。

其次，系统“知道”每个多项式环的一些基本事实。我们可以检查给定对象是否为环、是否为诺特环：

```sage
sage: A = QQ['x']
sage: A.is_ring() and A.is_noetherian()
True
```

或者检查 \(\mathbb{Z}\) 是否为 \(\mathbb{Q}[x]\) 的子环，以及对于哪些 \(n\)，环 \(\mathbb{Z}/n\mathbb{Z}\) 是整环：

```sage
sage: ZZ.is_subring(A)
True
sage: [n for n in range(20)
....:     if Integers(n)['x'].is_integral_domain()]
[0, 2, 3, 5, 7, 11, 13, 17, 19]
```

这些能力很大程度上依赖 Sage 范畴系统（另见 §5.2.3）。多项式环属于若干“范畴”，如集合范畴、欧几里得环范畴等：

```sage
sage: R.categories()
[Category of euclidean domains,
 Category of principal ideal domains,
 ...
 Category of sets with partial maps, Category of objects]
```

这反映出任何多项式环也是一个集合、一个欧几里得整环，等等。因此，系统可以自动将这些不同范畴中对象的一般性质迁移到多项式环上。

**整除性与欧几里得除法**

| 操作 | Sage 命令 |
|---|---|
| 整除性测试 \(p\mid q\) | `p.divides(q)` |
| 除数的重数 \(q^k\mid p\) | `k = p.valuation(q)` |
| 欧几里得除法 \(p=qd+r\) | `q, r = p.quo_rem(d)` 或 `q, r = p//d, p%d` |
| 伪除法 \(a^k p=qd+r\) | `q, r, k = p.pseudo_quo_rem(d)` |
| 最大公因数 | `p.gcd(q), gcd([p1, p2, p3])` |
| 最小公倍数 | `p.lcm(q), lcm([p1, p2, p3])` |
| 扩展 gcd \(g=up+vq\) | `g, u, v = p.xgcd(q)` 或 `xgcd(p, q)` |
| “中国剩余” \(c\equiv a\pmod p,\ c\equiv b\pmod q\) | `c = crt(a, b, p, q)` |

**其他**

| 操作 | Sage 命令 |
|---|---|
| 插值 \(p(x_i)=y_i\) | `p = R.lagrange_polynomial([(x1,y1), ...])` |
| \(p\in\mathbb{Z}[x]\) 的内容 | `p.content()` |

表 7.3 – 多项式算术。

## 7.2 欧几里得算术

除加法和乘法之外，多项式上最基本的运算就是欧几里得除法和最大公因数计算。相应的运算符和方法（表 7.3）模仿整数上的对应操作。然而，这些运算常常被额外的抽象层隐藏：环的商（§7.2.2）中每次算术运算都涉及隐式欧几里得除法；有理函数（§7.4）的规范化意味着要进行一些 gcd 计算……

### 7.2.1 整除性

**除法。** 欧几里得除法在域中可行，更一般地，在除数的首项系数可逆的交换环中也可行，因为该系数是唯一需要从基环中去除的系数：

```sage
sage: R.<t> = Integers(42)[]; (t^20-1) % (t^5+8*t+7)
22*t^4 + 14*t^3 + 14*t + 6
```

当首项系数不可逆时，我们仍然可以定义*伪欧几里得除法*（简称伪除法）：设 \(A\) 为交换环，\(p,d\in A[x]\)，且 \(a\) 为 \(d\) 的首项系数。那么存在两个多项式 \(q,r\in A[x]\)，满足 \(\deg r<\deg d\)，以及一个整数 \(k\leq\deg p-\deg d+1\)，使得

\[
a^k p=qd+r.
\]

伪除法由 Sage 的 `pseudo_quo_rem` 方法给出。

要执行精确除法，我们也使用欧几里得商运算符 `//`。实际上，用 `/` 除以非常数多项式会返回有理函数类型的结果（见 §7.4），或者在没有意义时失败：

```sage
sage: ((t^2+2*t)//t).parent()
Univariate Polynomial Ring in t over Ring of integers modulo 42
sage: (t^2+t)/t
Traceback (most recent call last):
...
TypeError: self must be an integral domain.
```

**练习 25。** 通常，在 Sage 中，\(\mathbb{Q}[x]\) 中的多项式以单项式基 \((x^n)_{n\in\mathbb{N}}\) 表示。由 \(T_n(\cos\theta)=\cos(n\theta)\) 定义的切比雪夫多项式 \(T_n\) 构成一族正交多项式，因此构成 \(\mathbb{Q}[x]\) 的一组基。前几个切比雪夫多项式为

```sage
sage: x = polygen(QQ); [chebyshev_T(n, x) for n in (0..4)]
[1, x, 2*x^2 - 1, 4*x^3 - 3*x, 8*x^4 - 8*x^2 + 1]
```

编写一个函数，输入 \(\mathbb{Q}[x]\) 中的一个元素，返回其在基 \((T_n)_{n\in\mathbb{N}}\) 下分解的系数。

**练习 26**（按升幂除法）。设 \(n\in\mathbb{N}\)，\(u,v\in A[x]\)，且 \(v(0)\) 可逆。那么存在唯一一对多项式 \((q,r)\in A[x]\)，满足 \(\deg q\le n\)，使得 \(u = qv + x^{n+1}r\)。编写一个函数，通过类似欧几里得除法算法的方式计算 \(q\) 和 \(r\)。如何使用可用的 Sage 函数以最简单的方式执行此计算？

**最大公因数。** Sage 能够计算域上多项式的 gcd，这得益于 \(K[x]\) 的欧几里得结构；它也能在某些其他环上计算，包括整数环：

```sage
sage: S.<x> = ZZ[]; p = 2*(x^10-1)*(x^8-1)
sage: p.gcd(p.derivative())
2*x^2 - 2
```

我们可能更偏好更对称的表达式 `gcd(p,q)`，它产生与 `p.gcd(q)` 相同的结果。不过，它在 Sage 中稍显不自然，因为它不是一种通用机制：`gcd(p,q)` 调用一个在 Sage 源代码中手工定义的双参数函数，该函数又调用 `p.gcd`。只有一些常用方法才有这样的关联函数。

*扩展 gcd，即计算贝祖关系*

\[
g = \gcd(p,q) = ap + bq, \quad p,q,a,b \in K[x]
\]

由 `p.xgcd(q)` 给出：

```sage
sage: R.<x> = QQ[]; p = x^5-1; q = x^3-1
sage: print('the gcd is %s = (%s)*p + (%s)*q' % p.xgcd(q))
the gcd is x - 1 = (-x)*p + (x^3 + 1)*q
```

`xgcd` 方法也适用于 `ZZ['x']` 中的多项式，但要注意：由于 \(\mathbb{Z}[x]\) 不是主理想环，结果一般不是贝祖关系（\(ap+bq\) 可能是 gcd 的整数倍）！

### 7.2.2 理想与商

**\(A[x]\) 的理想。** 多项式环的理想以及这些理想的商，由通过 `ideal` 和 `quo` 方法从多项式环构建的 Sage 对象表示。多项式元组与多项式环的乘积被解释为一个理想：

```sage
sage: R.<x> = QQ[]
sage: J1 = (x^2 - 2*x + 1, 2*x^2 + x - 3)*R; J1
Principal ideal (x - 1) of Univariate Polynomial Ring in x
over Rational Field
```

我们可以乘理想，并将多项式模一个理想进行约化：

```sage
sage: J2 = R.ideal(x^5 + 2)
sage: ((3*x+5)*J1*J2).reduce(x^10)
421/81*x^6 - 502/81*x^5 + 842/81*x - 680/81
```

在这种情况下，约化后的多项式仍是 \(\mathbb{Q}[x]\) 的一个元素。另一种方法是构造关于理想的商，并将元素投影到其上。投影后元素的父结构此时位于商环中。商元素的 `lift` 方法将它们转换回初始环。

```sage
sage: B = R.quo((3*x+5)*J1*J2)  # quo automatically names 'xbar' which is
sage: B(x^10)                   # the generator of B image of x
421/81*xbar^6 - 502/81*xbar^5 + 842/81*xbar - 680/81
sage: B(x^10).lift()
421/81*x^6 - 502/81*x^5 + 842/81*x - 680/81
```

如果 \(K\) 是域，那么环 \(K[x]\) 是主理想环：计算过程中理想由生成元表示，这一切是 §7.1 中运算的代数语言。其主要优点是商环可以很容易地用于新的构造，这里是 \((\mathbb{F}_5[t]/(t^2+3))[x]\) 的构造：

```sage
sage: R.<t> = GF(5)[]; R.quo(t^2+3)['x'].random_element()
(3*tbar + 1)*x^2 + (2*tbar + 3)*x + 3*tbar + 4
```

Sage 也允许像在 \(\mathbb{Z}[x]\) 中那样构造非主理想，此时可用运算受到限制——但域上的多元多项式除外，这是第 9 章的主题。

**练习 27。** 我们定义序列 \((u_n)_{n\in\mathbb{N}}\)，初始条件为 \(0 \le n < 1000\) 时 \(u_n = n + 7\)，以及线性递推关系

\[
u_{n+1000} = 23u_{n+729} - 5u_{n+2} + 12u_{n+1} + 7u_n \quad (n \ge 0).
\]

计算 \(u_{10^{10000}}\) 的最后五位数字。*提示：* 我们可以查看 §3.2.4 中的算法。然而，当递推阶数很大时，该算法代价过高。引入一个巧妙的多项式环商来避免这个问题。

