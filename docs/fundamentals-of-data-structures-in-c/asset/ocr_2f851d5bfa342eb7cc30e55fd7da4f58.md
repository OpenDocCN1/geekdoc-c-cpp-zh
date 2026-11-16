# 6. List out some of the stable and unstable sorting techniques.

Stable sorting techniques includes

+   - Bubble sort
+   - Selection sort
+   - Insertion sort
+   - Merge sort.

Unstable sorting techniques includes

+   - Shell sort
+   - Radix sort
+   - Quick sort.

# 7. Why is the bubble sort called by name ?

The bubble sort derives its name from the fact that while sorting the data, the smallest data item bubbles to the initial position of the partially sorted list.

# 8. Why is the bubble sort is also called as sinking sort ?

Bubble sort also referred as sinking sort derives its name from the fact that while sorting the data, the largest data item sinks to the final position of the list.

# 9. Mention the limitation of insertion sort.

Insertion sort has the limitation, that it compares only the consecutive elements and interchanges the elements by only one space. The smaller elements that are far away require many passes through the sort to properly place them in its correct position.

# 10. How sorting is performed in merge sort ?

The merge sort algorithm chops the list into two. If the list has even length, split the list into two equal sub lists. If the list has odd length, divide the list into two by making the first sub list one entry greater than the second sub list. Then split both the sub lists into two and go on until each of the sub lists are of size one. Finally, start merging the individual sub lists to obtain a sorted list.

# 11. How sorting is performed in quick sort ?

Quick sort divides the initial unsorted list into two parts, such that every element in the first list is less than all the elements present in the second list. The procedure is then repeated recursively for both the parts, up to relatively short sequences, which can be sorted until the sequences, reduces to length one.

# 12. What is median-of-three-portitioning method ?

The median-of-three-portitioning method is employed in quick sort to find the pivot value. This is done by randomly choosing three elements in the list and finding the median of the elements gives the pivot value.