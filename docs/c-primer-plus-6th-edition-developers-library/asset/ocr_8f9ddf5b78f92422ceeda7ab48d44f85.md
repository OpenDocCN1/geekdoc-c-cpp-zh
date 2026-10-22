```
/* general type definitions */

typedef struct film Item;

typedef struct node
{
    Item item;
    struct node * next;
} Node;

typedef Node * List;

/* function prototypes */

/* operation:      initialize a list                */
/* preconditions:  plist points to a list           */
/* postconditions: the list is initialized to empty */
void InitializeList(List * plist);

/* operation:      determine if list is empty       */
/*                 plist points to an initialized list */
/* postconditions: function returns True if list is empty */
/*                 and returns False otherwise       */
bool ListIsEmpty(const List *plist);

/* operation:      determine if list is full        */
/*                 plist points to an initialized list */
/* postconditions: function returns True if list is full */
/*                 and returns False otherwise       */
bool ListIsFull(const List *plist);

/* operation:      determine number of items in list */
/*                 plist points to an initialized list */
/* postconditions: function returns number of items in list */
unsigned int ListItemCount(const List *plist);

/* operation:      add item to end of list          */
/* preconditions:  item is an item to be added to list */
/*                 plist points to an initialized list */
/* postconditions: if possible, function adds item to end */
/*                 of list and returns True; otherwise the */
/*                 function returns False             */
bool AddItem(Item item, List * plist);

/* operation:      apply a function to each item in list */
/*                 plist points to an initialized list    */
```