
**表1.** 基本电路元件的 *n* 阶模型。

| 电路元件 | *n* 阶模型替代 | 详情 |
|---|---|---|
| 独立电压源，给定 $V(t)$ [10] | $n=1$: $V(t)$; $n>1$: 短路 | 一阶：不变；更高阶：短路 |
| 独立电流源，给定 $I(t)$ [10] | $n=1$: $I(t)$; $n>1$: 开路 | 一阶：不变；更高阶：开路 |
| 非线性电阻器，$V(t)=\sum_{k=1}^{\infty}R_k I^k(t)$ [10] | $n=1$: $R_1$; $n>1$: 电压源 $V_{En}(t)$ 与 $R_1$ 串联 | $V_{E1}(t)=0$; $V_{E2}(t)=R_2 I_1^2(t)$; $V_{E3}(t)=2R_2 I_1(t)I_2(t)+R_3 I_1^3(t)$ |
| 非线性电容器，$V(t)=\sum_{k=1}^{\infty}S_k Q^k(t)$ [10] | $n=1$: $C=1/S_1$; $n>1$: 电压源 $V_{En}(t)$ 与 $C$ 串联 | $V_{E1}(t)=0$; $V_{E2}(t)=S_2 Q_1^2(t)$; $V_{E3}(t)=2S_2 Q_1(t)Q_2(t)+S_3 Q_1^3(t)$ |
| 非线性电感器，$V(t)=\dot{\Phi}(t)$, $\Phi(t)=\sum_{k=1}^{\infty}L_k I^k(t)$ [10] | $n=1$: $L_1$; $n>1$: 电压源 $V_{En}(t)$ 与 $L_1$ 串联 | $V_{E1}(t)=0$; $V_{E2}(t)=\frac{d}{dt}L_2 I_1^2(t)$; $V_{E3}(t)=\frac{d}{dt}\left(2L_2 I_1(t)I_2(t)+L_3 I_1^3(t)\right)$ |
| 忆阻器，$V(t)=M(Q(t))I(t)$, $M(Q)=\sum_{k=0}^{\infty}M_k Q^k$（第3.2节） | $n=1$: $M_0$; $n>1$: 电压源 $V_{En}(t)$ 与 $M_0$ 串联 | $V_{E1}(t)=0$; $V_{E2}(t)=M_1 Q_1(t)I_1(t)$; $V_{E3}(t)=M_1 Q_2(t)I_1(t)+M_2 Q_1^2(t)I_1(t)+M_1 Q_1(t)I_2(t)$ |

对于前三个阶数 $n$，我们得到

\[
V_1(t)=M_0I_1(t),
\]

\[
V_2(t)=M_0I_2(t)+\left(M_1Q_1(t)I_1(t)\right),
\]

\[
V_3(t)=M_0I_3(t)+\left(M_1Q_2(t)I_1(t)+M_2Q_1^2(t)I_1(t)+M_1Q_1(t)I_2(t)\right).
\]

可以看出，$V_n(t)$ 是 $M_0$ 乘以 *n* 阶电流与括号中一项的和，该项不依赖于任何阶数 $\ge n$ 的量。因此，*n* 阶忆阻器模型是一个线性电阻 $M_0$，与一个时变电压源串联（见表1）。

## 3.3. *CM 电路*

为简单起见，假设 CM 电路（图6）中的电容器是线性的，且忆阻值给定为

\[
M(Q)=M_0+M_1Q\quad\text{with }M_0C>0.
\]

![img/039e7d3c23390584a66737067db8b75b_545_0.png](img/039e7d3c23390584a66737067db8b75b_545_0.png)

*图6.* CM 电路的原理图。

电路由一个独立的正弦电压源激励

\[
V_S(t)=\hat V_S\cos(\omega_0t+\varphi_{V_S}), \tag{10}
\]

我们希望计算流过忆阻器的电流 $I(t)$。

此外，假设 $Q(t)=Q_C(t)$，其中 $Q_C(t)$ 表示电容器的电荷。那么，

![img/039e7d3c23390584a66737067db8b75b_546_0.png](img/039e7d3c23390584a66737067db8b75b_546_0.png)

该系统在 $V_S(t)\equiv0$ 时具有一个吸引不动点 $Q_{\mathrm{FP}}=0$。因此，对于足够小的 $Q(0)$，在 $Q_C(t)=Q(t)$ 且无激励的情况下，电路具有唯一的渐近行为。我们假设这对受激励的电路也成立。因此，我们忽略瞬态响应，仅计算稳态电流。（然而，如果 $Q(0)-Q_C(0)$ 非零，则 $Q(t)$ 将以恒定偏移跟随 $Q_C(t)$，即充当一种“影子状态”。因此，对该系统的分析将略有不同。）

#### 一阶电路

首先，上述电路中的电路元件必须替换为各自的一阶模型，这些模型可以从表1中获得。得到的一阶电路如图7所示。

由于一阶电路是线性的，因此可以直接确定一阶电流 $I_1(t)$。对于角频率为 $\omega_0$ 的正弦激励 $V_S(t)$，电流 $I_1(t)=\hat{I}_{1,\omega_0}\cos(\omega_0t+\varphi_{I_1,\omega_0})$ 也必须是正弦的。利用传递函数

\[
G_1(j\omega)=\frac{I_1}{V_S}=\frac{1}{M_0-j/(\omega C)},
\]

一阶电流的幅度 $\hat{I}_{1,\omega_0}$ 和相位 $\varphi_{I_1,\omega_0}$ 如下

\[
\hat{I}_{1,\omega_0}=\hat{V}_S\,|G_1(j\omega_0)|=\frac{\hat{V}_S}{\sqrt{M_0^2+\left(1/(\omega_0C)\right)^2}}
\]

和

\[
\varphi_{I_1,\omega_0}=\varphi_{V_S}+\arg G_1(j\omega_0)=\varphi_{V_S}+\arctan\frac{1}{\omega_0M_0C}.
\]

对 $I_1(t)$ 关于时间积分，得到

\[
Q_1(t)=\frac{\hat{I}_{1,\omega_0}}{\omega_0}\cos\left(\omega_0t+\varphi_{I_1,\omega_0}-\frac{\pi}{2}\right).
\]

#### 二阶电路

二阶电路包含一个新的独立电压源，它是忆阻器模型的一部分（图8）。该电压源的电压 $V_{E2}(t)$ 必须利用一阶电路的结果来确定。

![img/039e7d3c23390584a66737067db8b75b_546_1.png](img/039e7d3c23390584a66737067db8b75b_546_1.png)

使用缩写 $A=\omega_0t+\varphi_{I_1,\omega_0}$，$V_{E2}(t)$ 可写成

\[
V_{E2}(t)=M_1Q_1(t)I_1(t)=\frac{M_1\hat{I}_{1,\omega_0}^2}{\omega_0}\cos(A)\cos\left(A-\frac{\pi}{2}\right)=\frac{M_1\hat{I}_{1,\omega_0}^2}{2\omega_0}\left[\cos\left(2A-\frac{\pi}{2}\right)+\cos\left(\frac{\pi}{2}\right)\right]=\hat{V}_{E2,2\omega_0}\cos(2\omega_0t+\varphi_{V_{E2},2\omega_0}).
\]

因此，二阶电路的唯一激励是角频率为 $2\omega_0$ 的正弦电压，其幅度/相位为

\[
\hat{V}_{E2,2\omega_0}=\frac{M_1\hat{I}_{1,\omega_0}^2}{2\omega_0},\qquad
\varphi_{V_{E2},2\omega_0}=2\varphi_{I_1,\omega_0}-\frac{\pi}{2}.
\]

同样地，使用传递函数 $G_2(j\omega)=-G_1(j\omega)$ 来计算电流 $I_2(t)$。二阶电流的幅度为

\[
\hat{I}_{2,2\omega_0}=\frac{\hat{V}_{E2,2\omega_0}}{\sqrt{M_0^2+\left(1/(2\omega_0C)\right)^2}};
\]

其相位为

\[
\varphi_{I_2,2\omega_0}=\varphi_{V_{E2},2\omega_0}+\arctan\frac{1}{2\omega_0M_0C}+\pi.
\]

通过对 $I_2(t)$ 积分可以得到 $Q_2(t)$。

#### 三阶电路

二阶电路与三阶电路之间唯一的区别在于属于忆阻器模型的时变电压源。$V_{E3}(t)$ 和 $I_3(t)$ 都可以写成两个分别具有角频率 $\omega_0$ 和 $3\omega_0$ 的正弦分量之和。

#### 结果

为了获得原始电路中电流 $I(t)$ 的近似值，我们只需将一阶、二阶和三阶电流相加，得到

\[
\begin{aligned}
I(t)&\approx\hat{I}_{1,\omega_0}\cos(\omega_0t+\varphi_{I_1,\omega_0})\\
&\quad+\hat{I}_{2,2\omega_0}\cos(2\omega_0t+\varphi_{I_2,2\omega_0})\\
&\quad+\hat{I}_{3,\omega_0}\cos(\omega_0t+\varphi_{I_3,\omega_0})\\
&\quad+\hat{I}_{3,3\omega_0}\cos(3\omega_0t+\varphi_{I_3,3\omega_0}). \tag{11}
\end{aligned}
\]

使用 $C=1\,\mu\mathrm{F}$, $M_0=100\,\Omega$, $M_1=0.1\,\mathrm{G}\Omega\,(\mathrm{As})^{-1}$, $\omega_0=20000\,\mathrm{s}^{-1}$, $\hat{V}_S=1\,\mathrm{V}$, $\varphi_{V_S}=0.166667\,\pi$ 和 $Q(0)=2.5\,\mu\mathrm{As}$ 进行了数值仿真。从图9可以看出，（在瞬态衰减后）使用(11)获得的近似值与示例电路的数值仿真结果非常接近。

![img/039e7d3c23390584a66737067db8b75b_547_0.png](img/039e7d3c23390584a66737067db8b75b_547_0.png)

![img/039e7d3c23390584a66737067db8b75b_547_1.png](img/039e7d3c23390584a66737067db8b75b_547_1.png)

*图9.* 将多线性理论获得的结果（虚线）与 CM 电路数值仿真计算得到的结果（实线）进行比较。图中显示了电路中的电流 (a) 和忆阻器的紧滞回线 (b)。

## 4. 利用 Volterra 级数方法对单忆阻器电路的一般描述

尽管多线性理论的应用在某些情况下能得到精确的近似，但最好在更一般的基础上描述含忆阻器的电路。这可以通过引入如图10所示的所谓单忆阻器电路来实现。一个可以由其阻抗矩阵表示的通用线性二端口网络与一个忆阻器和一个给定的电流源耦合。请注意，定义这种特定形式并不失一般性，即可以用电压源代替电流源进行类似描述。

下面介绍 Volterra 级数，并将其应用于 SMC。

![img/039e7d3c23390584a66737067db8b75b_547_2.png](img/039e7d3c23390584a66737067db8b75b_547_2.png)

*图10.* 单忆阻器电路的一般结构，由连接到电源和忆阻器的线性二端口网络组成。

### 4.1. Volterra 级数方法

假设一个非线性系统，其输入函数为 $x(t)$，相应的输出函数为 $y(t)$。Volterra 级数根据下式将输入与输出函数联系起来：

\[
y(t)=\sum_{n=1}^{\infty}\int_{-\infty}^{\infty}\cdots\int_{-\infty}^{\infty}h_n(\tau_1,\ldots,\tau_n)x(t-\tau_1)\cdots x(t-\tau_n)\,d\tau_1\cdots d\tau_n. \tag{12}
\]

索引 $n$ 定义了所谓的 Volterra 阶数，因此可以将(12)想象为将 $y$ 分解为阶数为 $n$ 的齐次系统的输出 $y_n$。函数 $h_n(\tau_1,\ldots,\tau_n)$ 表示阶数为 $n$ 的 Volterra 核。一旦核 $h_n$ 已知，就可以确定与给定输入对应的正确输出函数。复频域中的核是时域中核的拉普拉斯变换。
