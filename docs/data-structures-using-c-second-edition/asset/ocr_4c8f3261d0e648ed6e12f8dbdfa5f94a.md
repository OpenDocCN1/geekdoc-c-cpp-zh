```
{
    ptr = start;
    printf("\n Deleted item is %d", ptr->data);
    start = start->next;
    free(ptr);
}
return start;
}
void display(struct node *start)
{
    struct node *ptr;
    ptr = start;
    if(start == NULL)
    printf("\nQUEUE IS EMPTY");
    else
    {
    printf("\nPRIORITY QUEUE IS : ");
    while(ptr != NULL)
    {
    printf("\t%d[%d]", ptr->data, ptr->priority);
    ptr=ptr->next;
    }
    }
}
Output
*******MAIN MENU******
1. INSERT
2. DELETE
3. DISPLAY
4. EXIT
Enter your option : 1
Enter the value and its priority : 5 2
Enter the value and its priority : 10 1
Enter your option : 3
PRIORITY QUEUE IS :
10[priority = 1] 5[priority = 2]
Enter your option : 4
```

# 8.4.4 Multiple Queues

When we implement a queue using an array, the size of the array must be known in advance. If the queue is allocated less space, then frequent overflow conditions will be encountered. To deal with this problem, the code will have to be modified to reallocate more space for the array.

In case we allocate a large amount of space for the queue, it will result in sheer wastage of the memory. Thus, there lies a tradeoff between the frequency of overflows and the space allocated. So a better solution to deal with this problem is to have multiple queues or to have more than one queue in the same array of sufficient size. Figure 8.31 illustrates this concept.

In the figure, a queue que[n] is used to represent two queues, queue A and queue B. The value of n is such that the combined size of both the queues will never exceed n. While operating on these queues, it is important to note one thing — queue A will grow from left to right, whereas queue B will grow from right to left at the same time.

![](bbox=[0.16, 0.78, 0.5, 0.84])

![](bbox=[0.16, 0.88, 0.5, 0.92])

Extending the concept to multiple queues, a queue can also be used to represent n number of queues in the same array. That is, if we have a queue que[n], then each queue i will be allocated an equal amount of space bounded by indices b[i] and e[i]. This is shown in Fig. 8.32.