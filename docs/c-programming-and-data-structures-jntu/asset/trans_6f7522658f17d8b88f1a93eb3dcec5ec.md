
```c
new1 = (struct Edge *) malloc(sizeof(struct Edge));
new1->terminal = vertex_no;
new1->next = NULL;
if (!first)
    return (new1);
for (current = first; current->next; current = current->next);
current->next = new1;
return (first);
}

/* Initializing entries */
void Table(int vertex_num, int matrix[size][size],
    struct Vertex vert[size])
{
    int i, j;
    for (i = 0; i < vertex_num; i++)
    {
        vert[i].visit = F;
        vert[i].vertex_no = i + 1;
        vert[i].info = 'A' + i;
        vert[i].path_length = 0;
        vert[i].Edge_Ptr = NULL;
    }

    for (i = 0; i < vertex_num; i++)
        for (j = 0; j < vertex_num; j++)
            if (matrix[i][j] > 0)
                vert[i].Edge_Ptr = Insert_Vertex(j, vert[i].Edge_Ptr);
}

/* Computing path length */
void DFS(int index, int *dist,
    struct Vertex vert[size])
{
    struct Edge *Link;
    vert[index].visit = T;
    vert[index].path_length = *dist;
    *dist += 1;
    for (Link = vert[index].Edge_Ptr; Link; Link = Link->next)
        if (vert[Link->terminal].visit == F)
            DFS(Link->terminal, dist, vert);
}

/* Input function to read adjacency matrix */
void Input(int number, int a[size][size])
{
    int i, j;
    printf("\n Input the adjacency matrix \n");
    for (i = 0; i < number; i++)
    {
        for (j = 0; j < number; j++)
        {
            scanf("%d", &a[i][j]);
        }
        printf("\n");
    }
}

/* Output function */
void Output(int number, int a[size][size])
{
    int i, j;
    printf("\n Adjacency matrix \n");
    for (i = 0; i < number; i++)
    {
        for (j = 0; j < number; j++)
        {
            printf(" %d", a[i][j]);
        }
        printf("\n");
    }
}

/* Function main */
void main()
{
    int i;
    int number, index, dist;
    int a[size][size];
    struct Vertex vert[size];
    struct Edge *List;
    printf("\n Input the number of vertices in the graph: ");
    scanf("%d", &number);
    Input(number, a);
    Output(number, a);

    Table(number, a, vert);
    printf("\n Input the starting vertex 0-%d: ", number - 1);
    scanf("%d", &index);
    dist = 0;
    DFS(index, &dist, vert);
    printf("\n Path length of the vertex from %c", vert[index].info);
    printf("\n Vertex Length Vertex Connectivity \n");
    for (i = 0; i < number; i++)
    {
        printf("\n %c %d ", vert[i].info, vert[i].path_length);
        for (List = vert[i].Edge_Ptr; List; List = List->next)
        {
            printf(" ");
            putchar(List->terminal + 'A');
        }
    }
}
```

## 广度优先搜索

与 DFS 类似，在广度优先搜索中也会选择一个任意顶点。不过，我们需要遍历该任意顶点的所有相邻顶点。这里遍历的是与已访问顶点相邻的未访问顶点。此过程持续进行，直到图中的所有顶点都被访问。

例如，考虑上图。要使用 BFS 方法遍历该图，请选择一个任意顶点，比如 A。

顶点 A 的相邻顶点是 B、C 和 H。选择顶点 B。

顶点 B 的未访问顶点是 D 和 E。

然后遍历顶点 D 和 E。

回到其余顶点，并访问 A 的未访问相邻顶点。

选择顶点 C。顶点 C 的未访问相邻顶点是 F 和 G。

顶点 H、D、E、F 和 G 不再有未访问的相邻顶点。

BFS 方法的遍历过程如图 16.11(a)–(d) 所示。

![](img/65953ea584e494f3d396b2252cb5ea53_459_0.png)

图 16.11

BFS 方法帮助我们按 A、B、H、C、D、E、F 和 G 的顺序遍历上图。

下面的程序演示了广度优先方法。

```c
/* BREADTH FIRST SEARCH TECHNIQUE */

#include <stdio.h>
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
struct Q
{
    int info;
    struct Q *next;
};

void Table(int, int matrix[size][size], struct Vertex vert[size]);
struct Edge *Insert_Vertex(int, struct Edge *);
void BFS(int, struct Vertex vert[size]);
void Input(int, int mat[size][size]);
void Output(int number, int mat[size][size]);
struct Q *Insert_Queue(int vertex_no, struct Q *first);
struct Q *Delete_Queue(int *vertex_no, struct Q *first);

/* Insert data into connectivity list */

struct Edge *Insert_Vertex(int vertex_no, struct Edge *first)
{
    struct Edge *new1, *current;
    new1 = (struct Edge *) malloc(sizeof(struct Edge));
    new1->terminal = vertex_no;
    new1->next = NULL;
    if (!first)
        return (new1);
    for (current = first; current->next; current = current->next);
    current->next = new1;
    return (first);
}

/* Insert vertices into queue */

struct Q *Insert_Queue(int vertex_no, struct Q *first)
{
    struct Q *new1, *current;
    new1 = (struct Q *) malloc(sizeof(struct Q));
    new1->info = vertex_no;
    new1->next = NULL;
    if (!first)
        return (new1);
    for (current = first; current->next; current = current->next);
    current->next = new1;
    return (first);
}

struct Q *Delete_Queue(int *vertex_no, struct Q *first)
{
    struct Q *previous;
    if (!first)
        return (NULL);
    *vertex_no = first->info;
    previous = first;
    first = first->next;
    free(previous);
    return (first);
}

/* Initializing entries */

void Table(int vertex_num, int matrix[size][size],
    struct Vertex vert[size])
{
    int i, j;
    for (i = 0; i < vertex_num; i++)
    {
        vert[i].visit = F;
        vert[i].vertex_no = i + 1;
        vert[i].info = 'A' + i;
        vert[i].path_length = 0;
        vert[i].Edge_Ptr = NULL;
    }

    for (i = 0; i < vertex_num; i++)
        for (j = 0; j < vertex_num; j++)
            if (matrix[i][j] > 0)
                vert[i].Edge_Ptr = Insert_Vertex(j, vert[i].Edge_Ptr);
}

/* Computing path length */

void BFS(int index, struct Vertex vert[size])
{
    struct Q *queue = NULL;
    struct Edge *Link;
    vert[index].visit = T;
    queue = Insert_Queue(index, queue);
    while (queue)
    {
        queue = Delete_Queue(&index, queue);
        for (Link = vert[index].Edge_Ptr; Link; Link = Link->next)
        {
            if (vert[Link->terminal].visit == F)
            {
                vert[Link->terminal].visit = T;
                vert[Link->terminal].path_length = vert[index].path_length + 1;
                queue = Insert_Queue(Link->terminal, queue);
            }
        }
    }
}

/* Input function to read adjacency matrix */
void Input(int number, int mat[size][size])
{
    int i, j;
    printf("\n Input the adjacency matrix \n");
    for (i = 0; i < number; i++)
    {
        for (j = 0; j < number; j++)
        {
            scanf("%d", &mat[i][j]);
        }
        printf("\n");
    }
}

/* Output function to display adjacency matrix */
void Output(int number, int mat[size][size])
{
    int i, j;
    printf("\n Adjacency matrix \n");
    for (i = 0; i < number; i++)
    {
        for (j = 0; j < number; j++)
        {
            printf(" %d", mat[i][j]);
        }
        printf("\n");
    }
}

/* Function main */
void main()
{
    int i, number, index;
    int mat[size][size];
    struct Vertex vert[size];
    struct Edge *List;
    printf("\n Input the number of vertices in the graph: ");
    scanf("%d", &number);
    Input(number, mat);
    Output(number, mat);
    Table(number, mat, vert);
    printf("\n Input the starting vertex 0-%d: ", number - 1);
    scanf("%d", &index);
    BFS(index, vert);
    printf("\n Path length of the vertex from %c", vert[index].info);
    printf("\n Vertex Length Vertex Connectivity \n");
    for (i = 0; i < number; i++)
    {
        printf("\n %c %d ", vert[i].info, vert[i].path_length);
        for (List = vert[i].Edge_Ptr; List; List = List->next)
        {
            printf(" ");
            putchar(List->terminal + 'A');
        }
    }
}
```

## 最短路径问题

正如我们所见，图是通过其边来遍历的。让我们考虑这样一种情况：当从一个地方前往另一个地方时，我们需要确定两地之间的最小距离。这里，两个地点之间的距离被赋为边的权重。

例如，考虑我们想从金奈前往纽约的情况。我们可以经由伦敦从金奈前往纽约，费用为 1500 美元；也可以经由新加坡，费用为 2500 美元。从金奈前往纽约时，我们通常希望经由伦敦，因为旅行费用更低。类似地，在许多应用中，我们需要找到最短路径，即两个顶点之间权重最小的路径。在我们的旅行示例中，顶点指代金奈和纽约这两个地点，权重指代旅行费用。

考虑一个图，其中 S 是源顶点，E 是目标顶点。

图中的路径是指从源顶点到目标顶点的一系列顶点，并且我们沿着两个相邻顶点之间的边前进。各边权重之和称为路径长度。最小长度确定了源顶点与目标顶点之间的最短路径。例如，考虑图 16.12 所示的一个加权图。
