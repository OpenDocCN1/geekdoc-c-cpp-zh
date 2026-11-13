FrontElement() returns the data element at the front of the queue. Here, the front is not updated. FrontElement() just reads what is at front.

```
int Queue :: GetFront()
{
    if(!IsEmpty())
        return(Front->data);
}
```

Note that if the NewNode is a node getting added in an empty queue, then along with the rear, the front should also be set to point to the newly added node, which is at the front of the queue. Hence, as both the front and the rear may get updated. Program Code 6.20 shows the addition of an element to a linked queue.

```
void Queue :: Add(int x)
{
    QNode *NewNode;
    NewNode = new QNode;
    NewNode->data = x;
    NewNode->link = Null;
    // if the new is a node getting added in empty queue
    // then front should be set so as to point to new
    if(Rear == Null)
    {
        Front = NewNode;
        Rear = NewNode;
    }
    else
    {
        Rear->link = NewNode;
        Rear = NewNode;
    }
}
```

Delete() function first verifies if there is any data element in the queue. If there is an element, Delete() gets and returns the data at the front of the queue to the caller function. Then, the front is set to point to the new queue front node, which is next to the node being deleted. If the last node is being deleted, then the deleted node's next pointer is guaranteed to be null. Note that if the current deletion of a node results in queue empty state, then along with the front, the rear should also be set to Null.

```
int Queue :: Delete()
{
```