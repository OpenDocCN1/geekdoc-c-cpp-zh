
the reader to specialized textbooks for other types of inserting operations.

The use of the functions is illustrated by the following piece of code, which exactly creates the list (4, 7, 5, 6) by inserting the elements in reverse order all at the beginning of the list, one after the other.

```c
1    elem_t *list, *elem;
2
3    list = NULL;
4    elem = create_element(6);
5    list = insert_element(list, elem, NULL);
6    elem = create_element(5);
7    list = insert_element(list, elem, NULL);
8    elem = create_element(7);
9    list = insert_element(list, elem, NULL);
10   elem = create_element(4);
11   list = insert_element(list, elem, NULL);
```

Once a list is created, one would like to do something with it. For example one could just print all members in the given order from the first to the last element. This is performed by the function print_list(), which receives a pointer list to the first element and returns nothing.

```c
1    void print_list(elem_t *list)
2    {
3        while(list != NULL)               /* run through list */
4        {
5            printf("%d ", list->info);
6            list = list->next;
7        }
8        printf("\n");
9    }
```

The function just prints the list to stdout. The functions illustrated nicely the main operation for lists, the iteration over all members of the list. This works (lines 3-7) by starting at the beginning of the list, and moving the pointer along the list by iteratively assigning it to its successor (line 6). Note that the pointer list is passed by value, hence its value outside the function print_list() remains unaffected by changing list inside the function.

Finally, we address the removal of an element from the list. This is illustrated in Fig. 6.10. We assume that the pointer elem to the element to be removed is given, as well as a pointer list to the first element of the list. Now we face the difficulty that we have to know the predecessor of the with pointers. Everyone who wants to be an expert simulation program developer should have implemented a rudimentary lists type at least once.

## 6.7 Trees

Now, we present trees, which are probably the most important advanced data structure for computer programming, in particular for many types of simulations. They help in many cases to replace operations which take time O(N) for a simulation of "size" N by operations which only take time O(log N). Hence, trees and other data structures which are derived from trees help a great deal in speeding up simulations, thereby allowing for larger systems to be treated.

For the data structures presented in the previous section, arrays and lists, always a linear order was used or assumed. Very often, additionally a hierarchical order is present or can be imposed. A very simple example of a system exhibiting a hierarchy is a company or a governmental organization. To consider a toy example, let us assume that a railway company consists of a planning division, an accounting division and a division operating the transportations. The planning division may be subdivided into a department for planning the network, another one for planning the schedules, a third for developing new pricing schemes, and a fourth responsible for buying new locomotives and wagons. The account division may be subdivided into four departments responsible for personal, maintenance, purchasing, and revenue, respectively. The operation division might be subdivided into departments for the freight trains, for passenger trains, for night trains, for busses, and one for actually performing the maintenance. The natural way to represent the structure of the railway company in the computer is a tree, as shown in Fig. 6.11.

Now we introduce some definitions. The elements of the tree are denoted as nodes or as vertices, the latter one is more generally used for graphs, see Sec. 6.8. For the railway company, e.g. "railway company", "accounting" and "night trains" are nodes. When two nodes A,B are connected by an arrow A→B, usually called a link or an edge, node A is called predecessor or parent of B, while B is called successor or child of A. In Fig. 6.11, "personal" is a child of "accounting". The children of a node A are also defined as descendents of A. Furthermore, all children of descendents of A are also defined as descendents of A. The single node without parent is called the root of the tree. Hence, all nodes, where A is located on a path from the root

to the node, are descendents of A. In the example tree, “railway company” is the root of the tree. On the other hand, each node A together with all its descendants also forms a tree, called a *subtree*, with A being the root of the subtree. Nodes without children are called *leaves*, e.g. “network” and “busses”. In principle, the number of children per node, also for the non-leaves, may vary within the tree. In case each node has at most two children, the tree is called a *binary tree*. To reach a node A, one can always start at the root of a tree and follow some links in the direction of the arrow, until the node A is reached. The sequence of visited nodes is called a *path*.<sup>5</sup> For example, “schedule” can be reached via the path “railway company” → “planning” → “schedule”. Note that for each node, the path to reach it from the root is unique. The number of traversed links between the root and node A is called the *height* or *level* of node A. Hence, the root has always height zero. In the example tree Fig. 6.11, node “planning” has height one, while node “prices” has height two. For this example, all leaves have the same height. In general, the leaves of a tree can have different heights, for example, if the railway company has a division “public relations” which is not subdivided into departments. Finally, the *height of the tree* itself is the largest height of any leaf.

<sup>5</sup> Equivalently, one can also call the sequence of traversed links a path.

As a very simple example of useful and general-purpose data structures, we consider binary search trees, where we want to store a set S of elements e, which can be ordered according to some value of a key k(e), like in Sec. 6.3, where the mergesort algorithm was presented. For simplicity, we assume that for each possible value of the key at most one element is present. Here, it is desirable to be able to test very quickly whether an element with a certain value of the key is present in the data structure. Also, we assume that constantly elements may be added or removed while the elements should preserved sorted. It would be too slow to sort the data again after each change. Thus, we cannot use the mergesort algorithm, since it results only in a fixed linear order of the sorted elements. The basic idea for overcoming this restriction is that one can introduce an artificial hierarchy by picking any value k0 of the key and subdividing the set of elements into elements which exhibit a smaller key k(e) < k0 (denoted as subset S(−∞, k0)), another subset containing elements exhibiting k(e) > k0 S(k0, ∞)) and possibly one remaining element with k(e) = k0. The subsets S(−∞, k0) and S(k0, ∞) can be subdivided in the same way. For example, using a key value k1,0 < k0, S(−∞, k0) can be subdivided into a subset S(−∞, k1,0) containing elements smaller than k1,0, into a subset S(k1,0, k0) containing elements between k1,0 and k0, and finally possibly the element with exactly the key value k1,0. In the same way, the other subset S(k0, ∞) can be subdivided using a key k2,0 > k0. By this hierarchical splitting of the set of elements a tree structure is generated. A binary tree can be used to store the elements via representing this hierarchy. In this case, for convenience, only the key values of existing elements are used for the hierarchical subdivision of the set. Hence, at each node an element e is stored. For this node, one subtree (usually denoted as left subtree) contains all elements e′ with key values k(e′) < k(e) the other (right) subtree the elements exhibiting k(e′) > k(e). A possible binary search tree containing elements with key values 13, 15, 20, 23, 24, 25, 27 is shown in Fig. 6.12.

A very natural way to represent trees in memory is to use a C structure for each element and pointers to represent the links. This is similar to the way we have represented lists in Sec. 6.6. The only difference is, since we are dealing with binary trees where each node has up to two children, that we store two pointers for each element. For leaves, both pointers have the value NULL. The following data structure can be used:

| GET SOURCE CODE |
|---|
| DIR: algorithms |
| FILE(S): tree.h |

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_198_0.png)

Fig. 6.11 Example of a hierarchical structure, represented as a tree: a railway company. Note that a tree is often drawn with the root node (here “railway company”) not located at the bottom.
