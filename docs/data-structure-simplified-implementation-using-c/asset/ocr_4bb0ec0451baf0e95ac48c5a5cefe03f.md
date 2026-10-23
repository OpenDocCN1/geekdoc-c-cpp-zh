```
void queue::display()
{
    qnode *current;
    if(front==NULL)
    {
    cout<<"queue is empty"<<endl;
    return;
    }
    current=front;
    while(current!=rear)
    {
    cout<<current->info<<endl;
    current=current->next;
    }
    cout<<current->info<<endl;
}
```

The isEmpty () is one of the other functions that has the significant role in this program. It can supports both the enqueue and dequeue. During enqueue, it can be used to check whether the queue is empty or not. Correspondingly, the next course of action can be initiated.

This function also plays a significant role while calling the dequeue function. We can include isEmpty() into other functions as a condition. If the queue is empty then dequeue operation cannot be performed. isEmpty() function has been defined in the following program.

```
int queue::isEmpty()
{
    int flag=0;
    if(front==NULL)
    {
    flag=1;
    }
    return flag;
}
```

All the above discussed functions can be called from the main function. Order and arguments to be passed have been given in the main function. Same has been depicted in the following main function.