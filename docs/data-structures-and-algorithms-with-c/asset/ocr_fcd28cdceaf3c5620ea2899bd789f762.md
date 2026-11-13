# # SEARCHING AND SORTING

> > "You think you know when you learn, are more sure when you can write, even more when you can teach, but certain when you can program." -Alan J. Perlis

+   **KEY FEATURES**
+   - Linear Search
+   - Binary Search
+   - Interpolation Search
+   - Bubble Sort
+   - Selection Sort
+   - Insertion Sort
+   - Quick Sort
+   - Merge Sort
+   - Shell Sort
+   - Heap Sort

Searching for items and sorting through items are tasks that we do everyday. We search for all occurrences of a word in a file in order to replace it with another word. We sort the items on a list into alphabetical or numerical order. Searching and sorting are also most common operations in computer programs.

# ## SEARCHING

Searching refers to the operation of finding the location of the desired key element within some data structures. Data structures can include linked lists, arrays, search trees or hash tables. The search is successful if the item is found, and then returns its location; otherwise, the search is unsuccessful. The appropriate search algorithm often depends on the data structure being searched.

+   - Linear Search
+   - Binary Search
+   - Interpolation Search

# ### Linear Search

Linear search, or sequential search is a method for finding the position of a particular key value in a list, where the search starts from beginning of the list and checking every element, one at a time in sequence until the desired key is found or the end of the list is reached.

# #### Algorithm of Linear Search

```
Algorithm: LINEAR_SEARCH (A, N, KEY, LOC)
{A is an array of N elements, Key is the searching key}
1. Set I = 0
2. Repeat while I < N and A[I] # KEY
   Set I = I + 1
   [End of loop]
3. If I < N then Set LOC = I
   ELSE LOC = -1
4. Return
```