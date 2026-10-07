

## 4.6.6 谐波激励下的非线性参数共振

线性振子器 (4.320b) 在接近自然频率 (4.320a) 第一谐波 (4.302b) 的频率下受到激励，会导致相应的响应 (4.320b)。

```
$$\omega_a = 2(\omega_0 + \varepsilon); \quad \ddot{x}_1 + \omega_0^2 x_1 = f_a \cos(\omega_0 t), \quad x_1(t) = -\frac{f_a}{3\omega_0} \cos[2(\omega_0 + \varepsilon)t].$$
```

(4.320a–c)

线性阻尼谐振器 (4.303)的一阶近似为 (4.321)：

```
$$\ddot{x}_2 + 2\lambda\dot{x}_2 + \omega_0^2(x_2 + \alpha x_2^2) = -2\alpha\omega_0\dot{x}_1x_2 + \dots$$
```

其中右侧（r.h.s.）仅保留会导致两倍自然频率 (4.320a) 激励的项。将 (4.320c) 代入 (4.321) 得：

```
$$\ddot{x}_2 + 2\lambda\dot{x}_2 + \omega_0^2x_2 \left[1 - \frac{2\alpha f_a}{3\omega_0} \cos[2(\omega_0 + \varepsilon)t]\right] + \omega_0^2(\alpha x_2^2 + \beta x_2^3) = 0,\ (4.322a)$$
```

根据振荡频率 (4.304a) 的 (4.322b) 项，这对应于第 4.3 节中的参数共振 (4.181)：

```
$$\ddot{x}_2 + 2\lambda\dot{x}_2 + \omega_0^2x_2 = \omega_0^2\frac{2\alpha f_a}{3\omega_0} \cos[2(\omega_0 + \varepsilon)t]. \ (4.322b)
```

将 (4.323a, b) 代入 (4.322b) 右侧的参数项中，得到 (4.323c)：

$$\omega \sim \omega_0, x_2(t) \sim \cos[(\omega_0 + \varepsilon)t]:$$

```
$$\frac{2\alpha f_b\omega_0^2}{3\omega_0^2}x_2 \cos[2(\omega_0 + \varepsilon)t] \sim \frac{2\alpha f_b}{3\omega_0} \cos[(\omega_0 + \varepsilon)t] \cos[2(\omega_0 + \varepsilon)t]$\\
= \frac{\alpha f_b}{3\omega_0} [\cos[(\omega_0 + \varepsilon)t] + \cos[3(\omega_0 + \varepsilon)t]];$\$\n\quad (4.323a–c)$$
```

频率为 $3(\omega_0 + \varepsilon)$ 的项是非共振的，在代入 (4.322b) 右侧时将其省略，得到 (4.323d)：

```
$$\ddot{x}_2 + 2\lambda\dot{x}_2 + \omega_0^2x_2 = \frac{\alpha f_b}{3\omega_0} \cos[(\omega_0 + \varepsilon)t].$$ (4.323d)
```

## 非稳态、非线性与混沌系统

振荡 (4.323d) 与代入 (4.324a) 后 (4.303) = (4.305) 相似：

```
$f_2 = \frac{\alpha |f_a| b}{3 \omega_0}} \quad b^2 = \left[\omega_0 b^2 \psi - \varepsilon\right]^2 + \lambda^2\right] = \left[\frac{f_2}{2\omega_0}\right]^2, \left[\frac{\alpha |f_a|^2}{6\omega_0^2}\right], \quad (4.324a, b)$
```

通过 (4.308a) (4.324a) 代换 $|f_a|$，得到激励幅度 $|f_a|$ 与振荡幅度 $b$ 之间的关系 (4.324b)。该关系可能导致：(i) 如前所述幅度跳跃（节 4.6.1–4.6.4）；同时也导致 (ii) 下面所示的振荡抑制（节 4.6.7）。

## 4.6.7 幅度跳跃与振荡抑制

带有近似值 (4.325a) 的幅度方程 (4.324b) 可以因式分解 (4.325b)：

```
$\varepsilon^2 <<\omega_0^2 b^4 \psi^2; \quad 0 = b^2 \left[\omega_0 b^4 \psi^2 - 2\omega_0 b^2 \psi + \lambda^2 - \left[\frac{\alpha f_a}{6\omega_0}\right]^2\right], \quad (4.325a, b)$
```

对于 $b^2$ 有三个根：(i) 零根 (4.326a)，根 (4.326b, c)：

```
$b_0 = 0, \quad (b_{\pm})^2 = \frac{1}{\omega_0 \psi} \left[\varepsilon \pm \sqrt{\lambda^2 - \left[\frac{\alpha f_a}{6\omega_0}\right]^2}\right], (4.326a–c)$
```

如果阻尼不是太强 (4.327a)，根 (4.326b, c) 为实数 (4.327b)：

```
$\lambda < \frac{\alpha f_a}{6\omega_0^3}: \quad (b_{\pm})^2 = \frac{\varepsilon \pm \varepsilon_0}{\omega_0 \psi}, \quad \varepsilon_0 = \frac{\sqrt{\left[\frac{\alpha f_a}{6\omega_0^3}\right]^{1/2}} - \lambda}{1}, (4.327a–c)$
```

根 (4.327b, c) 在点 $\varepsilon_0$ 处消失 (4.324a, b)：

```
$b_{\pm}(-\varepsilon_0) = 0 = b_{\pm}(\varepsilon_0), \quad b_{\pm}(\varepsilon_0) = \frac{2\varepsilon_0}{\omega_0 \psi}, \quad (4.328a–c)$
```

在 $\varepsilon_0$ 处第二个根具有值 (4.328c)。如图 14 所示：(i) 根 $b_-$ 在 $-\varepsilon_0$ 之外是真实的且稳定的。

## 非线性微分方程与动力学系统

![](img/6ac3bd14297bb79c4b6425c204_0.png)

**图 14** 在激励下势能为位置四次函数的非谐振器共振中，有：(i) 在低频范围 $\varepsilon < -\varepsilon_0$ 内零幅度；(ii) 三个幅度中最低的在 $-\varepsilon_0 < \varepsilon < \varepsilon_0$ 范围内稳定的；(iii) 两个幅度中最高的在中间范围内稳定的。在低频范围内，在 $\varepsilon = -\varepsilon_0$ 处无振荡，随后随频率增加；在高频范围内，在 $\varepsilon = \varepsilon_0$ 处发生 (i) 的反向情况，幅度减小；(iii) 在高频范围 $\varepsilon > \varepsilon_0$，振荡在 $\varepsilon_0$ 处开始带有幅度跳跃 (ii) 根 $b_r$ 在 $+\varepsilon_0$ 之外是真实的，但始终是不稳定的，它包含 $b_* > b_r > 0$ 段且朝向下；(iii) 根 $b_0 = 0$ 对应实轴，在 $-\varepsilon_0$ 和 $+\varepsilon_0$ 之外是不稳定的。运动可以描述为：(i) 从高频开始到 $+\varepsilon_0$ 处无振荡，在该处发生 $E$ 的跳跃 (4.328c)，随后是 $-\varepsilon_0$ 处幅度衰减的振荡；(ii) 在 $-\varepsilon_0$ 处随 $B$ 平滑增加幅度。如果 $\psi > 0$，则适用于图 14；因此，线性阻尼非谐振器 (4.303) 在接近自然频率第一谐波 (4.320a) 的激励频率下受到激励，自然频率非线性共振（图 14）具有：(i) $(-\varepsilon_0, +\varepsilon_0)$ 范围内的振荡；(ii) 低频 $\varepsilon < -\varepsilon_0$ 振荡被抑制；(iii) 高频处，如果从 $\varepsilon > \varepsilon_0$ 来自，直到 $\varepsilon_0$ 处发生幅度跳跃 (4.328c)，振荡从下方平滑增长。这对应于 Hopf 分叉 (4.5)。

## 非稳态、非线性与混沌系统

## 4.6.8 二谐波激励下的非线性参数共振

线性振子 (4.329b) 在接近自然频率第二谐波 (4.302a) 的激励频率 (4.329a) 下受到激励，会导致响应 (4.329c)：

```
$$\omega_a = 3(\omega_0 + \varepsilon); \quad \ddot{x}_1 + \omega_0^2x_1 = f_u \cos(\omega_a t), \quad x_1(t) = \frac{f_u}{8\omega_0^2} \cos[3(\omega_0 + \varepsilon)t].$$
```

(4.329a-c)

阻尼非线性振器 (4.303) 的一阶近似为 (4.330)：

```
$$\ddot{x}_2 + 2\lambda\dot{x}_2 + \omega_0^2x_2 + \alpha x_2^2 + \beta x_2^2 = -3\beta x_1x_2^2 + \dots$$
```

(4.330)

其中仅保留了一阶和二阶二次项。这是因为对于接近自然频率 (4.331a) 的振荡 (4.331b)：

```
$$\omega = \omega_0 + \varepsilon; \quad x_2(t) = b \cos[(\omega_0 + \varepsilon)t] = b \cos(\omega).$$
```

(4.331a, b)

(4.330) 右侧的激励项：

```
$$-3\beta x_1(t)[x_2(t)]^2 = \frac{3\beta f_u b^2}{8\omega_0^2}\cos^2[(\omega_0 + \varepsilon)t] \cos[3(\omega_0 + \varepsilon)t]$$\\
= \frac{3\beta f_u b^2}{16\omega_0^2}\{1 + \cos[2(\omega_0 + \varepsilon)t]\} \cos[3(\omega_0 + \varepsilon)t]$$\\
= \frac{3\beta f_u b^2}{32\omega_0^2}\{\cos[(\omega_0 + \varepsilon)t] + \dots\},$\n(4.331c)$)$```

+   (i) 包含一个乘以频率平方的三倍频率；(ii) 后者引入了一个双倍频率；(iii) 双倍频率与三倍频率的乘积重新引入导致共振的频率；(iv) (4.330) = (4.331c) 右侧的共振项，以及将 (4.330) 左侧如 (4.303) 所示替换为振荡频率 (4.304a) 如 (4.305)，得到：

```
$$\dot{x}_2 + 2\lambda x_2 + \omega_0^2x_2 = \frac{3\beta f_u b^2}{32\omega_0^2}\cos[(\omega_0 + \varepsilon)t].$$
```
(4.332)$)$```

