

- 1. 初始步骤

集合 V = {a}，其中 a 是源顶点

而 U = {b, c, d, e} 是未访问顶点的集合。

Dist[] = { -, 5, 3, ∞, 2}。该数组也可以写成

| | b | c | d | e |
|---|---|---|---|---|
| 距离 | 5 | 3 | ∞ | 2 |

该 Dist[] 数组表示 a 与其他顶点之间当前的最短距离。

Path = {∅, ab, ac, ∅, ∅}

- 2. 现在，到顶点 e 的距离最短，因此 e 被添加到集合 V。

我们得到 V = {a, e}；现在让我们更新 Dist 数组。

| | b | c | d | e |
|---|---|---|---|---|
| 距离 | 5 | 3 | 6 | 2 |

当前选定顶点 e 与 d 之间边的权重为 4，且从 a 到 e 的距离为 2；因此 a 到 d 的距离变为 6，因为它小于 ∞。因此，顶点 d 的路径也通过当前选定顶点（即 e）的路径进行更新。

Path = {∅, ab, ac, aed, ae}

- 3. 现在，在未访问顶点中，到顶点 c 的距离最短。因此，c 是当前选定顶点，被加入 V。

因此 V = {a, e, c}。现在让我们更新 Dist 数组。

| | b | c | d | e |
|---|---|---|---|---|
| 距离 | 4 | 3 | 5 | 2 |

这里，源点 a 到 b 和 d 的最短距离更新如下，

```
Dist[b] = min[5, Dist[c] + w(c, b)]
= min[5, 3 + 1]
= 4
```

和

```
Dist[d] = min{6, Dist[c] + w(c, d)}
= min {6, 3 + 2}
= 5
```

由于 b 和 d 的最短距离已更新，它们各自的路径也按以下表达式更新：

Path = {∅, acb, ac, acd, ae}

路径向量也可以如下所示：

| | b | c | d | e |
|---|---|---|---|---|
| 路径 | acb | ac | acd | ae |

- 4. 现在 b 是具有最短距离且未访问的顶点。

因此，V = {a, e, c, b}

| | b | c | d | e |
|---|---|---|---|---|
| 距离 | 4 | 3 | 5 | 2 |

这里，没有最短距离被更新。因此，路径也保持不变。

| | b | c | d | e |
|---|---|---|---|---|
| 路径 | acb | ac | acd | ae |

- 5. 现在 d 是下一个选定顶点，最终距离和路径向量与所述相同。因此，a 与 {b, c, d, e} 之间的最短距离分别为 {4, 3, 5, 2}。此外，a 与 {b, c, d, e} 之间的最短路径分别为 {acb, ac, acd, ae}。

在最后两步中，将顶点 b 和 d 添加到 V 得到如图 8.31 所示的路径和距离。

![](img/a99ec79093c067f0bed8f1086197950e_424_0.png)

图 8.31 最短路径和距离

要在 C++ 中实现此算法，让我们使用邻接矩阵实现，因为它便于随机访问图中所有顶点。此外，通过在矩阵中存储权重，我们可以使用矩阵来表示权重和邻接关系。我们将在对应边不存在的位置放置一个特殊的大值 9999（用于表示 >>）（程序代码 8.6）。

```
PROGRAM CODE 8.6

// Shortest distance using Dijkstra's algorithm

#include <iostream.h>
#include <conio.h>
#define infinite 9999
class graph
{
 int Graph[20][20];
 // Adjacency Matrix int No_of_Vertices;
 public:
 void Accept();
 void Display();
 int Calc_Shortest_Dist();
};

void graph :: Accept()
{
 int i,j;
 cout << "Enter no of vertex";
 cin >> No_of_Vertices;
 for(i = 1; i<= No_of_Vertices; i++)
 {
 for(j = 1; j<= No_of_Vertices; j++)
 {
 Graph[i][j] = infinite;
 }
 for(i = 1; i<= No_of_Vertices; i++)
 {
    for(j = i + 1; j<= No_of_Vertices; j++)
    {
        cout << "\n Please enter weight from to :";
        cin >> Graph[i][j];
        Graph[j][i] = Graph[i][j];
    }
 }
}

void graph :: Display()
{
    int i,j;
    cout << "Graphs Adjacency Matrix is\n";
    for(i = 1; i<= No_of_Vertices; i++)
    {
        for(j = 1; j<= No_of_Vertices; j++)
        {
            cout << "\t" << Graph[i][j];
        }
        cout << "\n";
    }
}

int graph :: Calc_Shortest_Dist()
{
    int cost, curr, src, cost1 = 0, desti, start, new1,
    i, k = 1, temp;
    int visited[20], dist[20];
    cout << " \nEnter the source";
    cin >> src;
    cout << " \nEnter the destination";
    cin >> desti;
    for(i = 0; i<= No_of_Vertices; i++)
    {
        visited[i] = 0;
        dist[i] = infinite;
    }
    visited[src] = 1;
    dist[src] = 0;
    curr = src;
    cout << "\nPath is" << src;
    while(curr != desti)
    {
        cost = infinite;
        start = dist[curr];
        for(i = 1; i<= No_of_Vertices; i++)
        {
            if(visited[i] == 0)
            {
                new1 = start + Graph[curr][i];
                if(new1 < dist[i])
                {
                    dist[i] = new1;
                    if(dist[i] < cost)
                    {
                        cost = dist[i];
                        temp = i;
                    }
                }
            }
        }
        curr = temp;
        visited[curr] = 1;
        cout << "\nCurrent node is" << curr;
        // cost1 = cost1 + cost;
    }
    return cost1;
}

void main()
{
    clrscr();
    graph G;
    int Shortest_Distance;
    G.Accept();
    G.Display();
    Shortest_Distance = G.Calc_Shortest_Dist();
    cout << "\ndistance is" << Shortest_Distance;
    getch();
}
```

## 回顾

- 图是最重要的非线性数据结构之一。图是关系的一种表示。顶点表示元素，边表示关系。换句话说，图是节点（顶点）和连接节点对的弧（边）的集合。两个顶点之间的边表示它们之间的关系。
- 图分为有向图和无向图。在无向图中，边是两个顶点的集合，顺序无关紧要；而在有向图中，边是有序对。
- 图可以使用数组或链表表示法实现。邻接表是一种数据结构，通过为每个顶点保存邻接顶点列表来表示图。邻接矩阵是一种数据结构，将图表示为布尔矩阵，其中 0 表示无边，1 表示有边。
- 图有两种标准遍历方式——深度优先和广度优先。
- 最小生成树是包含图中所有顶点的树，其边的总权重最小。计算最小生成树常用的两种算法是 Prim 算法和 Kruskal 算法。
- 双连通分量是一个极大子图。双连通图的分量在建模健壮通信网络方面很有用。
- 不相交集是一种数据结构，用于跟踪被划分为若干不相交子集的元素集合。对其执行诸如“并”和“查找”等操作，分别用于将两个集合合并为一个以及确定给定集合的位置。
- Dijkstra 算法是图中另一种常用算法，用于查找图中两个顶点之间的最短路径。

## 关键术语

- **邻接表** 在邻接表中，邻接表的 n 行表示为 n 个链表，每个顶点一个列表。我们可以用数组 Head 表示 G，其中 Head[i] 是指向顶点 i 的邻接表的指针。列表的每个节点至少有两个字段：vertex 和 link。vertex 字段包含顶点 id，link 字段存储指向存储与 i 相邻的另一个顶点的下一个节点的指针。
- **邻接矩阵** 使用矩阵的顺序表示法表示的图称为邻接矩阵。
- **邻接多重表** 多重表是节点可能在多个其他列表中共享的列表。对于每条边，不是两个节点，而是恰好一个节点，但该节点会出现在两个列表中，即它所关联的两个节点各自的邻接表中。
- **双连通分量** 双连通分量是图 G = (V, E) 的不含分离顶点或边的极大双连通子图。
- **广度优先搜索 (BFS)** 在 BFS 中，访问起始顶点 i 并将其标记为已访问后，访问所有与 i 相邻的未访问顶点。接着，访问与这些顶点相邻的未访问顶点，依此类推，直到遍历完整个图。
- **连通分量** 如果存在至少一条路径连接，则无向图是连通的。

