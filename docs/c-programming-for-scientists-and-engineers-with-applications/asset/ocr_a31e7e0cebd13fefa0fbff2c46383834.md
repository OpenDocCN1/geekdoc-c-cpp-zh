# 444 One-Dimensional Arrays

```
****************************************************
/*
 * funcncubble: Bubble Sort
 */
****************************************************
/* Local Variables: */
 *   temp            - storage to hold array element  */
/* Input/Output Parameters: */
 *   array[n]        - array                          */
 *   n               - size of array                   */
****************************************************
void funcncubble(float array[ ], int n)
{
    float temp;
    int i, j;
    for (i = 1; i < n; i++)
    {
        for(j = n - 1; j >= i; j--)
        {
            if(array1[j] > array1[j])
            {
                temp = array1[j];
                array1[j] = array1[j - 1];
                array1[j - 1] = temp;
            }
        }
    }
    return;
}
Input and Output
====================
Enter ten values to be sorted:
12.0 56.0 76.0 98.0 34.5 65.3 76.2 81.5 95.7 86.9
Sorted Array:
98.00 95.70 86.90 81.50 76.20 76.00 65.30 56.00 34.50 12.00
```

# Optimized Bubble Sort

Pseudocode

Function funcoptbubble(optimized bubble sort)