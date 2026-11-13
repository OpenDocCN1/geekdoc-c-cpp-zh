

```
1. Set N = number of vertices
2. Repeat For I = 1 to N
3. Repeat For J = 1 to N
4. If I = J then [avoid self-loop]
   Adj[I][J] = 0
   Else
   Adj[I][J] = 1
   [End of if]
[End of Loop]
[End of Loop]
5. Return
```

## 从图 G 中删除顶点的算法

以下算法描述了从图中删除顶点的过程。如果要删除顶点 V，则将 Adj[I][V] 的状态设置为 0，并将 Adj[V][V] 的状态设置为 0。

## 从图中删除顶点的算法

```
**Algorithm: Delete (G)**
[G is a given graph of N vertices]
1. Set N = number of vertices
2. Set V = vertex to be deleted
3. Repeat For I = 1 to N
4. Adj [I] [V] = 0
   Adj [V] [V] = 0
   [End of Loop]
5. Return
```

## 图遍历

图遍历技术用于从图 G 的顶点 v 到达顶点 u。遍历图有两种方式。

## 深度优先搜索

在深度优先搜索中，当发现新顶点 u 时，首先探索的顶点 v 的探索会停止，然后探索新顶点。在探索完所有子顶点后，会再次探索父顶点。

给定一个具有 n 个顶点的无向图 G = (V, E) 和一个初始设置为零的数组 VISITED[n]，该算法访问从 s 可到达的所有顶点。G 和 VISITED 是全局的。

## 使用深度优先搜索遍历图的算法

```
**Algorithm: DFS (G, s)**
[G is a given graph of N vertices, s is the source node]
1. Set VISITED [s] = 1
2. Visit s
3. Repeat for each vertex v adjacent to s do
4. If VISITED [v] = 0 then
5. Call DFS (v)
[End of if]
[End of For loop]
6. Return
```

## 使用非递归/迭代过程进行深度优先搜索遍历图的算法

```
Algorithm: DFS (G, s)
[G is a given graph of N vertices, s is the source node]
1. Repeat for all vertices v of graph G do
2. Set VISITED [v] = 0
[End of loop]
3. Initialize Stack STK to be empty
4. Set VISITED [s] = 1
5. Call PUSH (STK, s)
6. While ISEMPTY (STK) = false do
7. Call POP (STK, s)
8. Visit s
9. Repeat for all vertices v adjacent to s do
10. If VISITED [v] = 0 then
11. Call PUSH (STK, v)
12. Set VISITED[v] = 1
[End of For loop]
[End of While loop]
13. Return
```

如果 G 由其邻接表表示，则可以通过跟随链接链来确定与 v 相邻的顶点 w。由于算法 DFS 最多会检查邻接表中的每个顶点一次，并且有 2e 个列表顶点，因此完成搜索的时间为 O(e)。如果 G 由其邻接矩阵表示，则确定与 v 相邻的所有顶点的时间为 O(n)。由于最多访问 n 个顶点，总时间为 O(n^2)。

## 示例

![](img/723fa3ef35f5102eb67dc45b74bb823d_252_0.png)

图 9.23：有向图 (G) 的深度优先搜索

在上述示例中，图从顶点 A 遍历到顶点 F。在 DFS 中使用递归调用，而递归始终使用栈数据结构。因此，这里也给出了栈位置。

## 表 9.2：深度优先搜索

| 操作 | 栈 | 显示 |
|---|---|---|
| 压入 A | A | - |
| 弹出 A | B,C,D | A |
| 压入 B, C, D | B,C,D | A, D |
| 弹出 D | B,C,E | A, D |
| 压入 E | B,C,F | A, D, E |
| 弹出 E | B,C,F | A, D, E |
| 压入 F | B,C | A, D, E, F |
| 弹出 F | B,C | A, D, E, F |
| 弹出 C | B | A, D, E, F, C |
| 弹出 B | G | A, D, E, F, C, B |
| 压入 G | - | A, D, E, F, C, B, G |
| 弹出 G | - | A, D, E, F, C, B, G |

在 DFS 期间，有向图的边可以分为以下几类：

- 后向边：边 (u, v)，其中 v 被视为树中 u 的祖先（尽管可能不是按正确顺序）。因此，自环被视为后向边。
- 前向边：边 (u, v)，其中 v 是树中 u 的真后代。此类边称为前向边。
- 交叉边：边 (u, v)，其中 u 和 v 互不为祖先或后代关系。此类边称为交叉边。

## 深度优先搜索的生成树

在深度优先搜索中，访问图 G 顶点的序列可以形成该图 G 的一棵生成树。以下是上述图 G 的 DFS 生成树。

![](img/723fa3ef35f5102eb67dc45b74bb823d_253_0.png)

图 9.24：有向图 (G) 的深度优先搜索生成树

## 广度优先搜索 (BFS)

在广度优先搜索中，我们首先访问一个顶点 (v)，然后探索其所有相邻顶点并将其标记为已访问。当一个顶点 (v) 的所有相邻顶点都被访问时，该顶点被视为已探索。新访问的顶点被放入未探索顶点列表中。

在 BFS 中，使用队列 Q 来实现未探索顶点。从顶点 s 开始对图 G 进行广度优先搜索。所有已访问的顶点都标记为 VISITED[i] = 1。图 G 和数组 VISITED 是全局的，且 VISITED 初始化为零。

## 广度优先搜索 (BFS) 算法

```
Algorithm: BFS (G, s)
[G is a given graph of N vertices, s is the source node]
1. Repeat for all vertices v of graph G do
2.     Set VISITED [v] = 0
    [End of loop]
3. Initialize queue Q to be empty
4. Set VISITED [s] = 1
5. Call ENQUEUE (Q, s)
6. While IS EMPTY(Q) = false do
7.     Call DEQUEUE (Q, s)
8.     visit s
9.     Repeat for all vertices v adjacent to s do
10.        If VISITED[v] = 0 then
11.            Call ENQUEUE (Q, v)
12.            Set VISITED[v] = 1
    [End For loop]
    [End of While loop]
13. Return
```

![](img/723fa3ef35f5102eb67dc45b74bb823d_254_0.png)

图 9.25：有向图 (G) 的广度优先搜索遍历

在 BFS 中，使用队列数据结构，因此在上述示例中，给出了 BFS 遍历的队列位置。

## 表 9.3：广度优先搜索

| 操作 | 队列(q) | 打印 |
|---|---|---|
| 入队 A | A | - |
| 出队 A | B, C, D | A |
| 入队 B, C, D | | |
| 出队 B | C, D, G | A, B |
| 入队 G | | |
| 出队 C | D, G, F | A, B, C |
| 入队 F | | |
| 出队 D | G, F, E | A, B, C, D |
| 入队 E | | |
| 出队 G | F, E | A, B, C, D, G |
| 出队 F | E | A, B, C, D, G, F |
| 出队 E | - | A, B, C, D, G, F, E |

## 广度优先搜索的生成树

![](img/723fa3ef35f5102eb67dc45b74bb823d_255_0.png)

图 9.26：有向图 (G) 的广度优先搜索生成树

引理 4：从 S 到 V 的最短路径长度表示为 $\delta(S, V)$。那么，BFS 完成后 dist[V] = $\delta(S, V)$

证明：证明基于归纳法，以最短路径长度为准。
考虑从 S 到 V 的最短路径，设 u 为 V 的前驱，且 BFS 在所有此类顶点中首先处理 u。
因此，$\delta(S, V) = \delta(S, u) + 1$ (i)
当 u 被处理时，根据归纳法，我们有 dist[u] = $\delta(S, u)$ (ii)
由于 V 是 u 的邻居，我们设置
dist[V] = dist[u] + 1 (iii)
因此，由方程 (ii)
dist[V] = $\delta(S, u) + 1$ (iv)
由方程 (i) 我们有
dist[V] = $\delta(S, V)$

| 特性 | 广度优先搜索 | 深度优先搜索 |
| :--- | :--- | :--- |
| 内存空间 | 需要更多空间 | 需要较少空间 |
| 回溯 | 不需要回溯 | 如果走错了路径，则需要回溯。 |
| 速度 | 搜索较慢 | 搜索较快 |
| 时间 | 我们可以较早到达目标。 | 如果我们走了一条错误的路径，则需要更多时间才能到达目标。否则，我们可以比 BFS 更快地到达目标。 |
| 复杂度 | O(V+E) | O(V+E) |

## 生成树和最小生成树

无向图 G = (V, E) 的一个子图 T 是生成树，如果它是一棵包含图 G 所有顶点且没有环的树。

一个图会有多个生成树。如下图所示。

![](img/723fa3ef35f5102eb67dc45b74bb823d_256_0.png)

图 9.27：(a) 一个无向图。(b, c, d, e) 图的不同生成树

如果图的边带有权重，则该图称为“加权图”。对于加权图，生成树的代价通过计算该生成树所有边的权重之和来衡量。

**引理 5：** 图的生成树数量是图 G 拉普拉斯矩阵任何余子式的值。

**证明：** 设 L = L(G) 为图 G 的拉普拉斯矩阵，其特征值为 0 = λ1 ≤ λ2 ≤ . . . ≤ λn。矩阵 M 的 (i, j)-余子式定义为

