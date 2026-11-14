

![](img/255d48531d66773aa863436a333dac7d_120_0.png)

图 4.9 各基组下最终能量相对误差随精度阈值 $\epsilon^{prec}$ 的变化。右侧显示了测试分子。每个点是五个测试系统的平均值。误差棒表示均值以上的 2 个标准差。黑线显示了公式 (4.6-4) 的经验误差界。

# 表 4.2 使用 6-31G 基组对各分子进行 RHF 计算的动态精度性能

| 系统 | 原子 | BFS | GPU | 时间 (s) | 迭代 | 最终能量 | |ΔE| | 加速比 |
|---|---|---|---|---|---|---|---|---|
| 抗坏血酸 | 20 | 124 | 1 | 1.47 | 12 | -680.6986414386 | 1.2E-07 | 2.0 |
| 乳糖 | 45 | 251 | 1 | 6.83 | 10 | -1290.0883461502 | 1.4E-07 | 2.2 |
| 蓝藻毒素 | 110 | 598 | 1 | 66.23 | 13 | -2492.3971987780 | 4.9E-07 | 2.3 |
| 神经激肽 A | 157 | 864 | 1 | 146.75 | 14 | -4091.3672646454 | 9.7E-08 | 2.3 |
| 5 x 6 纳米管 | 386 | 3320 | 8 | 1138.49 | 15 | -13793.7293926019 | 1.1E-07 | 2.7 |
| 崩菜碱 | 642 | 3597 | 8 | 741.23 | 12 | -17996.6569297786 | 2.3E-07 | 1.8 |
| 泛素 | 1231 | 6680 | 8 | 7418.08 | 18 | -29616.4426380779 | 4.5E-07 | 2.0 |
| T-钙粘蛋白 ECI | 1542 | 8404 | 8 | 10592.68 | 16 | -36975.8726052678 | 3.4E-07 | 2.0 |

各列分别列出每个系统的原子数、每个系统的 AO 轨道数、使用动态精度进行整个 SCF 评估所需的时间（秒）、将 SPF*SPF 的最大矩阵元收敛到 10^-4 a.u. 所需的迭代次数、最终动态能量（哈特里）、动态精度与双精度最终能量之间的绝对差值（哈特里），以及动态精度相对于双精度运行的 SCF 计算的总加速比。

单精度仅提供 2:1 的优势。理论峰值只是决定整体性能的一个因素。如上所述，单精度间隔所需的寄存器占用也小于双精度值。这使得编译器能够为单精度内核生成更高效的代码，并解释了单精度 ERI 内核所享受的大部分优势。

## 4.6 后 SCF 方法

虽然 GPU-J 和 K-能量是在 SCF 加速的背景下开发的，但这些算法也可以更广泛地应用于计算性质和实现后 SCF 方法。例如，扩展到库仑和交换梯度积分是简单直接的，并遵循上文详细阐述的相同原理 [32]。作为一个更有趣的例子，我们考虑构型相互作用单替代（CIS）和 TDDFT 算法的 GPU 加速实现 [33]。这些方法的完整综述可在其他文献中找到 [34]。TDDFT 的基本工作方程可以写成以下矩阵表示法：

$$ \begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B} & \mathbf{A} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix} = \omega \begin{pmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & -\mathbf{1} \end{pmatrix} \begin{pmatrix} \mathbf{X} \\ \mathbf{Y} \end{pmatrix}. $$

这里，\(\mathbf{X}\) 和 \(\mathbf{Y}\) 是表示跃迁振幅的向量，\(\omega\) 是激发能。将公式 (4.6-5) 应用于 Hartree–Fock 理论会得到时依赖 Hartree–Fock（TDHF）方法，其中算符 \(A\) 和 \(B\) 定义如下：

$$ A_{ia,jb} = \delta_{ij}\delta_{ab}(\epsilon_a - \epsilon_i) + (\theta_i \theta_a | \theta_j \theta_b) - (\theta_i \theta_j | \theta_a \theta_b), $$

$$ B_{ia,jb} = (\theta_i \theta_a | \theta_j \theta_b) - (\theta_i \theta_j | \theta_a \theta_b). $$

对于 TDDFT，算符定义类似，但类库仑 ERI 被交换相关势的泛函导数所取代：

$$ A_{ia,jb} = \delta_{ij}\delta_{ab}(\epsilon_a - \epsilon_i) + (\theta_i \theta_a | \theta_j \theta_b) + (\theta_i f_{xc} | \theta_a \theta_b), $$

$$ B_{ia,jb} = (\theta_i \theta_a | \theta_j \theta_b) + (\theta_i f_{xc} | \theta_a \theta_b), $$

$$ (\theta_i \theta_j | f_{xc} | \theta_a \theta_b) = \iint \theta_i(\vec{r}_1) \theta_j(\vec{r}_1) \frac{\delta^2 E_{xc}}{\delta \rho(\vec{r}_1) \delta \rho(\vec{r}_2)} \theta_a(\vec{r}_2) \theta_b(\vec{r}_2). $$

在上述方程中，ERIs 用之前 SCF 计算得到的分子轨道表示。下标 \(i\) 和 \(j\) 指占据轨道，而 \(a\) 和 \(b\) 索引虚拟轨道。为清晰起见，忽略自旋。使用 Tamm–Dancoff 近似（TDA），\(B\) 矩阵设为零。这对于 TDHF 得到 CIS，对于 TDDFT 得到 TDA–TDDFT：

$$ \mathbf{AX} = \alpha \mathbf{X}. $$

该方程可使用迭代对角化算法（如 Davidson 方法 [35]）高效求解。此类算法通过 \(A\) 与试探特征向量之间的一系列矩阵向量乘积来求解特征值问题：

$$ (\mathbf{A}\mathbf{X})_{\mu} = \sum_{\nu} [\delta_{\mu\nu}\delta_{ab}(\epsilon_a - \epsilon_i) + (\theta_i \theta_a | \theta_j \theta_b) - (\theta_i \theta_j | \theta_a \theta_b)] X_{\nu}. $$

为了应用 J- 和 K-引擎算法，这些乘积可以使用以下变换在 AO 基组中进行：

$$ \sum_{\mu} [(\theta_i \theta_a | \theta_j \theta_b) - (\theta_i \theta_j | \theta_a \theta_b)] X_{\mu} = \sum_{\mu\nu} C_{\mu i} C_{\nu a} F_{\mu \nu}. $$

$$ F_{\mu \nu} = \sum_{\lambda \sigma} T_{\mu \lambda} [(\mu \nu | \lambda \sigma) - (\mu \lambda | \nu \sigma)], $$

$$ T_{\mu \lambda} = \sum_{\alpha \nu} X_{\nu i} C_{\nu a} C_{\alpha \nu}. $$

这里，\(\mathbf{T}\) 是在 AO 基组中表示的非对称跃迁密度。主要的计算步骤是构建 \(\mathbf{F}\)，这类似于计算 SCF Fock 矩阵的双电子贡献。由于矩阵 T 是非对称的，因此需要对上述算法进行两处小调整。对于 J-引擎，对跃迁密度进行对称化即可：

$$\tilde{T}_\mu = \frac{1}{2}(T_{\mu\nu} + T_{\nu\mu}).$$ (4.76)

然而，对于非对称密度，交换矩阵本身也变得非对称。因此，K-引擎必须被调用两次来处理 T 的上三角和下三角。因此，忽略筛选，激发态交换贡献名义上计算所有 N^2 个 ERIs。然而，跃迁密度 T_μν 只包含一个电子，并且比总基态密度稀疏得多。这使得 K-引擎能够忽略激发态的更多 ERIs，并最终使得激发态 K-构建优于其基态类似物。

## 4.7 示例计算

这里我们说明了先前讨论的 GPU 算法在实际计算中的应用。以下描述的所有 GPU 计算均使用 TeraChem 量子化学软件包进行。为了阐明我们的 GPU 实现随系统尺寸增加的计算规模，我们考虑两种类型的系统：首先，长度在 25 到 706 个碳原子之间的线性烯烃链提供了低维极限的基准。其次，包含 10 到 988 个分子的立方水团提供了一个致密的三维测试系统，这更具代表性，适用于大多数感兴趣的凝聚相系统。每种系统类型的示例均显示于图 4.10。

对于每个系统，在单块 Tesla M2090 GPU 上使用 6-31G 基组进行了受限 B3LYP 计算。图 4.11 显示了第一次 SCF 迭代期间 J-引擎、K-引擎、线性代数（LA）和 DFT 交换相关势的时间分解。对于水团，K-引擎和距离掩码 K-引擎在单独运行中进行了测试，并均提供以供比较。距离掩码 K-引擎选择了保守的 8 Å 筛选距离。图例中给出了每个系列幂律拟合得到的指数。

线性代数时间主要由 Fock 矩阵的对角化主导，其规模明显差于 Fock 构建例程。对于大型系统，对角化显然将

![](img/255d48531d66773aa863436a333dac7d_122_0.png)

![](img/255d48531d66773aa863436a333dac7d_122_1.png)

图 4.10 一维烯烃和三维水立方体测试系统。烯烃长度从 24 到 706 个碳原子不等，水立方体范围从 10 到近 850 个水分子。所有水箱均使用均匀密度

