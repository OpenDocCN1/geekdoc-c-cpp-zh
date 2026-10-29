# Display 5.5 Partially Filled Array (part 3 of 3)

```
63   for (int index = 0; index < numberUsed; index++)
64     cout << a[index] << " differs from average by "
65         << (a[index] - average) << endl;
66   }
```

# SAMPLE DIALOGUE

This program reads golf scores and shows how much each differs from the average.
Enter golf scores:
Enter up to 10 nonnegative whole numbers.
Mark the end of the list with a negative number.
69 74 68 -1
Average of the 3 scores = 70.3333
The scores are:
69 differs from average by -1.33333
74 differs from average by 3.66667
68 differs from average by -2.33333

# Example SEARCHING AN ARRAY

A common programming task is to search an array for a given value. For example, the array may contain the student numbers for all students in a given course. To tell whether a particular student is enrolled, the array is searched to see if it contains the student's number. The simple program in Display 5.6 fills an array and then searches the array for values specified by the user. A real application program would be much more elaborate, but this shows all the essentials of the sequential search algorithm you could imagine: The program looks at the array elements in order, first to last, to see if the target number is equal to any of the array elements.

In Display 5.6 the function search is used to search the array. When searching an array, you often want to know more than simply whether or not the target value is in the array. If the target value is in the array, you often want to know the index of the indexed variable holding that target value, since the index may serve as a guide to some additional information about the target value. Therefore, we designed the function search to return an index giving the location of the target value in the array, provided the target value is, in fact, in the array. If the target value is not in the array, search returns -1. Let's look at the function search in a little more detail.

The function search uses a while loop to check the array elements one after the other to see whether any of them equals the target value. The variable found is used as a flag to record whether or not the target element has been found. If the target element is found in the array, found is set to true, which in turn ends the while loop.

sequential search