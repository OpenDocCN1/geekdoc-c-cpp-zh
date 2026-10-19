

![](img/bccda43674e4a93dee81c749eba8d2f7_381_0.png)

Figure 14.8 A chaotic attractor for the 4D Lotka–Volterra model projected onto three axes.

所有物种共存的情况：

$$
p_i(t = 0) = \begin{pmatrix} 0.3013 \\ 0.4586 \\ 0.1307 \\ 0.3557 \end{pmatrix}. \tag{14.45}
$$

一种可视化 (14.43) 解的方法是绘制 \(p_1(t)\)、\(p_2(t)\)、\(p_3(t)\) 和 \(p_4(t)\) 随时间变化的四个图。结果相当有趣，我们将其作为练习留给读者。更具启发性的可视化方法是创建 \([p_1(t_i), p_2(t_i), p_3(t_i), p_4(t_i)]\) 的 4D 相空间图，其中 \(i = 1, \ldots, N\)，\(N\) 为数值解中使用的步数。即使存在混沌，由此创建的几何结构也可能具有光滑且定义良好的形状。不幸的是，我们无法展示此类图，因此我们必须将其投影到 2D 和 3D 轴上。我们在图 14.8 中展示了其中一个 3D 图。这是一种典型的混沌吸引子类型，其 3D 结构折叠成近乎 2D 的结构（Rössler 方程以产生此类结构而闻名）。

## 14.11.1 Exercises

- 1. 求解在建议参数和初始条件下 (14.43)，并绘制 \(p_{1-4}(t)\) 随时间变化的图。评论这些图所表现的行为类型。
- 2. 通过将值 \([p_1(t_i), p_2(t_i), p_3(t_i), p_4(t_i)]\) 写入文件来构建由 (14.43) 的解形成的 4D 相空间混沌吸引子，其中 \(i\) 表示时间步。为了避免文件过长，您可能希望在每次文件输出前跳过若干个时间步。
  - a) 绘制所有可能的 2D 相空间图，即 \(p_i\) vs \(p_j\)，\(i \neq j = 1\)–\(4\) 的图。
  - b) 绘制所有可能的 3D 相空间图，即 \(p_i\) vs \(p_j\) vs \(p_k\) 的图。

*Note: you have to adjust the parameters or initial conditions slightly to obtain truly chaotic behavior.*

*注：您必须稍微调整参数或初始条件才能获得真正的混沌行为。*

## 14.11.2 LVM with Prey Limit

LVM 中猎物在没有捕食者的情况下无限制增长的初始假设显然是不现实的。与 logistic map 一样，我们引入对猎物数量的限制，以考虑猎物种群增长时食物供应的耗竭。因此，我们将恒定增长率从 \(a\) 修改为 \(a(1 - p/K)\)，使得种群达到极限 \(K\)、即环境容纳量时增长消失：

$$
\frac{\mathrm{d}p}{\mathrm{d}t} = a p \left(1 - \frac{p}{K}\right) - b p P, \tag{14.46}
$$

$$
\frac{\mathrm{d}P}{\mathrm{d}t} = \epsilon b p P - m P \quad \text{(LVM-II)}. \tag{14.47}
$$

该模型在存在猎物限制时的行为如图 14.9 所示。我们看到两个种群都表现出阻尼振荡，随着它们接近平衡值而衰减，并且如所希望的那样，平衡种群与初始条件无关。

![](img/bccda43674e4a93dee81c749eba8d2f7_382_0.png)

Figure 14.9 (a) The Lotka–Volterra model of prey population \(p(t)\) (solid curve) and predator population \(P(t)\) (dashed curve) vs. time when a prey population limit is included. (b) Prey population \(p\) as a function of predator population \(P\).

图 14.9 (a) 包含猎物种群限制时猎物种群 \(p(t)\)（实线）和捕食者种群 \(P(t)\)（虚线）随时间变化的 Lotka–Volterra 模型。(b) 猎物种群 \(p\) 随捕食者种群 \(P\) 的变化。

注意相空间图如何向内螺旋收敛到单一闭合极限环，并在其上保持，猎物数量变化很小。这就是“控制”，我们可以用它来开办一家无化学品的害虫控制业务。

## 14.11.3 LVM with Predation Efficiency

原始 LVM 中的另一个不现实的假设是捕食者立即吃掉它们接触到的所有猎物。正如任何观察过猫捕老鼠的人都知道，捕食者花费一些时间寻找猎物，还要追逐、杀死、吃掉和消化它（统称为处理）。这额外的时间降低了猎物被消除的速率 \(b p P\)。我们定义功能反应 \(p_a\) 为一个捕食者找到一个猎物的概率。如果单个捕食者花费时间 \(t_{\mathrm{search}}\) 寻找猎物，则

$$
p_a = b t_{\mathrm{search}} p \quad \Rightarrow \quad t_{\mathrm{search}} = \frac{p_a}{b p}. \tag{14.48}
$$

如果我们称捕食者处理单个猎物花费的时间为 \(t_h\)，则捕食者有效处理猎物花费的时间为 \(p_a t_h\)。因此，捕食者寻找和处理单个猎物花费的总时间 \(T\) 为

$$
T = t_{\mathrm{search}} + t_{\mathrm{handling}} = \frac{p_a}{b p} + p_a t_h \tag{14.49}
$$

$$
\Rightarrow \quad \frac{p_a}{T} = \frac{b p}{1 + b p t_h}, \tag{14.50}
$$

其中 \(p_a / T\) 是吃掉猎物的有效速率。我们看到当猎物数量 \(p \to \infty\) 时，吃掉它们的效率 \(\to 1\)。我们在 (14.46) 中包含此效率，通过将捕食者消除猎物的速率 \(b\) 修改为 \(b / (1 + b p t_h)\)：

$$
\frac{\mathrm{d}p}{\mathrm{d}t} = a p \left(1 - \frac{p}{K}\right) - \frac{b p P}{1 + b p t_h}, \quad \text{(LVM-III)}. \tag{14.51}
$$

为了更真实地描述捕食者增长，我们还对捕食者环境容纳量设置限制，但使其与猎物数量成正比：

$$
\frac{\mathrm{d}P}{\mathrm{d}t} = m P \left(1 - \frac{P}{k p}\right), \quad \text{(LVM-III)}. \tag{14.52}
$$

扩展模型 (14.51) 和 (14.52) 的解如图 14.10 所示。观察到 \(b\) 作为函数存在三种动态状态：

- small \(b\): no oscillations, overdamping,
- medium \(b\): damped oscillations that converge to a stable equilibrium,
- large \(b\): limit cycle.

小 \(b\)：无振荡，过阻尼，
中等 \(b\)：阻尼振荡收敛到稳定平衡，
大 \(b\)：极限环。

从平衡到极限环的转变称为相变。

![](img/bccda43674e4a93dee81c749eba8d2f7_384_0.png)

Figure 14.10 Lotka–Volterra model with predation efficiency and prey limitations. From left to right: overdamping, \(b = 0.01\); damped oscillations, \(b = 0.1\), and limit cycle, \(b = 0.3\).

图 14.10 具有捕食效率和猎物限制的 Lotka–Volterra 模型。从左到右：过阻尼，\(b = 0.01\)；阻尼振荡，\(b = 0.1\)，和极限环，\(b = 0.3\)。

我们终于对问题有了令人满意的解决方案。虽然猎物种群不会被消除，但可以防止其变得过大并大幅波动。尽管如此，参数的变化可能导致大幅波动或捕食者几乎消失。

## 14.11.4 LVM Implementation and Assessment

- 1. 编写程序使用 rk4 算法求解 (14.51) 和 (14.52)，并使用以下参数值。
- 2. 对于每三个模型，构造
  - a) 猎物和捕食者种群的时间序列，
  - b) 捕食者 vs 猎物种群的相空间图。
- 3. LVM-I：计算猎物和捕食者种群的平衡值。你认为循环振幅取决于初始条件的模型可以是现实的吗？解释。
- 4. LVM-II：计算猎物和捕食者种群平衡值的数值。针对不同的猎物环境容纳量 \(K\) 进行一系列运行。你能推断平衡种群如何随猎物环境容纳量变化吗？
- 5. 针对捕食者和猎物种群的不同初始条件进行一系列运行。循环振幅是否取决于初始条件？
- 6. LVM-III：针对不同的 \(b\) 值进行一系列运行并重现图 14.10 中存在的三种状态。
- 7. 计算对应于稳定平衡与极限环之间相变的 \(b\) 的临界值。

| Model | a | b | ε | m | K | k |
|---|---|---|---|---|---|---|
| LVM-I | 0.2 | 0.1 | 1 | 0.1 | 0 | — |
| LVM-II | 0.2 | 0.1 | 1 | 0.1 | 20 | — |
| LVM-III | 0.2 | 0.1 | — | 0.1 | 500 | 0.2 |

## 14.11.5 Two Predators, One Prey (Exploration)

- 1. LVM 的另一个版本包括两个捕食者种群 \(P_1\) 和 \(P_2\) 可能“共享”同一猎物种群 \(p\) 的可能性。研究一个系统中猎物种群在没有捕食者的情况下按 logistic 增长的行为：

$$
\frac{\mathrm{d}p}{\mathrm{d}t} = a p \left(1 - \frac{p}{K}\right) - (b_1 P_1 + b_2 P_2) p \tag{14.53}
$$

$$
\frac{\mathrm{d}P_1}{\mathrm{d}t} = \epsilon_1 b_1 p P_1 - m_1 P_1, \qquad \frac{\mathrm{d}P_2}{\mathrm{d}t} = \epsilon_2 b_2 p P_2 - m_2 P_2 \tag{14.54}
$$

  - a) 使用以下模型参数和初始条件值：\(a = 0.2\)，\(K = 1.7\)，\(b_1 = 0.1\)，\(b_2 = 0.2\)，\(m_1 = m_2 = 0.1\)，\(\epsilon_1 = 1.0\)，\(\epsilon_2 = 2.0\)，\(p(0) = P_2(0) = 1.7\)，且 \(P_1(0) = 1.0\)。
  - b) 确定每个种群的时间依赖性。
  - c) 改变第二捕食者的特征并计算三个组分的平衡种群。
  - d) 对问题“两个共享同一猎物的捕食者能否共存？”你的回答是什么？

- 2. Lotka–Volterra 模型的非线性性质可能导致混沌和分形行为。通过改变增长率来寻找复杂行为。

