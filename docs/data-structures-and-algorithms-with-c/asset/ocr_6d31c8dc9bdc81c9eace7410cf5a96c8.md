# Algorithm to traverse a linear array

```
Algorithm: Traverse (A, N)
[A is the name of the array and N is the number of elements of the array]
1. Set I=0
2. Repeat steps 3 and 4 while I < N
3. Visit A[I]
4. Set I=I+1
   [End of loop]
5. Return
```

# Inserting an Element into a Linear Array

On array, insertion operation can be performed in different ways. Insert an element in an array can be done on the following ways:

+   - To a specific position into the unsorted array
+   - By value of the inserted element in the sorted array

# Inserting an Element to a Specific Position

Now, to insert a key element to a specific position in a linear array, at first, it needed to move each element from the back up one position until getting the specified position. Then insert a key element into a given position. Finally, increment array size by one.

# Example:

Insert 50 to the 2nd position of the array with 5 elements.

![](bbox=[0.1, 0.53, 0.9, 0.75])

Figure 3.5: (a-e) Insertion in the array to a specific position

# Algorithm to insert an element to a specific position into a linear array

```
Algorithm: Insert (A, N, P, KEY)
[A is an array of N elements; P is the position of the inserted item, KEY is the inserted item]
1. Set I=N-1
```