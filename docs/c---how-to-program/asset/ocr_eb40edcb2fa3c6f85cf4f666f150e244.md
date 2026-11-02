The binary search algorithm eliminates from consideration **one-half** of the elements in a sorted array after each comparison. The algorithm locates the **middle** element of the array and compares it to the search key. If they’re equal, the search key is found and the array index of that element is returned. If they’re not equal, the problem is reduced to searching **one-half** of the array. If the search key is less than the middle element of the array, the algorithm searches the **first half** of the array, otherwise the algorithm searches the **second half**. If the search key is not the middle element in the specified subarray (piece of the original array), the algorithm repeats on one-quarter of the original array. The search continues until the search key is equal to the middle element of a subarray, or until the subarray consists of one element that’s not equal to the search key (i.e., the search key is not found).

In a worst case-scenario, searching a sorted array of 1023 elements takes **only** 10 comparisons using a binary search. Repeatedly dividing 1,024 by 2 yields the values 512, 256, 128, 64, 32, 16, 8, 4, 2 and 1. The number 1,024 (2¹⁰) is divided by 2 only 10 times to get the value 1. Dividing by 2 is equivalent to one comparison in the binary search algorithm. An array of 1,048,576 (2²⁰) elements takes a maximum of **only 20** comparisons to find the search key. A sorted array of one billion elements takes a maximum of **only 30** comparisons to find the search key. This is a tremendous increase in performance over a linear search of a sorted array, which requires comparing the search key to an average of half of the array elements. For a one-billion-element array, this is a difference between an average of 500 million comparisons and a maximum of 30 comparisons! The maximum comparisons for any array can be determined by finding the first power of 2 greater than the number of array elements.

Figure 6.19 presents the *iterative* version of function `binarySearch` (lines 40–68). The function receives four arguments—an integer array `b` to be searched, an integer `searchKey`, the low array index and the high array index (these define the portion of the array to be searched). If the search key does *not* match the middle element of a subarray, the low index or high index is modified so that a smaller subarray can be searched. If the search key is *less than* the middle element, the high index is set to `middle - 1` and the search is continued on the elements from low to middle - 1. If the search key is *greater than* the middle element, the low index is set to `middle + 1` and the search is continued on the elements from middle + 1 to high. The program uses an array of 15 elements. The first power of 2 greater than the number of elements in this array is 16 (2⁴), so no more than 4 comparisons are required to find the search key. The program uses an auxiliary function `printHeader` (lines 71–88) to output the array indices and function `printRow` (lines 92–110) to output each subarray during the binary search process. The middle element in each subarray is marked with an asterisk (*) to indicate the element to which the search key is compared.

```
```c
// Fig. 6.19: fig06_19.c
// Binary search of a sorted array.
#include <stdio.h>
#define SIZE 15

// function prototypes
size_t binarySearch(const int b[], int searchKey, size_t low, size_t high);
```
```

**Fig. 6.19** | Binary search of a sorted array. (Part 1 of 4).