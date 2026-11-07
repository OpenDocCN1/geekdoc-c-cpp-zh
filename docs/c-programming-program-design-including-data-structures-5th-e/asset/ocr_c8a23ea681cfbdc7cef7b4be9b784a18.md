If the queue is nonempty, the operation front returns the first element of the queue, and so the element of the queue indicated by the pointer queueFront is returned. If the queue is empty, the function front terminates the program.

If the queue is nonempty, the operation back returns the last element of the queue, so the element of the queue indicated by the pointer queueRear is returned. If the queue is empty, the function back terminates the program. Similarly, if the queue is nonempty, the operation deleteQueue removes the first element of the queue, so we access the pointer queueFront.

The definitions of the functions to implement these operations are:

```
template <class Type>
void linkedQueue<Type>::addQueue(const Type& newElement)
{
    nodeType<Type> *newNode;

    newNode = new nodeType<Type>;   //create the node

    newNode->info = newElement; //store the info
    newNode->link = NULL; //initialize the link field to NULL

    if (queueFront == NULL) //if initially the queue is empty
    {
        queueFront = newNode;
        queueRear = newNode;
    }
    else                 //add newNode at the end
    {
        queueRear->link = newNode;
        queueRear = queueRear->link;
    }
}//end addQueue

template <class Type>
Type linkedQueue<Type>::front() const
{
    assert(queueFront != NULL);
    return queueFront->info;
} //end front

template <class Type>
Type linkedQueue<Type>::back() const
{
    assert(queueRear != NULL);
    return queueRear->info;
} //end back
```