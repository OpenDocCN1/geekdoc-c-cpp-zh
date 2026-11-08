A solution of the Königsberg bridge problem is given in the book *Discrete Mathematics: Theory and Applications (Revised Edition)* listed in Appendix H.

Over the past 200 years, graph theory has been applied to a variety of applications. Graphs are used to model electrical circuits, chemical compounds, highway maps, and so on. They are also used in the analysis of electrical circuits, finding the shortest route, project planning, linguistics, genetics, social science, and so forth. In this chapter, you will learn about graphs and their applications in computer science.

# Graph Definitions and Notations

To facilitate and simplify our discussion, we borrow a few definitions and terminology from set theory. Let $X$ be a set. If $x$ is an element of $X$, then we write $x \in X$. (The symbol “$\in$” means “belongs to”.) A set $Y$ is called a **subset** of $X$ if every element of $Y$ is also an element of $X$. If $Y$ is a subset of $X$, we write $Y \subseteq X$. (The symbol “$\subseteq$” means “is a subset of”.) The intersection of sets $A$ and $B$, written $A \cap B$, is the set of all of the elements that are in $A$ and $B$; that is, $A \cap B = \{x \mid x \in A \text{ and } x \in B\}$. (The symbol “$\cap$” means “intersection”.) The union of sets $A$ and $B$, written $A \cup B$, is the set of all of the elements that are in $A$ or in $B$; that is, $A \cup B = \{x \mid x \in A \text{ or } x \in B\}$. (The symbol “$\cup$” means “union”. Notice that $x \in A \cup B$ means $x$ is in $A$ or $x$ is in $B$ or $x$ is in both $A$ and $B$. Also, the symbol “$\mid$” is read as “such that”.)

For sets $A$ and $B$, the set $A \times B$ is the set of all of the ordered pairs of elements of $A$ and $B$; that is, $A \times B = \{(a,b) \mid a \in A, b \in B\}$.

A **graph** $G$ is a pair, $G = (V, E)$, in which $V$ is a finite nonempty set, called the set of **vertices** of $G$, and $E \subseteq V \times V$. That is, the elements of $E$ are the pair of elements of $V$. $E$ is called the set of **edges**.

Let $\Gamma(G)$ denote the set of vertices and $E(G)$ denote the set of edges of a graph $G$. If the elements of $E(G)$ are ordered pairs, $G$ is called a **directed graph** or digraph; otherwise, $G$ is called an **undirected graph**. In an undirected graph, the pairs $(u,v)$ and $(v,u)$ represent the same edge. If $(u,v)$ is an edge in a directed graph, then sometimes the vertex $u$ is called the **origin** of the edge, and the vertex $v$ is called the **destination**.

Let $G$ be a graph. A graph $H$ is called a **subgraph** of $G$ if $V(H) \subseteq V(G)$ and $E(H) \subseteq E(G)$; that is, every vertex of $H$ is a vertex of $G$, and every edge in $H$ is an edge in $G$.

To learn more about sets and graph terminology, the interested reader is referred to the book *Discrete Mathematics: Theory and Applications (Revised Edition)*, listed in Appendix H.