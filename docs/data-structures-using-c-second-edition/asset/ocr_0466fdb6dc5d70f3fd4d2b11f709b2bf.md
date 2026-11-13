```
while(ptr != NULL)
{
    printf("\n %d", ptr -> data);
    ptr = ptr -> next;
}
}
return top;
}
struct stack *pop(struct stack *top)
{
    struct stack *ptr;
    ptr = top;
    if(top == NULL)
    printf("\n STACK UNDERFLOW");
    else
    {
    top = top -> next;
    printf("\n The Value being deleted is %d", ptr -> data);
    free(ptr);
    }
    return top;
}
int peek(struct stack *top)
{
    if(top==NULL)
    return -1;
    else
    return top ->data;
}
```

Output
******MAIN MENU******
1. PUSH
2. POP
3. Peek
4. DISPLAY
5. EXIT
Enter your option : 1
Enter the number to be pushed on stack : 100

# 7.6 MULTIPLE STACKS

While implementing a stack using an array, we had seen that the size of the array must be known in advance. If the stack is allocated less space, then frequent OVERFLOW conditions will be encountered. To deal with this problem, the code will have to be modified to reallocate more space for the array. In case we allocate a large amount of space for the stack, it may result in sheer wastage of memory. Thus, there lies a trade-off between the frequency of overflows and the space allocated. So, a better solution to deal with this problem is to have multiple stacks or to have more than one stack in the same array of sufficient size. Figure 7.20 illustrates this concept.

![](bbox=[0.312, 0.815, 0.75, 0.856])

Figure 7.20 Multiple stacks

In Fig. 7.20, an array STACK[n] is used to represent two stacks, stack A and stack B. The value of n is such that the combined size of both the stacks will never exceed n. While operating on