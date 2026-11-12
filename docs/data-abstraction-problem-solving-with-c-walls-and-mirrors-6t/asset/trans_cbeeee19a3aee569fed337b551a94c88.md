

图 20-23 从顶点 a 开始对图 20-22 中的图执行 Prim 算法的跟踪

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_1.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_2.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_3.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_4.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_5.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_6.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_7.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_649_8.png)

## 20.4.4 最短路径

加权图中两个顶点之间的最短路径具有最小的边权重和

再次考虑一张航空路线图。加权有向图可以表示这张地图：顶点是城市，边表示城市之间现有的航班。边权重表示城市（顶点）之间的里程；因此，权重不是负数。例如，你可以将图 20-5 中的两个图合并，得到这样的加权有向图。

查找顶点 0 与所有其他顶点之间的最短路径

对于加权有向图，你通常需要知道两个特定顶点之间的最短路径。加权图中两个给定顶点之间的**最短路径**是边权重之和最小的路径。虽然我们使用“最短”一词，但要意识到权重可以是距离以外的度量，例如每趟航班的美元成本或每趟航班的小时数。路径的边权重之和称为路径的**长度**或**权重**或**成本**。

例如，图 20-24a 中从顶点 0 到顶点 1 的最短路径不是 0 和 1 之间的边——其成本为 8——而是从 0 到 4 到 2 到 1 的路径，成本为 7。为方便起见，起始顶点或源点标记为 0，其他顶点标记为 1 到 n - 1。请注意图 20-24b 中图的邻接矩阵。

下面的算法归功于 E. Dijkstra，它实际上确定了给定源点与所有其他顶点之间的最短路径。该算法使用一组选定的顶点 vertexSet 和一个数组 weight，其中 weight[v] 是从顶点 0 到顶点 v 且经过 vertexSet 中顶点的最短（最便宜）路径的权重。

如果 v 在 vertexSet 中，则最短路径仅涉及 vertexSet 中的顶点。但是，如果 v 不在 vertexSet 中，那么 v 是路径上唯一不在 vertexSet 中的顶点。也就是说，路径以从 vertexSet 中的一个顶点到 v 的边结束。

最初，vertexSet 仅包含顶点 0，weight 包含从顶点 0 到所有其他顶点的单边路径的权重。也就是说，对于所有 v，weight[v] 等于 matrix[0][v]，其中 matrix 是邻接矩阵。因此，最初 weight 是 matrix 的第一行。

初始化步骤之后，你找到一个不在 vertexSet 中且使 weight[v] 最小的顶点 v。你将 v 添加到 vertexSet。对于所有（未选定的）不在 vertexSet 中的顶点 u，你检查 weight[u] 的值以确保它们确实是最小值。也就是说，你能否通过新选定的顶点 v 来降低 weight[u]——即从顶点 0 到顶点 u 的路径的权重？

为做出此判断，将从 0 到 u 的路径分为两部分，并按如下方式查找它们的权重：

weight[v] = weight of the shortest path from 0 to v
matrix[v][u] = weight of the edge from v to u

然后将 weight[u] 与 weight[v] + matrix[v][u] 进行比较，并令

weight[u] = the smaller of the values weight[u] and weight[v] + matrix[v][u]

图 20-24 (a) 加权有向图及 (b) 其邻接矩阵

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_650_0.png)

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| 0 | ∞ | 8 | ∞ | 9 | 4 |
| 1 | ∞ | ∞ | 1 | ∞ | ∞ |
| 2 | ∞ | 2 | ∞ | 3 | ∞ |
| 3 | ∞ | 2 | 2 | ∞ | 7 |
| 4 | ∞ | ∞ | 1 | ∞ | ∞ |

Dijkstra 最短路径算法的伪代码如下：

```
// Finds the minimum-cost paths between an origin vertex
// (vertex 0) and all other vertices in a weighted directed
// graph (theGraph. The graph's weights are nonnegative
shortestPath(TheGraph graph, weight: weightArray)
// Step 1: initialization
// Create a set vertexSet that contains only vertex 0
n = number of vertices in theGraph
for (v = 0 through n - 1)
    weight[v] = matrix[0][v]
// Step 2 through n
// Invariant: For v not in vertexSet, weight[v] is the
// smallest weight of all paths from 0 to v that pass
// through only vertices in vertexSet before reaching
// v. For v in all vertexSet, weight[v] is the smallest
// weight of all paths from 0 to v.
// Outside vertexSet, and the shortest paths
// from 0 to v lies entirely in vertexSet.
for (step = 2 through n)
    Find the smallest weight[v] such that v is not in vertexSet
    Add v to vertexSet
    // Check weight[u] for all u not in vertexSet
    for (all vertices u not in vertexSet)
        if (weight[u] > weight[v] + matrix[v][u])
            weight[u] = weight[v] + matrix[v][u]
}
```

循环不变式指出，一旦顶点 v 被放入 vertexSet，weight[v] 就是从 0 到 v 的绝对最短路径的权重，并且不会改变。

图 20-25 跟踪了图 20-24a 中图的算法。该算法采取以下步骤：

- 步骤 1。vertexSet 最初包含顶点 0，weight 最初是图的邻接矩阵的第一行，如图 20-24b 所示。

- 步骤 2。weight[4] = 4 是 weight 中的最小值，忽略 weight[0] 因为 0 在 vertexSet 中。因此，v = 4，所以将 4 添加到 vertexSet。对于不在 vertexSet 中的顶点——即 u = 1、2 和 3——检查从 0 到 4 然后沿边到 u 是否比直接从 0 沿边到 u 更短。对于顶点 1 和 3，这样并不更短以

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_651_0.png)

| Step | v | vertexSet | [0] | [1] | [2] | [3] | [4] |
|---|---|---|---|---|---|---|---|
| 1 | - | 0 | 0 | 8 | ∞ | 9 | 4 |
| 2 | 4 | 0, 4 | 0 | 8 | 5 | 9 | 4 |
| 3 | 2 | 0, 4, 2 | 0 | 7 | 5 | 8 | 4 |
| 4 | 1 | 0, 4, 2, 1 | 0 | 7 | 5 | 8 | 4 |
| 5 | 3 | 0, 4, 2, 1, 3 | 0 | 7 | 5 | 8 | 4 |

图 20-26 通过检查图来检查 weight[u]：(a) 步骤 2 中的 weight[2]；(b) 步骤 3 中的 weight[1]；(c) 步骤 3 中的 weight[3]；(d) 步骤 4 中的 weight[3]

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_652_0.png)

- 步骤 2。路径 0-4-2 比 0-2 更短

- 步骤 3。路径 0-4-2-1 比 0-1 更短

- 步骤 3（续）。路径 0-4-2-3 比 0-3 更短

- 步骤 4。路径 0-4-2-3 比 0-4-2-1-3 更短

将顶点 4 包含在路径中。但是，对于顶点 2，请注意 weight[2] = ∞ > weight[4] + matrix[4][2] = 4 + 1 = 5。因此，将 weight[2] 替换为 5。你也可以通过直接检查图来验证此结论，如图 20-26a 所示。步骤 3。weight[2] = 5 是 weight 中的最小值，忽略 weight[0] 和 weight[4] 因为 0 和 4 在 vertexSet 中。因此，v = 2，所以将 2 添加到 vertexSet。对于不在 vertexSet 中的顶点——即 u = 1 和 3——检查从 0 到 2 然后沿边到 u 是否比直接从 0 沿边到 u 更短。（参见图 20-26b 和 20-26c。）

请注意
weight[1] = 8 > weight[2] + matrix[2][1] = 5 + 2 = 7。因此，将 weight[1] 替换为 7。
weight[3] = 9 > weight[2] + matrix[2][3] = 5 + 3 = 8。因此，将 weight[3] 替换为 8。

步骤 4。weight[1] = 7 是 weight 中的最小值，忽略 weight[0]、weight[2] 和 weight[4] 因为 0、2 和 4 在 vertexSet 中。因此，v = 1，所以将 1 添加到 vertexSet。对于不在 vertexSet 中的唯一顶点 3，请注意 weight[3] = 8 < weight[1] + matrix[1][3] = 7 + ∞，如图 20-26d 所示。因此，保持 weight[3] 不变。

步骤 5。vertexSet 中唯一剩余的顶点是 3，所以将其添加到 vertexSet 并停止。

weight 中的最终值是最短路径的权重。这些值出现在图 20-25 的最后一行。例如，从顶点 0 到顶点 1 的最短路径的成本为 weight[1]，即 7。此结果与我们之前关于图 20-24 的观察一致。我们当时看到最短路径是从 0 到 4 到 2 到 1。另外，从顶点 0 到顶点 2 的最短路径的成本为 weight[2]，即 5。此路径是从 0 到 4 到 2。

只要算法的循环不变式为真，weight 中的权重就是最小可能的。循环不变式为真的证明是通过对步骤进行归纳，并作为一道难题留给读者。（参见练习 20。）

## 20.4.5 回路

回路只是某些问题陈述中常见的一种循环的另一个名称。回顾，图中的循环是一条起止于同一顶点的路径。典型的回路要么访问每个顶点一次，要么访问每条边一次。

图的第一个应用可能发生在 18 世纪初，当时欧拉提出了一个桥梁问题。如图 20-27a 所示，河中的两个岛屿通过几座桥梁彼此相连并连接到河岸。桥梁对应于图 20-27b 中伪图的边，陆地对应于顶点。该问题询问你能否从顶点 v 出发，恰好通过每条边一次，然后终止于 v。欧拉证明了对于这种特定的边和顶点配置不存在解。

为简单起见，我们将考虑无向图而不是伪图。无向图中从顶点 v 出发，恰好通过图中每条边一次，并终止于 v 的路径称为欧拉回路。欧拉表明，当且仅当每个顶点触及偶数条边时，欧拉回路才存在。直观地说，如果你沿一条边到达一个顶点，你必须能够沿另一条边离开该顶点。如果不能，你将无法到达所有顶点。

欧拉回路从顶点 v 开始，恰好通过每条边一次，并终止于 v

图 20-27 (a) 欧拉的桥梁问题及 (b) 其伪图表示

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_653_0.png)

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_653_1.png)

