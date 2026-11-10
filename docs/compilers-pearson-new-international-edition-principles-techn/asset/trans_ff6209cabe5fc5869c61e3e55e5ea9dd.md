
## §9.7.4 关于传递函数的必要假设

为了使基于区域的分析能够工作，我们需要对框架中传递函数集合的性质作出某些假设。具体来说，我们需要传递函数上的三种基本操作：复合、交和闭包；对于使用迭代算法的数据流框架，只需要第一种操作。

### 复合

一系列节点的传递函数可以通过复合表示各个节点的函数来推导。设 *f₁* 和 *f₂* 是节点 *n₁* 和 *n₂* 的传递函数。执行 *n₁* 后接 *n₂* 的效果由 *f₂* ∘ *f₁* 表示。函数复合已在 9.2.2 节讨论，使用到达定义的例子已在 9.2.4 节给出。回顾一下，设 *genᵢ* 和 *killᵢ* 为 *fᵢ* 的 *gen* 和 *kill* 集。那么：

$$f_2 \circ f_1(x) = gen_2 \cup ((gen_1 \cup (x - kill_1)) - kill_2)$$

$$= (gen_2 \cup (gen_1 - kill_2)) \cup (x - (kill_1 \cup kill_2))$$

因此，*f₂* ∘ *f₁* 的 *gen* 和 *kill* 集分别为 *gen₂* ∪ (*gen₁* − *kill₂*) 和 *kill₁* ∪ *kill₂*。同样的思路适用于任何 gen-kill 形式的传递函数。其他传递函数也可能封闭，但我们必须分别考虑每种情况。

### 交（Meet）

这里，传递函数本身是带有交运算符 ∧ 的半格的值。两个传递函数 *f₁* 和 *f₂* 的交 *f₁* ∧ *f₂* 定义为 (*f₁* ∧ *f₂*)(*x*) = *f₁*(*x*) ∧ *f₂*(*x*)，其中 ∧ 是数据流值的交运算符。传递函数上的交运算符用于合并具有相同终点的不同执行路径的效果。在不引起歧义的情况下，从现在起，我们也把传递函数的交运算符称为 ∧。对于到达定义框架，有

$$(f_1 \land f_2)(x) = f_1(x) \land f_2(x)$$

$$= (gen_1 \cup (x - kill_1)) \cup (gen_2 \cup (x - kill_2))$$

$$= (gen_1 \cup gen_2) \cup (x - (kill_1 \cap kill_2))$$

也就是说，*f₁* ∧ *f₂* 的 *gen* 和 *kill* 集分别为 *gen₁* ∪ *gen₂* 和 *kill₁* ∩ *kill₂*。同样，该论证适用于任何 gen-kill 传递函数集合。

- 要取传递函数的交，取各 *gen* 的并集和各 *kill* 的交集。
- 要复合传递函数，取各 *gen* 的并集以及各 *kill* 的并集。但例外的是，一个表达式如果由第一个函数生成、不由第二个函数生成、却被第二个函数杀死，则不在结果的 *gen* 中。
- 要取传递函数的闭包，保留其 *gen*，并将 *kill* 替换为 ∅。

前五个区域 $R_1,\ldots,R_5$ 分别是块 $B_1,\ldots,B_5$。对于 $1 \le i \le 5$，$f_{R_i,\mathrm{IN}[B_i]}$ 是恒等函数，而 $f_{R_i,\mathrm{OUT}[B_i]}$ 是块 $B_i$ 的传递函数：

$$f_{B_i,\mathrm{OUT}[B_i]}(x) = (x - kill_{B_i}) \cup gen_{B_i}.$$

| 区域 | 传递函数 | gen | kill |
|---|---|---|---|
| R4 | $f_{R4,\mathrm{IN}[R2]} = I$ | $\emptyset$ | $\emptyset$ |
| R4 | $f_{R4,\mathrm{OUT}[B2]} = f_{R2,\mathrm{OUT}[B2]} \circ f_{R4,\mathrm{IN}[R2]}$ | $\{d_1\}$ | $\{d_1\}$ |
| R4 | $f_{R4,\mathrm{IN}[R3]} = f_{R4,\mathrm{OUT}[B2]}$ | $\{d_4\}$ | $\{d_1\}$ |
| R4 | $f_{R4,\mathrm{OUT}[B3]} = f_{R3,\mathrm{OUT}[B3]} \circ f_{R4,\mathrm{IN}[R3]}$ | $\{d_1,d_5\}$ | $\{d_1,d_5\}$ |
| R4 | $f_{R4,\mathrm{IN}[R4]} = f_{R4,\mathrm{OUT}[B3]} \wedge f_{R4,\mathrm{OUT}[B2]}$ | $\{d_4,d_5\}$ | $\{d_1\}$ |
| R4 | $f_{R4,\mathrm{OUT}[B4]} = f_{R4,\mathrm{OUT}[B3]} \circ f_{R4,\mathrm{IN}[R4]}$ | $\{d_1,d_5,d_6\}$ | $\{d_1,d_2\}$ |
| R5 | $f_{R5,\mathrm{IN}[R4]} = f_{R4,\mathrm{OUT}[B4]}$ | $\{d_4,d_5,d_6\}$ | $\emptyset$ |
| R5 | $f_{R5,\mathrm{OUT}[B5]} = f_{B5,\mathrm{OUT}[B5]} \circ f_{R5,\mathrm{IN}[B5]}$ | $\{d_1,d_3\}$ | $\{d_1,d_3\}$ |
| R5 | $f_{R5,\mathrm{OUT}[B4]} = f_{R5,\mathrm{OUT}[B5]} \circ f_{R5,\mathrm{IN}[R4]}$ | $\{d_4,d_5,d_6\}$ | $\{d_1,d_2\}$ |
| R6 | $f_{R6,\mathrm{IN}[R1]} = I$ | $\emptyset$ | $\emptyset$ |
| R6 | $f_{R6,\mathrm{OUT}[B1]} = f_{R1,\mathrm{OUT}[B1]}$ | $\{d_1,d_2,d_3\}$ | $\{d_4,d_5,d_6\}$ |
| R6 | $f_{R6,\mathrm{IN}[R1]} = f_{R6,\mathrm{OUT}[B1]}$ | $\{d_1,d_2,d_3\}$ | $\{d_4,d_5,d_6\}$ |
| R6 | $f_{R6,\mathrm{OUT}[B5]} = f_{R6,\mathrm{OUT}[B1]} \circ f_{R6,\mathrm{IN}[R1]}$ | $\{d_1,d_3\}$ | $\{d_1,d_3\}$ |
| R6 | $f_{R6,\mathrm{OUT}[B4]} = f_{R6,\mathrm{OUT}[B5]} \circ f_{R6,\mathrm{IN}[R1]}$ | $\{d_1,d_2\}$ | $\{d_1,d_2\}$ |
| R6 | $f_{R6,\mathrm{IN}[R4]} = f_{R6,\mathrm{OUT}[B4]}$ | $\{d_2,d_3,d_4,d_5,d_6\}$ | $\{d_1\}$ |
| R6 | $f_{R6,\mathrm{OUT}[B5]} = f_{R6,\mathrm{OUT}[B4]} \circ f_{R6,\mathrm{IN}[R4]}$ | $\{d_2,d_3,d_4,d_5,d_6\}$ | $\{d_1\}$ |

图 9.51：使用基于区域的分析计算图 9.48(a) 中流图的传递函数

算法 9.53 的步骤 2 中构造的其余传递函数汇总于图 9.51。区域 R6 由区域 R2、R3 和 R4 组成，表示循环体，因此不包括回边 $B_4 \rightarrow B_2$。处理这些区域的顺序将是拓扑顺序：$R_2, R_3, R_4$。首先，$R_2$ 在 $R_6$ 内没有前驱；记住边 $B_4 \rightarrow B_2$ 通向 $R_6$ 外部。因此，$f_{R_6,\mathrm{IN}[B_2]}$ 是恒等函数¹¹，而 $f_{R_6,\mathrm{OUT}[B_2]}$ 是块 $B_2$ 本身的传递函数。

区域 $B_3$ 的头部在 $R_6$ 内有一个前驱，即 $R_2$。到其入口的传递函数就是到 $B_2$ 出口的传递函数 $f_{R_6,\mathrm{OUT}[B_2]}$，它已经计算过了。我们将此函数与 $B_3$ 在其自身区域内的传递函数复合，以计算到 $B_3$ 出口的传递函数。

最后，对于到 $R_4$ 入口的传递函数，我们必须计算

$$f_{R_6,\mathrm{OUT}[B_2]} \wedge f_{R_6,\mathrm{OUT}[B_3]}$$

因为 $B_2$ 和 $B_3$ 都是 $B_4$（$R_4$ 的头部）的前驱。将此传递函数与传递函数 $f_{R_4,\mathrm{OUT}[B_4]}$ 复合，得到所需的函数 $f_{R_6,\mathrm{OUT}[B_4]}$。例如注意，$d_3$ 在此传递函数中未被杀死，因为路径 $B_2 \rightarrow B_4$ 没有重新定义变量 $a$。

现在考虑循环区域 $R_7$。它只包含一个表示其循环体的区域 $R_6$。由于只有一条指向 $R_6$ 头部的回边 $B_4 \rightarrow B_2$，表示循环体执行 0 次或多次的传递函数就是 $f_{R_6,\mathrm{OUT}[B_4]}$：其 gen 集为 $\{d_4, d_5, d_6\}$，kill 集为 $\emptyset$。区域 $R_7$ 有两个出口，即块 $B_3$ 和 $B_4$。因此，将此传递函数与 $R_6$ 的每个传递函数复合，得到 $R_7$ 相应的传递函数。例如注意，由于存在诸如 $B_2 \rightarrow B_4 \rightarrow B_2 \rightarrow B_3$，甚至 $B_2 \rightarrow B_3 \rightarrow B_4 \rightarrow B_2 \rightarrow B_3$ 这样的路径，$d_6$ 会出现在 $f_{R_7,\mathrm{OUT}[B_3]}$ 的 gen 集中。

最后，考虑 $R_8$，即整个流图。其子区域是 $R_1$、$R_7$ 和 $R_5$，我们将按该拓扑顺序考虑它们。如前所述，传递函数 $f_{R_8,\mathrm{IN}[B_1]}$ 就是恒等函数，而传递函数 $f_{R_8,\mathrm{OUT}[B_1]}$ 就是 $f_{R_1,\mathrm{OUT}[B_1]}$，后者又是 $f_{B_1}$。

$R_7$ 的头部是 $B_2$，它只有一个前驱 $B_1$，因此到其入口的传递函数就是区域 $R_8$ 中从 $B_1$ 出去的传递函数。我们将 $f_{R_8,\mathrm{OUT}[B_1]}$ 与 $R_7$ 内到 $B_2$ 和 $B_4$ 出口的传递函数复合，以获得它们在 $R_8$ 内相应的传递函数。最后，我们考虑 $R_5$。其头部 $B_5$ 在 $R_8$ 内有两个前驱，即 $B_3$ 和 $B_4$。因此，我们计算 $f_{R_8,\mathrm{OUT}[B_3]} \wedge f_{R_8,\mathrm{OUT}[B_4]}$ 以得到 $f_{R_8,\mathrm{IN}[B_5]}$。由于块 $B_5$ 的传递函数是恒等函数，所以 $f_{R_8,\mathrm{OUT}[B_5]} = f_{R_8,\mathrm{IN}[B_5]}$。

步骤 3 根据传递函数计算实际的到达定义。在步骤 3(a) 中，$\mathrm{IN}_{R_8}[B_1] = \emptyset$，因为程序开始时没有到达定义。图 9.52 展示了步骤 3(b) 如何计算其余数据流值。从 $R_8$ 起点到其每个子区域起点的传递函数已经

¹¹严格来说，我们指的是 $f_{R_6,\mathrm{IN}[R_2]}$，但当像 $R_2$ 这样的区域是单个块时，在这种情况下使用块名而不是区域名通常更清楚。
