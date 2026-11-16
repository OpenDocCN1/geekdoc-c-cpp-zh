# # Chapter 5

# # Searching and Sorting Algorithms

# ## 5.1 Introduction

In this chapter, we will discuss two most important techniques used in programming, sorting and searching. **Sorting** a group or sequence of elements or data items means rearranging them in either ascending or descending order depending upon the relationship among the data items present in the group. **Searching** is a programming technique that determines whether an element or a data item is present in a list or not.

Sorting is, without doubt, the most fundamental algorithmic problem. Many different approaches lead to useful sorting algorithms and these ideas can be used to solve many other problems. Finding better algorithms to sort a given set of data is an ongoing problem in the field of computer science. Simple sorting techniques sort data in ascending and descending order. The same algorithm can be used for sorting in increasing or decreasing order but all we need is to change $\le$ to $\ge$ in the comparison algorithm as we desire. In this chapter we will see some sorting techniques and the data is sorted only in ascending order. The factors to be considered while choosing a sorting technique are,

+   - Programming time of the sorting technique.
+   - Execution time of the sorting technique.
+   - Number of comparisons required for sorting the list.
+   - Main or auxiliary memory space needed for the sorting technique.

One reason why sorting is so important is that once a set of items is sorted, many other problems become easy. Speeding up searching is perhaps the most important application of sorting. Once the elements are placed in sorted order in an array, the k$^{th}$ largest element can be found in constant time by simply looking in the k$^{th}$ position of the array.

All data processing requires accessing records efficiently and quickly. Search techniques are most efficient only when the data items are already sorted according to some specified keys. If the list is not sorted, searching a record takes more time when the list is large. Therefore sorting becomes a necessary technique. A sorting method is said to be stable when it has minimum number of swaps i.e., if the two data items of matching value are guaranteed not to be rearranged with respect to each other when the algorithm progresses.