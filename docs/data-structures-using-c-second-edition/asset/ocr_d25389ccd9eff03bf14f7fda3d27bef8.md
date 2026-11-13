```
while(ptr!=q -> rear)
{
    printf("%d\t", ptr->data);
    ptr = ptr -> next;
}
printf("%d\t", ptr->data);
return q;
}
struct queue *delete_element(struct queue *q)
{
    struct node *ptr;
    ptr = q -> front;
    if(q->front == NULL)
    {
    printf("\n UNDERFLOW");
    }
    else
    {
    q->front = q -> front->next;
    printf("\n The value being deleted is : %d", ptr -> data);
    free(ptr);
    }
    return q;
}
int peek(struct queue *q)
{
    if(q->front=NULL)
    {
    printf("\n QUEUE IS EMPTY");
    return -1;
    }
    else
    return q->front->data;
}
```

```
**Output**
******MAIN MENU******
1. INSERT
2. DELETE
3. PEEK
4. DISPLAY
5. EXIT
Enter your option : 3
ENTER IS EMPTY
Enter your option : 5
```

# 8.4 TYPES OF QUEUES

A queue data structure can be classified into the following types:
1. Circular Queue 2. Deque 3. Priority Queue 4. Multiple Queue
We will discuss each of these queues in detail in the following sections.

# 8.4.1 Circular Queues

In linear queues, we have discussed so far that insertions can be done only at one end called the rear and deletions are always done from the other end called the front. Look at the queue shown in Fig. 8.13.

| 54 | 9 | 7 | 18 | 14 | 36 | 45 | 21 | 99 | 72 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

Figure 8.13 Linear queue

Here, FRONT = 0 and REAR = 9.