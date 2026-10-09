
### 8.1.3.2 包含证明元素

ACSL 的扩展以及 Frama-C 的插件已经开发。它们通过添加额外注释使得指示证明局部契约成为可能。例如，以下语法：

```c
/* requires in_ellipsoid(P,vect_of_scalar(
    v_1,v_2));
 @ ensures in_ellipsoid(Q,vect_of_scalar(
    v_1,v_2,v_3));*/
 @ PROOF_TACTIC (use_strategy (Affineipsoid));
{
    // assignment of
```

建议 Frama-C 使用 `AffineEllid` 策略。

### 8.1.3.3 闭路语义：代码中的对象动态

为了表示与系统闭路行为相关的属性，需要引用对象。这是通过使用 `ghost` 变量实现的。这些变量可以像普通变量一样初始化和更新，但它们只存在于代码注释中，不会影响实际代码的结果。

## 第8章

由于我们所有的闭路分析、稳定向量裕量都是基于对象的离散（线性）表示，因此，定义对象的离散块可以生成 `ghost` 代码。在控制循环结束时，我们使用这些变量表示对象的状态更新。我们还公理地强制要求传感器的输入等于对象的输出。

### 8.1.4 PVS 中的控制语义

通过使用 ACS `ghost` 变量，可以在交互式证明器的帮助下完成注释代码的正确性验证。在 8.3 节描述的过程中，我们使用 PVS 来表示控制器的稳定性。通过向量裕量也基于对象的离散（线性）表示。

#### 8.1.4.1 基础类型和理论

在 [114] 中作为 PVS 库的一部分引入的线性代数允许通过定义类型对控制系统进行推理。例如：

- 向量类型
- 矩阵类型
- 各种矩阵子类型，如平方、对称和正定
- 块矩阵
- 行列式
- Schur 补和正定性

在 [114] 中，引入了一个名为椭圆的定理。图8.4所示的第一个定理在 PVS 中表示了通用椭圆 $G_Q$ 如何通过线性映射 $x \mapsto Mx$ 转换为 $G_{QM}$。第二个定理如图8.5所示，表示给定位于椭圆 $G_1$ 和 $G_2$ 中的向量 $x$ 和 $y$，以及乘倍因子 $\lambda_1, \lambda_2 > 0$，使得 $\lambda_1 + \lambda_2 \leq 1$，则可以说：

$$(x \ y)^T \in G_Q, \text{ 其中 } Q = \begin{pmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{pmatrix}$$

这些定理在8.3节中被大量用于证明给定 Hoare 三元组的正确性。虽然它们并不新颖，但它们 PVS 中的证明并非简单的过程，需要接近 10000 个手动证明步骤。

## 代码级验证

155

```c
ellipsoid_general: THEOREM
\forall\ (n:posnat,m:posnat, Q:SquareMat(n),
M: Mat(m,n), x:Vector[n], y:Vector[m]):
in_ellipsoid_?(n,Q,x)
IMPLIES
AND y = M*x
in_ellipsoid_?(m,M*transpose(M),y)
```

图 8.4。PVS 中的椭圆定理。

```c
ellipsoid_combination: THEOREM
\forall\ (n:posnat, lambda_1, lambda_2:
posreal, Q_1: Mat(m,n),
_2: Mat(m,m), x:Vector[n], y:Vector[m],
z: Vector[m+n]
in_ellipsoid_?(n,Q_1,x)
AND in_ellipsoid_?(m,Q_2,y)
AND lambda_1+ lambda_2 <= 1
AND z = Block2V(V2Block(n,m,n,m))
IMPLIES
in_ellipsoid_?(n+m,Block2M(M2Block(n,m,n,m)))
)(1/lambda_1*Q_1,
Zero_mat(m,n),Zero_mat(m,n),
1/lambda_2*Q_2)),z
```

图 8.5。PVS 中的椭圆组合定理。

### 8.2 生成注释：最强后置传播算法

如果有如此强大的工具，我们只需要在循环体上注释一个循环不变性：下水平 $\varepsilon p$ 的 $\mu$。遗憾的是，由于内存模型的编码复杂，证明目标往往随着语句数量的增加而增加，工具很难在大段代码中证明复杂的属性。

```c
/*@ logic matrix QMat_0 =
mat_of_2x2_scalar(1484.8760396857954,-25.78902824188802,
  -25.78902824188802,406.11067541120576);

/*@ logic matrix QMat_1 =
mat_of_2x2_scalar(1484.8760396857954,-25.78902824188802,
  -25.78902824188802,406.11067541120576);
*/

/*@ logic matrix QMat_2 =
mat_of_2x2_scalar(1484.8760396857954,-25.78902824188802,
  -25.78902824188802,406.11067541120576);
*/
```

图 8.6. 作为注解的椭圆。

因此，可以引入中间注解来表示计算对循环不变性的影响。由正定矩阵 $P$ 特征的椭圆不能包含变量之间的任何依赖关系，且中间计算可能会导致椭圆变为退化形式。退化的椭圆在二维空间中可以视觉化为一条线段。另一种方法是通过它们的 Q 形式来操纵椭圆，这是舒尔补补（Schur complement）的一种应用。

**定义 8.1 (Q 形式)。** 如果矩阵 $P^{-1}$ 存在并令 $Q=P^{-1}$，则 $x^{op}Px \le 1$ 等价于 $\begin{bmatrix} x & Q \end{bmatrix} \ge 0$，这为 Q 形式。

在提供注释时，可以将其转换为 Q 形式，并使用带有归纳契约的函数来标注循环体。然后，在每条指令之间注入 Q 形式椭圆以表示局部不变性。
接下来的图显示了运行示例自动代码输出的一部分。图 8.7 中的三个 ACSL 注解定义了矩阵变量 `QMat_0`、`QMat_1` 和 `QMat_2`。所有的矩阵变量参数化同一个椭圆，与从稳定性分析中获得并插入 Simulink 模型作为 *Ellipsoid#Stability* 观察者的椭圆相同。

# 代码层面的验证

# 157

```c
/*@
  requires in_ellipsoidQ(QMat_0,
  vect_of_2_scalar(_state_->Integrator_1_memory,
      _state_->Integrator_2_memory));
  requires \valid(_ic_) && \valid(_state_);
  ensures in_ellipsoidQ(QMat_1,
  vect_of_2_scalar(_state_->Integrator_1_memory,
      _state_->Integrator_2_memory);
*/

void discrete_timeg_no_plant_08b_compute(
  t_discrete_timeg_no_plant_08b_io *_io,
  t_discrete_timeg_no_plant_08b_state *
      _state_);
```

**图 8.7. 循环体函数契约。**

使用 ACSL 关键字 `requires` 和 `ensures`，我们可以对代码行以及函数表示前置和后置条件。图 8.7 中的 ACSL 函数契约表示了控制器状态转换函数 `discrete_timeg_no_plant_08b_compute` 插入的椭圆前置和后置条件。

在该循环函数的体内，ACSL 注解（如图 8.8 所示）操纵着中间椭圆。在这种情况下，它包含了来自函数契约注解的前置条件的副本。这是为了在函数体开始处插入的椭圆前置条件。

### 8.2 不变量的前向传播

椭圆不变性的手动正向传播在 [92] 中已有描述。我们在此回顾其基本原理。更多细节可参见 [147] 或 [145]。

#### 8.2.1 仿射变换

对于椭圆的线性传播，定义了 *AffineEllipsoid* 规则。它用于线性赋值 `\|y\|_F = Lx`，其中 `x \in \mathbb{R}^m` 是程序状态向量，`L \in \mathbb{R}^{l \times m}`。它被应用于已有的 `Q` 形式椭圆 `Q_n` 和 `Q_{n+1}`。

记得 `Q_n` 定义为 $\begin{bmatrix} 1 & x \end{bmatrix}^T Q \geq 0$，这等价于经典不等式 $x^T Q^{-1} x \leq 1$。

```c
/* @
behavior ellipsoid0_0:
  requires in_ellipsoidQ(QMat_2,
  vect_of_2_scalar(
    _state->Integrator_1_memory,
    _state->Integrator_2_memory));
  ensures in_ellipsoidQ(QMat_3,
  vect_of_2_scalar(
    _state->Integrator_1_memory,
    _state->Integrator_2_memory));
*/
```

图 8.8. 语句注解。

`Q_{n+1}` 的形式定义涉及 $\begin{bmatrix} 1 & y \end{bmatrix}^T Q \geq 0$，适用于 `y`。然而，核心思想是：

##### 8.2.1.2 S 补

舒尔补用于组合椭圆。在存在多个椭圆的情况下，我们依赖舒尔补生成更强的后置条件。这通常在 PVS 中实现，如图所示。

#### 8.2.2 后置条件的验证

在传播步骤之后，我们得到了新的后置条件。需要检查此后置条件是否蕴含插入的椭圆。这将在第10章介绍。

# 8.3 使用 PVS 消除目标

一旦生成了注释代码，还需要证明注释是正确的。图 8.9 展示了检查过程的概述。首先，Frama-C/WP 为每个霍尔三元生成验证条件，然后将其转换为 PVS。这是通过 Why3 完成的，如 8.3 节所述。

### 8.3.1 从代码到 PVS 定理

上一节描述的自动代码生成了两个 C 函数。其中一个是初始化函数，另一个实现了循环的单次执行，负责获取输入并更新状态变量和输出。实现者负责编写组合这两个函数的函数，将后者放入循环并与传感器和执行器接口以提供输入并交付输出。然而，开环和闭环稳定性以及状态边界可以通过仅考虑更新函数来建立，本节专注于此。

让我们考虑 8.10 中的注释代码。Frama-C/WP 能够刻画 `ensures` 语句的最弱前置条件并构建证明目标 $pre \implies wp(code, post)$。通过 Why3 可以将其表示为 PVS 定理。例如，图 8.10 所示的 ACSL/C 三元组变成了图 8.11 所示的定理。

注意，为了便于阅读，定理的部分假设（包括关于变量性质的假设以及源于代码早期霍尔三元组的假设）被省略了。同样注意翻译过程中出现了诸如 `malloc.0` 或 `mftlt_1` 的函数，它们描述了程序在不同执行点的内存状态。

## 代码层面的验证

161

```c
wp: THEOREM
FORALL (integrator_1_0: real):
FORALL (malloc_0: [int -> int]):
FORALL (mflt_2: [addr -> real],
  mflt_1: [addr -> real],
  mflt_0: [addr -> real])
FORALL (io_2: addr, io_1: addr,
  io_0: addr, state_2: addr,
  state_1: addr, state_0: addr);
...
=> p_in_ellipsoid(1_qmat_4,
1_vect_of_3_scalar(
  mflt_2(shift (state_2, 0)),
  mflt_2(shift (state_2, 1)),
  integrator_1_0))
=> p_in_ellipsoid(1_qmat_5,
1_vect_of_4_scalar(
  mflt_2(shift (state_2, 0)),
  mflt_2(shift (state_2, 1)),
  integrator_1_0,
  (1411/25 * integrator_1_0))
```

11. 图 8.10 所示三元组 PVS 翻译提取。

### 8.3.2 理论解释

在 ACSL 中，引入了一组最小的线性代数符号，以及定义其语义的公理。第 8.1.4 节描述了其中一些。每个生成的 PVS 定理都写在一个理论中，该理论包含了这些定义和公理的“原样”翻译，以及一些用于处理 C 程序语义的特定结构。例如，表示 2x2 矩阵行数的 ACSL 公理：

```c
/*@ axiom mat_of_2x2_scalar_row:
  @ \forall matrix A, real x0101,
  x0102, x0201, x0202;
  @ A == mat_of_2x2_scalar(x0101, x0102, x0201,
  x0202) =>=
  @ mat_row(A) == 2; /*
```

第 8 章在翻译为 PVS 后变为：

```c
q_mat_of_2x2_scalar_row:
AXIOM FORALL(x0101:real, x0102:real, x0201_0:
  real, x0202_0:real):
  FORALL(a_0:a_matrix):
  (a_0 = 1_mat_of_2x2_scalar(x0101_0, x0102_0,
  x0201_0, x0202_0)) ->
  (2 = 1_mat_row(a_0))
```
