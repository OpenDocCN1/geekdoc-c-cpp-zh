# Chapter 5

# Graphs

# 5.1  Reliable distribution

# Problem

A communication network consists of a set $V$ of nodes and a set $E \subset V \times V$ of directed edges (communication links). Each edge $e \in E$ has a weight $w(e) \geq 0$ representing the cost of using $e$. A distribution from a given source $s \in V$ is a set of directed $|V|-1$ paths from $s$ to each of the other $|V|-1$ vertices in $V-\{s\}$. The cost of a distribution is the sum of the weights of its constituent paths. (Thus, some edges may be counted more than once in the cost of the distribution.)

+   1. Give an efficient algorithm to determine the cheapest distribution from a given source $s \in V$. You may assume all nodes $V$ are reachable from $s$.
+   
+   2. One of the edges in the communication network may fail, but we don't know which one. Give an efficient algorithm to determine the maximum amount by which the cost of the cheapest distribution from $s$ might increase if an adversary removes an edge from $E$. (The cost is infinite if the adversary can make a vertex unreachable from $s$.)

# Solution

+   1. This problem can be modeled as a single-source shortest paths problem. A distribution is a tree of paths from $s$ to every other vertex in the graph. Since the cost of a distribution is the sum of the lengths of its paths, a minimum cost distribution is a set of shortest paths. Since the edge weights are non-negative, we can use Dijkstra's algorithm. The running time of Dijkstra's algorithm can be improved from $O(|V|^2)$ to $O((|V|+|E|)\log |V|)$ using a binary heap.