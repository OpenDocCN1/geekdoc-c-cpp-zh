# Output

![](bbox=[0.117, 0.142, 0.873, 0.382])

By using functions

```
#include<stdio.h>
#include<math.h>
#define SIZE 20
//Function prototypes
void FillArray(int *array,int size);
void PrintArray(int *array,int size);
void BubbleSort(int *array,int size);
void swap(int *x,int *y);
//driver program
int main()
{
    int NumList[SIZE],i;
    FillArray(&NumList,SIZE);
    printf("\n Before sort array elements are :\n");
    PrintArray(&NumList,SIZE);
    BubbleSort(&NumList,SIZE);
    printf("\n After sort array elements are :\n");
    PrintArray(&NumList,SIZE);
}
//code for fillarray()
void FillArray(int *array,int size)
{
    int i;
    for(i=0;i<SIZE;i++)
    *(array+i)= rand() % 100 ; //generate 20 random
    numbers and assigned to array
}
//logic for printing the array elements
void PrintArray(int *array,int size)
```