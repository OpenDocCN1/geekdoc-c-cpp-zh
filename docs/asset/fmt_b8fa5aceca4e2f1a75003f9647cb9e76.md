
$E=\frac{1}{2}mx^2+\frac{1}{2}kx^2+\frac{1}{4}\beta x^4=\frac{1}{2}mb^2=\frac{1}{2}ka^2(1+\frac{\beta}{2}a^2). (4.234e)$

对于闭合或振荡运动，位移为零的时间 (4.234a, b) [速度 (4.234c, d)] 与速度达到最大时刻 (4.235a) 重合：

$x(t_1)=0; \dot{x}(t_1)\leq a; x(t_2)=0; |\dot{x}(t_2)|\leq a. (4.235a)$

参数 $\beta$ (4.234a) 具有长度平方的，**无量纲非线性参数**定义为 (4.236a)：

$\gamma=\frac{\beta}{2}a^2=\frac{2E}{ma^2}\frac{1}{\omega_0\sqrt{1+\gamma}}, (4.236a-d)$

它出现在最大速度 (4.236b) 与最大位移或幅度 (4.236c) 的关系中。该比例 (4.236c) ≡ (4.236d) 对于硬弹簧或软弹簧，非线性的影响会增加或减少 (4.235a)。

## 非稳态、非线性与混沌系统

总能量在速度为零时（例如对于最大位移或幅度 (4.237a) 的周期性运动），轨迹方程 (4.212b) 变为 (4.237c)，对于任意势函数：

$E = \Phi(a); \quad x(0) = 0; \quad t = \int_{0}^{x} \frac{k}{2} \left[Phi(a) - \Phi(\xi) \right]^{-1/2} d\xi, \quad (4.237a-c)$

在原点处 (4.237b)，二次势 (4.215b) 情况下的运动方程 (4.222b) ≡ (4.238)：

$t = \int_{0}^{x} \frac{1}{\beta} \left[ (a^2 - \xi^2) + \frac{\beta}{a^2} (a^4 - \xi^4) \right]^{-1/2} d\xi, \quad (4.238)$

可以转化为无量纲形式 (4.239)：

$\omega_0 t = \int_{0}^{a} a^2 - \xi^2 + \gamma \left( a^2 - \frac{\xi^4}{a^2} \right)^{-1/2} d\xi, \quad (4.239)$

其中仅涉及自然频率 (4.221a) 和非线性参数 (4.236a)。由于 (4.239) 被积函数中的根号是一个二次多项式，该积分可以通过 [4.4.9] 作为雅可比椭函数（I.399）。

### 4.4.9 椭正弦的精确解

变量 $\xi$ 和模 $q$ 的雅可比椭正弦定义为 (I.39.114c) ≡ (4.240a, b)：

$z = sn(\xi;q); \quad \zeta = \arg sn(z;q) = \int_{0}^{\zeta} (1-y^2) (1-q^2)^{-1/2} dy. \quad (4.240a, b)$

将 (4.239) 改写为形式 (4.241)：

$\omega_0 t = \int_{0}^{a} a^2 (1+\gamma) - \gamma \frac{\xi^4}{a^2})^{-1/2} d\xi, \quad (4.241)$

建议变量变量 (4.242a) 导致 (4.242b)：

$y = \frac{\xi}{a}; \quad \omega_0 t = \int_{0}^{a} |1+\gamma y - y^2 - \gamma y^4|^{-1/2} dy. \quad (4.242a, b)$

积分 (4.242b) 可以重写为形式：

$\omega_t\sqrt{1+\gamma} = \int_{0}^{x/a} \frac{y^2}{1+\gamma} \frac{\gamma}{1+\gamma} dy = \int_{0}^{x/a} (1-y^2) \left(1+\frac{\gamma}{1+\gamma} y^2\right)^{-1/2} dy, \quad (4.243)$

这与反椭函数 (4.240a, b) 一致 (4.244a-c)：

$z=\frac{x}{a} \quad \zeta = \omega_t\sqrt{1+\gamma}\sqrt{1+\frac{\beta a^2}{2}}, \quad q^2=-\frac{\gamma}{1+\gamma}-\frac{\beta a^2}{2}, \quad (4.244a)$

已经证明具有二次势 (4.215b) 的**非线性振子** (4.215a) 的**轨迹**通过椭正弦函数 (10) 指定：

$x=asn(\omega_t\sqrt{1+\gamma}), \quad (4.245)$

涉及：

- (i) 幅度 (4.220b)；
- (ii) 自然频率 (4.221c)；
- (iii) 非线性参数 (4.236a)，它指定了模 (4.244c)。

在 (4.245) 中，对于 $\gamma>0$（硬弹簧），模为实；对于 $\gamma<0$（软弹簧），非谐振子的精确频率不同于谐振子的自然频率 (4.4.11)，它是从反椭正弦序列 [4.4.10] 得到的，这导致了第二类切比夫多项式 [4.4.12]，精确地指定了时间形式的谐振子轨迹。

### 4.4.10 反椭正弦的正正弦序列

变量的变化 (4.246a, b) 简化了椭积分 (4.240b; 4.244-c)：

$\sin\phi=z=\frac{x}{a}; \quad \sin\psi=\frac{\xi}{a}; \quad \omega_t\sqrt{1+\gamma} = \int_{0}^{\sin\phi} \left|1-q^2\sin^2\psi\right|^{-1/2} d\psi, \quad (4.244a)$

$x=asn(\dots;q)$。椭积分 (4.246b) 可以使用两种展开精确求值：

- (i) 首先，二项式展开 (5.37a-c) (4.247a, b)，对于积分 (4.246b)：

$q^2 = \left| \frac{\gamma}{1+\gamma} \right| - \frac{\beta a^2}{2+\beta a^2} < 1; \quad \left|1-q^2\sin^2\psi\right|^{-1/2} = 1+\sum_{n=0}^{\infty} a_nq^{2n}\sin^{2n}\psi, \quad (4.247a, b)$

其中系数 (5.6a, b) = (4.248a, b)：

$n \ge 1: \quad a_n = (-)^{\frac{-1/2}{n}} \frac{(-)^{n}}{n!} - \dots - (-)^{\frac{-1}{2}} \frac{n+1}{2}, \quad (4.248a, b) = \frac{2^{-n}}{n!} - \dots \frac{(2n-1)!!}{(2n)!!} = \frac{(2n-1)!!}{(2n)!}$

对于第一值 (5.57b)：

- (ii) 正弦的偶次幂 (4.247b) 可以展开为倍角余弦的有限和 (5.7a)：

$\sin^2\psi = 2^{-1}\left[ \frac{2n}{n} \right] + 2\sum_{m=0}^{n-1} (-1)^{n-m} \left[ \frac{2n}{m} \right] \cos[2(n-m)\psi], \quad (4.249)$

将 (4.249) 代入 (4.247b) 得到 (4.250b)：

$|1+\gamma; |1-q^2\sin^2\psi|^{-1/2} = 1+\sum_{n=1}^{\infty} \left( \frac{q}{2} \right)^n \frac{(2n-1)!!}{(2n)!!} \times \left[ \frac{(2n)!!}{n!} + 2\sum_{m=1}^{n-1} (-1)^{n-m} \left[ \frac{2n}{m} \right] \cos[2(n-m)\psi]\right], \quad (4.250a, b)$

如果满足条件 (4.247a; 4.244c) = (4.250a)，代入 (4.246b) 允许立即积分指定变量 $\phi$ 和模 $q$ 的反椭正弦 (4.251) 为偶倍正弦序列：

$\sin\phi; q = \Lambda + \sum_{n=1}^{\infty} \left( \frac{q}{2} \right)^n \frac{(2n-1)!!}{(2n)!!} \sum_{m=1}^{n-1} (-1)^{n-m} \left[ \frac{2n}{m} \right] \sin[2(n-m)\phi]\frac{1}{n-m}, \quad (4.251)$

$A(q) = 1+\sum_{n=1}^{\infty} \left( \frac{q}{2} \right)^n \frac{(2n-1)!!}{(n)!} = 1+\sum_{n=1}^{\infty} \left[ \frac{(2n)!!}{(n)!} \right]^2 \frac{q^{2n}}{2^{2n}}, \quad (4.252a, b)$

涉及非谐因子 (4.252a) = (4.252b)。在 (4.252a) 到 (4.252b) 的通过使用了：

$\frac{(2n-1)!!}{(2n)!!} = \frac{(2n)!}{[(2n)!]^2} = \frac{(2n)!}{(n!)^2 2^{2n}}, \quad (4.252c)$

现在 [4.4.11] 显示，非谐因子 (4.252a) = (4.252b) 将非谐振子的频率与谐振子的频率联系起来。

## 4.4.11 非谐振子与谐振子的频率

使用 (4.253b)，它是 (4.246a) 的反 (4.234a)，对应于谐振子 (4.253a)：

- (i) 位移 (4.220b) 是周期的四分之一；
- (ii) 对于 $\phi$ 的值 (4.253d)：

$\omega_0 t = \sin\left(\frac{\tau}{4}\right) \Rightarrow \phi = \frac{\pi}{2}. \quad (4.253a-d)$

# 不稳定、非线性与混沌系统

幅（4.253b）对应于四分之一周期的位移（4.253c）或角度（4.253d），因此级数（4.254a）的所有项在 $x = a$ 时除了第一项外全部消失：

```
$\omega_0 - \frac{u}{u_0} \frac{\omega_0}{2\pi} \frac{2\omega_0}{\pi} t(x=a) = \frac{2A \arcsin a}{\sqrt{1+\gamma}} - \frac{A}{\sqrt{1+\gamma}} \quad (4.255)$
```

频率比由 (4.244c) 非线性参数 (4.236a) 通过 (4.252b) 引入了非谐因子 (4.256b) = 4.252a, b：

```
$$\frac{\omega_0}{\omega} \sqrt{1+\gamma} = 1 + \sum_{n=1}^{\infty} \frac{\gamma/4}{\gamma+1} \frac{[(2n)!]^2}{(n!)^2 2^{2n}} = 1 + \sum_{n=1}^{\infty} \frac{\beta^2}{2-\beta^2} \frac{(2n)!}{(n!)^2 2^{2n}} = A. \quad (4.256a)$$
```

非线性振荡器的振动频率 $\omega$ 比线性（4.221a）硬（4.257a）软（4.257c）弹簧的自然频率（4.257b）要大（小）小，这对应于弹簧刚度的增加（减小）：

```
$$\gamma < 0: \frac{\omega_0}{\omega} \frac{\gamma}{\gamma+1} < 1; \quad \gamma < 0: \frac{\omega_0}{\omega} > 1. \quad (4.257a-d)$$
```

谐振振荡器的自然频率（4.221c）不依赖于振幅，因为振幅很小（不小）对于线性（非线性）振荡器。证明（4.257c, d）如下。对于软（4.257c = 4.258a）弹簧：(i) 级数（4.258b）具有正项且大于1，因此它超过了1；由于它也超过了1（4.258d）：

```
$$\gamma < 0: A > \frac{1}{\sqrt{1+\gamma}} \Rightarrow \frac{\omega_0}{\omega} \frac{A}{\sqrt{1+\gamma}} > 1; \quad (4.258a-d)$$
```

```
$$\gamma > 0: A < \frac{1}{\sqrt{1+\gamma}} \Rightarrow \frac{\omega_0}{\omega} \frac{A}{\sqrt{1+\gamma}} < 1, \quad (4.258e-h)$$
```

硬（4.257a = 4.258e）证明（4.257a）如下：(i) 级（4.256b）具有交替和且绝对值递减，因此它收敛于连续项之间的和，例如第一项和第二（4.258f）；从（4.258g）得出（4.257b）。非线性振荡器轨迹的逆形式精确解（4.254a）等于（4.251; 4.252a, b），并将反正弦表示为第二切比多项式的级数（4.4.12节）。

## 4.4.12 作为切比多项式级数的精确解

第二切比多项式由 (II.129b) \equiv (4.259a) 定义，意味着（4.259b, c）：

```
$U_N(\cos \phi) = 2^{1-N} \frac{\sin[(N+1)\phi]}{\sin \phi}, \quad (4.259a)$
```

```
$N = 2n-m-1: \quad \sin[2(n-m)\phi] = 2^{2n-m-2} U_{2n-m-1}(\cos \phi). \quad (4.259b, c)$
```

将 (4.259c) 代入 (4.251)，将反正弦规定为第二切比多项式的级数：

```
$\arg(\phi) = A\phi + \sum_{n=1}^{m} \frac{q^{2n}}{(2n-1)!} \sum_{m=0}^{n-1} \frac{(-1)^{n-m}}{(n-m)!} 2^{2n-m-2} U_{2n-m-1}(\cos \phi). \quad (4.260)$
```

在 (4.254a) 中使用 (4.246a; 4.259c) 得到等效的结果：

```
$\omega_0\sqrt{1+\gamma} = A \left( \frac{x}{a} + \sum_{n=1}^{m} \left( - \frac{\gamma}{\gamma+1} \right)^n \frac{(2n)!}{(n!)^2} 2^{2n} \right) \sum_{m=0}^{n-1} \frac{(-1)^{n-m}}{n-m!} \frac{2^{2n-m-2}}{(2n-m)!} U_{2n-m-1}\left( \sqrt{\frac{x^2}{a^2}}\right), \quad (4.261)$
```

这规定了（问题11）具有二次势能（4.215b）的非谐振荡器（4.215a）的轨迹，使用了第二切比多项式（4.259a）、振幅 $A$（4.218b）、自然频率（4.221c）和非线性参数（4.244c）。在线性情况 $\gamma=0$ 下，仅保留 (4.261) 右侧的第一项，留下了谐振振荡器（4.223），因为振幅很小（不小）对于线性（非线性）振荡器。最低阶 $O(\gamma)$ 非线性扰动被考虑：(i) 频率（4.4.13节），(ii) 振幅（4.4.14节），以及 (iii) 谐波（4.4.15节）。

### 4.4.13 非线性对频率的影响

最低阶非线性近似（4.262a）通过（4.246）规定（4.4b）：

```
$q^4 \ll 1: \omega_0\sqrt{1+\gamma} = \int_0^\phi [1+q^2/2] d\phi
= \int_0^\phi [1+\frac{\gamma}{4}] d\phi \quad (4.262a, b)
= \left(1+\frac{\gamma}{4}\right)\phi \quad (4.27)$
```

最低阶非线性近似（4.262a）通过（4.244c）对应（4.263a）并意味着：

```
$\gamma^2 \ll 1: \frac{\omega_0}{\omega} = 1+\gamma=\frac{\gamma}{4} \quad (4.263a-b)$
```

第二项（4.262b）的右侧具有（4.263d）的上界：

```
$-\frac{q^2}{8}\sin(2\phi) \le \frac{|q^2|}{8}-\frac{\gamma}{16} \quad (4.263d)$
```

对于足够长的时间（4.264a），（4.262b）的右侧是可以忽略的，导致了（4.264b）：

```
$t \gg \frac{\gamma}{8}: \omega_0\sqrt{1+\gamma} = \int_0^\phi [1+\frac{\gamma}{2}-\frac{\gamma}{4}] d\phi = \left(1+\frac{\gamma}{4}\right)\phi \quad (4.264, b)$
```

设定 (4.265a) 得到：

```
$\phi = \omega_0 t \left(1+\frac{\gamma}{4}\right)\left(1+\frac{3\gamma}{4}\right) \quad (4.265b)$
```

这是振动频率（4.267c）。与无阻振荡器（4.254）相比，非线性效应（4.26）不仅影响频率（4.4.13），还影响位移（4.4.14）。

## 4.4.4 非线性对位移的影响
