# 5.3 Binary Search

The *binary search algorithm* is one of the most efficient searching techniques, which requires the list to be sorted in ascending order. To *search for an element* in the list, the binary search algorithm splits the list and locates the middle element of the list. It is then compared with the search element. If the search element is less than the middle element, the first part of the list is searched else the second part is searched. The algorithm again reduces the list into two halves, locates the middle element, and compares with the search element. If the search list is less than the middle element, the first part of the list is searched. This process continues until the search element is equal to the middle element or the list consists of only one element that is not equal to the search element.

```
Algorithm for Binary Search
BINARY_SEARCH (ARR, FIND, BEG, END)
where ARR is an array in which the element FIND is to be searched, BEG refers
to the initial index position of the list, END refers to the final position of the list.
Step 1 : If (BEG > END) Then
    RETURN –1
    [End of If structure]
Step 2 : Assign MID = (BEG + END) / 2
Step 3 : If (FIND = ARR(MID)) Then
    RETURN MID
Else If (FIND < ARR(MID)) Then
    RETURN BINARY_SEARCH (ARR, FIND, BEG, MID–1)
Else
    RETURN BINARY_SEARCH (ARR, FIND, MID+1, END)
    [End of If structure]
END BINARY_SEARCH()
```

```
Program_5.2 :
/* Program to search an element using binary search. */
/* binaries.c * /
#include<stdio.h>
int binary_search(int [], int, int, int);
void main()
{
int i, n, flnd, pos = 0, list[100];
printf("Enter the limit : ");
scanf("%d", &n);
```