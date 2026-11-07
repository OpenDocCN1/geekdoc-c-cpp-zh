```
```text
? 4
3 3 removed from list
The list is empty

? 5
End list test

All nodes destroyed

All nodes destroyed
```
```

**Fig. 20.5** | Manipulating a linked list. (Part 4 of 4.)

# *Member Function* `insertAtFront`

Over the next several pages, we discuss each of the member functions of class `List` in detail. Function `insertAtFront` (Fig. 20.4, lines 62–74) places a new node at the front of the list. The function consists of several steps:

+   1. Call function `getNewNode` (line 65), passing it `value`, which is a constant reference to the node value to be inserted.
+   2. Function `getNewNode` (lines 150–155) uses operator `new` to create a new list node and return a pointer to this newly allocated node, which is assigned to `newPtr` in `insertAtFront` (line 65).
+   3. If the list is empty (line 67), `firstPtr` and `lastPtr` are set to `newPtr` (line 68)—i.e., the first and last node are the same node.
+   4. If the list is not empty (line 69), then the node pointed to by `newPtr` is threaded into the list by copying `firstPtr` to `newPtr->nextPtr` (line 71), so that the new node points to what used to be the first node of the list, and copying `newPtr` to `firstPtr` (line 72), so that `firstPtr` now points to the new first node of the list.

Figure 20.6 illustrates function `insertAtFront`. Part (a) shows the list and the new node before calling `insertAtFront`. The dashed arrows in part (b) illustrate Step 4 of the `insertAtFront` operation that enables the node containing 12 to become the new list front.

![](bbox=[0.326, 0.668, 0.681, 0.911])

**Fig. 20.6** | Operation `insertAtFront` represented graphically.