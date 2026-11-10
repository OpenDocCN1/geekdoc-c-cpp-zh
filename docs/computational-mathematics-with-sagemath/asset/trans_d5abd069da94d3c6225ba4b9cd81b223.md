

一个*常微分方程*（ODE）是涉及单个变量的（未知）函数以及该函数的一个或多个导数（无论阶次是否连续）的方程。

在方程 $y'(x)+x·y(x)=sin(x)$ 中，未知函数 $y$ 称为*因变量*，变量 $x$（$y$ 相对于其变化）称为*自变量*。

一个*偏微分方程*（简称 PDE）涉及多个自变量以及因变量关于这些自变量的偏导数。

除非另有说明，本章中我们将考虑实变量函数。

## 10.1.2 一阶常微分方程

**基本命令。** 我们想要解一个一阶常微分方程：

$$F(x,y(x),y'(x))=0.$$

我们首先定义一个变量 $x$ 和一个依赖于该变量的函数 $y$：

```sage
x = var('x')
y = function('y')(x)
```

然后：

```sage
desolve(equation, variable, ics = ..., ivar = ...,
        show_method = ..., contrib_ode = ...)
```

其中：

- `equation` 是微分方程。等号用 `==` 表示，例如，方程 $y' = 2y + x$ 写作 `diff(y,x) == 2*y+x`；
- `variable` 是因变量，即 $y' = 2y + x$ 中的 $y$；
- `ics` 是可选的，表示初值条件。对于一阶方程，写成 $[x_0,y_0]$；对于二阶方程，写成 $[x_0,y_0,x_1,y_1]$ 或 $[x_0,y_0,y_0']$；
- `ivar` 是可选的，表示自变量，即 $y' = 2y+x$ 中的 $x$。如果存在多个自变量或参数（如 $y' = ay + bx + c$），则必须指定；
- `show_method` 是一个可选的布尔值，默认设为 `false`。若为 `true`，则 Sage 返回一个对 $[solution, method]^4$，其中 method 是描述用于获得解的方法的字符串。该方法可以是以下之一：`linear`、`separable`、`exact`、`homogeneous`、`bernoulli`、`generalized homogeneous`。
- `contrib_ode` 是一个可选的布尔值，默认设为 `false`。若为 `true`，`desolve` 允许求解 Clairaut、Lagrange、Riccati 及其他一些方程。这可能会花费很长时间，因此默认关闭。

### 可由 Sage 直接求解的一阶方程

本节中我们将研究如何使用 Sage 求解线性、可分离、Bernoulli、Riccati、Lagrange、Clairaut、齐次和恰当方程。

线性方程。这些是如下形式的方程

$$y' + P(x)y = Q(x),$$

其中 $P$ 和 $Q$ 在给定区间上是连续函数。

示例：$y' + 3y = e^x$。

```sage
x = var('x'); y = function('y')(x)
```

```sage
desolve(diff(y,x) + 3*y == exp(x), y, show_method=True)
[1/4*(4*_C + e^(4*x))*e^(-3*x), 'linear']
```

可分离方程。这些是如下形式的方程

$$P(x) = y'Q(y),$$

其中 $P$ 和 $Q$ 在给定区间上是连续函数。

示例：$yy' = x$。

```sage
desolve(y*diff(y,x) == x, y, show_method=True)
[1/2*y(x)^2 == 1/2*x^2 + _C, 'separable']
```

注意！有时 Sage 会将可分离方程当作恰当方程求解。示例：$y' = e^{x+y}$。

```sage
desolve(diff(y,x) == exp(x+y), y, show_method=True)
[-(e^(x + y(x)) + 1)*e^(-y(x)) == _C, 'exact']
```

Bernoulli 方程。这些是如下形式的方程

$$y' + P(x)y = Q(x)y^\alpha,$$

其中 $P$ 和 $Q$ 在给定区间上是连续函数，且 $\alpha \notin \{0,1\}$。示例：$y' - y = xy^4$。

```sage
desolve(diff(y,x)-y == x*y^4, y, show_method=True)
[e^x/(-1/3*(3*x - 1)*e^(3*x) + _C)^(1/3), 'bernoulli']
```

齐次方程。这些是如下形式的方程

$$y' = \frac{P(x,y)}{Q(x,y)},$$

其中 $P$ 和 $Q$ 在给定区间上是同次数的齐次函数。

示例：$x^2y' = y^2 + xy + x^2$。

```sage
desolve(x^2*diff(y,x) == y^2+x*y+x^2, y, show_method=True)
[_C*x == e^(arctan(y(x)/x)), 'homogeneous']
```

解没有显式给出。我们将在后文中看到在某些情况下如何处理这些方程。

**恰当方程。** 这些是如下形式的方程

$$\frac{\partial f}{\partial x}\,dx + \frac{\partial f}{\partial y}\,dy,$$

其中 $f$ 是二元可微函数。

示例：$y' = \frac{\cos(y)-2x}{y+x\sin(y)}$，其中 $f=x^2-x\cos y+y^2/2$。

```text
sage: desolve(diff(y,x) == (cos(y)-2*x)/(y+x*sin(y)), y,
....:         show_method=True)
[x^2 - x*cos(y) + 1/2*y(x)^2 == _C, 'exact']
```

同样，解没有显式给出。

**Riccati 方程。** 这些是如下形式的方程

$$y' = P(x)y^2 + Q(x)y + R(x),$$

其中 $P$、$Q$ 和 $R$ 在给定区间上是连续函数。

示例：$y' = xy^2 + \frac{1}{x}y - \frac{1}{x^2}$。

在这种情况下，我们设置 `contrib_ode` 为 `True`，以使 Sage 使用更复杂的方法。

```text
sage: desolve(diff(y,x) == x*y^2+y/x-1/x^2, y,
....:         contrib_ode=True, show_method=True)[1]
'riccati'
```

**Lagrange 方程和 Clairaut 方程。** 当方程为 $y = xP(y') + Q(y')$ 的形式时，其中 $P$ 和 $Q$ 在给定区间上为 $C^1$，这就是一个 Lagrange 方程。当 $P$ 为恒等函数时，它是 Clairaut 方程。示例：$y = xy' - y'^2$。

```text
sage: desolve(y == x*diff(y,x)-diff(y,x)^2, y,
....:         contrib_ode=True, show_method=True)
[(y(x) == -_C^2 + _C*x, y(x) == 1/4*x^2), 'clairaut']
```

**线性方程。** 让我们求解 $y' + 2y = x^2 - 2x + 3$：

```text
sage: x = var('x'); y = function('y')(x)
```

```text
sage: DE = diff(y,x)+2*y == x**2-2*x+3
sage: desolve(DE, y)
1/4*((2*x^2 - 2*x + 1)*e^(-2*x) - 2*(2*x - 1)*e^(-2*x) + 4*_C
+ 6*e^(-2*x))*e^(2*x)
```

我们可以用 `expand` 重新整理输出：

```sage
sage: desolve(DE, y).expand()
1/2*x^2 + _C*e^(-2*x) - 3/2*x + 9/4
```

因此使用 `desolve(...).expand()` 的形式很方便。让我们检查使用了哪种方法：

```sage
sage: desolve(DE, y, show_method=True)[1]
'linear'
```

让我们添加一个初值条件，例如 y(0) = 1：

```sage
sage: desolve(DE, y, ics=[0,1]).expand()
1/2*x^2 - 3/2*x - 5/4*e^(-2*x) + 9/4
```

### 可分离方程

让我们求解 y' log(y) = y sin(x)：

```sage
sage: x = var('x'); y = function('y')(x)
sage: desolve(diff(y,x)*log(y) == y*sin(x), y, show_method=True)
[1/2*log(y(x))^2 == _C - cos(x), 'separable']
```

Sage 同意我们的看法：这是一个可分离方程。
我们应该将解赋值，以便之后使用：

```sage
sage: ed = desolve(diff(y,x)*log(y) == y*sin(x), y); ed
1/2*log(y(x))^2 == _C - cos(x)
```

这里，y(x) 没有显式给出：1/2 log²(y(x)) = _C − cos(x)。
我们可以使用 `solve` 显式求出 y(x)。请注意，ed 是一个以 y 为变量的方程：

```sage
sage: solve(ed, y)
[[y(x) == e^(-sqrt(2*_C - 2*cos(x))), y(x) == e^(sqrt(2*_C - 2*cos(x)))]]
```

我们应当注意，即使 Sage 没有警告我们，sqrt(2*_C - 2*cos(x)) 也可能引起一些问题。因此我们将假设 _C ≥ 1。
要绘制解的图像，我们需要它们的右端表达式。例如，为了得到 _C = 5 时第一个解的右端表达式，我们可以输入：

```sage
sage: solve(ed, y)[0].substitute(_C==5).rhs()
Traceback (most recent call last):
...
NameError: name '_C' is not defined
```

`_C` 没有被定义，只是由 Sage 引入的。我们可以通过 `variables()` 命令获取它，该命令给出变量列表：

```sage
sage: ed.variables()
(_C, x)
```

只有 `_C` 和 `x` 是变量，`y` 已被定义为变量 `x` 的函数。

```sage
sage: c = ed.variables()[0]
sage: solve(ed, y)[0].substitute(c == 5).rhs()
e^(-sqrt(-2*cos(x) + 10))
```

```sage
....:      f = solve(ed,y)[j].substitute(c==2+0.25*k).rhs()
....:      P += plot(f, x, -3, 3)
sage: P
```

但是比例尺差别太大，无法同时看到两组曲线：

![](img/99840d73c45ee58b635c4eedc727fd9a_234_0.png)

**练习 39**（可分离方程）。求下列可分离方程在 $\mathbb{R}$ 中的解：

1. $(E_1):\quad \dfrac{w y'}{\sqrt{1+y^2}} = \sin(x);$
2. $(E_2):\quad y' = \dfrac{\sin(x)}{\cos(y)}.$

**齐次方程。** 我们要求解微分方程 $x y' = y + \sqrt{y^2+x^2}$，它是齐次的，因为

$$\frac{dy}{dx}=\frac{y+\sqrt{y^2+x^2}}{x}=\frac{N(y,x)}{M(y,x)},$$

且 $N(ky,kx)=kN(y,x)$，$M(ky,kx)=kM(y,x)$。

对于所有实数 $x$，我们只需引入变量替换 $y(x)=x\cdot u(x)$ 即可得到一个可分离方程。

```sage
sage: u = function('u')(x)
sage: y = x*u
sage: DE = x*diff(y,x) == y + sqrt(x**2 + y**2)
```

让我们在初始微分方程中进行变量替换。由于该方程在 0 处无定义，我们首先在 $]0,+\infty[$ 上求解，然后在 $]-\infty,0[$ 上求解。

```sage
sage: assume(x>0)
sage: desolve(DE, u)
x == -_C*e^arcsinh(u(x))
```

我们没有显式得到 $u$。因此我们使用 Maxima 的 `ev` 命令（即 `evaluate`），并设置 `logarc=True`，以便将反双曲函数用作对数；然后 $u$ 将通过 `solve` 命令表示出来：

