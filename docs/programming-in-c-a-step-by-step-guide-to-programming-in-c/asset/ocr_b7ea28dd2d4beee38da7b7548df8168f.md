available on an array. The limitation of an array implementation is that the queue cannot grow and shrink dynamically as per the requirement.

# Program 14.5: A complete C program to implement a queue by using an array is shown here

```
#include <stdio.h>
#define MAX 10 /* The maximum size of the queue */
#include <stdlib.h>

void insert(int queue[], int *rear, int value)
{
if(*rear < MAX-1)
{
*rear= *rear +1;
queue[*rear] = value;
}
else
{
printf("The queue is full can not insert a value\n");
exit(0);
}
}

void delete(int queue[], int *front, int rear, int * value)
{
if(*front == rear)
```