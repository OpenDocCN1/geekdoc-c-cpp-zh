
注意它对应于定义在误差项序列 $(\epsilon_1, \epsilon_2)$ 之上的元组向量：

```math
$x = \begin{pmatrix} -1, (1, -1)^\top \ 0 & 0 \end{pmatrix}, 0, 0, 0, \ y = \begin{pmatrix} 1, (0, 2)^\top \ 1/2 & 0 \end{pmatrix}, 0, 0, 0.$
```

图 9.4 表示了它的几何解释，一个二次分区区域。
令 $\mathcal{Z}_{P^m}^p$ 为维度为 $p$ 的二次向量集：$(q^p) \in \mathcal{Z}_{P^m}^p = (c^p, (b^p)_m, (A^p)_{m^2}, \epsilon_1^p, \epsilon_2^p, \dots, \epsilon_m^p) \in \mathbb{R}^{p \times m} \times \mathbb{R}^{p \times m \times m} \times \mathbb{R}^{p \times m \times m} \times \mathbb{R}^p \times \mathbb{R}^p \times \mathbb{R}^p$。
分区域是一个参数化的关系域，由 $m$ 个误差项的向量参数化。在实践中，它模拟了基于抽象 $\mathcal{Z}_{P^m}^p$ 的 $\ell(\mathbb{R}^p)$ 的非关系域。算子为：
(i) 将分区区域的变量赋值为由算术表达式定义的新值，具有 $Q$ 中表达式的语义和二次向量中的替换；(ii) 守卫评估，即对分区区域的约束，使用表达式的正向和反向评估的经典组合 [49, §2.4]。

## 几何解释与包框投影

可以将几何解释考虑为二次向量到二次分区区域的具象化。从现在起，对于所有 $n \in \mathbb{N}$，$[n]$ 表示集合 $\{1, \dots, n\}$。

### 定义 9.17

具象化映射 $\gamma_{Z_q}: Z_q^m \mapsto \wp(\mathbb{R}^p)$ 为所有 $q = (q_1, \dots, q_p) \in Z_q^m$ 定义为：

```math
$\gamma_{Z_q}(q) = \left\{ x \in \mathbb{R}^p \middle| \begin{matrix} t \in C^m \ \text{s.t.} \ \forall k \in [p], \ x_k = q_k(t)\end{matrix} \right\}$
```

### 备注 9.18

显式地作为约束集来描述此类 $\mathbb{R}^p$ 的子集并不容易。经典的（仿射）分区区域是多面体（超立方体）通过仿射映射的像，因此它是多面体，可以通过仿射不等式的取交来表示。对于二次向量，尚未证明存在由最多多项式不等式的取交的表示。这使得二次集的具象化计算变得困难。为了方便对计算值的后者的解释，我们依赖于包框的原始投影：二次向量的每个二次型都使用 $\gamma_Q$ 具象化为区间。

## 序结构与上界

我们为二次向量配备了一个依赖于映射 $\gamma_{Z_q}$ 提供的几何包含关系的预序。

### 定义 9.19

$Z_q^m$ 上的预序 $\sqsubseteq_{Z_q}$ 定义为：

```math
$x \sqsubseteq_{Z_q} y \Longiff \gamma_{Z_q}(x) \subseteq \gamma_{Z_q}(y).
```
