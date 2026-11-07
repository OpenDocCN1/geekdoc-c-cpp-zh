```
```cpp
{
    linkedQueueType<int> queue;
    int x, y;

    queue.initializeQueue();
    x = 4;
    y = 5;
    queue.addQueue(x);
    queue.addQueue(y);
    x = queue.front();
    queue.deleteQueue();
    queue.addQueue(x + 5);
    queue.addQueue(16);
    queue.addQueue(x);
    queue.addQueue(y - 3);

    cout << "Queue Elements: ";

    while (!queue.isEmptyQueue())
    {
        cout << queue.front() << " ";
        queue.deleteQueue();
    }

    cout << endl;

    return 0;
}
```
```

**Sample Run:**

Queue Elements: 5 9 16 4 2

# ## Queue Derived from the class `unorderedLinkedListType`

From the definitions of the functions to implement the queue operations, it is clear that the linked implementation of a queue is similar to the implementation of a linked list created in a forward manner (see Chapter 17). The addQueue operation is similar to the operation insertFirst. Likewise, the operations initializeQueue and initializeList and isEmptyQueue and isEmptyList are similar. The deleteQueue operation can be implemented as before. The pointer queueFront is the same as the pointer first, and the pointer queueRear is the same as the pointer last. This correspondence suggests that we can derive the class to implement the queue from the class `linkedListType` (see Chapter 17). Note that the class `linkedListType` is an abstract class and does not implement all of the operations. However, the class `unorderedLinkedListType` is derived from the class `linkedListType` and provides the definitions of the abstract functions of the class `linkedListType`. Therefore, we can derive the class `linkedQueueType` from the class `unorderedLinkedListType`.