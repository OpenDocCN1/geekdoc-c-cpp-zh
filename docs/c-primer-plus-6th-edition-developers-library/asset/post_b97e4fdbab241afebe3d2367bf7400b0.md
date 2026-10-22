
```
scan = scan->next;    /* find end of list     */
scan->next = pnew;    /* add pnew to end      */
}

    return true;
}
```

The first thing the AddItem() function does is allocate space for a new node. If this succeeds, the function uses CopyToNode() to copy the item to the node. Then it sets the next member of the node to NULL. This, as you’ll recall, indicates that the node is the last node in the linked list. Finally, after creating the node and assigning the correct values to its members, the function attaches the node to the end of the list. If the item is the first item added to the list, the program sets the head pointer to the first item. (Remember, AddItem() is called with the address of the head pointer as its second argument, so * plist is the value of the head pointer.) Otherwise, the code marches through the linked list until it finds the item having its next member set to NULL. That node is currently the last node, so the function resets its next member to point to the new node.

Good programming practice dictates that you call ListIsFull() before trying to add an item to the list. However, a user might fail to observe this dictate, so AddItem() checks for itself whether malloc() has succeeded. Also, it’s possible a user might do something else to allocate memory between calling ListIsFull() and calling AddItem(), so it’s best to check whether malloc() worked.

The Traverse() function is similar to the ListItemCount() function with the addition of applying a function to each item in the list:

```
void Traverse  (const List * plist, void (* pfun)(Item item) )
{
    Node * pnode = *plist;    /* set to start of list  */

    while (pnode != NULL)
    {
        (*pfun)(pnode->item); /* apply function to item */
        pnode = pnode->next;   /* advance to next item    */
    }
}
```

Recall that pnode->item represents the data stored in a node and that pnode->next identifies the next node in the linked list. For example, the function call

```
Traverse(movies, showmovies);
```

applies the showmovies() function to each item in the list.

Finally, the EmptyTheList() function frees the memory previously allocated using malloc():

```
void EmptyTheList(List * plist)
{
```

```
Node * psave;

while (*plist != NULL)
{
    psave = (*plist)->next; /* save address of next node */
    free(*plist);           /* free current node      */
    *plist = psave;         /* advance to next node   */
}
}
```

The implementation indicates an empty list by having the List variable being set to NULL. Therefore, this function needs to be passed the address of the List variable to be able to reset it. Because List already is a pointer, plist is a pointer to a pointer. Thus, within the code, the expression *plist is type pointer-to-Node. When the list terminates, *plist is NULL, meaning the original actual argument is now set to NULL.

The code saves the address of the next node because the call to free(), in principle, may make the contents of the current node (the one pointed to by *plist) no longer available.

## Note The Limitations of const

Several of the list-handling functions have const List * plist for a parameter. This indicates the intent that these functions don’t alter the list. Here, const does provide some protection. It prevents *plist (the quantity to which plist points) from being changed. In this program, plist points to movies, so const prevents those functions from changing movies, which, in turn, points to the first link in the list. Therefore, code such as this is not allowed in, say, ListItemCount():

```
*plist = (*plist)->next;   // not allowed if *plist is const
```

This is good, because changing *plist, and, hence, movies, would cause the program to lose track of the data. However, the fact that *plist and movies are treated as const doesn’t mean that data pointed to by *plist or movies is const. For example, code such as this is allowed:

```
(*plist)->item.rating = 3; // allowed even if *plist is const
```

That’s because this code doesn’t change *plist; it changes data that *plist points to. The moral is that you can’t necessarily rely on const to catch programming errors that accidentally modify data.

## Contemplating Your Work

Take a little time now to evaluate what the ADT approach has done for you. First, compare Listing 17.2 with Listing 17.4. Both programs use the same fundamental method (dynamic allocation of linked structures) to solve the movie listing problem, but Listing 17.2 exposes all the programming plumbing, putting malloc() and prev->next into public view. Listing 17.4, on the other hand, hides these details and expresses the program in a language that relates directly

to the tasks. That is, it talks about creating a list and adding items to the list, not about calling memory functions or resetting pointers. In short, Listing 17.4 expresses the program in terms of the problem to be solved, not in terms of the low-level tools needed to solve the problem. The ADT version is oriented to the end user's concerns and is much easier to read.

Next, the list.h and list.c files together constitute a reusable resource. If you need another simple list, just haul out these files. Suppose you need to store an inventory of your relatives: names, relationships, addresses, and phone numbers. First, you would go to the list.h file and redefine the Item type:

```
typedef struct itemtag
{
    char fname[14];
    char lname[24];
    char relationship[36];
    char address[60];
    char phonenum[20];
} Item;
```

Next... well, that's all you have to do in this case because all the simple list functions are defined in terms of the Item type. In some cases, you would also have to redefine the CopyToNode() function. For example, if an item were an array, you couldn't copy it by assignment.

Another important point is that the user interface is defined in terms of abstract list operations, not in terms of some particular set of data representations and algorithms. This leaves you free to fiddle with the implementation without having to redo the final program. For example, the current AddItem() function is a bit inefficient because it always starts at the beginning of the list and then searches for the end. You can fix this problem by keeping track of the end of the list. For example, you can redefine the List type this way:

```
typedef struct list
{
    Node * head;      /* points to head of list */
    Node * end;       /* points to end of list  */
} List;
```

Of course, you would then have to rewrite the list-processing functions using this new definition, but you wouldn't have to change a thing in Listing 17.4. This sort of isolating implementation from the final interface is particularly useful for large programming projects. It's called data hiding because the detailed data representation is hidden from the final user.

Note that this particular ADT doesn't even force you to implement the simple list as a linked list. Here's another possibility:

```
#define MAXSIZE 100
typedef struct list
{
    Item entries[MAXSIZE];  /* array of items      */
```

```
int items;        /* number of items in list */
} List;
```

Again, this would require rewriting the list.c file, but the program using the list doesn’t need to be changed.

Finally, think of the benefits this approach provides for the program-development process. If something is not working right, you probably can localize the problem to a single function. If you think of a better way to do one of the tasks, such as adding an item, you just have to rewrite that one function. If you need a new feature, you can think in terms of adding a new function to the package. If you think that an array or double-linked list would be better, you can rewrite the implementation without having to modify the programs that use the implementation.

## Getting Queued with an ADT

The abstract data type approach to programming in C, as you’ve seen, involves the following three steps:

- 1. Describing a type, including its operations, in an abstract, general fashion
- 2. Devising a function interface to represent the new type
- 3. Writing detailed code to implement the interface

You’ve seen this approach applied to a simple list. Now, apply it to something slightly more complex: the queue.

## Defining the Queue Abstract Data Type

A queue is a list with two special properties. First, new items can be added only to the end of the list. In this respect, the queue is like the simple list. Second, items can be removed from the list only at the beginning. You can visualize a queue as a line of people buying tickets to a theater. You join the line at the end, and you leave the line at the front, after purchasing your tickets. A queue is a first in, first out (FIFO) data form, just the way a movie line is (if no one cuts into the line). Once again, let’s frame an informal, abstract definition, as shown here:

| Type Name: | Queue |
| Type Properties: | Can hold an ordered sequence of items. |
| Type Operations: | Initialize queue to empty. Determine whether queue is empty. Determine whether queue is full. Determine number of items in the queue. Add item to rear of queue. Remove and recover item from front of queue. Empty the queue. |
