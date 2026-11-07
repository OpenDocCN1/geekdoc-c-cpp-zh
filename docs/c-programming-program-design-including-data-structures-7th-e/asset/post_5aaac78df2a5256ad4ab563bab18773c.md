
> **NOTE** The sequential search algorithm, as given here, uses an iterative control structure (the `while` loop) to compare the search item with the list elements. You can also write a recursive algorithm to implement the sequential search algorithm. (See Programming Exercise 1 at the end of this chapter.)

## SEQUENTIAL SEARCH ANALYSIS

This section analyzes the performance of the sequential search algorithm in both the worst case and the average case.

The statements before and after the loop are executed only once and hence require very little computer time. The statements in the `while` loop are the ones that are repeated several times. For each iteration of the loop, the search item is compared with an element in the list, and a few other statements are executed, including some other comparisons. Clearly, the loop terminates as soon as the search item is found in the list. Therefore, execution of the other statements in the loop is directly related to the outcome of the key comparison. Also, different programmers might implement the same algorithm differently, although the number of key comparisons would typically be the same. The speed of a computer can also easily affect the time an algorithm takes to perform, but it, of course, does not affect the number of key comparisons required.

Therefore, when analyzing a search algorithm, we count the number of key comparisons because this number gives us the most useful information. Furthermore, the criteria for counting the number of key comparisons can be applied equally well to other search algorithms.

Suppose that L is a list of length n. We want to determine the number of key comparisons made by the sequential search when the list L is searched for a given item.

If the search item is not in the list, we then compare the search item with every element in the list, making n comparisons. This is an unsuccessful case.

Suppose that the search item is in the list. Then, the number of key comparisons depends on where in the list the search item is located. If the search item is the first element of L, we make only one key comparison. This is the best case. On the other hand, if the search item is the last element in the list, the algorithm makes n comparisons. This is the worst case. The best and worst cases are not likely to occur every time we apply the sequential search. In a list, it would be more helpful if we could determine the average behavior of the algorithm. That is, we need to determine the average number of key comparisons the sequential search algorithm makes in the successful case.

To determine the average number of comparisons in the successful case of the sequential search algorithm:

- 1. Consider all possible cases.
- 2. Find the number of comparisons for each case.
- 3. Add the number of comparisons and divide by the number of cases.

If the search item, called the *target*, is the first element in the list, one comparison is required. If the target is the second element in the list, two comparisons are required. Similarly, if the target is the *k*th element in the list, *k* comparisons are required. We assume that the target can be any element in the list; that is, all list elements are equally likely to be the target. Suppose that there are *n* elements in the list. The following expression gives the average number of comparisons:

$$\frac{1+2+\cdots+n}{n}$$

It is known that:

$$1+2+\cdots+n=\frac{n(n+1)}{2}.$$

Therefore, the following expression gives the average number of comparisons made by the sequential search in the successful case:

$$\frac{1+2+\cdots+n}{n}=\frac{1}{n}\frac{n(n+1)}{2}=\frac{n+1}{2}.$$

This expression shows that, on average, a successful sequential search searches half of the list. It thus follows that if the list size is 1,000,000, on average, the sequential search makes 500,000 comparisons. As a result, the sequential search is not efficient for large lists.

## Binary Search

As you can see, the sequential search is not efficient for large lists because, on average, it searches half the list. We, therefore, describe another search algorithm called the **binary search**, which is very fast. However, a binary search can be performed only on sorted lists. We, therefore, assume that the list is sorted. Later in this chapter, we will describe several sorting algorithms.

The binary search algorithm uses the “divide and conquer” technique to search the list. First, the search item is compared with the middle element of the list. If the search item is less than the middle element of the list, we restrict the search to the first half of the list; otherwise, we search the second half of the list.

Consider the sorted list of `length = 12` in Figure 18-1.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1320_0.png)

**FIGURE 18-1** List of length 12

Suppose that we want to determine whether 75 is in the list. Initially, the entire list is the search list (see Figure 18-2).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1320_1.png)

**FIGURE 18-2** Search list, `list[0]...list[11]`

First, we compare 75 with the middle element in this list, `list[5]` (which is 39). Because 75 ≠ `list[5]` and 75 > `list[5]`, we then restrict our search to the list `list[6]...list[11]`, as shown in Figure 18-3.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1320_2.png)

**FIGURE 18-3** Search list, `list[6]...list[11]`

This process is now repeated on the list `list[6]...list[11]`, which is a list of length = 6.

Because we need to determine the middle element of the list frequently, the binary search algorithm is typically implemented for array-based lists. To determine the middle element of the list, we add the starting index, first, and the ending index, last, of the search list and then divide by 2 to calculate its index. That is:

$$\mathrm{mid} = \frac{\mathrm{first} + \mathrm{last}}{2}$$

Initially, `first = 0` and `last = length - 1` (this is because an array index in C++ starts at 0, and length denotes the number of elements in the list).

The following C++ function implements the binary search algorithm. If the item is found in the list, its location is returned; if the search item is not in the list, -1 is returned.

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

In the binary search algorithm, each time through the loop, we make two key comparisons. The only exception is in the successful case; the last time through the loop, only one key comparison is made.

> **NOTE** The binary search algorithm, as given in this chapter, uses an iterative control structure (the `while` loop) to compare the search item with the list elements. You can also write a recursive algorithm to implement the binary search algorithm. (See Programming Exercise 2 at the end of this chapter.)

Example 18-1 further illustrates how the binary search algorithm works.

### EXAMPLE 18-1

Consider the list given in Figure 18-4.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1322_0.png)

**FIGURE 18-4** Sorted list for a binary search

The size of this list is 12; that is, the length is 12. Suppose that we are searching for item 89. Table 18-1 shows the values of `first`, `last`, and `mid` each time through the loop. It also shows the number of times the item is compared with an element in the list each time through the loop.

### **TABLE 18-1** Values of `first`, `last`, and `mid` and the Number of Comparisons for Search Item 89

| Iteration | `first` | `last` | `mid` | `list[mid]` | Number of comparisons |
|---:|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 5 | 39 | 2 |
| 2 | 6 | 11 | 8 | 66 | 2 |
| 3 | 9 | 11 | 10 | 89 | 1 (found is `true`) |

The item is found at location 10, and the total number of comparisons is 5.

Next, let us search the list for item 34. Table 18-2 shows the values of `first`, `last`, and `mid` each time through the loop. It also shows the number of times the item is compared with an element in the list each time through the loop.
