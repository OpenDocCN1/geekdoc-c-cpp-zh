+   - From a specific position of the deleted element
+   - By value of the deleted element

# Deleting an element from a specific position

To delete an key element from a specific position of a linear array, at first, it needed to move each element from one after the given position forward one position until end of the array. Finally, the array size is decremented by one.

# Example:

Delete an element from 3rd position (i.e. 21) of the array with 6 elements.

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 21 | 14 | 77 | (6) | (7) | (8) | (9) |
*a) Initial Array*

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 14 | 14 | 77 | | | | |
*b) Move from 4th position to 3rd position*

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 14 | 77 | | | | | |
*c) Move from 5th position to 4th position*

Figure 3.7: (a-c) Delete element from a specific position

# Algorithm to delete an element from a specific position

```
Algorithm: Delete (A, N, P, KEY)
[A is an of N number of elements, P is the position of the deleted
item; KEY is the deleted item returns by reference]
1. Set I = P
2. KEY = A[P]
3. Repeat steps 4 and 5 while I < N - 1
4.   Set A[I] = A[I+1]
5.   Set I = I + 1
   [End of loop]
6. Set N = N - 1
7. Return
```

# Deleting an element by value

When deleting operation performed on the array by the value of the element, then it needed to search through the array to find its position.

Now there are two ways to find out the position of the deleted element. In the case of the sorted array, we can use binary search to find the position; otherwise if the array is unsorted then perform a linear search to find the position.

The following algorithm, deleting a key element from a specific position of an unsorted array. At first, it needed to search the array to find its position using linear searching. After getting the position, move each element from one after that position forward one position until end of the array. Finally, the array size is decremented by one.

The following algorithm, deleting an element of the linear array.