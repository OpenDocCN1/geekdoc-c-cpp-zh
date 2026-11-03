```
```c
int elements[MAXSIZE],maxsize;
int main()
{
int i;
printf("\nHow many elements you want to sort: ");
scanf("%d",&maxsize);
printf("\nEnter the values one by one: ");
for (i = 0; i < maxsize; i++)
{
printf ("\nEnter element %i :",i);
scanf("%d",&elements[i]);
}
printf("\nArray before sorting:\n");
for (i = 0; i < maxsize; i++)
printf("[%d]", elements[i]);
printf ("\n");
insertionsort(elements, maxsize);
printf("\nArray after sorting:\n");
for (i = 0; i < maxsize; i++)
printf("[%d]", elements[i]);
}
void insertionsort(int elements[], int maxsize)
{
int i, j, index;
for (i=1; i < maxsize; i++)
{
index = elements[i];
j = i;
while ((j > 0) && (elements[j-1] > index))
{
elements[j] = elements[j-1];
j = j - 1;
}
elements[j] = index;
}
}
```
```

Fig. 17.6 C program for insertion sort

# 2. Efficiency of insertion sort

Let us now analyze the efficiency of the selection sort. Assuming there are n elements in the array, we must pass through n − 1 entry. For each entry, we may need to examine and shift a maximum of n − 1 other entries, resulting in a efficiency of O(n²).