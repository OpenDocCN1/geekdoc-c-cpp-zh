Chapter 9 introduced arrays, a structured data type. When the data values are all of the same type, arrays are a convenient way to store and process them. You can effectively use loops for input/output, initialization, and other operations. Moreover, you can pass the entire set of values as a parameter with a single statement. The next section continues our discussion of one-dimensional arrays and shows you how to use them effectively for list processing. We then examine the vector type.

# List Processing

A list is a collection of values of the same type. Because all values are of the same type, a convenient place to store a list is in an array and, particularly, in a one-dimensional array. The size of a list is the number of elements in the list. Because the size of a list can increase and decrease, the array you use to store the list should be declared as the maximum size of the list.

Basic operations performed on a list include the following:

+   - Search the list for a given item.
+   - Sort the list.
+   - Insert an item in the list.
+   - Delete an item from the list.
+   - Print the list.

The following sections discuss searching and sorting algorithms.

# Searching

In Chapter 9, we described the sequential search algorithm. Recall that the sequential search algorithm is:

```
```cpp
int seqSearch(const int list[], int listLength, int searchItem)
{
    int loc;
    bool found = false;
    loc = 0;

    while (loc < listLength && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;

}
```
```