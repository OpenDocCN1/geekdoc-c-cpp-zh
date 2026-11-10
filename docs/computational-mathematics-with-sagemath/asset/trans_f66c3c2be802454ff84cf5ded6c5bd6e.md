
```sage
sage: p.add_constraint(
....:   p.sum( weight[o] * taken[o] for o in L ) <= C )
sage: p.set_objective(
....:   p.sum( utility[o] * taken[o] for o in L ) )
sage: p.solve()
1.41999999999999999999
sage: taken = p.get_values(taken)
```

我们可以检查该解是否可行：

```sage
sage: sum( weight[o] * taken[o] for o in L )
0.96000000000000000000
```

我们应该拿一个烧瓶吗？

```sage
sage: taken["Flask"]
1.0
```

练习 65（子集和）。称为子集和的组合问题是在一组整数中找到一个非空元素子集，使其和为零。请用整数线性规划对集合 {28, 10, −89, 69, 42, −37, 76, 78, −40, 92, −93, 45} 求解该问题。

### 17.4.2 匹配

在图里寻找一个匹配，相当于找出一组两两不相交的边。空集是平凡匹配，因此我们把注意力集中在最大匹配上：我们寻求使匹配中的边数最大化。计算最大匹配是一个多项式问题，这可由 Jack Edmonds [Edm65] 的一个结果推出。Edmonds 算法基于局部改进，以及该算法在找到最大匹配之前不会停止的证明。在图论所提供的算法中，该算法并不是最难实现的，不过这个问题可以用一个非常简单的 MILP 来建模。

对于这个任务，和上一个问题一样，我们需要为每个对象——图的边——关联一个二元值，指示该边是否属于我们的匹配。

然后需要确保两条相邻边不能同时出现在匹配中。实际上，这看起来就像一个线性约束：如果 x 和 y 是同一图的两条边，且 mₓ 和 mᵧ 是它们关联的变量，只需要求不等式 mₓ + mᵧ ≤ 1 成立即可。由于这两条边不会同时出现在我们的解中，我们就能写出一个计算最大匹配的线性规划。注意，如果两条边不能同时出现在匹配中，是因为它们都有图的一个公共顶点 v。于是更简单的说法是：匹配中至多只能取与每个顶点 v 相关联的一条边，这又是一个线性约束。

$$\max: \sum_{e\in E(G)} m_e$$

$$\text{such that: } \forall v\in V(G), \sum_{e\in E(G), e\sim v} m_e \leq 1.$$

使用 Sage 可以很容易地把这个问题转化为 MILP：

```sage
sage: g = graphs.PetersenGraph()
sage: p = MixedIntegerLinearProgram()
sage: matching = p.new_variable(binary = True)

sage: p.set_objective(p.sum(matching[e]
....:                     for e in g.edges(labels = False)))

sage: for v in g:
....:     p.add_constraint(p.sum(matching[e]
....:                          for e in g.edges_incident(v, labels = False)) <= 1)
sage: p.solve()
5.0

sage: matching = p.get_values(matching)
sage: [e for e, b in matching.iteritems() if b == 1]
[(0, 1), (4, 9), (6, 8), (5, 7), (2, 3)]
```

**练习 66**（*支配集*）。图中的一个支配集是一个顶点集合 $S$，使得每个不在 $S$ 中的顶点在 $S$ 中至少有一个邻居。请写出一个整数线性规划，为 Petersen 图找到一个基数最小的支配集。

### 17.4.3 流

在本节中，我们介绍图论中另一个基本算法：最大流！给定 *有向图* $G$ 的一对顶点 $s$ 和 $t$（即边有方向，参见图 17.1），该问题是在使用 $G$ 的边的情况下，从 $s$ 向 $t$ 发送一个 *最大流*。这些边中的每一条都有一个关联的 *最大容量*——即能够通过它的最大流量。

该问题的定义几乎就是其线性规划形式：我们为每条边寻找一个实数值，表示流经它的流量强度，并受两类约束：

- 到达某顶点（不同于 $s$ 或 $t$）的流量应等于离开该顶点的流量；
- 一条边上的流量不能超过其容量。

![](img/99840d73c45ee58b635c4eedc727fd9a_409_0.png)

图 17.1 —— Chvátal 图上的一个最大流问题。

话虽如此，我们剩下的任务是最大化离开 $s$ 的流量：所有流量最终都会到达 $t$，因为其他顶点发送的流量与接收的流量一样多。我们可以用如下线性规划对流问题建模（假设所有边的容量均为 1）：

$$\text{Maximise: } \sum_{sv\in E(G)} f_{sv}$$

$$\text{such that: } \forall v\in V(G)\setminus\{s,t\},\quad \sum_{uv\in E(G)} f_{uv}=\sum_{uv\in E(G)} f_{vu}$$

$$\forall uv\in E(G),\ f_{uv}\leq 1.$$

我们将在 Chvátal 图的一个定向（参见图 17.1）上求解流问题，其中所有边的容量均为 1：

```python
sage: g = graphs.ChvatalGraph()
sage: g = g.minimum_outdegree_orientation()

sage: p = MixedIntegerLinearProgram()
sage: f = p.new_variable()
sage: s, t = 0, 2

sage: for v in g:
.....:     if v == s or v == t: continue
.....:     p.add_constraint(
.....:         p.sum(f[v,u] for u in g.neighbors_out(v)) ==
.....:         p.sum(f[u,v] for u in g.neighbors_in(v)))

sage: for e in g.edges(labels = False): p.add_constraint( f[e] <= 1 )

sage: p.set_objective(p.sum( f[s,u] for u in g.neighbors_out(s)))

sage: p.solve()
2.0
```

![](img/99840d73c45ee58b635c4eedc727fd9a_411_0.png)

图 17.3 —— 非精确建模的一个可能解。

- 对图中每个顶点 $v$，关联一个整数 $i_v$，表示环 $C$ 访问它的阶段，其中对于固定顶点 $v_0$，有 $i_{v_0}=0$；
- 对 $G$ 的每条边 $uv$，关联两个二元变量 $b_{uv}$ 和 $b_{vu}$，指示该边是否属于环 $C$（并用于判断该边正被使用的方向）；
- 我们要求每个顶点在 $C$ 中都有一条出边和一条入边；
- 仅当 $i_u < i_v$ 时，边 $uv$ 才属于 $C$（边按照访问顺序递增的方向延伸）。

我们可以用几行线性方程改写该算法：

max：无目标函数

满足：

$$\forall v \in V(G),\quad \sum_{uv\in E(G)} b_{uv}=1$$

$$\forall v \in V(G),\quad \sum_{uv\in E(G)} b_{vu}=1$$

$$\forall uv \in E(G)\setminus\{v_0\},\quad i_u-i_v+|V(G)|b_{uv}\leq |V(G)|-1$$

$$i_v-i_u+|V(G)|b_{vu}\leq |V(G)|-1$$

$$\forall v \in V(G),\quad i_v\leq |V(G)|-1$$

$b_{uv}$ 是二元变量

$i_v$ 是整数变量。

在这个公式中，有一个系数 $|V(G)|$，这通常表明求解器将无法高效地求解该线性规划。因此，我们将对哈密顿环采用另一种建模方法。考虑下面这个简单的观察：如果我们的图中存在一个哈密顿环 $C$，那么对于每个顶点真子集 $S$，都至少存在两条 $C$ 的边进入或离开 $S$。如果我们用 $\bar{S}$ 表示恰好有一个端点在 $S$ 中的边集，那么可以得到如下公式（将变量 $b_{uv}$ 和 $b_{vu}$ 视为相同）：

max：无目标函数

满足：$\forall u \in V(G),\quad \sum_{uv\in E(G)} b_{uv}=2$

$\forall S \subseteq V(G),\ \emptyset \ne S \ne V(G),\quad \sum_{e\in\bar{S}} v_e \geq 2$

$b_{uv}$ 是二元变量。

我们不太可能直接使用前面的公式来求解哈密顿环问题，即使对于像 $4 \times 6 = 24$ 个元素这样的小网格也是如此：关于集合 $S$ 的约束将有 $2^{24}-2=16\,777\,214$ 条。另一方面，线性不等式求解器所使用的 *分支定界*方法（或 *分支切割*）非常适合在线性规划求解*期间*生成约束¹。为哈密顿环问题生成约束对应于以下步骤：

- 创建一个线性规划——不带目标函数——每条边有一个二元变量；
- 对每个顶点添加一个约束，强制其度数为 2；
- 求解该线性规划；
- 当当前解不是哈密顿环时（此时它是一个具有若干连通分量的子图），令 $S$ 为其一个连通分量，并添加约束，要求至少有两条边离开 $S$。

幸运的是，验证当前解无效并生成相应约束在算法上很快。使用 Sage 的约束生成方法，下面是我们如何在网格上求解哈密顿环问题：

```sage
sage: g = graphs.Grid2dGraph(4, 6)
sage: p = MixedIntegerLinearProgram()
sage: b = p.new_variable(binary = True)
```

为了避免变量 $b[u,v]$ 和 $b[v,u]$ 之间的差异，方便的做法是创建一个 lambda 函数，把对 $x,y$ 替换为集合 $\{x,y\}$：

```sage
sage: B = lambda x,y : b[frozenset([x,y])]
```

¹ 这意味着，一旦线性规划求解完成，就可以添加一个额外约束，并利用前一次计算中获得的部分结果来求解新的线性规划。
