The preceding array can be shown as follows:

| 1 | 100 | 2 | 200 | 3 | 300 | 4 | 400 |
|---|---|---|---|---|---|---|---|
| [0][0] | [0][1] | [1][0] | [1][1] | [2][0] | [2][1] | [3][0] | [3][1] |
| 8000 | 8001 | 8002 | 8003 | 8004 | 8005 | 8006 | 8007 |

Dimensions are just conceptual design. In the memory, the preceding array elements are stored in a contiguous manner; for example, 1 is stored at the location [0][1], 100 is stored at the location [0][1], and 2 is stored at the location [1][0]. This scheme is referred to as a row major order of representing an array in memory. However, there is another representation as well which is called column major representation. Let’s discuss the significant differences between the two representations. Figure 4.2 shows the two representations of a two-dimensional array:

**Row Major Representation**

| Row | Col | Info |
|---:|---:|---:|
| 0 | 0 | 1 |
| 0 | 1 | 100 |
| 1 | 0 | 2 |
| 1 | 1 | 200 |
| 2 | 0 | 3 |
| 2 | 1 | 300 |
| 3 | 0 | 4 |
| 3 | 1 | 400 |

**Column Major Representation**

| Row | Col | Info |
|---:|---:|---:|
| 0 | 0 | 1 |
| 1 | 0 | 100 |
| 0 | 1 | 2 |
| 1 | 1 | 200 |
| 0 | 2 | 3 |
| 1 | 2 | 300 |
| 0 | 3 | 4 |
| 1 | 3 | 400 |

**Figure 4.2: Showing the Row Major and Column Major Representations**

The major difference between the two representations is the way the elements are stored in a two-dimensional array. In a row major representation, after element a[0][0], the next element to be found is element a[0][1]; whereas, in a column major representation, the next element to be found is element a[1][0].

# ## Exploring Pointer Arithmetic in Two-Dimensional Array

As already discussed, a two-dimensional array can be considered as a collection of single dimensional arrays. Therefore, typical declaration, such as int arr[3][3], would mean that arr[0] will give the base address of the first single dimensional array, arr[1] will give the address of the second single dimensional array, and arr[2] will give the address of the third single dimensional array. Listing 4.7 shows the base address calculation for a two-dimensional array:

**Listing 4.7: Showing the Base Address Calculation for a Two-Dimensional Array**

```
```c
# include <stdio.h>

int main()
{
    int i;
    int arr[3][3] = {
                    {1,100,1000},
                    {2,200,2000},
                    {3,300,3000}
```
```