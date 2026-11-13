
```
a) Repeatedly pop from the STACK and add to B (each operator on
top of stack until a left parenthesis is found)
b) Pop the left parenthesis from stack.
[End of loop]
7. Return
```

We can also convert an infix expression to prefix expression in three steps. In the first step reverse the infix expression and convert left parenthesis to right parenthesis and vice versa. Then in the second step, the modified infix expression is converted to postfix expression which algorithm discussed above. Finally, the postfix expression is reversed to get the equivalent prefix expression.

## QUEUE

The queue is also another useful non-primitive linear data structure in computer science. A real-life example of the queue is line or sequence of people or vehicles awaiting their turn to be attended to or to proceed.

**Definition:** A queue is a homogeneous collection of elements in which deletions can take place only at the front end, known as dequeue and insertions can take place only at the rear end, known as enqueue.

The element to enter the queue first will be deleted from the queue first. That is why a queue is called First-In-First-Out (FIFO) system.

The concept of the queue can be understood by our real life problems. For example, a customer comes and join in a queue to take the train ticket at the end (rear) and the ticket is issued from the front end of the queue. That is, the customer who arrived first will receive the ticket first. It means the customers are serviced in the order in which they arrive at the service center.

### Operations on Queue

The queue is an abstract data type since it is defined in terms of operations on it and its implementation is hidden. Therefore, the queue can be implemented with an array or with the help of the linked list. The queue includes a finite sequence of the same type of items with the different operations described in table 6.3.

| Operation | Description |
| :--- | :--- |
| Creation | This operation creates a queue and initialization is done here. |
| isempty | This operation checks whether the queue is empty or not. |
| isfull | This operation checks whether the queue is full or not. |
| Insertion (Enqueue) | This operation inserts an item only at the rear of the queue when the queue is not full. |
| Deletion (Dequeue) | This operation deletes an item only from the front of the queue when the queue is not empty. |
| Peek | This operation returns the value of the front of the queue without removing the element from the queue. |

### Table 6.4: Difference between stack and queue

| Stack | Queue |
| :--- | :--- |
| In the stack, items are inserted and deleted at the one end of the list | In the queue, items are inserted at one end (called rear) and deleted at another end (called the front) |
| Stack is Last-In-First-out system | The queue is the First-in-First-out system |

### Queue Representation with Array

The array can be used to implement a queue of fixed size, therefore only fixed a number of data items can be inserted and deleted. Consider the following example, the queue of size 5, therefore maximum only 5 data items can be inserted. The front index always keeps track of the last deleted item from the queue and rear index always keep track of the last inserted item in the queue. Initially, front and rear both are initialized by -1 (for the zero-based array) when there are no items in the queue, i.e. the queue is empty.

When a new item is inserted in the queue, the rear is incremented by 1 before the item is stored in the queue. Once all the five items are inserted, then rear is 4, as shown in the figure 6.4. Now, if we try to insert next item, it leads to an overflow condition. It indicates that the queue is full and we cannot insert the new item.

### Algorithm to insert an item to rear of a queue by using an array

```
ALGORITHM: ENQUEUE (Q, ITEM)
[Q is an array represent queue and ITEM is deleted item]
1. [check overflow]
   If Rear = MAX - 1 then
   a) Print: Queue is Full
   b) Return
2. Set Rear = Rear + 1
3. Q[Rear] = ITEM
4. Return
```

When an item is deleted from the queue, the front is incremented by 1, before the item is removed from the queue. Now, if front = rear then we try to delete an item, it results in underflow condition. It indicates that the queue is empty and we cannot delete an item. Whenever the queue is found empty, then to reuse the empty slots at the front of the queue we can reset the front and rear by -1.

### Algorithm to delete from the front of a queue by using an array

```
ALGORITHM: DEQUEUE (Q, ITEM)
[Q is an array represent queue and ITEM is inserted item]
1. [Check underflow]
   If Rear = Front then
   a) Print: Queue is Empty
   b) Return
2. Set Front = Front+1
3. ITEM = Q[Front]
4. If Rear = Front then
   Set Front = Rear = -1
5. Return
```

Therefore, it is required to check overflow and underflow conditions whenever insertions and deletions operations take place.

![](img/723fa3ef35f5102eb67dc45b74bb823d_154_0.png)

### Queue Representation with Linked List

Singly linked list can be used to represent a queue, which is also known as Linked Queue. In this representation, any number of data items can be inserted and deleted. The front and rear pointers always keep track of the first node and the last node in the linked list respectively. Initially, front and rear are initialized by null (i.e. front = rear = null), when there are no items in the queue, that means the queue is empty. The linked list header acts as the front of the queue. All deletion operations take place at the front of the list. All insertion operations take place at the end of the list. If the queue contains a single element then front and rear points to head/new node (i.e. front = rear = head).

When a new item is inserted in the queue, a new node is inserted at the end of the linked list, the rear points to the new node. When an item is deleted from the queue, the node from the front of the queue is deleted. Now, if front = null then if we try to delete an item, it results in underflow condition. It indicates that the queue is empty and we cannot delete an item. Whenever the queue is found empty, we can reset the front and rear by null.

### Algorithm: insert an item to rear of a queue using linked list

```
Algorithm: ENQUEUE (FRONT, REAR, ITEM)
[FRONT points to the first node and REAR points to the last node of the linked list. ITEM is the inserted value]
1. Allocate memory for NEW node.
2. If NEW = NULL then Print: Out of memory and Return
3. Set NEW → DATA = ITEM
4. Set NEW → LINK = NULL
5. If REAR = NULL then
   Set FRONT = REAR = NEW
   Else
   Set REAR -> LINK = NEW
   Set REAR = NEW
   [End of If]
6. Return
```

### Algorithm to delete from the front of a queue using linked list

```
Algorithm: DEQUEUE (FRONT, REAR, ITEM)
[FRONT points to the first node and REAR points to the last node of the linked list. ITEM is the deleted value]
1. If FRONT = NULL then Print: Queue is underflow and Return
2. Set P = FRONT
3. Set ITEM = P -> DATA
4. Set FRONT = P -> LINK
5. If FRONT = NULL then Set REAR = NULL
6. Set P -> LINK = NULL
7. De-allocate memory for node P
8. Return
```

### Comparisons of queue representation using linked list over the array

- The array is fixed size, therefore, a number of elements will be limited in the queue. Since linked list is dynamic and can be changed easily, so the number of elements can be changed.
- The pointers in linked list consume additional memory compared to an array.
- In array implementation, sometimes dequeue operation not possible, although there are free slots. This drawback can be overcome in linked list representation.
- In array and linked list enqueue and dequeue operations can be done in O (1).

### Application of Queue

- A major application of the queue is in simulation [see Kruse for example].
- In operating systems, queues are used for process management, I/O request handling, etc. Examples: Print queue of DOS, Message queue of Unix IPC.
- Queues are also used in some elegant algorithms like graph algorithms (breadth first search), radix sort etc.
- Different types of customer service software are designed using a queue for proper service to the customer.
- Example: Railway ticket reservation system

### Drawbacks of Linear Queue

The linear queue, when represented using an array, suffers from drawbacks. Once the queue is full, even though few elements are deleted from the front end and some free slots are created, it is not possible to insert new elements, as the rear has already reached the queue's rear most position. Consider the figure, the queue of size 5 and the front is 2, rear is 4. Now, we are not able to insert new data item into the queue, although there are free slots (first and second location) in the front of the queue, because of rigid rule followed by linear queue (insertion can be done at the rear end of the queue). It is also known as a boundary case problem.
