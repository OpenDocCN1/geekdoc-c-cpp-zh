14.14 For the following recurrence, give a closed-form solution. You should not give an exact solution, but only an asymptotic solution (i.e., using $\Theta$ notation). You may assume that $n$ is a power of 2. Prove that your answer is correct.

```
$T(n) = T(n/2) + \sqrt{n}$ for $n > 1; \quad T(1) = 1.$
```

14.15 Using the technique of expanding the recurrence, find the exact closed-form solution for the recurrence relation

```
$T(n) = 2T(n/2) + n; \quad T(2) = 2.$
```

You may assume that $n$ is a power of 2.

14.16 Section 5.5 provides an asymptotic analysis for the worst-case cost of **buildHeap**. Give an exact analysis for **buildHeap**.

14.17 Each of the following recurrences, find and prove (using induction) an exact closed-form solution. When convenient, you may assume that $n$ is a power of 2.

+   (a) $T(n) = T(n-1) + n/2$ for $n > 1; \quad T(1) = 1$.
(b) $T(n) = 2T(n/2) + n$ for $n > 2; \quad T(2) = 2.$

14.18 Use Theorem 14.1 to prove that binary search requires $\Theta(\log n)$ time.

14.19 Recall that when a hash table gets to be more than one half full, its performance quickly degrades. One solution to this problem is to reinsert all elements of the hash table into a new hash table that is twice as large. Assuming that the (expected) average cost to insert is constant, prove that the cost to insert is $\Theta(1)$ when re-insertion is used.

14.20 Given a 2-3 tree with $n$ nodes, prove that inserting $M$ additional nodes requires $O(M + n)$ node splits.

14.21 One approach to implementing an array-based list where the list size is unknown is to let the array grow and shrink. This is known as a **dynamic array**. When necessary, we can grow or shrink the array by copying the array's contents to a new array. If we are careful about the size of the new array, this copy operation done rarely enough so as not to affect the amortized cost of operations.

+   What is the amortized cost of inserting elements into the list if its size is initially of 1 and we double the array size whenever the number of elements that we wish to exceeds the size of the array? Assume that the insert itself costs $O(1)$ time per operation and so we are just concerned with minimizing the copy time to the new array.