![](bbox=[0.408, 0.122, 0.629, 0.226])

**Figure 6.43:** State of the array after the first cycle of right rotation

Note that 10, which was the first element of the array, has become the last element and rest of the elements are shifted ahead as seen in Figure 6.43. If you apply another cycle of right rotation, the new state of the array will be as shown below:

![](bbox=[0.411, 0.379, 0.629, 0.481])

**Figure 6.44:** State of the array after the second cycle of right rotation

Hence after two cycles, 30 becomes the first element of the array and 20 becomes the last element as seen in Figure 6.44. Number of cycles to be applied to an array is specified by a rotation factor. The program should apply m cycles of rotation to an array a if the rotation factor is m . The program should take the following as input from the user:

+   1. Size of an array a .
+   2. Elements of an array a .
+   3. Rotation factor m to specify number of cycles of right rotation to be applied to array a .

Program should print the resultant array a on the computer screen after applying m rotation cycles.

```
#include<stdio.h>
void main()
{
    int n, i, k, m, temp[100], a [100];
    printf("How many elements are to be stored in the array\n");
```