adjacency list in O(n) time. In addition, when all the edges are to be processed, the total edges of G may be processed in time O(n + e).

In case of a directed graph, the outgoing degree of any vertex i may be determined by counting the number of nodes on its adjacency list. For computing an incoming degree of vertex i, we have to traverse the adjacency lists of each of the other vertices to confirm whether it is incident on i. In other words, we will have to search for the vertex i in the adjacency lists of all other vertices. This is a tedious task; hence, it is better to keep another set of lists in addition to the adjacency list called inverse adjacency lists. The inverse adjacency list for a vertex i is a list of all vertices j to which i is adjacent to. Inverse adjacency list can be used to compute the incoming degree of a vertex. We shall learn about inverse adjacency list in Section 8.3.4.

Program Code 8.3 depicts the implementation of storing a graph as an adjacency list.

# PROGRAM CODE 8.3

```
// Class for the node of the graph class GraphNode
//
public:
int vertex; // The adjacent node
GraphNode* next;
GraphNode()
{
vertex = 0;
next = null;
}
}
// class for storing graph as adjacency list
class Graph
{
// List of headnodes containing list of connected
// vertices
GraphNode* headnodes[max];
int n;
int visited[max];
public:
Graph(); // Constructor to initialize all
headnodes to null
void create(); // To create graph
// To initialize the visited array to false
void initialize_visited();
void BFS(int v); // Breadth-first search
```