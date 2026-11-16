
上面的定义可以在 HOL4 中形式化如下：

```
⊢ ∀ p1 p2 X B Y. conditional_belief_vulnerability p1 p2 X B Y =
Σ y Σ b joint distribution p1 B Y (( b ) , { y }) * 1 / Γ b,y *
Σ z:T_a . belief_conditional_distribution p1 X Y B (( x ) , { y } , { b })
```

现在，我们可以应用逆对数来得到条件信念最小熵。

H∞ (X | Y : B) = – log ( V (X | Y : B))

基于之前的度量，我们定义了信息泄漏，用于确定从输入到输出泄漏了多少信息。

信息泄漏 = 初始不确定性 - 剩余不确定性

接下来，我们将使用本节提出的定义，对它们的经典性质进行形式化推理，从而允许我们使用 HOL4 定理证明器进行形式化信息流分析。

## 10.3 信息流的形式化分析

本章的主要重点是对一次猜测关键信息的威胁模型进行分析，这通常被认为是最坏情况场景，如前所述，香农熵无法处理这种情况。在本节中，我们将正式验证前一节提出的定义可以处理这种特定模型。

关于信息流模型，Min-Entropy（Mhamdi, Hasan & Tahar, 2011）允许我们测量不确定性。以下定理提供了初始不确定性的下界。

### 定理 10.1

```
|- ∀ X p b. FINITE (Ω) ∧ Ω ≠ ∅ ∧ random_variable X p Borel ∧
(∀ x. x ∈ X (Ω) ∧ (distribution p X { x }) ≤ 1/2^p )) ∧
(∀ x. x ∈ Ω ⇒ (x) ∈ events p) ∧
X (Ω) ∈ subsets Borel) ⇒
b ≤ (min entropy X p)
```

其中 Ω = p_space P。如果这种初始不确定性在输入集 X 上均匀分布，则初始不确定性等于 | X |：

### 定理 10.2

```
|- ∀ X p. FINITE (Ω) ∧
random_variable X p Borel ∧
∀ x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / | X (Ω) |
⇒ min_entropy X p = log | X (Ω) |
```

上述定理中的第一个假设是必需的，因为集合的最大值仅在有限集合中才有定义。

与信息泄漏相关的另一个有用方面是剩余不确定性，它表示事后行为的模型。如果程序是确定性的且初始分布是均匀分布，则其信息泄漏仅取决于输出集。此结果可以形式化验证为以下定理：

### 定理 10.3

```
|- ∀ X Y p c. (∀x. x ∈ X (Ω) ⇒ distribution p X { x } = 1 / |X(Ω)| ∧
Deterministic_cond Y c ⇒
Information_leakage p X Y = log ( | Y (Ω) | )
```

其中假设模拟了确定性条件和均匀分布。接下来，我们分析考虑攻击者信念的信息流。为此，我们引入另一个随机变量 B，用于建模对手关于高输入的额外知识。在完全不准确信念的条件下，以下定理成立：

### 定理 10.4

```
|- ∀ B sp ev p1 p2. FINITE (p_space (sp, ev, p2)) ∧
FINITE (p_space (sp, ev, p1)) ∧
∀a b. (a, b) ∈ totally_inaccurate_belief_set sp ev p1 p2 A B ⇒
Belief_min_entropy sp ev p1 p2 A B = +∞
```

根据上述定理，当攻击者对秘密输入没有任何信息时，系统的初始脆弱性趋于零。此结果的证明基于贝叶斯规则和我们对信念最小熵的定义。

以下定理验证了条件最小熵始终小于或等于信念最小熵。

### 定理 10.5

```
|- ∀ X B sp ev p1 p2.
∀ x b. (b ∈ B (Q)) ∧
(belief_set (sp, ev, p1) (sp, ev, p2) X B b ≠ ∅) ∧
(x ∈ (belief_set (sp, ev, p1) (sp, ev, p2) X B b)) ∧
conditional_distribution (sp, ev, p1) B X (( b ), ( x )) ≤ 1 / |B(Q)| ⇒
min_entropy X (sp, ev, p1) ≤ belief_min_entropy sp ev p1 p2 X B
```

先前结果的解释是，在存在额外知识的情况下，系统的脆弱性更大。同样，以下定理提供了确定性情况下的信念初始不确定性。

### 定理 10.6

```
|- ∀ X B sp ev p1 p2 c.
∀ x b. x ∈ belief_set (sp, ev, p1) (sp, ev, p2) X B b ∧
b ∈ B (Q) ∧
∀ x. (x ∈ belief_set (sp, ev, p1) (sp, ev, p2) X B b) ∧
distribution (sp, ev, p1) X (x) = 1 / |X(Q)| ∧
events (sp, ev, p1) = POW (Q) ∧
deterministic_cond B c ⇒
log |X(Q)| / |B(Q)| ≤ belief_min_entropy sp ev p1 p2 X B
```

接下来，就像在 Min-Entropy 的情况中一样，我们验证剩余信念不确定性由条件最小熵与对手信念联合下界，即 H∞(A | O, B) ≤ H∞(A | O : B)，可以表示为以下 HOL4 定理：

### 定理 10.7

```
|- ∀ X B Y p1 p2. FINITE (Q) ∧ random_variable X p1 Borel ∧
Random_variable B p1 Borel ∧ random_variable Y p1 Borel ∧
∀ x. x ∈ (Q) ⇒ { x } ∈ events p1
⇒ conditional_joint_min_entropy p1 X B Y ≤
Conditional_belief_min_entropy p1 p2 X B Y
```

因此，在确定性条件下，信念剩余不确定性由 log (|X|/|Q|) 界定。现在我们可以在 HOL4 中正式验证以下结果：

### 定理 10.8

```
|- ∀ X Y B p q c c'. FINITE Q ∧ Q ≠ {} ∧
∀ x b y. x ∈ belief_conditioned_set p q X B Y b y ∧
∀ b. b ∈ B (Q) ∧ ∀ y. y ∈ Y (Q) ∧
∀ x. x ∈ Q ⇒ { x } ∈ events p ∧
∀ x. x ∈ X (Q) ⇒ distribution p X { x } = 1 / |X(Q)| ∧
Deterministic_cond Y c ∧ deterministic_cond B c' ⇒
log |X(Q)| / |Y(Q)| / |B(Q)| ≤ conditional_belief_min_entropy p q X B Y
```

其中 belief_conditioned_set p q X B Y b y = Γb.y 表示根据对手的信念和低观测，对手可能选择的集合。

上述定理的证明主要基于确定性条件下的 Min-Entropy 性质。最后，定理 10.6 和 10.8 可用于对确定性程序的信念信息泄漏进行推理。

```
log | Y | ≤ I_L(X; (Y: B)) (10.2)
```

根据上述结果，我们得出结论：信念行为有助于对手根据观测选择更可靠的初始知识。上述提到的性质之前已被验证，但我们工作的主要新颖之处在于使用交互式定理证明器重新验证了这些结果。基于定理证明的可靠性，形式化验证的定理保证准确且包含所有必需的假设。此外，这些形式化验证的结果可以在定理证明器的可靠内核之上，用于对各种应用的信息流分析进行推理。为说明目的，下一节将形式化分析级联信道的信息泄漏。这些额外优势是以形式化和交互式验证上述结果所需的人力努力为代价获得的。证明脚本由 3400 行代码组成，开发时间约为 1000 人时。

## 10.4 应用：级联信道

信道是一个三元组 (A, B, CAB)，其中 A 是关键输入的有限集合，B 是可观测输出，CAB 是表示从输入到输出的转换概率的信道矩阵。信道经常以级联方式连接，使得前一阶段的输出作为下一阶段的输入。在级联信道中，最终输出在 n 个步骤中产生，其中 n 表示级联信道的数量。

本节的主要目标是对级联信道的信息流进行形式化推理，并分析此类系统中的信息泄漏。我们将首先在高阶逻辑中形式化信道和级联信道的概念。这些定义，连同前一节的形式化验证结果，将随后用于对两个级联信道模型的信息量度和信息泄漏进行形式化推理。

### 10.4.1 信道和级联信道的形式化

信道可以使用以下函数在 HOL4 中形式化：

### 定义 10.5

```
∀ X Y p f. channel p X Y f =
Random_variable X p Borel ∧
Random_variable Y p Borel ∧
∀ x y. x ∈ X (Ω) ∧
y ∈ Y (Ω) ∧
f (x, y) = conditional_distribution p Y X ({y}, { x })
```

谓词 channel 接受一个概率空间 p，表示关键输入和可观测输出的有限集合的随机变量 X 和 Y，以及一个函数 f，该函数以获取输出 b 的条件概率来模拟信道矩阵 CAB，使得输入为 a。

现在，两个信道的级联行为，即 (X, Z, CXZ) 和 (Z, Y, CZY)，等价于信道 (X, Y, CXZ * CZY)。两个信道级联的定义可以在 HOL4 中形式化如下：
