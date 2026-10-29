The function declaration for our delete function is now

```
void delete(DoublyLinkedIntNodePtr& head,
    DoublyLinkedIntNodePtr discard);
```

The parameter discard is a pointer to the node we wish to remove. We must also input the head of the list to handle the case where discard is the same as head:

```
if (head == discard)
{
    head = head->getNextLink();
    head->setPreviousLink(nullptr);
}
```

In this case we have to advance head to the next node in the list. We then set the previous link to nullptr because there is no prior node. In the more general case, the variable discard points to any other node that is not the head. We handle this case by redirecting the links to bypass discard, as shown in Display 17.12:

```
else
{
    DoublyLinkedIntNodePtr prev = discard->getPreviousLink();
    DoublyLinkedIntNodePtr next = discard->getNextLink();
    prev->setNextLink(next);
    if (next != nullptr)
    {
        next->setPreviousLink(prev);
    }
}
```

The previous node now links to discard’s next node, and the next node now links to discard’s previous node. Since discard might be the last node in the list, we have to check and make sure that next != nullptr so we do not try to dereference a nullptr pointer in the function setPreviousLink.

The complete function definition is given in Display 17.13.

# Display 17.13 Functions to Add and Remove a Node from a Doubly Linked List (part 1 of 3)

# NODE AND POINTER TYPE DEFINITIONS

```
class DoublyLinkedIntNode
{
public:
    DoublyLinkedIntNode() {}
    DoublyLinkedIntNode(int theData, DoublyLinkedIntNode* previous,
        DoublyLinkedIntNode* next)
        : data(theData), nextLink(next), previousLink(previous) {}
    DoublyLinkedIntNode* getNextLink() const
    { return nextLink; }
```