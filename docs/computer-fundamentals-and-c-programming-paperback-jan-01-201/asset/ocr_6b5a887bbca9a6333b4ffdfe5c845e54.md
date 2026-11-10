query and edit operations at intermediate locations in the list. Some of these functions are called directly from `main` and the others are invoked from these functions. This program performs the following tasks:

+   - Creates a list from user input.
+   - Traverses the list for counting and printing nodes.
+   - Searches a node for a user-specified value.
+   - Adds and deletes a node as a consequence of the search.

The program lists the function prototypes and the `main` function. The function definitions are shown in the following sub-sections where they are discussed. These discussions don’t include the `print_list` function which has already been explained in Section 16.13.

The program first creates the linked list using `scanf`, `malloc` and the `add_node` function. Because all the user-defined functions use a pointer to `struct node` as argument, the structure itself must be declared before `main`. This makes the structure and its pointer global, i.e., visible in the entire file.

```
/* list manipulation.c: A comprehensive program that uses 6 functions to
                         create, query, add and delete nodes of a linked list. */
#include <stdio.h>
#include <stdlib.h>

struct node {                               /* Declaration before main */
    short data;
    struct node *next;
};

/* The function prototypes */
void add_node(struct node *p, struct node *q);
void print_list(struct node *head);
short count_nodes(struct node *head);
struct node *find_node(struct node *head, short val);
void insert_after(struct node *head, short val1, short val2);
void delete_node(struct node **head, short val);

int main(void)
{
    struct node *head, *p, *q;
    short count = 0, temp, val1, val2;

    /* Create the list first */
    fputs("Key in some short integers and press [Ctrl-d]:\n", stderr);
    while (scanf("%hd", &temp) == 1) {
        count++;
        q = malloc(sizeof(struct node));
```