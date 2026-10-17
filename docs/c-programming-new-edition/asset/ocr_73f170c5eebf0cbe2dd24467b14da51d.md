```
```c
printf(“Enter the elements of the first array in sorted order: “);
for (int i = 0; i < N; i++)
{
    scanf(“%d”, &arr1[i]);
}
printf(“Enter the size of the second array (M): “);
scanf(“%d”, &M);
int arr2[M];
printf(“Enter the elements of the second array in sorted order: “);
for (int i = 0; i < M; i++)
{
    scanf(“%d”, &arr2[i]);
}
printf(“Enter the value of k: “);
scanf(“%d”, &k);
int kthElement = findKthElement(arr1, N, arr2, M, k);
if (kthElement != -1)
{
    printf(“The k-th element in the merged array is: %d\n”, kthElement);
}
else
{
    printf(“Invalid input. The k-th element is out of bounds.\n”);
}
return 0;
}
```
```

+   - **Practical 28:** Write a c program to take multiline string input and print individual string length.
+   - **Solution:**

```
```c
#include <stdio.h>
#include <string.h>
int main()
```
```