algorithm to outperform more complicated algorithms depends on your system. Typically this algorithm is only faster for arrays holding 5 or 10 items.

# Selectionsort in Arrays

In addition to describing insertionsort for linked lists, Chapter 3 also describes selectionsort for linked lists. Similarly Chapter 4 described selectionsort algorithms that use stacks and queues.

The basic idea is to search the input list for the largest item it contains and then add it to the end of a growing list. Alternatively, the algorithm can find the smallest item and move it to the beginning of the growing list. The following pseudocode shows the algorithm for use with arrays:

```
Selectionsort(Data: values[])
For i = 0 To <length of values> - i
  // Find the item that belongs in position i.
  <Find the smallest item with index j >= i>.
  Swap values[i] and values[j].
Next i
End Selectionsort
```

The code loops through the array to find the smallest item that has not yet been added to the sorted array. It then swaps that smallest with the item in position i.

Figure 6-2 shows the algorithm's keys. The image at the top shows the original unset array. In the middle image, the first three items (outlined in bold) have been sorted, and the algorithm is searching the unsorted items to find the one with the smallest value (3 in this case). The algorithm then swaps the item that has the smallest value to the next unsorted position. The image at the bottom of the figure shows the array after the new item has been moved to the sorted part of the array. The algorithm now continues the For loop to add the next item (which has value 5) to the growing portion of the array.

Like insertionsort, it sorts the items in the original array, so it doesn't need any additional storage (aside a few variables to control loops and move items).

If the array contains N items, the algorithm considers each of the N positions in the array. For each position i, it must search the N - i items that have not been sorted to find the item that belongs in position i. It swaps the item into its final position using a constant number of steps. Adding the steps to move all the items gives the following run time:

(N - 1) + (N - 2) + ... + 2 + 1 = (N^2 + N) / 2

This means the algorithm has run time O(N^2), the same run time as insertionsort. Like insertionsort, selectionsort is fast enough for small arrays (fewer than 10,000 or so items). It's also a fairly simple algorithm, so it may