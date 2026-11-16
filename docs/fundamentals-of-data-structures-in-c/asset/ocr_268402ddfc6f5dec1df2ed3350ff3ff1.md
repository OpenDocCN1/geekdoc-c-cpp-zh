```
case 5 :
    view();
    break;
default:
    printf("\n End of Run of your Program . . .");
    exit(0);
}
}
```

```
void displayMenu()
{
    printf("\n Representation of stack using single linked lists . . .");
    printf("\n\t 1. Push ");
    printf("\n\t 2. Pop ");
    printf("\n\t 3. Peek ");
    printf("\n\t 4. Size ");
    printf("\n\t 5. View ");
    printf("\n\t 6. Exit ");
}
```

```
stack *getNode()
{
    return((stack *)malloc(sizeof(stack)));
}
```

```
void releaseNode(stack *newnode)
{
    free(newnode);
}
```

```
int push(int value)
{
    extern stack *topStk;
    stack *newptr;
    if(isFull())
    return -1;
    newptr = getNode();
    newptr -> data = value;
    newptr -> next = topStk;
    topStk = newptr;
    return 0;
}
```