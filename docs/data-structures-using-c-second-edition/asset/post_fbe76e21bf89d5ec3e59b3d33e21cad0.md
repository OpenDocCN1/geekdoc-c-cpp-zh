
```c
else if (arr[mid] > num)
    end = mid - 1;
else
    beg = mid + 1;
}
if (beg > end && found == 0)
    printf("\n %d does not exist in the array", num);
return 0;
}
int smallest(int arr[], int k, int n)
{
    int pos = k, small = arr[k], i;
    for (i = k + 1; i < n; i++)
    {
        if (arr[i] < small)
        {
            small = arr[i];
            pos = i;
        }
    }
    return pos;
}
void selection_sort(int arr[], int n)
{
    int k, pos, temp;
    for (k = 0; k < n; k++)
    {
        pos = smallest(arr, k, n);
        temp = arr[k];
        arr[k] = arr[pos];
        arr[pos] = temp;
    }
}
```

## 14.4 INTERPOLATION SEARCH

Interpolation search, also known as extrapolation search, is a searching technique that finds a specified value in a sorted array. The concept of interpolation search is similar to how we search for names in a telephone book or for keys by which a book's entries are ordered. For example, when looking for a name “Bharat” in a telephone directory, we know that it will be near the extreme left, so applying a binary search technique by dividing the list in two halves each time is not a good idea. We must start scanning the extreme left in the first pass itself.

![](img/be6359df08208122bec6fad1103de211_441_0.png)

Figure 14.3 Algorithm for interpolation search

In each step of interpolation search, the remaining search space for the value to be found is calculated. The calculation is done based on the values at the bounds of the search space and the value to be searched. The value found at this estimated position is then compared with the value being searched for. If the two values are equal, then the search is complete.

However, in case the values are not equal then depending on the comparison, the remaining search space is reduced to the part before or after the estimated position. Thus, we see that interpolation search is similar to the binary search technique. However, the important difference between the two techniques is that binary search always selects the middle value of the remaining search space. It discards half of the values based on the comparison between the value found at the estimated position and the value to be searched. But in interpolation search, interpolation is used to find an item near the one being searched for, and then linear search is used to find the exact item.

The algorithm for interpolation search is given in Fig. 14.3.

Figure 14.4 helps us to visualize how the search space is divided in case of binary search and interpolation search.

![](img/be6359df08208122bec6fad1103de211_442_0.png)

Figure 14.4 Difference between binary search and interpolation search

### Complexity of Interpolation Search Algorithm

When n elements of a list to be sorted are uniformly distributed (average case), interpolation search makes about log(log n) comparisons. However, in the worst case, that is when the elements increase exponentially, the algorithm can make up to O(n) comparisons.

### Example 14.1

Given a list of numbers a[] = { 1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21}. Search for value 19 using interpolation search technique.

**Solution**
Low = 0, High = 10, VAL = 19, a[Low] = 1, a[High] = 21
Middle = Low + (High - Low)×((VAL - a[Low]) / (a[High] - a[Low]))
= 0 + (10 - 0) × ((19 - 1) / (21 - 1))
= 0 + 10 × 0.9 = 9
a[middle] = a[9] = 19 which is equal to value to be searched.

### PROGRAMMING EXAMPLE

- 3. Write a program to search an element in an array using interpolation search.

```c
#include <stdio.h>
#include <conio.h>
#define MAX 20
int Interpolation_search(int a[], int low, int high, int val)
{
    int mid;
    while(low < high)
    {
        mid = low + (high - low)*(val - a[low]) / (a[high] - a[low]);
        if(val == a[mid])
        return mid;
        if(val < a[mid])
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}
int main()
{
    int arr[MAX], i, n, val, pos;
    clrscr();
    printf("\n Enter the number of elements in the array : ");
    scanf("%d", &n);
    printf("\n Enter the elements : ");
    for(i = 0; i < n; i++)
    scanf("%d", &arr[i]);
    printf("\n Enter the value to be searched : ");
    scanf("%d", &val);
    pos = Interpolation_search(arr, 0, n-1, val);
    if(pos == -1)
    printf("\n %d is not found in the array", val);
    else
    printf("\n %d is found at position %d", val, pos);
    getche();
    return 0;
}
```

## 14.5 JUMP SEARCH

When we have an already sorted list, then the other efficient algorithm to search for a value is jump search or block search. In jump search, it is not necessary to scan all the elements in the list to find the desired value. We just check an element and if it is less than the desired value, then some of the elements following are skipped by jumping ahead. After moving a little forward again, the element is checked. If the checked element is greater than the desired value, then we have a boundary and we are sure that the desired value lies between the previously checked element and the currently checked element. However, if the checked element is less than the value being searched for, then we again make a small jump and repeat the process.

Once the boundary of the value is determined, a linear search is done to find the value and its position in the array. For example, consider an array a[] = {1,2,3,4,5,6,7,8,9}. The length of the array is 9. If we have to find value 8 then following steps are performed using the jump search technique:

Step 1: First three elements are checked. Since 3 is smaller than 8, we will have to make a jump ahead

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|

Step 2: Next three elements are checked. Since 6 is smaller than 8, we will have to make a jump ahead

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|

Step 3: Next three elements are checked. Since 9 is greater than 8, the desired value lies within the current boundary

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|

Step 4: A linear search is now done to find the value in the array.

The algorithm for jump search is given in Fig. 14.5.

```
JUMP_SEARCH ( A, lower_bound, upper_bound, VAL, N )
Step 1: [INITIALIZE] SET STEP = sqrt(N), I = 0, LOW = lower_bound, HIGH = upper_bound, POS = -1
Step 2: Repeat Step 3 while I < STEP
Step 3:
    IF VAL < A[STEP]
        SET HIGH = STEP - 1
    ELSE
        SET LOW = STEP + 1
        [END OF IF]
        SET I = I + 1
    [END OF LOOP]
Step 4: SET I = LOW
Step 5: Repeat Step 6 while I <= HIGH
Step 6:
    IF A[I] = VAL
        POS = I
        PRINT POS
        GO TO Step 8
    [END OF IF]
    SET I = I + 1
[END OF IF]
Step 7: IF POS = -1
    PRINT "VALUE IS NOT PRESENT IN THE ARRAY"
[END OF IF]
Step 8: EXIT
```

Figure 14.5 Algorithm for jump search

### Advantage of Jump Search over Linear Search

Suppose we have a sorted list of 1000 elements where the elements have values 0, 1, 2, 3, 4, ..., 999, then sequential search will find the value 674 in exactly 674 iterations. But with jump search, the same value can be found in 44 iterations. Hence, jump search performs far better than a linear search on a sorted list of elements.

### Advantage of Jump Search over Binary Search

No doubt, binary search is very easy to implement and has a complexity of O(log n), but in case of a list having very large number of elements, jumping to the middle of the list to make comparisons is not a good idea because if the value being searched is at the beginning of the list then one (or even more) large step(s) in the backward direction would have to be taken. In such cases, jump search performs better as we have to move little backward that too only once. Hence, when jumping back is slower than jumping forward, the jump search algorithm always performs better.

### How to Choose the Step Length?

For the jump search algorithm to work efficiently, we must define a fixed size for the step. If the step size is 1, then search is same as linear search. Now, in order to find an appropriate step size, we must first try to figure out the relation between the size of the list (n) and the size of the step (k). Usually, k is calculated as √n.

### Further Optimization of Jump Search

Till now, we were dealing with lists having small number of elements. But in real-world applications, lists can be very large. In such large lists searching the value from the beginning of the list may not be a good idea. A better option is to start the search from the k-th element as shown in the figure below.
