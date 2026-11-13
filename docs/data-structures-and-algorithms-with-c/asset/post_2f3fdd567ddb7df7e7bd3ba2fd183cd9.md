
## Example:

```
int m[3][3];
/* Reading */
for(i = 0; i < 3; i++)
    for(j = 0; j < 3; j++)
        scanf("%d", &m[i][j]);
```

Therefore, the above code will read all the elements of the two-dimensional array m row by row. Similarly, the following code can be used to print all the elements of the two-dimensional array m in matrix form.

## Example:

```
/* Writing */
for(i = 0; i < 3; i++)
    for(j = 0; j < 3; j++)
        printf("%d ", m[i][j]);
    printf("\n ");
}
```

By surrounding the elements of each row by braces. C allows arrays of three or more dimensions. The compiler determines the maximum number of dimensions. The general form of a multidimensional array declaration is:
data_type array_name[s1][s2][s3]...[si]...[sn];
where s_i is the size of the i-th dimension. Some examples are:

## Example:

```
int survey[3][5][12];
float table [5][4][5][3];
```

Here survey is a three-dimensional array and table is a four-dimensional array.

## Operations Perform on Arrays

Arrays are most important and commonly used data structures. They are also used to implement many other data structures. Almost all types of operations are performed on Arrays.

### Table 3.1: Operations on Arrays

| Operation | Description |
| :--- | :--- |
| Traversing | Accessing and processing each data item of the array exactly once. |
| Insertion | Insert a data item into the array. |
| Deletion | Delete a data item from the array. |
| Merging | Combining the data items of two different sorted arrays into a single sorted array. |
| Searching | Find the location of the key value within the array. |
| Sorting | Arranging all the array elements either in ascending or in descending order. |

## Traversing a Linear Array

The method of accessing and processing each element of the array exactly once is known as traversing. In an array, traversal beginning from the first element in the array and ends at the last element of the array.

### Algorithm to traverse a linear array

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

## Inserting an Element into a Linear Array

In an array, insertion operation can be performed in different ways. Insert an element in an array can be done in the following ways:

- To a specific position into the unsorted array
- By value of the inserted element in the sorted array

### Inserting an Element to a Specific Position

Now, to insert a key element to a specific position in a linear array, at first, it needed to move each element from the back up one position until getting the specified position. Then insert a key element into a given position. Finally, increment array size by one.

### Example:

Insert 50 to the 2nd position of the array with 5 elements.

![](img/723fa3ef35f5102eb67dc45b74bb823d_51_0.png)

Figure 3.5: (a-e) Insertion in the array to a specific position

### Algorithm to insert an element to a specific position into a linear array

```
Algorithm: Insert (A, N, P, KEY)
[A is an array of N elements; P is the position of the inserted item, KEY is the inserted item]
1. Set I=N-1
2. Repeat steps 3 and 4 while I>=P
3. Set A[I+1]=A[I]
4. Set I=I-1
   [End of loop]
5. Set A[P]=KEY
6. Set N=N+1
7. Return
```

### Inserting an Element in a sorted Array

While inserting an element into a sorted linear array, at first, it needs to find the correct position to insert the key element. When the position cannot be found, then insert at the end. Otherwise, move each element from the back up one position until getting position to insert. Then insert a key element into required position. Finally, the array size is incremented by one.

### Example:

Insert 50 into a sorted array with 5 elements.

![](img/723fa3ef35f5102eb67dc45b74bb823d_52_0.png)

Figure 3.6: (a-d) Insertion in the sorted Array

### Algorithm to insert an element in the sorted Array

```
Algorithm: Insert (A, N, KEY)
[A is the sorted array of N elements and KEY is the inserted item]
1. Set I = N – 1
2. Repeat steps 3 and 4 while A[I]>KEY
3. Set A[I+1]=A[I]
4. Set I=I-1
   [End of loop]
5. Set A[I+1]=KEY
6. Set N=N+1
7. Return
```

## Deleting an element from a Linear Array

In the array, delete operation can be performed in different ways. Delete an element in an array can be done in the following ways:

- From a specific position of the deleted element
- By value of the deleted element

### Deleting an element from a specific position

To delete a key element from a specific position of a linear array, at first, it needed to move each element from one after the given position forward one position until end of the array. Finally, the array size is decremented by one.

### Example:

Delete an element from 3rd position (i.e. 21) of the array with 6 elements.

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 21 | 14 | 77 | (6) | (7) | (8) | (9) |

a) Initial Array

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 14 | 14 | 77 | | | | |

b) Move from 4th position to 3rd position

| [0] | [1] | [2] | [3] | [4] | [5] | [6] | [7] | [8] | [9] |
|---|---|---|---|---|---|---|---|---|---|
| 40 | 84 | 50 | 14 | 77 | | | | | |

c) Move from 5th position to 4th position

Figure 3.7: (a-c) Delete element from a specific position

### Algorithm to delete an element from a specific position

```
Algorithm: Delete (A, N, P, KEY)
[A is an array of N number of elements, P is the position of the deleted item; KEY is the deleted item returned by reference]
1. Set I = P
2. KEY = A[P]
3. Repeat steps 4 and 5 while I < N - 1
4.   Set A[I] = A[I+1]
5.   Set I = I + 1
   [End of loop]
6. Set N = N - 1
7. Return
```

### Deleting an element by value

When deleting operation performed on the array by the value of the element, then it needed to search through the array to find its position.

Now there are two ways to find out the position of the deleted element. In the case of the sorted array, we can use binary search to find the position; otherwise if the array is unsorted then perform a linear search to find the position.

The following algorithm, deleting a key element from a specific position of an unsorted array. At first, it needed to search the array to find its position using linear searching. After getting the position, move each element from one after that position forward one position until end of the array. Finally, the array size is decremented by one.

The following algorithm, deleting an element of the linear array.

### Algorithm to delete an element using by value

```
Algorithm: Delete (A, N, KEY)
[A is the name of the array, N is the number of elements of the array, P is the position of the deleted item, KEY is the deleted item]
1. Set I = 0
2. Repeat while A[I] != KEY AND I < N
3. Set I = I + 1
   [End of loop]
4. Repeat steps 5 and 6 while I < N-1
5. Set A[I] = A[I+1]
6. Set I = I + 1
   [End of loop]
7. Set N = N - 1
8. Return
```

## Merging

Merging is an operation of combining more than one sorted array together so that resulting array remains sorted. The merge algorithm used in the merge-sort algorithm, a comparison-based sorting algorithm.

Merging of two sorted arrays can be done in linear time and space. Let two sorted arrays, A of m elements and B of n elements merge to form a sorted array C of total m + n elements.

The first element of array A is compared with the first element of array B. If the first element of array A is smaller than the first element of array B, the element from array A is moved to the new array C. The subscript of the array A is now increased since the first element is now set and we move on.

Otherwise, the element from array B should be smaller; it is moved to the new array C. The subscript of array B is increased. This process of comparing the elements in the two arrays continues until either array A or array B is empty. When one array is empty, any elements remaining in the other (non-empty) array are appended to the end of array C and the merge is complete.

### Example:

Merge two sorted arrays A of 6 elements and B of 5 elements to form a sorted array C of 11 elements

A:

| 0 | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 3 | 6 | 9 | 12 | 14 | 17 |

B:

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| 2 | 5 | 8 | 11 | 15 |

C:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | | | | | | | | | | |

- (a) Since 3 > 2, hence copy 2 and increment indices of B and C

C:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | | | | | | | | | |

- (b) Since 3 < 5, hence copy 3 and increment indices of A and C

C:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 2 | 3 | 5 | | | | | | | | |

- (c) Since 6 > 5, hence copy 5 and increment indices of B and C
