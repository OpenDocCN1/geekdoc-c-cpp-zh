

## 8.4.2 广度优先搜索

访问顶点的另一种系统方法是广度优先搜索（BFS）。BFS 与 DFS 的不同之处在于，在访问起始顶点 i 并将其标记为已访问后，会访问所有与 i 相邻的未访问顶点。接下来，访问这些顶点相邻的未访问顶点，以此类推，直到遍历完整个图。这种方法被称为“广度优先”，因为从我们访问的顶点 i 出发，通过接下来访问所有与 i 相邻的顶点，尽可能广泛地进行搜索。例如，图 8.13 中图的 BFS 会按以下顺序访问节点：1、2、3、4、5、6、7 和 8。

此搜索算法使用队列来存储图中每一层的顶点，在访问时即时存储。然后按顺序从队列中取出这些顶点，即先进先出（FIFO），并访问它们的相邻顶点，直到所有顶点都被访问。当队列为空时，算法终止。BFS 的工作过程如算法 8.3 所示。该算法将布尔数组 visited[] 初始化为 0（false），即将每个顶点标记为未访问。

```
ALGORITHM 8.3
Breadth-first search (vertex j)
1. Let us start search at vertex j
   Mark all vertices as unvisited
   for i = 1 to n do
       visited[i] = 0
2. Mark j as visited
   visited[j] = 1
3. Add j in queue
4. while not queue empty do
   begin
       i = delete from queue
       for all vertices j adjacent to i do
           begin
               if(not visited[j] = 1)
               Add j in queue
               visited[j] = 1
           end
       end
   end
6. stop
```

在算法 8.3 的步骤 5 中，while 循环执行 n 次。这里，n 是顶点的数量，每个顶点只插入队列一次。如果使用邻接表表示，则相邻节点在 for 循环中计算。for 循环执行 e 次。因此，对于邻接表示，BFS 需要 O(n + e) 时间，对于邻接矩阵表示，需要 O(n^2) 时间。

在程序代码 8.5 中，我们使用队列 Q 作为遍历的数据结构。

### 程序代码 8.5

```cpp
// Breadth-first traversal using adjacency matrix
void Graph :: BreadthFirstSearch(int i)
{
	int k, visited[max];
	queue Q;
	for(k = 1; k <= n; k++)
		visited[k] = 0;
	visited[i] = 1;
	Q.Add(i);
	while(!Q.IsEmpty())
	{
		j = Q.Delete();
		for(k = 1; k <= n; k++)
		{
			if(Adj_Matrix [j,k] && !visited[k])
			{
				Q.Add(k);
				visited[k] = 1;
			}
		}
	}
}
// Function for breadth-first search
void Graph :: BFS(int v)
{
	Queue q;
	GraphNode* curr;
	visited[v] = true;
	cout << "\t" << headnodes[v]->vertex;
	q.addq(headnodes[v]);
	while(!q.emptyq())
	{
		curr = q.deleteq();
		curr = curr->next;
		while(curr != null)
		{
			if(!visited[curr->vertex - 1])
			{
				q.addq(headnodes[curr->vertex - 1]);
				cout << "\t" << curr->vertex;
			}
		}
	}
}
visited[curr->vertex - 1] = true;
}
curr = curr->next;
}
return;
}
```

这里，`add()` 和 `delete()` 分别是用于向队列添加和删除元素的成员函数。让我们再次考虑图 8.13 中的图，用于 BFS。让我们使用一个使用队列的非递归算法来遍历图。设 1 为起始顶点。最初，队列为空，已访问顶点的初始集合 V = \(\phi\)。

- 1. 将 1 添加到队列。将 1 标记为已访问。V = {1}。

![](img/a99ec79093c067f0bed8f1086197950e_406_0.png)

- 2. 由于队列不为空，vertex = 从队列中 delete()，我们得到 1。将 1 的所有未访问相邻顶点添加到队列。此外，将它们标记为已访问。现在，V = {1, 2, 5, 4}。

![](img/a99ec79093c067f0bed8f1086197950e_406_1.png)

- 3. 由于队列不为空，vertex = delete()，我们得到 2。将 2 的所有相邻未访问顶点添加到队列并将其标记为已访问。现在 V = {1, 2, 5, 4, 3}。

![](img/a99ec79093c067f0bed8f1086197950e_406_2.png)

- 4. 由于队列不为空，vertex = 从队列中 delete()，我们得到 5。现在，将 5 的所有相邻未访问顶点添加到队列并将其标记为已访问。

现在，V = {1, 2, 5, 4, 3, 7}。

![](img/a99ec79093c067f0bed8f1086197950e_407_0.png)

- 5. 由于队列不为空，vertex = 从队列中 delete()，我们得到 4。现在，将 4 的所有相邻未访问顶点添加到队列。顶点 1 和 7 与 4 相邻，因此已被访问。现在我们从队列中得到的下一个元素是 3。现在，我们将 3 的所有未访问顶点添加到队列，使 V = {1, 2, 5, 4, 3, 7, 6}。

![](img/a99ec79093c067f0bed8f1086197950e_407_1.png)

- 6. 由于队列不为空，vertex = delete()，我们得到 7。将 7 的所有相邻未访问顶点添加到队列并将其标记为已访问。现在，V = {1, 2, 5, 4, 3, 7, 6, 8}。

![](img/a99ec79093c067f0bed8f1086197950e_407_2.png)

- 7. 由于队列不为空，vertex = delete()，我们得到 6。然后，将 6 的所有未访问相邻顶点添加到队列并将其标记为已访问。现在 V = {1, 2, 5, 4, 3, 7, 6, 8}。

![](img/a99ec79093c067f0bed8f1086197950e_407_3.png)

- 8. 由于队列不为空，vertex = delete()，我们得到 8。将其相邻未访问顶点添加到队列并将其标记为已访问。V = {1, 2, 5, 4, 3, 7, 6, 8, 9}。

![](img/a99ec79093c067f0bed8f1086197950e_407_4.png)

- 9. 由于队列不为空，vertex = delete() = 9。
- 此处，请注意 9 没有未访问的相邻顶点。
- 10. 由于队列为空，我们停止。
- BFS 访问顶点的顺序是 1、2、5、4、3、7、6、8、9
- 这在图 8.18 中表示。

![](img/a99ec79093c067f0bed8f1086197950e_408_0.png)

## 8.5 生成树

树是一个没有环的连通图。生成树是 G 的一个子图，包含 G 的所有顶点并且是一棵树。加权图 G 的最小生成树是 G 的生成树，其边权之和最小。

一个图可以有多个最小生成树。图 8.19 显示了一个图、其一棵生成树和一棵最小生成树。

![](img/a99ec79093c067f0bed8f1086197950e_408_1.png)

最小生成树在许多应用中很有用，例如查找连接一组计算机、房屋或城市所需的最少电线长度。最小生成树在所有可能的生成树中最小化总长度。

我们希望高效地计算最小生成树。理论上，我们可以枚举加权图的所有生成树，然后简单地选择权重最小的树。但是，如果图比较复杂，这不是一种容易且高效的获取方式。在本节中，我们将研究 20 世纪 50 年代由 J.B. Kruskal 和 R.C. Prim 发现的两种最有效的方法。这两种算法都是贪心算法，通过在每个阶段添加一条边并做出下一条边的最佳选择来生成最小生成树。用于计算图的最小生成树的这两种流行方法是

- 1. Prim 算法
- 2. Kruskal 算法

在讨论这些算法之前，让我们先了解连通分量。

### 8.5.1 连通分量

如果图中每对顶点之间至少有一条路径，则无向图是连通的。图的连通分量是一个极大连通子图，即连通分量中的每个顶点都可以从该分量中的顶点到达。

考虑图 8.20 中的图 G1。

![](img/a99ec79093c067f0bed8f1086197950e_409_0.png)

在这个无向图中，只有一个连通分量，即图 G1 本身。

如果从图 G1 中删除边 e1 和 e3，我们得到一个具有两个连通分量的图 G2：({V1, V2, V3}, {E1, E2, E5}) 和 ({V4}, Ø)。这在图 8.21 中表示。

![](img/a99ec79093c067f0bed8f1086197950e_409_1.png)

### 8.5.2 Prim 算法

任何连通图的所有顶点都包含在图 G 的最小代价生成树中。Prim 算法从一个顶点开始，一次添加一个顶点（及其关联边）来增长树的其余部分。该算法通过迭代添加边来构建一棵树，直到获得最小生成树，即当所有节点

