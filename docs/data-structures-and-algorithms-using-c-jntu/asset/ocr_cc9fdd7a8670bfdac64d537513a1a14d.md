```
cin>>a[i];
cout<<"Enter Search Element :";
cin>>search;
sort(a,n);
fsearch(a,0,n,search);
}
```

# Output

```
Enter Size Of Array:10
Enter 10 Elements:4 2 6 3 1 5 7 8 10 21
Enter Search Element :8
Search Element 8 Is Found

Enter Size Of Array:5
Enter 5 Elements:6
2
4
3
7
Enter Search Element:10
Search Element 10 Is Not Found
```

# SUMMARY

+   - The bubble sort works by iterating down an array to be sorted from the first element to the last, comparing each pair of elements and switching their positions if necessary.
+   - Insertion sort inserts each element of the array into its proper position leaving progressively larger stretches of the array sorted.
+   - Quicksort is a relatively simple sorting technique using the divide-and-conquer recursive procedure.
+   - Merge sort is a fast, stable sorting routine with guaranteed O(n log n) efficiency.
+   - The idea of Shell sort is to arrange the data sequence in a two-dimensional array and sort the columns of the array.
+   - Radix sort keeps the elements in order by comparing the digits of the numbers.
+   - Heap sort is a relatively simple technique built upon the heap data structure.
+   - Searching is the process of finding the location of a given element in a set of elements.
+   - Linear is the technique of searching a given item in the list by comparing each and every element in the list sequentially.
+   - Binary search is a technique of searching an item in the ordered list by dividing the list into two halves with each comparison until the item is found or not.
+   - The Fibonacci search is a technique of searching a sorted array using the divide and conquer principle.
+   - Fibonacci search determines the next element for comparison based on the sequence of the Fibonacci number and it performs a search technique only on the ordered list.