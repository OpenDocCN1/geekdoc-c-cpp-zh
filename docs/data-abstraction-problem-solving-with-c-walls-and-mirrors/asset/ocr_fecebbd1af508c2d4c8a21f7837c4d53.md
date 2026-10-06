# 278 CHAPTER 9 List Implementations

FIGURE 9-7 Deleting a node from a chain

![](bbox=[0.263, 0.134, 0.931, 0.296])

linked-based implementations of the ADT bag in Chapter 4 and the ADT stack in Chapter 7 do this. Let's consider the deletion of an interior node.

As Figure 9-7 indicates, you can remove the node N to which `curPtr` points by altering the value of the pointer that precedes N. You need to set this pointer so that it points to the node that follows N, bypassing N on the chain. (The dashed line indicates the old pointer value) Notice this pointer change does not directly affect node N. N remains in existence, and it is the same node that it pointed to before. For example, a traversal of the chain would reach node N.

To accomplish this pointer change, notice that if you had only the curPtr pointing to N, you would have no direct way to access the node that precedes N. After all, you cannot follow the links in the chain backward. Thus, you must have the variable `prevPtr` in Figure 9-7. It points to the node that precedes N on the chain and makes it possible for you to alter that node's next pointer, thereby removing node N from the chain. The following assignment is all that you need to remove the node to which curPtr points:

Removing an interior node

```
prevPtr->setNext(curPtr->getNext());
```

Does the previous technique work for any node N, regardless of where in the linked chain it appears? No, it does not work if the node to be deleted is the first node in the chain, but it does work for the last node in the chain. Thus, deletion of the first node in a chain is a special case. Since we already know how to delete the first node, let's consider deleting the last.

Figure 9-8 shows the deletion of the node to which curPtr points, which is the last node. That pointer alone is insufficient, as we have the variable `prevPtr` to the next-to-last node. You set the pointer within the next-to-last node to `nullPtr`. The same statement that we just used to remove an interior node will make this pointer change, since the value of `curPtr->getNext()` is `nullPtr`:

```
prevPtr->setNext(curPtr->getNext());
```

FIGURE 9-8 Removing the last node

![](bbox=[0.263, 0.796, 0.836, 0.893])