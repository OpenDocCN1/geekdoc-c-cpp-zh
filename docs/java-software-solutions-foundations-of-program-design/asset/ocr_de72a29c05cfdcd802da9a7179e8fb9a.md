# Insertion Sort

The Sorting class also contains a method that performs an insertion sort on an array of Comparable objects. If used to sort the array of Contact objects in the PhoneList program, it would produce the same results as the selection sort did. However, the logic used to put the objects in order is different.

The insertion sort algorithm sorts a list of values by repetitively inserting a particular value into a subset of the list that has already been sorted. One at a time, each unsorted element is inserted at the appropriate position in that sorted subset until the entire list is in order.

The general strategy of insertion sort is: Begin with a “sorted” list containing only one value. Sort the first two values in the list relative to each other by exchanging them if necessary. Insert the list’s third value into the appropriate position relative to the first two (sorted) values. Then insert the fourth value into its proper position relative to the first three values in the list. Each time an insertion is made, the number of values in the sorted subset increases by one. Continue this process until all values are inserted in their proper places, at which point the list is completely sorted.

The insertion process requires that the other values in the array shift to make room for the inserted element. Figure 10.3 demonstrates the behavior of the insertion sort algorithm with integers.

![](bbox=[0.08, 0.62, 0.88, 0.88])

FIGURE 10.3 Insertion sort processing