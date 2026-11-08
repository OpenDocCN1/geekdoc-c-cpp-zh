
A solution of the Königsberg bridge problem is given in the book *Discrete Mathematics: Theory and Applications (Revised Edition)* listed in Appendix H.

Over the past 200 years, graph theory has been applied to a variety of applications. Graphs are used to model electrical circuits, chemical compounds, highway maps, and so on. They are also used in the analysis of electrical circuits, finding the shortest route, project planning, linguistics, genetics, social science, and so forth. In this chapter, you will learn about graphs and their applications in computer science.

## Graph Definitions and Notations

To facilitate and simplify our discussion, we borrow a few definitions and terminology from set theory. Let $X$ be a set. If $x$ is an element of $X$, then we write $x \in X$. (The symbol “$\in$” means “belongs to”.) A set $Y$ is called a **subset** of $X$ if every element of $Y$ is also an element of $X$. If $Y$ is a subset of $X$, we write $Y \subseteq X$. (The symbol “$\subseteq$” means “is a subset of”.) The intersection of sets $A$ and $B$, written $A \cap B$, is the set of all of the elements that are in $A$ and $B$; that is, $A \cap B = \{x \mid x \in A \text{ and } x \in B\}$. (The symbol “$\cap$” means “intersection”.) The union of sets $A$ and $B$, written $A \cup B$, is the set of all of the elements that are in $A$ or in $B$; that is, $A \cup B = \{x \mid x \in A \text{ or } x \in B\}$. (The symbol “$\cup$” means “union”. Notice that $x \in A \cup B$ means $x$ is in $A$ or $x$ is in $B$ or $x$ is in both $A$ and $B$. Also, the symbol “$\mid$” is read as “such that”.)

For sets $A$ and $B$, the set $A \times B$ is the set of all of the ordered pairs of elements of $A$ and $B$; that is, $A \times B = \{(a,b) \mid a \in A, b \in B\}$.

A **graph** $G$ is a pair, $G = (V, E)$, in which $V$ is a finite nonempty set, called the set of **vertices** of $G$, and $E \subseteq V \times V$. That is, the elements of $E$ are the pairs of elements of $V$. $E$ is called the set of **edges**.

Let $V(G)$ denote the set of vertices and $E(G)$ denote the set of edges of a graph $G$. If the elements of $E(G)$ are ordered pairs, $G$ is called a **directed graph** or digraph; otherwise, $G$ is called an **undirected graph**. In an undirected graph, the pairs $(u,v)$ and $(v,u)$ represent the same edge. If $(u,v)$ is an edge in a directed graph, then sometimes the vertex $u$ is called the **origin** of the edge, and the vertex $v$ is called the **destination**.

Let $G$ be a graph. A graph $H$ is called a **subgraph** of $G$ if $V(H) \subseteq V(G)$ and $E(H) \subseteq E(G)$; that is, every vertex of $H$ is a vertex of $G$, and every edge in $H$ is an edge in $G$.

To learn more about sets and graph terminology, the interested reader is referred to the book *Discrete Mathematics: Theory and Applications (Revised Edition)*, listed in Appendix H.

A graph can be shown pictorially. The vertices are drawn as circles, and a label inside of the circle represents the vertex. In an undirected graph, the edges are drawn using lines. In a directed graph, the edges are drawn using arrows. Moreover, in a directed graph, the tail of a pictorial directed edge is the origin, and the head is the destination.

### EXAMPLE 20-1

Figure 20-3 shows some examples of undirected graphs.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1407_0.png)

**FIGURE 20-3** Various undirected graphs

### EXAMPLE 20-2

Figure 20-4 shows some examples of directed graphs.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1408_0.png)

**FIGURE 20-4** Various directed graphs

For the graphs of Figure 20-4, we have

$V(G_1)=\{1,2,3,4,5\}$

$V(G_2)=\{0,1,2,3,4,5,6,7,8\}$

$E(G_1)=\{(1,2),(1,4),(2,3),(2,5),(4,2),(4,3),(4,5)\}$

$E(G_2)=\{(0,1),(0,3),(1,2),(1,5),(2,0),(2,7),(3,4),(3,6),(4,8),(5,4),(6,0),(8,5),(8,6)\}$

Let $G$ be an undirected graph. Let $u$ and $v$ be two vertices in $G$. Then, $u$ and $v$ are called **adjacent** if there is an edge from one to the other, that is, $(u,v)\in E(G)$. Let $e=(u,v)$ be an edge in $G$. We then say that edge $e$ is **incident** on the vertices $u$ and $v$. An edge incident on a single vertex is called a **loop**. If two edges, $e_1$ and $e_2$, are associated with the same pair of vertices, then $e_1$ and $e_2$ are called **parallel edges**. A graph is called a **simple graph** if it has no loops and no parallel edges. There is a **path** from $u$ to $v$ if there is a sequence of vertices $u_1,u_2,\ldots,u_n$ such that $u=u_1$, $u_n=v$, and $(u_i,u_{i+1})$ is an edge for all $i=1,2,\ldots,n-1$. Vertices $u$ and $v$ are called **connected** if there is a path from $u$ to $v$. A **simple path** is a path in which all of the vertices, except possibly the first and last vertices, are distinct. A **cycle** in $G$ is a simple path in which the first and last vertices are the same. $G$ is **connected** if there is a path from any vertex to any other vertex. A maximal subset of connected vertices is called a **component** of $G$.

Let $G$ be a directed graph, and let $u$ and $v$ be two vertices in $G$. If there is an edge from $u$ to $v$, that is, $(u,v)\in E(G)$, then we say that $u$ is **adjacent to** $v$ and $v$ is **adjacent from** $u$. The definitions of the paths and cycles in $G$ are similar to those for undirected graphs. $G$ is called **strongly connected** if any two vertices in $G$ are connected.

Consider the directed graphs of Figure 20-4. In $G_1$, $1$-$4$-$2$-$5$ is a path from vertex 1 to vertex 5. There are no cycles in $G_1$. In $G_2$, $0$-$3$-$4$-$8$-$5$ is a path from vertex 0 to vertex 5; $6$-$0$-$1$-$2$-$7$ is a path from vertex 6 to vertex 7; $0$-$1$-$2$-$0$ is a cycle; $3$-$4$-$8$-$6$-$0$-$3$ is a cycle; and $0$-$1$-$5$-$4$-$8$-$6$-$0$ is a cycle.

## Graph Representation

To write programs that process and manipulate graphs, the graphs must be stored—that is, represented—in computer memory. A graph can be represented (in computer memory) in several ways. Now we discuss two commonly used methods: adjacency matrices and adjacency lists.

### Adjacency Matrix

Let $G$ be a graph with $n$ vertices, in which $n \ge 0$. Let $V(G)=\{v_1,v_2,\ldots,v_n\}$. The adjacency matrix $A_G$ of $G$ is a two-dimensional $n \times n$ matrix such that the $(i,j)$th entry of $A_G$ is 1 if there is an edge from $v_i$ to $v_j$; otherwise, the $(i,j)$ entry is zero. That is:

$$A_G(i,j)=\begin{cases}1 & \text{if }(v_i,v_j)\in E(G)\\0 & \text{otherwise}\end{cases}$$

In an undirected graph, if $(v_i,v_j)\in E(G)$, then $(v_j,v_i)\in E(G)$, so $A_G(i,j)=1=A_G(j,i)$. It follows that the adjacency matrix of an undirected graph is symmetric.

### EXAMPLE 20-3

Consider the directed graphs of Figure 20-4. The adjacency matrices of the directed graphs $G_1$ and $G_2$ are as follows:

$$A_{G_1}=\begin{bmatrix}0&1&0&1&0\\0&0&1&0&1\\0&0&0&0&0\\0&1&1&0&1\\0&0&0&0&0\end{bmatrix}\qquad\text{and}\qquad A_{G_2}=\begin{bmatrix}0&1&0&1&0&0&0&0&0\\0&0&1&0&0&1&0&0&0\\1&0&0&0&0&0&0&1&0\\0&0&0&0&1&0&0&0&0\\0&0&0&0&0&0&0&0&1\\0&0&0&0&1&0&0&0&0\\1&0&0&0&0&0&0&0&0\\0&0&0&0&0&0&0&0&0\\0&0&0&0&0&1&1&0&0\end{bmatrix}$$

- 4. Traverse the graph.
- 5. Print the graph.

We will add more operations on a graph when we discuss a specific application or a particular graph later in this chapter.

How a graph is represented in computer memory depends on the specific application. For illustration purposes, we use the adjacency list (linked list) representation of graphs. Therefore, for each vertex, v, the vertices adjacent to v (in a directed graph, also called the immediate successors) are stored in the linked list associated with v.

To manage the data in a linked list, we use the class `unorderedLinkedList`, discussed in Chapter 16.

The labeling of the vertices of a graph depends on a specific application. If you are dealing with the graph of cities, you could label the vertices as the names of the cities. However, to write algorithms to manipulate a graph as well as to simplify the algorithm, there must be some ordering to the vertices. That is, we must specify the first vertex, the second vertex, and so on. Therefore, for simplicity, throughout this chapter, we assume that the n vertices of the graphs are numbered 0, 1, ..., n − 1. Moreover, it follows that the way we will design to implement the graph algorithm will not be a template.

## Graphs as ADTs

In this section, we describe the class to implement graphs as an abstract data type (ADT) and provide the definitions of the functions to implement the operations on a graph.

The following class defines a graph as an ADT:

```cpp
class graphType
{
public:
    bool isEmpty() const;
        //Function to determine whether the graph is empty.
        //Postcondition: Returns true if the graph is empty;
        //              otherwise, returns false.

    void createGraph();
        //Function to create a graph.
        //Postcondition: The graph is created using the
        //              adjacency list representation.

    void clearGraph();
        //Function to clear graph.
        //Postcondition: The memory occupied by each vertex
        //              is deallocated.

    void printGraph() const;
        //Function to print graph.
        //Postcondition: The graph is printed.
```
