

# 非线性微分方程与动力学系统

## 3.8 全微分与非全一阶微分

一阶微分方程等价于一个二变量微分，根据系数向量的旋度是否为零（非零），可分为两种情况：取决于该微分是否为全微分（非全微分）[ 3.8.1-3.8.2 节](3.8.3-3.8.11)；即它是否与函数的微分重合（不重合）。因此，微分的积性条件是系数向量的旋度为零[3.8.1 节]；或者在这种情况下，它是函数的微分等于任意常数，从而确定了通解。通解可以通过观察法[3.8.1 节]或通过形式积分（[3.8.2 节]）得到。

如果二变量微分是非全的，可以将其变为全微分[3.8.3 节]，并因此通过乘以积分因子来求解[3.8.4 节]；该积分因子满足一个偏微分方程[3.8.5 节]，且任何解都越简单越好。这些积分因子有无穷多个[3.8.6 节]，其中两个之比是非全微分方程的一个解。要获得非全微分的解，只需找到一个积分因子，例如：
(i) 单变量函数（[3.8.7 节]）；
(ii) 二变量的对称函数，如[3.8.8 (3.8.9)] 中的和（积）；
(iii) 两个变量之比[3.8.10 节]；或 (iv) 二变量的非对称非齐次函数[3.8.11 节]。

### 3.8.1 旋度为零的系数向量

显式 (3.9a) 一阶微分方程可以写为二变量微分 (3.145b)：

```
$$\tilde{X} = X(x,y)dx+Y(x,y)dy = \tilde{X} \cdot dx,$$
```

即之前考虑的微分方程（3.1–3 节）是正于向量场 (3.145a) 的平面曲线的 (3.145b) 类型（图 3.6）的实例。如果它与可微函数 (3.146a) 的微分 (3.146b) 重合，则它是全微分（标准 LXVI）：

```
$$\Phi \in D(|R^2|); \quad 0=d\Phi= \frac{\partial \Phi}{\partial x}dx+\frac{\partial \Phi}{\partial y}dy; \quad \Phi(x,y)=C$$
```

在这种情况下，通过将函数等于任意常数 (3.146c) 得到通积分。(3.145b) 为全微分的必要条件是存在可微函数 $\Phi$ 使得 (3.145b) $\equiv$ (3.146b)，这意味着该向量场提供了其全微分 (3.147a) $\equiv$ (3.147b, c)：

$\tilde{X} = \nabla\Phi; \quad X = \frac{\partial\Phi}{\partial x}, \quad Y = \frac{\partial\Phi}{\partial y}. \quad (3.147a–c)$

如果函数具有连续的二阶导数 (3.148a)，则交叉导数相等 (3.148b)，从而导致全微分 (3.145b) 的**积性条件** (3.148c)：

$\Phi \in C^2(R^2); \quad \frac{\partial^2\Phi}{\partial x\partial y} - \frac{\partial^2\Phi}{\partial y\partial x} = 0 \Rightarrow \Omega = \frac{\partial Y}{\partial x} - \frac{\partial X}{\partial y} = 0. \quad (3.148a–c)$

条件 (3.148a–c) 等于：

$\tilde{X} \in C^1(R^2); \quad 0 = \nabla\tilde{X} = \left( \frac{\partial Y}{\partial x} - \frac{\partial X}{\partial y} \right) \vec{z} = \Omega, \quad (3.149a, b)$

系数向量 (3.145a) 可微 (3.149a) 且旋度为零的陈述。

积性条件 (3.148a–c) $\equiv$ (3.149a, b) 是必要也是充分的，即如果满足 (3.149b)，则 (3.145b) 是全微分。

![](img/6a4cb3bd142917bb79c4b64251c_59.png)
**图 3.6**
平面曲线族可以通过其切线（法线）指定，作为一阶二变量微分方程的[图 3.2 (3.6)]。

### 3.8 非线性微分方程与动力学系统

证明使用了斯克斯定理 (5.210a, b) $\equiv$ (3.150a)，该定理适用于由闭合曲线 (3.150b) 边界的平面区域可微向量 (3.150a)。旋度为零的积性条件 (3.149b) $\equiv$ (3.151a) 通过斯克斯定理 (3.150a) 意味着：

```
$$\tilde{X} \in C^1(|D|): \int_D(\nabla \wedge \tilde{X})dS = \int_{\partial D} \tilde{X}dx, \quad (3.150a)$$
```

从 (3.151b) 可以得出积分是全微分 (3.152) $\equiv$ (3.145b)。已经证明系数可微向量 (3.145a) 的微分 (3.145b) 为全微分 (LXVI) 的充分充分条件是旋度为零 (3.149b) $\equiv$ (3.153c)：

```
$$X,Y \in C^1(|R^2|): \quad 0=Xdx+Ydy=d\Phi \Leftrightarrow \Omega = \frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}=0 \Leftrightarrow \Phi(x,y)=C; \quad (3.153a-d)$$
```

在这种情况下，通积分通过等于任意常数 (3.153d) 指定，它是二阶可微的 (3.148a)。例如，方程 (3.154a)：

```
$$0=2y^3dx+3x^2dy=d(x^2y^3), \quad x^2y^3=C, \quad (3.154a, b)$$
```

具有通积分 (3.154b)。可以检查微分 (3.154a) $\equiv$ (3.155b) 的系数 (3.155a)：

```
$$X=2y^3, \quad Y=3x^2: \quad \frac{\partial Y}{\partial x}=6xy^2=\frac{\partial X}{\partial y}, \quad (3.155a-c)$$
```

满足积性条件 (3.148c) $\equiv$ (3.155c)。

### 3.8.2 全微分的形式积分

在无法观察 (LXVI) 方程 (3.145b) 识别积分 (3.146b, c) 的情况下，可以通过形式积分 (3.147b, c) 得到。(3.147b) 的积分导致了 (3.156a)：

```
$$\Phi(x,y) = \int X(x,y)dx+u(y) = \int Y(x,y)dy+v(x), \quad (3.156a)$$
```

涉及任意函数 $u(y)$ $[v(x)]$，该函数通过在 (3.147c) 中代入 (3.157a) 得到：

```
$$\frac{du}{dy} = \frac{\partial \Phi}{\partial y} - \frac{\partial X}{\partial y} = Y - \frac{\partial X}{\partial y}, \quad \frac{dv}{dx} = \frac{\partial \Phi}{\partial x} - \frac{\partial Y}{\partial x} = X - \frac{\partial Y}{\partial x}.$$
```

因此，如果微分 (3.145b) 是全 (3.147b, c)，其通积分 (3.146c) 可以从包含 (3.157a) 的任意函数 $u(y)$ $[v(x)]$ 的积分求法 (3.156a) 得到。

例如，一阶微分方程或二变量微分：

```
$$y \log ye^x(1+x)dx+xe^x(1+\log y)dy=0, \quad (3.158)$$
```

具有 (3.145b) 系数：

```
$$X = y \log ye^x(1+x), \quad Y = xe^x(1+\log y), \quad (3.145b)$$
```

显示它满足积性条件 (3.148c)：

```
$$\frac{\partial Y}{\partial x}=6xy^2=\frac{\partial X}{\partial y}, \quad (3.149a)$$
```

因此是全微分。积分 (3.146b) 由 (3.156) 给出：

```
$$\Phi(x,y) = \int X(x,y)dx+u(y) = \int Y(x,y)dy+v(x), \quad (3.156a)$$
```

其中函数 $u(y)$ 满足 (3.157a)：

```
$$\frac{du}{dy} = \frac{\partial \Phi}{\partial y} - \frac{\partial X}{\partial y} = Y - \frac{\partial X}{\partial y}, \quad \frac{dv}{dx} = \frac{\partial \Phi}{\partial x} - \frac{\partial Y}{\partial x} = X - \frac{\partial Y}{\partial x}.$$
```

因此，通积分 (3.146c) 为 (3.159)：

```
$$\Phi(x,y)=C$$
```

### 3.8.3 全微分与非全微分之间的变换

微分 (3.145b) 的解在乘以任意函数时保持不变；这种乘可能会将全微分变为非全微分，如果 (X,Y) 不满足积性条件 (3.148c)，那么通常 (X,Y) 不满足；反之总是可能的，即如果 (X,Y) 不满足积性条件 (3.148c)，可以找到一个函数 $\lambda$ 使得 (X,Y) 满足。

