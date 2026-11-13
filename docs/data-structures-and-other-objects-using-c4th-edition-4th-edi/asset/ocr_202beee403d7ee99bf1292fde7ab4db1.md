# Self-Test Exercises for Section 15.2

![](bbox=[0.123, 0.182, 0.265, 0.283])

+   8. Write an adjacency matrix for the graph drawn in the margin.

+   9. Consider this adjacency matrix. Are there any loops in the graph?

| | [0] | [1] | [2] | [3] |
|---|---|---|---|---|
| [0] | false | true | false | true |
| [1] | false | true | true | false |
| [2] | false | false | false | false |
| [3] | false | true | true | true |

Which node has the highest in-degree? Which node has the highest out-degree?

+   10. Write a new graph member function to remove the highest-numbered vertex from a graph.

+   11. We have assumed that there are no multiple edges in a graph, and therefore we could store simple true/false values in the adjacency matrix. Describe how adjacency matrices might be used if the graphs have multiple edges.

+   12. Compare and contrast the adjacency lists and edge lists.

+   13. Write a function with one parameter that is a graph. The return value of the function is the total number of edges in the graph.

+   14. Suppose that g is a graph with integer labels. What is the label of vertex 3 at the three points marked here? Assume that the statements are executed one after another, and i is an integer variable.

```
g[3] = 42; // Point 1
i = g[3]; // Point 2
i = 43; // Point 3
```

# FIGURE 15.2 Header File for the Graph Class

# A Header File

```
// FILE: graph.h (part of the namespace main_savitch_15)
// TEMPLATE CLASS PROVIDED: graph<Item> (a class for labeled graphs)
//   The vertices of an n-vertex graph are numbered from 0 to n-1. Each vertex has a
//   label of type Item. It may be any of the C++ built-in types (int, char, etc.), or any
//   class with a default constructor and an assignment operator. The graph may not have
//   multiple edges.
// MEMBER CONSTANTS for the graph<Item> template class:
//   static const size_t MAXIMUM = _______
//      graph::MAXIMUM is the maximum number of vertices that a graph can have.
// CONSTRUCTOR for the graph<Item> template class:
//   graph( )
//      Postcondition: The graph has been initialized with no vertices and no edges.
```