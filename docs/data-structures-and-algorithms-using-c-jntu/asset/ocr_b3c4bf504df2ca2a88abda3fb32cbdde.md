![](bbox=[0.08, 0.08, 0.92, 0.42])

# Figure 16.5 Merge tree

Algorithm 16.5.2 contains several passes over the elements to be sorted. Now sorting can be done by repeatedly invoking the algorithm called MERGEPASS. In this first pass, lists with size 1 are merged and in the second pass lists with size 2 are merged and so on. On the i th pass, the size of the lists to be merged will be 2^(i-1). Therefore a total of [log2 n] passes are required to merge the sublists. Since two lists are merged with linear time and the complexity of merge sort is O(n), the total time complexity is O(n log n)

# Algorithm 16.5.1: MERGEPASS (list,FinalList, n,s)

```
/*s is the size of sublists. n is the number of elements in the list. Sublists of size s are merged from list to FinalList.*/
1. Set i=1 // i is the first position in the first sub list being merged
2. loop for i<=n-2*s+1 do
   1. Set i=i+2*s
   2. MERGE (list,FinalList,i,i+s-1,i+2*s-1);
   3. MERGE (list,FinalList,i,i+s-1,n) // Merging the remaining list
   4. Check whether (i+s-1)<n then
   5. Else
   6. Copy (list+1,list+n+1,FinalList+i)
3. End
```

# Algorithm 16.5.2: MERGESORT(A,n)

```
/* sorting Array A[1:n] into ascending order. Let temp be an array which holds the sorted elements. 1 is the length of the sublist that is to the merged.*/
1. Set l=1
2. loop for (1<n; l*=2)
   1. MERGEPASS (A,temp,n,l)
   2. Set l=l*2
```