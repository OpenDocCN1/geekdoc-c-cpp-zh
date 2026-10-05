267

algorithm to modify the key values such that every modified key value is unique, the resulting key values give the same sort order as the original keys, the result is stable (in that the duplicate original key values remain in their original order), and the process of altering the keys is done in linear time by using only a constant amount of additional space.

7.8 The discussion of Quicksort in Section 7.5 described using a stack instead of recursion to reduce the number of function calls made.

+   (a) How deep the stack get in the worst case?

+   (b) Quicksort makes recursive calls. The algorithm could be changed to make these two calls in a specific order. In what order should the two calls be made, and how does this affect how deep the stack can become?

7.9 Give a permutation of the values 0 through 7 that will cause Quicksort (as implemented in Section 7.5) to have its worst case behavior.

7.10 Assume L is an array, length (L) returns the number of records in the array and qsort(L, i, j) sorts the records of L from i to j (leaving the records sorted in L) using the Quicksort algorithm. What is the average-case complexity for each of the following code fragments?

```
(a) for (i=0; i<length(L); i++)
qsort(L, 0, i);
```

```
(b) for (i=0; i<length(L); i++)
qsort(L, 0, length(L)-1);
```

7.11 Modify Quicksort to find the smallest k values in an array of records. Your output should be the array modified so that the smallest values are sorted in the first k positions of the array. Your algorithm should do the minimum amount of work necessary, that is, no more than the array should be sorted.

7.12 Modify Quicksort to sort a sequence of variable-length strings one after the other in a character array, with a second array (pointers to strings) used to index the strings. Your function should modify the index array so that the first pointer points to the beginning of the lowest value string, and so on.

7.13 Graph f1(n)=n log n, f2(n)=n^1.5, and f3(n)=n^2 in the range 1 ≤ n ≤ 1000 to compare their growth rates. Typically, the constant factor in the running-time expression for an implementation of Insertion Sort will be less than the constant factors for Shellsort or Quicksort. How many times greater can the constant factor be for Shellsort to be faster than Insertion Sort when n = 1000? How many times greater can the constant factor be for Quicksort to be faster than Insertion Sort when n = 1000?