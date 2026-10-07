

## 非线性微分方程与动力系统

一阶微分方程 (3.16a) 可分离变量 (3.16b)：

```
$$\frac{dy}{dx} = \cos x \sqrt{1-y^2}, \quad \int \frac{dy}{\sqrt{1-y^2}} = \int \cos x dx, \quad (3.16a, b)$$
```

且有通积分 (3.17a) 等价于 (3.17b)：

```
$$\arcsin y = C+\sin x, \quad y(x) = \sin(C+\sin x). \quad (3.17a, b)$$
```

边界条件 (3.18a) 导致任意常数有无穷多个取值 (3.18b)：

```
$1=y(0)=\sin C, \quad C=\frac{\pi}{2}+2n\pi.$
```

```
$y(x)=\sin(2n\pi+\frac{\pi}{2}+\sin x)=\sin(\frac{\pi}{2}+\sin x)=\cos(\sin x). \quad (3.18a–c)$
```

全部对应于解 (3.18c)。另一可分离的一阶微分方程在 EXAMPLE 10.6 中讨论。

### 3.2.2 线性无迫微分方程

若显式微分方程 (3.10a) 中的 $g(x, y)$ 关于独立变量 $y$ 线性且无迫，系数为 $P(x)$ 函数，依赖于被依赖变量 (3.19a)：

```
$$\frac{dy}{y}=P(x)y, \quad log y=\int \frac{dy}{y}=\int P(x)dx+\log C, \quad (3.19a, b)$$
```

则方程可分离变量 (3.11b)，从而可由积分求解：

```
$$X(x)=\exp{\{\int P(x)dx\}} \quad y(x)=CX(x). \quad (3.20a, b)$$
```

因此线性无迫 (标准 LI) 一阶微分方程 (3.20a) 有通积分 (3.21a, b)。对于例子，微分方程 (3.22a)：

```
$$y'=\left(\frac{1}{x}-x\right)y; \quad y(x)=C\exp(-\frac{x^{2}}{2}+x). \quad (3.21a, b)$$
```

## 微分与一阶方程

有通积分 (3.21b)=(3.22b)：

```
$P(x)=-\frac{1}{x}; \quad y(x)=C\exp\left(\int^{x} \frac{1}{\xi} d\xi\right)=C\exp\left(\log x-\frac{x^{2}}{2}\right), \quad (3.22a, b)$
```

其中在此情况下应用了 (3.20a) 与 (3.22a)。边界条件 (3.23a) 确定了常数：

```
$1=y(1)=\frac{C}{\sqrt{e}}; \quad y(x)=x\sqrt{e}\exp\left(-\frac{x^{2}}{2}\right)=x\exp\left(\frac{1-x^{2}}{2}\right), \quad (3.23a, b)$
```

在唯一解 (3.23b) 中。另一线性无迫一阶微分方程的例子 (3.24a) 有通积分 (3.24b)：

```
$y'=y\tan x; \quad y(x)=C\sec x, \quad (3.24a, b)$
```

由 (3.19a) 可得，其中 (3.25a) 导致 (3.25b)\equiv$ (3.24b)：

```
$P(x)=\tan x; \quad y(x)=C\exp\left(\int^{x} \tan \xi \,d\xi\right)=C\exp\left{-\log(\cos x)\right}=\frac{C}{\cos x}. \quad (3.25a, b)$
```

边界条件 (3.26a)：

```
$1=y(0)=C; \quad y(x)=x\sec x, \quad (3.26a, b)$
```

导致唯一解 (3.26b)：

### 3.3 线性有迫微分方程

参数变异法 (Bernoulli 1697) 可用于从线性无迫微分方程的通积分中获得相应有迫无迫微分方程的特积分，该线性无迫微分方程具有变系数 (Notes 1.2–1.4)。例如，对于：(i) 常系数二阶系统 (section 2.9) 和 (ii) (3.19a) 的推广作为一阶线性有迫微分方程，具有变系数 (标准 LII)：

```
$y'=P(x)y+Q(x), \quad (3.27)$
```

## 非线性微分方程与动力系统

因此命名是因为 $y'$ 是 $y$ 的线性函数，系数依赖于 $x$。它将通过常数变异法求解，从无迫方程 (3.19a) 的解 (3.20a, b) 出发，将任意常数 C 替换为函数 C(x)，使得有迫方程 (3.27) 得到满足。因此，线性有迫方程 (3.27) 的解被求为形式：

```
$y(x)=C(x)X(x)=C(x)\exp\left{\int^x P(\xi)d\xi\right};\quad(3.28)$
```

求导得到：

```
$y'=(C'+CP)\exp\left{\int^x P(\xi)d\xi\right}=Py+C'X.\quad(3.29)$
```

方程 (3.29) 与 (3.27) 吻合，前提是仍未确定的函数 C(x) 满足 (3.30a)：

```
$Q=C'X,\quad\quad C(x)=C+\int^x\frac{Q(\xi)}{X(\xi)}d\xi,\quad(3.30a, b)$
```

即一阶微分方程，其解为 (3.30b)。将 (3.30b) 代入 (3.28)：

```
$Y(x)=\int^x\frac{Q(\xi)}{X(\xi)}d\xi,\quad\quad y(x)=X(x)[C+Y(x)],\quad\quad(3.31a, b)$
```

可知线性有迫 (标准 LII) 一阶微分方程 (3.27) 的完全积分 (3.31b) 由以下组成：(i) 无迫方程 (3.19a) 的通积分 (3.20b)，即 (3.31b) 右端的第一项，涉及一个任意常数和函数 (3.20a)；以及 (ii) 后者也出现在有迫方程 (3.27) 的特积分中，即 (3.31b) 右端的第二项，涉及 (3.31a) 且不含积分常数。例如线性有迫一阶微分方程 (3.32a)：

```
$y'=-\frac{y}{x}+\exp(x^2);\quad\quad\quad y(x)=\frac{C}{x}\frac{e^{x^2}}{2},\quad\quad(3.32a, b)$
```

## 微分与一阶方程

有完全积分 (3.32b)，通过代入 (3.33a–d) 得到

$P(x)=-\frac{1}{x} \quad X(x)=\exp\left(-\int \frac{d\xi}{\xi}\right)=\exp(-\log x)=\frac{1}{x}, \quad (3.33a, b)

$Q(x)=e^{x^2}: \quad Y(x)=\int \xi e^{\xi^2} d\xi=\frac{1}{2}e^{x^2}, \quad (3.33c, d)

在 (3.31b) 中。边界条件 (3.34a)：

$1=y(1)=C+\frac{e}{2}; \quad y(x)=\left(1-\frac{e}{2}\right)\frac{1}{x}\frac{e^{x^2}}{x}-\frac{e^{x^2}}{2x}, \quad (3.34a, b)

导致唯一解 (3.34b)。

另一线性一阶有迫一阶微分方程，具有变系数 (3.35a)：

$y'=y\cot x+csc x: \quad y(x)=C\sin x-\cos x, \quad (3.35a, b)

其完全积分是 (3.35b)，如下通过代入 (3.36a–d) 得到：

$P(x)=\cot x: \quad X(x)=\exp\left{\int^x \cot \xi d\xi\right}=\\exp[\log(\sin x)]=\sin x \quad (3.36a, b)

$Q(x)=csc x: \quad Y(x)=\int^x csc^2 \xi d\xi=-cot x, \quad (3.36c, d)

在 (3.31b) 中。边界条件 (3.37a)：

$1=y\left(\pi/2\right)=C: \quad y(x)=\sin x-\cos x, \quad (3.37a, b)

导致唯一解 (3.37b)。另一线性有迫一阶微分方程在 EXAMPLE 10.6 中讨论。

## 非线性微分方程与动力系统

### 3.4 Bernoulli 变换 (1695)
非线性微分方程

Bernoulli (1695) 一阶常微分方程 (标准 LIII)：

```
y' = P(x)y+Q(x)y^n, (3.38)
```

约化：(i) 对于 n=0 到线性有迫 (3.27) 标准 LII，其积分为 (3.20a; 3.31a, b)；(ii) 对于 n=1 到线性有迫 (0.19a) 标准 LI，P→Q，其通积分 (3.20a, b) 为 (3.39b)：

```
n=1:
y(x)=exp\{\int^x[P(\xi)+Q(\xi)]d\xi\},\n(3.39a, b)
```

在所有 n≠0,1 的情况下，Bernoulli (1695) 方程 (3.38) 是一个非线性一阶微分方程 (标准 LIII)，推广了线性无迫 (标准 LIII)。除以 y^n：

```
n≠1:
Q+Py^{1-n}=y^{-n}'\frac{y^{1-n}'}{1-n},\n(3.40a)
```

它变为线性微分方程 (3.27)，通过变换：

```
y,P,Q→y^{1-n},(1-n)P,(1-n)Q;
(3.41a–c)
```

(3.40b) 的解 (3.31a, b) 因此是 (3.31a) [[3.31b]] 用替换 (3.41b)[3.41a)] 导致 (3.42a)[3.42b]：

```
X_n(x)=exp\{\int^xP(\xi)d\xi\},Y_n(x)=(1-n)exp\{\int^x\frac{Q(\xi)}{X_n(\xi)}d\xi\},\n(3.42a, b)
```

其中 X=X 且 Y_0=Y。通积分类似于 (3.31b)：

```
n≠1:
[y(x)]^{-n}=X_n(x)[C+Y(x)],
(3.43a, b)
```

其：(i) 对于 n=0 与 (3.31b) 吻合；(ii) 对于 n=1 破坏 (3.43a)，此时用 (3.39a, b) 替换。因此 (标准 LIII) Bernoulli (1695) 非线性一阶微分方程 (3.38) 有解 (Leibniz 1696)：(3.39b) 在

## 微分与一阶方程

线性无迫情形 (3.39a)；(3.43a, b) 在所有非线性情形 $n\neq0,1$，以及线性无迫情形 $n=0$ 在 (3.31a, b) 中。一个简单的非线性情形 (标准 LIV) 特定 Riccati 方程为 (3.44a, b)：

```
$n=2: \quad y'=yP(x)+y^2Q(x), \quad y=X_2(x)[C+Y_2(x)], \quad (3.44a-c)$
```

```
$X_2(x)=\exp\left{-\int^x P(\xi)d\xi\right\}, \quad Y_2(x)=-\int^x \frac{Q(\xi)}{X_2(\xi)}d\xi, \quad (3.44d)$
```

其解为 (3.44c-e)。接下来给出 Bernoulli 方程求解的两个例子，然后将 (3.44b) 推广到 Riccati 方程 (sec-3.5)。

非线性 Bernoulli 微分方程的特定 Riccati 类型的一个例子是 (3.45a)：

```
$xy'==-y+y^2\log x, \quad \frac{1}{y(x)}=Cx+1+\log x, \quad (3.45a, b)$
```

其完全积分 (3.45b) 由 (3.44b) 与 (3.44a–e) 得到，使用 (3.46a–d)：

```
$n=2: \quad P(x)=-\frac{1}{x}, \quad X_2(x)=\exp\left(\int^x \frac{d\xi}{\xi}\right)=\exp(\log x)=x \quad (3.46a-d)\nQ(x)=-\frac{\log x}{x}, \quad Y_2(x)=-\int^x \frac{\log \xi}{\xi^2}d\xi=\frac{1+\log x}{x},
```

最后一次积分 (3.46d) 可用两种方法进行：(i) 分部积分 (3.47)：

```
$Y_2(x)=\int^x \frac{\log \xi}{\xi}d\xi=\frac{\log x}{x}-\int^x \frac{1}{\xi}d(\log \xi)=\frac{\log x}{x}-\int^x \frac{d\xi}{\xi^2}=\frac{1+\log x}{x}, \quad (3.47)$
```

或 (ii) 改变同一变量 (3.4a) 得到相同结果 (3.48b)；(3.47)：

```
$$\eta=\frac{1}{\xi};Y_2(x)=-\int^x \log(\frac{1}{\xi})d(\frac{1}{\xi})=-\int_1^{1/x} \log \eta d\eta=-[\frac{\eta}{2} \log \eta - \eta]_1^{1/x}=\frac{1+\log x}{x} \quad (3.48a, b)$$
```
