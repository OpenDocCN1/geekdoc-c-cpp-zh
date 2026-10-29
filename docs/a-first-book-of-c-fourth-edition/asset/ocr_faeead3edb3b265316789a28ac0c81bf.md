receives direct access to the original array, not a copy of the array elements. A parameter must be declared in the called function to receive the passed array name. The declaration of the parameter can omit the array's row size for both one- and two-dimensional arrays.

# 7.7 Chapter Supplement: Searching and Sorting Methods

Most programmers encounter the need to both sort and search a list of data items at some time in their programming careers. For example, you might have to arrange experiment results in increasing (ascending) or decreasing (descending) order for statistical analysis or sort a list of names in alphabetical order and search this list to find a particular name. Similarly, you might have to arrange a list of dates in ascending or descending order and search this list to locate a certain date. This section introduces the fundamentals of sorting and searching lists. Note that sorting a list before searching it isn't necessary, although much faster searches are possible if the list is in sorted order, as you'll see.

# Search Algorithms

A common requirement of many programs is searching a list for a given element. For example, in a list of names and phone numbers, you might search for a specific name so that the corresponding phone number can be printed, or you might need to search the list simply to determine whether a name is there. The two most common methods of performing these searches are the linear and binary search algorithms.

# Linear Search

In a linear search, also known as a sequential search, each item in the list is examined in the order in which it occurs until the desired item is found or the end of the list is reached. This search method is analogous to looking at every name in the phone directory, beginning with Aardvark, Aaron, until you find the one you want or until you reach Zzxgy, Zora. Obviously, it's not the most efficient way to search a long alphabetized list. However, a linear search has these advantages:

+   - The algorithm is simple.
+   - The list need not be in any particular order.

In a linear search, the search begins at the first item in the list and continues sequentially, item by item, through the list. The pseudocode for a function performing a linear search is as follows:

```
For all items in the list
  Compare the item with the desired item
  If the item is found
    Return the index value of the current item
  EndIf
EndFor
Return -1 if the item is not found
```