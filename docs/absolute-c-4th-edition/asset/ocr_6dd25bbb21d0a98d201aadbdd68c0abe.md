```
front = back;
//First node created and filled with data.
//New nodes are now added AFTER this first node.

temp = temp->getLink( );//temp now points to second
//node or NULL if there is no second node.

while (temp != NULL)
{
    back->setLink(new Node<T>(temp->getData( ), NULL));
    back = back->getLink( );
    temp = temp->getLink( );
}
//back->link == NULL
}
```

18. The following should be placed in the namespace QueueSavitch:

```
//Uses cstddef:
template<class T>
Queue<T>& Queue<T>::operator =(const Queue<T>& rightSide)
{
    if (front == rightSide.front)//if the queues are the same
        return *this;
    else //send left side back to freestore
    {
        T next;
        while (! isEmpty( ))
            next = remove( );//remove calls delete.
    }

    if (rightSide.isEmpty( ))
    {
        front = back = NULL;
        return *this;
    }
    else
    {
        Node<T> *temp = rightSide.front;//temp moves
        //through the nodes from front to back of rightSide.

        back = new Node<T>(temp->getData( ), NULL);
        front = back;
        //First node created and filled with data.
        //New nodes are now added AFTER this first node.

        temp = temp->getLink( );//temp now points to second
```