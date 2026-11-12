

**图 20-18 图 20-11 所示图的生成树**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_645_0.png)

**图 20-19 各具有四个顶点和三条边的连通图**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_645_1.png)

- **2. 具有** $n$ **个顶点且恰好有** $n-1$ **条边的连通无向图不能包含环。** 要理解这一点，请从前一条观察开始：要使图连通，具有 $n$ 个顶点的图至少必须有 $n-1$ 条边。如果连通图确实包含一个环，你可以移除环上任意一条边，图仍然保持连通。因此，如果具有 $n$ 个顶点和 $n-1$ 条边的连通图确实包含一个环，移除环上的一条边将留下一个只有 $n-2$ 条边的连通图，根据观察 1，这是不可能的。

- **3. 具有** $n$ **个顶点且超过** $n-1$ **条边的连通无向图必须包含至少一个环。** 例如，如果你向图 20-19 中的任何图添加一条边，将在图中创建一个环。这一事实较难证明，留作练习。（参见本章末尾的练习 17。）

因此，你可以通过简单地计算连通图的顶点数和边数来判断其是否包含环。

由此可见，一棵树（即没有环的连通无向图）必须用 $n-1$ 条边连接其 $n$ 个节点。因此，要获得具有 $n$ 个顶点的连通图的生成树，你必须移除环上的边，直到只剩下 $n-1$ 条边。

确定图生成树的两种算法基于之前的遍历算法，将在下文介绍。通常，这些算法对任何特定图都会生成不同的生成树。

**DFS 生成树。** 确定连通无向图生成树的一种方法是使用深度优先搜索遍历图的顶点。在遍历图时，标记你所遵循的边。遍历完成后，图的顶点和标记的边构成一个生成

**图 20-20 图 20-11 中以顶点 a 为根的 DFS 生成树**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_646_0.png)

DFS 生成树算法按以下顺序访问顶点：a, b, c, d, e, f, g, h, i。数字表示算法标记边的顺序。

树，称为深度优先搜索（DFS）生成树。（或者，你可以从图中移除未标记的边来形成生成树。）对之前的迭代和递归版本的 dfs 进行简单修改，即可得到创建 DFS 生成树的算法。例如，递归算法如下：

DFS 生成树算法

```
```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v by using depth-first search.
// Recursive version.
dfsTree(v: Vertex)
  Mark v as visited
  for (each unvisited vertex u adjacent to v)
    Mark the edge from u to v
    dfsTree(u)
  }
```
```

当你将此算法应用于图 20-11 中的图时，你会得到图 20-20 中所示的以顶点 a 为根的 DFS 生成树。该图指示了算法访问顶点和标记边的顺序。你应该通过追踪算法来追踪这些结果。

**BFS 生成树。** 确定连通无向图生成树的另一种方法是使用广度优先搜索遍历图的顶点。在遍历图时，标记你所遵循的边。遍历完成后，图的顶点和标记的边构成一个生成树，称为广度优先搜索（BFS）生成树。（或者，你可以从图中移除未标记的边来形成生成树。）你可以通过在将 u 加入队列之前标记 w 和 u 之间的边来修改之前的 bfs 迭代版本。结果是创建 BFS 生成树的以下迭代算法。

```
```
// Forms a spanning tree for a connected undirected graph
// beginning at vertex v by using breadth-first search.
// Iterative version.
bfsTree(v: Vertex)
  q = a new empty queue
  // Add v to queue and mark it
  q.enqueue(v)
  Mark v as visited
  while (!q.isEmpty())
  {
    q.dequeue(w)
    // Loop invariant: there is a path from vertex w to
    // every vertex in the queue q
    for (each unvisited vertex u adjacent to w)
    {
      Mark u as visited
      Mark edge between w and u
      q.enqueue(u)
    }
  }
```
```

**图 20-21 图 20-11 中以顶点 a 为根的 BFS 生成树**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_647_0.png)

BFS 生成树算法按以下顺序访问顶点：a, b, f, i, c, e, g, d, h。数字表示算法标记边的顺序。

当你将此算法应用于图 20-11 中的图时，你会得到图 20-21 中所示的以顶点 a 为根的 BFS 生成树。该图指示了算法访问顶点和标记边的顺序。你应该通过追踪算法来复现这些结果。

## 20.4.3 最小生成树

想象一个发展中国家雇佣你设计其电话系统，使该国所有城市都能互相呼叫。显然，一个解决方案是在每对城市之间铺设电话线。然而，你的工程团队确定，由于该国多山地形，某些城市对之间无法铺设线路。团队的报告包含图 20-22 中的带权无向图。图中的顶点代表 n 个城市。两个顶点之间的边表示在顶点所代表的城市之间铺设电话线是可行的，每条边的权重表示电话线的安装成本。请注意，如果该图不连通，你将无法通过电话线网络连接所有城市。然而，图 20-22 中的图是连通的，使得问题可行。如果你在图中由边连接的每对城市之间安装电话线，你当然会解决问题。然而，这个解决方案可能成本过高。根据前一节的观察 1，你知道 n - 1 是具有 n 个顶点的图保持连通所需的最小边数。因此，n - 1 是连接 n 个城市所需的最少线路数。

**图 20-22 带权、连通、无向图**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_648_0.png)

如果安装每条线路的成本相同，问题就简化为寻找图的任意生成树。总安装成本——即生成树的成本——是生成树中边的成本之和。然而，如图 20-22 所示，安装每条线路的成本各不相同。由于可能存在多个生成树，且不同树的成本可能不同，你需要通过选择成本最低的生成树来解决问题；也就是说，你必须选择边权重（成本）之和最小的生成树。这样的树称为最小生成树，且不一定唯一。尽管某个特定图可能有多个最小生成树，但它们的成本相等。

连通无向图的最小生成树具有最小的边权重和

最小生成树算法

```
```
// Determines a minimum spanning tree for a weighted,
connected, undirected graph whose weights are
nonnegative, beginning at any vertex v.
primsAlgorithm(v: Vertex)
Mark vertex v as visited and include it in the minimum spanning tree
while (there are unvisited vertices)
    { Find the least-cost edge (v, w) from a visited vertex v to some unvisited vertex u
      Mark u as visited
      Add the vertex u and the edge (v, w) to the minimum spanning tree
    }
```
```

图 20-23 追踪了从顶点 a 开始对图 20-22 中图应用 primsAlgorithm 的过程。加入树中的边显示为实线，而正在考虑的边显示为虚线。

primsAlgorithm 确定的生成树是否最小并不明显。然而，证明 primsAlgorithm 正确性超出了本书的范围。

