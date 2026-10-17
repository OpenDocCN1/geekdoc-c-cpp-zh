
将不精确微分 (3.185b) $\equiv$ (3.186a) 乘以积分因子 (3.189b) [(3.190b)] 可得到精确微分 (3.191) [(3.92)]：

```latex
$0=\exp\left(-\int P dx\right)(Py dx-dy\right)=-d\left[y\exp\left(-\int P dx\right)\right],\quad (3.191)$
```

```latex
$0=\frac{1}{y}(Py dx-dy)=Pdx-\frac{dy}{y}=d\left[\int Pdx-\log y\right],\quad (3.192)$
```

由 (3.191) [(3.192)] 可得到一般积分 (3.193a) [(3.193b)]，通过对积分常数进行适当识别，它们与 (3.188b) 一致：

```latex
$y\exp\left\{-\int P(\xi)d\xi\right\}=C,\quad\int P(\xi)d\xi-\log y=-\log C;\quad (3.193a, b)$
```

这两个积分因子是独立的，因为其中一个 (3.189b) 依赖于 $x$，另一个 (3.190b) 依赖于 $y$ 以及它们的比值：

```latex
$C=\frac{\lambda(x)}{\mu(y)}=y\exp\left\{-\int P(\xi)d\xi\right\},\quad (3.194)$
```

这是 (3.188b) $\equiv$ (3.193a) $\equiv$ (3.194) 与 (3.180b) 一致。求解线性无外力一阶微分方程 (3.19a) 的四种方法已用于说明积分因子的性质。标准的 (LII) 线性一阶微分方程 (3.27) 也可以使用仅依赖于 $x$ 的积分因子求解（例 10.7）。在依赖于单个变量（[节 3.8.7]）（$x$ 或 $y$）的最简单积分因子与任意依赖于两个变量（$x$ 和 $y$）的最一般（[节 3.8.11]）积分因子之间，存在积分因子：(i/ii) 通过两个变量之和（积）（[节 3.8.8(3.8)]）对称依赖；以及 (iii) 关于变量的比（[节 3.8.10]），如齐次方程 (3.7) 中。

### 3.8.8 对两个变量对称依赖的积分因子

对称积分因子的例子是变量的函数 (3.195a)，它意味着 (3.195b)：

```latex
$z=x+y;\quad\frac{\partial}{\partial x}-\frac{\partial z}{\partial x}\frac{\partial z}{\partial z}-\frac{\partial z}{\partial z}\frac{\partial z}{\partial y}-\frac{\partial}{\partial y}=\quad\Omega=(X-Y)\frac{d}{dz}\{\log[\lambda(z)]\},\quad (3.195a–d)$
```

# 46 非线性微分方程与动力学系统

将 (3.195b, c) 代入 (3.176b) 可得（标准 LXX）不精确微分 (3.197c) 微分 (3.197a, b) 的系数满足 (3.196a)：

```latex
$$\frac{1}{X-Y}\left(\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}\right)=\frac{\Omega}{X-Y}=h(x+y);\quad\lambda(x+y)=\exp\left\{\int^{x+y}h(z)dz\right\},$$
```

(3.196a, b) 存在一个仅取决于变量之和 (3.196b) 的积分因子 (3.174b)。例如，微分 (3.197a) 的系数 (3.197b, c) 导致非零旋度 (3.197d)，证明了是不精确的：

```latex
$0=2ydx+(x+3y)dy;\quad\{X,Y}=\{2y,x+3y\};\quad\Omega=-1.$
```

(3.197a–d) 通过 (3.198a) 满足条件 (3.196a)：

```latex
$$\frac{\Omega}{X-Y}=\frac{1}{x+y}=h(x+y);\quad\lambda(x+y)=\exp\left\{\int^{x+y}dz\right\}=x+y,$$
```

(3.198a, b) (3.196b) 积分因子 (3.198b)。将不精确微分 (3.197a) 乘以积分因子 (3.198b) 得到精确微分 (3.199a)：

```latex
$0=(x+y)[2ydx+(x+3y)dy]=(x+y)[2ydx+(x+y)dy]$
```

```latex
$=yd[(x+y)^2]+(x+y)^2dy=d[(x+y)^2],$
```

(3.199a) 得到：

```latex
$C(x+y)^2=x^2y+2xy^2,$
```

(3.199b) 作为不精确微分 (3.197a) 的一般积分 (3.199a)：

### 3.8.9 依赖于变量之和或积的积分因子

涉及两个变量对称 (x, y) 的积分因子依赖于其和 (3.195a–d) [或依赖于 3.200a–c]：

```latex
$u=xy:[\frac{\partial}{\partial x}-\frac{\partial}{\partial y}\left[\frac{\partial u}{\partial x}-\frac{\partial u}{\partial y}\frac{d}{du}\right]=\{y,x\};\quad\Omega=(X-Y)\frac{d}{du}\left[\log(u)\right];$
```

3.200a–d) # 微分与一阶方程 将 (3.200b, c) 代入 (3.176b) 得到 (3.200d)，意味着：

```latex
$$\frac{\Omega}{X-Y} = \frac{\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}}{X-Y} = j(xy);\quad\lambda(xy) = \exp\left\{\int^{xy}j(u)\right\}.$$
```

(3.201a, b) 已证明，如果（标准 LXX）不精确微分 (3.177c) 微分 (3.177a, b) 的系数满足 (3.201a)，则存在依赖于变量积 (3.201b) 的积分因子 (3.174b)。例如，微分 (3.202a) 的系数 (3.202b, c) 且是不精确的 (3.202d)：

```latex
$y(1+xy)dx+xdy=0;\{X,Y}=\{xy^2, x\};\quad\Omega=-2;
```

(3.202a–d) 因为 (3.201a) 满足 (3.203a)，存在 (3.201b) 积分因子：

```latex
$$\frac{\Omega}{X-Y} = \frac{-2}{xy} = j(xy);\quad\lambda(xy) = \exp\left\{\int^{xy}\frac{-2}{u}\right\} = \frac{1}{x^2}.$$
```

(3.203a, b) 将不精确微分 (3.202a) 乘以积分因子 (3.203b) 得到精确微分 (3.204a)：

```latex
$0=\frac{y(1+xy)dx+xdy}{x^2y^2} = \frac{dx}{x^2y}+\frac{dy}{xy^2} = d\left(\log x-\frac{1}{xy}\right);
```

$C=\log x-\frac{1}{xy},$

```

(3.204a, b) 因此是不精确微分 (3.202a) 的一般积分 (3.210)。

### 3.8.10 齐次函数的积分因子

与齐次方程类似，(127) 被视为依赖于变量比 (3.205a) 的积分因子，导致 (3.205b, c)：

```latex

$$y=\frac{1}{x};\quad \left\{\frac{\partial}{\partial x}-\frac{\partial}{\partial y}\right\} = \left\{\frac{\partial v}{\partial x}-\frac{\partial v}{\partial y}\right\} = \left\{\frac{y}{x^2}-\frac{1}{x}\right\}\frac{d}{dv},

```

(3.205a–d) $\Omega=\frac{X}{X+x^2}\frac{d}{dv} = \{\log[\lambda(v)]$;

# 48 非线性微分方程与动力学系统

将 (3.205b, c) 代入 (3.176b) 得到 (3.205d)；后续如果（标准 LII）不精确微分 (3.177c) 微分 (3.177a, b) 的系数满足 (3.206a)：

```latex

$x^2\Omega = x^2\left(\frac{\partial Y}{\partial x} \frac{\partial X}{\partial y}\right) = k\left(\frac{y}{x}\right) = \lambda\left(\frac{y}{x}\right) = \exp\left\{\int^{y/x} k(v)dv\right\},

```

(3.206a, b) 存在仅依赖于变量比 (3.206b) 的积分因子 (3.174)。例如，微分 (3.207a) 的系数 (3.207b, c)是不精确的 (3.207d)：

```latex

$0=(2x+y)dx+(2y-x)dy;\{X,Y}=\{2x+y,2y-x\};\quad\Omega=-2;

```

(3.207a-d) 条件 (3.208a) 满足：

```latex

$$\frac{\Omega}{X-Y} = \frac{x^2}{x^2+y^2} = \frac{1}{1+y^2/x^2} = k\left(\frac{y}{x}\right),$$

```

$\lambda\left(\frac{y}{x}\right)=\exp\left\{\int^{y/x} \frac{dv}{1+v^2}\right\}=\exp\left[-\arctan\left(\frac{y}{x}\right)\right],$

(3.208a) 得到积分因子 (3.208b)，其微分为：

```latex

$d\lambda=-\lambda\left[\arctan\left(\frac{y}{x}\right)\right]=-\lambda\frac{d(y/x)}{1+y^2/x^2}.

```

(3.208c) 将不精确微分 (3.207a) 乘以积分因子 (3.208b) 得到精确微分：

```latex

$0=\lambda[(2x+y)dx+(2y-x)dy]=\lambda(ydx-xdy)+2\lambda(xd+yd)=(x^2+y^2)d\lambda,

```

使用了 (3.209) (3.208c)。将方括号中的项等于任意常数 (3.209) 并使用 (3.208b)，得到：

```latex

$x^2+y^2=\frac{C}{\lambda}=C\exp\left[-\arctan\left(\frac{y}{x}\right)\right],

```

(3.210) 是不精确微分 (3.207a) 的一般积分 (3.210)。

# 微分与一阶方程

### 3.8.11 非对称齐次积分因子

作为依赖于两个变量（不同于 3.8.6）且既不对称（节 3.8.8–3.9）也不齐次（节 3.8.10）积分因子的例子，考虑微分 (3.211a)，它在 $a \neq b$ 时是不精确的，并有一个积分因子 (3.211b)：

```latex

$0 = ay \ dx + bx \ dy;\quad \lambda = x^{a-1}y^{b-1}, \quad (3.211a, b)

```

通过它们的积 (3.211) 得到 (3.212a)：

```latex

$0 = x^ay^b = x^{a-1}y^{b-1}(ay \ dx + bx \ dy) = d(x^ay^b), \quad (3.212a)

```

这证明了 (3.212b) 是不精确微分 (3.211a) 的一般积分。将 $a, b$ 替换为 $\alpha, \beta$，由此推导出不精确微分 (3.213a) 有积分因子 (3.213b)，得到一般积分 (3.213c)：

```latex

$0 = \alpha y \ dx + \beta x \ dy; \quad \lambda = x^{\alpha-1}y^{\beta-1}; \quad x^\alpha y^\beta = C, \quad (3.213a, c)

```

积分因子的比 (3.211, 3.213b) 在 (3.214a) 中：

```latex

$$\frac{\mu}{\lambda} = x^{\alpha-a}y^{\beta-b}; \quad (ay \ dx + bx \ dy)x^{\alpha-a}y^{\beta-b} = (3.214a, b)

```

意味着不精确微分 (3.211b) 有积分因子，因为其积是精确微分：

```latex

$0 = \lambda[(ay \ dx + bx \ dy) + x^{\alpha-a}y^{\beta-b}(\alpha \ dx + bx \ dy)] = d(x^\alpha y^\beta). \quad (3.215)

```

不精确微分 (3.214b) 有积分因子 (3.211b) 得到一般积分 (3.216)：

```latex

$x^\alpha y^\beta = C.

```

# 非线性微分方程与动力系统

且不需要积分因子。在情况 (3.217a) 中，积分因子 (3.211b) 简化为 (3.218a)，从而得出 (3.218b)：

它指定了与之前相同的通积分 (3.217c)。在示例 10.8 中考虑了其他五种关于非精确微分的积分因子情况。

## 3.9 积分因子的存在或不存在

除了二变量一阶微分方程的两种情况 (i, ii)（第 3.8 节）外，还有针对三变量的第三种情况 (iii)，即积分因子不存在，导致了法夫问题（Pfaff problems）。对于二变量的一阶微分方程，积分因子总是存在，这意味着存在与系数确定的连续向量场正交的平面曲线。对于三变量的一阶微分方程有三种情况 (i-iii)。如果系数向量的旋度为零，则情况 (i) 是精确微分（第 3.9.1 节）；在这种情况下，积分是直接的，并满足与向量场正交的一族面。在情况 (ii) 下，微分是非精确且具有积分子的（第 3.9.2 节），同时也存在与向量场正交的一族面（第 3.9.4 节）；完整性的充分必要条件是贝尔特米条件（Beltrami condition），即系数向量场与其旋度正交（第 3.9.3 节），这意味着切线没有扭率或速度为零（第 3.9.5 节）。最简单的法夫问题出现在三变量非精确微分的情况 (iii) 中，此时向量不满足贝尔特米条件（第 3.9.6 节）；但在任何正则曲面上都存在一族与向量场正交的曲线（第 3.9.7 节）。三变量的一般一阶微分导致了用三个标量克莱布什势对向量场的最一般表示（第 3.9.8 节）。存在两种替代表示方法（第 3.9.9 节）：(i) 使用一组不同的标量势；以及 (ii) 用一个矢量势替换其中两个标量势。三维力的功在 (a) 中是三变量的一个没有积分因子的非一阶微分（第 3.9.10 节）；在保守力场的特殊情况 (b) 下（即单个标量势的梯度），它成为一个精确微分。一般情况 (a) 引出了热力学第一定律（第 3.11 节）；即熵、温度和内能的存在。

# 微分与一阶方程

### 3.9.1 三变量的精确微分

二变量微分 (3.145b) 的系数向量具有两个分量 (3.145a)，这意味着：(i) 为了成为由单个函数指定的精确微分（第 3.8 节），必须满足可积性条件；(ii) 对于非精确微分（第 3.9 节），积分因子总是存在，因为它提供了第二个函数。随着变量数量的增加，需要满足的向量分量更多，因此对 (i) 精确微分和 (ii) 积分因子的约束更多。例如，三变量的一阶微分 (3.219)：

```
0 = X(x,y,z)dx+Y(x,y,z)dy+Z(x,y,z)dz,
```

如果它与一个三变量函数的微分一致 (3.220a)，则它是精确的，这意味着必须满足三个条件 (3.220b)：

```
dΦ = X dx+Y dy+Z dz: {X,Y,Z} = {\frac{\partial Φ}{\partial x},\\frac{\partial Φ}{\partial y},\\frac{\partial Φ}{\partial z}}. (3.220a, b)
```

如果该函数具有连续的二阶导数 (3.221a)，则跨阶二阶导数相等 (3.221b–d)：

```
Φ \in C^2(R³): {\frac{\partial^2\Phi}{\partial y\partial x},\\frac{\partial^2\Phi}{\partial x\partial y},\\frac{\partial^2\Phi}{\partial z\partial x},\\frac{\partial^2\Phi}{\partial x\partial z},\\frac{\partial^2\Phi}{\partial z\partial y},\\frac{\partial^2\Phi}{\partial y\partial z}}. (3.221a–d)
```

这意味着系数向量具有连续的一阶导数 (3.222a)，并遵循 (3.222b–d)：
