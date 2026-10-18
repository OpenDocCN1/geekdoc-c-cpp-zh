```
```cpp
tempPtr->data = theSymbol;
tempPtr->link = top;
top = tempPtr;
}
```
```

```
```cpp
11. //Uses cstddef:
Stack::Stack(const Stack& aStack)
{
    if (aStack.top == NULL)
        top = NULL;
    else
    {
        StackFramePtr temp = aStack.top; //temp moves
            //through the nodes from top to bottom of
            //aStack.
        StackFramePtr end; //Points to end of the new stack.

        end = new StackFrame;
        end->data = temp->data;
        top = end;
        //First node created and filled with data.
        //New nodes are now added AFTER this first node.

        temp = temp->link;
        while (temp != NULL)
        {
            end->link = new StackFrame;
            end = end->link;
            end->data = temp->data;
            temp = temp->link;
        }
        end->link = NULL;
    }
}
```
```

```
```cpp
12. //Uses cstddef:
Queue::Queue(const Queue& aQueue)
{
    if (aQueue.empty())
        front = back = NULL;
    else
    {
        QueueNodePtr tempPtrOld = aQueue.front;
        //tempPtrOld moves through the nodes
        //from front to back of aQueue.
        QueueNodePtr tempPtrNew;
        //tempPtrNew is used to create new nodes.

        back = new QueueNode;
        back->data = tempPtrOld->data;
```
```