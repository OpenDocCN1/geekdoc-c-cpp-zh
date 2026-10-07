

## 微分与一阶方程

相反，将不全微分乘以一个合适的积分因子可能会使其变为全微分，从而导出通积分。例如，该微分：

```
$0 = d\Phi = \tan y \ dx + \tan x \ dy
```

它是不全的，因为系数 (3.169a, b) 不满足 (3.169a) 的可积条件 (3.148c)：

```
\{X, Y\} = \{\tan y, \tan x\}: \quad \frac{\partial Y}{\partial x} = \sec^2 x \neq \sec^2 y = \frac{\partial X}{\partial y} \quad (3.169a-c)$
```

当乘以积分因子 (3.169a) 时：

```
$\lambda = \cos x \cos y; \quad \lambda d\Phi = \cos x \sin y \ dx + \cos y \sin x \ dy, \quad (3.169a, b)$
```

不全微分形式 (3.168) 变为 (3.169b)，后者是一个全微分 (3.170a)：

```
$0 = d\Phi = d(\sin x \sin y), \quad \sin x \sin y = C, \quad (3.170a, b)$
```

并导出了 (3.168) 的通积分 (3.170b)。这引出了二变量不全微分是否存在积分因子的问题，将在接下来证明（第3.8.4 节）。

## 3.8.4 不全微分积分因子的存在

任何显微分方程 (3.145b)即使是不全的，也可以写成形式：

```
$\frac{\partial y}{\partial x} = \frac{X(x,y)}{Y(x,y)}, \ (3.171)$
```

它有一个解 (3.146c)，意味着 (3.146b)，从而：

```
$\frac{\partial y}{\partial x} = \frac{\partial \Phi / \partial x}{\partial \Phi / \partial y}, \quad (3.172)$
```

将 (3.171) $\equiv$ (3.172) 相等可得到 (3.173a)：

```
$\frac{X}{Y} \frac{\partial \Phi / \partial x}{\partial \Phi / \partial y} = \frac{1}{X \ \partial x} \frac{1}{Y \partial y} \equiv \lambda, \quad (3.173a-c)$
```

这等价于 (3.173b)；该系数 (3.173c) 被称为**积分因子**，它将不全微分 (3.174a) 变为全微分 (3.174b)：

```
$$\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y} = \lambda(X dx + Y dy) = \frac{\partial \Phi}{\partial x}+\frac{\partial \Phi}{\partial y}dy = d\Phi.. (3.174a, b)$$
```

由此得出，不全微分 (3.174a) (3.145b) 具有一个满足 (3.173b, c) 的积分因子 $\lambda$，它导致了乘以全微分 (3.174b)。可以认为，由于微分 (3.145b) 涉及两个函数 (X, Y)：(i) 单个函数 $\Phi$ 无法导出全微分，除非满足可积条件 (3.148c)；以及 (ii) 两个函数 $(\lambda, \Phi)$ 可以导出全微分 (3.174b)，正如刚才所示的那样，此外 $\lambda$ 有无限种选择，如接文所示（第 3.8.5–3.8.6 节）。

## 3.8 求解积分因子的偏微分方程

为了确定**积分因子**所满足的方程，将 (3.173b, c) 代入 (3.148a, b)，得到 (3.175c) ：

```
$$\Phi \in C^2(|\mathbb{R}^2|): \quad 0=\frac{\partial^2 \Phi}{\partial x\partial y}-\frac{\partial^2 \Phi}{\partial y\partial x}-\frac{\partial}{\partial x}(\lambda Y)-\frac{\partial}{\partial y}(\lambda X), \quad (3.175a–c)$$
```

这等价于 (3.175c)=(3.176b) ：

```
$$\lambda \in C^1(|\mathbb{R}^2|): \quad \Omega=\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}+\frac{1}{\lambda}(\frac{\partial \lambda}{\partial x}Y-X\frac{\partial \lambda}{\partial y})=(X\frac{\partial \lambda}{\partial y}-Y\frac{\partial \lambda}{\partial x})\log\text{此处有误}$$
```

此处积分因子必须是连续可微的 (3.176a)。因此不全微分 (3.177c) (3.177a, b) ：

```
$$X,Y \in C^1(|\mathbb{R}^2|): \quad 0=X(x,y)dx+Y(x,y)dy, \Omega=\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y} \neq 0, \quad (3.177a–c)$$
```

具有一个可微的 (3.176a) 积分因子 (3.174a, b)，其满足的偏方程 (3.176b) 通常比不全微分 (3.145b) 更复杂；然而，为了获得 (3.145b) 的通积分，越简单的 (3.176b) 越好。如果 (3.145b) 是全微分，则积分因子为任意常数；如下所示。

## 3.8.6 无数积分因子

一般不全微分 (3.145b) 的积分因子 $\lambda$ 是一个不唯一的函数 $\lambda(x,y)$。例如，将 (3.178a) 代入 (3.176b) 得到 (3.178b) ：

```
$$\lambda = \mu\Phi; \quad \frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}+\left(Y\frac{\partial}{\partial x}-X\frac{\partial}{\partial y}\right)\log\mu = 0, \quad (3.178a, b)$$
```

从 (3.173a) 开始，如果 (3.178b) 的积分消失，则 $\mu$ 是 (3.179a)，导致：

```
$$\frac{\partial \Phi}{\partial x}=X\frac{\partial \Phi}{\partial y}; \quad \left(Y\frac{\partial \Phi}{\partial x}-X\frac{\partial \Phi}{\partial y}\right)\log\Phi = 0, \quad (3.179a, b)$$
```

证明了 $\mu$ 也是满足 (3.176b) 的积分因子。这一结果有两种表述方式：(i) 如果 $\lambda,\mu$ 是不全微分 (3.145b)(3.176b; 3.179b) 的积分因子，它们的比值 $\Phi=\lambda/\mu$ 在 (3.148a) 中是一个解 (3.46c)；或者如果 $\Phi$ 是不全微分 (3.145b) 的解 (3.46c) 且 $\mu$ 是积分因子 (3.179b)，那么 (3.178a) 和 (3.180b) 也是积分因子 (3.176b)，其中 (3.180a) 是解的可微函数：

```
$$G \in D(\mathbb{R}); \quad\quad\quad \lambda = \mu(\Phi). \quad (3.180a, b)$$
```

后者的结果源于以下陈之一：(i) 如果 $\Phi$ 是不全微分 (3.145b) 的解，那么 (3.181a) 也是解：

```
$$G(\Phi(x,y))=C; \quad \lambda(dX+dY)=G(\Phi); \quad (3.181a, b)$$
```

ii 如果通过乘以积分因子 $\lambda$ 将不全微分 (3.145b; 3.174a) 转换为全微分 (3.174b)，则 (3.181b) 也是全微分，证明 $\lambda$ 是积分因子。

## 3.8.7 依赖单变量的积分因子

由于积分因子不是唯一的，如果它们满足 (3.176a, b)，则可以在几种形式中寻找。仅为变量 $x$ 的简单积分因子由 (3.176b) 通过 (3.182a) 给出：

```
$$\Omega=\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}=-Y\frac{d}{dx}(\log[\lambda(x)]); \quad\quad X\frac{d}{dy}(\log[\lambda(y)]); \quad\quad (3.182a, b)$$
```

意味着不全微分 (3.177c) (3.177a, b) 的系数满足 (3.183a) [(3.184a)]，具有一个仅依赖于 $x$ 或 $y$ (3.183b) [(3.184b)] 的积分因子 (3.174) ：

```
$$\frac{1}{Y} \left( \frac{\partial X}{\partial y}-\frac{\partial Y}{\partial x} \right) = \Omega f(x); \quad \lambda(x)=\exp\left( \int^x f(\xi)d\xi \right), \quad (3.183a, b)$$
```

```
$$\frac{1}{X} \left( \frac{\partial X}{\partial x}-\frac{\partial Y}{\partial y} \right) = \Omega g(y); \quad \lambda(y)=\exp\left( \int^y g(\eta)d\eta \right), \quad (3.184a, b)$$
```

