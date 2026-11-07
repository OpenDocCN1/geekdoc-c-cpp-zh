
## 例 21-5

设 G 为图 21-8 所示的图。

![](img/f97f778697507bb6fdd80c5991210cba_1381_0.png)

**图 21-8** 带权图 *G*

假设 G 的源顶点为 0。该图显示了每条边的权重。步骤 1 和步骤 2 执行后，所得图如图 21-9 所示。

![](img/f97f778697507bb6fdd80c5991210cba_1381_1.png)

|  | [0] | [1] | [2] | [3] | [4] |
|---|---:|---:|---:|---:|---:|
| `smallestWeight` | 0 | 16 | ∞ | 2 | 3 |
| `weightFound` | true | false | false | false | false |

**图 21-9** 步骤 1 和步骤 2 执行后的图

**步骤 3 至 5 的第 1 次迭代：** 在步骤 3 中，我们选择一个最接近顶点 0 且其最短路径尚未被找到的顶点。我们通过在数组 `smallestWeight` 中找到一个权重最小、且在数组 `weightFound` 中对应项为 `false` 的顶点来实现。因此，在这次迭代中，我们选择顶点 3。在步骤 4 中，我们将 `weightFound[3]` 标记为 `true`。接下来，在步骤 5 中，我们考虑顶点 1 和 4，因为这些是从顶点 3 出发存在边的顶点，并且从 0 到这些顶点的最短路径尚未被找到。然后我们检查从顶点 0 经由顶点 3 到顶点 1 和 4 的路径是否可以被改进。从 0 到 1 的路径 0-3-1 的权重小于路径 0-1 的权重。因此我们将 `smallestWeight[1]` 更新为 14。路径 0-3-4 的权重为 2 + 7 = 9，大于路径 0-4 的权重 3。因此我们不更新顶点 4 的权重。图 21-10 显示了所得图。（虚线箭头表示从源点——即从 0——到该顶点的最短路径。）

![](img/f97f778697507bb6fdd80c5991210cba_1382_0.png)

**图 21-10** 步骤 3、4 和 5 第一次迭代后的图

**步骤 3 至 5 的第 2 次迭代：** 在步骤 3 中，我们选择顶点 4，因为这是数组 `smallestWeight` 中权重最小的顶点，并且它在数组 `weightFound` 中的对应项为 `false`。接下来，我们执行步骤 4 和 5。在步骤 4 中，我们将 `weightFound[4]` 设置为 `true`。在步骤 5 中，我们考虑顶点 1 和 2，因为这些是从顶点 4 出发存在边的顶点，并且从 0 到这些顶点的最短路径尚未被找到。然后我们检查从顶点 0 经由顶点 4 到顶点 1 和 2 的路径是否可以被改进。特别地，路径 0-4-1 的权重为 13，小于顶点 1 的当前权重 14。因此我们更新 `smallestWeight[1]`。类似地，我们更新 `smallestWeight[2]`。图 21-11 显示了所得图。

![](img/f97f778697507bb6fdd80c5991210cba_1383_0.png)

**图 21-11** 步骤 3、4 和 5 第二次迭代后的图

**步骤 3 至 5 的第 3 次迭代：** 在步骤 3 中，选择的顶点是 2。在步骤 4 中，我们将 `weightFound[2]` 设置为 `true`。接下来，在步骤 5 中，我们考虑顶点 1，因为这是从顶点 2 出发存在边的顶点，并且从 0 到该顶点的最短路径尚未被找到。然后我们检查从顶点 0 经由顶点 2 到顶点 1 的路径是否可以被改进。显然，从 0 到 1 的路径 0-4-2-1 的权重为 10，小于顶点 1 的当前权重（为 13）。因此我们更新 `smallestWeight[1]`。图 21-12 显示了所得图。

![](img/f97f778697507bb6fdd80c5991210cba_1383_1.png)

**图 21-12** 步骤 3、4 和 5 第三次迭代后的图

**步骤 3 至 5 的第 4 次迭代：** 在步骤 3 中，选择顶点 1，并且在步骤 4 中，将 `weightFound[1]` 设置为 `true`。在这次迭代中，步骤 5 的操作是空的，因为从顶点 0 到图中其他每个顶点的最短路径都已确定。图 21-13 显示了最终图。

![](img/f97f778697507bb6fdd80c5991210cba_1384_0.png)

|  | [0] | [1] | [2] | [3] | [4] |
|---|---:|---:|---:|---:|---:|
| `smallestWeight` | 0 | 10 | 7 | 2 | 3 |
| `weightFound` | T | T | T | T | T |

**图 21-13** 步骤 3、4 和 5 第四次迭代后的图

下面的 C++ 函数 `shortestPath` 实现了前面的算法：

```cpp
void weightedGraphType::shortestPath(int vertex)
{
    for (int j = 0; j < gSize; j++)
        smallestWeight[j] = weights[vertex][j];

    bool *weightFound;
    weightFound = new bool[gSize];

    for (int j = 0; j < gSize; j++)
        weightFound[j] = false;

    weightFound[vertex] = true;
    smallestWeight[vertex] = 0;

    for (int i = 0; i < gSize - 1; i++)
    {
        double minWeight = DBL_MAX;
        int v;

        for (int j = 0; j < gSize; j++)
            if (!weightFound[j])
                if (smallestWeight[j] < minWeight)
                {
                    v = j;
                    minWeight = smallestWeight[v];
                }
        weightFound[v] = true;

        for (int j = 0; j < gSize; j++)
            if (!weightFound[j])
                if (minWeight + weights[v][j] < smallestWeight[j])
                    smallestWeight[j] = minWeight + weights[v][j];
    } //end for
} //end shortestPath
```

注意，函数 `shortestPath` 只记录从源点到某个顶点的最短路径的权重。我们留给你修改这个函数，以便也记录从源点到某个顶点的最短路径。此外，这个函数使用了命名常量 `DBL_MAX`，它定义在头文件 `cfloat` 中。

函数 `printShortestDistance` 以及构造函数和析构函数的定义如下：

```cpp
void weightedGraphType::printShortestDistance(int vertex)
{
    cout << "Source Vertex: " << vertex << endl;
    cout << "Shortest Distance from Source to each Vertex."
         << endl;
    cout << "Vertex  Shortest Distance" << endl;

    for (int j = 0; j < gSize; j++)
        cout << setw(4) << j << setw(12) << smallestWeight[j]
             << endl;
    cout << endl;
} //end printShortestDistance

//Constructor
weightedGraphType::weightedGraphType(int size)
                         : graphType(size)
{
    weights = new double*[size];

    for (int i = 0; i < size; i++)
        weights[i] = new double[size];

    smallestWeight = new double[size];
}

//Destructor
weightedGraphType::~weightedGraphType()
{
    for (int i = 0; i < gSize; i++)
        delete [] weights[i];

    delete [] weights;
    delete [] smallestWeight;
}
```

## 最小生成树

考虑图 21-14 中的图，它表示一家公司在七个城市之间的航线连接。每条边上的数字表示维持城市之间连接的某个成本因子。

![](img/f97f778697507bb6fdd80c5991210cba_1386_0.png)

**图 21-14** 城市间的航线连接以及维持这些连接的成本因子

由于财务困难，公司需要关闭尽可能多的连接，同时仍能从一个城市飞往另一个城市（航班不必是直飞）。图 21-15(a)、(b) 和 (c) 的图显示了三种不同的解决方案。

![](img/f97f778697507bb6fdd80c5991210cba_1387_0.png)

**图 21-15** 图 21-14 的图的可能解

图 21-15(a) 中维持剩余连接的总成本因子为 33，图 21-15(b) 中为 28，图 21-15(c) 中为 25。显然，在这三种解决方案中，期望的解决方案是图 21-15(c) 的图所示的方案，因为它给出的成本因子最低。图 21-15 的图称为图 21-14 的图的生成树。

从图 21-15 的图中我们注意到以下内容。每个图都是图 21-14 的图的子图，并且从一个节点到任何其他节点都有唯一路径。这样的图称为树。还有许多其他情况：给定一个带权图，我们需要确定一个权重最小的图，如图 21-15 所示。在本节中，我们给出一个确定此类图的算法。不过，首先我们介绍一些术语。

一个**（自由）树** T 是一种简单图，使得若 u 和 v 是 T 中的两个顶点，则从 u 到 v 存在唯一路径。若树中某个特定顶点被指定为根，则该树称为**有根树**。如果为 T 中的边分配权重，则 T 称为**带权树**。如果 T 是带权树，则 T 的**权重**，记为 W(T)，是 T 中所有边的权重之和。

