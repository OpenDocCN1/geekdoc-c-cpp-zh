4.10 Let f(N) be the average number of full nodes in an N-node binary search tree.
a. Determine the values of f(0) and f(1).
b. Show that for N > 1

f(N) = \frac{N-2}{N} + \frac{1}{N} \sum_{i=0}^{N-1} (f(i) + f(N-i-1))

c. Show (by induction) that f(N) = (N - 2)/3 is a solution to the equation in part (b), with the initial conditions in part (a).
d. Use the results of Exercise 4.6 to determine the average number of leaves in an N-node binary search tree.

4.11 Write an implementation of the set class, with associated iterators using a binary search tree. Add to each node a link to the parent node.

4.12 Write an implementation of the map class by storing a data member of type set<Pair<KeyType,ValueType>>.

4.13 Write an implementation of the set class, with associated iterators using a binary search tree. Add to each node a link to the next smallest and next largest node. To make your code simpler, add a header and tail node which are not part of the binary search tree, but help make the linked list part of the code simpler.

4.14 Suppose you want to perform an experiment to verify the problems that can be caused by random insert/remove pairs. Here is a strategy that is not perfectly random, but close enough. You build a tree with N elements by inserting N elements chosen at random from the range 1 to M = \alpha N. You then perform N^2 pairs of insertions followed by deletions. Assume the existence of a routine, randomInteger(a,b), which returns a uniform random integer between a and b inclusive.
a. Explain how to generate a random integer between 1 and M that is not already in the tree (so a random insertion can be performed). In terms of N and \alpha, what is the running time of this operation?
b. Explain how to generate a random integer between 1 and M that is already in the tree (so a random deletion can be performed). What is the running time of this operation?
c. What is a good choice of \alpha? Why.

4.15 Write a program to evaluate empirically the following strategies for removing nodes with two children:
a. Replace with the largest node, X, in T_L and recursively remove X.
b. Alternately replace with the largest node in T_L and the smallest node in T_R, and recursively remove the appropriate node.
c. Replace with either the largest node in T_L or the smallest node in T_R (recursively removing the appropriate node), making the choice randomly.
Which strategy seems to give the most balance? Which takes the least CPU time to process the entire sequence?

4.16 Redo the binary search tree class to implement lazy deletion. Note carefully that this affects all of the routines. Especially challenging are findMin and findMax, which must now be done recursively.