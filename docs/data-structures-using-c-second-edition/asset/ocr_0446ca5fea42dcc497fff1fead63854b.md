```
Union_Binomial-Heap(H1, H2)
Step 1: SET H = Create_Binomial-Heap()
Step 2: SET Head[H] = Merge_Binomial-heap(H1, H2)
Step 3: Free the memory occupied by H1 and H2
Step 4: IF Head[H] = NULL, then RETURN H
Step 5: Make PTR = NULL, PRE = Head[H] and NEXT = Sibling[PTR]
Step 6: Repeat Step 7 while NEXT != NULL
Step 7: IF Degree[PTR] != Degree[NEXT] OR (Sibling[NEXT] != NULL AND Degree[Sibling[NEXT]] = Degree[PTR]), then SET Prev = PTR, PTR = NEXT ELSE IF Val[PTR] <= Val[NEXT], then SET Sibling[PTR] = Sibling[NEXT] Link_Binomial-Tree(NEXT, PTR) ELSE IF Prev = NULL, then Head[H] = NEXT ELSE Sibling[Prev] = NEXT Link_Binomial-Tree(PTR, NEXT) SET PTR = NEXT SET NEXT = Sibling[PTR]
Step 8: RETURN H
```

# Figure 12.18 Algorithm to unite two binomial heaps

The algorithm destroys the original representations of heaps H1 and H2. Apart from Link_Binomial-Tree(), it uses another procedure Merge_Binomial-Heap() which is used to merge the root lists of H1 and H2 into single linked list that is sorted by degree into a monotonically increasing order.

In the algorithm, Steps 1 to 3 merge the root lists of binomial heaps H1 and H2 into a single root list H in such a way that H1 and H2 are sorted strictly by increasing degree. Merge_Binomial-Heap() returns a root list H that is sorted by monotonically increasing degree. If there are m roots in the root lists of H1 and H2, then Merge_Binomial-Heap() runs in O(m) time. This procedure repeatedly examines the roots at the heads of the two root lists and appends the root with the lower degree to the output root list, while removing it from its input root list.

Step 4 of the algorithm checks if there is at least one root in the heap H. The

algorithm proceeds only if H has at least one root. In Step 5, we initialize three pointers: PTR which points to the root that is currently being examined, PREV which points to the root preceding PTR on the root list, and next which points to the root following PTR on the root list.

In Step 6, we have a while loop in which at each iteration, we decide whether to link PTR to NEXT or next to PTR depending on their degrees and possibly the degree of Sibling[NEXT].

In Step 7, we check for two conditions. First, if degree[PTR] != degree[NEXT], that is, when PTR is the root of a binomial tree and NEXT is the root of a binomial tree for some j > 1, then PTR and NEXT are not linked to each other, but we move the pointers one position further down the list. Second, we check if PTR is the first of three roots of equal degree, that is, degree[PTR] = degree[NEXT] = degree[Sibling[NEXT]]

In this case also, we just move the pointers one position further down the list by writing PREV = PTR, PTR = NEXT.

However, if the above IF conditions do not satisfy, then the case that pops up is that PTR is the first of two roots of equal degree, that is, degree[PTR] = degree[NEXT] != degree[Sibling[NEXT]]

In this case, we link either PTR with NEXT or NEXT with PTR depending on whichever has the smaller key. Of course, the node with the smaller key will be the root after the two nodes are linked.

The running time of Union-Binomial-Heap() can be given as O(log n), where n is the total number of nodes in binomial heaps H1 and H2. If n1 contains n nodes and H2 contains n2 nodes, then H1 contains at most log(n1 + 1) roots and H2 contains at most log(n2 + 1) roots, so H contains at most (log n1 + log n2 + 2) <= 2(log n + 2) = O(log n) roots when we call Merge_Binomial-Heap(). Since, n = n1 + n2, the Merge_Binomial-Heap() takes O(log n) to execute. Each iteration of the while loop takes O(1) time, and because there are at most (log n1 + log n2 + 2) iterations, the total time is thus O(log n).