
```sage
sage: sum( CC.is_isomorphic(P)
....:     for CC in U.connected_components_subgraphs() )
3
sage: sum( CC.is_isomorphic(C)
....:     for CC in U.connected_components_subgraphs() )
2
```

**技术细节。** 应注意，加法运算和乘积运算会创建副本。这可能会在内存和时间方面造成额外开销。因此，修改 P 或 C 并不会反过来导致 U 被修改。此外，这两种运算还会导致另外两种信息丢失：

-   最终图的顶点被整数 {0,1,2,...} 重新标记；
-   顶点（在布局中）的位置在 U 中不会被保留。

disjoint_union 方法的行为有所不同：如果图 g 包含顶点 a，图 h 包含顶点 b，则 g.disjoint_union(h) 返回的图包含顶点 (0, a) 和 (1, b)。当 a 或 b 不是整数，而是其他类型的对象（字符串、元组等）时，使用此方法会大大简化对该并运算所得图的遍历。

### 16.1.4 图的可视化

在 Sage 中研究图的一个非常有用的方面是能够对它们进行可视化。对于基本、无多余装饰的可视化，一条命令就足够了：

```sage
sage: C = graphs.ChvatalGraph() ; C.show()
```

![](img/99840d73c45ee58b635c4eedc727fd9a_382_0.png)

这是可视化某些函数结果的有价值工具。这里，我们突出显示一个独立集：

```sage
sage: C.show(partition = [C.independent_set()])
```

show 和 plot 命令的选项无穷无尽，并且有完善的文档。至少我们应该提到 figsize = 15 选项，它指定图像的分辨率，并且对于大型图会很有用。

## 16.2 Graph 类的方法

Graph 类有 250 多个可用方法，不包括仅在 DiGraph 类中定义的方法，或仅出现在扩展模块中的方法。这使 Sage 成为一个表达力强且完整的图论库，使我们能够专注于本质——也就是说，我们可以花更少时间编写基本函数，而把更多时间花在我们真正感兴趣的问题上。

正如学习任何编程语言（或库）时一样，至少浏览一遍其函数列表以熟悉其功能是很有用的。本（非详尽的）节试图简洁地介绍 Graph 的方法。建议读者花几分钟浏览每一类方法的内容——甚至完整的方法列表；当面对图问题时，这些时间将被证明极其值得。还建议打开一个 Sage 会话，以便查阅所介绍的每个方法的在线文档（例如 g.degree_constrained_subgraph?），因为有些方法接受许多选项，或者名称并不完全明确。

### 16.2.1 修改图结构

当然，Graph 类的许多内容由用于定义和修改图的自然方法组成——这是必要但并非特别引人注目的功能。

Graph 类的访问和修改方法

| add_cycle | add_edge | add_edges |
|---|---|---|
| adjacency_matrix | allow_loops | allow_multiple_edges |
| allow_loops | delete_edge | clear |
| delete_edge | delete_edges | delete_multiedge |
| delete_vertex | delete_vertices | edge_iterator |
| edges | edge_label | edges |
| edges_incident | get_vertex | get_vertices |
| has_edge | has_loops | has_multiple_edges |
| has_vertex | incidence_matrix | latex_options |
| loop_edges | loop_vertices | loops |
| merge_vertices | neighbors | multiple_edges |
| neighbor_iterator | num_verts | networkx_graph |
| num_edges | relabel | number_of_loops |
| order | rename | remove_loops |
| remove_multiple_edges | set_edge_label | reset_name |
| set_vertex | set_vertices | set_vertices |
| subdivide_edge | subdivide_edges | size |
| vertices | weighted | vertex_iterator |
| | | weighted_adjacency_matrix |

### 16.2.2 运算符

沿着同样的思路，我们发现一些充当运算符的方法，它们返回 Graph 类（或 DiGraph）的实例。例如，应用于图 $G$ 的 complement 方法返回一个定义在同一顶点集上的图，使得边 $uv$ 存在当且仅当 $uv \notin G$。subgraph 方法从图 $G$ 获得由给定顶点集诱导的子图（见第 368 页定义），该运算记为 $G[\{v_1,\ldots,v_k\}]$。

让我们检查一些基本关系。$P_5$ 的补图（记为 $\overline{P_5}$）是一个房子图，而图 $P_4$ 和 $C_5$ 是自补的：

```sage
sage: P5 = graphs.PathGraph(5); House = graphs.HouseGraph()
sage: P5.complement().is_isomorphic(House)
True
sage: P4 = graphs.PathGraph(4); P4.complement().is_isomorphic(P4)
True
sage: C5 = graphs.CycleGraph(5); C5.complement().is_isomorphic(C5)
True
```

Sage 还（通过同名方法）定义 $G$ 的线图——通常记为 $L(G)$——其中顶点对应于 $G$ 的边，并且如果两个顶点对应的边在 $G$ 中相关联，则这两个顶点相邻。我们还找到图的不同乘积的定义。在以下每个示例中，我们假设 $G$ 是 $G_1$ 和 $G_2$ 的乘积，定义在顶点集 $V(G_1) \times V(G_2)$ 上。两个顶点 $(u,v), (u',v') \in G$ 相邻当且仅当：

| 乘积 | Sage 方法 | 邻接条件 |
|---|---|---|
| 笛卡尔积 | `cartesian_product` | $u=u'$ 且 $vv'\in E(G_2)$，或 $uu'\in E(G_1)$ 且 $v=v'$ |
| 字典序积 | `lexicographic_product` | $uu'\in E(G_1)$，或 $u=u'$ 且 $vv'\in E(G_2)$ |
| 析取积 | `disjunctive_product` | $uu'\in E(G_1)$ 或 $vv'\in E(G_2)$ |
| 张量积 | `tensor_product` | $uu'\in E(G_1)$ 且 $vv'\in E(G_2)$ |
| 强积 | `strong_product` | $u=u'$ 且 $vv'\in E(G_2)$，或 $uu'\in E(G_1)$ 且 $v=v'$，或 $uu'\in E(G_1)$ 且 $vv'\in E(G_2)$ |

我们可以将方形网格 GridGraph 构造为两条路径的笛卡尔积：

```sage
sage: n = 5; Path = graphs.PathGraph(n)
sage: Grid = Cartesian_product(Path)
sage: Grid.is_isomorphic(graphs.GridGraph([n,n]))
True
```

流、连通性等

| | |
|---|---|
| `blocks_and_cut_vertices` | `connected_component_containing_vertex` |
| `connected_components` | `connected_components_number` |
| `connected_components_subgraphs` | `degree_constrained_subgraph` |
| `edge_boundary` | `edge_connectivity` |
| `edge_cut` | `edge_disjoint_paths` |
| `edge_disjoint_spanning_trees` | `frozenset` |
| `gomory_hu_tree` | `is_connected` |
| `matching` | `multicommodity_flow` |
| `vertex_boundary` | `vertex_connectivity` |
| `vertex_cut` | `vertex_disjoint_paths` |

### 16.2.5 NP 完全问题

Sage 包含用于精确求解某些 NP 完全问题的算法。当然，这些问题可能需要大量计算资源，但许多现实世界的情况可能比其理论反例更容易求解。例如，可以求解以下优化问题。

**最大团与独立集。** 图的最大团是最大基数的两两相邻顶点集合（对于独立集则是两两不相邻的顶点集合）。此类问题的一个应用在 §16.4.1 中介绍。这是程序 Cliquer [NO] 所使用的算法。

方法：`clique_maximum`、`independent_set`

**顶点着色与边着色。** 图的正常顶点着色是为顶点分配颜色，使得任意两个相邻顶点具有不同颜色。Sage 有若干函数来计算精确着色，大多使用线性规划或 *Dancing Links* 算法。读者将在 §16.3.1 中找到一种简单但非最优的图着色算法的解释。

方法：`chromatic_number`、`coloring`、`edge_coloring`¹、`grundy_coloring`¹。

**支配集。** 图的一个顶点集合 *S* 称为支配集，如果 *G* 中的所有顶点 *v* 都与 *S* 中的某个元素相邻——我们称不在集合 *S* 中的顶点被该集合的元素*支配*。所有顶点构成的集合显然是支配集，因此问题是最小化集合 *S* 的大小。此问题由 Sage 借助线性规划求解。

方法：`dominating_set`

**哈密顿环、旅行商。** 图 *G* 称为*哈密顿的*，如果它包含一个经过其每个顶点一次且仅一次的环。与*欧拉环*问题——使用 *G* 的每条*边*一次且仅一次的环——不同，此问题是 NP 完全的，并且在*旅行商*问题的特定情况下，由 Sage 使用线性规划求解。

¹这些方法不能通过 `Graph` 类直接访问。要访问这些及其他着色函数，请参阅 `graph_coloring` 模块。
