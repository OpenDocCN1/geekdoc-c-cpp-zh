```
continue; // dispose of rest of line
}
return ret_val;
}
```

# Implementing the Interface

Of course, you still have to implement the List interface. The C approach is to collect the function definitions in a file called list.c. The complete program, then, consists of three files: list.h, which defines the data structures and provides prototypes for the user interface, list.c, which provides the function code to implement the interface, and films3.c, which is a source code file that applies the list interface to a particular programming problem. Listing 17.5 shows one possible implementation of list.c. To run the program, you must compile both films3.c and list.c and link them. (You might want to review the discussion in Chapter 9, "Functions," on compiling multiple-file programs.) Together, the files list.h, list.c, and films3.c constitute a complete program (see Figure 17.5).

# Listing 17.5 The list.c Implementation File

```
/* list.c -- functions supporting list operations */
#include <stdio.h>
#include <stdlib.h>
#include "list.h"

/* local function prototype */
static void CopyToNode(Item item, Node *pnode);

/* interface functions */

/* set the list to empty */
void InitializeList(List *plist)
{
    *plist = NULL;
}

/* returns true if list is empty */
bool ListIsEmpty(const List *plist)
{
    if (*plist == NULL)
        return true;
    else
        return false;
}
```