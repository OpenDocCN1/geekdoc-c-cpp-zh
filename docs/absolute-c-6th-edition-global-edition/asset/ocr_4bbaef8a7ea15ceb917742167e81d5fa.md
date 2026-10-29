# Programming Projects

+   1. Write a template version of the iterative binary search algorithm from Display 13.8 which only searches an array of integers for an integer key. Specify requirements on the template parameter type. Discuss the requirements on the template parameter type.

+   2. Write a template version of the recursive binary search function from Display 13.6. Specify requirements on the template parameter type. Discuss the requirements on the template parameter type.

+   3. The template sort routine in Display 16.3 is based on an algorithm called the selection sort. Another related sorting algorithm is called insertion sort. The insertion sort algorithm is the sort method often used to sort a Bridge hand. Consider each element in turn, inserting it into its proper place among the elements at the start of the array that are already sorted. The element being considered is inserted by moving the larger elements "to the right" to make space and inserting the vacated place. For example, the following shows the steps in a selection sort of an array of ints a. The values of a[0] through a[4] are given on each line. The asterisk marks the boundary between the sorted and unsorted portions of the array.

```
2 * 5 3 4
2 5 * 3 4
2 3 5 * 4
2 3 4 5 *
```

First, write an insertion sort function that works for ints. Next, write the template version of this sort function. Finally, test thoroughly using several primitive types, using a type you create with the minimal machinery necessary to use the sort routine.

+   4. Write a template-based function that takes two parameters and checks whether the two are identical. The function should operate with any numeric data types (e.g., float, int, double, char)

+   5. Write a template-based class that implements a set of items. The class should allow the user to
+   
+   a. Add a new item to the set.
+   
+   b. Get the number of items in the set.
+   
+   c. Get a pointer to a dynamically created array containing each item in the set. The caller of this function is responsible for deallocating the memory.
+   
+   Test your class by creating sets of different data types (e.g., integers, strings).

+   6. Do Programming Project 10.6 for the wrapper class around a dynamic array of strings that allowed for the deletion and addition of string entries. Except this time, use a template-based class so the implementation is not limited to strings. Test the class with dynamic arrays of integers in addition to strings.