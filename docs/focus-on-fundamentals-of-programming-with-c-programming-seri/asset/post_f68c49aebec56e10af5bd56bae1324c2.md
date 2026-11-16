
## Example 2

Assume a linear linked list is ordered so that the smaller items precede the larger ones (i.e., the list is sorted). We want to insert an item x into this list in its proper place. Two functions are used:

- `insertFront()` will be used to insert a node at the front of the list.
- `insertAfter()` will be used to insert a node into the middle of the list.

```
insertItem.c
p = list;
q = NULL;
while p!= NULL and x > info(p)
    q = p;
    p = next(p)
If q == NULL
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

```
// node1.c
struct node {
    int info;
    struct node *next;
};

typedef struct node *NODEPTR;
```

or, we can combine the two declarations above as follows:

```
// node2.c
typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;
```

In either case, we declare `NODEPTR` to be a pointer to a `node struct`. Note that the `next` field in the `node struct` is a pointer that contains the address of the next node in the list.

We can now declare a `NODEPTR p` and dynamically create a new node:

```
// node3.c
NODEPTR p;
p = (NODEPTR) malloc(sizeof(struct node));
```

We access the `info` field of the node as:

```
p->info
```

and we can access the `next` field of the node as:

```
p->next
```

As before, we can use the `free()` function to dispose of the dynamically created node:

```
free(p);
```

Work through the following program to create a linked list containing five dynamically created nodes:

```
// dynamic.c
#include <stdio.h>
#include <stdlib.h>
typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;
int main(void) {
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
    return 0;
}
```

### Linear Linked List Operations

Here are functions to manipulate a linear linked list of integers. It is very important for you to work through each of these functions to be sure that you understand how they work. Be sure to draw pictures to linked lists to assist you in visualizing the algorithms. It is extremely difficult to write code using linked lists without drawing pictures of the lists and how the list changes as your algorithm executes.

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

```
// deletes the node at the front of the list
int deleteFront(NODEPTR *list) {
    int temp;
    NODEPTR p;

    if (*list == NULL) {
        error("List underflow.");
    }
    p = *list;
    temp = p->info;
    *list = p->next;
    freeNode(p);
    return temp;
}
```

```
// adds an element to the end of a list
void addLast(NODEPTR *list, int num) {
    NODEPTR p, q;

    p = getNode();
    p->info = num;
    p->next = NULL;
    if (*list == NULL) {
        *list = p;
    } else {
        q = *list;
        while (q->next) {
            q = q->next;
        }
        q->next = p;
    }
}
```

```
// deletes the last element in a list
int deleteLast(NODEPTR *list) {
    NODEPTR p, q;
    int temp = -1;

    if (*list) {
        p = *list;
        q = NULL;
        while (p->next) {
            q = p;
            p = p->next;
        }
        if (!q) {
            *list = NULL;
        }
        else {
            q->next = NULL;
        }
        temp = p->info;
        freeNode(p);
    }
    return temp;
}
```

```
// inserts a new node after the node pointed to by p
void insertAfter(NODEPTR p, int num) {
    NODEPTR q;

    if (p == NULL) {
        error("Void insertion.");
    }
    q = getNode();
    q->info = num;
    q->next = p->next;
    p->next = q;
}
```

```
// deletes the node after the node pointed to by p

int deleteAfter(NODEPTR p) {
    int temp;
    NODEPTR q;

    if (p == NULL || p->next == NULL) {
        error("Void deletion.");
    }

    q = p->next;
    temp = q->info;
    p->next = q->next;
    freeNode(q);
    return temp;
}
```

```
// insert a node into its correct location within a sorted list

void Insert(NODEPTR *list, int num) {
    NODEPTR p, q;

    p = *list;
    q = NULL;

    while (p != NULL && p->info < num) {
        q = p;
        p = p->next;
    }

    if (q == NULL) {
        addFront(list, num);
    } else {
        insertAfter(q, num);
    }
}
```

```
// returns the number of nodes in the list

int numElements(NODEPTR list) {
    int count=0;

    while (list) {
        count++;
        list = list->next;
    }

    return count;
}
```

```
// returns sum of integers in the list
int sumElements(NODEPTR list) {
    int sum=0;
    while (list) {
        sum += list->info;
        list = list->next;
    }
    return sum;
}

// traverses a list and outputs contents of list
void outputList(NODEPTR list) {
    while (list) {
        printf("%d", list->info);
        list = list->next;
    }
    printf("\n");
}

// Returns true if the item is found in the list
int contains(NODEPTR list, int num) {
    NODEPTR p;
    p = list;
    while (p != NULL && p->info != num) {
        p = p->next;
    }
    return p != NULL;
}

// determines whether or not a list is empty
int isEmpty(NODEPTR list) {
    return list == NULL;
}
```

```
// frees all the nodes in a list
void freeList(NODEPTR *list) {
    NODEPTR p;
    while (*list) {
        p = *list;
        *list = p->next;
        freeNode(p);
    }
}
```

```
// returns a pointer to the node with the requested value;
// otherwise returns NULL
NODEPTR select(NODEPTR list, int num) {
    while (list) {
        if (list->info == num) {
            return list;
        }
        else {
            list = list->next;
        }
    }
    return list;
}
```

```
// removes the first occurrence of an item in a list
int remove(NODEPTR *list, int num) {
    NODEPTR p, q;
    p = *list;
    q = NULL;
    while (p != NULL && p->info != num) {
        q = p;
        p = p->next;
    }
    if (p == NULL) {
        return -1;
    }
    else {
        return q == NULL ? deleteFront(list) : deleteAfter(q);
    }
}
