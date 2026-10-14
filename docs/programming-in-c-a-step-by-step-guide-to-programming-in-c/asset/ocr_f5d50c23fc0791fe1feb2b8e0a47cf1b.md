```
```c
printf("Enter the data values to be placed in a node\n");
scanf("%d", &x);
start = insert(start, x);
}
printf("The created list is\n");
printlist(start);
}
```
```

# 12.4.1 Inserting a node by using Recursive Programs

A linked list is a recursive data structure. A *recursive data structure* is a data structure that has the same form regardless of the size of the data. You can easily write recursive programs for such data structures.

# Program 12.3

```
```c
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *link;
};

struct node *insert(struct node *p, int n)
if(p == NULL)
{
    p = (struct node *)malloc(sizeof(struct node));
    if(p == NULL)
    {
        printf("Error\n");
```
```