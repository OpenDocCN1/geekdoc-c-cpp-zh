6.15 Suppose we need to perform $M$ percolateUps and $N$ deleteMins on a $d$-heap that initially has $N$ elements.
a. What is the total running time of all operations in terms of $M$, $N$, and $d$?
b. If $d = 2$, what is the running time of all heap operations?
c. If $d = \Theta(N)$, what is the total running time?
* d. What choice of $d$ minimizes the total running time?

6.16 Suppose that binary heaps are represented using explicit links. Give a simple algorithm to find the tree node that is at implicit position $i$.

6.17 Suppose that binary heaps are represented using explicit links. Consider the problem of merging binary heap lhs with rhs. Assume both heaps are perfect binary trees, containing $2^l - 1$ and $2^r - 1$ nodes, respectively:
a. Give an $O(\log N)$ algorithm to merge the two heaps if $l = r$.
b. Give an $O(\log N)$ algorithm to merge the two heaps if $|l - r| = 1$.
* c. Give an $O(\log^2 N)$ algorithm to merge the two heaps regardless of $l$ and $r$.

6.18 A min-max heap is a data structure that supports both deleteMin and deleteMax in $O(\log N)$ per operation. The structure is identical to a binary heap, but the heap-order property is that for any node, $X$, at even depth, the element stored at $X$ is smaller than the parent but larger than the grandparent (where this makes sense), and for any node, $X$, at odd depth, the element stored at $X$ is larger than the parent but smaller than the grandparent. See Figure 6.58.
a. How do we find the minimum and maximum elements?
* b. Give an algorithm to insert a new node into the min-max heap.
* c. Give an algorithm to perform deleteMin and deleteMax.
* d. Can you build a min-max heap in linear time?
* * e. Suppose we would like to support deleteMin, deleteMax, and merge. Propose a data structure to support all operations in $O(\log N)$ time.

![](bbox=[0.05, 0.6, 0.85, 0.88])

Figure 6.58 Min-max heap