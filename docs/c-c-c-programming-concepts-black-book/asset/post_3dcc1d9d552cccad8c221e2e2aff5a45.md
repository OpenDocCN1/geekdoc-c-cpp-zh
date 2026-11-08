
Table 24.5: Comparison between Separate Chaining and Open Addressing

|  | **Separate Chaining** | **Open Addressing** |
|---|---|---|
| **Hash Function** | Hash function is defined in such a way that it results in the uniform distribution of the elements in a hash table. | Hash function is defined in such a way that it results in the uniform distribution of the elements as well as avoids clustering. |
| **Implementation** | It is easy to implement though its overhead is high. | Implementation of open addressing highly depends on the selection of hash function. Therefore, it is a tricky job to correctly implement open addressing. |

Next, let’s learn about graphs, in detail.

## Graphs

A graph G = (V, E) is a set of vertices and edges, where V is a non-empty set of vertices and E is a finite set of edges, which can be empty, such that each edge (a, b) is identified by an unordered pair of vertices. Suppose for a graph of six vertices, V = {A, B, C, D, E, F} and E = {(A, B), (C, C), (D), (E), (F), (A), (D)}. If a pair of nodes makes the ordered set of edges, then the graph is known as a directed graph or digraph. In the area of computer science, graphs are commonly used in representing communication networks and flow of computation. Some graphs, used for such minimization problems, also have a weight associated with every edge, indicating the cost of visiting one node from the other. Such graphs are known as weighted graphs.

Graphs are of high utility value with respect to many real world applications. The area of graph theory is particularly of high interest in the entire computer science domain because we can easily map the graphs into suitable data structures and start the computations in algorithmic way. This approach saves a lot of time because for complex graphs, where a computer system can solve the problem within few microseconds, handling them in real life by a person would take days to solve them. Following are the multiple ways to map a graph into a program:

- a. **Adjacency List**—Allows us to store the vertices as the records of objects. In this case, every vertex stores a list of vertices that are adjacent to it.
- b. **Incidence List**—Allows us to store the vertices and edges as the records or objects. For an incidence list, each vertex in a graph stores the list of edges incident on it and each edge stores the list of vertices incident on it.
- c. **Adjacency Matrix**—Refers to a two-dimensional matrix, where rows represent the source vertices and the columns represent the destination vertices. The cost is filled up at the intersection point of the two vertices, in case of weighted graphs.
- d. **Incidence Matrix**—Refers to a two-dimensional matrix filled with binary values, where the rows represent the vertices and the columns represent the edges. It is a binary matrix with only zero or one entry in it. The entries at the intersection generally indicate whether a vertex at a row is incident to an edge at a column. If so, then we mark the intersection with one; else, we mark it with zero.

Both adjacency matrix and incidence matrix are primarily used for array implementation. With arrays, the maintenance overhead is less and we just need to allocate a chunk of memory for the entire graph. However, there are two problems associated with array implementation, which are given as follows:

- In case the structure of a graph is complex, the static two-dimensional array will consume large amount of memory, and for large computations, there is a memory overflow.
- For a sparse matrix, an incidence matrix contains a lot of NULL or 0 entries, which unnecessarily consumes memory resources of the system.

## Chapter 24

### Method

- 1. Let v1 be the root of T. Form the set V = {v1};
- 2. (Add new edges) Consider the vertices of V in the order consistent with the original labeling. Then, for each vertex ‘x’ of V, add the edge (x, vi) to T, where ‘i’ is the minimum index such that adding the edge (x, vi) to T does not produce a cycle. If no edge can be added, then stop. T is a spanning tree for G. After all the vertices of V have been considered, go to the step 3.
- 3. Replace V with all the children ‘v’ in T of the vertices x of V, where the edges (x, v) are added in the step 2. Go back and repeat the step 2 for the new set of V.

Following is the implementation of BFS in the C language.

```c
/* The following program outputs a spanning tree of the input connected graph */
#include<stdio.h>

int main()
{
    int q[10],vis[10],a[10][10],rear=-1,front=0,t[10],p,m,n,i,j;
    printf("enter the number of nodes\n");
    scanf("%d",&n);
    for(i=0;i<n;i++)
    {
        for(j=0;j<n;j++)
        {
            printf("enter 1 if a path exists betwn vertex %d and %d otherwise 0:-",i,j);
            scanf("%d",&a[i][j]);
        }
    }
    for(i=0;i<n;i++)
    {
        vis[i]=0;
    }
    printf("\nenter the starting vertex and the destination vertex:-");
    scanf("%d%d",&m,&p);
    rear++;
    q[rear]=m;
    t[m]=999;
    vis[m]=1;

    while(front<n)
    {
        i=q[front];
        front++;
        for(j=0;j<n;j++)
        {
            if((a[i][j]==1)&&(vis[j]==0))
            {
                {
                    q[rear]=j;
                    vis[j]=1;
                    t[j]=i;
                }
            }
        }
    }
    printf("\nthe path from %d to %d is:-",m,p);
    printf("%d->",p);
    while(p!=m)
    {
        printf("%d->",t[p]);
        p=t[p];
    }
    return 0;
}
```

## DFS

The way DFS works is somewhat different and more interesting than BFS. Although both BFS and DFS find a spanning tree in a connected graph, unlike BFS, DFS uses the backtracking method. Moreover, the DFS execution requires a stack for the backtracking mechanism.

In DFS, we start the search by expanding the first child node of the connected graph by going deeper until a goal node is found or we encounter a terminal node, which has no children. The search then backtracks, returning to the recent last node, which it did not finish exploring.

Now, let’s find a spanning tree T from a connected graph G using the DFS procedure. Consider the following connected graph G:

G = {V, E}

V = {a, b, c, d, e, f, g, h, i, j, k}

E = {(a, b), (a, d), (b, c), (c, d), (c, e), (d, e), (e, f), (e, g), (f, h), (g, h), (h, i), (h, j), (h, k)}

First, choose an ordering of vertices, say {a, b, c, d, e, f, g, h, i, j, k}, and then, select ‘a’ as the root of T. The vertex ‘a’ is said to be visited. Next, select the edge (a, x), where ‘x’ is the first level in the designated order that does not form a cycle with those edges already chosen in T. In this case, we add the edge (a, b), which is now said to be examined; and thereby, becomes a tree edge. In this context, ‘a’ is the parent of ‘b’ and ‘b’ is the child of ‘a’.

In general, while we are at some vertex ‘x’, two situations might arise, which are as follows:

**Situation 1**—If there are some unexamined edges that are incident on ‘x’, then we consider the edge (x, y), where ‘y’ is the first vertex in the designated ordering on the vertices for which (x, y) is unexamined. In this situation, we can have two cases, given as follows:

- **Case 1**—If ‘y’ has not been previously visited, then visit ‘y’, select (x, y) as the tree edge, and continue the search from ‘y’. In this case, ‘x’ is the parent of ‘y’.
- **Case 2**—If ‘y’ has been visited previously, then reject the edge (x, y), consider it examined, and proceed further to select another unexamined edge (x, z) incident on ‘x’, where ‘z’ is the first vertex from which (x, z) is an unexamined edge. Each such rejected edge in the context of DFS is called a back edge.

In the preceding example, we would select the edge (b, c), continue the search at ‘c’, and select (c, d). Then, we would continue the search at ‘d’, by first rejecting the edge (d, a) and then selecting the edge (d, e). At ‘e’, we reject the edge (e, c) and select (e, f). Continuing in this manner, we select (f, g), reject (g, e), select (g, h), reject (h, f), and select (h, i).

At this point, we are going to present a second general situation.

**Situation 2**—If all the edges incident on ‘x’ have already been examined, then we return to the parent of ‘x’ and continue the search from there. In this case, the vertex ‘x’ is said to be completely scanned. Moreover, the process of returning to the parent of ‘x’ is known as backtracking.

Therefore, in the preceding example, since there are no unexamined edges left at ‘i’, we must backtrack to ‘h’ and continue the search from ‘h’. Then, we select (h, j) and (j, k) and finally reject (k, h). Actually, we are through because there are no more unexamined edges. The DFS procedure then terminates when the search returns to the root and all the vertices have been visited.
