
## 9.5 Single Source Shortest Path

The shortest path weight from a vertex u ∈ V to a vertex v ∈ V in the weighted graph is the minimum cost of all paths from u to v. If there exists no such path from vertex u to vertex v, then the weight of the shortest path is ∞.

We can also define as
δ(u, v) = {
  Min(w(p): u → v) if there is a path from u to v
  ∞
  otherwise
}

### NEGATIVE WEIGHTED EDGES

The negative weight cycle is a cycle whose total weight is –ve. No path from starting vertex S to a vertex on the cycle can be a shortest path.

Since a path can run around the cycle many many times so it may get any –ve costing other word we can say that a negative cycle invalidates the notion of distance based on edge weights.

If some path from S to v contains a negative cost cycle, there does not exist a shortest path otherwise there exist one that is simple.

![](img/1faaa0256577c74e8a61f42967760aa8_327_0.png)

### RELAXATION TECHNIQUE

This technique consists of testing whether we can improve the shortest path found so far, if so update the shortest path. A relaxation step may or may not decrease the value of the shortest path estimate.

### ALGORITHM RELAX(u,v,w)

- 1. if d[u] + w(u,v) < d[v]
- 2. then d[v] <- d[u] + w(u,v)
- 3. π[v] <- u

Example:

![](img/1faaa0256577c74e8a61f42967760aa8_328_0.png)

### ALGORITHM INITIALIZE_SINGLE_SOURCE(G,S)

- 1. for each vertex v ∈ V[G]
- 2. do d[v] ← ∞
- 3. π[v] ← Nil
- 4. d[s] ← 0

### 9.5.1 Bellman-Ford Algorithm

Bellman-Ford algorithm solves the single source shortest path problem in the general case in which edges of a given digraph can have –ve weight as long as G contains no negative cycles.

It uses d[u] as an upper bound on the distance d[u,v] from u to v. The algorithm progressively decreases an estimate d[v] on the weight of the shortest path from the source vertex S to each vertex v in V until it achieves the actual shortest path.

This algorithm returns TRUE if the given digraph contains no –ve cycle that are reachable from source vertex S otherwise FALSE.

### ALGORITHM BELLMAN-FORD(G,W,S)

- 1. INITIALIZE-SINGLE-SOURCE(G,S)
- 2. for each edge i = 1 to V[G] – 1 do
- 3. for each edge (u,v) ∈ E(G) do
- 4. RELAX(u,v,w)
- 5. for each edge (u,v) in E(G)
- 6. do if d[u] + w(u,v) < d[v]
- 7. then return FALSE
- 8. Return TRUE

![](img/1faaa0256577c74e8a61f42967760aa8_329_0.png)

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | ∞ | ∞ | ∞ | ∞ | ∞ |
| | 0 | | | | |
| 1 | | 6 | | | 7 |
| 2 | | | 11 | 2 | |
| 3 | | | 9 | | |
| 4 | | | 4 | | |
| 5 | | 2 | | | |
| 6 | | | | -2 | |
| 7 | No effect | | | | |

Parent (π)

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | Nil | Nil | Nil | Nil | Nil |
| 1 | | S | | | S |
| 2 | | | U | U | |
| 3 | | | Y | | |
| 4 | | | X | | |
| 5 | | V | | | |
| 6 | | | | U | |
| 7 | No effect | | | | |

### STEPS

**For i=1** Consider the vertex S
Now Since the Adj(S) = (U,X) now implement Relax with (S,U) and (S,X)
Relax(s,u,w)
d[s] + w(s,u) < d[u] = 0 + 6 < ∞ so d[u] = 6 and π(u) = S
Relax(s,x,w)
d[s] + w(s,x) < d[x] = 0 + 7 < ∞ so d[x] = 7 and π(x) = S

**For i=2** Consider the vertex U (min(u,x))
Now Since the Adj(U) = (V,X,Y) now implement Relax with (U,V),(U,X) and (U,Y)
Relax(u,v,w)
d[u] + w(u,v) < d[v] = 6 + 5 < ∞ so d[v] = 11 and π(v) = u
Relax(u,x,w)
d[u] + w(u,x) < d[x] = 6 + 8 < 7 (False)
Relax(u,y,w)
d[u] + w(u,y) < d[y] = 6 + -4 < ∞ so d[y] = 2 and π(y) = u

**For i=3** Consider the vertex Y (minimum)
Now Since the Adj(Y) = (V,S) now implement Relax with (Y,V) and (Y,S)
Relax(y,v,w)
d[y] + w(y,v) < d[v] = 2 + 7 < 11 so d[v] = 9 and π(v) = y
Relax(y,s,w)
d[y] + w(y,s) < d[s] = 2 + 2 < 0 (False)

**For i=4** Consider the vertex X (minimum)
Now Since the Adj(X) = (V,Y) now implement Relax with (X,V) and (X,Y)
Relax(x,v,w)
d[x] + w(x,v) < d[v] = 7 + -3 < 9 so d[v] = 4 and π(v) = x
Relax(x,y,w)
d[x] + w(x,y) < d[y] = 7 + 9 < 2 (False)

**For i=5** Consider the vertex V (minimum)
Now Since the Adj[V] = (U) now implement Relax with (V,U)
Relax(v,u,w)
d[v] + w(v,u) < d[u] = 4 + -2 < 6 so d[u] = 2 and π(u) = v

**For i=6** Consider the vertex U (minimum)
Now Since the Adj[U] = (V,Y,X) now implement Relax with (U,V),(U,Y),(U,X)
Relax(u,v,w)
d[u] + w(u,v) < d[v] = 2 + 5 < 4 (False)
Relax(u,y,w)
d[u] + w(u,y) < d[y] = 2 + -4 < 2 so d[y] = -2 and π(y) = u
Relax(u,x,w)
d[u] + w(u,x) < d[x] = 2 + 8 < 7 (False)

**For i=7** Consider the vertex Y (minimum)
Now Since the Adj[Y] = (V,S) now implement Relax with (Y,V),(Y,S)
Relax(y,v,w)
d[y] + w(y,v) < d[v] = -2 + 7 < 4 (False)
Relax(y,s,w)
d[y] + w(y,s) < d[s] = -2 + 2 < 0 (False)

So the shortest path graph is

![](img/1faaa0256577c74e8a61f42967760aa8_331_0.png)

### 9.5.2 Dijkstra's Algorithm

Dijkstra's algorithm solves the single source shortest path problem when all edges have non-negative weights. It is a greedy algorithm and similar to Prim's algorithm. Algorithm starts at the source vertex S it grows a tree T that ultimately spans all vertices reachable from S. Vertices are added to T in order of distance i.e., first S, then the vertex closest to S, then the next closest and so on.

### ALGORITHM DIJKSTRA(G,W,S)

- 1. INITIALIZE-SINGLE-SOURCE(G,S)
- 2. S <- {}
- 3. Initialize Priority Queue i.e., Q <- V[G]
- 4. While Q != ∅
- 5. do u <- Extract_min(Q)
- 6. S <- S ∪ {u}
- 7. for each vertex v ∈ Adj[u]
- 8. do RELAX(u,v,w)

Example:

![](img/1faaa0256577c74e8a61f42967760aa8_332_0.png)

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | ∞ | ∞ | ∞ | ∞ | ∞ |
| | 0 | | | | |
| 1 | | 10 | | | 5 |
| 2 | | 8 | 14 | 7 | |
| 3 | | | 13 | | |
| 4 | | | 9 | | |

Parent (π)

| Steps | S | U | V | Y | X |
|---|---|---|---|---|---|
| | Nil | Nil | Nil | Nil | Nil |
| 1 | | S | | | S |
| 2 | | X | X | X | |
| 3 | | | Y | | |
| 4 | | | U | | |

**STEP-1** Consider the vertex S
Now Since the Adj(S) = (X,U) now implement Relax with (S,U) and (S,X,Y)
Relax(s,u,w)
d[s] + w(s,u) < d[u] = 0 + 10 < ∞ so d[u] = 10 and π(u) = S
Relax(s,x,w)
d[s] + w(s,x) < d[x] = 0 + 5 < ∞ so d[x] = 5 and π(x) = S delete S

**STEP-2** Consider the vertex X (minimum)
Now Since the Adj(X) = (U,Y,V) now implement Relax with (X,U) (X,Y) and (X,V)
Relax(x,u,w)
d[x] + w(x,u) < d[u] = 5 + 3 < 10 so d[u] = 8 and π(u) = X
Relax(x,v,w)
d[x] + w(x,v) < d[v] = 5 + 9 < ∞ so d[v] = 14 and π(v) = X
Relax(x,y,w)
d[x] + w(x,y) < d[y] = 5 + 2 < ∞ so d[y] = 7 and π(y) = X delete X

**STEP-3** Consider the vertex Y (minimum)
Now Since the Adj(Y) = (S,V) now implement Relax with (Y,S) (Y,V)
Relax(y,s,w)
d[y] + w(y,s) < d[s] = 7 + 7 < 0 (False)
Relax(y,v,w)
d[y] + w(y,v) < d[v] = 7 + 6 < 14 so d[v] = 13 and π(v) = Y
delete Y

**STEP-4** Consider the vertex U (minimum)

Now Since the Adj(U) = (V,X) now implement Relax with (U,V) (U,X)

Relax(u,v,w)
d[u] + w(u,v) < d[v] = 8 + 1 < 13 so d[v] = 9 and π(v) = U

Relax(u,x,w)
d[u] + w(u,x) < d[x] = 8 + 2 < 5 (False)

delete U

So final shortest path matrix is

![](img/1faaa0256577c74e8a61f42967760aa8_334_0.png)

Dsv = Dsx + Dxu + Duv = 5 + 3 + 1 = 9

### PROGRAM USING DIJKSTRA ALGORITHM

```c
#include<stdio.h>
#include<conio.h>
#define INFINITY 9999
#define MAX 10
void createGraph(int G[MAX][MAX],int n);
void dijkstra(int G[MAX][MAX],int n,int startnode);
int main()
{
 int G[MAX][MAX],i,j,n,u;
 char ch;
 //input the number of vertices
 printf("\nEnter no. of vertices:");
 scanf("%d",&n);
 createGraph(G,n);
 printf("\nEnter the starting node.:");
 fflush(stdin);
 scanf("%c",&ch); //read the starting vertex
 u= toupper(ch)-65; //convert to its equivalent numeric value i.e. a=0,b=1,c=2 and so on....
 dijkstra(G,n,u);
 return 0;
}

//create the graph by using the concepts of adjacency matrix.
void createGraph(int G[MAX][MAX],int n)
{
 int i,j;
 //read the adjacency matrix
 printf("\nEnter the adjacency matrix:\n");
 for(i=0;i<n;i++)
 for(j=0;j<n;j++)
 scanf("%d",&G[i][j]);
}

void dijkstra(int G[MAX][MAX],int n,int startnode)
{
 int cost[MAX][MAX],distance[MAX],pred[MAX];
 int visited[MAX],count,mindistance,nextnode,i,j;
 char version='A';
 //pred[] stores the predecessor of each node
 //count gives the number of nodes seen so far
 //create the cost matrix
 for(i=0;i<n;i++)
 for(j=0;j<n;j++)
 if(G[i][j]==0)
 cost[i][j]=INFINITY;
 else
 cost[i][j]=G[i][j];
 //initialize pred[], distance[] and visited[]
 for(i=0;i<n;i++)
 {
 distance[i]=cost[startnode][i];
 pred[i]=startnode;
 visited[i]=0;
 }
 distance[startnode]=0;
}
```
