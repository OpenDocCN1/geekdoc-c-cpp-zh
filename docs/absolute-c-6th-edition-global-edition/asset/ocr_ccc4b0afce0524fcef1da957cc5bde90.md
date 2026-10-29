# Display 17.12 Deleting a Node from a Doubly Linked List

# Existing list before deleting discard

# Set pointers to the previous and next nodes

```
DoublyLinkedIntNodePtr prev = discard->getPreviousLink( );
DoublyLinkedIntNodePtr next = discard->getNextLink( );
```

# Bypass discard

```
prev->setNextLink(next);
next->setPreviousLink(prev);
```

# Delete discard

```
delete discard;
```