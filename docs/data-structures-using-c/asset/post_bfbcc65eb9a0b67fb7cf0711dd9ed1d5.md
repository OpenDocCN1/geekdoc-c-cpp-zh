
- 3. Insert 6 => 3, 5, 6, 7
- 4. Insert 1 => 1, 3, 5, 6, 7

The piece of code needed to do this will look like

```
for(int i = 1; i < n; i++)
{ // insert a[i] into a[0:i - 1]
  // code to insert comes here
}
```

After adding the code for insertion we have already built, the resultant code will be

```
for(int i = 1; i < n; i++)
{ // insert a[i] into a[0:i - 1]
  int t = a[i];
  int j;
  for(j = i - 1; j >= 0 && t < a[j]; j--)
    a[j + 1] = a[j];
  a[j + 1] = t;
}
```

To save memory, most implementations use an in-place sort that works by moving the current item past the already sorted items and repeatedly swapping it with the preceding item until it is in place. The main idea behind the insertion sort is to insert the i-th element, in the i-th pass, into A(1), A(2), ..., A(i), in the right place. Algorithm 9.6 lists the steps for insertion sort.

### ALGORITHM 9.6

- 1. Set J = 2, where J is an integer
- 2. Check if list (J) < list (J - 1); if so interchange them; set J = J - 1 and repeat step (2) until J = 1
- 3. Set J = 3, 4, 5, ... , N and keep on executing step (2)

The following steps in Example 9.3 essentially define the insertion sort as applied to sorting into ascending order an array list containing N elements:

### EXAMPLE 9.3

Consider the given unsorted array. Sort this array in ascending order using insertion sort.

| Elements | 76 | 67 | 36 | 55 | 23 | 14 | 6 |
|---|---|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 |

Solution Pass 1: Consider the first list is sorted, and insert the second number 67 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 76 | 67 36 55 23 14 6 |
| Index | 0 | 1 2 3 4 5 6 |

Pass 2: Insert number 36 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 67 76 | 36 55 23 14 6 |
| Index | 0 1 | 2 3 4 5 6 |

Pass 3: Insert number 55 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 36 67 76 | 55 23 14 6 |
| Index | 0 1 2 | 3 4 5 6 |

Pass 4: Insert number 23 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 36 55 67 76 | 23 14 6 |
| Index | 0 1 2 3 | 4 5 6 |

Pass 5: Insert number 14 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 23 36 55 67 76 | 14 6 |
| Index | 0 1 2 3 4 | 5 6 |

Pass 6: Insert number 6 in the first list.

| | Sorted array | Unsorted array |
|---|---|---|
| Elements | 14 23 36 55 67 76 | 6 |
| Index | 0 1 2 3 4 5 | 6 |

The final sorted array is

| Elements | 6 | 14 | 23 | 36 | 55 | 67 | 76 |
|---|---|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 |

Program Code 9.8 defines the InsertionSort() function.

```
PROGRAM CODE 9.8
void InsertionSort(int A[], int n)
{
    int i, j, element;
    for(i = 1; i < n; i++)
    {
        element = A[i];
        // insert i-th element in 0 to i - 1 array
        j = i;
        while((j > 0) && (A[j - 1] > element))
        //compare if A[j - 1] > element
        {
            A[j] = A[j - 1]; // shift elements
            j = j - 1;
        }
        A[j] = element; // place element at j-th position
    }
}
```

### Analysis of Insertion Sort

Although the insertion sort is almost always better than the bubble sort, the time required in both the methods is approximately the same, that is, it is proportional to n^2, where n is the number of data items in the array.

The total number of comparisons is given as follows:
(n - 1) + (n - 2) + ... + 1 = (n - 1) x n/2

which is O(n^2).

If the data is initially sorted, only one comparison is made on each pass so that the sort time complexity is O(n). The number of interchanges needed in both the methods is on an average (n^2)/4, and in the worst case is about (n^2)/2.

When the data is already partially ordered, the insertion sort will normally take less time than the bubble sort. The insertion sort is highly efficient if the array is already in an almost sorted order. Example 9.4 provides a pictorial representation of the insertion sort.

### EXAMPLE 9.4 Figure 9.6 is an example of insertion sort.

![](img/a99ec79093c067f0bed8f1086197950e_460_0.png)

Fig. 9.6 Insertion sorting

## 9.3.5 Selection Sort

The selection sort algorithms construct the sorted sequence, one element at a time, by adding elements to the sorted sequence in order. At each step, the next element to be added to the sorted sequence is selected from the remaining elements.

Because the elements are added to the sorted sequence in order, they are always added at one end. This makes the selection sorting different from the insertion sorting. In insertion sorting, the elements are added to the sorted sequence in an arbitrary order. Therefore, the position in the sorted sequence at which each subsequent element is inserted is arbitrary.

Both selection and insertion sorts sort the arrays in-place.

In this method, we sort a set of unsorted elements in two steps. In the first step, find the smallest element in the structure. In the second step, swap the smallest element with the element at the first position. Then, find the next smallest element and swap with the element at the second position. Repeat these steps until all elements get arranged at proper positions.

This is illustrated in Program Code 9.9.

```
PROGRAM CODE 9.9
void SelectionSort(int A[], int n)
{
    int i, j;
    int minpos, temp;
    for(i = 0; i < n - 1; i++)
    {
        minpos = i;
        for(j = i + 1; j < n; j++)
        {
            //find the position of min element as minpos from
            //i + 1 to n - 1
            if(A[j] < A[minpos])
                minpos = j;
        }
        if(minpos != i)
        {
            temp = A[i];
            // swap the ith element and minpos element
            A[i] = A[minpos];
            A[minpos] = temp;
        }
    }
}
```

Look at following array of unsorted integers. The working of selection sort is shown in Table 9.4 with the resultant array after each pass where the updated values of index variable i and minpos after each pass are indicated.

| | Original unsorted array |
|---|---|
| Elements | 76 | 67 | 36 | 55 | 23 | 14 | 6 |
| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 |

### Table 9.4 Selection sort

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | i | minpos |
|---|---|---|---|---|---|---|---|---|---|
| | 76 | 67 | 36 | 55 | 23 | 14 | 6 | 0 | 6 |
| Pass 1 | 6 | 67 | 36 | 55 | 23 | 14 | 76 | 1 | 5 |
| Pass 2 | 6 | 14 | 36 | 55 | 23 | 67 | 76 | 2 | 4 |
| Pass 3 | 6 | 14 | 23 | 55 | 36 | 67 | 76 | 3 | 4 |
| Pass 4 | 6 | 14 | 23 | 36 | 55 | 67 | 76 | 4 | 4 |
| Pass 5 | 6 | 14 | 23 | 36 | 55 | 67 | 76 | 5 | 5 |
| Sorted array | 6 | 14 | 23 | 36 | 55 | 67 | 76 | | |

The same can be done in reverse order also to arrange the elements. That is, first find the largest element in the structure. In the second step, swap the largest element with the element at the last position. Then, find the next largest element and swap with the element at the last but one position, and so on. Let us have look at one more example on the working of selection sort.

### EXAMPLE 9.5 Figure 9.7 shows an unsorted array and the sorting process with the resultant array after each pass.

![](img/a99ec79093c067f0bed8f1086197950e_462_0.png)

Fig. 9.7 Selection sort sample run

### Analysis of Selection Sort

In Program Code 9.9, we can note that there are two loops, one nested within the other. During the first pass, (n - 1) comparisons are made. In the second pass, (n - 2) comparisons are made. In general, for the i-th pass, (n - i) comparisons are required. The total number of comparisons is as follows:

```
(n - 1) + (n - 2) + ... + 1 = n(n-1)/2
```

Therefore, the number of comparisons for the selection sort is proportional to n^2, which means that it is O(n^2). The different cases are as follows:

- Average case: O(n^2) Best case: O(n^2) Worst case: O(n^2)

The maximum number of interchanges required is (n - 1) as there is utmost one interchange required for each pass. However, the actual number of interchanges depends on the ordering of the original table, because if the smallest key is already at its proper place, the algorithm makes no interchanges.

The selection sort and insertion sort are more efficient than bubble sort. Selection sort is recommended for lists. When records are large, the keys are simple as the selection sort requires lesser swaps than the insertion sort and more comparisons than the insertion sort. If the records are small and the keys are difficult to compare, insertion sort is recommended.

## 9.3.6 Quick Sort

Quick sort is based on the divide-and-conquer strategy. This sort technique initially selects an element called as pivot that is near the middle of the list to be sorted, and then the items on either side are moved so that the elements on one side of pivot are smaller and on the other side are larger. Now, the pivot is at the right position with respect to the sorted sequence. These two steps, selecting the pivot and arranging the elements on either side of pivot, are now applied recursively to both the halves of the list till the list size reduces to one.

Quick sort is thus an in-place, divide-and-conquer-based, massively recursive sort technique. This technique reduces unnecessary swaps and moves the element at a great distance in one move.

To choose the pivot, there are several strategies. The popular way is considering the first element as the pivot.

Thus, the recursive algorithm consists of four steps:

- 1. If the array size is 1, return immediately.
- 2. Pick an element in the array to serve as a 'pivot' (usually the left-most element in the list).
- 3. Partition the array into two parts—one with elements smaller than the pivot and the other with elements larger than the pivot by traversing from both the ends and performing swaps if needed.
- 4. Recursively repeat the algorithm for both partitions.
