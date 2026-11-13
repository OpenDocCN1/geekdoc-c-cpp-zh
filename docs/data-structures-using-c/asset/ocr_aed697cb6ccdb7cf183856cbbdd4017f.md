The recursive algorithm consists of four steps:

+   1. If there is one element in the array to be sorted, return immediately.
+   2. Pick an element in the array to serve as a 'pivot' point. Usually the leftmost element in the array is used.
+   3. Split the array into two parts—one with elements smaller than the pivot and the other with elements larger than the pivot.
+   4. Recursively repeat the algorithm for both halves of the original array.

In quick sort, the given array is divided into two subarrays so that the sorted subarrays need not be merged later. This is accomplished by rearranging the elements in A[1:n] such that A[i] < A[j] for all i between 1 and m and all j between m + 1 and n for some m, 1 <= m <= n. Thus, the elements in A[1:m] and A[m + 1:n] can be independently sorted. No merge is needed.

The rearrangement of elements is accomplished by picking some element of array A[], say t = A[5] and then reordering the other elements so that all elements appearing before t in A[1:n] are less than or equal to t, and those appearing after t are greater than or equal to t. This rearrangement is called partitioning.

Let us assume that m represents the first position in a partition in Algorithm 16.5 which describes partitioning.

```
ALGORITHM 16.5
Algorithm Partition(A, m, p)
begin
  v = A[m], i = m, j = p
  do
    begin
      // find first element lesser than pivot
      do i = i + 1 while(A(i) <= v);
      // find first element greater than pivot
      do j = j - 1 while(A(j) >= v);
      if i < j exchange(A(i), A(j))
    end
  while(i <= j);
  A(m) = A(j), A(j) = v  // place pivot at its correct position
  return(j);
end
```

Algorithm 16.6 is the quick sort algorithm.

```
ALGORITHM 16.6
Algorithm qsort (p, q)
/* p and q are start and end positions of a partition */
begin
  if(p < q) then
    begin
      j = q + 1
```