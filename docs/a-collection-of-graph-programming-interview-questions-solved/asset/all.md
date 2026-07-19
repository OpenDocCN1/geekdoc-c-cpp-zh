![](images/00266.jpeg)

A collection of Graph Programming Interview Questions Solved in C++

Antonio Gulli

Copyright © 2015 Antonio Gulli

All rights reserved.

ISBN:

ISBN-13:

“Graph” is the second of a series of 25 Chapters devoted to algorithms, problem solving and C++ programming.

DEDICATION

To my father Elio and my mother Maria.

For your priceless help during all my life

ACKNOWLEDGMENTS

Thanks to Gaetano Mendola  for code reviewing

Table of Contents

[1 Implementing a direct graph](#part0000_split_005.html__Toc415584877)

[Solution](#part0000_split_005.html__Toc415584878)

[Code](#part0000_split_005.html__Toc415584879)

[2 Choosing matrices or adjacency lists](#part0000_split_006.html__Toc415584880)

[Solution](#part0000_split_006.html__Toc415584881)

[3 Implementing a BFS visit](#part0000_split_007.html__Toc415584882)

[Solution](#part0000_split_007.html__Toc415584883)

[Code](#part0000_split_007.html__Toc415584884)

[Complexity](#part0000_split_007.html__Toc415584885)

[4 Erdős number](#part0000_split_008.html__Toc415584886)

[5 Implementing a DFS visit](#part0000_split_009.html__Toc415584887)

[Solution](#part0000_split_009.html__Toc415584888)

[Code](#part0000_split_009.html__Toc415584889)

[Complexity](#part0000_split_009.html__Toc415584890)

[6 How to detect a cycle in a graph](#part0000_split_010.html__Toc415584891)

[Solution](#part0000_split_010.html__Toc415584892)

[Code](#part0000_split_010.html__Toc415584893)

[Complexity](#part0000_split_010.html__Toc415584894)

[7 Given two nodes in an undirected graph, find the path connecting them](#part0000_split_011.html__Toc415584895)

[Solution](#part0000_split_011.html__Toc415584896)

[Code](#part0000_split_011.html__Toc415584897)

[Complexity](#part0000_split_011.html__Toc415584898)

[8 Solving mazes](#part0000_split_012.html__Toc415584899)

[Solution](#part0000_split_012.html__Toc415584900)

[9 Given a direct acyclic graph, implement a topological sort](#part0000_split_013.html__Toc415584901)

[Solution](#part0000_split_013.html__Toc415584902)

[Code](#part0000_split_013.html__Toc415584903)

[Complexity](#part0000_split_013.html__Toc415584904)

[10 Detecting a bipartite graph](#part0000_split_014.html__Toc415584905)

[Solution](#part0000_split_014.html__Toc415584907)

[Code](#part0000_split_014.html__Toc415584908)

[Complexity](#part0000_split_014.html__Toc415584909)

[11 Given a connected graph, compute the minimum spanning tree (MST)](#part0000_split_015.html__Toc415584910)

[Solution](#part0000_split_015.html__Toc415584911)

[Code](#part0000_split_015.html__Toc415584912)

[\](#part0000_split_015.html__Toc415584913)

[12](#part0000_split_016.html__Toc415584914)

[13 Find the strongly connected components in a direct graph](#part0000_split_017.html__Toc415584915)

[Solution](#part0000_split_017.html__Toc415584916)

[Code](#part0000_split_017.html__Toc415584917)

[Complexity](#part0000_split_017.html__Toc415584918)

[14 Covering DFS Trees](#part0000_split_018.html__Toc415584919)

[15 Find an Hamiltonian cycle](#part0000_split_019.html__Toc415584920)

[Solution](#part0000_split_019.html__Toc415584921)

[Code](#part0000_split_019.html__Toc415584922)

[16 Find the articulation points in a graph](#part0000_split_020.html__Toc415584923)

[Solution](#part0000_split_020.html__Toc415584924)

[Code](#part0000_split_020.html__Toc415584925)

[Complexity](#part0000_split_020.html__Toc415584926)

[17 Find the shortest path in a graph with non-negative edge weight](#part0000_split_021.html__Toc415584927)

[Solution](#part0000_split_021.html__Toc415584928)

[Code](#part0000_split_022.html__Toc415584929)

[Complexity](#part0000_split_022.html__Toc415584930)

[18 Find MST(Minimum Spanning Tree) using Kruskal Algorithm](#part0000_split_023.html__Toc415584931)

[Solution](#part0000_split_023.html__Toc415584932)

[Complexity](#part0000_split_023.html__Toc415584933)

[19 Find the longest path in a DAG](#part0000_split_024.html__Toc415584934)

[Solution](#part0000_split_024.html__Toc415584935)

[Code](#part0000_split_024.html__Toc415584936)

[Complexity](#part0000_split_024.html__Toc415584937)

[20 Find MST (Minimum Spanning Tree) using Prim Algorithm](#part0000_split_025.html__Toc415584938)

[Solution](#part0000_split_025.html__Toc415584939)

[Complexity](#part0000_split_025.html__Toc415584940)

[21 Find all pairs shortest paths using the Floyd-Warshall Algorithm](#part0000_split_026.html__Toc415584941)

[Solution](#part0000_split_026.html__Toc415584942)

[Complexity](#part0000_split_026.html__Toc415584943)

[22 Find all the single source shortest paths using Bellman Ford Algorithm](#part0000_split_027.html__Toc415584944)

[Solution](#part0000_split_027.html__Toc415584945)

[Complexity](#part0000_split_027.html__Toc415584946)

[23 Independent set of intervals](#part0000_split_028.html__Toc415584947)

[Solution](#part0000_split_028.html__Toc415584948)

[Complexity](#part0000_split_028.html__Toc415584949)

[24 Dominant set of intervals](#part0000_split_029.html__Toc415584950)

[Solution](#part0000_split_029.html__Toc415584951)

[Complexity](#part0000_split_029.html__Toc415584952)

[25 Weighted dominant set of intervals](#part0000_split_030.html__Toc415584953)

[Solution](#part0000_split_030.html__Toc415584954)

[26 Weighted shortest paths with cost associated to the nodes](#part0000_split_031.html__Toc415584955)

[Solution](#part0000_split_031.html__Toc415584956)

[27 Find the flow network using Ford–Fulkerson’Algorithm](#part0000_split_032.html__Toc415584957)

[Solution](#part0000_split_032.html__Toc415584958)

[Complexity](#part0000_split_032.html__Toc415584959)

[28 Assignment matching problem](#part0000_split_033.html__Toc415584960)

[Solution](#part0000_split_033.html__Toc415584961)

[29 Find an Eulerian circuit](#part0000_split_034.html__Toc415584962)

[Solution](#part0000_split_034.html__Toc415584963)

[Code](#part0000_split_034.html__Toc415584964)

[Complexity](#part0000_split_034.html__Toc415584965)

[30 Scheduling](#part0000_split_035.html__Toc415584966)

[Solution](#part0000_split_035.html__Toc415584967)

[Complexity](#part0000_split_035.html__Toc415584968)

## 1  Implementing a direct graph

A graph data structure ![](images/00001.jpeg) involves a finite set of nodes or vertices ![](images/00002.jpeg) and a set of ordered pairs ![](images/00003.jpeg) called edges or arcs connecting two nodes. A graph might have labels associated to the nodes and/or to the edges, thus denoting different attributes (such as names, costs, capacity, length, colours). A direct graph is a graph where the edges are associated to a direction, which is typically represented with an arrow.

 ![](images/00004.jpeg)![](images/00005.jpeg)

![](images/00006.jpeg) ![](images/00007.jpeg)

### Solution

The first direct graph implementation represents a node and an edge as a C++ struct. In addition a collection of nodes is memorized in a ![](images/00008.jpeg) and all the edges originating from each node are memorized in a![](images/00009.jpeg). This representation is known as Adjacency list. In this particular implementation each node has a unique identifier NodeID, a label NodeWeight and another label representing the name of the node.  Indeed each edge stores the destination NodeID, a label EdgeWeightI representing the weight of the edge and another label representing the name of the edge.

The second direct graph implementation represents a Graph using a matrix of size ![](images/00010.jpeg) where n is the number of nodes. This representation is known ad Adjacency Matrix.

### Code

const std::string emptyString;

//

// Direct Graph

// with Adjacent lists

class  Graph

{

public:

 typedef  unsigned  int  NodeID;

 typedef  unsigned  int  EdgeID;

 typedef  int  NodeWeight;

 typedef  int  EdgeWeight;

 struct  Edge

              {

                            Edge(NodeID  nid, EdgeWeight  wt,

 const std::string & lb)

                            : v(nid), w(wt), label(lb)  {};

 const  NodeID v;

 const  EdgeWeight w;

 const std::string label;

              };

 struct  Node

              {

                            Node(NodeWeight  wt, const std::string & l) :

                                          w(wt), label(l){};

 NodeWeight w;

                            std::string label;

              };

 // all nodes

 typedef std::vector<Node> Nodes;          

 // edges from a node

 typedef std::forward_list<Edge> EdgesList;

 // all edges (id -> edgeList)

 typedef std::vector<EdgesList> Edges;     

 // allocate |V| lists of edges

              Graph(NodeID  V = 0, EdgeID  E = 0)

              {

 if (V)

                            {

                                          _nodes.reserve(V); _outdegree.reserve(V);

                            }

 if (E)

                                          _edges.reserve(E);

              };

 void reserveNodes(NodeID  n)

              { _nodes.reserve(n); _outdegree.reserve(n); }

 void reserveEdges(EdgeID  n)

              { _edges.reserve(n); }

 //

 // we can have multiple edge (v1, v2)

 void addEdge(NodeID  v1,

 NodeID  v2,

 EdgeWeight  w = 0,

 const std::string & label = emptyString)

              {

 if (v1 > _nodes.size() || v2 > _nodes.size())

return;

 Edge e(v2, w, label);

                            _edges[v1].push_front(e);

                            _outdegree[v1]++;

              }

 //

 // nodes are unique

 void addNode(NodeWeight  w = 0,

 const std::string & label = emptyString)

              {

 EdgesList el;

 Node n(w, label);

_nodes.push_back(n); // another node

_edges.push_back(el); // with its EdgeList

                            _outdegree.push_back(0);

              }

 const  EdgesList & edges(NodeID  v) const

{ return _edges[v]; };

 Graph::NodeID outdegree(NodeID  v) const

{ return _outdegree[v]; }

 const  Nodes & nodes() const

{ return _nodes; };

 NodeID numNodes() const

{ return _nodes.size(); };

 EdgeID numEdges() const

{ return _edges.size(); };

private:

 Edges  _edges;

 Nodes  _nodes;

              std::vector<Graph::NodeID> _outdegree;

              Graph(const  Graph& g) = delete;

 Graph& operator=(const  Graph& g) = delete;

};

std::ostream & operator << (std::ostream & os,

 const  Graph & g)

{

 Graph::NodeID id = 0;

 for (const  auto & n : g.nodes())

              {

 os << " node=" << id << " weight=" << n.w <<

 " label=" << n.label << std::endl;

 for (const  auto & e : g.edges(id))

 os << " ->" << e.v << " w=" << e.w <<

 " label=" << n.label

<< " lableEdge=" << e.label << std::endl;

                            ++id;

              }

 return  os;

}

//

// Undirect Graph

// with Adjacency Matrix

template<typename  T>

class  Matrix

{

public:

              Matrix(const  Matrix&) = delete;

 Matrix& operator=(const  Matrix&) = delete;

              Matrix(unsigned  int  dim1, unsigned  int  dim2)

                            : _M(new  T*[dim1]), _dim1(dim1), _dim2(dim2)

              {

 for (unsigned  int i = 0; i < dim1; ++i)

_M[i] = new  T[dim2];

              }

              Matrix(unsigned  int  dim1, unsigned  int  dim2,

 T  defaultValue)

: Matrix(dim1, dim2)

              {

 for (unsigned  int i = 0; i < _dim1; ++i)

 for (unsigned  int j = 0; j < _dim2; ++j)

_M[i][j] = defaultValue;

              }

              Matrix(Matrix&& aMatrix) {

_dim1 = aMatrix._dim1;

_dim2 = aMatrix._dim2;

_M = aMatrix._M;

 aMatrix._dim1 = 0;

 aMatrix._dim2 = 0;

 aMatrix._M = nullptr;

              }

              ~Matrix()

              {

 for (unsigned  int i = 0; i < _dim1; ++i)

 delete[] _M[i];

 delete[] _M;

              }

 T & operator()(const  unsigned  int  i,

 const  unsigned  int  j)

              {

 return _M[i][j];

              }

 T & operator()(const  unsigned  int  i,

 const  unsigned  int  j) const

              {

 return _M[i][j];

              }

 unsigned  int dim1() const { return _dim1; };

 unsigned  int dim2() const { return _dim2; };

 friend std::ostream & operator <<(std::ostream & out,

 const  Matrix<T>& m)

              {

 for (unsigned  int i = 0; i < m._dim1; ++i){

 for (unsigned  int j = 0; j < m._dim2; ++j)

 out << m._M[i][j] << ' ';

 out << std::endl;

                            }

 return  out;

              }

 void swap(Matrix & other)

              {

std::swap(_M, other._M);

std::swap(_dim1, other._dim1);

std::swap(_dim2, other._dim2);

              }

private:

 T** _M;

 unsigned  int _dim1, _dim2;

};

//

// MatrixGraph

class  MatrixGraph{

 MatrixGraph& operator=(const  MatrixGraph&) = delete;

public:

 typedef  unsigned  int  NodeID;

 typedef  int  weight;

              MatrixGraph(NodeID  numNodes)

                            : n(numNodes)

              {

M = new  weight*[n];

 for (NodeID i = 0; i < n; ++i)

                            {

M[i] = new  weight[n];

 for (NodeID j = 0; j < n; ++j)

                                                        M[i][j] = 0;

                            }

              }

              ~MatrixGraph()

              {

 for (NodeID i = 0; i < n; ++i)

 delete[] M[i];

 delete[] M;

              }

              MatrixGraph(const  MatrixGraph& m)

              {

n = m.getNumNodes();

M = new  weight*[n];

 for (NodeID i = 0; i < n; ++i)

                            {

M = new  weight*[n];

memcpy(M[i], m.M[i], sizeof(int)*n);

                            }

              }

 NodeID size() const { return n; }

 const  weight & operator()(NodeID  i, NodeID  j) const

{ return M[i][j]; }

 weight & operator()(NodeID  i, NodeID  j)

{ return M[i][j]; }

 NodeID getNumNodes() const { return n; }

private:

 NodeID n;

 weight **M;

};

std::ostream& operator << (std::ostream & os, const  MatrixGraph & g)

{

 for (MatrixGraph::NodeID i = 0; i < g.size(); ++i){

 for (MatrixGraph::NodeID j = 0;

j < g.size(); ++j)

 os << g(i, j) << ' ';

 os << std::endl;

              }

 return  os;

}

void test()

{

 Graph G;

G.addNode(10, "donald duck");

G.addNode(1, "daisy duck");

G.addNode(1, "antonio");

G.addNode(1, "milena");

G.addNode(1, "lorena");

G.addNode(1, "mambo");

G.addNode(1, "salsa");

G.addNode(1, "adriana");

              G.addEdge(0, 2);

G.addEdge(1, 2, 10, "important");

              G.addEdge(1, 3);

              G.addEdge(2, 3);

              G.addEdge(2, 5);

              G.addEdge(2, 6);

              G.addEdge(4, 5);

              G.addEdge(5, 5);

              G.addEdge(5, 4);

              G.addEdge(5, 100);

              std::cout << G;

MatrixGraph mgA(5);

              mgA(0, 1) = 3;  mgA(1, 2) = 2; mgA(1, 3) = 2;

              mgA(2, 3) = mgA(3, 4) = 1;  mgA(4, 0) = 1;

              std::cout << mgA;

}

## 2  Choosing matrices or adjacency lists

Let us assume that we have a direct graph ![](images/00011.jpeg) with ![](images/00012.jpeg) nodes and ![](images/00013.jpeg)edges and that every pointer takes ![](images/00014.jpeg) bits, when is it more appropriate to use a matrix and when is it better to use adjacency lists to represent the graph?

### Solution

The matrix needs ![](images/00015.jpeg) bits, while the adjacency lists need ![](images/00016.jpeg) pointers for each starting list of ![](images/00017.jpeg) bits and ![](images/00018.jpeg) cells of ![](images/00019.jpeg) bits (![](images/00020.jpeg) for the pointer to the next cell and an additional ![](images/00021.jpeg) for the pointer to the node). Therefore combining all the information, we need to solve in ![](images/00022.jpeg) the formula ![](images/00023.jpeg)

## 3 Implementing a BFS visit

Breadth-first-Search (BFS) is a visiting strategy for a graph where a node is first visited and then all adjacent nodes are visited in turn.

### Solution

This is a classical interview question which can be implemented by using a simple queue. At the beginning the root node is enqueued and marked as visited. Then a node is dequeued and all the adjacent nodes not yet visited are enqueued for future visit in turn. The process is repeated until the queue is empty.

### Code

void bfs(const  Graph & g, Graph::NodeID  nid)

{

 // queue of visited nodes

              std::deque<Graph::NodeID> queue;       

 // bfs on unknown node

 if (nid >= g.numNodes())                                         

 return;

              std::vector<bool> visited(g.numNodes(), false);

              visited[nid] = true;

              queue.push_back(nid);

std::cout << "Start bfs" << std::endl;

 while (!queue.empty())

              {

 const  Graph::NodeID id = queue.front();

                            queue.pop_front();

std::cout << "Visited: " << id << std::endl;

 for (const  auto & e : g.edges(id))

                            {

 if (!visited[e.v])

                                          {

visited[e.v] = true;

                                                        queue.push_back(e.v);

                                          }

                            }

              }

std::cout << "End bfs" << std::endl << std::endl;

}

### Complexity

Space complexity is ![](images/00024.jpeg) for the queue and ![](images/00025.jpeg), if the graph is represented using an adjacency list, or ![](images/00026.jpeg) if an adjacency matrix is adopted. Time complexity is ![](images/00027.jpeg) , where ![](images/00028.jpeg) may vary between ![](images/00029.jpeg) and ![](images/00030.jpeg)) , depending on how sparse the graph is.

## 4   Erdős number

Paul Erdős is a famous mathematician who wrote more than 1500 scientific articles. His direct co-authors have distance 1 from him, while their respective co-authors have distance 2. Recursively, whoever has a collaboration with authors at distance ![](images/00031.jpeg)from Erdős will therefore be at distance ![](images/00032.jpeg) (also denoted as Erdős (author)=K). The author of this book has Erdős (“Antonio Gulli”)=3 because he wrote a paper with “Fabrizio Sebastiani” who, in turn, wrote a paper with “Micheal Anthony Steel”, who is a direct co-author of Erdős.  Erdős numbers can be computed with a slight variation of the BFS visit and this implementation is left as an exercise.

## 5  Implementing a DFS visit

Depth-first-Search (DFS) is a visiting strategy for a graph, where the visit starts from a selected root node and the exploration is run as far as possible along each branch before backtracking to the first not yet visited children.

### Solution

This is another classical interview question which can be solved by using either recursion or iteration.

The dfs method implements a recursive solution which starts from the root node sid and it keeps a boolean vector of visited nodes and their colours. For each node the colour is ‘w’ (white) at the very beginning, ‘g’ (gray) when the node is visitedand ‘b’ (black) when all the adjacent nodes are also visited.  In addition the time, when the node is visited, is stored in the vector timing.

The dfsStack method implements an iterative solution where the root node is inserted in the stack. Then the top of the stack is removed and all the adjacent not yet visited nodes are put on the stack itself. The process is repeated until the stack is empty.

### Code

void dfsUtilRich(const  Graph & g, Graph::NodeID  sid,

              std::vector<bool> & visited,

              std::vector<Graph::NodeID> & colour,

              std::vector<Graph::NodeID> & timing,

 unsigned  int & time)

{

std::cout << "Starting dfsUtilRich on " <<

 sid << std::endl;

 visited[sid] = true;

 colour[sid] = 'g'; // gray

              ++time;

 timing[sid] = time;

 for (const  auto & e : g.edges(sid))

 if (!visited[e.v])

                            dfsUtilRich(g, e.v, visited, colour, timing, time);

 colour[sid] = 'b'; //black

              ++time;

}

void dfs(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes()) // dfs on unknown node

 return;

 unsigned  int time = 0;

              std::vector<bool> visited(g.numNodes(), false);

 // white

              std::vector<Graph::NodeID> colour(g.numNodes(), 'w');

              std::vector<Graph::NodeID> timing(g.numNodes(), 0);

              visited[sid] = true;

std::cout << "Starting dfs on " <<

 sid << std::endl;

 for (const  auto & e : g.edges(sid))

              {

 if (!visited[e.v])

                            {

visited[e.v] = true;

                                          dfsUtilRich(g, e.v, visited,

                                                        colour, timing, time);

                            }

              }

std::cout << "End dfs" << std::endl << std::endl;

}

void dfsStack(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes()) // dfs on unknown node

 return;

              std::stack<Graph::NodeID> nodesToBeVisited;

              std::vector<bool> visited(g.numNodes(), false);

              visited[sid] = true;

              nodesToBeVisited.push(sid);

std::cout << "Starting dfs on " << sid << std::endl;

 while (!nodesToBeVisited.empty())

              {

 const  Graph::NodeID nid = nodesToBeVisited.top();

 bool myFullExploredNode = true;

 for (const  auto & e : g.edges(nid))

                            {

 if (!visited[e.v])

                                          {

visited[e.v] = true;

                                                        nodesToBeVisited.push(e.v);

std::cout << "Visited: " << e.v << std::endl;

myFullExploredNode = false;

 break;

                                          3}

                            }

 if (myFullExploredNode)

                                          nodesToBeVisited.pop();

              }

std::cout << "End dfs" << std::endl << std::endl;

}

### Complexity

Space complexity is ![](images/00033.jpeg) for the stack and ![](images/00034.jpeg), if the graph is represented using an adjacency list or ![](images/00035.jpeg) if an adjacency matrix is adopted. Time complexity is ![](images/00036.jpeg), where ![](images/00037.jpeg) may vary between ![](images/00038.jpeg) and ![](images/00039.jpeg) , depending on how sparse the graph is.

## 6  How to detect a cycle in a graph

### Solution

A DFS visit can detect a cycle, if there is a back edge during the visit of the graph. By using the notation defined in the above solution, this condition is represented by a transition from a grey node to a grey node.

### Code

This implementation is left as an exercise.

### Complexity

The complexity here is the same as DFS.

## 7  Given two nodes in an undirected graph, find the path connecting them 

### Solution

A simple solution is to visit the graph with DFS order starting from one of the two nodes and stopping the visit as soon as the other node is found. During this process the visited nodes are stored into a stack. At the end the stack will contain the desired path.

### Code

This implementation is left as an exercise.

### Complexity

The complexity is the same as DFS.

## 8  Solving mazes

Let’s suppose to have a maze as the one represented in this figure. What is the best way to find the exit?

![http://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/MAZE_40x20_DFS_no_deadends.png/220px-MAZE_40x20_DFS_no_deadends.png](images/00040.gif)

### Solution

The interested reader can think about how to represent the maze with a graph ![](images/00041.jpeg) and what the most appropriate visiting strategies on ![](images/00042.jpeg) are.

## 9  Given a direct acyclic graph, implement a topological sort

A topological sort of a [directed graph](http://en.wikipedia.org/wiki/Directed_graph) is a linear ordering of its [vertices](http://en.wikipedia.org/wiki/Vertex_(graph_theory)) such that for every directed edge ![](images/00043.jpeg) from vertex ![](images/00044.jpeg) to vertex ![](images/00045.jpeg) comes before ![](images/00046.jpeg) in the ordering. A topological ordering is possible, if and only if the graph has no directed cycles. Such graphs are called “directed acyclic graphs” (DAG). 

### Solution

Given a DAG, the topological sort is obtained by visiting the nodes with a BFS and storing the nodes into a stack stk. At the end of the process the stack will contain the topologically sorted nodes. The interested reader should modify the code in order to verify the presence of cycles, if the graph is not a DAG (left as exercise).

### Code

void topologicalSortUtil(const  Graph & g,

 Graph::NodeID  sid,

              std::vector<bool> & visited,

              std::stack<Graph::NodeID> &stk)

{

 visited[sid] = true;

std::cout << "\t topologicalSortUtil"

<< sid << std::endl;

 for (const  auto & e : g.edges(sid))

 if (!visited[e.v])

                            topologicalSortUtil(g, e.v, visited, stk);

 stk.push(sid);

}

void topologicalSort(const  Graph & g)

{

              std::vector<bool> visited(g.numNodes(), false);

              std::stack<Graph::NodeID> stk;

 for (Graph::NodeID nid = 0; nid < g.numNodes(); ++nid)

 if (!visited[nid])

                            topologicalSortUtil(g, nid, visited, stk);

std::cout << "topologicalSort" << std::endl;

 while (!stk.empty())

              {

                            std::cout << stk.top() << std::endl;

                            stk.pop();

              }

}

### Complexity

Time complexity is ![](images/00047.jpeg), space complexity is ![](images/00048.jpeg).

## 10  Detecting a bipartite graph

A bipartite graph is a graph, in which its vertices can be divided into two disjoint sets U and ![](images/00049.jpeg).

![](images/00050.jpeg) ![](images/00051.jpeg) ![](images/00052.jpeg) ![](images/00053.jpeg) ![](images/00053.jpeg) ![](images/00053.jpeg) ![](images/00054.jpeg)

![](images/00055.jpeg) ![](images/00056.jpeg) ![](images/00053.jpeg) ![](images/00053.jpeg)

![](images/00057.jpeg) ![](images/00058.jpeg) ![](images/00053.jpeg)

### ![](images/00059.jpeg)

### Solution

A DFS or a BFS visit can be performed by assigning colors to the graph in such a way that the children have opposite colors from their parents.  If two directly connected nodes have same color, the graph is not bipartite.

### Code

bool isBipartite(const  Graph & g, Graph::NodeID  sid)

{

 if (sid >= g.numNodes())                                         

 return  false;

              std::vector<Graph::NodeID> colour(g.numNodes(), -1);

              colour[sid] = 1;

              std::list<Graph::NodeID> queue;

              queue.push_back(sid);

 while (!queue.empty())

              {

 const  Graph::NodeID n = queue.front();

                            queue.pop_front();

std::cout << "Visited=" << n << std::endl;

 for (const  auto & e : g.edges(n))

                            {

 if (colour[e.v] == -1)

                                          {

                                                        colour[e.v] = 1 - colour[n];

                                                        queue.push_back(e.v);

                                          }

 else  if (colour[e.v] == colour[n])

 return  false;

                            }

              }

 return  true;

}

### Complexity

Time complexity is ![](images/00060.jpeg), space complexity is ![](images/00061.jpeg).

## 11  Given a connected graph, compute the minimum spanning tree (MST)

Let’s start with some definitions. An undirected graph is said to be connected, if every pair of vertices in the graph is connected. In particular, two vertices ![](images/00062.jpeg) and ![](images/00063.jpeg) are defined as connected, if the graph contains a [path](http://en.wikipedia.org/wiki/Path_(graph_theory)) from![](images/00064.jpeg) to ![](images/00065.jpeg). Given a connected graph, a spanning tree is a tree which connects all vertices together. If the graph has weights associated to the edges, then the minimum spanning tree is a spanning tree with minimal sum of the edges’ weight.

### Solution

One way to compute the MST is to adopt a classical greedy algorithm due to Prim[[1]](#part0000_split_036.html__ftn1). At the beginning the tree contains a single vertex, chosen arbitrarily from the graph. Then the minimum weight edge is selected among those connecting a vertex in the tree with a vertex not being in the tree. This edge is added to the tree and the previous step is repeated until all vertices are in the tree. In our implementation the edges are maintained ordered by using a priority queue realized with boost::fibonacci

### Code

struct  nodeComparison

{

 const  MatrixGraph::NodeID node;

 MatrixGraph::weight priority;

  nodeComparison(MatrixGraph::NodeID  name,

MatrixGraph::NodeID  p) : node(name), priority(p) {};

 bool operator < (nodeComparison  const & rhs) const

  {

 return priority > rhs.priority;

  }

};

void PrimMST(const  MatrixGraph & g, MatrixGraph::NodeID  startNode)

{

 typedef boost::heap::fibonacci_heap< nodeComparison > Heap;

 Heap heap;

  std::map <MatrixGraph::NodeID, Heap::handle_type> mapHandles;

// for decrease() key

 MatrixGraph::weight edgeWeight;

 MatrixGraph::NodeID numNodes = g.getNumNodes();

  std::vector<bool> isInHeap(numNodes, false);

  std::vector<MatrixGraph::NodeID> parent(numNodes + 1, 0);

 for (MatrixGraph::NodeID i = 0; i < numNodes; ++i)

  {

    mapHandles[i] =

heap.push(nodeComparison(i,

std::numeric_limits<MatrixGraph::weight>::max()));

isInHeap[i] = true;

  }

  (*(mapHandles[startNode])).priority = 0;

// initial node has priority 0

  heap.increase(mapHandles[startNode]);

 // fibonacci has increase ammortized constat

 // decrease is logaritmic -> inverted operator <

 while (!heap.empty()){

 const  nodeComparison nc = heap.top(); // extract top

    heap.pop();

isInHeap[nc.node] = false; // no longer in heap

std::cout << "node=" << nc.node << " w="

<< nc.priority << std::endl;

 for (MatrixGraph::NodeID v = 0; v < numNodes; ++v)

    {

 if ((edgeWeight = g(nc.node, v)) // an edge (nc.node, v)

&& (isInHeap[v]) // v is in Heap

        && (edgeWeight < (*(mapHandles[v])).priority))

// improving weight

      {

        (*(mapHandles[v])).priority = edgeWeight;

        heap.increase(mapHandles[v]);

        parent[v] = nc.node;

std::cout << "node=" << nc.node << "->"

<< v << " with w=" <<

          (*(mapHandles[v])).priority << std::endl;

      }

    }

  }

std::cout << "MST" << std::endl;

 for (MatrixGraph::NodeID i = 1; i < numNodes; ++i)

  {

std::cout << parent[i] << '-' << i <<

 " weight=" << g(parent[i], i) << std::endl;

  }

}

### \

This particular implementation uses an adjacency matrix and therefore its complexity is ![](images/00066.jpeg). However it is possible to get ![](images/00067.jpeg) by using adjacent lists and a Fibonacci heap in which a Find-minimum is![](images/00068.jpeg) amortized time[[2]](#part0000_split_036.html__ftn2)

| adjacency matrix for dense or sparse graph | ![](images/00069.jpeg) |
| binary heap and adjacency lists for sparse graph | ![](images/00070.jpeg)![](images/00071.jpeg) |
| binary heap and adjacency lists for dense graph | ![](images/00072.jpeg) |
| Fibonacci heap and adjacency list | ![](images/00073.jpeg) |

## 12  

Space complexity evaluation is here left as an exercise. An example of minimum spanning tree is in the picture below

![](images/00074.jpeg)

## 13  Find the strongly connected components in a direct graph

A direct graph ![](images/00075.jpeg) is said to be strongly connected, if every node is reachable from every other node. The strongly connected components of ![](images/00076.jpeg) create a partition into subgraph that are themselves strongly connected as in this figure.

![http://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Scc.png/220px-Scc.png](images/00077.jpeg)

### Solution

The here implemented solution is the Kosaraju’s algorithm[[3]](#part0000_split_036.html__ftn3) which uses two passes of DFS. The first pass is carried out on the original graph and it is used to choose the order in which the outer loop of the second DFS tests are connected to the vertices. The second DFS is on the transpose graph of the original graph. Each recursive exploration finds a single new strongly connected component.

### Code

// 

// Transpose

void transpose(const  Graph & g, Graph & gt)

{

 gt.reserveNodes(g.numNodes());

 gt.reserveEdges(g.numEdges());

 // add all nodes

 for (const  auto & n : g.nodes())

 gt.addNode(n.w, n.label);

 // add all edges

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 for (const  auto & e : g.edges(id))

 gt.addEdge(e.v, id, e.w, e.label);

}

//

// SCC

void fillOrder(const  Graph & g, Graph::NodeID  v,

              std::vector<bool> & visited,

              std::stack<Graph::NodeID> &stk)

{

 visited[v] = true;

 for (const  auto & e : g.edges(v))

 if (!visited[e.v])

                            fillOrder(g, e.v, visited, stk);

 stk.push(v);

}

void StrongConnectedComponents(const  Graph & g)

{

              std::stack<Graph::NodeID> stk;

              std::vector<bool> visited(g.numNodes(), false);

 unsigned componentID = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (visited[id] == false)

                            fillOrder(g, id, visited, stk);

 Graph gt;

              transpose(g, gt);

std::fill(visited.begin(), visited.end(), false);

 while (!stk.empty())

              {

 Graph::NodeID id = stk.top();

                            stk.pop();

 if (!visited[id])

                            {

                                          dfsUtil(g, id, visited);

std::cout << "end component id="

                                                        << componentID++ << std::endl;

                            }

              }

}

### Complexity

Time complexity is here ![](images/00078.jpeg)

## 14 Covering DFS Trees

Given a graph ![](images/00079.jpeg) it is possible to define a path tree ![](images/00080.jpeg) generated by a DFS visit. If G is not (strongly) connected then we need to restart the DFS from each node and the visit will generate a forest of trees, If the graph is direc,t the visit will respect the direction of the edges, while if the graph is not direct, the visit will produce a random orientation of each edge as a consequence of the direction of the visit. During the visit the edges not yet included in ![](images/00081.jpeg) can be divided into three categories:

*   If the edge is examined by passing from a node ![](images/00082.jpeg) in ![](images/00083.jpeg) to another node ![](images/00084.jpeg) in T, which is an ancestor of ![](images/00085.jpeg) in G, then the edge (u, v) is called  loop back edge
*   If the edge is examined by passing from a node ![](images/00086.jpeg) in ![](images/00087.jpeg) to another node ![](images/00088.jpeg) in T, which is a descendant of ![](images/00089.jpeg) in G, then the edge (u, v) is called  forward edge
*   Otherwise it is called cross edge

## 15  Find an Hamiltonian cycle

A Hamiltonian path[[4]](#part0000_split_036.html__ftn4) is a path through a[graph](http://mathworld.wolfram.com/Graph.html) that visits each node exactly once. If the path is also a cycle, then we have a Hamiltonian cycle as in the figure. The problem is NP-Complete so the worst case solution needs exponential time in the number of nodes.

![http://upload.wikimedia.org/wikipedia/commons/thumb/6/60/Hamiltonian_path.svg/220px-Hamiltonian_path.svg.png](images/00090.jpeg)

### Solution

Here we present a backtracking algorithm in C++

### Code

// hamiltonianCycle

bool isSafe(const  MatrixGraph& g,

 const  MatrixGraph::NodeID  v,

              std::vector<MatrixGraph::NodeID> & path,

 const  unsigned  int  pos)

{

 if (!g(path[pos - 1], v))

 return  false;

 for (MatrixGraph::NodeID i = 0; i < pos; ++i)

 if (path[i] == v)

 return  false;

 return  true;

}

bool hamiltonianCycleUtil(const  MatrixGraph & g,

              std::vector<MatrixGraph::NodeID> & path,

 const  unsigned  int  pos)

{

 if (pos == g.getNumNodes())

              {

 if (g(path[pos - 1], path[0]))

 return  true;

 else

 return  false;

              }

 for (MatrixGraph::NodeID v = 1; v < g.getNumNodes();                             ++v)

              {

 if (isSafe(g, v, path, pos))

                            {

 path[pos] = v; // insert v

 if (hamiltonianCycleUtil(g, path,

 pos + 1) == true)

 return  true;

 path[pos] = -1; // remove v

                            }

              }

 return  false;

}

bool hamiltonianCycle(const  MatrixGraph & g)

{

 MatrixGraph::NodeID V = g.getNumNodes();

              std::vector<MatrixGraph::NodeID>path(V, -1);

 bool returnValue;

              path[0] = 0;

 if ((returnValue = hamiltonianCycleUtil(g, path, 1)))

              {

std::cout << "Hamiltionian cycle " << std::endl;

 for (MatrixGraph::NodeID i = 0; i < V; ++i)

std::cout << path[i] << ' ';

                            std::cout << std::endl;

              }

 else {

std::cout << "No Hamiltionian cycle";

              }

 return returnValue;

}

## 16  Find the articulation points in a graph

An articulation point is any vertex, where its removal increases the number of connected components.

### Solution

The algorithm proposed is due to Hopcroft and Tarjan[[5]](#part0000_split_036.html__ftn5). The idea is to run a DFS while maintaining:

1.  the depth of each vertex in the DFS tree
2.  For each node ![](images/00091.jpeg), the lowest depth of neighbours of all descendants of ![](images/00092.jpeg) in the DFS tree, called the lowpoint. The lowpoint of ![](images/00093.jpeg) can be computed after visiting all descendants of ![](images/00094.jpeg) as the minimum of the depth of ![](images/00095.jpeg), the depth of all neighbors of ![](images/00096.jpeg) (excluding the parent of ![](images/00097.jpeg) in the DFS tree) and the lowpoint of all children of ![](images/00098.jpeg) in the DFS tree.

A non-root vertex ![](images/00099.jpeg) is an articulation point, if and only if there is a child ![](images/00100.jpeg) of ![](images/00101.jpeg)such that ![](images/00102.jpeg) This property can be tested, once the depth-first search is returned from every child of v.  The root vertex must be handled separately: it is an articulation point, if and only if it has at least two children.

### Code

//

// Articulation Points

void articulationUtil(const  Graph & g,

 const  Graph::NodeID  u,

 unsigned  int & time,

              std::vector<bool> & visited,

              std::vector<Graph::NodeID> & discovery,

              std::vector<Graph::NodeID> & lower,

              std::vector<Graph::NodeID> & parent,

              std::vector<bool> & articulationPoints)

{

 Graph::NodeID children = 0;

 visited[u] = true;

 discovery[u] = lower[u] = ++time;

 for (const  auto & e : g.edges(u))

              {

 if (!visited[e.v])

                            {

 parent[e.v] = u;

                                          children++;

                                          articulationUtil(g, e.v, time, visited,

 discovery, lower, parent,

 articulationPoints);

 lower[u] = std::min(lower[u], lower[e.v]);

 if (parent[u] ==

                                                        std::numeric_limits<Graph::NodeID>::max()

                                                        && children > 1)

 articulationPoints[u] = true;

 if (parent[u] ==

                                                        std::numeric_limits<Graph::NodeID>::max()

&& lower[e.v] >= discovery[u])

 articulationPoints[u] = true;

                            }

 else  if (e.v != parent[u])

 lower[u] = std::min(lower[u],

discovery[e.v]);

              }

}

void articulationPoints(const  Graph & g)

{

 unsigned  int time = 0;

              std::vector<bool> visited(g.numNodes(), false);

              std::vector<Graph::NodeID> discovery(g.numNodes(), 0);

              std::vector<Graph::NodeID> lower(g.numNodes(), 0);

              std::vector<Graph::NodeID> parent(g.numNodes(),

                            std::numeric_limits<Graph::NodeID>::max());

              std::vector<bool> articulationPoints(g.numNodes(),

 false);

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (!visited[id])

                            articulationUtil(g, id, time, visited, discovery,

                                          lower, parent, articulationPoints);

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (articulationPoints[id])

std::cout << "articulation point id=" <<

                            id << std::endl;

}

### Complexity

Time complexity is ![](images/00103.jpeg). An example of articulation point is in the picture below

![](images/00104.jpeg)

## 17  Find the shortest path in a graph with non-negative edge weight

### Solution

Given a graph with non-negative edge weight, we can apply Dijkstra’s algorithm for finding the single-source shortest path tree[[6]](#part0000_split_036.html__ftn6). Edger Dijkstra was born in the Netherlands and he invented the algorithm in 1959.  For a given source node ![](images/00105.jpeg), the algorithm looks for the path with lowest cost between ![](images/00106.jpeg) and every other node. This class of problems has multiple applications including optimization, routing and traffic assignment. The pseudo-code for Dijkstra is given below. The vector ![](images/00107.jpeg) contains the sum of weights for the path used to arrive to the node ![](images/00108.jpeg) (at the beginning this is infinite). The vector ![](images/00109.jpeg) contains the predecessor of ![](images/00110.jpeg) in the shortest path (at the beginning ![](images/00111.jpeg)). In addition a priority queue![](images/00112.jpeg) is used to select nodes ![](images/00113.jpeg) with the smallest ![](images/00114.jpeg)  (in the pseudo-code this is the operationu ← EXTRACT-MIN(Q))).Moreover, ![](images/00115.jpeg)]contains all the nodes ![](images/00116.jpeg) adjacent to ![](images/00117.jpeg). So for each ![](images/00118.jpeg) , if ![](images/00119.jpeg) - the sum of weights for the path leading to ![](images/00120.jpeg) - plus to the weight of the edge ![](images/00121.jpeg)is less than ![](images/00122.jpeg) - the sum of the weights for the path leading to ![](images/00123.jpeg) - then we have identified a shorter path. In this case, ![](images/00124.jpeg) and ![](images/00125.jpeg) are updated accordingly. Also the node v is added to Q, if it has never been visited before.  Instead, if it has been already visited, its priority in Q should be reduced according to the new weight (this is the operationDECREASE-KEY(Q, v)in the pseudo-code). At the end the vectors ![](images/00126.jpeg) and ![](images/00127.jpeg) are returned.

### Code

| DIJKSTRA(G, s, w) for each vertex u in V d[u] ← infinity p[u] ← u color[u] ← WHITE color[s] ←  GRAY d[s] ← 0  INSERT(Q, s) while (Q != Ø) u ← EXTRACT-MIN(Q) for each vertex v in Adj[u] if (w(u,v) + d[u] < d[v]) d[v] ← w(u,v) + d[u] p[v] ← u if (color[v] ==  WHITE) color[v] ←  GRAY          INSERT(Q, v) else if (color[v] == GRAY)          DECREASE-KEY(Q, v) color[u] ← BLACK  return (d, p) |  |

For this exercise[[7]](#part0000_split_036.html__ftn7) we start using boost::BGL a powerful framework for graph creation and processing[[8]](#part0000_split_036.html__ftn8). A graph can have weights and names labels associated to the edges and those are stored in a boost::property. In addition a graph can be represented either with a boost::adjacency_list or with a boost:adjacenty_matrix. The boost:adjacenty_list uses many parameters including OutEdgeList (the selector for the container used to represent the edge-list for each of the vertices), VertexList (the selector for the container used to represent the vertex-list of the graph), Directed (a selector to choose whether the graph is directed, undirected, or directed with bidirectional edge access), VertexProperties (for specifying internal property storage), EdgeProperties (for specifying internal property storage), GraphProperties (for specifying property storage for the graph object) , EdgeList (the selector for the container used to represent the edge-list for the graph). For instance, listS selects std::list and this is a good choice, if you need to add and remove vertices quickly. The adjacency_listclass implements boost::property_maps for accessing objects (properties) that are attached to the vertices and edges of the graph, and boost::iterator_property_map is  used to navigate inside the maps. All these features are used to represent multiple flavours of graphs with an uniform representation. Having this contest in mind, we can create a Graph  g and add vertices and edges with the appropriate boost method. The predecessorMap records the edges in the shortest path tree, the tree is computed by the graph traversal, while the shortest path weight from the source vertex  to each vertex in the graph g is recorded in the distanceMap. In this particular example we compute the shortest path starting from a specific source node v3 and we extract the shortest path by following the computed precedessorMap

#include  <boost/graph/adjacency_list.hpp>

#include  <boost/graph/dijkstra_shortest_paths.hpp>

#include  <boost/graph/graph_traits.hpp>

#include  <boost/graph/iteration_macros.hpp>

#include  <boost/graph/properties.hpp>

#include  <boost/property_map/property_map.hpp>

void boostDijkstra()

{

 typedef  float  Weight;

 // http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/property.html

 typedef boost::property<boost::edge_weight_t,

 Weight> WeightProperty;

 typedef boost::property<boost::vertex_name_t,

                            std::string> NameProperty;

 // http://www.boost.org/doc/libs/1_53_0/libs/graph/doc/adjacency_list.html

 typedef boost::adjacency_list < boost::listS,

                            boost::vecS, boost::directedS,

 NameProperty, WeightProperty > Graph;

 // http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/graph_traits.html

 typedef boost::graph_traits < Graph >::vertex_descriptor  Node;

 typedef boost::property_map < Graph,

                            boost::vertex_index_t >::type  IndexMap;

 typedef boost::property_map < Graph,

                            boost::vertex_name_t >::type  NameMap;

 // http://www.boost.org/doc/libs/1_37_0/libs/property_map/iterator_property_map.html

 typedef boost::iterator_property_map < Node*, IndexMap,

 Node, Node& > PredecessorMap;

 typedef boost::iterator_property_map < Weight*, IndexMap,

 Weight, Weight& > DistanceMap;

 Graph g;

 Node v0 = boost::add_vertex(std::string("v0"), g);

 Node v1 = boost::add_vertex(std::string("v1"), g);

 Node v2 = boost::add_vertex(std::string("v2"), g);

 Node v3 = boost::add_vertex(std::string("v3"), g);

              boost::add_edge(v0, v1, 15, g);

              boost::add_edge(v1, v3, 7, g);

              boost::add_edge(v0, v2, 2, g);

              boost::add_edge(v2, v3, 4, g);

              std::vector<Node> predecessors(boost::num_vertices(g));

              std::vector<Weight> distances(boost::num_vertices(g));

 IndexMap indexMap = boost::get(boost::vertex_index, g);

 PredecessorMap predecessorMap(&predecessors[0],

                            indexMap);

 DistanceMap distanceMap(&distances[0], indexMap);

              boost::dijkstra_shortest_paths(g, v0,

                            boost::distance_map(distanceMap).predecessor_map(predecessorMap));

std::cout << "distances and parents:" << std::endl;

 NameMap nameMap = boost::get(boost::vertex_name, g);

 BGL_FORALL_VERTICES(v, g, Graph)

              {

std::cout << "distance(" << nameMap[v0] << ", "

<< nameMap[v] << ") = " << distanceMap[v]

<< ", ";

std::cout << "predecessor(" << nameMap[v]

<< ") = "

                                          << nameMap[predecessorMap[v]] << std::endl;

              }

              std::cout << std::endl;

 typedef std::vector<Graph::edge_descriptor> PathType;

 PathType path;

 Node v = v3;

 for (Node u = predecessorMap[v];

                            u != v;

                            v = u, u = predecessorMap[v])

              {

                            std::pair<Graph::edge_descriptor, bool> edgePair =

                                          boost::edge(u, v, g);

 Graph::edge_descriptor edge = edgePair.first;

                            path.push_back(edge);

              }

 float totalDistance = 0;

 for (PathType::reverse_iterator pathIterator =

                            path.rbegin();

                            pathIterator != path.rend(); ++pathIterator)

              {

                            std::cout <<

nameMap[boost::source(*pathIterator, g)]

<< " -> " << nameMap[boost::target(*pathIterator, g)]

<< " = " <<

                                          boost::get(boost::edge_weight, g,

*pathIterator)

<< std::endl;

              }

std::cout << "Distance: "

<< distanceMap[v2] << std::endl;

}

A useful exercise is to use Dijkstra for computing the shortest path on the graph represented in picture.

![](images/00128.jpeg)

### Complexity

Time complexity is ![](images/00129.jpeg), if the priority queue is implemented using Fibonacci heaps. Fibonacci heap is a priority queue which implements extracting minimum efficiently. Note that Dijkstra’s original algorithm does not use a [min-priority queue](http://en.wikipedia.org/wiki/Min-priority_queue) and runs in [time](http://en.wikipedia.org/wiki/Time_complexity)![](images/00130.jpeg).

## 18  Find MST(Minimum Spanning Tree) using Kruskal Algorithm

Kruskal’s algorithm finds a minimum spanning tree (MST) in an undirected graph with weighted edges. The algorithm orders the edges for increasing weight and then every single edge is included in the solution, if it does not form a cycle with the edges already selected.

### Solution

The pseudo code uses UNION-FIND operations[[9]](#part0000_split_036.html__ftn9)  :

*   Find: Determine which subset a particular element is in. It is used for determining, if two elements are in the same subset.
*   Union: Join two subsets into a single subset.

KRUSKAL-MST(G, w)

 T ← Ø

 for each vertex u in V

    MAKE-SET(DS, u)

 for each edge (u,v) in E in order of nondecreasing weight

 if FIND-SET(DS, u) != FIND-SET(DS, v)

      UNION-SET(DS, u, v)

 T ← T U {(u,v)}

return  T

In boost[[10]](#part0000_split_036.html__ftn10), this is defined inboost/graph/kruskal_min_spanning_tree.hpp

As an exercise try to compute Kruskal on the following graph

![](images/00131.jpeg)

![](images/00132.jpeg) ![](images/00133.jpeg) ![](images/00134.jpeg) ![](images/00134.jpeg)

![](images/00135.jpeg) ![](images/00136.jpeg) ![](images/00137.jpeg) ![](images/00138.jpeg) ![](images/00139.jpeg)

![](images/00140.jpeg) ![](images/00141.jpeg)

![](images/00142.jpeg) ![](images/00143.jpeg) ![](images/00144.jpeg) ![](images/00144.jpeg)

### Complexity

Time complexity is ![](images/00145.jpeg) because we use union-find data structure to keep the set information,whereFind operations on![](images/00146.jpeg) elements require  ![](images/00147.jpeg)  time.

## 19  Find the longest path in a DAG

The problem of finding the longest path is NP-hard for a general graph. However if we have a DAG, we can easily compute the topological sort. Then for every node we update the distance of its adjacent nodes by using the distance of current vertex.

### Solution

This code uses the topological sort defined before and then adds weights starting from the source

### Code

void longestPathDAG(const  Graph & g,

 const  Graph::NodeID  id,

              std::vector<Graph::NodeID>& distance)

{

              std::stack<Graph::NodeID> stk;

 distance = std::vector<Graph::NodeID>(g.numNodes(),

                            std::numeric_limits<Graph::NodeID>::max());

              std::vector<bool> visited(g.numNodes(), false);

 distance[id] = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (!visited[id])

                            topologicalSortUtil(g, id, visited, stk);

 while (!stk.empty())

              {

 const  Graph::NodeID id = stk.top();

                            stk.pop();

 if (distance[id] !=

                                          std::numeric_limits<Graph::NodeID>::max())

                            {

 for (const  auto & e : g.edges(id))

 if (distance[e.v] > distance[id] + e.w)

 distance[e.v] = distance[id] + e.w;

                            }

              }

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (distance[id] ==

std::numeric_limits<Graph::NodeID>::max())

std::cout << "id=" << id <<

 " has infinity distance" << std::endl;

 else

std::cout << "id=" << id <<

 " has distance=" << distance[id] << std::endl;

}

### Complexity

Time complexity is ![](images/00148.jpeg). What is the space complexity?

## 20  Find MST (Minimum Spanning Tree) using Prim Algorithm

Prim’s[[11]](#part0000_split_036.html__ftn11) algorithm finds a minimum spanning tree (MST) in an undirected graph with weighted edges. Prim’s is a typical greedy algorithm which maintains two data structures ![](images/00149.jpeg) containing the predecessor of the node ![](images/00150.jpeg) and ![](images/00151.jpeg), containing the minimum distance from node![](images/00152.jpeg). At the beginning every node is marked as not visited and the distance is infinite. Then the source node ![](images/00153.jpeg) is inserted in a priority queue ![](images/00154.jpeg) ordered by distance![](images/00155.jpeg). Until the queue is not empty a node ![](images/00156.jpeg)is de-queued from ![](images/00157.jpeg) . For each node ![](images/00158.jpeg) adjacent to ![](images/00159.jpeg)the condition ![](images/00160.jpeg) is checked where ![](images/00161.jpeg) is the weight associated to the edge ![](images/00162.jpeg). The node v is inserted in Q, if the condition is met and the node was never visited before. Instead if priority is decreased, the condition is met but the node is already in ![](images/00163.jpeg).             

### Solution

The pseudo code is the following:

PRIM-MST(G, s, w)

 for each vertex u  in  V[G] 

 color[u] ←  WHITE; d[u] ←  infinity 

 color[s] ←  GRAY; d[s] ← 0

  ENQUEUE(Q, s); p[s] ← s

 while (Q != Ø)

 u := DEQUEUE(Q)

 for each v in Adj[u] 

 if (w(u,v) < d[v])

 d[v] ← w(u,v); p[v] ← u

 if (color[v] = WHITE)

          ENQUEUE(Q, v) ;color[v] ←  GRAY

 else if (color[v] = GRAY)

          DECREASE-KEY (Q, v)

 color[u] ←  BLACK

return (p, d)

In boost, this is defined in [boost/graph/prim_minimum_spanning_tree.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/prim_minimum_spanning_tree.hpp)

### Complexity

Time complexity is ![](images/00164.jpeg) where ![](images/00165.jpeg) is the time needed for extracting ![](images/00166.jpeg) nodes from ![](images/00167.jpeg) and ![](images/00168.jpeg) is the time needed for processing the adjacency list and update the queue. Note that if we use Fibonacci heap, then operations of insert and decreaseKey have cost ![](images/00169.jpeg) amortized by deleteKey with cost ![](images/00170.jpeg). So complexity is ![](images/00171.jpeg) by using Fibonacci

## 21  Find all pairs shortest paths using the Floyd-Warshall Algorithm

Floyd & Warshall’s algorithm finds the shortest distance between every pair of vertices in the graph. The algorithm detects, if there are loops with negative weights, which will produce a degenerate negative infinite shortest path otherwise.

### Solution

The pseudo-code is

let dist be a |V| × |V| array of min distances initialized to ∞

 for each vertex v

     dist[v][v] ← 0

 for each edge (u,v)

     dist[u][v] ← w(u,v)  // the weight for edge (u, v)

 for k from 1 to |V|

 for i from 1 to |V|

 for j from 1 to |V|

           if dist[i][j] > dist[i][k] + dist[k][j]

              dist[i][j] ← dist[i][k] + dist[k][j]

This pseudo-code computes the weight of each shortest path between all pair of nodes ![](images/00172.jpeg) in the graph. However, it does not memorize the minimum paths. These can be stored with some changes in the code which are here left for exercise.

Now let’s consider a negative cycle which is a cycle whose edges sum to a negative value. There is no shortest path between any pair of nodes ![](images/00173.jpeg) which form a part of a negative cycle, because path-lengths from ![](images/00174.jpeg) to![](images/00175.jpeg) can be arbitrarily small. As an exercise we ask to modify the pseudo-code for detecting negative cycles.

In boost this is defined in  [boost/graph/floyd_warshall_shortest.hpp](http://www.boost.org/doc/libs/1_41_0/boost/graph/floyd_warshall_shortest.hpp)

### Complexity

Time complexity is ![](images/00176.jpeg), while space complexity is ![](images/00177.jpeg)

## 22  Find all the single source shortest paths using Bellman Ford Algorithm

The Bellman-Ford algorithm finds the single-source shortest paths problem for a graph with both positive and negative edge weights. Dijkstra’s algorithm is more efficient for a graph with only positive edge weights. Bellman Ford is the code of the old RIP[[12]](#part0000_split_036.html__ftn12) (Routing Internet Protocol). Bellman-Ford is very similar to Dijkstra but it processes all the edges instead of selecting the node with minimum weight among those that still have to be processed (greedy choice). This computation is repeated for all the nodes.

### Solution

The pseudo-code is the following:

BELLMAN-FORD(G)

 for each vertex u in V

 d[u] ← infinity; p[u] ← u

 for  i ← 1  to  |V|-1

 for each edge (u,v) in E

 if (w(u,v) + d[u] < d[v])

 d[v] ← w(u,v) + d[u];

 p[v] ← u

 for each edge (u,v) in E

 if (w(u,v) + d[u] < d[v])

 return (false, , )

 return (true, p, d)

In boost this is defined in [boost/graph/bellman_ford_shortest_paths.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/bellman_ford_shortest_paths.hpp)

### Complexity

Time complexity is ![](images/00178.jpeg)

## 23 Independent set of intervals

Given a set of n intervals in the real line, a maximum independent set is a subset X of intervals with maximum size such that any pair of intervals in X has empty intersection.

### Solution

Without losing in generality, let us assume that the intervals ![](images/00179.jpeg) have 2 distinct bounds. Let us add to additional intervals ![](images/00180.jpeg) and ![](images/00181.jpeg) such that ![](images/00182.jpeg) and ![](images/00183.jpeg) for ![](images/00184.jpeg). We can build an acyclic graph ![](images/00185.jpeg) with ![](images/00186.jpeg) nodes corresponding to the![](images/00187.jpeg) intervals such that there is an edge ![](images/00188.jpeg), if and only if ![](images/00189.jpeg). Then we assign the weight ![](images/00190.jpeg)  to each edge![](images/00191.jpeg). It can be verified that the shortest path on ![](images/00192.jpeg) defines the independent set of intervals.

### Complexity

G is a DAG and can be built in ![](images/00193.jpeg) and therefore the shortest path can be computed in ![](images/00194.jpeg).

## 24 Dominant set of intervals

Given a set of n intervals in the real line, a dominant set is a subset X of intervals with minimum size, such that any interval which is not in X has non-empty intersection with the intervals in X.

### Solution

Let us make the same assumptions of the previous exercise: we will construct a new graph ![](images/00195.jpeg). For each interval ![](images/00196.jpeg) with ![](images/00197.jpeg) define ![](images/00198.jpeg) and ![](images/00199.jpeg) h: ![](images/00200.jpeg)} and introduce and edge ![](images/00201.jpeg). if and only if ![](images/00202.jpeg). Then we assign the weight![](images/00203.jpeg). It can be verified that the shortest path on ![](images/00204.jpeg) defines a dominant set of intervals.

### Complexity

G is a DAG and can be built in ![](images/00205.jpeg) and therefore the shortest path can be computed in ![](images/00206.jpeg).

## 25  Weighted dominant set of intervals

Given a set of n intervals in the real line where each interval has an associated weight integer and a non-negative. Find a dominant set with minimum weight.

### Solution

Left as an exercise

## 26  Weighted shortest paths with cost associated to the nodes

Suppose that the cost is associated to the nodes instead that to  the edges and that therefore the cost of a path is the sum of all the nodes it contains. According to this assumption compute the all pair shortest path.

### Solution

A solution can be easily computed associating to each ![](images/00207.jpeg) the new weight ![](images/00208.jpeg). However, all the paths should increase the weight by a constant w(root), because the root is not crossed by any edge

## 27  Find the flow network using Ford–Fulkerson’Algorithm

A flow network (also known as a transportation network) is a directed graph, where each edge ![](images/00209.jpeg) has a capacity ![](images/00210.jpeg)and receives a flow ![](images/00211.jpeg) that cannot exceed![](images/00212.jpeg).  The amount of flow into a node must be equal to the amount of flow out of it. However, a source has a more outgoing flow and a sink has a more incoming flow. A network can be used to model traffic information, currents in an electrical circuit and similar problems.

### Solution

The pseudo-code is the following:

Givena Network ![](images/00213.jpeg) withflow capacity ![](images/00214.jpeg), a source node ![](images/00215.jpeg), and a sink node ![](images/00216.jpeg)compute a flow f from  ![](images/00217.jpeg) to ![](images/00218.jpeg) of maximum value

1.  ![](images/00219.jpeg) ← 0 for all edges![](images/00220.jpeg)
2.  While there is a path ![](images/00221.jpeg) from ![](images/00222.jpeg) to ![](images/00223.jpeg) in G![](images/00224.jpeg), such that ![](images/00225.jpeg) for all edges ![](images/00226.jpeg) :
    1.  Find ![](images/00227.jpeg)
    2.  For each edge ![](images/00228.jpeg)
        1.  ![](images/00229.jpeg) + ![](images/00230.jpeg)
        2.  ![](images/00231.jpeg) - ![](images/00232.jpeg)

where ![](images/00233.jpeg)  is the residual graph when ![](images/00234.jpeg)flow is sent over the network where the capacity ![](images/00235.jpeg) and there is no flow

The algorithm is defined in [boost/graph/edmonds_karp_max_flow.hpp](http://www.boost.org/doc/libs/1_55_0/boost/graph/edmonds_karp_max_flow.hpp)

### Complexity

It can be proven that Ford-Fulkerson[[13]](#part0000_split_036.html__ftn13) has time complexity is ![](images/00236.jpeg) where f is the maximum flow in the graph. A variant of Ford-Fulkerson known as Edmon-Karp[[14]](#part0000_split_036.html__ftn14) has proven complexity![](images/00237.jpeg) 

## 28  Assignment matching problem

The assignment matching problem consists in finding a maximum weight matching for a given weighted bipartite graph.

Assume that we have ![](images/00238.jpeg) workers and ![](images/00239.jpeg) tasks to be completed. For each pair (worker, task) we know the costs that should be paid per worker to conclude the task. The goal is to conclude all the tasks and to minimize the total cost, under the condition that each worker can execute only one task and vice versa.

### Solution

Let ![](images/00240.jpeg) the cost matrix for the worker ![](images/00241.jpeg) to conclude the task ![](images/00242.jpeg) and let ![](images/00243.jpeg) the assignment matrix when the worker ![](images/00244.jpeg) has assigned the task![](images/00245.jpeg). Clearly, ![](images/00246.jpeg) and ![](images/00247.jpeg) and we want to minimize the total cost function![](images/00248.jpeg).  Note that the costs-matrix can be represented as a complete bipartite graph as in the following example:

![](images/00249.jpeg)

Given this representation, the problem can be solved as a special instance of min cost flow and the solution is left as an exercise.

## 29  Find an Eulerian circuit

An Eulerian path[[15]](#part0000_split_036.html__ftn15) is a visit in a graph which touches every[edge](http://en.wikipedia.org/wiki/Edge_(graph_theory)) exactly once. If such a walk exists, the graph is said semi-eulerian or traversable. An Eulerian circuit is an Eulerian visit which starts and ends on the same [vertex](http://en.wikipedia.org/wiki/Vertex_(graph_theory)). These problems were first discussed by Leonhard Euler for solving the famous problem of Seven Bridges of Konigsberg[[16]](#part0000_split_036.html__ftn16) .

![Thumbnail for version as of 17:12, 27 July 2006](images/00250.jpeg)

The city of [Königsberg](http://en.wikipedia.org/wiki/K%C3%B6nigsberg) in [Prussia](http://en.wikipedia.org/wiki/Kingdom_of_Prussia) was built on both sides of the[Pregel river](http://en.wikipedia.org/wiki/Pregolya), and had two large islands which were connected to each other and the mainland by seven bridges The problem was to find a walk through the city that would cross each bridge once and only once. Euler proved that the problem has no solution and this problem is considering the first one introducing a new discipline called graph theory, the subject of this book.

### Solution

At first glance the problem seems similar to the Hamiltonian path. However it is not. Indeed a solution can be computed in linear time.

We notice that a graph has Eulerian cycle if: (a) All vertices with non-zero degree are connected b) All vertices have even degree. In addition, a graph follows the Eulerian Path, if following two conditions hold: (a) All vertices with non-zero degree are connected, (b) If zero or two vertices have odd degree and all other vertices have even degree. The proof of these properties is left as an exercise.

### Code

bool isConnected(const  Graph & g)

{

              std::vector<bool> visited(g.numNodes(), false);

              std::vector<Graph::NodeID> color(g.numNodes(), false);

              std::vector<Graph::NodeID> timing(g.numNodes(), 0);

 Graph::NodeID id;

 for (id = 0; id < g.numNodes(); ++id)

 if (g.outdegree(id))

 break;

 if (id == g.numNodes())

 return  true;

              dfsUtil(g, id, visited);

 for (id = 0; id < g.numNodes(); ++id)

 if (visited[id] == false && g.outdegree(id))

 return  false;

 return  true;

}

enum  euler { notEulerian, SemiEulerian, Eulerian };

//

// Eulerian

euler isEulerian(const  Graph & g)

{

 if (isConnected(g) == false)

 return  notEulerian;

 unsigned  int odd = 0;

 for (Graph::NodeID id = 0; id < g.numNodes(); ++id)

 if (g.outdegree(id) & 1)

                            odd++;

 if (odd > 2)

 return  notEulerian;

 return (odd) ? SemiEulerian : Eulerian;

}

### Complexity

Time complexity is ![](images/00251.jpeg)

## 30  Scheduling

Given ![](images/00252.jpeg) programs ![](images/00253.jpeg) which require ![](images/00254.jpeg) time for being executed and an acyclic relation of dependency such that ![](images/00255.jpeg), if program ![](images/00256.jpeg) must be executed before![](images/00257.jpeg) find an algorithm which minimizes the total execution time and respects the dependency relation

### Solution

We can define a DAG ![](images/00258.jpeg) with ![](images/00259.jpeg) nodes and ![](images/00260.jpeg) if and only if![](images/00261.jpeg). If we compute the topological sort of ![](images/00262.jpeg), the sorted sequence of nodes is the solution. Each node can start just after the moment given by the sum of all the preceding nodes in the sorted order

### Complexity

Complexity is ![](images/00263.jpeg) , where ![](images/00264.jpeg) and ![](images/00265.jpeg)

ABOUT THE AUTHOR

An experienced data mining engineer, passionate about technology and innovation in consumers’ space. Interested in search and machine learning on massive dataset with a particular focus on query analysis, suggestions, entities, personalization, freshness and universal ranking. Antonio Gullì has worked in small startups, medium (Ask.com, Tiscali) and large corporations (Microsoft, Elsevier). His carrier path is about mixing industry with academic experience.

“Nowadays, you must have a great combination of research skills and a just-get-it-done attitude.”

* * *

[[1]](#part0000_split_015.html__ftnref1)  [http://en.wikipedia.org/wiki/Prim%27s_algorithm](http://en.wikipedia.org/wiki/Prim%27s_algorithm)

[[2]](#part0000_split_015.html__ftnref2) http://en.wikipedia.org/wiki/Fibonacci_heap

[[3]](#part0000_split_017.html__ftnref3)  [http://en.wikipedia.org/wiki/Kosaraju%27s_algorithm](http://en.wikipedia.org/wiki/Kosaraju%27s_algorithm)

[[4]](#part0000_split_019.html__ftnref4)  [http://en.wikipedia.org/wiki/Hamiltonian_cycle](http://en.wikipedia.org/wiki/Hamiltonian_cycle)

[[5]](#part0000_split_020.html__ftnref5)  [http://en.wikipedia.org/wiki/Biconnected_component](http://en.wikipedia.org/wiki/Biconnected_component)

[[6]](#part0000_split_021.html__ftnref6)  [http://en.wikipedia.org/wiki/Dijkstra's_algorithm](http://en.wikipedia.org/wiki/Dijkstra's_algorithm)

[[7]](#part0000_split_022.html__ftnref7)  [http://programmingexamples.net/wiki/Boost/BGL/DijkstraComputePath](http://programmingexamples.net/wiki/Boost/BGL/DijkstraComputePath)

[[8]](#part0000_split_022.html__ftnref8)  [http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/index.html](http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/index.html)

[[9]](#part0000_split_023.html__ftnref9)  [http://en.wikipedia.org/wiki/Disjoint-set_data_structure](http://en.wikipedia.org/wiki/Disjoint-set_data_structure)

[[10]](#part0000_split_023.html__ftnref10)  [http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/kruskal_min_spanning_tree.html](http://www.boost.org/doc/libs/1_55_0/libs/graph/doc/kruskal_min_spanning_tree.html)

[[11]](#part0000_split_025.html__ftnref11)  [http://en.wikipedia.org/wiki/Prim%27s_algorithm](http://en.wikipedia.org/wiki/Prim%27s_algorithm)

[[12]](#part0000_split_027.html__ftnref12)  [http://en.wikipedia.org/wiki/Routing_Information_Protocol](http://en.wikipedia.org/wiki/Routing_Information_Protocol)

[[13]](#part0000_split_032.html__ftnref13)  [http://en.wikipedia.org/wiki/Ford%E2%80%93Fulkerson_algorithm](http://en.wikipedia.org/wiki/Ford%E2%80%93Fulkerson_algorithm)

[[14]](#part0000_split_032.html__ftnref14)  [http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm](http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm)

[[15]](#part0000_split_034.html__ftnref15)  [http://en.wikipedia.org/wiki/Eulerian_path](http://en.wikipedia.org/wiki/Eulerian_path)

[[16]](#part0000_split_034.html__ftnref16)  [http://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg](http://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg)