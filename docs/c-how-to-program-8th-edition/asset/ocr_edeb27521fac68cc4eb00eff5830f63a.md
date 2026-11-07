c) Repeat this process for each subsequent digit position (tens, hundreds, thousands, etc.).

On the second (tens digit) pass, 100 is placed in row 0, 3 is placed in row 0 (because 3 has no tens digit) and 97 is placed in row 9. After the gathering pass, the order of the values in the one-dimensional vector is 100, 3 and 97. On the third (hundreds digit) pass, 100 is placed in row 1, 3 is placed in row 0 and 97 is placed in row 0 (after the 3). After this last gathering pass, the original vector is in sorted order.

Note that the two-dimensional vector of buckets is 10 times the length of the integer vector being sorted. This sorting technique provides better performance than a bubble sort, but requires much more memory—the bubble sort requires space for only one additional element of data. This comparison is an example of the space-time trade-off: The bucket sort uses more memory than the bubble sort, but performs better. This version of the bucket sort requires copying all the data back to the original vector on each pass. Another possibility is to create a second two-dimensional bucket vector and repeatedly swap the data between the two bucket vectors.

# **19.8 (Recursive Linear Search)**

Modify Exercise 7.33 to use recursive function `recursiveLinearSearch` to perform a linear search of the vector. The function should receive the search key and starting index as arguments. If the search key is found, return its index in the vector; otherwise, return −1. Each call to the recursive function should check one element value in the vector.

# **19.9 (Recursive Binary Search)**

Modify Fig. 19.3 to use recursive function `recursiveBinarySearch` to perform a binary search of the vector. The function should receive the search key, starting index and ending index as arguments. If the search key is found, return its index in the vector. If the search key is not found, return −1.

# **19.10 (Quicksort)**

The recursive sorting technique called quicksort uses the following basic algorithm for a one-dimensional vector of values:

+   a) **Partitioning Step:** Take the first element of the unsorted vector and determine its final location in the sorted vector (i.e., all values to the left of the element in the vector are less than the element’s value, and all values to the right of the element in the vector are greater than the element’s value—show how to do this below). We now have one value in its proper location and two unsorted subvectors.

+   b) **Recursion Step:** Perform the *Partitioning Step* on each unsorted subvector. Each time the *Partitioning Step* is performed on a subvector, another value is placed in its final location of the sorted vector, and two unsorted subvectors are created. When a subvector consists of one element, that element’s value is in its final location (because a one-element vector is already sorted).

The basic algorithm seems simple enough, but how do we determine the final position of the first element value of each subvector? As an example, consider the following set of values (the value in bold is for the partitioning element—it will be placed in its final location in the sorted vector):

37  2  6  4  89  8  10  12  68  45

Starting from the rightmost element of the vector, compare each element value with 37 until an element value less than 37 is found; then swap 37 and that element’s value. The first element value less than 37 is 12, so 37 and 12 are swapped. The new vector is

12  2  6  4  89  8  10  37  68  45

Element value 12 is in italics to indicate that it was just swapped with 37.

Starting from the left of the vector, but beginning with the element value after 12, compare each element value with 37 until an element value greater than 37 is found—then swap 37 and that element value. The first element value greater than 37 is 89, so 37 and 89 are swapped. The new vector is

12  2  6  4  37  8  10  89  68  45