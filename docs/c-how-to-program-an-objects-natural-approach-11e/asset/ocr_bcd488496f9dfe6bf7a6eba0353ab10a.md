ment of data. This comparison is an example of the space–time trade-off: The bucket sort uses more memory than the bubble sort but performs better. This version of the bucket sort requires copying all the data back to the original array on each pass. Another possibility is to create a second two-dimensional bucket array and repeatedly swap the data between the two bucket arrays.

**2.1.8**  *(Recursive Linear Search)* Modify Fig. 21.1 to define a linear search function named `recursiveLinearSearch` that performs a recursive linear search of an array. The function should receive the array, the search key and starting index as arguments. If the search key is found, return its index in the array; otherwise, return −1. Each call to the recursive function should check one element value in the array.

**2.1.9**  *(Recursive Binary Search)* Modify Fig. 21.2 to define a binary search function named `recursiveBinarySearch` that performs a recursive binary search of an array. The function should receive the array, the search key, starting index and ending index as arguments. If the search key is found, return its index in the array. If the search key is not found, return −1.

**2.1.10**  *(Quicksort)* The recursive sorting technique called quicksort uses the following basic algorithm for a one-dimensional array of values:

+   a) **Partitioning Step:** Take the first element of the unsorted array and determine its final location in the sorted array (i.e., all values to the left of the element in the array are less than the element’s value, and all values to the right of the element in the array are greater than the element’s value—we show how to do this below). We now have one value in its proper location and two unsorted sub-arrays.
+   
+   b) **Recursion Step:** Perform the *Partitioning Step* on each unsorted sub-array.

Each time *Step 1* is performed on a sub-array, another element is placed in its final location of the sorted array, and two unsorted sub-arrays are created. When a sub-array consists of one element, it must be sorted; therefore, that element is in its final location.

The basic algorithm seems simple enough, but how do we determine the final position of the first element of each sub-array? As an example, consider the following set of values (the element in bold is the partitioning element—it will be placed in its final location in the sorted array):

**37**  2  6  4  89  8  10  12  68  45

Starting from the rightmost element of the array, compare each element with **37** until an element less than **37** is found. Then swap **37** and that element. The first element less than **37** is 12, so **37** and 12 are swapped. The values now reside in the array as follows:

12  2  6  4  89  8  10  **37**  68  45

Element 12 is in italics to indicate that it was just swapped with **37**.

Starting from the left of the array but beginning with the element after 12, compare each element with **37** until an element greater than **37** is found. Then swap **37** and that element. The first element greater than **37** is 89, so **37** and 89 are swapped. The values now reside in the array as follows:

12  2  6  4  **37**  8  10  *89*  68  45