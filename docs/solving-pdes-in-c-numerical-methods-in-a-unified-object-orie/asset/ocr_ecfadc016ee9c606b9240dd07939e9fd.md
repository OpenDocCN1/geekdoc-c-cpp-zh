![](bbox=[0.286, 0.101, 0.711, 0.287])

**Figure 3.5.** *Schematic representation of a binary tree with three levels. The arrows represent pointers, and the bullets represent constructed objects. The circles at the lowest level stand for the null (zero) pointer.*

Furthermore, binary trees lack the natural order of items available in linked lists. Although one can order the items recursively (e.g., left, middle, right), this order can be much more complicated than the natural order in linked lists.

One can also define more general trees by replacing the "left" and "right" pointers by a pointer to a linked list of trees:

```
template<class T> class tree{
protected:
    T item;
    linkedlist<tree<T> >* branch;
public:

    ...

};
```

This tree may contain any number of subtrees in a linked list. This linked list is pointed at by the private member "branch". Note that the '>' symbols in the definition of "branch" are separated by a blank space to distinguish them from the string ">>", which has a completely different meaning in the "iostream.h" standard library.

In the above data structure, it is particularly easy to remove existing subtrees and add new ones. Two-sided trees can also be derived by adding a pointer field named "parent" to contain the address of the parent tree.

# 3.13 Graphs

In the above trees, an item can point only to new items; it cannot point to parent or ancestor trees or even sibling subtrees. Thus, a tree cannot contain circles.

In a graph, on the other hand, an item can point not only to new items but also to existing ones; they can be ancestors, siblings, or even itself.

In fact, the mathematical definition of a graph is a set of nodes numbered 1, 2, 3, ..., N and a set of edges (pairs of nodes). The set of edges is commonly denoted by E.