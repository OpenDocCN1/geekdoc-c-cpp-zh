
## 5.4.3 最小槽位需求（蜂窝网络）

设 $D_7^{(2)}(G)$ 为一个蜂窝 Distance 2 团 $G=(V,E)$ 中所有小区的需求之和，$|V|\leq 7$。则 $D_7^{(2)}(G)=\sum_{i\in G}w_i$，其中 $w_i$ 为小区 $i$ 的需求。

**定义 10.** 一个由最多七个小区组成的七节点蜂窝 Distance 2 团 $G$ 或其子图，称为 *critical block* $CB_7$，其节点数最大为七，且其内小区的需求之和在所有可能的蜂窝 Distance 2 团中达到最大。

我们用 $D_7^{(2)*}$ 表示 critical block 的需求，即 $D_7^{(2)*}=\max_{\forall G}D_7^{(2)}(G)$。注意，网络中可能存在多个蜂窝 Distance 2 团。

我们首先考虑需求均匀的情况，即所有小区的需求相同。

# 5.4.4 均匀小区需求

令 $w$ 表示网络中所有小区的统一需求。当 $w=1$ 时，critical block 的需求 $D_7^{(2)*}$ 为七个时隙。参考图 5.5(a)，由于结构对称性，任何 Distance 2 团都可以作为 critical block。若不失一般性，设蜂窝 Distance 2 团 $abcdefg$ 为七节点 critical block，节点 $g$ 为中心节点。再考虑以节点 $c$ 为中心的 Distance 2 团 $gbpqrdc$，我们观察到：

- 节点 $p$ 距离节点 $e$ 与 $f$（属于 $CB_7$）为 3，因此 $p$ 可以使用与 $e$ 或 $f$ 相同的时隙。

- 节点 *q* 距离节点 *a*、$f$ 与 $e$ 为 3，故 *q* 的需求可以由这三个节点中的任意一个满足。

- 节点 *a* 与 *f* 距离节点 *r* 为 3。

一个可能的分配方案是将节点 *p* 与节点 *e* 使用相同的时隙，而节点 *q* 与 *r* 分别使用节点 *f* 与 *a* 的时隙。

因此，我们发现，Distance 2 团 $gbpqrdc$ 的需求可以完全由 critical block 所分配的时隙满足。图 5.5(b) 展示了一个可能的分配方案。

我们现在给出以下结果。

**Lemma 20.** 对于任意一个未满足的节点 *u*，若它与一个或多个已满足的蜂窝 Distance 2 团相邻，则总能在距离 3 的节点 *v* 处找到一个已满足的节点，使得 *v* 所分配的时隙在 *u* 的 Distance 2 范围内是空闲的。

**证明。** 根据定义，蜂窝 Distance 2 团是七节点的子图，其内部任意两节点之间的距离不超过 2。若节点 *u* 与子图中的节点 *v* 相邻，则可以直观看出，在该子图中至少有两个节点距离 *u* 为 3。因此，*u* 可以使用这些距离 3 节点所对应的时隙进行分配，而不会违背时隙分离约束。

基于 Lemma 20，我们接下来证明：

**定理 20.** 对于具有两层缓冲、缓冲容量分别为 $s_0 = s_1 = s_2$ 且小区均要求一个时隙的蜂窝图，其最小时隙需求等于七节点 critical block 的需求。

**证明.** 设 $G^*$ 为网络的 critical block，节点 $g$ 为中心节点。设 $G$ 为与 $G^*$ 相邻的蜂窝 Distance 2 团，其节点需要分配时隙。由于 $G$ 与 $G^*$ 相邻，四个公共节点已分配时隙。根据 Lemma 20，对于 $G$ 中剩余的节点，蜂窝图的对称性保证：对于任意节点 *i* ∈ $G$，总能在距离 3 的节点 *j* 处找到一个已满足的节点，且 *j* 的时隙在 *i* 的 Distance 2 范围内是空闲的。因此，$G$ 可以仅使用 $G^*$ 中的时隙来满足。

上述过程可以对 $G^*$ 相邻的所有 Distance 2 团重复进行，从而得到一个无冲突的时隙分配，仅使用七个时隙。利用蜂窝图的对称性，该模式可以在网络中通过对每个已满足的 Distance 2 团考虑其相邻的未满足 Distance 2 团来循环使用。

# **Theorem 20.** *The minimum slot requirement of a cellular graph with two-cell buffering having s₀ = s₁ = s₂ and a homogeneous demand of one time slot per cell is equal to the demand of the seven-node critical block of the graph.*

**Proof.** Let G* be the critical block of the network with node *g* as the central node. Let G be a cellular Distance 2 clique adjacent to G*, whose nodes must be assigned time slots. As G is adjacent to G*, the four common nodes of G and G* have already been assigned time slots. From Lemma 20, for the remaining nodes in G we observe that the symmetry of the cellular graph implies that for any node *i* in G, it is always possible to find at least one satisfied node *j* at Distance 3 from *i* such that the time slot assigned to *j* is unused within Distance 2 of node *i*. Hence, G can be satisfied using only the time slots from G*.

The above procedure can be repeated for all cellular Distance 2 cliques adjacent to G* to obtain a collision‑free schedule using only seven time slots. By exploiting the symmetry of the cellular graph, this pattern can be repeated over the network by considering unsatisfied cellular Distance 2 cliques adjacent to each satisfied cellular Distance 2 clique.

# **Theorem 20.** *The minimum slot requirement of a cellular graph with two-cell buffering having s₀ = s₁ = s₂ and a homogeneous demand of one time slot per cell is equal to the demand of the seven-node critical block of the graph.*

**Proof.** Let G* be the critical block of the network with node *g* as the central node. Let G be a cellular Distance 2 clique adjacent to G*, whose nodes have to be assigned time slots. As G is adjacent to G*, the four common nodes of G and G* have already assigned time slots. From Lemma 20, for the remaining nodes in G we observe that the symmetry of the cellular graph implies that for any node *i* in G, it is always possible to find at least one satisfied node *j* at Distance 3 from *i* such that the time slot assigned to *j* is unused within Distance 2 of node *i*. Hence, G can be satisfied using only the time slots from G*.

The above procedure can be repeated for all cellular Distance 2 cliques adjacent to G* to obtain a collision‑free schedule using only seven time slots. By exploiting the symmetry of the cellular graph, this pattern can be repeated over the network by considering unsatisfied cellular Distance 2 cliques adjacent to each satisfied cellular Distance 2 clique.

# 5.4.4.2  Algorithm homogeneous_slot_assignment

+   **Step 1:** 为 critical block 的中心小区分配时隙编号 $(0, w-1)$。

+   **Step 2:** 对于位于中心小区右侧（沿水平方向，如图 5.5(b) 所示）的第 $i$ 个小区，分配时隙编号 $(iw, (i+1)w-1) \bmod 7w$，其中 $i \ge 1$。即依次分配 $(0, w-1), (w, 2w-1), \ldots, (6w, 7w-1)$ 给沿水平方向右侧的小区。

+   **Step 3:** 对于位于中心小区左侧的第 $i$ 个小区，分配时隙编号 $(-iw, -(i-1)w-1) \bmod 7w$，其中 $i \ge 1$。即依次分配 $(7w-1, 6w), (6w-1, 5w), \ldots, (w-1, 0)$ 给沿水平方向左侧的小区。

+   **Step 4:** 对于位于中心小区下方的行，将 $(0, w-1)$ 的时隙值向左平移 3 个单元后，再重复步骤 2 和 3，为每行分配时隙。

+   **Step 5:** 对于位于中心小区上方的行，将 $(0, w-1)$ 的时隙值向右平移 3 个单元后，再重复步骤 2 和 3，为每行分配时隙。

# 5.4.5  异构小区需求

我们现在考虑 SAP 的一般情况，即小区的需求各不相同，即存在 $w_i, w_j$（$i \neq j$）使得 $w_i \neq w_j$。七节点 critical block 不足以确定蜂窝图的最优时隙数量，如下例所示。

**Example 24.** *Consider the cellular graph in Figure 5.7. The numbers in parentheses beside each cell denote the demand of the cell. The cellular Distance 2 clique $abfjhde$ has a demand of 62 slots. The subgraphs $bcgjief$ and $abcfe$ have demands of 61 and 62 time slots, respectively. Thus, we see two candidate critical blocks in the network: subgraph $abfjhde$ or subgraph $abcfe$. We arbitrarily choose $abfjhde$ as a seven‑node critical block. For the Distance 2 clique $bcgjief$ adjacent to the critical block, cells $g$ and $j$ can have their demands satisfied from the slots assigned to cells $a$ and $d$. However, the demand of cell $c$ ($w_c = 12$) is greater than the slots assigned to its two Distance 3 neighbors, $d$ and $h$, of the seven‑node critical block. The sum of the demands of cells $d$ and $h$, $w_d + w_h = (4 + 6) < w_c = 12$. Hence, it is necessary to assign additional slots beyond those allocated to the critical block to satisfy the demand of cell $c$. Thus, for heterogeneous demands, the seven‑node critical block will not always give the optimal number of slots of the cellular network. Figure 5.8

