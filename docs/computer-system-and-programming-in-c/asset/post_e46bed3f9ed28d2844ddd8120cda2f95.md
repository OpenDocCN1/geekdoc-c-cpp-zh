
```c
->info);
free(temp);
}
```

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_275_0.png)

## 3. Search

As long as the linked list is not empty, we can search the list for the node containing particular value e. To accomplish this operation, we need two pointers, prev and cur. After completing the searching, the pointer cur will point to the node containing the value e, and prev will hold the previous node of cur. The following figures show the procedure step by step.

Step 1. Initializing pointer cur points to the first node of the list, while the pointer prev has a value of null. See the following figure.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_275_1.png)

Step 2. Set prev point to the node pointed by cur. See the following figure.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_275_2.png)

Step 3. Set cur point to the node after prev. See the following figure.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_275_3.png)

Step 4. Repeat step 2, step 3, until cur is pointing to the node that contains value. See the following figures.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_275_4.png)

### Procedure Search

> {Procedure to search for each value in a linked list pointed by head. If found, cur should point to that node; otherwise, cur should point to the last node in the list. If cur points to the first node, prev should have the null value; otherwise, prev should point to the previous node. }

```pascal
Procedure Search (head, cur, prev: pointer; e: datatype);
begin
  cur := head; {initialization}
  prev := null;
  while (cur^.info != e) and (cur^.link != null)
  do
  begin
    prev := cur;
    cur := cur^.link
  end;
end;
```

### Implementation in C language

Implementation of the above procedure in C language is as follows:

```c
struct node
{
  int info;
  struct node * next;
}*start=NULL;
void search()
{
  struct node * curr,*temp;
  int n,flag=0;
  if(start==NULL)
  {
    printf("\n list is empty");
    getch();
    exit(1);
  }

  printf("\n enter the number which you want to search");
}
```

### Binary Search

book. You do not start at page 1 and read every entry! Instead, you turn to a page somewhere about where you expect the item to be. If you are lucky you find the item straight away. If not, you know which part of the book will contain the item (if it is there), and repeat the process with just that part of the book.

If you always split the data in half and check the middle item, you halve the number of remaining items to check each time. This is much better than linear search, where each unsuccessful comparison eliminates just one item.

### Algorithm

- The algorithm of binary search is as follows:
  - bottom = first element
  - top = last element
  - while ((top>=bottom) and (not found)) loop
    - mid := (top+bottom)/2
    - if (list(mid) = item to find) then
      - found := true
    - elseif (item to find > list(mid)) then
      - bottom := mid +1
    - else
      - top := mid - 1
    - end if
  - end loop
  - if found = true
    - wanted item is in database
  - else
    - wanted item is NOT in database
  - end if

### Implementation in C language

The implementation of binary search in C language is as follows:

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a[10],n,i,j,temp;
int beg,end,mid,target;
clrscr();
printf("enter the array elements: ");
for(i=0;i<n;i++)
scanf("%d",&a[i]);
//Sorting process
for(i=0;i<n-1;i++)
{
for(j=0;j<n-i-1;j++)
{
if(a[j+1]<a[j])
{
temp=a[j];
a[j]=a[j+1];
a[j+1]=temp;
}
}
}
printf("the sorted numbers are:");
for(i=0;i<n;i++)
printf("%4d",a[i]);
beg=a[0];
end=a[9];
mid=(beg+end)/2;
printf("\n enter the number to be searched:");
scanf("%d",&target);
while(beg<=end && a[mid]!=target)
{
if(target<a[mid])
end=mid-1;
else
beg=mid+1;
mid=(beg+end)/2;
}
if(a[mid]==target)
{
printf("\n the number is found at position
%2d",mid);
}
else
{
printf("\n the number is not found");
}
getch();
}
```

### Example

The array is given and we want to search the value 123 with the help of binary search method then it is illustrated as follows.

Sorting is the process of putting data in order, either numerically or alphabetically. It is often necessary to arrange the elements in an array in numerical order from highest to lowest values (descending order) or vice versa (ascending order). If the array contains string values, alphabetical order may be needed (which is actually ascending order using ASCII values).

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_278_0.png)

The process of sorting an array requires the exchanging of values. While this seems to be a simple process, a computer must be careful that no values are lost during this exchange. Consider the following dilemma:

Suppose that grade[1] = 10 and grade[2] = 8 and you want to exchange their values so that grade[1] = 8 and grade[2] = 10. You could NOT just do this:

`grade[1] = grade[2];`
`grade[2] = grade[1]; // DOES NOT WORK!!!`

In the first step, the value stored in grade[1] is erased and replaced with grade[2]. The result is that both grade[1] and grade[2] now have the same value. Oops! Then what happened to the value in grade[1]? It is lost!!!

In order to swap two values, you must use a **third variable**, (a “temporary holding variable”), to temporarily hold the value you do not want to lose:

**// swapping variables**
`temp = grade[1]; // holding variable`
`grade[1] = grade[2];`
`grade[2] = temp;`

This process successfully exchanges, “swaps”, the values of the two variables (without the loss of any values).

## WAYS TO SORT ARRAYS

There are literally hundreds of different ways to sort arrays. The basic goal of each of these methods is the same: to compare each array element to another array element and swap them if they are in the wrong position. The bubble sort is one of the easiest algorithms to understand and we will begin our investigation with this sort.

### Bubble Sort

**Bubble sort** is a simple sorting algorithm. It works by repeatedly stepping through the list to be sorted, comparing two items at a time and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted. The algorithm gets its name from the way smaller elements “bubble” to the top of the list. Because it only uses comparisons to operate on elements, it is a comparison sort.

Bubble sorting is a simple sorting technique in sorting algorithm. In bubble sorting algorithm, we arrange the elements of the list by forming pairs of adjacent elements. It means we repeatedly step through the list which we want to sort, compare two items at a time and swap them if they are not in the right order. Another way to visualize the bubble sort algorithm is as its name, the smaller element bubble to the top. Here is the source code implements bubble sorting algorithm in C which sorts an unordered list of integer.

The following program implements the concept of bubble sort for an array.

```c
#include <stdio.h>
#include <stdlib.h>
void swap(int *x,int *y)
{
int temp;
temp = *x;
*x = *y;
*y = temp;
}
}
void bubblesort(int list[], int n)
{
    int i,j;
    for(i=0;i<(n-1);i++)
    for(j=0;j<(n-1-i);j++)
    if(list[j] > list[j+1])
    swap(&list[j],&list[j+1]);
}
void printlist(int list[],int n)
{
    int i;
    for(i=0;i<n;i++)
    printf("%d ",list[i]);
}
void main()
{
    const int MAX_ELEMENTS = 10;
    int list[MAX_ELEMENTS];
    int i = 0;
    // generate random numbers and fill them to the list
    for(i = 0; i < MAX_ELEMENTS; i++) {
        list[i] = rand();
    }
    printf("The list before sorting is:\n");
    printlist(list, MAX_ELEMENTS);
    // sort the list
    bubblesort(list,MAX_ELEMENTS);
    // print the result
    printf("The list after sorting using bubble sorting algorithm:\n");
    printlist(list, MAX_ELEMENTS);
}
```

### Step by Step Example

Let us take the array of numbers “5 1 4 2 8”, and sort the array from lowest number to greatest number using bubble sort algorithm. In each step, elements written in **bold** are being compared.

*First pass*

( 5 1 4 2 8 ) ( 1 5 4 2 8 )
Here, the algorithm compares the first two elements, and swaps them.
( 1 5 4 2 8 ) ( 1 4 5 2 8 )
( 1 4 5 2 8 ) ( 1 4 2 5 8 )
( 1 4 2 5 8 ) ( 1 4 2 5 8 )

Now, since these elements are already in order, the algorithm does not swap them.

*Second pass*
( 1 4 2 5 8 ) ( 1 4 2 5 8 )
( 1 4 2 5 8 ) ( 1 2 4 5 8 )
( 1 2 4 5 8 ) ( 1 2 4 5 8 )
( 1 2 4 5 8 ) ( 1 2 4 5 8 )
Now, the array is already sorted, but our algorithm does not know if it is completed. Algorithm needs one whole pass without any swap to know it is over.

*Third pass*
( 1 2 4 5 8 ) ( 1 2 4 5 8 )
( 1 2 4 5 8 ) ( 1 2 4 5 8 )
( 1 2 4 5 8 ) ( 1 2 4 5 8 )
Finally, the array is sorted, and the algorithm can terminate.

## Programming Problems

### Problem 1

Write a program to input 10 numbers and then sort that numbers in ascending order.

### Solution

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a[10],i,j,temp;
    clrscr();
    for(i=0;i<10;i++)
    {
        printf("\n enter the element");
        scanf("%d",&a[i]);
    }
    for(i=0;i<10;i++)
    {
        for(j=i+1;j<10;j++)
        {
            if(a[i]>a[j])
            {
                temp=a[i];
                a[i]=a[j];
                a[j]=temp;
            }
        }
    }
    printf("\n the sorted array in ascending order is");
}
```
