# Linear Linked List Code

```
// list.h

#ifndef _LIST_H
#define _LIST_H

typedef struct node {
    int info;
    struct node *next;
} *NODEPTR;

NODEPTR getNode(void);
void freeNode(NODEPTR p);
void addFront(NODEPTR *list, int num);
int deleteFront(NODEPTR *list);
void addLast(NODEPTR *list, int num);
int deleteLast(NODEPTR *list);
void insertAfter(NODEPTR p, int num);
void deleteAfter(NODEPTR p);
void insert(NODEPTR *list, int num);
int numElements(NODEPTR list);
int sumElements(NODEPTR list);
void outputList(NODEPTR list);
int contains(NODEPTR list, int num);
int isEmpty(NODEPTR list);
void freeList(NODEPTR *list);
NODEPTR select(NODEPTR list, int num);
int remove(NODEPTR *list, int num);
NODEPTR copyList(NODEPTR list);
void concatList(NODEPTR *list1, NODEPTR list2);
void intersect(NODEPTR list1, NODEPTR list2);
void error(char *msg);

#endif
```