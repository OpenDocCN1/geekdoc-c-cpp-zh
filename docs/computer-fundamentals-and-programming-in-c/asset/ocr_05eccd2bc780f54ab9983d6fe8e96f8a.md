# Insertion sort

The primary idea in insertion sort is to pick up a data element from a list or an array and insert it into its proper place in the partial data list or array considered so far.

The process of insertion sort is started by considering the first element to belong to a sorted sub-array while the remaining array elements to another sub-array which is considered as unsorted. The first step then is to compare the first element of the unsorted array with the sorted array’s element. If the sorting is for arranging the elements in ascending order, then the comparison is carried out to find whether the first element of the unsorted array is smaller than that of the sorted array’s element. If this is true, then the first element of the unsorted array is placed at the first position of the sorted array while the existing element in the sorted array is shifted right by one position. The sorted sub-array will now contain two sorted elements while the unsorted sub-array will contain N − 2 elements, where N denotes the size of the whole array. In the second step, again the first element of the unsorted sub-array is compared with the elements of the sorted sub-array and the resulting element is placed at the proper position while shifting the larger elements by one position to the right in the sorted sub-array.

The sorted sub-array now contains three elements arranged in order, while the rest of the elements form the unsorted sub-array. In the same way, the next step repeats the same procedure of comparison and placing the appropriate element at the proper position. This process continues till the last element in the array. Thus, in each pass, the first element of the unsorted portion is picked up, transferred to the sorted sub-list, and inserted at the appropriate place. A list of N elements will take at most N−1 passes to sort the data.

Figure 12.4 shows the insertion sort technique. This illustration demonstrates the sorting of array. Every time the first element, which is shown highlighted, is compared with the elements of the sorted sub-array and interposed at the proper position in sorted sub-array by suitably shifting the larger value elements.

A function prepared for implementing the insertion sort algorithm for sorting an array in ascending order is given below Fig. 12.4.

![](bbox=[0.045, 0.055, 0.906, 0.944])

Fig. 12.4  Insertion sort

```
```c
void insertSort(int A[], int arr_size)
{
    int i, j, temp;
    for (i=1; i < arr_size; i++)
    {
        temp = A[i];
        j = i;
        while ((j > 0) && (A[j-1] > temp))
        {
            A[j] = A[j-1];
            j = j - 1;
        }
        A[j] = temp;
    }
}
```
```

An alternate function that can also do insertion sorting is shown below.

```
```c
void insert(int A[], int size)
{
    int i, j, temp;
    for (i = 1; i < size; i++)
    {
        temp = A[i];
        for (j = i - 1; j >= 0 && temp < A[j]; j--)
            A[j + 1] = A[j];
        A[j + 1] = temp;
    }
}
```
```

An advantage of this procedure is that it sorts the array only when it is really necessary. If the array is already in order, no moves for sorting are performed. However, it overlooks the fact that the elements may already be in their proper positions. When an element has to be inserted, all elements greater than this have to be shifted. There may be