
$a^p a^q = a^{p+q}$,

$\frac{a^p}{a^q} = a^{p-q}$,

$(a^p)^q = a^{pq}$,

$a^{-p} = \frac{1}{a^p}$,

$a^0 = 1$（如果 $a \neq 0$），

$(a^m)^{1/n} = a^{m/n}$ ($m$ 和 $n$ 为正整数),

$(\frac{a}{b})^{1/n} = \frac{a^{1/n}}{b^{1/n}}$ ($n$ 为正整数),

$(ab)^q = a^q b^q$.

### H.1.2 对数

$x$ 以底 $a$ 的对数 $p$ 的定义为：

$log_a x = p$ 使得 $a^p = x$ ($a$ 不为0 或 1)。

## 附录 H

考虑到这些，定义了以下表达式：

$\log_a xy = \log_a x + \log_a y,$

$\log_a \frac{x}{y} = \log_a x - \log_a y,$

$\log_a x' = y \log_a x.$

对数中常用的底通常被限于 2、10 和 $e (= 2.7182818\dots,$，对数的自然底）。为了换底，我们可以使用：

$\log_a x = \frac{\log_b x}{\log_b a}$

或者

$\log_a x = C(a,b) \log_b x,$ 其中 $C(a,b) = \frac{1}{\log_b a}$。

现在我们可以找到转换三个常用底的常数 $C(a,b)$ 的不同值：

$C(2, 10) = 3.32198$ $C(2, e) = 1.442695,$

$C(e, 10) = 2.302585$ $C(e, 2) = 0.693147,$

$C(10, 2) = 0.301029$ $C(10, e) = 0.434294.$

例如：

$\log_{10} x = C(10, 2) \log_2 x = 0.301029 \log_2 x.$

### H.1.3 和与级数表达式

级数中和的符号使用希腊大字母 $sigma$ $(\Sigma)$ 以紧凑的形式表示项的相加（可能是无限的）：

$\sum_{k=1}^n k = 1 + 2 + 3 + \dots + n.$

该等式的左侧用英语读作“从 $k$ 等于 1 到 $n$ 的 $k$ 之和”。在数学术语中，$k$ 是*求和索引*，右侧是*展开式*。这类表达式通常会更复杂，但会有一定数量的项（例如，如果我们从1开始，则该数量等于 $n$，这个数字可能是无限的），并且求和索引在展开式的每一项中都增加 1。例如，以下表达式中 $k$ 作为 $A$ 的上标（表示 $A$ 有多个不同的值），并作为 $\cos()$ 函数内部的乘数：

$$\sum_{k=1}^{n} \cos(k\omega) = A_1 \cos(\omega) + A_2 \cos(2\omega) + \cdots + A_n \cos(n\omega).$$

### H.1.4 乘积表达式

与和类似，我们有一个在乘积中组合了几个因子的表达式，使用大字母 pi ($\Pi$) 并遵循 H.1.3 节中概述的原则：

$$\prod_{k=1}^{n} k = 1 \times 2 \times 3 \times \cdots \times n$$

### H.1.5 多项式

推广上述原理，我们将仅涉及 $x$ 的未知多项式的整数幂的表达式称为多项式。以下是一个关于一个未知数 $x$ 的多项式：

$f(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_2 x^2 + a_1 x^1 + a_0$。

在数学上，$n$ 是多项式的次数，$a_0$ 是常数项。

### H.1.6 函数

函数是一个将一个或多个参数映射到一个值或结果的数学表达式。本质上，给定一个输入，函数产生一个唯一的输出。例如，平凡函数 $f(x) = x$ 将参数映射到其本身，$f(x) = 2x$ 将 $x$ 倍，而 $f(x) = x^2$ 将函数的输出平方。单变量函数的分类取决于其定义中变量的最大指数。第一类是线性的（直线），第二类是二次的。其他高阶函数称为三次、四次等。

### H.1.7 方程

当函数 $f(x)$ 等于 $0$ 时，如 $f(x) = 0$，我们就有一个方程，它可能有一个或多个根。单未知数的多项式方程有一个特别简单的规则：根的个数与次数相同。线性方程有一个根，二次方程有两个根。

$\cos(A \pm B) = \cos(A)\cos(B) \mp \sin(A)\sin(B),$

$\sin 2A = 2 \sin A \cos A,$

$\cos 2A = \cos^2 A - \sin^2 A,$

$\sin^2 A = \frac{1 - \cos 2A}{2},$

$\cos^2 A = \frac{1 + \cos 2A}{2},$

$\cos A \cos B = \frac{\cos(A-B) + \cos(A+B)}{2},$

$\sin A \sin B = \frac{\cos(A-B) - \cos(A+B)}{2},$

$\sin A \cos B = \frac{\sin(A+B) + \sin(A-B)}{2},$

$\sin A \pm \sin B = 2 \sin\left(\frac{A \pm B}{2}\right) \cos\left(\frac{A \mp B}{2}\right),$

$\cos A \pm \cos B = 2 \cos\left(\frac{A+B}{2}\right) \cos\left(\frac{A-B}{2}\right),$

$\cos A - \cos B = -2 \sin\left(\frac{A+B}{2}\right) \sin\left(\frac{A-B}{2}\right).$.

在上述表达式中，$a \pm b = c \pm d$ 表示 $a+b = c-d$ 且 $a-b = c+d$。这些等式中的某些对音频编程非常重要。例如，

$\cos A \cos B = \frac{\cos(A-B) + \cos(A+B)}{2}$

表明如果你对两个不同频率（$A$ 和 $B$）的正弦波进行混合（求和），你将得到这两个频率之和 $(A+B)$ 和差 $(A-B)$ 的分量混合。此外，这两个分量中的每一个幅度将是原始幅度的一半。这被称为*环调制*。

# H.3 微积分

上述代数运算的一个重要进展发现于微积分中。主要的兴趣点在于描述表达式的变化率。微积分最初是为了是为了理解天体的速度和加速度。

![](img/4e80a3f6f432392037615a065cf9d4ba_887_0.png)

# H.3.1 求分

我们寻求对表达式瞬时变化提供数学描述。例如，如果我们有一个表达式 $f(x) = ax^2$，那么曲线如图 H.2 所示。表达式的变化可以通过曲线上某一点的切线来表征。微积分是一种为该切线提供代数表达式的方法，使其关于其发生点成为一个函数。

我们考虑一个点 $x$ 和一个靠近它的点 $x + \partial x$，并在 $f(x)$ 和 $f(x + \partial x)$ 之间连一条线产生一条弦。增长量为 $(f(x + \partial x)-f(x))/\partial x$。随着 $\partial x$ 变小，弦就越接近曲线在 $x$ 处的切线。微积分的意图是考虑表达式 $(f(x+\partial x)-f(x))/\partial x$ 在 $\partial x$ 趋于零时的极限。在我们的例子中，这

```
lim(\partial x\to0)(a(x+\partial x)^2 - ax^2)/\partial x = lim(\partial x\to0)(2ax\partial x + \partial x^2 - ax^2)/\partial x

=2ax
```

因此我们确定了二次形式切线的表达式，被称为该形式的导数。这通常写成 $df(x)/dx$，或者有时无义地写成 $f'(x)$。

通常，多项式 $x^n$ 的导数很容易证明为 $nx^{n-1}$，而和的导数规则为

```
$\frac{d(A+b)}{dx} = \frac{dA}{dx} + \frac{dB}{dx}$
```

和

```
$\frac{d(A-b)}{dx} = \frac{dA}{dx} - \frac{dB}{dx}$
```

积的等效导数规则为

```
$\frac{d(Ab)}{dx} = B\frac{dA}{dx} + A\frac{dB}{dx}$
```

和

```
$\frac{d(A/B)}{dx} = \frac{B\frac{dA}{dx} - A\frac{dB}{dx}}{B^2}$
```

这些允许我们计算任何多项式的导数。

# 其他函数

其他函数的导数也可以计算。证明主要在本文之后，但我们将考虑其中一个，$d\sin(x)/dx$。其定义为

```
$limit(\delta x \to 0)(\sin(x+\delta x) -\sin(x))/\delta x$.
```

使用 $\sin(A+B)$ 的公式，我们看到这等同于

```
$limit(\delta x \to 0)(\sin(x)+\cos(\delta x))/\delta x$.
```

对于较小的 $\delta x$ 值，$\cos(\delta x)$ 近似于 $1$，而 $\sin(\delta x)$ 近似于 $\delta x$，因此我们可以简化为

```
$limit(\delta x \to 0)(\sin(x)\cos(\delta x)-\sin(x)) = \sin(x)\cos(x)$.
```

其他结果通过类似的方法证明。

```
$d\sin(x)/dx = \cos(x)$ （以弧度为单位），
```

```
$d\tan(x)/dx = \tan^2(x) + 1$，
```

```
$d\log(x)/dx = 1/x$ （使用自然对数，底为 $e$），
```

```
$df(g(x))/dx = f'(g(x)) \cdot g'(x)$。（注：根据上下文修正）```
# H.3.2 反积分

求分的相反可以通过两种方式看到。第一是反积分；即回答“什么函数的导是 $f(x)$？”在简单多项式中，可以通过 3.1 节的逆规则很容易实现：

```
antideriv$(x^n) = x^{n+1}/(n+1)$ （$n \neq -1$),
```

```
antideriv$(1/x) = \log(x)$,
```

```
antideriv$(a^x) = a^x\log(a)$。
```
