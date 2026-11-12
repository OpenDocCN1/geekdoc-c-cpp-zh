one recursive call instead of two while still being able to perform the merge step in parallel.

# ## 7.4 Finding Ranks in Linked Lists

Generally, it is much more difficult to deal with linked representation in a parallel environment than with arrays. Linked lists, for example, are inherently sequential. If the only access to the link list is through the head of the list, then we have to traverse the list one element at a time with no possibility of parallelism. In many cases, however, the elements of the list, or pointers to them, are actually stored in a contiguous array. In such cases, where parallel access to the list is possible, there is hope for fast parallel algorithms.

The rank of an element in a linked list is defined here as the distance of the element from the end of the list, thus, the head has rank \(n\), the second element has rank \(n-1\), and so on.

# ### Problem Description

Given a linked list of \(n\) elements, all of which are stored in an array \(A[1..n]\), compute for each element its rank in the list.

# ### Solution

We can solve the sequential problem by simply traversing the list. The method we will use for designing a parallel algorithm for this problem is called doubling. We assign a processor to each element. Initially, each processor knows only the right neighbor of its element in the list. In the first step, each processor finds the neighbor of its neighbor. After the first step, each processor knows the element at distance 2 from its element. If, at step \(i\), each processor knows the element at distance \(k\) from its element, then in one step each processor can find the element at distance \(2k\). This process continues until the end of the list is reached.

Let \(N[i]\) be the farthest element to the right of \(i\) in the list that is known to \(P_i\) at a given moment. Initially, \(N[i]\) is the right neighbor except for the last element whose right neighbor is nil. Basically, in each step, \(P_i\) updates \(N[i]\) to \(N[N[i]]\) until the end of the list is reached. Let \(R[i]\) be the rank of \(i\). Initially \(R[i]\) is set to 0, except for the last element in the list, for which it is set to 1. This element is detected by its nil pointer. When a processor encounters a neighbor with a nonzero rank \(R\), this processor can determine its own rank.

Initially, only the element of rank 1 knows its rank. After the first step, the element of rank 2 finds that its right neighbor has rank 1, so it knows its own rank is 2. After the second step, rank 3 and rank 4 are determined, and so on. If \(P_i\) finds that \(N[i]\) points to a ranked