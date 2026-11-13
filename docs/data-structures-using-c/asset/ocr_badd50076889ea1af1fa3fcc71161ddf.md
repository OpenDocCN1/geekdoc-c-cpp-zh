# 6.12 LINKED QUEUE

We studied about how to represent queues using sequential organization in Chapter 5. Such a representation is efficient if we have a circular queue of fixed size. However, there are many drawbacks of implementing queues using arrays. The fixed sizes do not give flexibility to the user to dynamically exceed the maximum size. The declaration of arbitrary maximum size leads to poor utilization of memory. In addition, the major drawback is the updating of front and rear. For correctness of the said implementation, the shifting of the queue to the left is necessary and to be done frequently. Here is a good solution to this problem which uses linked list. We need two pointers, front and rear. Figure 6.52 shows a linked queue which is easy to handle.

![](bbox=[0.23, 0.32, 0.88, 0.42])

Notice that the direction link for nodes is to facilitate easy insertion and deletion of nodes. One can easily add a node at the rear and delete a node from the front. One of the node structures could be as in Program Code 6.19.

```
PROGRAM CODE 6.19
class Student
{
public:
    int Roll_No;
    char Name[30];
    int Year;
    char Branch[8];
    Student *link;
};
class Queue
{
    Student *front, *rear;
public:
    Queue()
    {
        front = rear = Null;
    }
};
```