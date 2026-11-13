
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

![](img/e449061a0cac9cafaefd979fab665b33_303_0.png)

Figure 6.58 Min-max heap

![](img/e449061a0cac9cafaefd979fab665b33_304_0.png)

Figure 6.59 Input for Exercises 6.19 and 6.26

6.19 Merge the two leftist heaps in Figure 6.59.

6.20 Show the result of inserting keys 1 to 15 in order into an initially empty leftist heap.

6.21 Prove or disprove: A perfectly balanced tree forms if keys 1 to 2^k - 1 are inserted in order into an initially empty leftist heap.

6.22 Give an example of input that generates the best leftist heap.

6.23 a. Can leftist heaps efficiently support decreaseKey? b. What changes, if any (if possible), are required to do this?

6.24 One way to delete nodes from a known position in a leftist heap is to use a lazy strategy. To delete a node, merely mark it deleted. When a findMin or deleteMin is performed, there is a potential problem if the root is marked deleted, since then the node has to be actually deleted and the real minimum needs to be found, which may involve deleting other marked nodes. In this strategy, removes cost one unit, but the cost of a deleteMin or findMin depends on the number of nodes that are marked deleted. Suppose that after a deleteMin or findMin there are k fewer marked nodes than before the operation.
* a. Show how to perform the deleteMin in O(k log N) time.
** b. Prove an implementation, with an analysis to show that the time to perform the deleteMin is O(k log(2N/k)).

6.25 We can perform buildHeap in linear time for leftist heaps by considering each element as a one-node leftist heap, placing all these heaps on a queue, and performing the following step: Until only one heap is on the queue, dequeue two heaps, merge them, and enqueue the result.
a. Prove that this algorithm is O(N) in the worst case.
b. Why might this algorithm be preferable to the algorithm described in the text?

6.26 Merge the two skew heaps in Figure 6.59.

6.27 Show the result of inserting keys 1 to 15 in order into a skew heap.

6.28 Prove or disprove: A perfectly balanced tree forms if the keys 1 to 2^k - 1 are inserted in order into an initially empty skew heap.

6.29 A skew heap of N elements can be built using the standard binary heap algorithm. Can we use the same merging strategy described in Exercise 6.25 for skew heaps to get an O(N) running time?

6.30 Prove that a binomial tree, B_k, has binomial trees B_0, B_1, ..., B_{k-1} as children of the root.

![](img/e449061a0cac9cafaefd979fab665b33_305_0.png)

Figure 6.60 Input for Exercise 6.32

6.31 Prove that a binomial tree of height k has $\binom{k}{d}$ nodes at depth d.

6.32 Merge the two binomial queues in Figure 6.60.

6.33
a. Show that N inserts into an initially empty binomial queue take O(N) time in the worst case.
b. Give an algorithm to build a binomial queue of N elements, using at most N - 1 comparisons between elements.
* c. Propose an algorithm to insert M nodes into a binomial queue of N elements in O(M + log N) worst-case time. Prove your bound.

6.34 Write an efficient routine to perform insert using binomial queues. Do not call merge.

6.35 For the binomial queue
a. Modify the merge routine to terminate merging if there are no trees left in H2 and the carry tree is nullptr.
b. Modify the merge so that the smaller tree is always merged into the larger.

** 6.36 Suppose we extend binomial queues to allow at most two trees of the same height per structure. Can we obtain O(1) worst-case time for insertion while retaining O(log N) for the other operations?

6.37 Suppose you have a number of boxes, each of which can hold total weight C and items i1, i2, ..., iy, which weigh w1, w2, ..., wy, respectively. The object is to pack all the items without placing more weight in any box than its capacity and using as few boxes as possible. For instance, if C = 5, and the items weights 2, 2, 3, 3, then we can solve the problem with two boxes.
In general, this problem is very hard, and no efficient solution is known. Write programs to implement efficiently the following approximation strategies:
a. Place the weight in the first box for which it fits (creating a new box if there is no box with enough room). (This strategy and all that follow would give three boxes, which is suboptimal.)
b. Place the weight in the box with the most room for it.
* c. Place the weight in the most filled box that can accept it without overflowing.
** d. Are any of these strategies enhanced by presorting the items by weight?

6.38 Suppose we want to add the decreaseAllKeys(Δ) operation to the heap repertoire. The result of this operation is that all keys in the heap have their value decreased by an amount Δ. For the heap implementation of your choice, explain the necessary modifications so that all other operations retain their running times and decreaseAllKeys runs in O(1).

6.39 Which of the two selection algorithms has the better time bound?

6.40 The standard copy constructor and makeEmpty for leftist heaps can fail because of too many recursive calls. Although this was true for binary search trees, it is more problematic for leftist heaps, because a leftist heap can be very deep, even while it has good worst-case performance for basic operations. Thus the copy constructor and makeEmpty need to be reimplemented to avoid deep recursion in leftist heaps. Do this as follows:
a. Reorder the recursive routines so that the recursive call to t->left follows the recursive call to t->right.
b. Rewrite the routines so that the last statement is a recursive call on the left subtree.
c. Eliminate the tail recursion.
d. These functions are still recursive. Give a precise bound on the depth of the remaining recursion.
* e. Explain how to rewrite the copy constructor and makeEmpty for skew heaps.

## References

The binary heap was first described in [28]. The linear-time algorithm for its construction is from [14].

The first description of d-heaps was in [19]. Recent results suggest that 4-heaps may improve binary heaps in some circumstances [22]. Leftist heaps were invented by Crane [11] and described in Knuth [211]. Skew heaps were developed by Sleator and Tarjan [24]. Binomial queues were invented by Vuillemin [27]; Brown provided a detailed analysis and empirical study showing that they perform well in practice [4], if carefully implemented. Exercise 6.7(b-c) is taken from [17]. Exercise 6.10(c) is from [6]. A method for constructing binary heaps that uses about 1.52N comparisons on average is described in [23]. Lazy deletion in leftist heaps (Exercise 6.24) is from [10]. A solution to Exercise 6.36 can be found in [8].

Min-max heaps (Exercise 6.18) were originally described in [1]. A more efficient implementation of the operations is given in [18] and [25]. Alternative representations for double-ended priority queues are the deap and diamond deque. Details can be found in [5], [7], and [9]. Solutions to 6.18(c) are given in [12] and [20].

A theoretically interesting priority queue representation is the Fibonacci heap [16], which we will describe in Chapter 11. The Fibonacci heap allows all operations to be performed in O(1) amortized time, except for deletions, which are O(log N). Relaxed heaps [13] achieve identical bounds in the worst case (with the exception of merge). The procedure of [3] achieves optimal worst-case bounds for all operations. Another interesting implementation is the pairing heap [15], which is described in Chapter 12. Finally, priority queues that work when the data consist of small integers are described in [2] and [26].
