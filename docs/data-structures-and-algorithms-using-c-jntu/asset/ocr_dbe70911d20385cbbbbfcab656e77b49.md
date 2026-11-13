```
0
4
9
54
26
35
11
Before Sorting List Is:
7 0 4 9 54 26 35 11
After Sorting List Is:
0 4 7 9 11 26 35 54
```

# 16.1.5 MERGE SORT

Before describing about merge sort, let us discuss about merging. Merging is the process of combining two ordered lists of elements and merged into a single ordered list. Merge sort can be formatted in two ways. The first approach is recursive merge sort which is more complex.

Let the two ordered lists to be merged be list [l..m] and list [m+1..n] and the resultant list is mergelist [l..n]. Algorithm 16.5 is the algorithm for merging two ordered lists.

```
Algorithm 16.5: MERGE (list, merge list, l, m, n)
1. Set i=l, j=1, k=m+1 //i,j,k are list partitions
2. Loop for i sm, ksn;j++
   1. Check whether list[i] <= list[k] then
   2. Set mergelist[j]=list(i)
   3. Set i=i+1
   4. Else
   5. Set mergelist[j]=list[k]
   6. Set k=k+1
   7. Copy (list+i, list+k, mergelist+j) /*copy the remaining elements, if any, of first list*/
   8. Copy (list+k, list+n+1, mergelist+j) /*copy the remaing elements, if any of second list*/
3. End loop
4. End
```

j will be incremented by 1 at each iteration of the loop. The total increment in j is at most n-l+1. Hence the total number of iterations in the loop is at n-l+1 times. The statement copy copies at most n-l+1 elements. So, the total time complexity is given by O (n-l+1).

**Non-recursive merge sort:** The non-recursive version of merge sort begins by treating the given input list of n elements as n independent ordered sublist of size 1. The first pass merges all these sublists into n/2 sublists each with two sublists again. If n is odd then one sublist will be of size 1. In the second pass, all these n/2 sublists are then merged to obtain n/4 sublists. Each pass reduces the number of sublists to half. Continue the process of merge until only one sublist exists.

# Example 16.5

The given list is {32, 4, 55, 1, 16, 11, 95, 51, 84, 19} which is to be sorted. The tree of Figure 16.5 illustrates the merging of sublists at each pass.