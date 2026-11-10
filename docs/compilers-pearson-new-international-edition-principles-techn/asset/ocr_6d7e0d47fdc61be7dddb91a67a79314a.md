# A Version of Quicksort

The sketch of a quicksort program in Fig. 7.2 uses two auxiliary functions *readArray* and *partition*. The function *readArray* is used only to load the data into the array *a*. The first and last elements of *a* are not used for data, but rather for “sentinels” set in the main function. We assume *a*[0] is set to a value lower than any possible data value, and *a*[10] is set to a value higher than any data value.

The function *partition* divides a portion of the array, delimited by the arguments *m* and *n*, so the low elements of *a[m]* through *a[n]* are at the beginning, and the high elements are at the end, although neither group is necessarily in sorted order. We shall not go into the way *partition* works, except that it may rely on the existence of the sentinels. One possible algorithm for *partition* is suggested by the more detailed code in Fig. 9.1.

Recursive procedure *quicksort* first decides if it needs to sort more than one element of the array. Note that one element is always “sorted,” so *quicksort* has nothing to do in that case. If there are elements to sort, *quicksort* first calls *partition*, which returns an index *i* to separate the low and high elements. These two groups of elements are then sorted by two recursive calls to *quicksort*.

**Example 7.2:** One possible activation tree that completes the sequence of calls and returns suggested in Fig. 7.3 is shown in Fig. 7.4. Functions are represented by the first letters of their names. Remember that this tree is only one possibility, since the arguments of subsequent calls, and also the number of calls along any branch is influenced by the values returned by *partition*. □

The use of a run-time stack is enabled by several useful relationships between the activation tree and the behavior of the program:

+   1. The sequence of procedure calls corresponds to a preorder traversal of the activation tree.
+   2. The sequence of returns corresponds to a postorder traversal of the activation tree.
+   3. Suppose that control lies within a particular activation of some procedure, corresponding to a node *N* of the activation tree. Then the activations that are currently open (*live*) are those that correspond to node *N* and its ancestors. The order in which these activations were called is the order in which they appear along the path to *N*, starting at the root, and they will return in the reverse of that order.