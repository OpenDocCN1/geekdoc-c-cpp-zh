# Chapter 24

The Sequential_Search() function returns the index of a list and compares each single list element with the key value until the match is found. In the algorithm, A[] is the input array and key represents the element to be searched. The function loops through each element of the array A[] until it finds an element that matches to the element key. If it finds the match, then it breaks the loop; otherwise, the loop continues to execute.

In the sequential search, the best case is the one where the key value is the first element in the list. In this case, only one comparison is required. On the other hand, the worst case is the one where the key value is the last list element or the key does not exist in the list. In this case, each list element needs to be compared with the key value. Therefore, in the best case, the time required to perform the search is O(1); whereas, in the worst case, the time required to perform the search operation is O(n), where n is the length of the array element. Similarly, in the average case, the key element will be at the middle of the list. Therefore, the time required to perform the search operation is O(n/2), which is nothing but O(n), where n is the length of the list. The case analysis of the sequential search is as follows:

+   - **Best Case:** O(1)
+   - **Worst Case:** O(n)
+   - **Average Case:** O(n/2) ≈ O(n)

Listing 24.43 shows the implementation of sequential search in C:

# Listing 24.43: Showing the Code for Sequential Search

```
```c
#include<stdio.h>

void main()
{
    int a[100], key, i, limit, pos=0;
    printf("Enter limit for Sequential search\n");
    scanf("%d",&limit);
    printf("Enter %d elements\n",l);
    for(i=0;i<limit;i++)
    {
        scanf("%d",&a[i]);
    }
    printf("Enter a number to be search\n");
    scanf("%d",&key);
    for(i=0;i<limit;i++)
    {
        if(a[i]==key)
        {
            pos=i+1;
            break;
        }
    }
    if(pos!=0)
        printf("%d is found in the list, at position %d\n",key,pos);
    else
        printf("%d is not in the list\n",key);
}
```
```

In the sequential search, as the list is unsorted, all the elements are compared in case of searching against a key value. However, this situation might completely change if the list is already sorted. Therefore, binary search is used to implement the searching technique on a sorted list.

Let’s learn about binary search, in detail.