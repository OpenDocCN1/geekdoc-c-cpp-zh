or greater than zero if the executing object is less than, equal to, or greater than the object to which it is being compared, respectively.

# SR 10.13

The sequence of changes the selection sort algorithm makes to the list of numbers is:

5 7 1 8 2 4 3
1 7 5 8 2 4 3
1 2 5 8 7 4 3
1 2 3 8 7 4 5
1 2 3 4 7 8 5
1 2 3 4 5 8 7
1 2 3 4 5 7 8

# SR 10.14

The sequence of changes the insertion sort algorithm makes to the list of numbers is:

5 7 1 8 2 4 3
5 7 1 8 2 4 3
1 5 7 8 2 4 3
1 5 7 8 2 4 3
1 2 5 7 8 4 3
1 2 4 5 7 8 3
1 2 3 4 5 7 8

# SR 10.15

The sorting methods in this chapter all operate on an array of Comparable objects. So the sorting method doesn’t really “know” what the objects are, other than that they are comparable and therefore have a compareTo method that can be invoked.

# SR 10.16

Selection sort and insertion sort are generally equivalent in efficiency, because they both take about n² number of comparisons to sort a list of n numbers. Selection sort, though, generally makes fewer swaps. Several sorting algorithms are more efficient than either of these.

# 10.5 Searching

# SR 10.17

a. 4, b. 1, c. 15, d. 15

# SR 10.18

A binary search assumes that the search pool is already sorted and begins by examining the middle element. Assuming the target is not found, approximately half of the data is eliminated as viable candidates. Then, the middle element of the remaining candidates is examined, eliminating another quarter of the data. This process continues until the element is found or all viable data has been examined.

# SR 10.19

a. 1, b. 3, c. 4, d. 4