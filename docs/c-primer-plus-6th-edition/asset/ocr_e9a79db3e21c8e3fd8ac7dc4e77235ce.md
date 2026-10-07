# A Queue Simulation 687

Removing an item from the front of the queue (dequeuing) also has several steps. Here is one approach:

```
bool Queue::dequeue(Item &item)
{
    if (front == NULL)
        return false;
    item = front->item; // set item to first item in queue
    items--;
    Node * temp = front; // save location of first item
    front = front->next; // reset front to next item
    delete temp;
    if (items == 0)
        rear = NULL; // delete former first item
    return true;
```

In brief, the method goes through the following phases (see Figure 12.11):

+   1. Terminate if the queue is already empty.
2. Provide the first item in the queue to the calling function. This is accomplished by copying the data portion of the current front node into the reference variable passed to the method.
3. Decrease the item count (items) by one.
4. Save the location of the front node for later deletion.
5. Take the node off the queue. This is accomplished by setting the Queue member pointer front to point to the next node, whose address is provided by front->next.
6. To conserve memory, delete the former node.
7. If the list is empty, set rear to NULL. (The front pointer would already be NULL in this case, after setting front->next.) Again, you can use 0 instead of NULL, or with C++11, you can use nullptr.

Step 4 is necessary because step 5 erases the queue's memory of where the former first node is.