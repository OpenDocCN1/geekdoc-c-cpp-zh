individual items. The very idea of using a linked list is to avoid any reference to specific number of items in the list so that we can insert or delete items as and when necessary. This can be achieved by using “anonymous” locations to store nodes. Such locations are accessed not by name, but by means of pointers which refer to them. (For example, we must avoid using references like node1.age and node1.next -> age.)

Anonymous locations are created using pointers and dynamic memory allocation functions such as malloc. We use a pointer head to create and access anonymous nodes. Consider the following:

```
struct linked_list
{
    int number;
    struct linked_list *next;
};
typedef struct linked_list node;
node *head;
head = (node *) malloc(sizeof(node));
```

The struct declaration merely describes the format of the nodes and does not allocate storage. Storage space for a node is created only when the function malloc is called in the statement

```
head = (node *) malloc(sizeof(node));
```

This statement obtains a piece of memory that is sufficient to store a node and assigns its address to the pointer variable head. This pointer indicates the beginning of the linked list.

![](bbox=[0.15, 0.79, 0.88, 0.9])

The following statements store values in the member fields:

```
head -> number = 10;
head -> next   = NULL;
```

![](bbox=[0.15, 0.97, 0.88, 1.0])

The second node can be added as follows:

```
head->next = (node *)malloc(sizeof(node));
head->next->number = 20;
head->next->next = NULL;
```