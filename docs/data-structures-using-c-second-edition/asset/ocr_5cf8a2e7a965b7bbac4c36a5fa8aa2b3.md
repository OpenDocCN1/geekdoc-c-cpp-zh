We then go up the tree with PTR initially pointing to node x. In each iteration of the while loop, val[PTR] is compared with the value of its parent PAR. However, if either PTR is the root or key[PTR] >= key[PAR], then the binomial tree is heap-ordered. Otherwise, node PTR violates heap-ordering, so its key is exchanged with that of its parent. We set PTR = PAR and PAR = Parent[PTR] to move up one level in the tree and continue the process.

The Binomial_Heap_Decrease_Val procedure takes O(log n) time as the maximum depth of node x is log n, so the while loop will iterate at most log n times.

# Deleting a Node

Once we have understood the Binomial_Heap_Decrease_Val procedure, it becomes easy to delete a node x's value from the binomial heap H in O(log n) time. To start with the algorithm, we set the value of x to -infinity. Assuming that there is no node in the heap that has a value less than -infinity, the algorithm to delete a node from a binomial heap can be given as shown in Fig. 12.24.

```
Binomial-Heap_Delete-Node(H, x)
Step 1: Binomial-Heap_Decrease_Val(H, x, -infinity)
Step 2: Min-Extract_Binomial-Heap(H)
Step 3: END
```

# Figure 12.24 Algorithm to delete a node from a binomial heap

The Binomial_Heap_Delete_Node procedure sets the value of x to -infinity, which is a unique minimum value in the entire binomial heap. The Binomial_Heap_Decrease_Val algorithm bubbles this key upto a root and then this root is removed from the heap by making a call to the Min-Extract_Binomial-Heap procedure. The Binomial_Heap_Delete_Node procedure takes O(log n) time.

# Example 12.7 Delete the node with the value 11 from the binomial heap H.

# Solution

![](bbox=[0.1, 0.515, 0.903, 0.93])