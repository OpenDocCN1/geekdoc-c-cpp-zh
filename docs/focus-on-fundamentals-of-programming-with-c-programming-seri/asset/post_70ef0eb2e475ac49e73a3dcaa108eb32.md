
Here's the output that's produced:

```c
Before sort
30567 35439 21431 9013 3992 28690 24735 8148 14330 24847
43747 10518 46366 40111 33228 46127 27945 8870 45536 21664
35024 10674 27724 16905 30488 19128 32991 3856 21268 45855
26816 803 39397 3986 44341 47219 33125 48655 36237 4323
10188 33574 48866 45132 16189 3823 6746 9497 32622 16402
8430 46630 1113 5271 47490 13727 7493 40531 46342 47608
30989 49988 14230 3472 48785 9291 900 26877 24400 17550
27638 19251 14013 41336 14304 39437 43991 30229 35682 654
41083 27520 47042 26948 47726 41156 27658 33215 15557 44269
2529 24729 16662 11997 9825 28596 25245 35327 7047 41915
After sort
654 803 900 1113 2529 3472 3823 3856 3986 3992
4323 5271 6746 7047 7493 8148 8430 8870 9013 9291
9497 9825 10188 10518 10674 11997 13727 14013 14230 14304
14330 15557 16189 16402 16662 16905 17550 19128 19251 21268
21431 21664 24400 24729 24735 24847 25245 26816 26877 26948
27520 27638 27658 27724 27945 28596 28690 30229 30488 30567
30989 32622 32991 33125 33228 33574 35024 35327 35439
35682 36237 39397 39437 40111 40531 41083 41156 41336 41915
43747 43991 44269 44341 45132 45536 45855 46127 46342 46366
46630 47042 47219 47490 47608 47726 48655 48785 48866 49988
```

Note that the array is sorted in increasing order, as defined by the comparison function. To sort an array in decreasing order, reverse the sense of "greater than" and "less than" in the comparison function.

Even if you are not using a primitive C data type, `qsort()` will work just fine as long as you know enough about the data representation to tell whether one item is "smaller" than another.

In the case of strings, the standard library function `strcmp()` is perfectly suited for use with `qsort()` in the compare function.

```c
// compare2.c
int compare(const void *p, const void *q) {
    return strcmp((char *) p, (char *) q);
}
```

Here's a program that sorts strings with `qsort()`:

```c
// qsort2.c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int compare(const void *p, const void *q);

int main() {
    char list[5][4] = {{"cat", "car", "cab", "cap", "can"}};
    qsort(list, 5, sizeof(list[0]), compare);
    for (i = 0; i < 5; ++i) {
        printf("%s ", list[i]);
    }
    return(0);
}

int compare(const void *p, const void *q) {
    return strcmp((char *) p, (char *) q);
}
```

## Searching an Array: Linear Search

The simplest search strategy is the linear or sequential search. The linear search is usually performed on unordered arrays. It starts at the beginning of the array, checks every element in order, until it either finds the data item it is looking for or until it reaches the end of the array, in which case the data item is not found in the array.

```c
// linearSearch.c
// returns the index in the array of data item found
// returns -1 if data item not in array
int linearSearch(int num[], int max, int key) {
   int i;
   for (i = 0; i < max; ++i) {
      if (num[i] == key) {
         return i;
      }
   }
   return -1;
}
```

Let's examine how long it will take to find a data item matching a key in the unsorted array. We can examine three different possibilities, average time, worst-case time, or best possible time. However, we will generally be most concerned with the worst-case time, as calculations based on worst-case times can lead to guaranteed performance predictions. Conveniently, the worst-case times are generally easier to calculate than average times.

To simplify analysis and comparison of algorithms, we look for a dominant operation and count the number of times that dominant operation has to be performed. In the case of searching, the dominant operation is the comparison.

If there are max items in our array, it is obvious that in the worst case when there is no item in the array with the desired key, then max comparisons of the key with the data items in the array will have to be made. In the best case we'll find our data item on the first comparison. In the average case we'll find our data item in (1 + max) / 2 comparisons or approximately max/2 comparisons.

Therefore, an array of 100 data items requires an average of 50 comparisons for a successful search. If we were to double the number of data items we had to search through, the number of comparisons would also double and therefore the run-time of our algorithm would double. We say that the number of comparisons is proportional to the number of data items n in the array. Accordingly, the search time of the algorithm is proportional to the number of data items max in the array. An array of 1000 data items takes 10 times longer to search than an array of 100 data items.

![](img/3a848cfa6d95e726766ad07c3ec2474a_293_0.png)

## Searching an Array: Binary Search

As we saw earlier, the linear search algorithm is simple and convenient for small problems, but if the array is large and/or requires many repeated searches, it makes good sense to have a more efficient algorithm for searching an array.

The binary search algorithm works on a sorted array. It selects the median (middle) element in the array and compares its value to that of the target value, key. Because the array is known to be sorted, if the target value is less than the middle value then the target must be in the first half of the array. Likewise if the value of the target item is greater than that of the middle value in the array, it is known that the target lies in the second half of the array. In either case we can, in effect, “throw out” one half of the search space with only one comparison.

Now, knowing that the target must be in one half of the array or the other, the binary search examines the median value of the half in which the target must reside. The algorithm thus narrows the search area by half at each step until it has either found the target data or the search fails.

The algorithm is easy to remember if you think about a child’s guessing game. Imagine I told you that I am. You would continue to refine your choice until you got the number correct.

Given a sorted array of items, say:

| Index | 0 | 1 | 2 | 3 | 4 | 5 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Value | 12 | 29 | 30 | 32 | 35 | 49 |
| low index | | | | | | high index |

Suppose we wish to search for the position of an element equal to key. We will search the array that begins at some low index and ends at some high index. In our case the low index of the effective array to be searched is 0 and the high index is 5. We can find the approximate midway index by integer division (low + high) / 2, i.e. 2. We compare our value, key with the element at index 2. If they are equal, we have found what we were looking for; the index is 2.
Otherwise, if key is greater than the item at this index, our new effective search array has a low index value of 3 and the high index remains unchanged at 5. If key is less than the element, the new effective search array has a high index of 1 and the low index remains at 0. The process repeats until the item is found, or there are no elements in the effective search array. The terminating condition is found when the low index exceeds the high index.

The binary search algorithm is implemented below:

```c
// binarySearch.c

// Assumes array is in sorted order.
// Returns index of the location of the key in the array.
// Returns -1 if not found.

int binarySearch(int num[], int n, int key) {
    int mid, i, j;

    i = 0;
    j = n-1;
    while (i <= j) {
        mid = (i + j) / 2;
        if (num[mid] > key) {
            j = mid - 1;
        }
        else if (num[mid] < key) {
            i = mid + 1;
        }
        else {
            return mid;
        }
    }
    return -1;
}
```

## Analysis of Binary Search

Why use a binary search when a linear search is easier to code? The answer lies in the efficiency of the search. With a linear search, if you double the size of an array, you could potentially take twice as much time to find an item. With a binary search, doubling the size of the array merely adds one more item to look at. Each time you look with a binary search, you eliminate half of the remaining array items as possible matches.

For example, suppose we're given a search space of 1,000,000 data elements. Sequential search would take about 500,000 searches or comparisons on the
