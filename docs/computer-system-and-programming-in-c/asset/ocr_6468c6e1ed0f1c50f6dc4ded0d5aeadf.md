```
item = pop (top) ;
printf (“%d “, item) ;
stack_display (top) ;
printf (“No. of items in stack = %d”, count
(top)) ;
```

```
/* traverse the entire linked list */
while (q != NULL)
{
    q = q -> next ;
    C++;
}
return c ;
}
```

```
/* adds a new element on the top of stack */
void push (struct node *top, int item)
{
    struct node *q ;
    q = (struct node *) malloc (sizeof (struct
    node)) ;
    q -> data = item ;
    q -> next = top ;
    top = q ;
}

/* removes an element from top of stack */
int pop (struct node *top)
{
    int item ;
    struct node *q ;
    /* if stack is empty */
    if (top == NULL )
        printf (“ stack is empty” ) ;
    else
    {
        q=top ;
        item = q -> data ;
        top = q -> next ;
        free (q) ;
        return (item) ;
    }
}

/* displays whole of the stack */
void stack_display (struct node *top)
{
    printf (“\n”) ;
    /* traverse the entire linked list */
    while (top ! = NULL)
    {
        printf (“%2d ”, q -> data) ;
        q = q -> next ;
    }
    printf (“\n”) ;
}

/* counts the number of nodes present in the
linked list representing a stack */
int count (struct node * q)
{
    int c = 0 ;
```

# LINKED LIST

A linked list is the collection of nodes and every node is divided into two parts (a) information field and (b) address of the next node.

A linked list is called so because each of items in the list is a part of a structure, which is linked to the structure containing the next item. This type of list is called a linked list since it can be considered as a list whose order is given by links from one item to the next.

The graphical representation of the linked list is as follows:

![](bbox=[0.506, 0.443, 0.596, 0.466])

Each item has a node consisting two fields one containing the variable and another consisting of address of the next item (i.e. pointer to the next item) in the list. A linked list is therefore a collection of structures ordered by logical links that are stored as the part of data.

Consider the following example to illustrate the concept of linking. Suppose we define a structure as follows:

```
struct linked_list
{
    float age;
    struct linked_list *next;
}
```

```
struct linked_list node1,node2;
This statement creates space for nodes each
containing 2 empty field’s
node1
    node1.age
    node1.next
node2
    node2.age
    node2.next
```

The next pointer of node1 can be made to point to the node 2 by the same statement.

```
node1.next=&node2;
```