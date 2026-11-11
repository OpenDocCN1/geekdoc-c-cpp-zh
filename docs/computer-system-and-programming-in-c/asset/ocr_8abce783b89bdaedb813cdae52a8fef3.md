```
```c
for(i=0;i<10;i++)
{
    printf("\n%d",a[i]);
}
getch();
```
```

# Problem 2

Write a program to input 10 numbers and then sort that numbers in descending order.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a[10],i,j,temp;
    clrscr();
    for(i=0;i<10;i++)
    {
        printf("\n enter the element");
        scanf("%d",&a[i]);
    }
    for(i=0;i<10;i++)
    {
        for(j=i+1;j<10;j++)
        {
            if(a[i]<a[j])
            {
                temp=a[i];
                a[i]=a[j];
                a[j]=temp;
            }
        }
    }
    printf("\n the sorted array in descending order is");
    for(i=0;i<10;i++)
    {
        printf("\n%d",a[i]);
    }
    getch();
}
```
```

# SUMMARY

+   - The most important application of pointer is dynamic memory allocation.
+   - If we want to allocate the memory at the run time then this concept is known as dynamic memory allocation.

+   - malloc(), calloc, free and realloc() are the predefined functions for dynamic memory allocation.
+   - The general syntax of malloc() function is as follows:
+   
+     `<pointer variable>=(<data type *) malloc (number of elements * sizeof(data type));`
+   - The general syntax of calloc() function is as follows:
+   
+     `<pointer variable>=(<data type *) malloc (number of elements, sizeof(data type));`
+   - Stack is a data structure which follow the concept of last in first out (LIFO).
+   - Push is a function which is used to insert an element into the stack.
+   - Pop is a function which is used to delete the top most element from the stack.
+   - Linked list is the collection of nodes and every node is divided into two parts (a) information part, (b) address of the next node.
+   - Sequential search means we want to search the data linearly.
+   - Binary search is only implemented when the data is sorted either in ascending order or in descending order.

# Exercises

# Section A

*Multiple Choice Questions*

+   1. We can allocate memory at run time by using
+      (a) malloc
+      (b) calloc
+      (c) realloc
+      (d) All of the above
+   
+   2. In stack insertion and deletion can be done at
+      (a) Top
+      (b) Bottom
+      (c) Both a and b
+      (d) None of the above
+   
+   3. The syntax of calloc function is
+      (a) void *calloc(size_t size_t);
+      (b) void *calloc(size_t numElements, size_t sizeOfElements);