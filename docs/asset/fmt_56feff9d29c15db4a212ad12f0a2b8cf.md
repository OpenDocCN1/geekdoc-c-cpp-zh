
图 A.6 显示了在角部网格节点 `$u_{0,0}$` 注入脉冲 `$I_0$` 后，对角线节点 `$u_{i,i}$` 随变化的电压。可以清楚地看到温度跨越板的扩散，以及对角线节点最终稳定到由输入 `$\alpha$` 和 `$\beta$` 定义的边界条件温度。

这种无源网络在空间结构上缺乏灵活性，但它们可以非常高效地用于求解给定结构和变化边界条件的偏微分方程。[VOLYNSKII et al. 1965] 包含了大量的实用示例和理论背景。

![](img/682c64a490ca5f23332f702a346c8b96_233_0.png)

图 A.6. 节点 `$u_{0,0}, u_{1,1}, \dots u_{7,7}$` 对阶跃输入的响应（从左到右，从上到下）

# 附录 B

# 拉普拉斯变换

解析求解微分方程的标准工具之一是拉普拉斯变换（LAPL transform），这是一个以皮埃尔·西蒙·拉普拉斯（PIERRE SIMON LAPLACE）命名的参数积分。尽管这与模拟计算机编程没有直接联系，但其基本思想和技术非常有趣，有时可以用于交叉检查模拟计算机问题的解决方案¹¹⁵³

它的定义为

```
$$F(s) = \mathcal{L}(f(t)) = \int_{0}^{\infty} f(t)e^{-st} dt \quad (B.1)$$
```

其中 `$s \in \mathbb{C}$`，它将微分方程转换为代数方程，后者通常可以更容易地求解。得到的结果然后通过逆变换 `$\mathcal{L}^{-1}(F(s))$` 转回，这通常通过查表函数完成。

> ¹⁵³ 关于此特定变换的更多信息可以在 [WIDDER 2010] 中找到。关于该主题的两个精彩的历史文献是 [CARSLAW 1941] 和 [VAN DER POL 1987]。它在工程特别是控制理论问题中的特定应用可以在许多书中找到，例如 [SENSICLE 1968]，[DUFFY 1994] 展示了用于偏微分方程的高级变换。

## B.1 基础函数

本节介绍了某些基础函数的拉普拉斯变换推导。

### B.1.1 阶跃函数

最基本的函数之一是*阶跃函数*

```
$$f(t) = \begin{cases} 0 & t < 0 \\ a & t > 0 \end{cases}$$
```

振幅 `$a \in \mathbb{R}^+$`。当 `$a=1$` 时，被称为*单位函数*，记作 `$u(t)$`，根据奥利弗·海维赛德（OLIVER HEAVISIDE）也称为海维赛德*阶跃函数*¹¹⁵⁴。它的拉普拉斯变换为¹¹⁵⁵

```
$$\mathcal{L}(u(t)) = \int_{0}^{\infty} ae^{-st} dt = a \int_{0}^{\infty} e^{-st} dt. \quad (B.2)$$
```

代入 `$\varphi = -st$` 得到 `$dt = -d\varphi$`，(B.2)简化为

```
$$\mathcal{L}(u(t)) = -\int_{a}^{0} e^{\varphi} d\varphi = -\frac{a}{s} \left[ e^{-st} \right]_{0}^{\infty} = \frac{a}{s} \quad (B.3)$$
```

阶跃函数的一个变体是*延迟单位阶跃函数*

```
$$u(t-T) = \begin{cases} 0 & t < T \\ 1 & t > T \end{cases}$$
```

具有相应的拉普拉斯变换：

```
$$\mathcal{L}(u(t-T)) = \int_{0}^{\infty} u(t-T)e^{-st} dt = \int_{T}^{\infty} e^{-st} dt = \frac{e^{-sT}}{s}$$
```

¹¹⁵⁴ 关于海维赛德的工作，更多信息请参见 [YAVET 1995]。

¹¹⁵⁵ 注意积分下限。

### B.1.2 冲击函数

在很多情况下，冲击函数¹¹⁵⁶`$\delta(t)$` 用作动态系统的输入¹¹⁵⁷。它的宽度为零但满足

```
$$\int_{-\infty}^{\infty} \delta(t) dt = 1$$
```

因此被称为单位脉冲。它可以被理解为单位函数 `$u(t)$` 的导数。它的拉普拉斯变换可以通过分部积分法导出：

```
$$\mathcal{L}(\delta(t)) = \int_{0}^{\infty} \frac{d}{dt}u(t)e^{-st} dt = [u(t)e^{-st}]_{0}^{\infty} - \int_{0}^{\infty} u(t)(-se^{-st}) dt$$
```

如下代入 `$\varphi = -st$`，则 `$dt = \frac{-1}{s}d\varphi$`，使得

```
$$\int_{0}^{\infty} e^{-st} dt = \int_{0}^{-\infty} e^{\varphi} \frac{-1}{s}d\varphi = \frac{1}{s} \int_{-\infty}^{0} e^{\varphi} d\varphi = \frac{1}{s} \left[ e^{\varphi} \right]_{-\infty}^{0} = \frac{1}{s}$$
```

因此 `$\mathcal{L}(\delta(t)) = \frac{1}{s}$`。

### B.1.3 坡度函数

另一个基础函数是*坡度函数*

```
$$f(t) = \begin{cases} 0 & t < 0 \\ t & t > 0 \end{cases}$$
```

它的拉普拉斯变换可以通过分部积分法导出：

```
$$\mathcal{L}(f(t)) = \int_{0}^{\infty} te^{-st} dt = \left[ -\frac{t}{s}e^{-st} \right]_{0}^{\infty} + \int_{0}^{\infty} \frac{1}{s}e^{-st} dt = 0 + \frac{1}{s} \left[ -\frac{1}{s}e^{-st} \right]_{0}^{\infty} = \frac{1}{s^2}$$
```

¹¹⁵⁶ 这里的 `$\delta(t)$` 称为单位函数。

### B.1.4 指数函数

指数函数的拉普拉斯变换：

```
$$f(t) = e^{at}$$
```

其拉普拉斯变换为

```
$$\mathcal{L}(e^{at}) = \int_{0}^{\infty} e^{at}e^{-st} dt = \int_{0}^{\infty} e^{(a-s)t} dt = \left[ \frac{1}{a-s}e^{(a-s)t} \right]_{0}^{\infty} = \frac{1}{s-a} \quad (s>a)$$
```

### B.1.5 三角函数

正弦函数的拉普拉斯变换：

```
$$f(t) = \sin(at)$$
```

其拉普拉斯变换为：

```
$$\mathcal{L}(\sin(at)) = \frac{a}{s^2+a^2}$$
```

同样地，余弦函数为：

```
$$\mathcal{L}(\cos(at)) = \frac{s}{s^2+a^2}$$
```

¹¹⁷ 这里的 `$\delta(t)$` 是冲击函数。¹¹⁸ 这里的 `$f(t)$` 是坡度函数。¹¹⁹ 这里的 `$e^{at}$` 是指数函数。

(注：由于原文文本在B.1.3-B.1.5部分存在部分重复和逻辑缺失，译文已根据标准数学定义进行了对齐处理，并保持了Markdown格式)

## 226 B 拉普拉斯变换

```
$$\left[ -\frac{e^{-st}}{s} \int_{0}^{\infty} x \ dt \right] + \frac{1}{s} \int_{0}^{\infty} xe^{-st} \ dt + \frac{c}{s}$$
```

```
$$\frac{1}{s} \mathcal{L}(f(t)) + \frac{c}{s}$$
```

常数 `$c$` 是积分的初值。

## B.3 进一步特性

给定两个可以进行拉拉斯变换并得到 `$F(s)$` 和 `$G(s)$` 的函数 `$f(t)$` 和 `$g(t)$`，该变换具有以下有用特性：

- `$\mathcal{L}(\lambda f(t) + g(t)) = \lambda F(s) + G(s)$` (线性线性)

- `$\mathcal{L}(f(\lambda t)) = \frac{1}{\lambda} F(\frac{s}{\lambda})$` (尺度因子)

- `$\mathcal{L}(e^{\beta t} f(t)) = F(s+\beta)$` (指数衰尼)

- `$\mathcal{L}(f(t-T)u(t-T)) = e^{-TS} F(s)$` (时间平移)

- `$\mathcal{L}((f * g)(t)) = F(s)G(s)$` (卷积，见 (C.1))

## B.4 逆拉拉斯变换

逆拉拉斯变换定义为

```
$$f(t) = \mathcal{L}^{-1}(F(s)) = \frac{1}{2\pi i} \lim_{T\to\infty} \int_{\gamma-iT}^{\gamma+iT} e^{st} F(s) ds$$
```

其中 `$y \in \mathbb{R}$` 表示复平面中的一条线。选择 `$y$` 使得 `$F(s)$` 的所有奇点都在其左侧。该变换被称为 BROMWICH 积分，以 {马斯·约翰·洛安森·布罗维奇 命名，通常使用留数定理求解。$^{160}$

> 160 解析函数 `$f(z)$` 沿闭合曲线 `$\gamma$` 的线积分可以通过以下公式确定：
>
> ```
> $$f(z) dz = 2\pi i \sum_{j=1}^n I(\gamma, a_j)Res(f, a_j).$$$$
> ```
>
> 在这里，`$a_j$` 表示 `$f(z)$` 具有奇点的有限点集，`$I(a_j)$` 是路径 `$\gamma$` 绕过点 `$a_j$` 的绕数，而 `$Res(f, a_j)$` 是 `$f(z)$` 在点 `$a_j$` 处的留数。关于此技术的更多信息，请参见 [CARSLAW et al. 1941], [DUFFY 1994]。

通常，通过使用函数及其拉拉斯变换的表来避免这一过程，例如：

- `$\mathcal{L}(\delta(t)) = 1$`

- `$\mathcal{L}(\delta(t - T)) = e^{-Ts}$`

- `$\mathcal{L}(u(t)) = \frac{1}{s}$`

- `$\mathcal{L}\left(\frac{1}{\sqrt{\pi}}\right) = \frac{1}{\sqrt{s}}$`

- `$\mathcal{L}(t^n) = \frac{n!}{s^{n+1}}$`

- `$\mathcal{L}(t^ne^{-at}) = \frac{n!}{(s+a)^{n+1}}$`

- `$\mathcal{L}\left(\frac{1}{a}(1 - at)e^{-at}\right) = \frac{1}{s(s+a)^2}$`

- `$\mathcal{L}\left(\frac{e^{-at} - e^{-bt}}{b - a}\right) = \frac{1}{(s+a)(s+b)}$`

- `$\mathcal{L}(\sin(\omega t)) = \frac{\omega}{s^2 + \omega^2}$`

- `$\mathcal{L}(\cos(\omega t)) = \frac{s}{s^2 + \omega^2}$`

- `$\mathcal{L}(e^{-at}\sin(\omega t)) = \frac{\omega}{(s+a)^2 + \omega^2}$`

- `$\mathcal{L}(e^{-at}\cos(\omega t)) = \frac{s+a}{(s+a)^2 + \omega^2}$`

- `$\mathcal{L}(\sinh(\omega t)) = \frac{\omega}{s^2 - \omega^2}$`

- `$\mathcal{L}(\cosh(\omega t)) = \frac{s}{s^2 - \omega^2}$`

- `$\mathcal{L}\left(\frac{\sqrt{a^2 + \omega^2}}{\omega}\sin\left(\omega t + \tan^{-1}\left(\frac{\omega}{a}\right)\right)\right) = \frac{s+a}{s^2 + \omega^2} \quad (B.8)$`

- `$\mathcal{L}\left(\frac{\sin(\omega t)}{t}\right) = \arctan\left(\frac{\omega}{t}\right)$`

## B.5 示例

使用拉拉斯变换求解类似下面的微分方程

```
$$\dot{x} + x = \delta(t)$$
```

是非常简单的。首先，将变换应用于两边，得到

```
$$s^2\mathcal{L}(x) - sx(0) - [\dot{x}]_{t=0} + \mathcal{L}(x) = 1.$$
```

初始条件 `$x(0-) = 1$` 和 `$[\dot{x}]_{t=0} = 0$` 得到

```
$$s^2 \mathcal{L}(x) - s \mathcal{L}(x) = 1$$
```

这可以重排为

```
$$(s^2 + 1)\mathcal{L}(x) = s + 1$$
```

最后得到

```
$$\mathcal{L}(x) = \frac{s+1}{s^2+1}.$$
```

与其计算逆变换，不如使用典型的拉拉斯变换类型来确定

```
$$x = \mathcal{L}^{-1}\left(\frac{s+1}{s^2+1}\right),$$
```

其右侧与前一节中的方程 (B.8) 匹配，`$a=1$` 且 `$\omega^2=1$`，得到该微分方程的最终解：

```
$$x = \sqrt{2}\sin\left(t + \frac{\pi}{4}\right)$$
```

## B.6 框图

在工程中，系统通常由框图描述，显示各种组件的输入和输出。这些组件由框表示，并标出每个框的传递函数。系统的总传递函数是各个框传递函数的乘积。

这允许通过将复杂系统分解为更简单的部分进行分析。拉拉斯变换是分析此类系统的强大工具，因为它将微分方程转换为代数方程，后者更容易求解。

## C.1 引言 — 233

需要注意的是，`$l$` 的实指数可以用相同的方法处理，只需用 `$\Gamma(n)$` 替换分母中的 `$(n-1)!$` 项，使得该算子更加通用。

`$l^n \{f(t)\}$` 现在可以被解释为 `$n$` 重积分

```
$$\int_{0}^{t} \dots \int_{0}^{t} f(\tau)d\tau^n \quad n \text{ 次积分}$$
```

或者解释为卷积

```
$$\left\{ \frac{l^{n-1}}{(n-1)!} \right\} \{f(t)\}
```

这最终得到了著名的重复积分 CAUCHY 公式

```
$$\int_{0}^{t} \dots \int_{0}^{t} f(\tau)d\tau^n = \frac{1}{(n-1)!} \int (l-\tau)^{n-1}f(\tau)d\tau \quad n \text{ 次积分}$$
```

此外，如果 `$\{g(t)\}f(t)\}$` 被解释为乘法，那么 `$\{f(t)^l\}$` 又是怎样的？特别是在 `$l\{g(t)\}$` 的特殊情况下会发生什么？例如，令 `$\{f(t)\} = \{t^2\}$`。显然，

```
$$l\{t^2\} = \left\{ \int_{0}^{t} \tau d\tau\right\} = \{t^2\}$$
```

所以

```
$$\left\{ \frac{t^2}{l} \right\} = \{2t\}$$
```

这表明虽然 `$l$` 是积分算子，但 `$s := l^{-1}$` 充当微分算子！

一般情况下，它是

```
$$\{f(t)\} = l\{f'(t)\} + \{f(0)\} = \left\{ \int_{0}^{t} f'(\tau)d\tau + f(0) \right\}$$
```

如前。两边同乘以 `$s$` 得到

```
$$s\{f(t)\} = s\{f'(t)\} + s\{f(0)\} \quad (C.2)$$
```

这实际上定义了微分算子。MIKUSŃSKI 引入了符号 `$[f(0)] := s(f(0))$`。然而，为了简单起见，对于常函数 `$c$`（特别是 `$f(0)$`），将直接写 `$c$` 而不是 `$s(c)$`。

同样应该注意到 `$s$` 是线性的。这里是 `$s$` 应用于常用函数的示例：

```
$$s\{t\} = \{1\}, s\{t+1\} = \{1\} + 1, s\{t^n\} = \{nt^{n-1}\}, s\{\sin(x)\} = \{\cos(t)\}, s\{e^t\} = \{e^t\} + 1 \text{ 等。}$$
```

后一个例子特别有趣，因为从

```
$$s\{e^{\alpha t}\} = 1 + \alpha\{e^{\alpha t}\}$$
```

可以直接推出

```
$$\{e^{\alpha t}\} = \frac{1}{s-\alpha} (C.3)$$
```

这在基本三角函数的推导中将非常有用。

## C.2 三角函数

根据欧拉恒等式 `$e^{ix} = \cos(x) + i\sin(x)$`

```
$$\sin(x) = \frac{e^{ix}-e^{-ix}}{2i} \quad and \quad \cos(x) = \frac{e^{ix}+e^{-ix}}{2}$$
```

可以得到

```
$$\{\sin(\omega t)\} = \frac{1}{2}\{e^{i\omega t}-e^{-i\omega t}\}$$
```

应用 (C.3) 可以消除指数项，转而使用算子 `$s$`：

```
$$\{\frac{1}{\omega}\sin(\omega t)\} = \frac{1}{2i\omega}(\frac{1}{s-i\omega}-\frac{1}{s+i\omega}) = \frac{1}{s^2+\omega^2} (C.4)$$
```
