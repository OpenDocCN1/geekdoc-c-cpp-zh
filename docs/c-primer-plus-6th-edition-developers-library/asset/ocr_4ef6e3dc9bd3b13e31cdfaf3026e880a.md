```
```c
if (QueueFull(pq))
	return false;
pnew = (Node *) malloc(sizeof(Node));
if (pnew == NULL)
{
	fprintf(stderr,"Unable to allocate memory!\n");
	exit(1);
}
CopyToNode(item, pnew);
pnew->next = NULL;
if (QueueIsEmpty(pq))
	pq->front = pnew; /* item goes to front */
else
{
	pq->rear->next = pnew; /* link at end of queue */
	pq->rear = pnew; /* record location of end */
	pq->items++;
	/* one more item in queue */
}
return true;
```
```

The CopyToNode() function is a static function to handle copying the item to a node:

```
```c
static void CopyToNode(Item item, Node * pn)
{
	pn->item = item;
}
```
```

Removing an item from the front of the queue involves the following steps:

+   1. Copying the item to a waiting variable
+   2. Freeing the memory used by the vacated node
+   3. Resetting the front pointer to the next item in the queue
+   4. Resetting the front and rear pointers to NULL if the last item is removed
+   5. Decrementing the item count

Here's code that does all these things:

```
```c
bool DeQueue(Item * pit, Queue * pq)
{
	Node * pt;
	if (QueueIsEmpty(pq))
		return false;
	CopyToItem(pq->front, pit);
	pt = pq->front;
	pq->front = pq->front->next;
	// (code continues in image but truncated in provided text)
```
```