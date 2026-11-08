

## 第 24 章

现在，让我们用算法的方式解释整个过程。下面是算法的输入、输出以及步骤：

输入：一个连通图 G，其顶点标记为 v1, v2, ……, vn

输出：G 的一棵生成树 T

**方法：**

- 1. （访问一个顶点）令 v1 为 T 的根，并设置 L = v1（其中 L 表示最后访问的顶点）。
- 2. （查找一条未检查的边和一个与 L 相邻的未检查顶点）对于所有与 L 相邻的顶点，选择边 (L, vk)，其中 k 是最小下标，使得将 (L, vk) 添加到 T 中不会形成回路。如果不存在这样的边，则转到步骤 3；否则，将边 (L, vk) 添加到 T，并设置 L = vk。在新的 L 值处重复步骤 2。
- 3. （回溯或终止）如果 x 是 L 在 T 中的父节点，则设置 L = x，并在新的 L 值处应用步骤 2。另一方面，如果 L 在 T 中没有父节点（即 L = v1），则 DFS 终止，T 即为 G 的生成树。

下面是用 C 语言实现 DFS 的代码：

```c
/* The following program outputs a spanning tree of the input connected graph */
#include<stdio.h>

int main()
{
    int a[10][10],s[10],vis[10],top=-1,i,j,m,n;
    printf("enter the number of nodes");
    scanf("%d",&n);
    for(i=0;i<n;i++)
    {
        for(j=0;j<n;j++)
        {
            printf("enter the path between %d and %d:-",i,j);
            scanf("%d",&a[i][j]);
        }
    }
    printf("enter the starting vertex");
    scanf("%d",&m);
    for(i=0;i<n;i++)
    {
        vis[i]=0;
    }
    top++;
    s[top]=m;
    vis[m]=1;
    while(top>=0)
    {
        i=s[top];
        top--;
        printf("%d ",i);
        for(j=0;j<n;j++)
        {
            if((a[i][j]==1)&&(vis[j]==0))
            {
                top++;
                s[top]=j;
                vis[j]=1;
            }
        }
    }
    return 0;
}
```

在下一节中，让我们学习最小生成树。

### 最小生成树

通常，在一个连通图中，可能存在不止一棵生成树。如果带权连通图 G 的一棵生成树的权重是该连通图中所有其他生成树中最小的，那么它被称为最小生成树。确定带权连通图 G 的最小生成树的两个最流行的算法如下：

- Prim 算法
- Kruskal 算法

让我们逐一讨论这两种算法。

### Prim 算法

Prim 算法为带权连通无向图 G 寻找一棵最小生成树。它采用解决问题时的贪心方法，即选择那些显然能构成最小生成树的路径。为此，我们将带权连通无向图 G 作为算法的输入，并得到一棵最小生成树 T 作为输出。以下是 Prim 算法的步骤：

- 1. 在图 G 中取一个顶点 v₀，使得 T = {(v₀), ∅}，其中 T 的第一个元素表示顶点集，第二个元素表示边集。
- 2. 在 E（G 的边集）中找到边 (v₀, v₁)，使得其一个端点 v₀ 在 T 中，且其权重最小。将 v₁ 和边 e₁ 并入 T。因此，我们得到 T = {(v₀, v₁), (e₁)}。
- 3. 选择下一条边 eᵢⱼ = (vᵢ, vⱼ)，使得它的一个端点 vᵢ 在 T 中，另一个端点 vⱼ 不在 T 中（即 eᵢⱼ 不应与 T 中的边形成回路），并且边 eᵢⱼ 的权重尽可能小。将边 eᵢⱼ 和顶点 vⱼ 并入 T。
- 4. 重复步骤 3，直到 T 包含 G 的所有顶点。此时，集合 T 将给出 G 的最小生成树。

下面是用 C 语言实现 Prim 算法的代码：

```c
/* Finding the minimum spanning tree of a graph G using Prim’s method. */
#include<stdio.h>

typedef struct min
{
    int row;
    int colm;
    int value;
}smin;

smin c[20][20];

int main()
{
    int count=0,i,j,n,a[20][20],b[20][20],min,h;
```

### Kruskal 算法

为此，我们将带权连通无向图 G 作为算法的输入，并得到一棵最小生成树 T 作为输出。以下是 Kruskal 算法的步骤：

- 1. 找到一条边，使其权重 w(eᵢ) 最小。
- 2. 此时，我们有 3 个子步骤：
  - a. 如果已经选择了边 e₁, e₂, ..., eₙ，则选取一条边 e₍ₙ₊₁₎，使得对于 i = 1 到 n，它不等于 eᵢ。
  - b. 边 e₁, e₂, ..., eₙ, e₍ₙ₊₁₎ 不形成回路。
  - c. 在满足步骤 2(b) 条件的前提下，边 e₍ₙ₊₁₎ 的权重 w(e₍ₙ₊₁₎) 尽可能小。
- 3. 当 G 的所有顶点都在 T 中时，停止。

下面是用 C 语言实现 Kruskal 算法的代码：

```c
/* Finding the minimum spanning tree of a graph G using Kruskal’s method. */
# include<stdio.h>
# include<stdlib.h>
struct node
{
    int weight, i, fin;
    struct node *next;
    struct node *prev;
};
struct node *head,*c,*temp,*cur,*cur1;

void main()
{
    int term, i,count=0,vis[20],n;
    printf("\n\n\t Enter the number of edges :-> ");
    scanf("%d",&term);
    head=(struct node *)malloc(sizeof(struct node));
    head->i=0;
    head->fin=0;
    head->weight=1;
    head->next=NULL;
    head->prev=NULL;
    cur=head;

    for(i=1;i<=term;i++)
    {
        temp=(struct node *)malloc(sizeof(struct node));
        printf("\n\n\t Enter initial vertex :-> ");
        scanf("%d",&temp->i);
        printf("\n\n\t Enter the final vertex :-> ");
        scanf("%d",&temp->fin);
        printf("\n\n\t Enter the weight :-> ");
        scanf("%d",&temp->weight);
        if((temp->weight)<(cur->weight))
        {
            cur1=cur;
            while((temp->weight)<(cur1->weight))
            {
                cur1=cur1->prev;
            }
            temp->next=cur1->next;
            cur1->next->prev=temp;
            cur1->next=temp;
            temp->prev=cur1;
        }
        else
        {
            temp->next=NULL;
            cur->next=temp;
            temp->prev=cur;
            cur->next;
        }
    }
    printf("\n\n\tEnter the number of vertices:->");
    scanf("%d",&n);
    for(i=1;i<=n;i++)
    {
        vis[i]=0;
    }
    c=head->next;
    printf("The nodes that form the minimum spanning tree are:->");
    while(c)
    {
        if((vis[c->init]==0)&&(vis[c->fin]==0))
        {
            printf("\n\t Initl ver -> %d Fin ver -> %d weight -> %d ", c->init,c->fin,c->weight);
            vis[c->init]=1;
            vis[c->fin]=1;
        }
        c=c->next;
    }
    return 0;
}
```

接下来，让我们讨论 Dijkstra 算法。

### Dijkstra 算法

Dijkstra 算法是一种图搜索算法，它解决图的单源最短路径问题，并生成一棵最短路径树。在这种情况下所做的假设是，与边相关联的所有代价或权重都应为非负值。给定图中的一个顶点，该算法会找出该顶点与图中其他每个顶点之间的最小距离。这类算法主要用于通信网络和旅行商问题。它旨在确定图中源顶点与网络中其他每个顶点之间的最短路径。

为了解释该算法，我们需要了解一些基本的最短距离度量，整个算法都基于这些度量。假设 uᵢ 是从源顶点到任意顶点 'j' 的最短距离。此外，我们定义距离 dᵢⱼ ≥ 0 为弧 (i, j) 的长度。然后，Dijkstra 算法通过定义紧接其后继顶点的标号（例如 vⱼ）来进行，如下所示：

$$[u_j, i] = [u_i + d_{ij}, i], \text{ where } d_{ij} \ge 0$$

在开始算法时，我们将起始顶点的标号定义为 [0, −]，这表示该顶点没有前驱。Dijkstra 算法中的顶点标号有两种类型：临时标号和永久标号。最初，我们总是为图中的每个顶点关联一个临时标号。当且仅当可以通过其他路径找到到该顶点的更短路线，并且该路径确保它仍然是一棵树时，临时标号才会被修改。此时，当找不到更好的路径时，我们将临时标号的状态改为永久标号，如下所示：

