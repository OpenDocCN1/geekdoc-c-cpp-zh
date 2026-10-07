anything useful other than show the code required for the most basic linked list tasks.
The program does the following:

+   1. It defines a structure and the required pointers for the list.
2. It adds the first element to the list.
3. It adds an element to the end of the list.
4. It adds an element to the middle of the list.
5. It displays the list contents onscreen.

# Input

LISTING 16.5 linkdemo.c-- The Basics of a Linked List

```
/* demonstrates the fundamentals of using */
/* a linked list. */
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
/* The list data structure. */
struct data {
    char name[20];
    struct data *next;
};
/* Define typedefs for the structure */
/* and a pointer to it. */
typed struct data PERSON;
ttypedef PERSON *LINK;\int main( void ) {
/* Head, new and current pointers. */
LINK head = NULL;
LINK new = NULL;
LINK current = NULL;
/* Add the first element. We do not */
/* assume the list is empty, although in */
/* this demo program it always will be. */
new = (LINK)malloc(sizeof(PERSON));
new->next = head;
head = new;
strcpy(new->name, "Abigail");
/* Add an element to the end of the list. */
```