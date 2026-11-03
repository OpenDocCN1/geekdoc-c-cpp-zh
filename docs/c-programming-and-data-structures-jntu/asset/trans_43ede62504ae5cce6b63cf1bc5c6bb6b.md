
```c
struct NODE * Create_Tree (char Info, struct NODE *Node)
{
    if (Node == NULL)
    {
        Node = (struct NODE *) malloc(sizeof(struct NODE));
        Node->Info = Info;
        Node->Left_Child = NULL;
        Node->Right_Child = NULL;
        return (Node);
    }

    /* Test for the left child */
    if (Info < Node->Info)
        Node->Left_Child = Create_Tree (Info, Node->Left_Child);

    else
        /* Test for the right child */
        if (Info > Node->Info)
            Node->Right_Child = Create_Tree (Info, Node->Right_Child);
    return(Node);
}

/* Function main */
void main()
{
    int Number = 0;
    char Info;
    char choice;
    int depth;
    struct NODE *T = (struct NODE *) malloc(sizeof(struct NODE));
    T = NULL;
    printf("\n Please enter your choice, 'b' to break:");
    choice = getchar();

    while(choice != 'b')
    {
        fflush(stdin);
        printf("\n Input information of the node: ");
        scanf("%c", &Info);
        T = Create_Tree(Info, T);
        Number++;

        fflush(stdin);
        printf("\n Input choice 'b' to break");
        choice = getchar();
    }
    printf("\n Number of elements in the list is %d", Number);
    printf("\n Tree is \n");
    Output(T, 1);
    depth = Depth(T, 0);
    printf("\n Depth of the above tree is: %d", depth);
}
```

## 16.3 图

图是一组节点（也称为顶点）和一组弧（也称为边）。一个示例图如图 16.4 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_450_0.png)

图 16.4 图

上图中的节点或顶点集合表示为：{A, B, C, D, E}。该图的弧集合为：{(A, B), (A, C), (A, D), (A, E), (C, D), (E, D)}。

如果图中任意两个节点之间都存在路径，即可以从一个节点遍历到图中的任何其他节点，则该图是连通的。否则，该图是非连通的。图 16.5 展示了一个连通图和一个非连通图。

![](img/65953ea584e494f3d396b2252cb5ea53_450_1.png)

图 16.5 连通图与非连通图

## 16.4 C 语言中的图表示

在 C 语言中，图可以表示为数组或链表。考虑下图（图 16.6）：

![](img/65953ea584e494f3d396b2252cb5ea53_451_0.png)

图 16.6 示例图

我们约定如下：

- 如果任意两个节点之间存在边，则写 1，并且
- 如果任意两个节点之间不存在边，则写 0

因此，我们将得到如下表示：

|   | A | B | C | D | E | F |
|---|---|---|---|---|---|---|
| A | 0 | 1 | 0 | 0 | 0 | 1 |
| B | 1 | 0 | 1 | 0 | 0 | 0 |
| C | 0 | 0 | 0 | 1 | 1 | 0 |
| D | 0 | 0 | 1 | 0 | 1 | 0 |
| E | 1 | 0 | 1 | 1 | 0 | 1 |
| F | 1 | 0 | 0 | 0 | 1 | 0 |

图 16.7 图的数组表示

如我们所见，第一行中 A-B 和 A-F 之间的“1”表示 A-B 和 A-F 之间存在边。所有其他 0 表示所述节点之间不存在边（例如，节点 A-C 之间不存在边，用“0”表示）。

图也可以表示为链表形式。在这种情况下，有两种类型的链表节点：头节点（也称为图节点）和链表节点。

- 头节点包含节点的实际信息、指向下一个节点的指针以及指向一条弧的指针。
- 链表节点包含指向一个节点的指针和指向下一条弧的指针。

这两种节点类型可以如图 16.8 所示表示。

![](img/65953ea584e494f3d396b2252cb5ea53_452_0.png)

图 16.8 图中节点的类型

用 C 语言术语来说，我们将弧指针称为 arcptr，将节点指针称为 nodeptr。如果 p 指向表示弧 (A, B) 的链表节点，则 Nodeptr(p) 指向表示图节点 B 的头节点。Next arc(p) 指向表示来自图节点 A 的下一条弧的链表节点。示例图及其对应的链表表示如图 16.9 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_452_1.png)

图 16.9 示例图及其链表表示

请注意，我们使用箭头来表示节点之间弧的方向。因此，这里的 C-E 是有效的，但 E-C 是无效的。包含这种方向的图称为有向图。不以这种方式表示方向的图称为无向图。

让我们来看一下可以与此链表形式的图相关联的各种 C 操作。

节点类型的基本定义如下：

```c
#define MAX 1000
struct nodetype
{
    int point;
    int info;
    int next;
};

struct nodetype node[MAX];
```

### 连接两个节点

以下函数可用于在两个节点之间创建一条弧。它接受两个指针并将它们连接起来形成一条弧。

```c
void join (int x, int y)
{
    int r1, r2;

    /* Search list of arcs originating from node [x] for an arc to node [y] */
    r1 = node [x].point;

    while (r1 >=0 && node[r1].point != y)
    {
        r2 = r1;
        r1 = node[r1].next;
    }

    if (r1 >=0)
        /* node [r1] represents an arc between x and y */
        node[r1].info = 1;

    /* if an arc between x and y does not exist, create it */
    r1 = getnode ();
    node [r1].point = y;
    node [r1].next = -1;
    node [r1].info = 1;

    if (r2 < 0)
        node [x].point = r1;
    else
        node [r2].next = r1;
}
```

删除弧的函数可以编写如下：

```c
void delete (int x, int y)
{
    int r1 = node[x].point;
    int r2 = -1;

    while (r1 >= 0 && node[r1].point != y)
    {
        r2 = r1;
        r1 = node[r1].next;
    }

    if (r1 >= 0)
    {
        /* r1 points to an arc from node[x] to node[y] */
        if (r2 < 0)
            node[x].point = node[r1].next;
        else
            node[r2].next = node[r1].next;

        free (node[r1]);
        return;
    }

    /* do nothing if the arc is not found */
}
```

以下函数可用于测试节点 y 是否与节点 x 相邻。

```c
int isadjacent (int x, int y)
{
    int r = node[x].point;

    while (r >= 0)
        if (node[r].point == y)
            return 1;  /* found */
        else
            r = node[r].next;
    return 0; /* not found */
}
```

最后，以下函数可用于查找特定节点。如果找到，它返回指向 information = x（正在搜索的节点）的头节点的指针，否则返回 null。

```c
int findnode (int graph, int x)
{
    int r = graph;

    while (r >= 0)
    {
        if (node [r].info == x)
            return r; /* found */
        else
            r = node [r].next;
    }
    return -1; /* not found */
}
```

## 16.5 图遍历

遍历图上的所有节点或顶点的过程称为图遍历。遍历图中的节点有多种方法。最常用的方法是：

- 深度优先搜索（DFS）
- 广度优先搜索（BFS）

### 深度优先搜索

在深度优先搜索中，我们需要选择一个顶点作为遍历图的任意顶点。我们将确定该任意顶点的所有相邻顶点。然后，我们需要从邻接表中选择任意一个相邻顶点。现在，访问与所选顶点相邻的所有顶点，然后选择另一个顶点，并访问与该顶点相邻的所有顶点，依此类推。此过程持续进行，直到访问完图中的所有顶点。例如，考虑图 16.10 所示的图。

![](img/65953ea584e494f3d396b2252cb5ea53_455_0.png)

图 16.10

让我们看看如何使用 DFS 方法遍历上图中所示图的所有顶点。

- 我们将任意顶点设为 A。
- 顶点 A 的相邻顶点是 B、H 和 C。选择相邻顶点 B。
- 顶点 B 的相邻顶点是 A、D 和 E。A 已经被遍历或访问过，因此选择顶点 D。
- 顶点 D 的相邻顶点是 B 和 H。B 已经被遍历过，因此选择顶点 H。
- 顶点 H 的相邻顶点是 D、E、A、F 和 G。D 和 A 已经被遍历过，因此选择顶点 E。
- 顶点 E 的相邻顶点是 B 和 H。B 和 H 都已经被访问过，因此回溯到遍历顶点 H，以遍历未访问的顶点 F 和 G。现在，选择顶点 F。
- 顶点 F 的相邻顶点是 C 和 H。H 已经被遍历过，因此选择顶点 C。
- 顶点 C 的相邻顶点是 F 和 G。F 已经被访问过。因此遍历顶点 G。
- 顶点 G 的所有相邻顶点都已访问，因此回溯并确定是否所有相邻顶点都已访问。

DFS 方法帮助我们按序列 A、B、D、H、E、F、C 和 G 遍历上述图。

以下程序演示了深度优先方法。

```c
/* DEPTH FIRST SEARCH TECHNIQUE */

#include<stdio.h>
#define size 50
#define T 1
#define F 0

struct Edge
{
    int terminal;
    struct Edge *next;
};
struct Vertex
{
    int visit;
    int vertex_no;
    char info;
    int path_length;
    struct Edge *Edge_Ptr;
};
void Table(int, int matrix [size][size], struct Vertex vert[size]);
struct Edge *Insert_Vertex (int , struct Edge *);
void DFS ( int , int *dist, struct Vertex vert [size]);
void Input(int , int a [size][size]);
void Output(int, int a [size][size]);

struct Edge * Insert_Vertex (int vertex_no, struct Edge *first)
{
    struct Edge *new1, *current;
```
