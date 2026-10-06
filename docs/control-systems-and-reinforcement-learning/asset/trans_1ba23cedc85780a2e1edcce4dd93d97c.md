

# 值函数近似

**命题 5.4** *假设 $R_N$ 的秩小于 $d$。那么存在一个非零向量 $v \in \mathbb{R}^d$，对于每个 $0 \le k \le N-1$，满足以下条件：*

- (i) 对于任意 $\theta \in \mathbb{R}^d$ 和 $r \in \mathbb{R}$，

```
$\mathcal{D}_{k+1}(Q^{\theta})=\mathcal{D}_{k+1}(Q^{\theta'}), \quad \text{with } \theta'=\theta+rv$
```

- (ii) 对于同策略（on-policy）实现，

```
$v^T \psi(x(0), u(0)) = v^T \psi(x(k), u(k)).$
```

因此，这属于 5.1.5 节讨论的“冗余”类别。

证明 *如果 $R_N$ 不是满秩，则存在一个非零向量 $v$ 满足 $v^T R_N v = 0$。根据定义，

```
$0 = v^T R_N v = \frac{1}{N} \sum_{k=0}^{N-1} (v^T \Upsilon_{k+1})^2$.
```

也就是说，对于每一个观测样本，$v^T \Upsilon_k = 0$，这意味着

```
$0 = v^T \psi(x(k), u(k)) - v^T \psi(x(k+1), \phi(x(k+1))), \quad 0 \le k \le N-1. \quad (5.35)
```

部分 (i) 由 (5.35) 和定义 (5.28a) 得出：对于任意标量量 $r$，当 $\theta' = \theta + rv$ 时：

```
$\mathcal{D}_{k+1}(Q^{\theta}) = -Q^{\theta}(x(k), u(k)) + c(x(k), u(k)) + Q^{\theta}(x(k+1), \phi(x(k+1)))\n= c(x(k), u(k)) + [\theta + rv]^T [-\psi(x(k), u(k)) + \psi(x(k+1), \phi(x(k+1)))]\n= c(x(k), u(k)) + \theta^T [-\psi(x(k), u(k)) + \psi(x(k+1), \phi(x(k+1)))] = \mathcal{D}_{k+1}(Q^{\theta}).$
```

如果对于所有 $k, u(k) = \phi(x)$，则 (5.35) 变为：

```
$v^T \psi(x(k), u(k)) = v^T \psi(x(k+1), u(k)), \quad 0 \le k \le N-1$,
```

这意味着 (ii)。

同策略算法之所以被优选是因为易于分析（主要在随机控制背景下）。为了确保足够的探索，最好采用 (2.55) 中引入的重启选项：

## 最小二乘时间差分学习（带重启）

假设给定 $d \times d$ 矩阵 $W > 0$，整数 $N$ 和 $M$，以及观测样本

```
${u'(k), x'(k) : 0 \le i \le N, 1 \le i \le M\}$ (5.36a)
```

带有用户定义的初始条件 $\{x^0(i) : 1 \le i \le M\}$，且输入 $u'(k) = \phi(x(k), \xi'(k))$。

得到 Q 函数 $Q^{\theta^{\text{STD}}} = \psi^T \theta^{\text{STD}}}$ 的近似，其中最优参数通过以下步骤确定：

## 5.3 TD 学习与线性回归

(i) 引入每批次的损失函数 $\Gamma_N(\theta)$：通过公式 (5.34) 使用第 $i$ 批次 $B^i = \{u^i(k), x^i(k) : 0 \leq k \leq N\}$ 定义。

(ii) 定义 $\theta_N^{STD} = \arg\min_{\theta} \Gamma_N(\theta)$

```
$$\Gamma_N(\theta) = \frac{1}{M} \sum_{i=1}^M \Gamma_i^N(\theta). \quad (5.36b)$$
```

这种方法并没有排除对于每个 $i$ 和 $k$，$u^i(k) = \phi(x^i(k))$（同策略）。
注意，带重启的 RL 算法分析需要修改假设 $(\Lambda\Xi)$。

## 5.3.3 递归 LSTD 和 Zap

LSTD 学习通常以递归算法的形式给出：

**命题 5.5** 形式为 (5.34) 的 LSTD 学习允许递归表示：

```
$$\theta_{N+1}^1 = \theta_N^1 + G_{N+1}Y_{N+1}^1[Y_N - \Upsilon_{N+1}^1\theta_N], \quad (5.37a)$$
```

```
$G_{N+1} = G_N - \frac{1}{k_{N+1}}G_N\Upsilon_{N+1}^1G_N, \quad N \geq 0 \quad (537b)$
```

其中 $k_{N+1} = 1 + \Upsilon_{N+1}^1G_N$。

**证明** 递归是命题 5.3 的应用：令 $G_N = [W + R_N]^{-1}$，对于 $N \geq 0$，

```
$$\theta_{N+1}^1 = (N+1)\psi_{N+1}$$
```

递归 (57b) 源于矩阵求逆引理 (A.1)。为了得到 (5.37a)，我们对 $\psi_N^Y$ 使用此递归，这也由命题 5.3 意味着：

```
$(N+1)\psi_{N+1}^Y = N\psi_N^Y + \Upsilon_{N+1}^Y.$$
```

因此，

```
$$\Gamma_{N+1}^1\theta_{N+1} = (N+1)\psi_{N+1}^Y\\= N\psi_N^Y + \Upsilon_{N+1}^Y\\= G_N^1\theta_N + \Upsilon_{N+1}^Y\\= \{G_{N+1}^1 - \Upsilon_{N+1}^1\}\theta_N^1 + \Upsilon_{N+1}^Y.$$
```

每一边乘以 $G_{N+1}$ 建立了 (5.37a)。算法 (37) 可以表示为带有矩阵增益的 QSA 递归：

```
$$\theta_{N+1}^1 = \theta_N^1 + \alpha_{N+1}[Y_N - \Upsilon_{N+1}^1\theta_N]$$
```

# 值函数近似

$\alpha_N = 1/N$ 和

```
$$R_N^{-1} = \frac{1}{N} [W + \sum_{k=1}^N \Upsilon_k].$$
```

我们可能通过 ODE 方法得到了这种算法，该递归算法用于近似矩阵增益 ODE：

```
$$\partial_t \theta_t = M(\theta_t).$$
```

给定我们的损失函数目标 (33)，取 $f(\theta) = -\frac{1}{2}\Gamma(\theta)$ 且 $M$ 为正是自然的。递归 (57a) 使用 $M = E_0[\Upsilon_k \Upsilon_k^T]$ 是此 ODE 的近似。

```
$$M^{-1} = E_0[\Upsilon_k \Upsilon_k^T] = \partial^2 E_0[(\Upsilon_k \theta)^2] = \partial^2 \Gamma(\theta) = -\partial f(\theta).$$
```

因此 LSTD 是 QSA 的单尺度近似。

## 5.4 投影贝尔曼方程和 TD 算法

LSTD 面临两个计算挑战：

- (i) 如果 $d=10^7$，怎么办？机器学习从业者经常面对高维问题，并声称维度不再问题。这一成功归功于优化理论、计算机工程的进展。
- (ii) 如何将 LSTD 扩展到非线性函数近似，当每个 $\theta_t$ 是神经网络中的权重时？

在 RL 研究社区，通常修改目标以降低复杂度。一种流行的方法是创建获取*投影*规划方程解的算法。虽然缺乏理论支持，但这种观点启发的算法在神经网络近似上非常成功。

这些算法背后的动力需要更多关于函数近似的背景，这里使用 5.1 节的符号描述。我们从一个抽象开始：找到满足固定点方程的 $h^*$：

```
$$h^* = T(h^*).$$
```

$h^*$ 的定义域范围以及映射 $T$ 的含义取决于我们想要解决的问题。DP 方程 (3.5) 是其中一个例子，$h^* = J^*$。如果求解 (5.38) 不可行，我们寻求近似。

我们选择一个类 $\mathcal{H}$ 和一个映射 $P_H : \mathcal{H} \to \mathcal{H}$。即对于任何 $h \in \mathcal{H}$，$P_H(h) \in \mathcal{H}$。稍会对该映射施加更多条件。我们随后引入 (5.38) 的近似：

```
$$h = \mathcal{T}(h) \overset{\text{and}}{=} P_H\{T(h)\}.$$
```

5.4 投影贝尔曼方程和 TD 算法 

在某些情况下，这种方法失效或过于复杂，因此我们考虑另一种方案：给定第二个函数类 $\mathcal{G}$，找到一个 $h \in \mathcal{H}$ 满足：

```
$0 = P_{\mathcal{G}}(h - T(h)).$
```

这是 (39) 的推广：

**命题 5.6** 假设以下条件成立：

- (i) $\mathcal{H} = \mathcal{G}$。
- (ii) $\mathcal{H}$ 是线性的：当 $h_1, h_2 \in \mathcal{H}$ 时，$a_1h_1 + a_2h_2 \in \mathcal{H}$。
- (iii) 映射 $P_{\mathcal{H}}$ 是线性的：$a_1P_{\mathcal{H}}(h_1) + a_2P_{\mathcal{H}}(h_2) = P_{\mathcal{H}}(a_1h_1 + a_2h_2)$。

## 5.4.1 伽尔金投影

我们对 $\mathcal{G}$ 进行假设：(A1) 中引入的期望用于定义函数 $h_1, h_2: Z \to \mathbb{R}$ 的内积：

```
$\langle h_1, h_2 \rangle_{\omega} = \mathbb{E}[h_1(\Phi)h_2(\Phi)], \quad \|h_1\|_{\omega} = \sqrt{\mathbb{E}[(h_1(\Phi))^2]} = \sqrt{\langle h_1, h_1 \rangle_{\omega}}.$
```

定义 $L_{\mathcal{G}}(\omega)$ 为所有 $\|h\|_{\omega}$ 有限的函数。对于 $h \in L_2(\omega)$，到 $\mathcal{G}$ 的投影定义为：

```
$h = P_{\mathcal{G}}(h) = \arg\min_{g \in \mathcal{G}} \|g - h\|_{\omega}.$
```

最优 $h \in \mathcal{G}$ 满足正交条件：

```
$\langle h - h, g \rangle_{\omega} = 0, \quad g \in \mathcal{G}.$
```

**命题 5.7** 假设对于每个 $i$，zeta_i \in L_2(\omega)$，且这些函数在 $L_2(\omega)$ 中线性无关。也就是说，$\|	theta^T\zeta\|_{\omega} = 0$ 意味着 $	theta = 0$。
对于每个 $h \in L_2(\omega)$，存在且唯一的投影，并由 $h^* = \theta^{*T}\zeta$给出：

```
$$	theta^* = [C^{-1}]^Th.$
```

