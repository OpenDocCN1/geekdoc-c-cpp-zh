# ## 3.2.1 单源最短路径

给定一个带权有向图 G=(V,E)，其中每条边的权是一个实数。另外，还给定 V 中的一个顶点，称为源。我们要计算从源到所有其他各顶点的最短路径长度。这里路径的长度是指路径上各边权之和。这个问题通常称为单源最短路径问题。

Dijkstra 算法是解决单源最短路径问题的一个贪心算法。它通过逐步扩展已知最短路径的顶点集合来求解。

算法描述：

+   1. 初始化：设源点为 s，dist[s]=0，其余顶点 dist[v]=∞。
+   2. 选择：从未处理的顶点中选择 dist 值最小的顶点 u。
+   3. 更新：对于 u 的所有邻接边 (u,v)，若 dist[u]+w(u,v) < dist[v]，则更新 dist[v]。
+   4. 标记：将 u 标记为已处理。
+   5. 重复步骤 2-4，直到所有顶点都被处理。

下面给出一个示例图：

![](bbox=[0.3, 0.63, 0.7, 0.8])

算法复杂度为 O(V²)，若使用优先队列可优化至 O((V+E)logV)。

```
```python
def dijkstra(graph, source):
    dist = {v: float('inf') for v in graph}
    dist[source] = 0
    visited = set()
    while len(visited) < len(graph):
        u = min((v for v in graph if v not in visited), key=lambda x: dist[x])
        visited.add(u)
        for v, w in graph[u].items():
            if dist[u] + w < dist[v]:
                dist[v] = dist[u] + w
    return dist
```
```