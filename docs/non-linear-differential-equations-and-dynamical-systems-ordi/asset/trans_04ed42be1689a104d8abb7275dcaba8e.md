

## 54 非线性微分方程与动力系统

将 (3.223b) 和 (3.230b) 代入 (3.229c) 得到 (3.228a–c)。在 (3.229b) 中使用了梯度的旋度 (3.231) [标量与矢量的乘积的旋度 (3.332)] [(3.229c)]

$$\nabla(\nabla\Phi)) = e_{ijk} \partial_j\partial_k\Phi = 0,$$ (3.231)

$$\nabla(\lambda\tilde{X}) = e_{ijk} \partial_j(\lambda\tilde{X}) = e_{ijk}(\partial_j\lambda)\tilde{X} + e_{ijk}\lambda\partial_j\tilde{X} = (\nabla\lambda\cdot\tilde{X}) + \lambda(\nabla\tilde{X}),$$ (3.232)

可利用三维中的置换符号使用：

$e_{ijk} = \begin{cases} +1 & \text{if } (i,j,k) \text{ is an even permutation,} & (3.233a) \ -1 & \text{if } (i,j,k) \text{ is an odd permutation of } (1,2,3), & (3.233b) \ 0 & \text{otherwise: there are repeated indices.} & (3.233c) \end{cases}$

由 (3.229c) 可得 (3.234b)：

$$\lambda \neq 0: \quad 0=\tilde{X}.(\nabla\lambda\tilde{X})=-\lambda\tilde{X}. \Rightarrow \quad H=\tilde{X}.\tilde{\Omega}=\tilde{X}.(\nabla\tilde{X})=0,$$ (3.234a–c)

这意味着对于非零积分因子 (3.234a)，*helicity* 为零 (3.234c)。

### 3.9.3  helicity 与 Beltrami 矢量

积分因子存在的必要条件 (3.234c) = (3.235)：

$0=H=\tilde{X}.(\nabla\tilde{X})=X(\frac{\partial Z}{\partial y}-\frac{\partial Y}{\partial z})+Y(\frac{\partial X}{\partial z}-\frac{\partial Z}{\partial x})+Z(\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}),$ (3.235)

可另由 (3.228a–c) 分别乘以左端 (Z,Y,X) 并相加得到左端消失而得到。helicity 由 (3.235) 或由 (3.236a, b) 等价：

$H=\begin{array}{ccc} X & Y & Z \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ X & Y & Z \end{array}=X(\frac{\partial Z}{\partial y}-\frac{\partial Y}{\partial z})+Y(\frac{\partial X}{\partial z}-\frac{\partial Z}{\partial x})+Z(\frac{\partial Y}{\partial x}-\frac{\partial X}{\partial y}),$ (3.236a, b)

由内积 (3.234c) = (3.222a) = (3.224a)，以及 (3.223a, b) 可得。helicity 为零的矢量 (3.235) 称为 Beltrami 矢量，且 (3.234c) = (3.235) 不仅是积分因子存在的必要条件，也是充分条件 (注 3.9–3.111)。

已证明在三变量中系数矢量 (3.222a)=(3.237a) 为 (标准 LXXV) 连续可微的微分 (3.219) = (3.237b)：若旋度的 helicity 不为零 (3.237c)：

$$\hat{X} \in c^1(\mathbb{R}^3);\quad\quad\quad\nabla \wedge \hat{X} \neq 0;\quad\quad\quad\quad\quad\quad\quad(3.237a-)$

- (ii) 若 helicity 为零 (3.234c) = (3.235) = (3.238a)；即系数矢量是与其实旋度正交的 Beltrami 矢量，则存在积分因子 (3.238b)，由 (3.229c) = (3.228a-c) 的任一解给出：

$0=H=\hat{X}(\nabla \wedge \hat{X})\quad\Leftrightarrow\quad0=\lambda(\hat{X}.d\hat{X})=d\Phi\quad\quad\Phi(\hat{X})=C.\quad(3.238a-)$

(且 iii) 将微分乘以积分因子得到一般积分 (3.238c)。

### 3.9.4 三变量中的不精确、可积微分

例如，微分 (3.239a) 是不精确的，因为系数矢量 (3.239b) 的旋度非零 (3.239c)：

$0=y\dx+x\dy+xy\dz;\quad\quad\quad\hat{X}=\{y,x,xy\};\quad\quad\quad\quad(3.239a-)$

由 (3.240a) 可得：

$$\begin{array}{ccccc} \bar{e}_x & \bar{e}_y & \bar{e}_z & & \ \ \nabla \wedge \bar{X} & \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} & =\bar{e}_x x-\bar{e}_y y; \quad (\nabla \wedge \bar{X}).\bar{X}=0, \ \ y & x & xy & & \end{array} \quad(3.240a, b)$$

三维矢量场 (3.239b) 是 helicity 为零的 Beltrami 矢量 (3.240b)，因此不精确微分具有积分因子，而且事实上具有无穷多个。不精确 (3.239c) 可积 (3.240b) 的微分 (3.239a) 可化为形式 (3.241a)：

$0=d(xy)+xy\dz,\quad\quad\quad\lambda(x,y)=\frac{1}{xy},\quad\quad\quad(3.241a,)$

$y \ dx + x \ dy + xy \ dz = \frac{dx}{x} + \frac{dy}{y} + dz = d[z + \log(xy)], \quad z + \log(xy) = C,$

(3.242a, b)

并确定三变量中一般的一阶微分 (3.239a) 是精确的 (3.239b, c) 但具有 (3.240a, b) 积分因子 (3.241b)，从而得到一般积分 (3.242b)；后者确定了与矢量场 (3.239b) 正交的曲面族 (图 3.7)。若系数矢量具有非零 helicity，则不存在正交的曲面族 (小节 3.9.5–3.9.6)。

### 3.9.5 平面曲线与具有挠率的曲线

平面矢量 (3.243a) 具有正交于该平面的曲线 (3.223a, b) (3.243b)，因此 helicity 即矢量的内积为零 (3.243c)：

$\tilde{X} = \tilde{e}_x A + \tilde{e}_y B, \quad \nabla \cdot \tilde{X} = \nabla (\frac{\partial B}{\partial x} - \frac{\partial A}{\partial y}) = 0, \quad H \equiv \tilde{X}(\nabla \times \tilde{X}) = 0. \quad (3.243a–c)$

已证明平面矢量 (3.243a) 具有零 helicity (3.243c)，且二变量中的微分总是有积分因子，与小节 3.9.1 一致；几何解释 (图 3.6) 是平面中连续可微的矢量场具有正交的曲线族。helicity 是偏离平面的度量，对应于空间中具有 *挠率* 的曲线。例如，具有 (图 3.8) 常半径 $a$ 和倾角 $\alpha$ 的圆柱螺旋线具有圆柱坐标 (3.244a)：

$\tilde{X} = \tilde{e}_r a + \tilde{e}_z \sin \alpha \phi, \quad \nabla \cdot \tilde{X} = \frac{1}{a} \partial_\phi \tilde{X}_z = \alpha \sin \alpha, \quad H \equiv \tilde{X}(\nabla \times \tilde{X}) = 0.$

(3.244a–c)

对应于：(i) 圆柱坐标中旋度 (3.241b) (III.6.1) 和 (ii) 常 helicity (3.244c)。在三维中：(i) 与旋度为零的矢量场类似，微分是精确的 (通过具有积分因子而不精确)，因此存在正交的曲面族 (图 3.7)；且 (ii) 若系数矢量具有非零 helicity，因为不存在正交的曲面族。在最后一种情况下，可积性条件零 helicity 被积分函数 $\Psi$ 取代，连同积分因子 $\lambda$ 和一般积分 $\Phi$ 满足三变量中系数矢量的三个分量 (小节 3.9.6)。

## 微分与一阶方程

![](img/6a4cb3b3bd1429197bb791c4b642651c_79_0.png)

FIGURE 3.8
具有半径 $a$ 和恒定斜率 $\alpha$ 的圆柱螺旋线具有常 helicity $a \sin \alpha$。

### 3.9.6 没有积分因子的不精确微分

考虑三变量中一阶微分 (3.219) $\equiv$ (3.245b) 具有 (标准 LXXVI) 连续可微系数矢量 (3.232a) $\equiv$ (3.245a) 具有非零 helicity (3.245d) 且因此旋度非零 (3.245c)：

$$\tilde{X} \in c^1(\mathbb{R}^3): \quad \tilde{X} \cdot d\mathbf{x} = 0, \quad \nabla \times \tilde{X} \neq 0. \tilde{X} \cdot (\nabla \times \tilde{X}) = H. \quad (3.245a-d)$$

(然后) 可施加任意可微函数 (3.246a) (3.246b) 指定一个变量的微分用其他变量表示 (3.246c)：

$$\Psi(x,y,z) \in c^1(\mathbb{R}^3): \quad 0 = d\Psi = \frac{\partial \Psi}{\partial x}dx + \frac{\partial \Psi}{\partial y}dy + \frac{\partial \Psi}{\partial z}dz,$$
$dz = -\frac{\partial \Psi}{\partial z}dx - \frac{\partial \Psi}{\partial y}dy; \quad (3.246a-c)$

(ii) 将 (3.246c) 代入三变量中不精确不可积微分 (3.219) 得到二变量中的微分 (3.247a)：

$$0 = \left(X-Z\frac{\partial \Psi /\partial x}{\partial \Psi /\partial z}\right)dx+\left(Y-Z\frac{\partial \Psi /\partial y}{\partial \Psi /\partial z}\right)dy = \lambda^{-1}d\Phi, \quad \Phi(x,y,z)=C, \quad (3.247a-c)$$

