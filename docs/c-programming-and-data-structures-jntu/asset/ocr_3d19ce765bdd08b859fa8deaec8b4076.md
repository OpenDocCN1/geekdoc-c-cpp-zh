```
```c
#include <stdlib.h>
#include <stdio.h>
#define MAXSIZE 500
void selection(int elements[], int maxsize);
int elements[MAXSIZE],maxsize;
int main()
{
int i;
printf("\nHow many elements you want to sort: ");
scanf("%d",&maxsize);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i :");
scanf("%d",&elements[i]);
}
printf("\nArray before sorting:\n");
for (i = 0; i < maxsize; i++)
printf("%d ",elements[i]);
printf ("\n");
selection(elements, maxsize);
printf("\nArray after sorting:\n");
for (i = 0; i < maxsize; i++)
{
printf("[%i]", elements[i]);
}
void selection(int elements[], int array_size)
{
int i, j, k;
int min, temp;
for (i = 0; i < maxsize-1; i++)
{
min = i;
for (j = i+1; j < maxsize; j++)
{
if (elements[j] < elements[min])
min = j;
}
temp = elements[i];
elements[i] = elements[min];
elements[min] = temp;
}
}
```
```

Fig. 17.3 C program for selection sorting