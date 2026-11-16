
## Step 4: freeNode (p)

list

X = 10

Algorithm 3: Given a linear linked list of integers, create an algorithm that will traverse (visit) each node in the list and output the data in each of the `info` fields.

![](img/0603fdf2eefeabaf26542250cc2fb439_472_0.png)

```
p = list
while (p != null)
    output (p.getInfo())
    p = p.getNext()
```

Can you see the importance of ensuring that there is a null value in the next field of the last node in the linear linked list?

## Additional List Operations

It is easy to insert and delete elements from the middle of a list without any data movements. For example, the amount of work required to insert a node into the middle of a list is independent of the size of the list. All that is necessary is to:

- allocate a new node
- insert the information into the node
- adjust two pointers

![](img/0603fdf2eefeabaf26542250cc2fb439_473_0.png)

## Algorithm 4: Given a pointer p to a node in a linear linked list, write an algorithm, insertAfter, that will insert a node after the node pointed to by p:

![](img/0603fdf2eefeabaf26542250cc2fb439_474_0.png)

- q = getNode()

![](img/0603fdf2eefeabaf26542250cc2fb439_474_1.png)

- info(q) = x

x = 25

![](img/0603fdf2eefeabaf26542250cc2fb439_474_2.png)

- next(q) = next(p)

![](img/0603fdf2eefeabaf26542250cc2fb439_475_0.png)

- next(p) = q

![](img/0603fdf2eefeabaf26542250cc2fb439_475_1.png)

Note that an item can only be inserted after a given node, not before the node. This is because there is no way to proceed from a given node to its predecessor in a list without traversing the list from the beginning.

Here's the algorithm from above:

```
q = getNode()
info(q) = x
next(q) = next(p)
next(p) = q
```

## Algorithm 5: Given a pointer p to a node in a linear linked list, write an algorithm, deleteAfter, that will delete a node after the node pointed to by p:

![](img/0603fdf2eefeabaf26542250cc2fb439_476_0.png)

- q = next(p)

![](img/0603fdf2eefeabaf26542250cc2fb439_476_1.png)

- x = info(q)

![](img/0603fdf2eefeabaf26542250cc2fb439_476_2.png)

X = 30

- next(p) = next(q)

![](img/0603fdf2eefeabaf26542250cc2fb439_477_0.png)

- freeNode(q)

![](img/0603fdf2eefeabaf26542250cc2fb439_477_1.png)

Again, we cannot just be given a pointer to the node we want to delete. This is because the next field of the node's predecessor must be changed to point to the node's successor and there is no direct way of reaching the predecessor of a given node.

Here's the algorithm from above:

```
q = next(p)
x = info(q)
next(p) = next(q)
freeNode(q)
```

## Linear Linked List Examples

### Example 1

Suppose we wanted to delete all occurrences of the number 4 from a linear linked list. We would have to traverse the list for nodes with 4 in the info field and delete that node. But to delete a node, its predecessor must be known. Therefore we must use two pointers, p and q, to traverse the list. p will be considered the lead pointer and q will be considered the lag pointer, i.e., p will traverse the list and q will always point to the predecessor of p. Note the practice of using two pointers, one following the other, is very common when working with lists.

Two functions will be used:

- `deleteFront()` will be used to delete the node from the front of the list.
- `deleteAfter()` will be used to delete a node from the middle of the list.

```
// deleteNumber.c

p = list
q = NULL
while p != NULL
    if info(p) == 4
        p = next(p)
        if q == NULL
            x = deleteFront(list)
        else
            x = deleteAfter(q)
    else
        q = p
        p = next(p)
```

It is left as an exercise to work through the algorithm. Be sure to draw pictures as you work through the algorithm line by line.

### Example 2

Assume a linear linked list is ordered so that the smaller items precede the larger ones (i.e., the list is sorted). We want to insert an item x into this list in its proper place. Two functions are used:

- insertFront() will be used to insert a node at the front of the list.
- insertAfter() will be used to insert a node into the middle of the list.

```
insertItem.c
p = list
q = NULL
while p!= NULL and x > info(p)
    q = p
    p = next(p)
if q == NULL
    insertFront(list, x)
else
    insertAfter(q, x)
```

Again, it is left as an exercise to work through the algorithm. Be sure to draw pictures as you work through the algorithm line by line.

## Linear Linked List Homework

Write a pseudo code algorithm to perform each of the following operations:

- 1. Determine the number of nodes in a list.
- 2. Determine the sum of the integers in a list.
- 3. Append a node to the end of a list.
- 4. Concatenate two lists.
- 5. Free all the nodes in a list.
- 6. Delete the last element from a list.
- 7. Make a copy of a list.

## Chapter 20. Implementation of Linear Linked Lists

- Defining Nodes in C
- Linear Linked List Operations
- Separate Compilation
- Linear Linked List Code
- Addition of Polynomials
- Linear Linked List Lab
- Calculating Very Large Factorials Lab

### Defining Nodes in C

We've seen that pointers allow us to build and manipulate linked lists of various types. By altering the values of pointers, nodes can be attached, detached, and reassembled in patterns that grow and shrink as execution of a program progresses.

We can create a chain of these nodes, and keep track of the first one in the list and then store within each node a pointer to the next node in the list. To accomplish this, each node will therefore be defined as a `struct` with one field containing the information and another field containing the address of the next node in the list. We make the declarations as follows:

```c
// node1.c

struct node {
    int info;
    struct node *next;
};

typedef struct node *NODEPTR;
```

or, we can combine the two declarations above as follows:

```c
// node2.c

typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;
```

In either case, we declare NODEPTR to be a pointer to a `node struct`. Note that the `next` field in the `node struct` is a pointer that contains the address of the next node in the list.

We can now declare a NODEPTR p and dynamically create a new node:

```c
// node3.c

NODEPTR p;
p = (NODEPTR) malloc(sizeof(struct node));
```

We access the `info` field of the node as:

```c
p->info
```

and we can access the `next` field of the node as:

```c
p->next
```

As before, we can use the `free()` function to dispose of the dynamically created node:

```c
free(p);
```

Work through the following program to create a linked list containing five dynamically created nodes:

```c
// dynamic.c

#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;

void main(void) {
    int i;
    NODEPTR list, p, q;

    list = (NODEPTR) malloc(sizeof(struct node));
    p = list;
    p->info = 1;
    for (i = 2; i <= 5; i++) {
        q = (NODEPTR) malloc(sizeof(struct node));
        q->info = i;
        p->next = q;
        p = q;
    }
    p->next = NULL;
}
```

## Linear Linked List Operations

Here are functions to manipulate a linear linked list of integers. It is very important for you to work through each of these functions to be sure that you understand how they work. Be sure to draw pictures of linked lists to assist you in visualizing the algorithms. It is extremely difficult to write code using linked lists without drawing pictures of the lists and how the list changes as your algorithm executes.

```
// returns the address of a newly created node

NODEPTR getNode(void) {
    NODEPTR p;

    p = (NODEPTR) malloc(sizeof(struct node));
    if (p == NULL) {
        error("List overflow.");
    }
    return(p);
}

// frees the node pointed to by p

void freeNode(NODEPTR p) {
    free(p);
}

// adds a new node to the front of the list

void addFront(NODEPTR *list, int num) {
    NODEPTR p;

    p = getNode();
    p->info = num;
    p->next = *list;
    *list = p;
}
```
