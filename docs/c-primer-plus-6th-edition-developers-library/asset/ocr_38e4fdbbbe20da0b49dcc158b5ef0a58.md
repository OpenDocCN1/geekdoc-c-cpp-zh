```
free(pt);
pq->items--;
if (pq->items == 0)
    pq->rear = NULL;

return true;
}
```

There are a couple of pointer facts you should note. First, the code doesn’t explicitly set the front pointer to NULL when the last item is deleted. That’s because it already sets the front pointer to the next pointer of the node being deleted. If that node is the last node, its next pointer is NULL, so the front pointer gets set to NULL. Second, the code uses a temporary pointer (pt) to keep track of the deleted node’s location. That’s because the official pointer to the first node (pq->front) gets reset to point to the next node, so without the temporary pointer, the program would lose track of which block of memory to free.

We can use the Dequeue() function to empty a queue. Just use a loop calling Dequeue() until the queue is empty:

```
void EmptyTheQueue(Queue * pq)
{
    Item dummy;
    while (!QueueIsEmpty(pq))
        Dequeue(&dummy, pq);
}
```

# Note Keeping Your ADT Pure

After you’ve defined an ADT interface, you should use only the functions of the interface to handle the data type. Note, for example, that Dequeue() depends on the Enqueue() function doing its job of setting pointers correctly and setting the next pointer of the rear node to NULL. If, in a program using the ADT, you decided to manipulate parts of the queue directly, you might mess up the coordination between the functions in the interface package.

Listing 17.7 shows all the functions of the interface, including the CopyToItem() function used in Enqueue().

# Listing 17.7 The queue.c Implementation File

```
/* queue.c -- the Queue type implementation*/
#include <stdio.h>
#include <stdlib.h>
#include "queue.h"

/* local functions */
static void CopyToNode(Item item, Node * pn);
```