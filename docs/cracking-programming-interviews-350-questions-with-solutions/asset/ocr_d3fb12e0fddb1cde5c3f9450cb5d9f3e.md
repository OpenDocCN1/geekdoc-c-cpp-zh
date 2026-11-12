image-processing applications, where the leaves correspond to the inputs (e.g., pixels in a picture) and the algorithms for manipulating them are hierarchical. Let us solve the problem of finding the *k*th smallest element.

# Solution

This example illustrates the translation of a sequential algorithm to a parallel algorithm, and the use of pipelining.

First, we recall the sequential algorithm for finding the *k*th smallest element. We assume, for simplicity, that the elements are distinct. The algorithm is a probabilistic one. In each step, a random element *x* is chosen as the pivot. The rank of *x* is computed by comparing *x* to all other elements and, according to whether the rank is smaller or greater than *k*, the elements that are less than *x* or greater than *x* are eliminated.

The algorithm terminates when the rank of the pivot is *k*.

The expected number of iterations is *O*(log *n*), and the expected number of comparisons is *O*(*n*).

There are three different phases in each iteration of the algorithm:

+   1. choosing a random element,
+   2. computing its rank, and
+   3. eliminating.

*We first describe efficient parallel implementations of each phase, then improve the parallelization even further.*

Choosing a random element can be achieved by a *tournament* arranged on the tree. Each leaf sends its number to its parent where the number competes with the number of its sibling leaf by flipping a coin. The winning number is then promoted up again, and the same process continues up the tree until the root chooses the overall winner.

Please note that this works only in the first iteration; we discuss later how to make it work after some elements are eliminated.

The winning number is then broadcast down the tree, so that all leaves can compare it with their number. If the identity of the pivot is known at all the leaves, they can all compare their numbers to the pivot in one step. They then send a

+   - 1 (if their number is smaller than or equal to the pivot)
+   - 0 (otherwise)