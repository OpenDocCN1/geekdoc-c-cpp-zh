# 6.7.2 Deletion of a Node from a Doubly Linked List

Deleting from a DLL needs the deleted node's predecessor, if any, to be pointed to the deleted node's successor. In addition, the successor, if any, should be set to point to the predecessor node as shown in Fig. 6.30.

![](bbox=[0.32, 0.205, 0.765, 0.62])

Fig. 6.30 Deletion node in doubly linked list (a) Links modified on deletion of node (b) Memory of the deleted node freed (c) Realignment of nodes (d) After node deletion

The core steps involved in this process are the following:

```
(curr->Prev)->Next = curr->Next;
(curr->Next)->Prev = curr->Prev;
delete curr;
```

The C++ code for the same is as shown in Program Code 6.11.

```
PROGRAM CODE 6.11
void DList :: DeleteNode(int val)
{
    DLL_Node *curr, *temp;
```