named as merge sort. The Mergesort algorithm can be described in general terms as consisting of the following three steps:

Suppose A is an array with N elements from A[0] to A[N-1].

+   1. Divide Step: If given array A has zero or one element, then return, as it is already sorted. Otherwise, divide A into two sub-arrays, A1 = A[0], A[1], ..., A[N/2-1] and A2 = A[N/2], A[N/2+1], ..., A[N-1], each containing about half of the elements of A.
+   2. Recursion Step: Recursively sort two sub-array A1, and A2;
+   3. Conquer Step: Combine the elements back in A by merging the two sorted arrays A1 and A2 into a single sorted sequence.

Example:

Input Data: 8, 6, 3, 5, 2, 7, 4 and 1.

![](bbox=[0.15, 0.305, 0.85, 0.575])

![](bbox=[0.15, 0.605, 0.85, 0.855])

Figure 10.116: (a) Divide phase and (b) Combine phase