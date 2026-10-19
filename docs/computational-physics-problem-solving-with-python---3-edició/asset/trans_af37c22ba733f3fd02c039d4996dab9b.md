

这种方法的变体——*连续超松弛法*，通过放大因子 \(\omega\) 来提高残差趋零的速度：

\[
v^x_{i,j} = v^*_{i,j} + \omega r_{i,j} \quad \text{(SOR)} . \tag{25.20}
\]

当 \(\omega = 1\) 时，得到标准松弛算法 (25.18)；当 \(\omega > 1\) 时，得到加速收敛（*超松弛*）；而当 \(\omega < 1\) 时，则发生*低松弛*。人们发现，取值 \(\omega > 2\) 会导致数值不稳定。虽然需要对算法进行详细分析才能预测 \(\omega\) 的最优值，但我们建议你测试不同的 \(\omega\) 取值，看看哪一个能为你的问题提供最快的收敛速度。

### 25.2.3 连续超松弛实现

1. 修改程序 `Beam.py`，或自行编写程序，求解二维流动中流体速度的 Navier–Stokes 方程。用数组 `vx[Nx,Ny]` 和 `vy[Nx,Ny]` 表示速度的 \(x\) 和 \(y\) 分量。

2. 将你的解专门应用于图 25.2 所示的矩形区域和边界条件。

3. 使用以下参数值，
   \[
   \nu = 1\ \mathrm{m^2/s}, \quad \rho = 10^3\ \mathrm{kg/m^3}, \quad \text{(流动参数)},
   \]
   \[
   N_x = 400, \quad N_y = 40, \quad h = 1, \quad \text{(网格参数)},
   \]
   可得到解析解
   \[
   \partial P/\partial x = -12, \quad \partial P/\partial y = 0, \quad v^x = \frac{3j}{20}\left(1 - \frac{j}{40}\right), \quad v^y = 0. \tag{25.21}
   \]

4. 对于松弛法，输出迭代次数和计算得到的 \(v^x\)，然后比较解析结果与数值结果。

5. 重复计算，看看 SOR 是否能加快收敛速度。

## 25.3 梁上的二维流动

既然与解析解的比较表明我们的 CFD 模拟是有效的，我们便回到确定图 25.1 中的梁是否能为鲑鱼提供良好栖息地的问题上。虽然我们没有任何解析解可作为比较，但我们的独木舟和垂钓经历告诉我们，溪流中岩石后方常常会形成含有鱼类的*驻波*，因此我们预期在梁的后方也会形成驻波。

## 25.4 理论：Navier–Stokes 方程的涡量形式

我们已经看到了如何数值求解流体动力学方程

\[
\nabla\cdot\mathbf{v}=0,\tag{25.22}
\]

\[
(\mathbf{v}\cdot\nabla)\mathbf{v}=-\frac{1}{\rho}\nabla P+\nu\nabla^2\mathbf{v}.\tag{25.23}
\]

这些方程确定了流体的速度、压力和密度分量随位置变化的函数。类比静电学中人们通常先求解较简单的标量势，然后取其梯度来确定更复杂的矢量场，我们现在将流体动力学方程改写成便于我们求解两个关于更简单函数的更简单方程的形式，速度则通过梯度运算从这些函数中得到。

我们引入*流函数* \(u(\mathbf{x})\)，速度通过旋度算子由它确定：

\[
\mathbf{v}\equiv\nabla\times u(\mathbf{x})=\hat{\mathbf{e}}_x\left(\frac{\partial u_z}{\partial y}-\frac{\partial u_y}{\partial z}\right)+\hat{\mathbf{e}}_y\left(\frac{\partial u_x}{\partial z}-\frac{\partial u_z}{\partial x}\right).\tag{25.24}
\]

注意在我们的问题中不存在速度 \(\mathbf{v}\) 的 \(z\) 分量。由于 \(\nabla\cdot(\nabla\times\mathbf{u})=0\)，我们看到任何可以写成 \(\mathbf{u}\) 的旋度的 \(\mathbf{v}\) 都自动满足连续性方程 \(\nabla\cdot\mathbf{v}=0\)。此外，由于我们问题中的 \(\mathbf{v}\) 只有 \(x\) 和 \(y\) 分量，\(u(\mathbf{x})\) 只需有一个 \(z\) 分量：

\[
u_z\equiv u\quad\Rightarrow\quad v_x=\frac{\partial u}{\partial y},\qquad v_y=-\frac{\partial u}{\partial x}.\tag{25.25}
\]

值得指出，在二维流动中，等值线 \(u=\text{常数}\) 即为*流线*。

第二个简化函数是*涡量*场 \(\mathbf{w}(\mathbf{x})\)，它在物理上和字母上都与流体的角速度 \(\boldsymbol{\omega}\) 相关。涡量定义为速度的旋度（有时前面带负号）：

\[
\mathbf{w}\equiv\nabla\times\mathbf{v}(\mathbf{x}).\tag{25.26}
\]

由于我们问题中的速度在 \(z\) 方向不发生变化，我们有

\[
w_z=\left(\frac{\partial v_y}{\partial x}-\frac{\partial v_x}{\partial y}\right).\tag{25.27}
\]

从物理上看，涡量度量了流体速度卷曲或旋转的程度，其方向由旋转的右手³定则确定。事实上，如果我们能将流体的一个小单元提取到空间中（这样它就不会感受到流体的内应变），我们会发现它像刚体一样旋转，角速度 \(\omega \propto w\) (Lamb, 1993)。既然如此，将涡量视为流体局部角速度矢量的值是很有用的。如果 \(w = 0\)，则流动是无旋的。

³ 如果我们只需要求解较简单的*无旋流动*（无湍流）问题，那么就可以使用标量速度势，与静电学非常类似 (Lamb, 1993)。对于更一般的*有旋流动*，则需要两个矢量势。

\(w\) 的场线是连续的，并且移动时仿佛附着在流体粒子上。均匀流动的流体旋度为零，而非零涡量则表示电流（译者注：此处应为水流）卷曲回自身或发生旋转。由流函数的定义 (25.24) 可知，涡量 \(w\) 与它的关系为

\[
w = \nabla \times v = \nabla \times (\nabla \times u) = \nabla(\nabla \cdot u) - \nabla^2 u ,    \tag{25.28}
\]

这里我们对 \(\nabla \times (\nabla \times u)\) 使用了矢量恒等式。然而散度 \(\nabla \cdot u = 0\)，因为 \(u\) 只有一个 \(z\) 方向分量，且该分量与 \(z\) 无关（或者因为 \(u\) 没有源）。现在我们得到了流函数 \(u\) 与涡量 \(w\) 之间的基本关系：

\[
\nabla^2 u = -w .    \tag{25.29}
\]

方程 25.29 类似于静电学中的泊松方程 \(\nabla^2\phi = -4\pi\rho\)，只不过现在涡量 \(w\) 的每个分量都是流函数 \(u\) 相应分量的源。如果流动是无旋的，即 \(w = 0\)，那么我们只需对 \(u\) 的每个分量求解拉普拉斯方程。有旋流动具有耦合的非线性，会导致更有趣的行为。

正如从 \(w\) 的定义中所预期的，Navier–Stokes 方程的涡量形式是通过取速度形式的旋度得到的，即对两边进行 \(\nabla\times\) 运算。经过大量推导后，得到

\[
\nu\nabla^2 w = [(\nabla \times u) \cdot \nabla] w .    \tag{25.30}
\]

这个方程和 (25.29) 是我们需要求解的两个联立偏微分方程。在二维情形下，由于 \(u\) 和 \(w\) 只有 \(z\) 分量，它们是

\[
\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = -w ,    \tag{25.31}
\]

\[
\nu\left(\frac{\partial^2 w}{\partial x^2} + \frac{\partial^2 w}{\partial y^2}\right) = \frac{\partial u}{\partial y}\frac{\partial w}{\partial x} - \frac{\partial u}{\partial x}\frac{\partial w}{\partial y} .    \tag{25.32}
\]

所以经过所有这些推导后，我们最终得到两个联立的、非线性的椭圆型偏微分方程，看起来像是泊松方程与波动方程的混合体。关于 \(u\) 的方程是以 \(w\) 为源的泊松方程，必须与第二个方程同时求解。正是第二个方程包含 \(u\) 和 \(w\) 导数的混合乘积，从而引入了非线性。

### 25.4.1 有限差分与 SOR 算法

我们在间距均匀为 \(h\) 的 \(N_x \times N_y\) 网格上求解 (25.31) 和 (25.32)，其中

\[
x = i\Delta x = i h , \quad i = 0, \dots, N_x , \quad y = j\Delta y = j h , \quad j = 0, \dots, N_y . \quad (25.33)
\]

由于梁关于其中心线对称（图 25.1a），我们只需要上半平面内的解。我们对 \(u\) 和 \(w\) 的拉普拉斯算子应用现在已经很熟悉的中心差分近似，得到差分方程

\[
\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} \simeq \frac{u_{i+1,j} + u_{i-1,j} + u_{i,j+1} + u_{i,j-1} - 4u_{i,j}}{h^2} . \quad (25.34)
\]

同样，对于一阶导数的乘积，

\[
\frac{\partial u}{\partial y} \frac{\partial w}{\partial x} \simeq \frac{u_{i,j+1} - u_{i,j-1}}{2h} \frac{w_{i+1,j} - w_{i-1,j}}{2h} . \quad (25.35)
\]

泊松方程 (25.31) 和 Navier–Stokes 方程涡量形式 (25.32) 的有限差分形式变为

\[
u_{i,j} = \frac{1}{4} \left( u_{i+1,j} + u_{i-1,j} + u_{i,j+1} + u_{i,j-1} + h^2 w_{i,j} \right) , \quad (25.36)
\]

\[
w_{i,j} = \frac{1}{4}(w_{i+1,j} + w_{i-1,j} + w_{i,j+1} + w_{i,j-1}) - \frac{R}{16} \left\{ [u_{i,j+1} - u_{i,j-1}] \times [w_{i+1,j} - w_{i-1,j}] - [u_{i+1,j} - u_{i-1,j}] [w_{i,j+1} - w_{i,j-1}] \right\} , \quad (25.37)
\]

\[
R = \frac{1}{\nu} = \frac{V_0 h}{\nu} \text{(按普通单位)} . \quad (25.38)
\]

注意我们将 \(u_{i,j}\) 和 \(w_{i,j}\) 放在方程的左边，以便得到适用于松弛法求解的算法。

(25.38) 中的参数 \(R\) 与雷诺数相关。当我们以自然单位求解问题时，距离以网格间距 \(h\) 为单位，速度以初始速度 \(V_0\) 为单位，流函数以 \(V_0 h\) 为单位，涡量以 \(V_0/h\) 为单位。第二种形式是普通单位，且无量纲。这个 \(R\) 称为网格雷诺数，它与物理 \(R\) 不同，后者以管道直径代替网格间距 \(h\)。

网格雷诺数度量了方程中非线性项耦合的强度。当物理 \(R\) 较小时，粘性起到摩擦力的作用，抑制涨落并保持流动平滑。当 \(R\) 较大（\(R \simeq 2000\)）时，物理流体会经历从层流到湍流的相变，其中湍流发生在越来越小的级联空间尺度上 (Reynolds, 1883)。然而，自 1883 年 Reynolds 首次实验以来，产生湍流起始的模拟一直是一个研究问题 (Falkovich and Sreenivasan, 2006)，这可能是因为层流对小扰动是稳定的，可能需要某种大尺度的“踢”来改变

