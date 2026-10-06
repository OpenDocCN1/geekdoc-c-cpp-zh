394 — 9 Collections and Their Organization

```
}
}
#endif
```

# 9.3.4 Sequential Search

Sequential search is a basic search method. It scans through the array, and compares each element with the desired one until it finds the match. The search is unsuccessful if there is no element that matches the desired one.

Example 9.14: Sequential search.

```
//9_14.h
#ifndef SEARCH_METHODS
#define SEARCH_METHODS

//Find element with value key in the array list using sequential
//search
//Return the index of the element if found, otherwise return -1
template <class T>
int SeqSearch(T list[], int n, T key)
{
    for(int i=0; i < n; i++)
        if (list[i] == key)
            return i;
    return -1;
}

#endif //SEARCH_METHODS
```

# 9.3.5 Binary Search

We can use binary search if we search a sorted collection. The idea of binary search is that a comparison splits the sequence into two parts of equal size and only one of them can contain the desired one. Figure 9.22 shows the procedure of a binary search.

Example 9.15: Binary search.

```
//9_15.h
#ifndef SEARCH_METHODS
#define SEARCH_METHODS
```