
| 22 | 19 | 7 | | Result: | 9 | 19 | 7 |
| 9 | 27 | 36 | | | 22 | 27 | 36 |
| 33 | 45 | 59 | | | 33 | 45 | 54 |
| 41 | 63 | 90 | | | 41 | 63 | 59 |
| 81 | 72 | 54 | | | 81 | 72 | 90 |

The elements of the array can be given as:
9, 19, 7, 22, 27, 36, 33, 45, 54, 41, 63, 59, 81, 72, 90

Finally, arrange the elements of the array in a single column and sort the column.

## Result:

| 9 | 7 |
| 19 | 9 |
| 7 | 19 |
| 22 | 22 |
| 27 | 27 |
| 36 | 33 |
| 33 | 36 |
| 45 | 41 |
| 54 | 45 |
| 41 | 54 |
| 63 | 59 |
| 59 | 63 |
| 81 | 72 |
| 72 | 81 |
| 90 | 90 |

Finally, the elements of the array can be given as:
7, 9, 19, 22, 27, 33, 36, 41, 45, 54, 59, 63, 72, 81, 90

The algorithm to sort an array of elements using shell sort is shown in Fig. 14.13. In the algorithm, we sort the elements of the array Arr in multiple passes. In each pass, we reduce the gap_size (visualize it as the number of columns) by a factor of half as done in Step 4. In each iteration of the for loop in Step 5, we compare the values of the array and interchange them if we have a larger value preceding the smaller one.

```
Shell_Sort(Arr, n)
Step 1: SET FLAG = 1, GAP_SIZE = N
Step 2: Repeat Steps 3 to 6 while FLAG = 1 OR GAP_SIZE > 1
Step 3: SET FLAG = 0
Step 4: SET GAP_SIZE = (GAP_SIZE + 1) / 2
Step 5: Repeat Step 6 for I = 0 to I < (N - GAP_SIZE)
Step 6: IF Arr[I + GAP_SIZE] > Arr[I]
        SWAP Arr[I + GAP_SIZE], Arr[I]
        SET FLAG = 0
Step 7: END
```

### Figure 14.13 Algorithm for shell sort

## PROGRAMMING EXAMPLE

## 12. Write a program to implement shell sort algorithm.

```
#include<stdio.h>
void main()
{
 int arr[10]={-1};
 int i, j, n, flag = 1, gap_size, temp;
 printf("\n Enter the number of elements in the array: ");
 scanf("%d", &n);
 printf("\n Enter %d numbers: ", n); // n was added
 for(i=0;i<n;i++)
 scanf("%d", &arr[i]);
 gap_size = n;
 while(flag == 1 || gap_size > 1)
 {
 flag = 0;
 gap_size = (gap_size + 1) / 2;
 for(i=0; i<(n - gap_size); i++)
 {
 if(arr[i+gap_size] < arr[i])
 {
 temp = arr[i+gap_size];
 arr[i+gap_size] = arr[i];
 arr[i] = temp;
 flag = 0;
 }
 }
 }
 printf("\n The sorted array is: \n");
 for(i=0;i<n;i++)
 printf("%d\t", arr[i]);
 printf("\n");
}
```

## 14.15 TREE SORT

A tree sort is a sorting algorithm that sorts numbers by making use of the properties of binary search tree (discussed in Chapter 10). The algorithm first builds a binary search tree using the numbers to be sorted and then does an in-order traversal so that the numbers are retrieved in a sorted order. We will not discuss this topic in detail here because we assume that reader has already studied it in sufficient details in the Chapter 10.

### Complexity of Tree Sort Algorithm

Let us study the complexity of tree sort algorithm in all three cases.

| Best Case | Worst Case |
| :--- | :--- |
| • Inserting a number in a binary search tree takes O (log n) time. | • Occurs with an unbalanced binary search tree, i.e., when the numbers are already sorted. |
| • So, the complete binary search tree with n numbers is built in O (n log n) time. | • Binary search tree with n numbers is built in O (n^2) time. |
| • A binary tree is traversed in O (n) time. | • A binary tree is traversed in O (n) time. |
| • Total time required = O (n log n) + O (n) = O (n log n) | • Total time required = O(n^2) + O(n) = O(n^2). |
| | • The worst case can be improved by using a self-balancing binary search tree. |

## PROGRAMMING EXAMPLE

## 13. Write a program to implement tree sort algorithm.

```
#include <stdio.h>
#include <conio.h>
#include <alloc.h>
struct tree
{
    struct tree *left;
    int num;
    struct tree *right;
};
void insert (struct tree **, int);
void inorder (struct tree *);
void main( )
{
    struct tree *t;
    int arr[10];
    int i ;
    clrscr( ) ;
    printf("\n Enter 10 elements : ");
    for(i=0;i<10;i++)
        scanf("%d", &arr[i]);
    t = NULL;
    printf("\n The elements of the array are : \n" );
    for (i = 0 ; i < 10 ; i++)
        printf ( "%d ", arr[i] );
    for (i = 0 ; i < 10 ; i++)
        insert ( &t, arr[i] ) ;
    printf ( "\n The Sorted array is : \n" );
    inorder ( t ) ;
    getche( ) ;
}
void insert (struct tree **tree_node, int num)
{
    if ( *tree_node == NULL )
    {
        *tree_node = malloc ( sizeof ( struct tree ) ) ;
        ( *tree_node ) -> left = NULL ;
        ( *tree_node ) -> num = num ;
        ( *tree_node ) -> right = NULL ;
    }
    else
    {
        if ( num < ( *tree_node ) -> num )
            insert ( &( *tree_node ) -> left ), num );
        else
            insert ( &( *tree_node ) -> right ), num );
    }
}
void inorder (struct tree *tree_node )
{
    if ( tree_node != NULL )
    {
        inorder ( tree_node -> left ) ;
        printf ( "%d\t", tree_node -> num ) ;
        inorder ( tree_node -> right ) ;
    }
}
```

## Table 14.1 Comparison of algorithms

| Algorithm | Average Case | Worst Case |
|---|---|---|
| Bubble sort | O(n^2) | O(n^2) |
| Bucket sort | O(n.k) | O(n^2.k) |
| Selection sort | O(n^2) | O(n^2) |
| Insertion sort | O(n^2) | O(n^2) |
| Shell sort | - | O(n log^2 n) |
| Merge sort | O(n log n) | O(n log n) |
| Heap sort | O(n log n) | O(n log n) |
| Quick sort | O(n log n) | O(n^2) |

## 14.16 COMPARISON OF SORTING ALGORITHMS

Table 14.1 compares the average-case and worst-case time complexities of different sorting algorithms discussed so far.

## 14.17 EXTERNAL SORTING

External sorting is a sorting technique that can handle massive amounts of data. It is usually applied when the data being sorted does not fit into the main memory (RAM) and, therefore, a slower memory (usually a magnetic disk or even a magnetic tape) needs to be used. We will explain the concept of external sorting using an example discussed below.

Example 14.9 Let us consider we need to sort 700 MB of data using only 100 MB of RAM. The steps for sorting are given below.
Step 1: Read 100 MB of the data in RAM and sort this data using any conventional sorting algorithm like quick sort.
Step 2: Write the sorted data back to the magnetic disk.
Step 3: Repeat Steps 1 and 2 until all the data (in 100 MB chunks) is sorted. All these seven chunks that are sorted need to be merged into one single output file.
Step 4: Read the first 10 MB of each of the sorted chunks and call them input buffers. So, now we have 70 MB of data in the RAM. Allocate the remaining RAM for output buffer.
Step 5: Perform seven-way merging and store the result in the output buffer. If at any point of time, the output buffer becomes full, then write its contents to the final sorted file. However, if any of the 7 input buffers gets empty, fill it with the next 10 MB of its associated 100 MB sorted chunk or else mark the input buffer (sorted chunk) as exhausted if it does not has any more left with it. Make sure that this chunk is not used for further merging of data.
The external merge sorting can be visualized as given in Fig. 14.14.

![](img/be6359df08208122bec6fad1103de211_473_0.png)

### Generalized External Merge Sort Algorithm

From the example above, we can now present a generalized merge sort algorithm for external sorting. If the amount of data to be sorted exceeds the available memory by a factor of k, then k chunks (also known as k run lists) of data are created. These k chunks are sorted and then a k-way merge is performed. If the amount of RAM available is given as x, then there will be k input buffers and 1 output buffer.

In the above example, a single-pass merge was used. But if the ratio of data to be sorted and available RAM is particularly large, a multi-pass sorting is used. We can first merge only the first half of the sorted chunks, then the other half, and finally, merge the two sorted chunks. The exact number of passes depends on the following factors:
• Size of the data to be sorted when compared with the available RAM
• Physical characteristics of the magnetic disk such as transfer rate, seek time, etc.

### Applications of External Sorting

External sorting is used to update a master file from a transaction file. For example, updating the EMPLOYEES file based on new hires, promotions, appraisals, and dismissals.

It is also used in database applications for performing operations like Projection and Join. Projection means selecting a subset of fields and join means joining two files on a common field to create a new file whose fields are the union of the fields of the two files. External sorting is also used to remove duplicate records.

- Searching refers to finding the position of a value in a collection of values. Some of the popular searching techniques are linear search, binary search, interpolation search, and jump search.
- Linear search works by comparing the value to be searched with every element of the array one by one is a sequence until a match is found.
- Binary search works efficiently with a sorted list. In this algorithm, the value to be searched is compared with the middle element of the array segment.
- In each step of interpolation search, the search space for the value to be found is calculated. The calculation is done based on the values at the bounds of the search space and the value to be searched.
- Jump search is used with sorted lists. We first check an element and if it is less than the desired value, then a block of elements is skipped by jumping ahead, and the element following this block is checked. If the checked element is greater than the desired value, then we have a boundary and we are sure that the desired value lies between the previously checked element and the currently checked element.
- Internal sorting deals with sorting the data stored in the memory, whereas external sorting deals with sorting the data stored in files.
- In bubble sorting, consecutive adjacent pairs of elements in the array are compared with each other.
- Insertion sort works by moving the current data element past the already sorted values and repeatedly interchanging it with the preceding value until it is in the correct place.
- Selection sort works by finding the smallest value and placing it in the first position. It then finds the second smallest value and places it in the second position. This procedure is repeated until the whole array is sorted.
- Merge sort is a sorting algorithm that uses the divide, conquer, and combine algorithmic paradigm. Divide means partitioning the n-element array to be sorted into two sub-arrays of n/2 elements in each sub-array. Conquer means sorting the two sub-arrays recursively using merge sort. Combine means merging the two sorted sub-arrays of size n/2 each to produce a sorted array of n elements. The running time of merge sort in average case and worst case can be given as O(n log n).
- Quick sort works using a divide-and-conquer strategy. It selects a pivot element and rearranges the elements in such a way that all elements less than pivot appear before it and all elements greater than pivot appear after it.
- Radix sort is a linear sorting algorithm that uses the concept of sorting names in alphabetical order.
- Heap sorts an array in two phases. In the first phase, it builds a heap of the given array. In the second phase, the root element is deleted repeatedly and inserted into an array.
- Shell sort is considered as an improvement over insertion sort, as it compares elements separated by a gap of several positions.
- A tree sort is a sorting algorithm that sorts numbers by making use of the properties of binary search tree. The algorithm first builds a binary search tree using the numbers to be sorted and then does an in-order traversal so that the numbers are retrieved in a sorted order.
