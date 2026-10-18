# DISPLAY 7.11  Selection Sort

![](bbox=[0.243, 0.126, 0.858, 0.556])

As the sorting proceeds, the beginning array elements are set equal to the correct sorted values. The sorted portion of the array grows by adding elements one after the other from the elements in the unsorted end of the array. Notice that the algorithm need not do anything with the value in the last indexed variable, a[9]. That is because once the other elements are positioned correctly, a[9] must also have the correct value. After all, the correct value for a[9] is the smallest value left to be moved, and the only value left to be moved is the value that is already in a[9].

The definition of the function sort, included in a demonstration program, is given in Display 7.12. sort uses the function indexOfSmallest to find the index of the smallest element in the unsorted end of the array, and then it does an interchange to move this element down into the sorted part of the array.

The function swapValues, shown in Display 7.12, is used to interchange the values of indexed variables. For example, the following call will interchange the values of a[0] and a[3]:

```
swapValues(a[0], a[3]);
```

The function swapValues was explained in Chapter 5.