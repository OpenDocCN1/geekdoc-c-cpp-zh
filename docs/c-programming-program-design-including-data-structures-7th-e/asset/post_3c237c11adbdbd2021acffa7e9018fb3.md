
These operations require the list to be traversed. That is, given a pointer to the first node of the list, we must step through the nodes of the list.

Suppose that the pointer head points to the first node in the list, and the link of the last node is nullptr. We cannot use the pointer head to traverse the list because if we use head to traverse the list, we would lose the nodes of the list. This problem occurs because the links are in only one direction. The pointer head contains the address of the first node, the first node contains the address of the second node, the second node contains the address of the third node, and so on. If we move head to the second node, the first node is lost (unless we save a pointer to this node). If we keep advancing head to the next node, we will lose all of the nodes of the list (unless we save a pointer to each node before advancing head, which is impractical because it would require additional computer time and memory space to maintain the list).

Therefore, we always want head to point to the first node. It now follows that we must traverse the list using another pointer of the same type. Suppose that current is a pointer of the same type as head. The following code traverses the list:

```cpp
current = head;

while (current != nullptr)
{
    //Process the current node
    current = current->link;
}
```

For example, suppose that head points to a linked list of numbers. The following code outputs the data stored in each node:

```cpp
current = head;

while (current != nullptr)
{
    cout << current->info << " ";
    current = current->link;
}
```

## ITEM INSERTION AND DELETION

This section discusses how to insert an item into, and delete an item from, a linked list. Consider the following definition of a node. (For simplicity, we assume that the info type is int. The next section, which discusses linked lists as an abstract data type (ADT) using templates, uses the generic definition of a node.)

```cpp
struct nodeType
{
    int info;
    nodeType *link;
};
```

We will use the following variable declaration:

```cpp
nodeType *head, *p, *q, *newNode;
```

### INSERTION

Consider the linked list shown in Figure 16-7.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1127_0.png)

Figure 16-7  Linked list before item insertion

Suppose that p points to the node with info 65, and a new node with info 50 is to be created and inserted after p. Consider the following statements:

```cpp
newNode = new nodeType;   //create newNode
newNode->info = 50;       //store 50 in the new node
newNode->link = p->link;
p->link = newNode;
```

Table 16-1 shows the effect of these statements.

**TABLE 16-1  Inserting a Node in a Linked List**

| Statement | Effect |
|---|---|
| `newNode = new nodeType;` | A new node is created. The original list remains `head -> 45 -> 65 -> 34 -> 76 -> null`, with `p` pointing to the node containing `65`; `newNode` has no info value yet. |
| `newNode->info = 50;` | The new node's info field is set to `50`; the original list remains unchanged. |
| `newNode->link = p->link;` | The new node's link is set to the node following `p`, so the new node points to `34`. |
| `p->link = newNode;` | `p` now points to the new node, producing the list `head -> 45 -> 65 -> 50 -> 34 -> 76 -> null`. |

Note that the sequence of statements to insert the node is very important because to insert newNode in the list, we use only one pointer, p, to adjust the links of the node of the linked list. Suppose that we reverse the sequence of the statements and execute the statements in the following order:

```cpp
p->link = newNode;
newNode->link = p->link;
```

Figure 16–8 shows the resulting list after these statements execute.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1128_0.png)

**FIGURE 16-8**  List after the execution of the statement `p->link = newNode;` followed by the execution of the statement `newNode->link = p->link;`

From Figure 16–8, it is clear that newNode points back to itself and the remainder of the list is lost.

Using two pointers, we can simplify the insertion code somewhat. Suppose q points to the node with info 34 (see Figure 16–9).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1128_1.png)

**FIGURE 16-9**  List with pointers p and q

The following statements insert newNode between p and q.

```cpp
newNode->link = q;
p->link = newNode;
```

The order in which these statements execute does not matter. To illustrate this, suppose that we execute the statements in the following order:

```cpp
p->link = newNode;
newNode->link = q;
```

Table 16–2 shows the effect of these statements.

**TABLE 16-2  Inserting a Node in a Linked List Using Two Pointers**

| Statement | Effect |
|---|---|
| `p->link = newNode;` | Linked-list pointer diagram showing `newNode` inserted after `p` and before `q`. |
| `newNode->link = q;` | Linked-list pointer diagram showing `newNode` linked to `q`. |

### Deletion

Consider the linked list shown in Figure 16–10.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1129_0.png)

FIGURE 16–10  Node to be deleted is with `info 34`

Suppose that the node with `info 34` is to be deleted from the list. The following statement removes the node from the list:

```cpp
p->link = p->link->link;
```

Figure 16–11 shows the resulting list after the preceding statement executes.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1129_1.png)

FIGURE 16–11  List after the statement `p->link = p->link->link;` executes

From Figure 16–11, it is clear that the node with `info 34` is removed from the list. However, the memory is still occupied by this node, and this memory is inaccessible; that is, this node is dangling. To deallocate the memory, we need a pointer to this node. The following statements delete the node from the list and deallocate the memory occupied by this node.

```cpp
q = p->link;
p->link = q->link;
delete q;
```

Table 16-3 shows the effect of these statements.

**TABLE 16-3 — Deleting a Node from a Linked List**

| Statement | Effect |
|---|---|
| `q = p->link;` | Linked-list diagram showing `head` pointing to nodes `45 → 65 → 34 → 76`, with pointers `p` and `q`. |
| `p->link = q->link;` | Linked-list diagram showing `head` pointing to nodes `45 → 65 → 34 → 76`, with pointers `p` and `q`. |
| `delete q;` | Linked-list diagram showing `head` pointing to nodes `45 → 65 → 76`, with the deleted node removed. |

## Building a Linked List

Now that we know how to insert a node in a linked list, let us see how to build a linked list. First, we consider a linked list in general. If the data we read is unsorted, the linked list will be unsorted. Such a list can be built in two ways: forward and backward. In the forward manner, a new node is always inserted at the end of the linked list. In the backward manner, a new node is always inserted at the beginning of the list. We will consider both cases.

### BUILDING A LINKED LIST FORWARD

Suppose that the nodes are in the usual `info-link` form, and `info` is of type `int`. Let us assume that we process the following data:

```
2  15  8  24  34
```

We need three pointers to build the list: one to point to the first node in the list, which cannot be moved; one to point to the last node in the list; and one to create the new node. Consider the following variable declaration:

```cpp
nodeType *first, *last, *newNode;
int num;
```

Suppose that first points to the first node in the list. Initially, the list is empty, so both first and last are nullptr. Thus, we must have the statements:

```cpp
first = nullptr;
last = nullptr;
```

to initialize first and last to nullptr.

Next, consider the following statements:

```cpp
1  cin >> num;                                  //read and store a number in num
2  newNode = new nodeType;                      //allocate memory of type nodeType
   //and store the address of the
   //allocated memory in newNode
3  newNode->info = num;                         //copy the value of num into the
   //info field of newNode
4  newNode->link = nullptr;                     //initialize the link field of
   //newNode to nullptr
5  if (first == nullptr)                        //if first is nullptr, the list is empty;
   //make first and last point to newNode
{
5a    first = newNode;
5b    last = newNode;
6  } else                                      //list is not empty
{
6a    last->link = newNode;                   //insert newNode at the end of the list
6b    last = newNode;                         //set last so that it points to the
   //actual last node in the list
}
```

Let us now execute these statements. Initially, both first and last are nullptr. Therefore, we have the list as shown in Figure 16-12.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1131_0.png)

**FIGURE 16-12 Empty list**

After statement 1 executes, num is 2. Statement 2 creates a node and stores the address of that node in newNode. Statement 3 stores 2 in the info field of newNode, and statement 4 stores nullptr in the link field of newNode (see Figure 16-13).

![](img/d0be7fc6d804b63484835c6c8bc67a07_1131_1.png)

**FIGURE 16-13 newNode with info 2**
