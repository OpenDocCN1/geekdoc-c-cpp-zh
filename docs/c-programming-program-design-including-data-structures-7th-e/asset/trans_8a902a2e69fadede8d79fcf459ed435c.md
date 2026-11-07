

```cpp
while (adjacentVertex != -999)
{
    graph[vertex].insertLast(adjacentVertex);
    infile >> adjacentVertex;
} //end while
} // end for

infile.close();
} //end createGraph
```

函数 clearGraph 通过释放每个链表占用的存储空间，然后将顶点数设置为零来清空图。

```cpp
void graphType::clearGraph()
{
    int index;

    for (index = 0; index < gSize; index++)
        graph[index].destroyList();

    gSize = 0;
} //end clearGraph
```

下面给出函数 printGraph 的定义。

```cpp
void graphType::printGraph() const
{
    int index;

    for (index = 0; index < gSize; index++)
    {
        cout << index << " ";
        graph[index].print();
        cout << endl;
    }

    cout << endl;
} //end printGraph
```

构造函数和析构函数的定义如下：

```cpp
//Constructor
graphType::graphType(int size)
{
    maxSize = size;
    gSize = 0;
    graph = new unorderedLinkedList<int>[size];
}

//Destructor
graphType::~graphType()
{
    clearGraph();
}
```

## 图的遍历

处理图需要具备遍历图的能力。本节讨论图的遍历算法。

遍历图与遍历二叉树类似，只不过遍历图要稍微复杂一些。回顾一下，二叉树没有环。此外，从根节点开始，我们可以遍历整棵树。另一方面，图可能有环，并且我们可能无法从单个顶点遍历整个图（例如，如果图不连通）。因此，我们必须跟踪已经访问过的顶点。我们还必须从图中每个尚未访问的顶点出发遍历图。这确保整个图都被遍历。

两种最常见的图遍历算法是**深度优先遍历**和**广度优先遍历**，下面将分别介绍。为简单起见，我们假设访问一个顶点时输出其索引。此外，每个顶点只访问一次。我们使用 `bool` 数组 `visited` 来跟踪已访问的顶点。

### 深度优先遍历

**深度优先遍历**类似于二叉树的前序遍历。一般算法如下：

```text
for each vertex, v, in the graph
    if v is not visited
        start the depth first traversal at v
```

考虑图 20-6 中的图 G。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1464_0.png)

**图 20-6** 有向图 *G*

图 20-6 中图 G 的顶点的一种深度优先排序为

0, 1, 4, 3, 2, 5, 7, 8, 6, 9

对于图 20-6 中的图，深度优先搜索从顶点 0 开始。在访问完从顶点 0 开始可以到达的所有顶点后，深度优先搜索从下一个尚未访问的顶点开始。除顶点 6 和 9 外，从顶点 0 到其他每个顶点都存在路径。因此，当深度优先搜索从顶点 0 开始时，除 6 和 9 之外的所有顶点都会在这些顶点之前被访问。完成从顶点 0 开始的深度优先搜索后，深度优先搜索从顶点 6 开始，然后从顶点 9 开始。注意，从顶点 6 到顶点 9 没有路径。因此，完成从顶点 6 开始的深度优先搜索后，深度优先搜索从顶点 9 开始。

在给定节点 v 处进行深度优先遍历的一般算法如下：

- 1. 将节点 v 标记为已访问
- 2. 访问该节点
- 3. 对与 v 相邻的每个顶点 u
  - 如果 u 尚未访问
    - 从 u 开始深度优先遍历

显然，这是一个递归算法。我们使用递归函数 `dft` 来实现该算法。深度优先遍历的起始顶点以及 `bool` 数组 visited 作为参数传递给该函数：

```cpp
void graphType::dft(int v, bool visited[])
{
    visited[v] = true;
    cout << " " << v << " ";   //visit the vertex

    linkedListIterator<int> graphIt;

        //for each vertex adjacent to v
    for (graphIt = graph[v].begin(); graphIt != graph[v].end();
                                                    ++graphIt)
    {
        int w = *graphIt;
        if (!visited[w])
            dft(w, visited);
    } //end for
} //end dft
```

在前面的代码中，注意以下语句：

```cpp
linkedListIterator<int> graphIt;
```

将 graphIt 声明为一个迭代器。在 `for` 循环中，我们使用它来遍历指针 graph[v] 所指向的链表（邻接表）。接下来，让我们看看以下语句：

```cpp
int w = *graphIt;
```

表达式 `*graphIt` 返回 graphIt 所指向的、与顶点 v 相邻的顶点的标号。

接下来，我们给出函数 `depthFirstTraversal` 的定义，以实现图的深度优先遍历：

```cpp
void graphType::depthFirstTraversal()
{
    bool *visited; //pointer to create the array to keep
                    //track of the visited vertices
    visited = new bool[gSize];

    int index;

    for (index = 0; index < gSize; index++)
        visited[index] = false;

    //For each vertex that is not visited, do a depth
    //first traversal
    for (index = 0; index < gSize; index++)
        if (!visited[index])
            dft(index, visited);
    delete [] visited;
} //end depthFirstTraversal
```

函数 `depthFirstTraversal` 对整个图执行深度优先遍历。函数 `dftAtVertex` 在给定顶点处执行深度优先遍历，其定义如下：

```cpp
void graphType::dftAtVertex(int vertex)
{
    bool *visited;

    visited = new bool[gSize];

    for (int index = 0; index < gSize; index++)
        visited[index] = false;

    dft(vertex, visited);

    delete [] visited;
} // end dftAtVertex
```

### 广度优先遍历

图的**广度优先遍历**类似于逐层遍历二叉树（每一层的节点从左到右访问）。任意一层 *i* 的所有节点都在访问第 *i* + 1 层的节点之前被访问。

图 G（图 20-6）的顶点的一种广度优先排序为：

0, 1, 3, 4, 2, 5, 7, 8, 6, 9

对于图 G，我们从顶点 0 开始广度优先遍历。访问顶点 0 之后，接下来我们访问与它直接相连且尚未访问的顶点，即 1 和 3。接下来，我们访问与 1 直接相连且尚未访问的顶点，即 4。之后，我们访问与 3 直接相连且尚未访问的顶点，在这个例子中就是单个顶点 2。之后，我们访问与 2 直接相连且尚未访问的顶点，依此类推。

与深度优先遍历的情况一样，由于可能无法从单个顶点遍历整个图，广度优先遍历也会从每个尚未访问的顶点出发遍历图。从第一个顶点开始，尽可能多地遍历图；然后转到下一个尚未访问的顶点。为了实现广度优先搜索算法，我们使用一个队列。一般算法如下：

- a. `for` 图中的每个顶点 v
  - `if` v 尚未访问
    - 将 v 加入队列 //从 v 开始广度优先搜索
- b. 将 v 标记为已访问
- c. `while` 队列不为空
  - c.1. 从队列中移除顶点 u
  - c.2. 获取与 u 相邻的顶点
  - c.3. `for` 与 u 相邻的每个顶点 w
    - `if` w 尚未访问
      - c.3.1. 将 w 加入队列
      - c.3.2. 将 w 标记为已访问

下面的 C++ 函数 breadthFirstTraversal 实现了该算法：

```cpp
void graphType::breadthFirstTraversal()
{
    linkedQueueType<int> queue;

    bool *visited;
    visited = new bool[gSize];

    for (int ind = 0; ind < gSize; ind++)
        visited[ind] = false;    //initialize the array
                                 //visited to false

    linkedListIterator<int> graphIt;

    for (int index = 0; index < gSize; index++)
        if (!visited[index])
        {
            queue.addQueue(index);
            visited[index] = true;
            cout << " " << index << " ";
```

