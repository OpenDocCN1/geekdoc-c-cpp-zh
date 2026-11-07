
```cpp
// store the weights of the edges.
// edges is an array to store the edges
// of a minimal spanning tree.
// edgeWeight is an array to store the
// weights of the edges of a minimal
// spanning tree.

~msTreeType();
    //Destructor
    //The storage occupied by the vertices and the arrays
    //weights, edges, and edgeWeights is deallocated.

protected:
    int source;
    double **weights;
    int *edges;
    double *edgeWeights;
};
```

我们将类 `msTreeType` 的 UML 类图和继承层次结构留作练习。函数 `createSpanningGraph` 的定义也留给你作为练习。该函数创建图以及与该图关联的权重矩阵。

下面的 C++ 函数 `minimalSpanning` 实现了前面描述的 Prim 算法：

```cpp
void msTreeType::minimalSpanning(int sVertex)
{
    int startVertex, endVertex;
    double minWeight;

    source = sVertex;

    bool *mstv;
    mstv = new bool[gSize];

    for (int j = 0; j < gSize; j++)
    {
        mstv[j] = false;
        edges[j] = source;
        edgeWeights[j] = weights[source][j];
    }

    mstv[source] = true;
    edgeWeights[source] = 0;

    for (int i = 0; i < gSize - 1; i++)
    {
        minWeight = DBL_MAX;

        for (int j = 0; j < gSize; j++)
            if (!mstv[j])
                for (int k = 0; k < gSize; k++)
                    if (!mstv[k] && weights[j][k] < minWeight)
                    {
                        endVertex = k;
                        startVertex = j;
                        minWeight = weights[j][k];
                    }
        mstv[endVertex] = true;
        edges[endVertex] = startVertex;
        edgeWeights[endVertex] = minWeight;
    } // end for
} // end minimalSpanning
```

函数 `minimalSpanning` 的定义包含三个嵌套的 `for` 循环。因此，在最坏情况下，本节给出的 Prim 算法为 O(n³) 阶。可以设计出 O(n²) 阶的 Prim 算法。本章末尾的编程练习 5 要求你完成这一点。

函数 `printTreeAndWeight` 的定义如下：

```cpp
void msTreeType::printTreeAndWeight()
{
    double treeWeight = 0;

    cout << "Source Vertex: " << source << endl;
    cout << "Edges Weight" << endl;

    for (int j = 0; j < gSize; j++)
    {
        if (edges[j] != j)
        {
            treeWeight = treeWeight + edgeWeights[j];
            cout << "(" << edges[j] << ", " << j << ") "
                 << edgeWeights[j] << endl;
        }
    }

    cout << endl;
    cout << "Minimal Spanning Tree Weight: "
         << treeWeight << endl;
} // end printTreeAndWeight
```

构造函数和析构函数的定义如下：

```cpp
//Constructor
msTreeType::msTreeType(int size)
                : graphType(size)
{
    weights = new double*[size];

    for (int i = 0; i < size; i++)
        weights[i] = new double[size];

    edges = new int[size];
    edgeWeights = new double[size];
}
```

```cpp
//Destructor
msTreeType::~msTreeType()
{
    for (int i = 0; i < gSize; i++)
        delete [] weights[i];
    delete [] weights;
    delete [] edges;
    delete [] edgeWeights;
}
```

> **注意**（拓扑排序）本章还讨论拓扑排序。必要材料位于文件 `TopologicalOrder.pdf` 中。该文件可在 www.cengagebrain.com 获取。要找到该文件，请通过输入本文本的 ISBN 导航到本书页面，然后单击“免费资料”。

## 快速回顾

- 1. 图 $G$ 是一个二元组 $G = (V, E)$，其中 $V$ 是一个有限非空集合，称为 $G$ 的顶点集；$E \subseteq V \times V$，称为边集。
- 2. 在无向图 $G = (V, E)$ 中，$E$ 的元素是无序对。
- 3. 在有向图 $G = (V, E)$ 中，$E$ 的元素是有序对。
- 4. 设 $G$ 是一个图。如果 $H$ 的每个顶点都是 $G$ 的顶点，且 $H$ 中的每条边都是 $G$ 中的边，则图 $H$ 称为 $G$ 的子图。
- 5. 无向图中的两个顶点 $u$ 和 $v$，如果存在从其中一个到另一个的边，则称为邻接的。
- 6. 设 $e = (u, v)$ 是无向图 $G$ 中的一条边。称边 $e$ 关联于顶点 $u$ 和 $v$。
- 7. 关联于单个顶点的边称为自环。
- 8. 在无向图中，如果两条边 $e_1$ 和 $e_2$ 与同一对顶点相关联，则 $e_1$ 和 $e_2$ 称为平行边。
- 9. 如果一个图没有自环也没有平行边，则称为简单图。
- 10. 从顶点 $u$ 到顶点 $v$ 的路径是一个顶点序列 $u_1, u_2, \ldots, u_n$，使得 $u = u_1$、$u_n = v$，且对于所有 $i = 1, 2, \ldots, n - 1$，$(u_i, u_{i+1})$ 是一条边。
- 11. 如果存在从 $u$ 到 $v$ 的路径，则顶点 $u$ 和 $v$ 称为连通的。
- 12. 简单路径是指除第一个和最后一个顶点可能相同外，所有顶点都不同的路径。
- 13. $G$ 中的环是一条首尾顶点相同的简单路径。
- 14. 如果从任一顶点到任一其他顶点都存在路径，则无向图 *G* 称为连通的。
- 15. 一个极大连通顶点子集称为 *G* 的一个连通分量。
- 16. 假设 *u* 和 *v* 是有向图 *G* 中的顶点。如果存在从 *u* 到 *v* 的边，即 (*u*, *v*) ∈ *E*，则称 *u* 邻接到 *v*，且 *v* 从 *u* 邻接。
- 17. 如果有向图 *G* 中任意两个顶点都是连通的，则 *G* 称为强连通的。
- 18. 设 *G* 是一个有 *n* 个顶点的图，其中 *n* > 0。设 *V*(*G*) = { *v*₁, *v*₂, …, *v*ₙ }。邻接矩阵 *A*<sub>G</sub> 是一个二维 *n* × *n* 矩阵，使得如果存在从 *v*ᵢ 到 *v*ⱼ 的边，则 *A*<sub>G</sub> 的第 (*i*, *j*) 个元素为 1；否则，第 (*i*, *j*) 个元素为零。
- 19. 在邻接表表示中，对应于每个顶点 *v* 都有一个链表，使得该链表的每个结点包含顶点 *u*，且 (*v*, *u*) ∈ *E*(*G*)。
- 20. 图的深度优先遍历类似于二叉树的前序遍历。
- 21. 图的广度优先遍历类似于二叉树的逐层遍历。
- 22. 最短路径算法给出给定结点到图中其他每个结点的最短距离。
- 23. 在加权图中，每条边都有一个非负权重。
- 24. 路径 *P* 的权重是路径 *P* 上所有边的权重之和，也称为从 *u* 经 *P* 到 *v* 的权重。
- 25. （自由）树 *T* 是一个简单图，使得如果 *u* 和 *v* 是 *T* 中的两个顶点，则从 *u* 到 *v* 存在唯一路径。
- 26. 如果将树中某个特定顶点指定为根，则该树称为有根树。
- 27. 假设 *T* 是一棵树。如果为 *T* 中的边赋予权重，则 *T* 称为加权树。
- 28. 如果 *T* 是一棵加权树，则 *T* 的权重（记为 *W*(*T*)）是 *T* 中所有边的权重之和。
- 29. 如果 *T* 是图 *G* 的子图且满足 *V*(*T*) = *V*(*G*)，即如果 *G* 的所有顶点都在 *T* 中，则树 *T* 称为图 *G* 的生成树。

## 练习

练习末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述的正误。
  - a. 简单图没有自环，也没有平行边。(2)
  - b. 如果有一条边与两个顶点相关联，则这两个顶点称为连通的。(2)
  - c. 如果图 $G$ 中任意两个顶点都是连通的，则图 $G$ 称为强连通的。(2)
  - d. 如果图的邻接矩阵中某个元素为 1，则相应的顶点是邻接的。(3)
  - e. 在图 $G$ 的邻接表表示中，对应于每个顶点 $v$ 都有一个数组，使得从 $v$ 邻接到的每个顶点都存储在该数组中。(3)
  - f. 图的广度优先遍历类似于逐层遍历二叉树。(5)
  - g. 路径的权重是该路径上一条边的最大权重。(6)
  - h. 每个图都有生成树。(7)
  - i. 图的最小生成树是权重最小的生成树。(7)

使用图 20-17 中的图完成练习 2 至 10。

![](img/b217c421655b51e7494cf3b89bb5432d_1498_0.png)

**图 20-17** 练习 2 至 10 的图

- 2. 在图 20-17(a) 中，找出一条从顶点 0 到顶点 10 的路径。(2)
- 3. 在图 20-17(a) 中，找出一条从顶点 4 经由顶点 6 到顶点 10 的路径。你的路径长度是多少？(2)

