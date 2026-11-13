
## Example 12.5 Unite the binomial heaps given below.

## Solution

![](img/be6359df08208122bec6fad1103de211_382_0.png)

Figure 12.19(a)

After Merge-Binomial-Heap(), the resultant heap can be given as follows:

![](img/be6359df08208122bec6fad1103de211_382_1.png)

Figure 12.19(b)

Link next to PTR, making PTR the parent of the node pointed by NEXT.

![](img/be6359df08208122bec6fad1103de211_382_2.png)

Figure 12.19(c)

Now PTR is the first of the three roots of equal degree, that is, degree[PTR] = degree[NEXT] = degree[sibling[NEXT]]. Therefore, move the pointers one position further down the list by writing PREV = PTR, PTR = NEXT, and NEXT = sibling[PTR].

![](img/be6359df08208122bec6fad1103de211_382_3.png)

Figure 12.19(d)

Link PTR to NEXT, making NEXT the parent of the node pointed by PTR.

![](img/be6359df08208122bec6fad1103de211_383_0.png)

Figure 12.19(e)

Link NEXT to PTR, making PTR the parent of the node pointed by NEXT.

![](img/be6359df08208122bec6fad1103de211_383_1.png)

Figure 12.19(f) Binomial heap

```
Insert_Binomial-Heap(H, x)
Step 1: SET H' = Create_Binomial-Heap()
Step 2: SET Parent[x] = NULL, Child[x] = NULL and Sibling[x] = NULL, Degree[x] = NULL
Step 3: SET Head[H'] = x
Step 4: SET Head[H] = Union_Binomial-Heap(H, H')
Step 5: END
```

Figure 12.20 Algorithm to insert a new element in a binomial heap

```
Min-Extract_Binomial_Heap (H)
Step 1: Find the root R having minimum value in the root list of H
Step 2: Remove R from the root list of H
Step 3: SET H' = Create_Binomial-Heap()
Step 4: Reverse the order of R's children thereby forming a linked list
Step 5: Set head[H'] to point to the head of the resulting list
Step 6: SET H = Union_Binomial-Heap(H, H')
```

Figure 12.21 Algorithm to extract the node with minimum key from a binomial heap

## Inserting a New Node

The Insert_Binomial-Heap() procedure is used to insert a node x into the binomial heap H. The pre-condition of this procedure is that x has already been allocated space and val[x] has already been filled in.

The algorithm shown in Fig. 12.20 simply makes a binomial heap h' in O(1) time. H' contains just one node which is x. Finally, the algorithm unites H' with the n-node binomial heap H in O(log n) time. Note that the memory occupied by H' is freed in the Union_Binomial-Heap(H, H') procedure.

## Extracting the Node with Minimum Key

The algorithm to extract the node with minimum key from a binomial heap H is shown in Fig. 12.21. The Min-Extract_Binomial-Heap procedure accepts a heap H as a parameter and returns a pointer to the extracted node. In the first step, it finds a root node R with the minimum value and removes it from the root list of H. Then, the order of R's children is reversed and they are all added to the root list of H'. Finally, Union_Binomial-Heap(H, H') is called to unite the two heaps and R is returned. The algorithm Min-Extract-Binomial-Heap() runs in O(log n) time, where n is the number of nodes in H.

## Example 12.6 Extract the node with the minimum value from the given binomial heap.

![](img/be6359df08208122bec6fad1103de211_384_0.png)

Figure 12.22 Binomial heap

```
Binomial-Heap-Decrease_Val(H, x, k)
Step 1: IF Val[x] < k, then Print " ERROR"
Step 2: SET Val[x] = k
Step 3: SET PTR = x and PAR = Parent[PTR]
Step 4: Repeat while PAR != NIL and Val[PTR] < Val[PAR]
Step 5: SWAP ( Val[PTR], Val[PAR] )
Step 6: SET PTR = PAR and PAR = Parent [PTR]
[END OF LOOP]
Step 7: END
```

Figure 12.23 Algorithm to decrease the value of a node x in a binomial heap H

## Decreasing the Value of a Node

The algorithm to decrease the value of a node x in a binomial heap H is given in Fig. 12.23. In the algorithm, the value of the node is overwritten with a new value k, which is less than the current value of the node.

In the algorithm, we first ensure that the new value is not greater than the current value and then assign the new value to the node.

We then go up the tree with PTR initially pointing to node x. In each iteration of the while loop, val[PTR] is compared with the value of its parent PAR. However, if either PTR is the root or key[PTR] >= key[PAR], then the binomial tree is heap-ordered. Otherwise, node PTR violates heap-ordering, so its key is exchanged with that of its parent. We set PTR = PAR and PAR = Parent[PTR] to move up one level in the tree and continue the process.

The Binomial_Heap_Decrease_Val procedure takes O(log n) time as the maximum depth of node x is log n, so the while loop will iterate at most log n times.

## Deleting a Node

Once we have understood the Binomial_Heap_Decrease_Val procedure, it becomes easy to delete a node x's value from the binomial heap H in O(log n) time. To start with the algorithm, we set the value of x to -infinity. Assuming that there is no node in the heap that has a value less than -infinity, the algorithm to delete a node from a binomial heap can be given as shown in Fig. 12.24.

```
Binomial-Heap_Delete-Node(H, x)
Step 1: Binomial-Heap_Decrease_Val(H, x, -infinity)
Step 2: Min-Extract_Binomial-Heap(H)
Step 3: END
```

Figure 12.24 Algorithm to delete a node from a binomial heap

The Binomial_Heap_Delete_Node procedure sets the value of x to -infinity, which is a unique minimum value in the entire binomial heap. The Binomial_Heap_Decrease_Val algorithm bubbles this key up to a root and then this root is removed from the heap by making a call to the Min-Extract_Binomial-Heap procedure. The Binomial_Heap_Delete_Node procedure takes O(log n) time.

## Example 12.7 Delete the node with the value 11 from the binomial heap H.

## Solution

![](img/be6359df08208122bec6fad1103de211_385_0.png)

![](img/be6359df08208122bec6fad1103de211_386_0.png)

Figure 12.25 (Contd) Binomial heap

## 12.3 FIBONACCI HEAPS

In the last section, we have seen that binomial heaps support operations such as insert, extract-minimum, decrease-value, delete, and union in O(lg n) worst-case time. In this section, we will discuss Fibonacci heaps which support the same operations but have the advantage that operations that do not involve deleting an element run in O(1) amortized time. So, theoretically, Fibonacci heaps are especially desirable when the number of extract-minimum and delete operations is small relative to the number of other operations performed. This situation arises in many applications, where algorithms for graph problems may call the decrease-value once per edge. However, the programming complexity of Fibonacci heaps makes them less desirable to use.

A Fibonacci heap is a collection of trees. It is loosely based on binomial heaps. If neither the decrease-value nor the delete operation is performed, each tree in the heap is like a binomial tree. Fibonacci heaps differ from binomial heaps as they have a more relaxed structure, allowing improved asymptotic time bounds.

### 12.3.1 Structure of Fibonacci Heaps

Although a Fibonacci heap is a collection of heap-ordered trees, the trees in a Fibonacci heap are not constrained to be binomial trees. That is, while the trees in a binomial heap are ordered, those within Fibonacci heaps are rooted but unordered.

Look at the Fibonacci heap given in Figure 12.26. The figure shows that each node in the Fibonacci heap contains the following pointers:

- a pointer to its parent, and
- a pointer to any one of its children.

![](img/be6359df08208122bec6fad1103de211_386_1.png)

Figure 12.26 Fibonacci heap

Note that the children of each node are linked together in a circular doubly linked list which is known as the child list of that node. Each child x in a child list contains pointers to its left and right siblings. If node x is the only child of its parent, then left[x] = right[x] = x (refer Fig. 12.25). Circular doubly linked lists provide an added advantage, as they allow a node to be removed in O(1) time. Also, given two circular doubly linked lists, the lists can be concatenated to form one list in O(1) time.

Apart from this information, every node will store two other fields. First, the number of children in the child list of node x is stored in degree[x]. Second, a boolean value mark[x] indicates whether node x has lost a child since the last time x was made the child of another node. Of course, the newly created nodes are unmarked. Also, when the node x is made the child of another node, it becomes unmarked.

Fibonacci heap H is generally accessed by a pointer called min[H] which points to the root that has a minimum value. If the Fibonacci heap H is empty, then min[H] = NULL.

As seen in Fig. 12.27, roots of all the trees in a Fibonacci heap are linked together using their left and right pointers into a circular doubly linked list called the root list of the Fibonacci heap. Also note that the order of the trees within a root list is arbitrary.

![](img/be6359df08208122bec6fad1103de211_387_0.png)

Figure 12.27 Linked representation of the Fibonacci heap shown in Fig. 12.26

In a Fibonacci heap H, the number of nodes in H is stored in n[H] and the degree of nodes is stored in d(n).

### 12.3.2 Operations on Fibonacci Heaps

In this section, we will discuss the operations that can be implemented on Fibonacci heaps. If we perform operations such as create-heap, insert, find extract-minimum, and union, then each Fibonacci heap is simply a collection of unordered binomial trees. An unordered binomial tree v_u consists of a single node, and an unordered binomial tree v_i consists of two unordered binomial trees v_i-1 for which the root of one is made into a child of the root of another. All the properties of a binomial tree also hold for unordered binomial trees but for an unordered binomial tree v_i, the root has degree i, which is greater than that of any other node. The children of the root are roots of sub-trees v_i-1, v_i-2, ..., v_i,i in some order. Thus, if an n-node Fibonacci heap is a collection of unordered binomial trees, then t(n) = log n. The underlying principle of operations on Fibonacci heaps is to delay the work as long as possible.

## Creating a New Fibonacci Heap

To create an empty Fibonacci heap, the create_Fib_heap procedure allocates and returns the Fibonacci heap object h, where n[H] = 0 and min[H] = NULL. The amortized cost of Create_Fib_heap is equal to O(1).

## Inserting a New Node

The algorithm to insert a new node in an already existing Fibonacci heap is shown in Fig. 12.28. In Steps 1 and 2, we first initialize the structural fields of node x, making it its own circular doubly linked list. Step 3 adds x to the root list of H in O(1) actual time. Now, x becomes an unordered binomial tree in the Fibonacci heap. In Step 4, the pointer to the minimum node of Fibonacci heap H is updated. Finally, we increment the number of nodes in H to reflect the addition of the new node.
