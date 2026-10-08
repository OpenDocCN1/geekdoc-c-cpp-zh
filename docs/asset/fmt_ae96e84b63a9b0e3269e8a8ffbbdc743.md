
丢弃对流项（我们考虑此项）并将系统重写为线性形式。

|  | j-1 | j | j+1 |
|---|---|---|---|
| i+1 |  |  | * | * |
| i |  | * |  |  |
| i-1 |  |  |  |  |

正如所示，第一列和最后一列为零。对应的气体参数将作为平均包含在方案中。因此，我们考虑六阶阶方程组：

$$\begin{array}{ccccccc} u_x & 0 & 0 & n^{-1} & 0 & 0 \\ u_y & 0 & 0 & 0 & n^{-1} & 0 \\ \frac{\partial}{\partial t} \sigma_{xx}^2 & 0 & 0 & n^{-1} & 0 & \sigma_{xy}^2 & 3\sigma^2_{xx} & \sigma^2_{xy} & 0 & 0 \\ \sigma_{xz}^2 & 2\sigma^2_{xx} & \sigma_{xz}^2 & 0 & 0 & \sigma_{xz}^2 \\ \sigma_{yz}^2 & 2\sigma_{xz}^2 & 0 & 0 & 0 & \sigma_{yz}^2 \end{array} = 0$$

方程解的形式为：

$U_x = \frac{u_x^L+u_x^R}{2} + \frac{\left[\sigma_{xx}^2\right]^L-\left[\sigma_{xx}^2\right]^R}{2} = \frac{n^L+n^R}{\sqrt{3n^L n^R\left[\sigma_{xx}^2\right]^L+\left[\sigma_{xx}^2\right]^R}}$

$U_{y,z} = \frac{u_{y,z}^L+u_{y,z}^R}{2} + \frac{\left[\sigma_{xy,xz}^2\right]^L-\left[\sigma_{xy,xz}^2\right]^R}{2} = \frac{n^L+n^R}{\sqrt{3n^L n^R\left[\sigma_{xy,xz}^2\right]^L+\left[\sigma_{xy,xz}^2\right]^R}} +$

$$\left[\sigma_{xx}^2\right]^L-\left[\sigma_{xx}^2\right]^R = \frac{n^L+n^R}{\sqrt{3n^L n^R\left[\sigma_{xx}^2\right]^L+\left[\sigma_{xx}^2\right]^R}} \cdot \frac{\left[\sigma_{xy,xz}^2\right]^L-\left[\sigma_{xy,xz}^2\right]^R}{\left[\sigma_{xy}^2\right]^L+\left[\sigma_{xy}^2\right]^R}}(\pm-\sqrt{3})
