# Algorithm of Merge Sort

```
Algorithm: MERGE_SORT(A, F, L)
[A is an array of N elements, F is the first position and L is the last position of the sub-array]
1. If F < L then
    a) Set MID = (F + L)/2
    b) Call MERGE_SORT(A, F, MID)
    c) Call MERGE_SORT(A, MID+1, L)
    d) Call MERGE(A, F, L, MID)
2. Return

Function: MERGE(A, F, L, MID)
[A is an array, F is the first position, L is the last position and MID is the middle position of the sub-array]
1. Set I = F, J = MID + 1, K = F
2. Repeat while I <= MID and J <= L
    If A[I] < A[J] then
    a) Set C[K] = A[I]
    b) Set I = I + 1
    c) Set K = K + 1
    ELSE
    a) Set C[K] = A[J]
    b) Set J = J + 1
    c) Set K = K + 1
    [End of IF]
    [End of Loop]
3. Repeat while I <= MID
    a) Set C[K] = A[I]
    b) Set I = I + 1
    c) Set K = K + 1
    [End of Loop]
4. Repeat while J <= L
    a) Set C[K] = A[J]
    b) Set J = J + 1
    c) Set K = K + 1
    [End of Loop]
5. Repeat for I = F to K
    Set A[I] = C[I]
6. Return
```

# Time complexity of MergeSort

Best-case / Worst-case / Average-case time complexity: In Merge-sort the partitions are always evenly balanced, their sizes are equal, each partition has n/2 elements. Each of the subproblems of size n/2