# 7.4.12 /* Reversing a Linked List */

```
#include <stdio.h>
#include <alloc.h>
struct link
{
    int info;
    struct link *next;
};
int i, no;
struct link *start, *pnode, *previous, *current, *counter;
void display(struct link *);
void create(struct link *);
struct link * reverse(struct link *);
void main()
{
    struct link *node;
    struct link *p;
    node = (struct link *) malloc(sizeof(struct link));
    create(node);
    printf("\n Original List is as follows:\n");
    display(node);
    p = (struct link *)malloc(sizeof(struct link));
    p = reverse(node);
    printf("\n After reverse operation list is as follows:\n");
    display(p);
}
struct link * reverse(struct link *start)
{
    current = start;
    previous = NULL ;
    while( current != NULL )
    {
        counter = (struct link*)malloc(sizeof(struct link));
        counter = current->next ;
        current->next = previous ;
        previous = current ;
        current = counter ;
    }
    start = previous;
    return(start);
}
void display(struct link *node)
{
    while ( node != NULL)
    {
```