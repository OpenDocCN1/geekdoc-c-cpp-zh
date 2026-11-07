Let $G$ be a graph with $n$ vertices, in which $n > 0$. Let $V(G) = \{v_1, v_2, \ldots, v_n\}$. Let $W$ be a two-dimensional $n \times n$ matrix such that:

$$W(i,j)=\begin{cases}w_{ij} & \text{if }(v_i,v_j)\text{ is an edge in }G\text{ and }w_{ij}\text{ is the weight of the edge }(v_i,v_j)\\\infty & \text{if there is no edge from }v_i\text{ to }v_j\end{cases}$$

The input to the program is the graph and the weight matrix associated with the graph. To make inputting the data easier, we extend the definition of the class `graphType` (using inheritance) and add the function `createWeightedGraph` to create the graph and the weight matrix associated with the graph. Let us call this class `weightedGraphType`. The functions to implement the shortest path algorithm will also be added to this class.

```
class weightedGraphType: public graphType
{
public:
        void createWeightedGraph();
        //Function to create the graph and the weight matrix.
        //Postcondition: The graph using adjacency lists and
        //              its weight matrix is created.
        //
        void shortestPath(int vertex);
        //Function to determine the weight of a shortest path
        //from vertex that is source, to every other vertex
        //in the graph.
        //Postcondition: The weight of the shortest path from
        //              vertex to every other vertex in the
        //              graph is determined.
        //
        void printShortestDistance(int vertex);
        //Function to print the shortest weight from vertex
        //to the other vertex in the graph.
        //Postcondition: The weight of the shortest path from
        //              vertex to every other vertex in the
        //              graph is printed.
        //
        weightedGraphType(int size = 0);
        //Constructor
        //Postcondition: gSize = 0; maxSize = size;
        //              graph is an array of pointers to linked
        //              lists.
        //              weights is a two-dimensional array to
        //              store the weights of the edges.
        //              smallestWeight is an array to store the
        //              smallest weight from source to vertices.
        //
        ~weightedGraphType();
        //Destructor
        //The storage occupied by the vertices and the arrays
        //weights and smallestWeight is deallocated.
};
```