# Figure 12.1 Linear search. The grayed out elements are not considered during the search process.

```
int list[] = { 100, 44, 2, 80, 5, 13, 11, 2, 110 };
int x = locate(list, 9, 13);
```

![](bbox=[0.285, 0.226, 0.703, 0.318])

+   • print prints out the elements in any vector using the format function to properly format the values. This alignment simplifies the display function.

+   • display uses locate, print, and setw to provide a graphical display of the operation of the locate function.

The kind of search performed by locate is known as linear search, since the process takes a straight line path from the beginning to the end of the vector, and it considers each element in order. Figure 12.1 illustrates linear search.

# 12.3.2 Binary Search

Linear search is acceptable for relatively small vectors, but the process of examining each element in a large vector is time consuming. An alternative to linear search is binary search. In order to perform binary search a vector's elements must be in sorted order. Binary search exploits this sorted structure of the vector using a clever but simple strategy that quickly zeros in on the element to find:

+   1. If the vector is empty, return -1.

+   2. Check the element in the middle of the vector. If the element is what you are seeking, return its position. If the middle element is larger than the element you are seeking, perform a binary search on the first half of the vector. If the middle element is smaller than the element you are seeking, perform a binary search on the second half of the vector.

This approach is analogous to looking for a telephone number in the phone book in this manner:

+   1. Open the book at its center. If the name of the person is on one of the two visible pages, look at the phone number.

+   2. If not, and the person's last name is alphabetically less the names on the visible pages, apply the search to the left half of the open book; otherwise, apply the search to the right half of the open book.

+   3. Discontinue the search with failure if the person's name should be on one of the two visible pages but is not present.