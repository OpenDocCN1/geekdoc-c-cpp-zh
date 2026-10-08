

现在观察到

$$\mathbb { E } ( { \boldsymbol { \delta \varepsilon } } ^ { T } ) = \mathbb { E } ( { \boldsymbol { \varepsilon } } { \boldsymbol { \delta } } ^ { T } ) = \mathbf { 0 }$$

以及

$$\mathbb { E } ( { \boldsymbol { \delta \delta } } ^ { T } ) = \mathbb { E } ( { \boldsymbol { \varepsilon } } { \boldsymbol { \varepsilon } } ^ { T } ) = \sigma ^ { 2 } \mathbf { I } ,$$

且我们有 $\hat { \mathbf { U } } ^ { 2 } + \hat { \mathbf { V } } ^ { 2 } = \mathbf { I }$，因此在一阶近似下

$$\begin{array} { c } \mathbb { E } [ ( \Delta \hat { \mathbf { O } } ) ( \Delta \hat { \mathbf { O } } ) ^ { T } ] = \sigma ^ { 2 } ( \mathbf { W } ^ { T } \mathbf { W } ) ^ { - 1 } \mathbf { W } ^ { T } \mathbf { W } ( \mathbf { W } ^ { T } \mathbf { W } ) ^ { - 1 } \\ = \sigma ^ { 2 } ( \mathbf { W } ^ { T } \mathbf { W } ) ^ { - 1 } , \end{array}$$

其中未包含高阶（$\sigma ^ { 4 }$ 阶）项。公式 (7.6) 在统计学界是众所周知的。首先，它是更一般公式 (6.37) 的一个特例，该公式见 Fullér 的著作 [66] 中的定理 3.2.1。其次，(7.6) 由 Kanatani [96] 和其他人 [42] 通过较不直接的方法显式推导得出。

### 几何圆拟合的偏差。

现在我们将进行二阶误差分析，这在统计文献中以前未曾做过。根据一般公式 (6.18)，我们设

$$\begin{array} { c } { a = \tilde { a } + \Delta _ { 1 } a + \Delta _ { 2 } a + \mathcal { O } _ { P } ( \sigma ^ { 3 } ) , } \\ { b = \tilde { b } + \Delta _ { 1 } b + \Delta _ { 2 } b + \mathcal { O } _ { P } ( \sigma ^ { 3 } ) , } \\ { R = \tilde { R } + \Delta _ { 1 } R + \Delta _ { 2 } R + \mathcal { O } _ { P } ( \sigma ^ { 3 } ) . } \end{array}$$

这里 $\Delta _ { 1 } a$ , $\Delta _ { 1 } b$ , $\Delta _ { 1 } R$ 是 $\varepsilon _ { i }$ 和 $\delta _ { i }$ 的线性组合，它们在上面 (7.5) 中已求得；而 $\Delta _ { 2 } a$ , $\Delta _ { 2 } b$ , $\Delta _ { 2 } R$ 是 $\varepsilon _ { i }$ 和 $\delta _ { i }$ 的二次型，将在接下来确定。

将距离 $d _ { i }$ 展开至二阶项得到

$$\begin{array} { c } { d _ { i } = \bar { u } _ { i } ( \delta _ { i } - \Delta _ { 1 } a ) + \bar { v } _ { i } ( \varepsilon _ { i } - \Delta _ { 1 } b ) - \Delta _ { 1 } R } \\ { - \bar { u } _ { i } \Delta _ { 2 } a - \bar { v } _ { i } \Delta _ { 2 } b - \Delta _ { 2 } R } \\ { + \frac { \bar { v } _ { i } ^ { 2 } } { 2 \tilde { R } } ( \delta _ { i } - \Delta _ { 1 } a ) ^ { 2 } + \frac { \bar { u } _ { i } ^ { 2 } } { 2 \tilde { R } } ( \varepsilon _ { i } - \Delta _ { 1 } b ) ^ { 2 } } \\ { - \frac { \bar { u } _ { i } \bar { v } _ { i } } { \tilde { R } } ( \delta _ { i } - \Delta _ { 1 } a ) ( \varepsilon _ { i } - \Delta _ { 1 } b ) . } \end{array}$$

由于我们已经求出了 $\Delta _ { 1 } a$ , $\Delta _ { 1 } b$ , $\Delta _ { 1 } R$，唯一的未知量是 $\Delta _ { 2 } a$ , $\Delta _ { 2 } b$ , $\Delta _ { 2 } R$。最小化 $\sum d _ { i } ^ { 2 }$ 现在等价于最小化

$$\sum _ { i = 1 } ^ { n } ( \bar { u } _ { i } \Delta _ { 2 } a + \bar { v } _ { i } \Delta _ { 2 } b + \Delta _ { 2 } R - f _ { i } ) ^ { 2 } ,$$

其中

$$\begin{array} { c } { f _ { i } = \bar { u } _ { i } ( \delta _ { i } - \Delta _ { 1 } a ) + \bar { v } _ { i } ( \varepsilon _ { i } - \Delta _ { 1 } b ) - \Delta _ { 1 } R } \\ { + \frac { \bar { v } _ { i } ^ { 2 } } { 2 \tilde { R } } ( \delta _ { i } - \Delta _ { 1 } a ) ^ { 2 } + \frac { \bar { u } _ { i } ^ { 2 } } { 2 \tilde { R } } ( \varepsilon _ { i } - \Delta _ { 1 } b ) ^ { 2 } } \\ { - \frac { \bar { u } _ { i } \bar { v } _ { i } } { \tilde { R } } ( \delta _ { i } - \Delta _ { 1 } a ) ( \varepsilon _ { i } - \Delta _ { 1 } b ) . } \end{array}$$

这是另一个经典的**最小二乘**问题，其解为

\begin{equation}
\Delta_2\boldsymbol{\hat{\Theta}} = \left(\mathbf{W}^T\mathbf{W}\right)^{-1}\mathbf{W}^T\mathbf{F}, \tag{7.8}
\end{equation}

其中 $\mathbf{F} = (f_1, \ldots, f_n)^T$；当然，这是一个二次近似，不包含 $\varrho_B(\sigma^2)$ 项。事实上，(7.7) 中前三项（线性项）的贡献消失，这是完全可以预见的；因此只有最后两项（二次项）起作用。

取均值得到，在一阶近似下，

\begin{equation}
\mathbb{E}(\Delta\boldsymbol{\hat{\Theta}}) = \mathbb{E}(\Delta_2\boldsymbol{\hat{\Theta}}) \equiv \frac{\sigma^2}{2R}\left[\left(\mathbf{W}^T\mathbf{W}\right)^{-1}\mathbf{W}^T\mathbf{1} + \left(\mathbf{W}^T\mathbf{W}\right)^{-1}\mathbf{W}^T\mathbf{S}\right], \tag{7.9}
\end{equation}

其中 $\mathbf{1} = (1, 1, \ldots, 1)^T$ 且 $\mathbf{S} = (s_1, \ldots, s_n)^T$，这里 $s_i$ 是由以下公式给出的标量：

$$s_i = [-\tilde{v}_i, \tilde{u}_i, 0](\mathbf{W}^T\mathbf{W})^{-1}[-\tilde{v}_i, \tilde{u}_i, 0]^T.$$

(7.9) 中的第二项是 $\varrho(\sigma^2/n)$ 阶的，因此**本质偏差**仅由第一项给出：

$$\mathbb{E}(\Delta\boldsymbol{\hat{\Theta}}) \stackrel{\text{ess}}{=} \frac{\sigma^2}{2R}(\mathbf{W}^T\mathbf{W})^{-1}\mathbf{W}^T\mathbf{1}.$$

事实上，这个表达式可以简化。由于矩阵 $\mathbf{W}^T\mathbf{W}$ 的最后一列与向量 $\mathbf{W}^T\mathbf{1}$ 重合，我们有 $(\mathbf{W}^T\mathbf{W})^{-1}\mathbf{W}^T\mathbf{1} = [0, 0, 1]^T$；因此几何圆拟合的本质偏差为

\begin{equation}
\mathbb{E}(\Delta\boldsymbol{\hat{\Theta}}) \stackrel{\text{ess}}{=} \frac{\sigma^2}{2R} \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}. \tag{7.10}
\end{equation}

相同的结果也可以从一般公式 (6.39) 得到。因此，圆心的估计值 $\hat{a}$ 和 $\hat{b}$ *没有本质偏差*，而半径的估计值具有本质偏差

\begin{equation}
\mathbb{E}(\Delta\hat{R}) \stackrel{\text{ess}}{=} \frac{\sigma^2}{2R}, \tag{7.11}
\end{equation}

这与真实点的数量和位置无关。

## 7.2 圆拟合的 Cramer-Rao 下界

在这里，我们推导圆参数估计量协方差矩阵的经典下界。这是一个相当标准的工作，我们只需遵循第 2.8 节的思路。Zelniker 和 Clarkson 最近的一篇论文中也包含了类似的分析 [196]。

我们在笛卡尔函数模型的情境下进行工作，其中存在 \(n+3\) 个独立参数：三个主要参数 \((a, b, R)\) 以及每个数据点的一个“潜在”参数。

首先，我们通过以下公式指定真实点的坐标：

$$\tilde{x}_{i}=\tilde{\boldsymbol{a}}+\tilde{R} \cos \varphi_{i}, \quad \tilde{y}_{i}=\tilde{\boldsymbol{a}}+\tilde{R} \sin \varphi_{i}$$

其中 \(\varphi_{1}, \ldots, \varphi_{n}\) 是潜在参数（回顾一下，我们在第 4.8 节中使用过这种形式）。现在，在标准假设下（如第 6.1 节所述的笛卡尔函数模型），对数似然函数为

$$\ln L=\text { const }-\frac{1}{2 \sigma^{2}} \sum_{i=1}^{n}\left(x_{i}-\tilde{x}_{i}\right)^{2}+\left(y_{i}-\tilde{y}_{i}\right)^{2}. \qquad(7.12)$$

根据经典的 Cramer-Rao 定理，无偏参数估计量的协方差矩阵下界为

$$\operatorname{Cov}\left(\hat{a}, \hat{b}, \hat{R}, \hat{\varphi}_{1}, \ldots, \hat{\varphi}_{n}\right) \geq \mathbf{F}^{-1},$$

其中 **F** 是 Fisher 信息矩阵，**F** \(=\)-**E**\((**H**)\)，**H** 表示由 \(\ln L\) 关于参数的二阶偏导数组成的 Hessian 矩阵。

计算 (7.12) 关于 \(a, b, R\) 以及 \(\varphi_{1}, \ldots, \varphi_{n}\) 的二阶偏导数是一个常规练习，我们在此省略。取它们的期望值（并使用显然的关系 \(\mathbb{E}\left(x_{i}\right)=\tilde{x}_{i}\) 和 \(\mathbb{E}\left(y_{i}\right)=\tilde{y}_{i}\)）得到以下结果（为简洁起见，我们省略公共因子 \(\sigma^{-2}\)）：

$$\begin{aligned} & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a^{2}}\right]=-n, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b^{2}}\right]=-n, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial R^{2}}\right]=-n, \\ & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial R}\right]=-\sum \cos \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial b}\right]=0, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b \partial R}\right]=-\sum \sin \varphi_{i}, \\ & \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial a \partial \varphi_{i}}\right]=R \sin \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial b \partial \varphi_{i}}\right]=-R \cos \varphi_{i}, \quad \mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial R \partial \varphi_{i}}\right]=0, \end{aligned}$$

最后

$$\mathbb{E}\left[\frac{\partial^{2} \ln L}{\partial \varphi_{i} \partial \varphi_{j}}\right]=-R^{2} \delta_{i j},$$

其中 \(\delta_{i j}\) 表示 Kronecker delta 符号。现在 Fisher 信息矩阵可以写为

$$\mathbf{F}=\boldsymbol{\sigma}^{-2}\left[\begin{array}{cc} \mathbf{K} & \mathbf{L}^{T} \\ \mathbf{L} & R^{2} \mathbf{I}_{n} \end{array}\right],$$

其中

$$\mathbf{K}=\left[\begin{array}{ccc} n & 0 & \sum \cos \varphi_{i} \\ 0 & n & \sum \sin \varphi_{i} \\ \sum \cos \varphi_{i} & \sum \sin \varphi_{i} & n \end{array}\right]$$

