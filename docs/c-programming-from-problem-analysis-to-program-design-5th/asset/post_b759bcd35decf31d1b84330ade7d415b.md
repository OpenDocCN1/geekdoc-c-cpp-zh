
the list, we add the starting index, **first**, and the ending index, **last**, of the search list and then divide by 2 to calculate its index. That is, \(mid = \frac{first + last}{2}\). Initially, `first = 0` and (since array index in C++ starts at 0 and `listLength` denotes the number of elements in the list) `last = listLength - 1`. (Note that the formula for calculating the middle element works regardless of whether the list has an even or odd number of elements.)

The following C++ function implements the binary search algorithm. If the item is found in the list, its location is returned. If the search item is not in the list, −1 is returned.

```cpp
int binarySearch(const int list[], int listLength, int searchItem)
{
    int first = 0;
    int last = listLength - 1;
    int mid;

    bool found = false;

    while (first <= last && !found)
    {
        mid = (first + last) / 2;

        if (list[mid] == searchItem)
            found = true;
        else if (list[mid] > searchItem)
            last = mid - 1;
        else
            first = mid + 1;
    }

    if (found)
        return mid;
    else
        return -1;
} // end binarySearch
```

Note that in the binary search algorithm, two key (item) comparisons are made each time through the loop, except in the successful case—the last time through the loop—when only one key comparison is made.

Next, we walk through the binary search algorithm on the list shown in Figure 10-19.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_618_0.png)

**FIGURE 10-19**  Sorted list for a binary search

The size of the list in Figure 10-19 is 12, so `listLength = 12`. Suppose that the item for which we are searching is 89, so `searchItem = 89`. Before the while loop executes, first = 0, last = 11, and found = false. In the following, we trace the execution of the while loop, showing the values of first, last, and mid and the number of key comparisons during each iteration.

| Iteration | first | last | mid | list[mid] | No. of key comparisons |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 6 | 11 | 8 | 66 | 2 |
| 3 | 9 | 11 | 10 | 89 | 1 (found is true) |

The item is found at location 10, and the total number of key comparisons is 5.

Next, let’s search the list for 34, so searchItem = 34. Before the while loop executes, first = 0, last = 11, and found = false. In the following, as before, we trace the execution of the while loop, showing the values of first, last, and mid and the number of key comparisons during each iteration.

| Iteration | first | last | mid | list[mid] | No. of key comparisons |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 4 | 4 | 4 | 34 | 1 (found is true) |

The item is found at location 4, and the total number of key comparisons is 7.

Let’s now search for 22, so searchItem = 22. Before the while loop executes, first = 0, last = 11, and found = false. In the following, as before, we trace the execution of the while loop, showing the values of first, last, and mid and the number of key comparisons during each iteration.

| Iteration | first | last | mid | list[mid] | No. of key comparisons |
|---|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 0 | 4 | 2 | 19 | 2 |
| 3 | 3 | 4 | 3 | 25 | 2 |
| 4 | 3 | 2 |  |  | the loop stops (since first > last); unsuccessful search |

This is an unsuccessful search. The total number of key comparisons is 6.

From these tracings of the binary search algorithm, you can see that every time you go through the loop, you cut the size of the sublist by half. That is, the size of the sublist you search the next time through the loop is half the size of the previous sublist.

We leave it as an exercise for you to write a program to test the function binarySearch. See Programming Exercise 2 at the end of this chapter.

## Performance of Binary Search

Suppose that L is a sorted list of size 1024, and we want to determine whether an item x is in L. From the binary search algorithm, it follows that every iteration of the while loop cuts the size of the search list by half. (For example, see Figures 10-17 and 10-18.) Because 1024 = 2^{10}, the while loop will have, at most, 11 iterations to determine whether x is in L. Because every iteration of the while loop makes two item (key) comparisons, that is, x is compared twice with the elements of L, the binary search will make, at most, 22 comparisons to determine whether x is in L. On the other hand, recall that a sequential search, on average, will make 512 comparisons to determine whether x is in L.

To better understand how fast binary search is compared to sequential search, suppose that L is of size 1048576. Because 1048576 = 2^{20}, it follows that the while loop in a binary search will have, at most, 21 iterations to determine whether an element is in L. Every iteration of the while loop makes two key (that is, item) comparisons. Therefore, to determine whether an element is in L, a binary search makes, at most, 42 item comparisons.

Note that 40 = 2 * 20 = 2 * log_2(2^{20}) = 2 * log_2(1048576).

In general, suppose that L is a sorted list of size n. Moreover, suppose that n is a power of 2, that is, n = 2^m, for some nonnegative integer m. After each iteration of the while loop, about half of the elements are left to search, that is, the search sublist for the next iteration is half the size of the current sublist. For example, after the first iteration, the search sublist is of size about n/2 = 2^{m-1}. It is easy to see that the maximum number of the iteration of the while loop is about m + 1. Also m = log_2n. Each iteration makes two key comparisons. Thus, the maximum number of comparisons to determine whether an element x is in L is 2(m + 1) = 2(log_2n + 1) = 2log_2n + 2.

## vector Type (class)

> NOTE This section may be skipped without any discontinuation.

Chapter 9 and the previous sections of this chapter described how arrays can be used to implement and process lists. One of the limitations of arrays discussed so far is that once you create an array, its size remains fixed. This means that only a fixed number of elements can be stored in an array. Also, inserting an element in the array at a specific position could require the elements of the array to be shifted. Similarly, removing an element from the array also could require shifting the elements of the array, as we typically do not leave empty positions between array positions holding some data. Typically, empty array positions are at the end.

In addition to arrays, C++ provides the vector type (most commonly called the class vector) to implement a list. A variable declared using the vector type is called a vector container (or a vector, a vector object, or simply an object). Unlike an array, the size of a vector object can grow and shrink during program execution. Therefore, you do not need to be concerned with the number of data elements.

When you declare a vector object, you must specify the type of the element the vector object stores. Table 10-1 describes various ways a vector object can be declared.

**TABLE 10-1** Various Ways to Declare and Initialize a vector Object

| Statement | Effect |
|---|---|
| `vector<elemType> vecList;` | Creates the empty vector object vecList without any elements. |
| `vector<elemType> vecList(otherVecList);` | Creates the vector object vecList and initializes vecList to the elements of vector otherVecList. vecList and otherVecList are of the same type. |
| `vector<elemType> vecList(size);` | Creates the vector object vecList of size size. vecList is initialized using the default values. |
| `vector<elemType> vecList(n, elem);` | Creates the vector object vecList of size n. vecList is initialized using n copies of the element elem. |

In Table 10-1, elemType specifies the data type of the element to be stored in vecList.

### EXAMPLE 10-3

- a. The following statement declares intList to be an empty vector object, and the element type is `int`.

```cpp
vector<int> intList;
```

- b. The following statement declares intList to be a vector object of size 10, and the element type is `int`. The elements of intList are initialized to 0.

```cpp
vector<int> intList(10);
```
