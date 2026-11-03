
Number of elements n2: 6
Enter elements: 2 23 28 44 49 60
Resultant array after merge sort.
2 5 10 14 19 23 28 30 44 49 60

## 17.2.6 Simple insertion sort

We will discuss the insertion sort in this section. An example of an insertion sort occurs while playing cards. To sort the cards in your hand you extract a card, shift the remaining cards, and then insert the extracted card in the correct place. This process is repeated until all the cards are in the correct sequence. This is illustrated with a simple example in Fig. 17.5. Consider the list – 23, 17, 5, 14.

![](img/65953ea584e494f3d396b2252cb5ea53_481_0.png)

Fig. 17.5

Look at how the sorting proceeds in various stages. At each stage pushing the remaining elements down creates an empty space.

### 1. C program for insertion sort

Let us assume that an array named elements[] will hold the array to be sorted and maxsize is the number of elements to be sorted. We will also assume that the sorting order is ascending in nature. The required C program is shown in Fig 17.6.

```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500
void insertionsort(int elements[], int maxsize);
int elements[MAXSIZE],maxsize;
int main()
{
int i;
printf("\nHow many elements you want to sort: ");
scanf("%d",&maxsize);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i :",i);
scanf("%d",&elements[i]);
}
printf("\nArray before sorting:\n");
for (i = 0; i < maxsize; i++)
printf("[%d]", elements[i]);
printf ("\n");
insertionsort(elements, maxsize);
printf("\nArray after sorting:\n");
for (i = 0; i < maxsize; i++)
printf("[%d]", elements[i]);
}
void insertionsort(int elements[], int maxsize)
{
int i, j, index;
for (i=1; i < maxsize; i++)
{
index = elements[i];
j = i;
while ((j > 0) && (elements[j-1] > index))
{
elements[j] = elements[j-1];
j = j - 1;
}
elements[j] = index;
}
}
```

Fig. 17.6 C program for insertion sort

### 2. Efficiency of insertion sort

Let us now analyze the efficiency of the insertion sort. Assuming there are n elements in the array, we must pass through n − 1 entries. For each entry, we may need to examine and shift a maximum of n − 1 other entries, resulting in an efficiency of O(n²).

## 17.2.7 Shell sort

We will discuss the shell sort in this section. The shell sort is based on the insertion sort. The given list of elements is broken down in few smaller lists. After this, the insertion sort is applied on such smaller lists. These smaller lists are again recombined. Another partition is made and the procedure is repeated. The breaking down of the list into smaller lists is by selecting elements at specific locations. This is determined by a factor called increment. Consider the list – 23, 12, 6, 34, 13, 7, 44. We may initially take the increment as 3. This would break the list as 23, 34, 44; 12,13 and 6, 7. The first list is done using elements[0], elements[3] and elements[6] where the increment is 3. This list is sorted using insertion sort. The next list is elements[1] and elements[4] where the increment is the same 3. The final list is elements[2] and elements[5] with the same increment of 3. After sorting them, the sublists are recombined.

As a next stage, the increment is changed (reduced by a suitable amount) and the process is repeated. The process continues till the increment is 1. The choice of increment is left to our choice. We can use increments such as 7, 5, 3 and 1 or 6, 4, 1, etc.

### 1. C program for shell sort

Let us assume that an array named elements[] will hold the array to be sorted and maxsize is the number of elements to be sorted. We will also assume that the sorting order is ascending in nature. The required C program is shown in Fig. 17.7. Note that we have taken the increments as 7, 2 and 1. The successive increments are deduced by the formula increment / 2.

```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500
void shellsort(int elements[], int maxsize);
int elements[MAXSIZE],maxsize;
int main()
{
int i;
printf("\nHow many elements you want to sort: ");
scanf("%d",&maxsize);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i :");
scanf("%d",&elements[i]);
}
printf("\nArray before sorting:\n");
for (i = 0; i < maxsize; i++)
printf("%6d",elements[i]);
printf("\n");
shellsort(elements, maxsize);
printf("\nArray after sorting:\n");
for (i = 0; i < maxsize; i++)
    printf("[%d] ", elements[i]);
}
void shellsort(int elements[], int maxsize)
{
    int i, j, increment, temp;
    increment = 7;
    while (increment > 0)
    {
        for (i=0; i < maxsize; i++)
        {
            j = i;
            temp = elements[j];
            while ((j >= increment) && (elements[j-increment] > temp))
            {
                elements[j]= elements[j - increment];
                j = j - increment;
            }
            elements[j]= temp;
        }
        if (increment/3 != 0)
            increment = increment/3;
        else if (increment == 1)
            increment = 0;
        else
            increment = 1;
    }
}
```

Fig. 17.7

## 17.3 SEARCHING

All of us use searching in one way or the other in our daily life. Any information gathering process or retrieval process is basically a searching process. We already saw that searching is more efficient if the data is available in an ordered fashion (sorted). Let us now look into two of the widely used search methods—the linear search and binary search techniques.

## 17.3.1 Linear Search

The linear search or the sequential searching is most simple searching method. It does not expect the list to be sorted also. The key, which is to be searched, is compared with each element of the list one by one. If a match exists, the search is terminated. If the end of the list is reached, it means that the search has failed and the key has no matching element in the list.

### 1. C program for linear search

Figure 17.8 shows the C program for linear search

```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500
int linearsearch(int elements[], int maxsize, int key);
int elements[MAXSIZE], maxsize, key;
int main()
{
int i, pos;
printf("\nHow many elements you have in the list: ");
scanf("%d",&maxsize);
printf("\nEnter the key to be searched: ");
scanf("%d",&key);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i : ");
scanf("%d",&elements[i]);
}
pos = -1;
pos = linearsearch(elements, maxsize, key);
if (pos != -1)
printf("\nThe key %d is found at position %d", key, pos);
else
printf("\nThe key is not found in the list");
}
int linearsearch(int elements[], int maxsize, int key)
{
int i, j, temp;
for (i = 0; i < maxsize - 1; i++)
{
if (key == elements[i])
return i;
}
return -1;
}
```

Fig. 17.8

### 2. Efficiency of linear search

To find the number of key comparisons for a successful match, we can add the number required for each comparison and divide by the total number of elements in the list. This would give:

$$ \frac{1+2+3+...+n}{n} = \frac{n(n+1)}{2n} $$

## 17.3.2 Binary Search

The binary search is yet another simple searching method. However, in the binary search, the algorithm expects the list to be sorted. You can apply any one of the sorting methods before using the binary search algorithm.

How does the algorithm operates? The given list is divided into two equal halves. The given key is compared with the middle element of the list. Now three situations may occur:

- (a) The middle element matches with the key— the search will end peacefully here.
- (b) The middle element is greater than the key— then the value which we are searching is (possibly) in the first half of the list
- (c) The middle element is lower than the key— then the value which we are searching is (possibly) in the second half of the list

Now the list is searched either in the first half or in the second half as got by the result of conditions (b) and (c) given above. This process is repeated till we get the key or the search fails because the key does not exist.

### 1. C program for Iterative binary search

Figure 17.9 gives the C program for iterative binary search.

```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500

int binsearch(int elements[], int maxsize, int key);
void bubblesort(int elements[], int maxsize);
int elements[MAXSIZE], maxsize, key;

int main()
{
 int i, pos;
 printf("\nHow many elements you have in the list: ");
 scanf("%d",&maxsize);
 printf("\nEnter the key to be searched: ");
 scanf("%d",&key);
 printf("\nEnter the values one by one: ");
 for (i = 0; i < maxsize; i++)
 {
 printf ("\nEnter element %i : ");
 scanf("%d",&elements[i]);
 }
 bubblesort(elements, maxsize);
 pos = -1;
 pos = binsearch(elements, maxsize, key);
 if (pos != -1)
 printf("\nThe key %d is found at position %d", key, pos);
 else
```
