![](bbox=[0.315, 0.085, 0.685, 0.465])

# ## 4.6.4 Sorting

Sorting is an operation that is used to arrange the elements of an array either in ascending or descending order. Algorithm 4.4 illustrates sorting of the elements in an ascending order .

```
Algorithm 4.4
SORT : N=UB
1. Set N=UB
2. while i>=LB do
3. Set q=LB //comparing the first
4. while jci do
5. check whether A[j]&A[j+1] are in order, if so swap the elements
   SWAP (A[j], A[j+1])
6. Set j=j+1
7. Set i=i-1
8. End
```

# ## 4.6.5 Searching

Searching is an operation that is used to find the location of a particular element from the list of elements in an array. When the item is found, then search is said to be successful. There are different types of searching algorithms. Usage of these algorithms depends upon the way the data elements are arranged in the data structures. A detailed discussion of searching techniques can be found in Chapter 16.