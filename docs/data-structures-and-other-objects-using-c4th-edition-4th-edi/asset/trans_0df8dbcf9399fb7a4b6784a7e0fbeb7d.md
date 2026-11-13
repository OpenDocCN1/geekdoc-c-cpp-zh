
步骤 3c。最后，我们必须修订距离数组，以便新允许的顶点 next 可以出现在从起始顶点到另一个顶点的路径上。一个示例将解释必要的修订。假设顶点 0、1 和 5 已经在 allowed_vertices 集合中，并且我们刚刚将顶点 2 添加为下一个顶点，如下所示：

| 0 | 2 | 10 | 17 | 11 | 8 |
|---|---|---|---|---|---|
| [0] | [1] | (2) | [3] | [4] | [5] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_796_0.png)

阴影顶点是已经允许的顶点，我们刚刚将顶点 2 添加为下一个允许的顶点。

既然我们刚刚将顶点 2 添加为新允许的顶点，现在必须更新距离数组，以反映顶点 2 现在可能出现在路径上的事实。

例如，distance[3] 当前是 17。这意味着存在一条从起始顶点到顶点 3 的路径，该路径仅使用顶点 0、1 和 5，且长度为 17。关键问题是：如果我们也允许顶点 2 出现在从起始顶点到顶点 3 的路径上，能否获得小于 17 的距离？通过采用两部分路径，可能可以获得更小的距离，如下所示：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_796_1.png)

路径的第一部分从起始顶点 v0 到新允许的顶点 v2 ...

... 路径的第二部分由从新允许的顶点 v2 到顶点 v3 的一条更多边组成。

这条路径有两部分：从起始顶点到顶点 2 的部分，接着是从顶点 2 到顶点 3 的单边部分。这条路径的总权重是：

```
distance[2] + (weight of the edge from vertex 2 to vertex 3)
```

在我们的示例中，这个和是 11，小于当前的“到顶点 3 的最佳距离”。因此，我们应该用这个更小的和替换 distance[3]。我们还必须为其他每个未允许的顶点创建类似的两部分路径，如果两部分路径小于当前距离，则修改距离数组。这为步骤 3c 提供了以下改进后的伪代码：

## 步骤 3c。修订距离数组，以便新顶点 (next) 可以出现在允许的路径上。整数 n 是顶点的数量；v 和 sum 是局部整数变量，如下面的代码所示：

```
for (v = 0; v < n; ++v)
    if ((v is not an allowed vertex) and (there is an edge from next to v))
    {
        sum = distance[next] + (weight of the edge from next to v);
        if (sum < distance[v])
            distance[v] = sum;
    }
```

请注意，我们不考虑到已经是允许顶点的顶点可能出现的新的更小距离。这是因为这些顶点都比 next 更接近起始顶点，因此 distance[next] 将大于到这些顶点中任何一个的最短距离。

另外，在创建新的两部分路径时，我们只考虑路径的第二部分是从 next 到终点顶点的单边的情况。其原因是，从 next 到终点顶点的较长路径将不得不经过其他允许顶点，这意味着我们有一条从起始顶点出发，经过 next，经过另一个允许顶点，最后到达终点顶点的路径。但这样的路径通过完全避开 next 顶点总会更短——只需从起始顶点到达那个其他允许顶点（使用最短路径），然后再到达终点顶点。这样的不经过 next 顶点的路径已经是允许的。我们不需要再次考虑这样的路径——我们只需要考虑经过新允许顶点 next 的新路径。

该算法的完整伪代码如图 15.4 所示。主循环实际上在顶点数量减 1 处停止，因为此时只剩下一个未允许顶点，并且该顶点必须是距离起始顶点最远的顶点，因此没有最短路径可以经过这个最远的顶点。

我们将在示例图上执行该算法。以下是初始化距离数组后的情况：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_798_0.png)

| | 0 | ∞ | ∞ | ∞ | ∞ | ∞ |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

此时，允许顶点的集合为空，我们将第一次进入主循环。在步骤 3a 中，next 的值被设置为顶点 0（因为 distance[0] 是距离数组中的最小值）。然后我们查看每个从顶点 0 到顶点 v 有边的未允许顶点 v。这些是顶点 1 和 5，因此我们检查是否需要修订 distance[1] 和 distance[5]：

- distance[0] + (the weight of the edge from 0 to 1) 是 2。由于这小于 distance[1] 的当前值，我们用 2 替换 distance[1]。
- distance[0] + (the weight of the edge from 0 to 5) 是 9。由于这小于 distance[5] 的当前值，我们用 9 替换 distance[5]。

此时，距离数组如下所示（允许顶点已阴影）：

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_798_1.png)

| | 0 | 2 | ∞ | ∞ | ∞ | 9 |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

当前允许的顶点已阴影。

## 图 15.4 Dijkstra 最短距离算法

### 伪代码

**输入。** 一个带有正整数边权重和 n 个顶点的有向图。其中一个顶点，称为 start，被指定为起始顶点。

**输出。** 从起始顶点到图中每个其他顶点的最短距离列表。

该算法使用一个包含 n 个整数的数组（称为 distance）和一个顶点集合（称为 allowed_vertices）。变量 v、allowed_size 和 sum 是局部整数变量。存在一些特殊值（\(\infty\)），我们可以将其放在距离数组中以表示无限距离（这意味着不存在路径）。

- **步骤 1。** 将距离数组初始化为全部 \(\infty\)，除了 distance[start]，它被设置为 0。

- **步骤 2。** 将允许顶点的集合初始化为空集。

- **步骤 3。** 计算完整的距离数组：

```
for (allowed_size = 1; allowed_size < n; ++allowed_size)
{
   // At this point, allowed_vertices contains allowed_size - 1 vertices, which are the
   // allowed_size - 1 closest vertices to the start vertex. Also, for each vertex v, distance[v]
   // is the shortest distance from the start vertex to vertex v, provided that we are
   // considering only permitted paths (i.e., paths where each vertex except the final vertex
   // must be in allowed_vertices).
}
```

- **步骤 3a。** 令 next 为距离起始顶点最近且尚未在允许顶点集合中的顶点（如果有多个顶点距离相等，则可以将 next 选择为其中任何一个）。

- **步骤 3b。** 将顶点 next 添加到 allowed_vertices 集合中。

- **步骤 3c。** 修订距离数组，以便新顶点 (next) 可以出现在允许的路径上：

```
for (v = 0; v < n; ++v)
   if ((v is not an allowed vertex) and (there is an edge from next to v))
   {
      sum = distance[next] + (weight of the edge from next to v);
      if (sum < distance[v])
         distance[v] = sum;
   }
```

- **步骤 4。** 输出距离数组中的值。（每个 distance[v] 是从起始顶点到顶点 v 的最短距离。）

第二次进入主循环时，next 的值被设置为顶点 1（因为 distance[1] 是未允许顶点中的最小值）。然后我们查看每个从顶点 1 到顶点 v 有边的未允许顶点 v。这些是顶点 2、3 和 5，因此我们检查是否需要修订 distance[2]、distance[3] 和 distance[5]：

- distance[1] + (the weight of the edge from 1 to 2) 是 10。由于这小于 distance[2] 的当前值，我们用 10 替换 distance[2]。
- distance[1] + (the weight of the edge from 1 to 3) 是 17。由于这小于 distance[3] 的当前值，我们用 17 替换 distance[3]。
- distance[1] + (the weight of the edge from 1 to 5) 是 8。由于这小于 distance[5] 的当前值，我们用 8 替换 distance[5]。

此时，距离数组为：

| | 0 | 2 | 10 | 17 | ∞ | 8 |
|---|---|---|---|---|---|---|
| | [0] | [1] | [2] | [3] | [4] | [5] |

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_800_0.png)

当前允许的顶点已阴影。

第三次进入主循环时，next 的值将被设置为顶点 5（因为 distance[5] 是未允许顶点中的最小值）。然后我们查看每个从顶点 5 到顶点 v 有边的未允许顶点 v。顶点 4 是顶点 5 的边的唯一目标顶点，因此我们检查是否需要修订 distance[4]：

- distance[5] + (the weight of the edge from 5 to 4) 是 11。由于这小于 distance[4] 的当前值，我们用 11 替换 distance[4]。
