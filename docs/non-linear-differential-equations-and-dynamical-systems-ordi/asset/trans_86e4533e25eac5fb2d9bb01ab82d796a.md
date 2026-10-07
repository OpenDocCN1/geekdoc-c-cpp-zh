

# 微分与一阶方程

那么：(i) 分量为 (3.339a, b) 的向量导致了二变量的恰当微分：(3.153b) \equiv (3.339c) \equiv (3.339d)：

```
{A,B} = \frac{\{X,Y\}}{xX+yY}: d\Phi = Adx+Bdy = \frac{Xdx+Ydy}{xX+yY}; \quad (3.339a-d)
```

(ii) 该（标准 LXXXVI）一阶微分 (3.340a) 具有积分因子 (3.340b)，该因子被 (3.340) 使用：

```
d\Psi = Xdx+Ydy = \lambda^{-1}d\Phi; \frac{1}{\lambda}=xX+yY; \quad (3.340a-c)
```

以及 (iii) 如果二变量一阶微分 (3.340a) \equiv (3.341b) 是标准（LXXVII）恰当且关于 (3.341a) 次齐次函数，则积分为 (3.341c)：

```
q\neq-1; \quad Xdx+Ydy \Rightarrow xX+yY=C. \quad (3.341a-c)
```

(3.340a–c) 的证明遵循恒等式 (3.340b, c) \equiv (3.339c, d)。为了证明 (3.341a–c)，条件 (3.341a) 是恰当微分 (3.153c) \equiv (3.342a) 已被用在 (3.342b) 中：

```
\frac{\partial X}{\partial y}-\frac{\partial Y}{\partial x} = d(xX+yY)-Xdx-Ydy = xdx+Ydy\n=x(\frac{\partial X}{\partial x}dx+\frac{\partial X}{\partial y}dy)+y(\frac{\partial Y}{\partial x}dx+\frac{\partial Y}{\partial y}dy)\n=x(\frac{\partial X}{\partial x}dx+\frac{\partial Y}{\partial x}dy)+y(\frac{\partial X}{\partial y}dx+\frac{\partial Y}{\partial y}dy)\n=x(\frac{\partial X}{\partial x}+y\frac{\partial X}{\partial y})dx+x(\frac{\partial Y}{\partial y}+x\frac{\partial Y}{\partial x})dy\n=q(Xdx+Ydy), \quad (3.342a-c)
```

随后齐次性性质 (3.334c) 被用在 (3.342c) 中。重写 (3.342c) = \equiv (3.343)：

```
d(xX+yY)=(q+1)(Xdx+Ydy), \quad (3.343)
```

由此可知，如果 (3.341a) 成立，则 (3.343) 意味着 (3.341c)：

# 非线性微分方程与动力系统

注 3.18：NN变量齐次微分

上述结果扩展到 N 变量的一阶微分：如果函数 (3.344a) 是 q 次齐次的：

```
$X_n(x_1,...,x_N) = (x_1)^q X_n\left(\frac{x_2}{x_1}, \frac{x_N}{x_1}\right) \Leftrightarrow \sum_{m=1}^n x_m \frac{\partial X_n}{\partial x_m} = qX_n; \quad (3.344a, b)$
```

从 (3.344b) 可得：(i) 该（标准 LXXXVIII）一阶微分

```
$d\Psi = \sum_{m=1}^N X_m dx_n; \quad d_n = \frac{1}{\lambda} \sum_{m=1}^N X_n dx_n; \quad (3.345a, b)$
```

具有积分因子 (3.345b)；以及 (ii) 如果一阶微分 (3.345a) 是恰当的 (3.346b) 且（标准 LXXXIX）系数向量是关于 (3.346a) 次齐次的：

```
$q \neq -1; \quad d\Phi = \sum_{n=1}^N X_n dx_n \Rightarrow \sum_{n=1}^N X_n x_n = C; \quad (3.346a-c)$
```

那么通积分为 (3.346c)。

注 3.19：二阶齐次一阶微分的积分

作为一个例子，考虑二变量一阶微分 (3.347a)，它是二阶齐次的：

```
$(x^2+y^2)dx-xy=0; \quad \frac{1}{\lambda}=x(x^2+y^2)-xy^2=x^3; \quad (3.347a, b)$
```

其积分因子为 (3.347b)。将 (3.347a) 除以 (3.347b) 得到恰当微分 (3.348a)：

```
$0 = \frac{dx}{x} + \frac{y^2}{x^3}dx - \frac{y}{x^3}dy = d\left(\log x - \frac{y^2}{x^2}\right); \quad \log x + \frac{y^2}{x^2}; \quad (3.348a, b)$
```

指定了 (3.347a) 的通积分 (3.348b)。

# 微分与一阶方程

注 3.20：-1 次齐次一阶微分的例外

一阶微分：

```
0=(x^2+y^2)dx+2xyd=d(x^2+y^2)=\Phi, \quad (3.349)
```

是二阶齐次的且恰当的；可以检查它满足积分条件 3.350：

```
\partial y(x^2+y^2)=2y=\partial x(x^2+y^2)+C, \quad (3.350a, b)
```

并且其齐次一阶微分 (3.351a)：

```
0=dx/x-dy/x=-d(y/x), y=C, \quad (3.351a, b)
```

具有通积分 (3.351b)；它与 3.352a 不一致：

```
{X,Y}={y/x,-1/x}, C=x+y=0, \quad (3.352a, b)
```

因为 3.351a 的原因是 q=-1，且定理 (3.346b) 失失效。

# 注 3.21 高阶、空间与张量

微分可以从一阶（3.8–9 及注 3.1–20）推广到具有相关性质（注 22）的高阶。高阶微分的求解方法是将其分解为低阶（注 23），例如二变量的最简单二阶微分（标准 XIX）：

```
0=A(x,y)(dx)^2+B(x,y)(dy)^2+D(x,y)dy, \quad (3.353)
```

可以作为斜率的二次方程求解：

```
0=B(x,y)y'^2+D(x,y)y'+A(x,y), \quad (3.354)
```

```
$$x^i \in C^1(R); \ \text{Det}\left(\frac{\partial x^i}{\partial x^j}\right) \neq 0; \quad dx^i = \frac{\partial x^i}{\partial x^j}dx^j. \quad (3.359a-c)$$

# 微分与一阶方程

微分 (3.357b) 是不变的；也就是说，在每个允许的坐标系（3.359a-c）中取相同的形式 (3.360)：

```
0 = X_{i_1...i_m} dx^{i_1}...dx^{i_m}, \quad (3.360)
```

仅当系数具有变换律时：

```
X_{i_1...i_m} = X_{j_1...j_m} \frac{\partial x^{j_1}}{\partial x^{i_1}}...\frac{\partial x^{j_m}}{\partial x^{i_m}}, \quad (3.361)
```

对应于在指标上对称的 M 协变张量 (3.357c)。张量计算中微分的不不变性（注 III.9.1-III.52）。

# 注 3.23：二阶微分分解

微分的考虑（注 3.1–22）将以二变量或三变量的情况结束（注 23–24）。二变量二阶微分 (3.353) = (3.362a) 总是可以分解为两个一阶微分的积 (3.363b)：

```
$0 = B(dy-\lambda_+dx)(dy-\lambda_-dx), \quad 2\lambda_{\pm}B=-D \pm\sqrt{D^2-4AB}. \quad (3.362a, b)$
```

这不是三变量二阶微分一般的例（标准 XCI）：

```
$0 = A(dx)^2 + B(dy)^2 + C(dz)^2 + 2Edxdy + 2Edxdz + 2Fdydz. \quad (3.363)
```

如果条件 (3.364a) 成立，则二阶微分 (3.363) 可以代入完全平方中 (3.364b)：

```
$C \neq 0: \quad (Cdz+Edx+Fdy)^2\n=E(dx)^2+F(dy)^2+2EFdxdy+C[C(Edx+Fdy)]\n=E(dx)^2+F(dy)^2+2EFdxdy-C[A(dx)^2+B(dy)^2+2Dedxdz]\n=(E^2-CA)(dx)^2+(F^2-BC)(dy)^2+2(EF-CD)dxdz;\n\quad (3.364a, b)$
```

因此，如果 (3.364b) 的右侧是一个完全平方 (3.365a)，则微分 (3.363) 简化为差差：

```
$0=(E^2-CA)(F^2-CB)-(EF-CD)^2; \quad ABC+2DEF-AF$
```

# 非线性微分方程与动力系统

已经证明，如果三变量二阶微分 (3.363)（标准 XCI）满足条件 (3.365b)，则它可以被写为平方差 (3.366)：

```
$(Cdz+Edx+Fdy)^2-(\sqrt{E^2 - CA}dx + \sqrt{F^2 - CB}dy)^2 = 0, \quad (3.366)$
```

因此它可以分解为两个三变量一阶微分的积 (3.367)：

```
$Cdz \pm\sqrt{E^2 - CA}dx + \sqrt{F^2 - CB}dy = 0, \quad (3.367)$
```

其解 (3.372b) 为：(i) 球在原点半径为 $\sqrt{C_{\pm}}$ 的球，它与任何过原点的平面 $\alpha x + \beta y + \lambda z = 0$ 都是圆；以及 (ii) 绕 OZ 轴的旋转双面，在 OZ 轴上截于