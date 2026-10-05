208

Chap. 6 Non-Binary Trees

```
// General tree representation for UNION/FIND
class ParTrTree (
private:
int* array; // Node array
int size; // Size of node array
int FIND(int) const; // Find root
public:
ParTrTree(); // Constructor
ParTrTree() { delete array; } // Destructor
void UNION(int, int); // Merge equivalences
bool diff(int, int); // True if not in same tree
};
```

```
int ParTrTree(int curr) const { // Find root
while (array[curr]) curr = array[curr];
return curr; // At root
}
```

**Figure 6.4** General tree implementation using parent pointers for the UNION/FIND algorithm.

is two new methods, **differ** and UNION. Method **differ** checks if two objects are in different sets, and method UNION merges two sets together. Private method **FIND** is used to find the ultimate root for an object.

An application using the UNION/FIND operations should store a set of n objects, where each object is assigned a unique index in the range 0 to $n-1$. The index refers to the connecting parent pointers in the array. Class ParTrTree creates and initializes the UNION/FIND array, and methods **differ** and UNION take array as inputs.

Figure 6.5 illustrates the pointer implementation. Note that the nodes can appear in any order within the array, and the array can store up to n separate trees. For example, Figure 6.5 shows two trees stored in the same array. This single array can store a collection of items distributed among any arbitrary (and changing) of disjoint subsets.

Consider the problem of assigning members of a set to disjoint subsets called **equivalence classes**. Recall from Section 2.1 that an equivalence relation is reflexive, symmetric, and transitive. Thus, if objects $A$ and $B$ are equivalent, and objects $B$ and $C$ are equivalent, we must be able to recognize that objects $A$ and $C$ are also equivalent.

There are many practical uses for disjoint sets and representing equivalences. For example, Figure 6.6 shows a graph of nodes labeled $A$ through $J$, there is some series of edges that connect any pair of nodes, but node $J$ is disconnected from the rest of the nodes. Such a graph might be used to represent connections as wires between components on a circuit board, or as roads between cities. We can consider two nodes of the graph to be equivalent if there is a path between them. Thus,