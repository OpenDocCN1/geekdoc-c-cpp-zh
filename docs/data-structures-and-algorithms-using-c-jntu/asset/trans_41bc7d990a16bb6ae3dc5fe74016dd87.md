

outdegree 和 visit 字段。indegree 字段在删除方面非常有用。仅当顶点的 indegree 为零时，才允许删除顶点，即不应有边指向它。否则不允许删除，并会导致程序失败。visit 字段是一个标志，在遍历期间很有用，用于知道是否已访问过。如果为 true，则顶点已遍历，否则未遍历。边的详细信息存储在其结构中，该结构包含两个字段：destination 和 next edge。图 10.21 显示了图数据结构。

![](img/45784b9f0334626143002ec0d63692fd_313_0.png)

![](img/45784b9f0334626143002ec0d63692fd_313_1.png)

![](img/45784b9f0334626143002ec0d63692fd_313_2.png)

### 图 10.21 图数据结构

## 创建图
最初应创建一个图；可以通过初始化图头结构的元数据元素来完成。算法 10.1 给出了创建图的过程。

### Algorithm 10.1

```
creategraph
1. Set count to 0.
2. Set first to NULL.
3. Return graph head.
End creategraph.
```

## 顶点的插入
插入顶点操作用于向图中添加一个顶点。插入后，新顶点将是一个孤立顶点或不与任何其他顶点连接的离散顶点。这是插入过程的第一步。要将此顶点与另一个顶点连接，必须单独插入与其关联的边。将顶点插入图中如图 10.22 所示。

![](img/45784b9f0334626143002ec0d63692fd_314_0.png)

算法 10.2 解释了将顶点插入图中的过程。

### Algorithm 10.2

```
insertvertex(graph, data)
1. GETNODE (AVAIL)    //memory allocation for new vertex.
2. Set data to new vertex
3. Initialize metadata elements in new node
4. Increment graph count    //finding the insertion point or where to
                          //insert the new vertex
5. If graph is empty
    Set graphfirst to new node.
6. Else
    (i) Search for position of insertion
    (ii) If insertion as a first vertex set graphfirst to new vertex
    (iii)Else
        Insert new vertex (sequentially) as last vertex
    (iv) End if
7. End if
End insertvertex.
```

## 顶点的删除
删除顶点操作用于从图中移除一个顶点。要删除顶点，应先搜索它。如果找到，应确保没有边指向该顶点或从该顶点发出，然后删除顶点，否则不允许删除。图 10.23 显示了顶点的删除。

![](img/45784b9f0334626143002ec0d63692fd_314_1.png)

算法 10.3 解释了从图中删除顶点的过程。

### Algorithm 10.3

```
deletevertex(graph, element)
1. If graph is empty
   Print "element not found".
2. End If
3. Search for the vertex to be deleted
4. If not found
   Print "element not found"
Else
   1. If indegree(vertex)>0 or outdegree(vertex)>0
      Print "deletion is not allowed"
   2. Else
      deletevertex
   3. Decrement graph count
   4. Print "vertex deleted successfully"
6. End deletevertex.
```

## 边的插入
插入边操作用于添加连接顶点和目标顶点的边。要插入边，必须指定两个顶点。在有向图中，一个顶点必须指定为源，另一个指定为目标。如果一个顶点需要多条边，则必须为每个相邻顶点分别调用一次此操作。图 10.24 显示了在图中插入边 {B, D}。

![](img/45784b9f0334626143002ec0d63692fd_315_0.png)

### 图 10.24 边的插入

算法 10.4 详细说明了如何将边插入图中。

### Algorithm 10.4

```
insertedge(graph, fromvertex, tovertex)
1. GETNODE(AVAIL) // memory allocation for new edge
   Find and set fromvertex //identify the source vertex.
3. If fromvertex not found
   Print "fromvertex not found"
4. End if
5. Find and set tovertex //identify destination vertex.
6. If tovertex not found.
   Print "tovertex not found".
7. End if
8. Increment outdegree of fromvertex.
9. Increment indegree of tovertex.
10. Set edge destination to tovertex.
11. If edge list of fromvertex is empty.
    1. Set first edge of fromvertex to new edge.
    2. set next edge of new edge to null
    3. Print "insertion is successful"
12. End if
13. Search for insertion point in adjacency list
14. If insertion as a first edge
    Set first edge of fromvertex to new edge
15. Else
    Insert in edge list.
16. End if
17. Print "insertion successful"
18. End insertedge.
```

## 边的删除
删除边操作用于从图中移除一条边。要删除边，必须识别源顶点和目标顶点。因此，搜索顶点列表以找到源顶点。从源顶点的邻接表中识别目标顶点。现在，边已定位并从邻接表中移除。调整 from 和 to 顶点的度并回收内存。删除边 (B, D) 如图 10.25 所示。

![](img/45784b9f0334626143002ec0d63692fd_316_0.png)

### 图 10.25 边的删除

算法 10.5 给出了从图中删除边的过程。

### Algorithm 10.5

```
delete edge(graph, fromvertex, tovertex)
1. If graph is empty
   Print "source vertex not found".
2. End if
3. Find and set fromvertex //identify source vertex.
4. If fromvertex not found.
   Print "from vertex not found".
5. End if
   //identify the destination vertex in adjacency list.
6. If edge list of fromvertex is null.
   Print "tovertex not found".
7. End if
8. Find the tovertex and set the edge.
9. If tovertex not found
   Print "tovertex not found".
10. End if
    //fromvertex, tovertex and edge are located. Now delete edge.
11. Set tovertex to edge destination.
12. Delete edge.
13. Decrement the outdegree of fromvertex.
14. Decrement the indegree of tovertex.
15. Print "edge successfully deleted"
16. End deleteedge.
```

## 搜索顶点
搜索顶点操作用于返回存储在顶点中的数据。这与链表的搜索操作非常相似。算法 10.6 解释了在图中搜索顶点的过程。

### Algorithm 10.6

```
searchvertex(graph, key, item)
1. If graph is empty
   Print "search is not successful as the graph is empty".
2. End if
3. Search for vertex.
4. If vertex is found
    1. Set data(vertex) to item.
    2. Print "search is successful".
5. Else
   Print "search is not successful"
6. End if
7.End searchvertex.
```

## 销毁图
执行删除顶点操作时，应先通过删除其边将其隔离。销毁图操作在删除顶点之前先删除顶点的所有边。删除所有顶点（包括相应的边）即销毁图。算法 10.7 讨论了销毁图的方法。

### Algorithm 10.7

```
destroygraph (graph)
1. If graph is empty
   Return
2. If graph head count>0 loop
    1. If outdegree of vertex>0loop
       1. Delete first edge of vertex
       2. Decrement the outdegree of vertex by 1
    2. End loop
3. End loop
4. End destroygraph.
```

## 操作的实现
上述讨论的操作的实现在程序 10.1 中说明。

### Program 10.1

```
// To PERFORM GRAPH OPERATIONS USING LINKED LIST REPRESENTATION
#include<iostream.h>
#include<alloc.h>
#include<conio.h>
#include<stdlib.h>
typedef struct graph
{
int vertex,weight;
struct graph*next;
}GRAPH;
GRAPH*adj[100],*ptr;
int n,count=0,a,b,i;
void insertvertex() //To Insert Vertex
{
cout<<"Enter Vertex To Be Insert";
cin>>a;
cout<<"Enter Reference Vertex";
cin>>b;
if(a>n||a<1||b>n||b<1)
{
cout<<"Wrong Input";
return;
}
if(count==0)
{
ptr = adj[b];
while(ptr->vertex!=b)
ptr=ptr->next;
if(ptr==NULL)
{
cout<<"Vertex Not Found";
return;
}
}
ptr=(graph*)malloc(sizeof(graph));
ptr->vertex=b;
ptr->weight=1;
ptr->next=adj[a];
adj[a]=ptr;
if(count==0)
count+=2;
else
count++;
cout<<"Vertex"<<a<<"Is Inserted And Edge Is Established from"<<a<<"To"<<b;
}
void insertedg() //To Insert Edge
```

