If the number of vertices and edges in the graph are known ahead of time, the space complexity can also be expressed as O ( | E | + | V | ), where | E | is the total number of edges in G and | V | is the number of nodes or vertices.

# Time complexity

In the worst case, breadth-first search has to traverse through all paths to all possible nodes, thus the time complexity of this algorithm asymptotically approaches O(b^p). However, the time complexity can also be expressed as O ( | E | + | V | ), since every vertex and every edge will be explored in the worst case.

# Completeness

Breadth-first search is said to be a complete algorithm because if there is a solution, breadth-first search will find it regardless of the kind of graph. But in case of an infinite graph where there is no possible solution, it will diverge.

# Optimality

Breadth-first search is optimal for a graph that has edges of equal length, since it always returns the result with the fewest edges between the start node and the goal node. But generally, in real-world applications, we have weighted graphs that have costs associated with each edge, so the goal next to the start does not have to be the cheapest goal available.

# Applications of Breadth-First Search Algorithm

Breadth-first search can be used to solve many problems such as:

+   - Finding all connected components in a graph G.
+   - Finding all nodes within an individual connected component.
+   - Finding the shortest path between two nodes, u and v, of an unweighted graph.
+   - Finding the shortest path between two nodes, u and v, of a weighted graph.

# PROGRAMMING EXAMPLE

# 2. Write a program to implement the breadth-first search algorithm.

```
```c
#include <stdio.h>
#define MAX 10
void breadth_first_search(int adj[][MAX],int visited[],int start)
{
    int queue[MAX],rear =-1,front = -1, i;
    queue[++rear] = start;
    visited[start] = 1;
    while(rear != front)
    {
        start = queue[++front];
        if(start == 4)
            printf("%5t",start);
        else
            printf("%c \t",start + 65);
        for(i = 1; i < MAX; i++)
        {
            if(adj[start][i] == 1 && visited[i] == 0)
            {
                queue[++rear] = i;
                visited[i] = 1;
            }
        }
    }
}
int main()
```
```