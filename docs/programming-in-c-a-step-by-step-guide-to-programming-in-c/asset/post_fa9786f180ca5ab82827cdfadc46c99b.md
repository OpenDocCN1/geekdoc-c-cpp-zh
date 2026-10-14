
## 12.4 The Concept of Linked List

When dealing with many problems we need a dynamic list, dynamic in the sense that the size requirement need not be known at compile time. Thus, the list may grow or shrink during runtime. A linked list is a data structure that is used to model such a dynamic list of data items, so the study of the linked lists as one of the data structures is important.

An array is represented in memory using sequential mapping, which has the property that elements are fixed distance apart. But this has the following disadvantage: It makes insertion or deletion at any arbitrary position in an array a costly operation, because this involves the movement of some of the existing elements.

When we want to represent several lists by using arrays of varying size, either we have to represent each list using a separate array of maximum size or we have to represent each of the lists using one single array. The first one will lead to wastage of storage, and the second will involve a lot of data movement.

So we have to use an alternative representation to overcome these disadvantages. One alternative is a linked representation. In a linked representation, it is not necessary that the elements be at a fixed distance apart. Instead, we can place elements anywhere in memory, but to make it a part of the same list, an element is required to be linked with a previous element of the list. This can be done by storing the address of the next element in the previous element itself. This requires that every element be capable of holding the data as well as the address of the next element. Thus every element must be a structure with a minimum of two fields, one for holding the data value, which we call a data field, and the other for holding the address of the next element, which we call link field.

Therefore, a linked list is a list of elements in which the elements of the list can be placed anywhere in memory, and these elements are linked with each other using an explicit link field, that is, by storing the address of the next element in the link field of the previous element.

### Program 12.2: Here is a program for building and printing the elements of the linked list

```c
# include <stdio.h>
# include <stdlib.h>
struct node
{
int data;
struct node *link;
};
struct node *insert(struct node *p, int n)
{
struct node *temp;
/* if the existing list is empty then insert a new node as the
starting node */
if(p == NULL)
{
p=(struct node *)malloc(sizeof(struct node)); /* creates new node data value passes as parameter */
if(p == NULL)
{
printf("Error\n");
exit(0);
}
p-> data = n;
p-> link = p; /* makes the pointer pointing to itself because it
is a circular list*/
}
else
{
temp = p;
/* traverses the existing list to get the pointer to the last node of it */
while (temp-> link != p)
temp = temp-> link;
temp-> link = (struct node *)malloc(sizeof(struct node)); /* creates new node using data value passes as parameter and
puts its address in the link field of last node of the existing list*/ if(temp -> link == NULL)
{
printf("Error\n");
exit(0);
}
temp = temp-> link;
temp-> data = n;
temp-> link = p;
}
return (p);
}
void printlist ( struct node *p )
{
struct node *temp;
temp = p;
printf("The data values in the list are\n");
if(p!= NULL)
{
    do
    {
        printf("%d\t",temp->data);
        temp=temp->link;
    } while (temp!= p);
}
else
    printf("The list is empty\n");
}
void main()
{
    int n;
    int x;
    struct node *start = NULL;
    printf("Enter the nodes to be created \n");
    scanf("%d",&n);
    while ( n -- > 0)
    {
printf("Enter the data values to be placed in a node\n");
scanf("%d", &x);
start = insert(start, x);
}
printf("The created list is\n");
printlist(start);
}
```

### 12.4.1 Inserting a node by using Recursive Programs

A linked list is a recursive data structure. A *recursive data structure* is a data structure that has the same form regardless of the size of the data. You can easily write recursive programs for such data structures.

### Program 12.3

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
exit(0);
}
p-> data = n;
p-> link = NULL;
}
else
p->link = insert(p->link,n);/* the while loop replaced by recursive call */
return (p);
}
void printlist ( struct node *p )
{
printf("The data values in the list are\n");
while (p!= NULL)
{
printf("%d\t",p-> data);
p = p-> link;
}
}
void main()
{
int n;
int x;
struct node *start = NULL ;
printf("Enter the nodes to be created \n");
scanf("%d",&n);
while (n-- > 0)
{
    printf("Enter the data values to be placed in a node\n"); scanf("%d",&x);
    start = insert( start,x);
}
printf("The created list is\n");
printlist( start);
}
```

### 12.4.2 Sorting and reversing a linked list

To sort a linked list, first we traverse the list searching for the node with a minimum data value. Then we remove that node and append it to another list which is initially empty. We repeat this process with the remaining list until the list becomes empty, and at the end, we return a pointer to the beginning of the list to which all the nodes are moved.

To reverse a list, we maintain a pointer each to the previous and the next node, then we make the link field of the current node point to the previous, make the previous equal to the current, and the current equal to the next.

Therefore, the code needed to reverse the list is

```c
Prev = NULL;
While (curr != NULL)
{
Next = curr->link;
Curr -> link = prev;
Prev = curr;
Curr = next;
}
```

### Program 12.4: Example in sorting lists.

```c
# include <stdio.h>
# include <stdlib.h>
struct node
{
int data;
struct node *link;
};
struct node *insert(struct node *p, int n)
if(p==NULL)
{
p=(struct node *)malloc(sizeof(struct node));
if(p==NULL)
{
printf("Error\n");
exit(0);
}
}
p-> data = n;
p-> link = NULL;
}
else
{
temp = p;
while (temp-> link!= NULL)
temp = temp-> link;
temp-> link = (struct node *)malloc(sizeof(struct node)); if(temp -> link == NULL)
{
printf("Error\n");
exit(0);
}
temp = temp-> link;
temp-> data = n;
temp-> link = NULL;
}
return(p);
}
void printlist ( struct node *p )
{
printf("The data values in the list are\n"); while (p!= NULL)
{
printf("%d\t",p-> data);
p = p-> link;
}
}
/* a function to sort reverse list */ struct node *reverse(struct node *p) {
struct node *prev,*curr;
prev = NULL;
curr = p;
while (curr != NULL)
{
p = p-> link;
curr-> link = prev;
prev = curr;
curr = p;
}
return(prev);
}
/* a function to sort a list */
struct node *sortlist(struct node *p) {
struct node *temp1,*temp2,*min,*prev,*q; q = NULL;
while(p != NULL)
{
prev = NULL;
min = temp1 = p;
temp2 = p -> link;
while ( temp2 != NULL )
{
if(min -> data > temp2 -> data)
{
min = temp2;
prev = temp1;
} temp1 = temp2;
temp2 = temp2-> link;
}
if(prev == NULL)
p = min -> link;
else
prev -> link = min -> link;
min -> link = NULL;
if( q == NULL )
q = min; /* moves the node with lowest data value in the list pointed to by p to the list pointed to by q as a first node */
else
{
temp1 = q;
/* traverses the list pointed to by q to get pointer to its
last node */
while( temp1 -> link != NULL)
temp1 = temp1 -> link;
temp1 -> link = min; /* moves the node with lowest data value in the list pointed to by p to the list pointed to by q at the
end of list pointed by q */ }
}
return (q);
}
void main()
{
int n;
int x;
struct node *start = NULL ;
printf("Enter the nodes to be created \n"); scanf("%d",&n);
while ( n-- > 0 )
{
printf( "Enter the data values to be placed in a node\n");
scanf("%d",&x);
start = insert ( start,x);
}
printf("The created list is\n");
```
