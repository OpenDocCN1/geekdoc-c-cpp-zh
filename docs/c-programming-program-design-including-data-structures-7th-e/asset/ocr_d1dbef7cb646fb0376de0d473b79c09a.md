Initially, `first = 0` and `last = length - 1` (this is because an array index in C++ starts at 0, and length denotes the number of elements in the list).

The following C++ function implements the binary search algorithm. If the item is found in the list, its location is returned; if the search item is not in the list, -1 is returned.

```
```cpp
template <class elemType>
int binarySearch(const elemType list[], int length,
                const elemType& item)
{
    int first = 0;
    int last = length - 1;
    int mid;

    bool found = false;

    while (first <= last && !found)
    {
        mid = (first + last) / 2;

        if (list[mid] == item)
            found = true;
        else if (list[mid] > item)
            last = mid - 1;
        else
            first = mid + 1;
    }

    if (found)
        return mid;
    else
        return -1;
} //end binarySearch
```
```

In the binary search algorithm, each time through the loop, we make two key comparisons. The only exception is in the successful case; the last time through the loop, only one key comparison is made.

> **NOTE** The binary search algorithm, as given in this chapter, uses an iterative control structure (the `while` loop) to compare the search item with the list elements. You can also write a recursive algorithm to implement the binary search algorithm. (See Programming Exercise 2 at the end of this chapter.)

Example 18–1 further illustrates how the binary search algorithm works.