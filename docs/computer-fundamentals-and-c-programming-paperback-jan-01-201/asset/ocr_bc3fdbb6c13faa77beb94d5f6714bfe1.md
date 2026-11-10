a pointer to int. Thus, the expression *table is equivalent to &table[0][0] while the expression **table evaluates to the element table[0][0].

We’ll now derive a general expression that points to the element table[i][j]. Note that table and table[0] have the same address but of different objects. Adding 1 to table creates a pointer to table[1], but adding 1 to table[0] creates a pointer to table[0][1]. Thus, in the general case, table[i] + j is equivalent to &table[i][j]. But then table[i] is the same as *(table + i), so &table[i][j] can be represented in pointer notation as

```
*(table + i) + j
```

When we dereference the preceding expression, the resultant expression evaluates to the value of the element table[i][j]:

```
*(*(table + i) + j)
```

Array notation is simpler to use but you should also feel comfortable with pointer notation used in the following program (Program 12.14). This program populates a two-dimensional array with **scanf** using the pointer expression that was just derived. **printf** simply dereferences the same expression to print all array elements.

The annotations provided in the first three lines of output adequately explain the significance of the sizes of three objects determined by **sizeof**. Further, observe that the expressions **(table + 1) and **(table + 2) correctly move the pointer by increments of one row. *The compiler must know the number of columns of an array for such arithmetic to be possible.* Finally, the last loop establishes that table is actually a one-dimensional array. Because the elements of each row are contiguously laid out, the expression p + i could sequentially access all 15 elements.

```
```c
/* pointers_in_2darray.c: Uses scanf and printf with pointer notation
                              to initialize and print a 2D array. */
#define ROWS 3
#define COLUMNS 5
#include <stdio.h>
int main(void)
{
    int i, j;
    int table[ROWS][COLUMNS];
    int *p = &table[0][0];

    printf("Size of table = %d\n", sizeof(table));
    printf("Size of table[0] = %d\n", sizeof(table[0]));
    printf("Size of table[0][0] = %d\n", sizeof(table[0][0]));

    printf("\nKey in %d integers: ", ROWS * COLUMNS);
    for (i = 0; i < ROWS; i++)
        for (j = 0; j < COLUMNS; j++)
            scanf("%d", *(table + i) + j);
```
```