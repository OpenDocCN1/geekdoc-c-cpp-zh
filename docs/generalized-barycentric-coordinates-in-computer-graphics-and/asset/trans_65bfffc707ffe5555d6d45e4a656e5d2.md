

一种将重心插值方案扩展到单连通非凸域的简单方法在[200]中提出。处理非凸域的更简单方法在[251]中建议。我们将在3.2节末尾简要讨论这两种方法。

## 3.2 WEIGHTED MEAN VALUE INTERPOLATION

## 3.2 加权平均值插值

### 3.2.1 General construction

### 3.2.1 一般构造

Let us start from the transfinite mean value interpolation scheme proposed in [217]. Let \(\Omega\) be a bounded convex domain and \(\mathbf{x}\) be a point inside \(\Omega\). Consider the unit sphere \(S_z\) centered at \(\mathbf{x}\) and assume that \(S_z\) is parameterized by its outer unit normal \(e_\rho\). Let \(\mathbf{y}\) be a point on \(\partial\Omega\) and \(\rho = \|\mathbf{x} - \mathbf{y}\|\). Denote by \(\mathbf{z}\) the intersection point between the ray \([\mathbf{x}, \mathbf{y})\) and \(S_z\) (see Figure 3.1, left). If we assume that we know the values of the function \(u\) on \(\partial\Omega\) and at \(\mathbf{x}\), then we can estimate \(u(\mathbf{z})\) using linear interpolation,

让我们从[217]中提出的超有限平均值插值方案开始。设\(\Omega\)为有界凸域，\(\mathbf{x}\)为\(\Omega$内部的一点。考虑以\(\mathbf{x}$为中心的单位球\(S_z$，并假设\(S_z$由其外单位法线\(e_\rho$参数化。设\(\mathbf{y}$为\(\partial\Omega$上的一点，\(\rho = \|\mathbf{x} - \mathbf{y}\|$。用\(\mathbf{z}$表示射线\([\mathbf{x}, \mathbf{y})\)与\(S_z$的交点（见图3.1，左）。如果假设我们知道函数\(u$在\(\partial\Omega$和\(\mathbf{x}$处的值，则可以使用线性插值来估计\(u(\mathbf{z})$，

```
\(u(\mathbf{z}) \approx \frac{(\rho - 1)u(\mathbf{x}) + u(\mathbf{y})}{\rho}.\)
```

Now, applying S-averaging (circular averaging in the 2D case and spherical averaging in the 3D case) to the left and right sides of the above equation yields

现在，对上述等式左右两边应用S-平均（2D情况下的圆形平均和3D情况下的球形平均）得到

```
\(\int_{S_z} u(\mathbf{z}) d\theta = |S_z|u(\mathbf{x}) - u(\mathbf{x}) \int_{S_z} \frac{d\theta}{\|\mathbf{x} - \mathbf{y}\|} + \int_{S_z} \frac{u(\mathbf{y})d\theta}{\|\mathbf{x} - \mathbf{y}\|}.\)
```

where \(d\theta\) is the area element of the unit sphere \(S_z\) at \(\mathbf{z} \in S_z\) (to distinguish the 2D case we denote the angular element of the unit circle by \(d\theta\)), and \(|S_z|\) is the unit sphere area. Assuming that \(u\) is harmonic, we arrive at the transfinite mean value interpolation scheme

其中\(d\theta$是单位球\(S_z$在\(\mathbf{z} \in S_z$处的面积元素（为区分2D情况，我们用\(d\theta$表示单位圆的角元素），\(|S_z|$是单位球面积。假设\(u$是调和函数，我们得到超有限平均值插值方案

```
\(u(\mathbf{x}) = \int_{S_z} \frac{u(\mathbf{y})d\theta}{\|\mathbf{x} - \mathbf{y}\|} \Big/ \int_{S_z} \frac{d\theta}{\|\mathbf{x} - \mathbf{y}\|}.\) (3.4)
```

It is interesting that instead of mimicking the mean value property of harmonic functions we can derive (3.4) from the simple observation that the spherical (circular

![](img/4913dd83a2a14bc205a0a92cce102c82_65_0.png)

Figure 3.1 Left: notation used to define weighted mean value interpolation. Right: if \(\Omega\) is non-convex, then the rays emitted from \(\mathbf{x} \in \Omega\) may intersect \(\partial\Omega\) in multiple points.

in the 2D case) mean of all the directional derivatives of a given smooth function is equal to zero. Now, approximating the directional derivative of \(u\) in the direction of the ray \([x, y)\) by \((u(y) - u(x))/\|y - x\|\) and averaging with respect to all directions yields

有趣的是，我们不必模仿调和函数的平均值性质，而是可以从一个简单的观察中推导出(3.4)，即给定光滑函数的所有方向导数的球形（圆形

![](img/4913dd83a2a14bc205a0a92cce102c82_65_0.png)

图3.1 左：定义加权平均值插值所用的符号。右：如果\(\Omega$是非凸的，则从\(\mathbf{x} \in \Omega$发出的射线可能与\(\partial\Omega$在多个点相交。

在2D情况下）的平均值为零。现在，将\(u$在射线\([x, y)$方向上的方向导数近似为\((u(y) - u(x))/\|y - x\|$，并对所有方向求平均，得到

\(\int_{S_x} \frac{u(y) - u(x)}{\|x - y\|} d\theta = 0,\)

which is equivalent to (3.4).

这与(3.4)等价。

The interpolation scheme (3.4) allows for a natural generalization

插值方案(3.4)允许自然推广

\(u(x) = \int_{S_x} \frac{u(y)\omega(x, e_\theta)}{\|x - y\|} d\theta \big/ \int_{S_x} \frac{\omega(x, e_\theta)}{\|x - y\|} d\theta, \quad (3.5)\)

where \(\omega(x, e_\theta)\) is a weighting function that may depend on the interpolated location \(x\) and the direction \(e_\theta\). It is easy to see that (3.5) is just another form of (3.3) and we can also consider (3.5) as a transfinite version of the basic Shepard interpolation [354].

其中\(\omega(x, e_\theta)$是一个权函数，可能取决于插值位置\(x$和方向\(e_\theta$。可以看出(3.5)只是(3.3)的另一种形式，我们也可以将(3.5)视为基本Shepard插值[354]的超有限版本。

Let us check when (3.5) satisfies the linear precision property (3.2). Setting \(u(x) \equiv x\) yields \(u(y) \equiv y = x + p e_\theta\). Substituting the latter into (3.5) gives

让我们检查(3.5)何时满足线性精度性质(3.2)。设\(u(x) \equiv x$得到\(u(y) \equiv y = x + p e_\theta$。将后者代入(3.5)得到

\(0 = \int_{S_x} e_\theta \omega(x, e_\theta) d\theta \quad \forall x \in \Omega, \quad (3.6)\)

which is necessary and sufficient for linear precision. One can see that (3.6) is satisfied, if the weighting function is centrally symmetric and coincides at each pair of antipodal points,

这是线性精度的必要且充分条件。可以看出，如果权函数是中心对称的，并且在每对对极点处重合，则满足(3.6)，

\(\omega(x, e_\theta) = \omega(x, -e_\theta).\)

Consider now the case of planar interpolation with \(d = 2\) and \(e_\theta = (\cos \theta, \sin \theta)\),

现在考虑平面插值的情况，\(d = 2$和\(e_\theta = (\cos \theta, \sin \theta)$，

\(u(x) = \int_0^{2\pi} \frac{u(y)\omega(x, \theta)}{\|x - y\|} d\theta \big/ \int_0^{2\pi} \frac{\omega(x, \theta)}{\|x - y\|} d\theta. \quad (3.7)\)

Then, (3.6) becomes

那么，(3.6)变为

\(\int_0^{2\pi} \omega(x, \theta) \cos \theta d\theta = 0 = \int_0^{2\pi} \omega(x, \theta) \sin \theta d\theta \quad \forall x \in \Omega. \quad (3.8)\)

If \(\omega(x, \theta)\) satisfies (3.8), then by using the Fourier series expansion

如果\(\omega(x, \theta)$满足(3.8)，则通过使用傅里叶级数展开

\(\omega(x, \theta) = \sum c_n(x) e^{in\theta}, \quad i = \sqrt{-1},\)

it is easy to show that there exists \(p(x, \theta)\) such that

可以很容易地证明存在\(p(x, \theta)$使得

\(p''_{\theta\theta}(x, \theta) + p(x, \theta) = \omega(x, \theta). \quad (3.9)\)

Here and below we often use prime-notations for the first- and second-order derivatives with respect to \(\theta\):

下文中我们经常使用关于\(\theta$的一阶和二阶导数的素号表示法：

\((\cdot)'_\theta \text{ stands for } \frac{d}{d\theta}(\cdot) \text{ and } (\cdot)''_{\theta\theta} \text{ stands for } \frac{d^2}{d\theta^2}(\cdot).\)

The orthogonality condition (3.8) can be verified by simple integration by parts,

正交性条件(3.8)可以通过简单的分部积分验证，

```
\(\int_0^{2\pi} \omega(x, \theta)e^{il\theta} d\theta = \int_0^{2\pi} \left( \frac{\partial^2}{\partial \theta^2} p + p \right) e^{il\theta} d\theta = \int_0^{2\pi} p(x, \theta) \left( \frac{\partial^2}{\partial \theta^2} e^{il\theta} + e^{il\theta} \right) d\theta = 0.\)
```

Representation (3.9) has an interesting geometric interpretation. Given a curve \(\Sigma\) and a point \(x\), the geometry of \(\Sigma\) is determined by its support function \(p(x, \theta)\), the signed distance from \(x\) to the tangents of \(\Sigma\). The support function satisfies the second-order differential equation

表示式(3.9)有一个有趣的几何解释。给定一条曲线\(\Sigma$和一点\(x$，\(\Sigma$的几何由其支撑函数\(p(x, \theta)$确定，即从\(x$到\(\Sigma$切线的有向距离。支撑函数满足二阶微分方程

```
\(p''_\theta + p = R(\theta) \equiv 1/k(\theta),\)
```

where \(k(\theta)\) is the curvature of \(\Sigma\) and \(R(\theta)\) is the radius of curvature of \(\Sigma\). See, for example, [345] for details.

其中\(k(\theta)$是\(\Sigma$的曲率，\(R(\theta)$是\(\Sigma$的曲率半径。详情见，例如，[345]。

Now we can interpret (3.9) as follows. Each \(x \in \Omega\) defines a closed curve \(\Sigma_x\) with radius of curvature \(R = \omega(x, \theta)\). The orthogonality condition (3.8) then corresponds to

现在我们可以这样解释(3.9)。每个\(x \in \Omega$定义一个曲率半径为\(R = \omega(x, \theta)$的闭曲线\(\Sigma_x$。正交性条件(3.8)对应于

```
\(\int_0^{2\pi} n R d\theta \equiv \int_{\Sigma_x} n dl = 0,\)
```

where \(n = (\cos \theta, \sin \theta)\) is the outer unit normal of \(\Sigma_x\) and \(l\) denotes the arc-length parametrization of \(\Sigma_x\). For example, \(\Sigma_x\) is a unit circle for the 2D transfinite mean value coordinates and it is a unit sphere in \(\mathbb{R}^3\) for the three-dimensional transfinite mean value coordinates.

其中\(n = (\cos \theta, \sin \theta)$是\(\Sigma_x$的外单位法线，\(l$表示\(\Sigma_x$的弧长参数化。例如，\(\Sigma_x$是2D超有限平均值坐标的单位圆，而对于三维超有限平均值坐标，它是\(\mathbb{R}^3$中的单位球。

If \(\Omega\) is not convex, then a ray emitted from \(x \in \Omega\) may intersect \(\partial \Omega\) in multiple points (see Figure 3.1, right). One way to cope with this situation is proposed in [200] and consists of using alternating signs for intersection points. For instance, the example shown in the right image of Figure 3.1 leads to

如果\(\Omega$不是凸的，则从\(x \in \Omega$发出的射线可能与\(\partial\Omega$在多个点相交（见图3.1，右）。处理这种情况的一种方法在[200]中提出，即为交点使用交替符号。例如，图3.1右图所示的例子导致

```
\(\frac{u(y_1)}{\|x - y_1\|} - \frac{u(y_2)}{\|x - y_2\|} + \frac{u(y_3)}{\|x - y_3\|}\)
```

instead of \(u(y)/\|x - y\|\) in (3.5). However, in practice it is often better to follow a simpler approach suggested in [251] and consider only the first intersections: \(u(y_1)/\|x - y_1\|\) instead of \(u(y)/\|x - y\|\) in (3.5). For example, we use such a simplification in our numerical experiments with the so-called Gordon-Wixom coordinates and their extensions (see Section 3.3 and Figure 3.4).

而不是(3.5)中的\(u(y)/\|x - y\|$。然而，在实践中，通常遵循[251]中建议的更简单方法更好，即仅考虑第一个交点：(3.5)中的\(u(y_1)/\|x - y_1\|$而不是\(u(y)/\|x - y\|$。例如，我们在所谓的Gordon-Wixom坐标及其扩展的数值实验中使用这种简化（参见3.3节和图3.4）。

### 3.2.2 Transfinite three-point coordinates

### 3.2.2 超有限三点坐标

A general construction for discrete three-point coordinates (see Section 1.2.4) was introduced in [149]. Let \(A(x, y, z)\) denote the signed area of the triangle formed by points \(x\), \(y\), and \(z\). Given a convex polygon with vertices \(v_1, v_2, \dots, v_n\), and some point \(x\) inside the polygon, consider the signed triangle areas \(A_i(x) = A(x, v_i, v_{i+1})\) and \(B_i(x) = A(x, v_{i-1}, v_{i+1})\). Then, according to [149], the three-point coordinates are given by the weights

离散三点坐标的一般构造（参见1.2.4节）在[149]中引入。设\(A(x, y, z)$表示由点\(x$、\(y$和\(z$形成的三角形的有向面积。给定一个具有顶点\(v_1, v_2, \dots, v_n$的凸多边形和多边形内部的某一点\(x$，考虑有向三角形面积\(A_i(x) = A(x, v_i, v_{i+1})$和\(B_i(x) = A(x, v_{i-1}, v_{i+1})$。然后，根据[149]，三点坐标由以下权重给出

```
\(w_i = \frac{F(r_{i+1})A_{i-1} - F(r_i)B_i + F(r_{i-1})A_i}{A_{i-1}A_i},\) (3.10)
```

where \( r_i = \|\boldsymbol{x} - \boldsymbol{v}_i\| \) and \( F(r) \) is an arbitrary function. Following [149], one can also rewrite (3.10) as

其中\(r_i = \|\boldsymbol{x} - \boldsymbol{v}_i\|$和\(F(r)$是任意函数。遵循[149]，还可以将(3.10)改写为

```
\( w_i = \frac{2}{r_i} \left( \frac{f(r_{i+1}) - f(r_i) \cos \theta_i}{\sin \theta_i} + \frac{f(r_{i-1}) - f(r_i) \cos \theta_{i-1}}{\sin \theta_{i-1}} \right), \quad (3.11) \)
```

where \( f(r) = F(r)/r \) and \( \theta_i \) is the angle between the rays \( [\boldsymbol{x}, \boldsymbol{v}_i] \) and \( [\boldsymbol{x}, \boldsymbol{v}_{i+1}] \). Assuming that \( f(r) \) is sufficiently smooth, the number of vertices of the polygon tends to infinity, and all \( \theta_i \) uniformly tend to zero, \( \theta_i \approx d\theta \to 0 \), we then have

其中\(f(r) = F(r)/r$和\(\theta_i$是射线\([\boldsymbol{x}, \boldsymbol{v}_i]$和\([\boldsymbol{x}, \boldsymbol{v}_{i+1}]$之间的角。假设\(f(r)$足够光滑，多边形顶点数趋于无穷，且所有\(\theta_i$一致趋于零，\(\theta_i \approx d\theta \to 0$，则我们有

```
\(\frac{f(r_{i+1}) - f(r_i) \cos \theta_i}{\sin \theta_i} \approx \left[ f(p(\theta))'_{\theta} + f(r_i) \frac{\theta_i}{2} \right]_{p=r_{i+1}}, \quad \frac{f(r_{i-1}) - f(r_i) \cos \theta_{i-1}}{\sin \theta_{i-1}} \approx \left[ -f(p(\theta))'_{\theta} + f(r_i) \frac{\theta_{i-1}}{2} \right]_{p=r_i},\)
```

hence (3.11) is approximately equal to

因此(3.11)近似等于

```
\(\left[ \frac{2}{\rho} \left( f(p(\theta))''_{\theta\theta} + f(p(\theta)) \right) \right]_{p=r_i} d\theta.\)
```

This implies that the continuous or transfinite version of the three-point coordinates is described by (3.7) with

这意味着三点坐标的连续或超有限版本由(3.7)描述，其中

```
\(\omega(\boldsymbol{x}, \theta) = f(p(\theta))''_{\theta\theta} + f(p(\theta)). \quad (3.12)\)
```

### 3.2.3 Transfinite Laplace coordinates

### 3.2.3 超有限拉普拉斯坐标

Following [37, 94], let us define transfinite Laplace coordinates as the continuous version of discrete harmonic coordinates [309] (see Section 1.2.2), which are used widely in computational mechanics [375]. As discrete harmonic coordinates correspond to (3.10) with \( F(r) = r^2 \), their continuous version is given by (3.7) with the weight (3.12), where \( f(r) = r \). In other words,

遵循[37, 94]，让我们将超有限拉普拉斯坐标定义为离散调和坐标[309]（参见1.2.2节）的连续版本，后者在计算力学[375]中广泛使用。由于离散调和坐标对应于\(F(r) = r^2$的(3.10)，其连续版本由(3.7)给出，权重为(3.12)，其中\(f(r) = r$。换句话说，

```
\(\omega(\boldsymbol{x}, \theta) = p''_{\theta\theta} + p. \quad (3.13)\)
```

It turns out that (3.13) can also be derived by mimicking the Dirichlet energy minimization property of harmonic functions [37, 346]. Given \( u(\boldsymbol{y}) \), defined for each \( \boldsymbol{y} \in \partial\Omega \), let us choose \( \boldsymbol{x} \in \Omega \) and assume that \( u(\boldsymbol{x}) \) is known. Consider a ruled surface patch generated by straight segments connecting the inner point \( (\boldsymbol{x}, u(\boldsymbol{x})) \) with the boundary points \( (\boldsymbol{y}, u(\boldsymbol{y})) \). Now the value \( u(\boldsymbol{x}) \) is defined such that the Dirichlet energy of the constructed ruled surface attains its minimal value.

结果表明，(3.13)也可以通过模仿调和函数的狄里克莱能量最小化性质[37, 346]来推导。给定对每个\(\boldsymbol{y} \in \partial\Omega$定义的\(u(\boldsymbol{y})$，让我们选择\(\boldsymbol{x} \in \Omega$并假设\(u(\boldsymbol{x})$已知。考虑由连接内点\((\boldsymbol{x}, u(\boldsymbol{x}))$与边界点\((\boldsymbol{y}, u(\boldsymbol{y}))$的直线段生成的决面片。现在，\(u(\boldsymbol{x})$的值被定义为使构造的决面的狄里克莱能量达到最小值。

Let \( (r, \theta) \) be the polar coordinates centered at \( \boldsymbol{x} \). Then \( \partial\Omega \) is described by \( r = \rho(\theta) \). The ruled surface associated with \( \boldsymbol{x} \) is given by

设\((r, \theta)$为以\(\boldsymbol{x}$为中心的极坐标。那么\(\partial\Omega$由\(r = \rho(\theta)$描述。与\(\boldsymbol{x}$相关的决面由

```
\( U_{\boldsymbol{x}}(\boldsymbol{z}) = \frac{(\rho - r)u(\boldsymbol{x}) + ru(\boldsymbol{y})}{\rho},\)
```

