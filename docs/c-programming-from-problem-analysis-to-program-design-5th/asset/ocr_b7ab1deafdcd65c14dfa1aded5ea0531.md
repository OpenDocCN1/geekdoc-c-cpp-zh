```
```cpp
template <class Type>
Type queueType<Type>::front() const
{
    assert(!isEmptyQueue());
    return list[queueFront];
} //end front
```
```

# BACK

This operation returns the last element of the queue. If the queue is nonempty, the element of the queue indicated by the index queueRear is returned; otherwise the program terminates.

```
```cpp
template <class Type>
Type queueType<Type>::back() const
{
    assert(!isEmptyQueue());
    return list[queueRear];
} //end back
```
```

# addQueue

Next, we implement the addQueue operation. Because queueRear points to the last element of the queue, to add a new element to the queue, we first advance queueRear to the next array position and then add the new element to the array position indicated by queueRear. We also increment count by 1. So the function addQueue is:

```
```cpp
template <class Type>
void queueType<Type>::addQueue(const Type& newElement)
{
    if (!isFullQueue())
    {
        queueRear = (queueRear + 1) % maxQueueSize; //use the
                                                     //mod operator to advance queueRear
                                                     //because the array is circular
        count++;
        list[queueRear] = newElement;
    }
    else
        cout << "Cannot add to a full queue." << endl;
} //end addQueue
```
```

# deleteQueue

To implement the deleteQueue operation, we access the index queueFront. Because queueFront points to the array position containing the first element of the queue, in order to remove the first queue element, we decrement count by 1 and advance queueFront to the next queue element. So the function deleteQueue is: