![](bbox=[0.18, 0.18, 0.82, 0.65])

Figure 17.4 Linked list with several items.

# Using a Linked List

Now that you have a picture of how a linked list works, let’s implement it. Listing 17.2 modifies Listing 17.1 so that it uses a linked list instead of an array to hold the movie information.

# Listing 17.2 The films2.c Program

```
/* films2.c -- using a linked list of structures */
#include <stdio.h>
#include <stdlib.h>    /* has the malloc prototype    */
#include <string.h>    /* has the strcpy prototype    */
#define TSIZE  45      /* size of array to hold title */

struct film {
    char title[TSIZE];
    int rating;
```