```
/* insert_element.c: Inserts element at specified location in an array. */
#include <stdio.h>
int main (void)
{
    short i, j, num, new_value, arr[20];

    printf("Number of integers to input? ");
    scanf("%hd", &num);

    printf("Key in %hd numbers: ", num);
    for (i = 0; i < num; i++)
        scanf("%hd", &arr[i]);

    printf("Enter desired index at insertion and inserted value: ");
    scanf("%hd%hd", &j, &new_value);

    /* Section for shifting elements to right and insertion of element */
    for (i = num; i > j; i--)            /* arr[num] is last element plus one */
        arr[i] = arr[i - 1];              /* Moves a group of elements to right */
    arr[i] = new_value;                   /* Inserts new value at index j */

    for (i = 0; i <= num; i++)            /* Now <= because of an extra element */
        printf("%hd ", arr[i]);
    return 0;
}
```

PROGRAM 10.3: **insert_element.c**

```
Number of integers to input? 6
Key in 6 numbers: 11 22 33 55 66 77
Enter desired index at insertion and inserted value: 3 44
11 22 33 44 55 66 77
```

PROGRAM OUTPUT: **insert_element.c**

# 10.5.2  `delete_element.c`: Deleting an Element from an Array

Deletion of an element is equally simple and can be achieved with a similar but inverse line of reasoning. Just move to the specified location as before, and then shift to the left all elements from that location to the end of the array. Program 10.4 achieves this task. This time we use the technique discussed in Section 10.4 which populates an array without knowing the number of elements needed. This program too is well-documented, so no further explanation is provided.

Large arrays are often sorted for faster access. Insertion and deletion of elements in a sorted array require additional programming effort. Because a user can’t specify the insertion or deletion point for a sorted array, the program has to locate it. After you have learned to search an array, these tasks will be within your grasp.