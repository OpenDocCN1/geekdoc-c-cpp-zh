
# 图 4.10: 相邻节点的后续区域的精炼

$PQ + QT$，由此可得结果为 $QT = r_{u_{j-1},u_j}$。然而，如果点 $T$ 位于 $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$ 中的弧线/线段上，且不平行于 $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$ 中的任何弧线/线段，则从 $T$ 导出的对应点 $Q$ 在 $R'_{u_{j-1}}$ 上必须是两条不同弧线和/或线段的交点，如上文所述。没有失去一般性，设 $Q$ 为弧线 $\alpha$ 和 $\delta$ 在 $E^{u_{j-1}}_{u_0,u_1\ldots u_{j-2}}$ 中的交点（如图 4.10 所示）。弧线 $\delta$ 被映射到 $E^{u_j}_{u_0,u_1\ldots u_{j-1}}$ 中的平行弧线 $\eta$。设弧线 $\gamma$ 和 $\eta$ 的交点为 $T'$。因此，直线 $QT'$ 垂直于弧线 $\delta$ 的切线，从而 $\triangle PQT$ 为钝角三角形，钝角位于点 $Q$ 处。这意味着距离 $PT$ 大于 $PQ$ 或 $QT$ 中的任意一个，因此推论成立。

因此，我们看到，由 $u_0$ 开始的区域计算所引起的相邻节点 $u_j$（其中 $1 \le j \le k$）的边界部分（即被修改/精炼的部分）距离 $R_{u_0}$ 中导致该精炼的对应部分至少为 $r_{u_0,u_1}$。因此，我们得到以下重要结果，该结果保证了逐进精炼方案的终止。

# 定理 13.

*如果节点* $u$ *利用其所有邻居的范围读数来启动其区域计算，* 则节点 $u$ 计算出的区域 $R_u$ *可能会通过整个网络的后续邻居引起精炼，* 但它永远无法进一步精炼 $u$ 本身的 $R_u$。

# 定义 3.

节点 $u$ 的稳定居住区域是指使用网络中所有节点对的当前全局范围读数，对 $u$ 的最小居住区域进行最小改进后的区域。我们用 $S_u$ 表示该区域。

# 定理 14.

*节点* $u$ *在获得网络中所有直接通信节点的范围读数以及所有节点的初始区域信息后，即可计算其稳定居住区域。*

*证明.* 节点 $u$ 的最小居住区域仅在至少一个邻居（设为 $v$）能够改进其居住区域时才能被精炼。这又取决于 $v$ 的邻居（除 $u$ 外）是否能改进其居住区域，以此类推。过程会持续进行，直到网络中所有节点的居住区域都被评估为是否可以改进。因此，如果 $u$ 拥有来自所有这些更新的必要信息，$u$ 最终能够计算其稳定居住区域。

# 定理 15.

*所有节点的稳定居住区域的计算在功能上等价于网络中所有节点对的范围信息的全局广播（即集合 $RR$ 和集合 $Re_{fn}$）。*

*证明.* 要在中心重构自适应网络图，需要两类信息：i) 所有节点对的测量范围；ii) 每个节点是否为参考节点。从定理 14 可知，如果节点拥有网络中所有节点对的范围值（集合 $RR$）和集合 $Re_{fn}$，则可以本地构建网络图并计算所有节点的稳定居住区域。由于节点在网络中拥有集合 $RR$ 和集合 $Re_{fn}$ 等价于广播这两类信息，若每个节点都本地计算稳定居住区域，则问题等价于所有节点的全局广播集合 $RR_i$ 和每个节点 $i$ 的状态（是否为参考节点）。每个节点在收到邻居传来的信息后，会附带自身的 $RR_i$ 集合和状态一起广播该消息。□

# 4.5.2 区域估计算法

网络中每个节点维护一个本地变量 $status$，若节点为参考节点则设为 1，否则设为 0。初始时，所有非参考节点的最小居住区域被假设为无穷大。每个节点 $i$ 与其邻居进行测距以获取测量范围集合 $RR_i$，随后计算对每个 $j \in N(i)$ 的居住区域视图 $R_{ji}$。节点 $i$ 然后与每个邻居 $j \in N(i)$ 交换三类信息：i) 变量 $status_i$ 的值；ii) $j$ 的居住区域视图 $R_{ji}$；iii) 节点 $i$ 当前最小居住区域的面积 $A_i$。

设 $RR_i = \{r_{ij}: j \in N(i)\}$，$\mathcal{T}$ 表示所有节点的视图居住区域集合 $R_{ij}$。节点 $i$ 在从每个邻居 $j$ 获取其视图居住区域 $R_{ij}$ 后，使用以下算法计算其当前最小居住区域：

```
Function compute_region: Boolean
var $A_{old}$, $A_i$ : Real;

begin
    for each $R_{ij} \in \mathcal{T}$ such that $A_j \ne \infty$ do
        /* 计算节点 $i$ 从视图区域 $R_{ij}$ 得到的最小居住区域 */
        $\mathcal{R}_i \leftarrow \mathcal{R}_i \cap R_{ij}$;
    endfor;
    $A_i \leftarrow$ Area of $\mathcal{R}_i$;
    if $A_i < A_{old}$ then return true;  /* $\mathcal{R}_i$ improved */
else return false; /\* No improvement in \(\mathcal{R}_i\) \*/
end.
```

节点 $i$ 在计算完其最小居住区域后，会尝试改进其邻居的最小居住区域，具体操作如下：

Procedure improve_region

begin

for each \(j\in N(i)\) such that \(status_j\neq 1\) do

/\* Construct \(R_{ji}\), the viewed region of \(j\) \*/

\(R_{ji}=\mathcal{R}_i\oplus r_{ij};\)

Transmit \(R_{ji}\) to node \(j\);

endfor;

end.

每个节点 \(i\) 执行以下位置标识算法，直到节点获得其稳定居住区域 \(\mathcal{S}_i\)。

Algorithm location_region_identify

var region_change_flag : Boolean;

begin

while (true)

Get neighbor set \(N(i)\);

Generate \(RR_i\) : measure range with every neighbor \(j\in N(i)\);

region_change_flag = false;

repeat

Get T : viewed regions of residence \(R_{ij}\) from every neighbor \(j\);

if \(status_i=0\) then region_change_flag = compute_region(i, T);

improve_region(i, N(i), RR_i);

© 2016 by Taylor & Francis Group, LLC

[PAGE 226]

```
until `region_change_flag = false;` /* iterate until \(R_i = S_i\) */

**endwhile;**

**end.**
```

# 4.5.3 复杂度分析

函数 *compute_region* 和 *improve_region* 在最坏情况下均需要 \(O(\Delta)\) 时间，其中 \(\Delta\) 为网络中节点的最大度数。同时，*Get T* 操作也需要 \(O(\Delta)\) 时间。若为每个节点分配唯一的 *id* 编号 [15] 以避免碰撞，则每次 *repeat* 循环的迭代需要 \(O(n)\) 个时间槽。根据定理 15，当网络实现 $RR$ 和 $Ref_n$ 的全局广播时，算法 *location_region_identify* 终止。假设所有节点对的视图范围信息的传输需要 $O(1)$ 个时间槽，则整个通信过程将在 $O(D)$ 轮完成，其中 $D$ 为网络的直径（每轮包含 $O(n)$ 个时间槽，用于将消息从网络中一层节点传递到下一层节点 [15]）。因此，算法 *location_region_identify* 的总时间复杂度为 $O(nD)$。

# 4.5.4 仿真结果

作者在 [6] 中进行的仿真研究旨在评估算法 *location_region_identify* 在确定自适应网络中所有节点的稳定居住区域方面的性能。他们对多种图结构进行了实验，通过随机生成静态自适应图来模拟。一小部分节点被随机选为参考节点，这些节点被假设具有零面积的点位置。其余节点被假设具有初始无穷大的居住区域。所有通信均被假设为

