
非稳定、非线性与混沌系统

163

等价于：

```
$$\sin(\omega t) = \sin\left(1 + \frac{\gamma}{4} \cos^2 \phi\right), \quad (4.270)
```

使用 (4.268a)。将 (4.246a) 代入 (4.270) 得到非线性性的一阶项：

```
$$\frac{x}{a} = \sin \phi = \frac{\sin(\omega t)}{1 + (\gamma/4) \cos^2(\omega t)} = \sin(\omega t) \left[1 - \frac{\gamma}{4} \frac{1 + \cos(2\omega t)}{2}\right]$$
= \left(1 - \frac{\gamma}{8}\right) \sin(\omega t) - \frac{\gamma}{2} \sin(3\omega t) - \left(1 - \frac{\gamma}{16}\right) \sin(\omega t) - \frac{\gamma}{16} \sin(3\omega t),\quad (4.271)
```

其中使用了 (II.582a; II.588c)。由 (4.271) 可知，非线性效应改变了振幅（4.4.14节）并产生了谐波（4.4.15节）。

## 4.4.15 非线性振子器中谐波的产生

将 (4.271) 写成形式：

```
$x(t) = a \left(1 - \frac{\beta a^2}{32}\right) \sin(\omega t) - \frac{\beta a^3}{32} \sin(3\omega t) = -x(-t), \quad (4.272a, b)$
```

表明无阻尼无外力非谐振子 (4.215a)（问题 113）具有二次势 (4.215b)，相对于谐振振子 (2.54a; 4.223c)，在非线性参数 (4.236a) 的最低阶情况下，对于弹簧 $\beta > 0$（软弹）或 $\beta < 0$（硬弹）：(i) 频率（4.265c）增加（减少）且基频处的振幅减少（增加），对应于 (4.272a) 右侧的第一项；(ii) 对应于 (4.272a) 右侧的第二项，产生了三频谐波，其振幅较小且与基频同相位。恢复力 (4.215a) 中的立方非线性导致在非线性参数 (4.236a) 的最低阶下，在第一阶谐波之后产生二阶谐波，因为 (4.272a) 右侧的第二项频率是 $30$ 而不是 $20$；这意味着位移仍然是 (4.272b) 的奇函数，意味着在零时刻位移为零。因此，非线性恢复力会导致线性振子自然频率的谐波的产生；这一点通过接下来的章节（4.5 节）使用扰动展开近似法得到了证实，该方法被应用于包含二次和三次项的更一般的非线性恢复力。

## 4.5 扰动方程与谐波的产生

已经证明（4.4 节）非线性恢复力：(i) 相对于线性系统的自然频率改变了振动频率（4.4.13节）；以及 (ii) 产生了基模的谐波（4.4.15节）。获得频率变化和谐波振幅最直接的方法是使用扰动展开（4.5 节）。扰动展开是一种近似方法（4.5 节）。它应用于包含线性、二次和三次项的更一般的恢复力（4.5.1节），以获得谐谐振子的第一阶（二阶）非线性修正（4.5.2节和 4.5.3节），这些修正规定了频率的变化和谐波的产生。

### 4.5.1 具有二次和三次项的恢复力

重新考虑无外力无阻尼非谐振子 (4.216b)，其恢复力包含线性、二次和三次项 (4.273)，对应于具有二次、三次和四次方项的势 (4.274)：

```
$m\ddot{x}=-j(x)(1+\varepsilon ax+\varepsilon^2 \beta x^2)=-\frac{d\Phi}{dx},$ (4.273)
```

```
$$\Phi(x)=\frac{1}{2}kx^2(1+\frac{2}{3}\varepsilon ax+\frac{1}{2}\varepsilon^2 \beta x^2),$ (4.274)
```

其中小参数 $\varepsilon$ 表明恢复力 (4.273a) 中的二次（三次）项；即势 (4.273) 中的三次（二次）项是一阶（二阶）小量。势 (4.274) 满足 (4.214b, c)，因此原点处于稳定平衡位置，其邻域是对应于振荡运动的势阱。引入谐振子 (4.54c) 的自然频率 (4.221c) 得到 (4.275)：

```
$$\omega_0=\sqrt{\frac{k}{m}}\quad \ddot{x}+\omega_0^2x=-\omega_0^2(\varepsilon ax+\varepsilon^2 \beta x),$ (4.275a, b)
```

涉及二次（三次）非线性参数 $\alpha, \beta$。位移 (4.276a) 和频率 (4.276b) 由扰动展开规定：

```
$x(t)=x_1(t)+\varepsilon x_2(t)+\varepsilon^2 x_3(t)+..., \omega=\omega_0+\varepsilon \omega_1+\varepsilon^2 \omega_2+....$ (4.276a, b)
```

## 非稳定、非线性与混沌系统

严谨的方法需要扰动展开在 $n \rightarrow \infty$ 时收敛。在大多数问题中，只能得到 $O(\varepsilon)$ 或 $O(\varepsilon^2)$ 项作为小 $\varepsilon$ 的近似。将 (4.276a, b) 代入 (4.273)：

```
$$\dot{x}_1 + \varepsilon\dot{x}_2 + \varepsilon^2\dot{x}_3 + (\omega - \omega_1 - \varepsilon^2\omega_1)^2 (x_1 + \varepsilon x_2 + \varepsilon^2 x_3) = -\varepsilon\alpha\omega_1(x_1 + \varepsilon x_2 + \varepsilon^2 x_3) - \varepsilon^2\beta\omega_1^2(x_1 + \varepsilon x_2 + \varepsilon^2 x_3),$ (4.277)
```

在 (4.277) 的第二项中对于 $O(\varepsilon^2)$ 有：

```
$\varepsilon^3 \ll 1:quad \omega_0^2 = (\omega - \omega_1 - \varepsilon^2\omega_1)^2 = \omega_0^2 - 2\varepsilon\omega_1\omega + \varepsilon^2(\omega_1^2 - 2\omega_2).$ (4.278a, b)
```

等令 $\varepsilon$ 的连续幂次系数得到 (4.279a; 4.280;：

```
$\varepsilon^0:\quad \dot{x}_1 + \omega^2 x_1 = 0, \quad x_1(t) = a\sin(\omega t),$ (4.279a, b)
```

```
$\varepsilon^1:\quad \dot{x}_2 + \omega^2 x_2 = 2\omega\omega_1 x_1 - \varepsilon\alpha x_1^2,$
$\varepsilon^2:\quad \dot{x}_3 + \omega^2 x_3 = 2\omega\omega_1 x_2 + (2\omega - \omega_1)x_1 - \varepsilon\alpha x_1 x_2 - \varepsilon^2\beta x_1^3.$ (4.281)
```

扰动展开法 (4.276a, b) 将非线性问题 (4.273) 转换为（问题 114）无限线性问题序列 (4.279a; 4.280; 4.281;...)，每一阶：(i) 满足相同的微分方程；(ii) 由前阶的线性和非线性组合驱动。在具有恢复力 (4.273a) 的非谐振子情况下：(i) 最低阶 (4.279a) 是频率 $\omega$ 待定的振荡 (4.279b)；(ii) $n$ 阶涉及低阶 $(1, 2, ..., n-1)$ 项，产生频率高达 $n\omega$ 的谐波。这种扰动展开法通过第一阶（二阶）近似进行演示（4.5.2–4.5.3–4.5.4 节）。

### 4.5.2 一阶扰动与此性条件

```
$$\dot{x}_2 + \omega^2 x_2 = 2\omega\omega_1 a\sin(\omega t) - \frac{\alpha}{2}\omega_0^2 a^2 [1 - \cos(2\omega t)].$ (4.282)
```

## 非线性微分方程与动力系统

(4.282) 右侧的第一项是频率 $\omega$ 的激励，会导致无阻尼共振（2.7.3节），振幅随时间线性增长 (2.17b)；这意味着振子的能量将随时间平方级增长 (2.17c)，这是不可能的，因为系统没有外力作用且总能量是守恒的 (4.210c)。因此，该项必须排除，强制执行**此性条件**，其振幅为零；一阶没有频率变化 (4.283a)，且 (4.282) 简化为 (4.282)：

```
$\omega_1=0;\quad \dot{x}_2 + \omega^2 x_2 = -\frac{\alpha}{2}\omega_0^2 a^2[1 - \cos(2\omega t)].\quad(4.282)$
```
