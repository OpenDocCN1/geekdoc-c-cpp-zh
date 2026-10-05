# DATA STRUCTURES USING C

177

```
else
{
    printf("Enter the data to push:");
    scancf("%d",&data);
    temp->data=data;
    rear->next=temp;
    rear=temp;
    rear->next=NULL;
}
```

> After inserting the new node, it will become new REAR. so changing the REAR pointer

```
void view()
{
    struct stack *t;
    t=front;
    if(front==NULL)
        printf(\
Everything is deleted!!!Please push some data\n");
    else
    {
        while (t->next!=NULL)
        {
            printf("%d---", t->data);
            t=t->next;
        }
        printf("%d---", t->data);
    }
}
```

```
void del()
{
    struct stack *prev,*dummy;
    prev=front;
    if(front->next==NULL)
    {
        front=NULL;
        printf(\
nNothing can be deleted further!!!\n\n    }
    else
    {
        while (prev->next!=NULL)
        {
            dummy=prev;
            prev=prev->next;
        }
        rear=dummy;
        rear->next=NULL;
    }
    view();
}
```

# Program 11.3 Stack using linked lists