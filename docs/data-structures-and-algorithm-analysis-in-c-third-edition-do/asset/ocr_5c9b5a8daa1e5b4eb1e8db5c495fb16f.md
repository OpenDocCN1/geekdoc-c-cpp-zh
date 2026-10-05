106

Chap. 4 Lists, Stacks, and Queues

![](bbox=[0.418, 0.175, 0.58, 0.24])

**Figure 4.7** Initial state of a linked list when using a header node.

Implementations for member functions of the **list** class are straightforward. However, **insert** and **remove** should be studied carefully.
Inserting a new node is a three-step process. First, the new node is created and the new node is stored into it. Second, the **next** field of the new list node is assigned to point to the current node (the **after** the node that **curr** points to). Third, the **next** field of node pointed to by **curr** is assigned to the newly inserted node. The following line in the **insert** method of Figure 4.8 does all of these steps.

```
curr->next = new Link<E>(it, curr->next);
```

Operator creates the new link node and calls the **Link** class constructor, which takes two parameters. The first is the element. The second is the value to be placed in the list's **next** field, in this case "curr->next". Figure 4.9 illustrates this three-step process. The new node is added, **tail** is pushed forward if the new element was added to the end of the list. Insertion requires $\Theta(1)$.
Removing a node from the linked list requires only that the appropriate pointer be redirected around the node to be deleted. The following lines from the **remove** method of Figure 4.8 do precisely.

```
Link<E>* l1mp = curr->next; // Remember link node
curr->next = curr->next->next; // Remove from list
```

We are careful not to "lose" the memory for the deleted node. So, temporary **l1mp** is first assigned to point to the node being removed. A call to **delete** is used to return the old node to free storage. Figure 4.10 illustrates the **remove** method. Assuming that the free **delete** operator takes constant time, removing an element requires $\Theta(1)$.

Method next moves **curr** one position toward the tail of the list, which takes $\Theta(1)$ time. Method **prev** moves **curr** one position toward the head of the list. In a singly linked list, there is no pointer to the previous node. Thus, the only alternative is to march down the list from the beginning until we reach the current node (always sure to remember the node before it, because that is what we really need). This takes $\Theta(n)$ time in the average and worst cases. Implementation of method **moveToPos** is similar in finding the $i$-th position requires matching down $i$ positions from the head of the list, taking $\Theta(i)$.

Implementations for the remaining operations require $\Theta(1)$ time.