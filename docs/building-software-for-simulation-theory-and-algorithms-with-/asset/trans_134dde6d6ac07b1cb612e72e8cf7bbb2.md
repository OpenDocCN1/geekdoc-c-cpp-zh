
该元件由公式 2.10 的函数形式决定：它以 effort 变量为输入并产生 flow 变量。这就是选择履带速度作为输出的原因。

电机、变速箱和履带的模型考虑了电动机的电感和内阻、齿轮的角质量和摩擦，以及橡胶履带的顺应性。电动机为 Mabuchi FA-130 电机，与小型玩具中普遍使用的同类型直流电机相同。一个电机驱动一条履带。电机插入 Tamiya 双电机变速箱。该变速箱有两个相同、独立的齿轮组来转动链轮。链轮和履带来自 Tamiya 履带和轮组套件；履带在坦克加速时会伸长（在急转弯时这会导致履带从轮子上脱落！），因此其顺应性包含在模型中。

为了驱动电机，计算机在 Allegro A3953 全桥脉宽调制（PWM）电机驱动器中切换一组晶体管。当开关闭合时，坦克的电池连接到电机。当开关打开时，电池与电机断开。晶体管的开关速率比计算机操作它们的速率高三个数量级，且电路中的功率损耗与系统其他地方的效率低下相比可以忽略。因此，电池和电机驱动器被建模为理想的时变电压源。

连接的电机、变速箱和履带的示意图及其键合图如图 2.3 所示。表 2.2 列出了本模型中使用的参数。

![](img/df6085a1b35edf9c9ea818a5c66ccad9_25_0.png)

**图 2.3** 坦克的电机、齿轮和履带：（a）示意图；（b）键合图。

**表 2.2** 电机、变速箱和履带的参数

| Parameter | Value | Description |
|---|---|---|
| $L_m$ | 10⁻³ H | 电机的电感 |
| $R_m$ | 3.1 Ω | 电机的电阻 |
| $J_g$ | 1.2 × 10⁻⁶ kg·m² | 齿轮的角质量 |
| $B_g$ | 6.7 × 10⁻³ N·m·s/rad | 齿轮旋转的机械阻力 |
| $g$ | 204 | 变速箱的齿轮比 |
| $\alpha$ | 10⁻³ N·m/A | 电动机的电流-转矩比 |
| $r$ | 0.015 m | 链轮的半径 |
| $K_t$ | 10⁻³ m/N | 履带的顺应性 |

微分方程直接从键合图中读出：

$$
\dot i_l = \frac{1}{L_m}(e_l - i_l R_m - \alpha \omega_l) \tag{2.11}
$$

$$
\dot \omega_l = \frac{1}{J_g}\left(\alpha i_l - \omega_l B_g - \frac{r}{g}F_l\right) \tag{2.12}
$$

$$
\dot F_l = \frac{1}{K_t}\left(\frac{r}{g}\omega_l - v_l\right) \tag{2.13}
$$

$$
\dot i_r = \frac{1}{L_m}(e_r - i_r R_m - \alpha \omega_r) \tag{2.14}
$$

$$
\dot \omega_r = \frac{1}{J_g}\left(\alpha i_r - \omega_r B_g - \frac{r}{g}F_r\right) \tag{2.15}
$$

$$
\dot F_r = \frac{1}{K_t}\left(\frac{r}{g}\omega_r - v_r\right) \tag{2.16}
$$

其中 $e_l$ 和 $e_r$ 为电机电压，$v_l$ 和 $v_r$ 为由公式 2.8 和 2.9 给出的履带速度。

表 2.2 中的参数值来自制造商数据、测量结果和有根据的猜测。齿轮比 $g$ 和电流-转矩比 $\alpha$ 由制造商提供。齿轮比是准确且精确的（尤其是相对于模型中其他参数的值）。电流-转矩比是 Mabuchi，即电机制造商提供的两种情况的平均值。第一种情况是电机在峰值效率下运行，第二种情况是电机堵转。这两种情况之间的差异很小，表明 $\alpha$ 随着电机负载的变化而不会发生实质性变化。因此，对 $\alpha$ 的估计很可能非常合理。

链轮的半径 $r$ 以及电机的电阻 $R_m$ 和电感 $L_m$ 是直接测量的。使用尺子测量链轮的半径。确定 $R_m$ 和 $L_m$ 需要更多工作。空载电机中的电流 $i$ 与电机两端的电压 $e$ 之间的关系由微分方程给出

$$
\dot{i}=\frac{1}{L_m}(e-iR_m) \tag{2.17}
$$

参数 $L_m$ 和 $R_m$ 是通过将 1.5-V C 电池连接到电机并用示波器测量电机电流的上升时间和稳态来估计的。设 $i_f$ 为稳态电流，$t_f$ 为上升时间，且 $0.9i_f$ 为时间 $t_f$ 时的电流（即上升时间是从零电流到稳态电流 90% 所需的时间）。在稳态时 $\dot{i}=0$，电机的电阻由下式给出

$$
R_m=\frac{e}{i_f}
$$

需要瞬态电流来求 $L_m$。瞬态电流由公式 2.17 的解给出：

$$
i(t)=\frac{e}{R_m}\left(1-\exp\left(-\frac{R_m}{L_m}t\right)\right) \tag{2.18}
$$

将 $0.9i_f$ 代入 $i(t)$，$t_f$ 代入 $t$，并在公式 2.18 中求解 $L_m$ 得到

$$
\frac{1}{L_m}=-\frac{1}{R_mt_f}\ln\left(1-0.9\frac{R_m}{e}i_f\right)=-\frac{i_f}{et_f}\ln(0.1)\approx 2.3\frac{i_f}{et_f}
$$

或等价地

$$
L_m\approx 0.652\frac{t_f}{i_f}
$$

类似的实验用于获得 $B_g$。在此实验中，电机连接到变速箱。如前所述，使用示波器测量电机电流的上升时间和稳态值。电机的旋转速度 $\dot{\omega}$ 由下式给出

$$
\dot{\omega}=\frac{1}{J_g}(\alpha i-B_g\dot{\omega})
$$

制造商给出电机在峰值效率下运行时速度为 $\dot{\omega}=731.6$ 弧度每秒（rad/s）。在稳态时 $\dot{\omega}=0$。稳态电流 $i_f$ 用示波器测量。利用 $i_f$ 和电机速度，变速箱的机械阻力由下式给出

$$
B_g \approx \frac{\alpha i_f}{\dot{\omega}} = 1.37 \times 10^{-6} i_f
$$

变速箱的角质量 $J_g$ 由其质量 $m_{gb}$、齿轮半径 $r_{gb}$ 以及质量在圆柱体中均匀分布的假设估计得出。在这组测量和假设下，角质量为

$$
J_g = m_{gb} r_{gb}^2
$$

履带的顺应性是一个数量级近似。履带在从轮子上滑落之前只能拉伸几毫米。履带的最大推进力约为一牛顿。因此，履带顺应性的数量级估计为 $10^{-3}$ 米/$10^{0}$ 牛顿，或约为 $10^{-3}$ m/N。

### 2.2.3 坦克连续动力学的完整模型

公式 2.1–2.9 和 2.11–2.16 共同描述了坦克的物理行为。运动方程和电机、变速箱和履带的方程是分开开发的，但求解算法在耦合方程合并时效果最好。因此，这些被放入一个名为 “tank physics” 的单一功能模型中，如图 2.4 所示。坦克的输入是其左右电机的电压；这些来自计算机。坦克的输出是其位置和航向；这些由坦克操作员观察。坦克物理动力学的完整状态空间模型为

$$
turning = \begin{cases}
true & \text{if } \frac{1}{2}|F_l - F_r| \ge S_t \\
false & \text{otherwise}
\end{cases} \tag{2.19}
$$

$$
\dot{v} = \begin{cases}
\frac{1}{m_t}\left(F_l + F_r - (B_r + B_s)v\right) & \text{if } turning = true \\
\frac{1}{m_t}\left(F_l + F_r - B_r v\right) & \text{if } turning = false
\end{cases} \tag{2.20}
$$

$$
\dot{\omega} = \begin{cases}
\frac{1}{J_r}\left(\frac{B}{g}(F_l-F_r)-B_i\omega\right) & \text{if turning} = \text{true}\\
0 & \text{if turning} = \text{false}
\end{cases} \tag{2.21}
$$

$$
\dot{\theta} = \omega \tag{2.22}
$$

$$
\dot{x} = v \sin(\theta) \tag{2.23}
$$

$$
\dot{y} = v \cos(\theta) \tag{2.24}
$$

$$
\text{If turning} = \text{false then } \omega = 0 \tag{2.25}
$$

$$
\dot{i}_l = \frac{1}{L_m}(e_l - i_l R_m - \alpha \omega_l) \tag{2.26}
$$

$$
\dot{\omega}_l = \frac{1}{J_g}\left(\alpha i_l - \omega_l B_g - \frac{r}{g}F_l\right) \tag{2.27}
$$

$$
\dot{F}_l = \frac{1}{K_t}\left(\frac{r}{g}\omega_l - \left(v + \frac{B\omega}{g}\right)\right) \tag{2.28}
$$

$$
\dot{i}_r = \frac{1}{L_m}(e_r - i_r R_m - \alpha \omega_r) \tag{2.29}
$$

$$
\dot{\omega}_r = \frac{1}{J_g}\left(\alpha i_r - \omega_r B_g - \frac{r}{g}F_r\right) \tag{2.30}
$$

$$
\dot{F}_r = \frac{1}{K_t}\left(\frac{r}{g}\omega_r - \left(v - \frac{B\omega}{g}\right)\right) \tag{2.31}
$$

该模型有 11 个状态变量——v、ω、θ、x、y、i_l、ω_l、F_l、i_r、ω_r 和 F_r；两个输入变量——e_l 和 e_r；以及三个输出变量——x、y 和 θ。

### 2.2.4 计算机

计算机是来自 Maxim 的 TINI 微控制器，它通过无线网络接收操作员的命令并将其转换为电机的电压信号。计算机从连接计算机和无线电的以太网中提取原始位，将位通过以太网和用户数据报协议（UDP）栈处理以获得数据包，从该数据包中获取控制信息，并将该信息存储在寄存器中，以便生成电压信号的中断处理程序可以找到它。中断处理程序定期运行，其优先级高于处理操作员命令的线程。因此，中断处理程序花费的时间无法用于处理操作员的命令。

电压信号的频率由中断处理程序的频率决定。频繁的中断产生高频电压信号；不频繁的中断产生低频信号。图 2.5 说明了中断处理程序的工作方式。它每 N 个机器周期执行一次，并在每次调用时向存储在 8 位寄存器中的计数器添加 32。该计数器与设定的开启时间进行比较，
