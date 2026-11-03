```
printf("ENTER YOUR CHOICE");
scanf("%d",&choice);

switch(choice)
{
case 1: stack = push(stack);
break;
case 2: stack = pop(stack);
break;
case 3: display(stack);
break;
case 4: exit();
}
}
    getch();
}

push(nodeptr stack)
{
nodeptr temp;
int info;
printf("ENTER THE ELEMENT TO BE PUSHED");
scanf("%d",&info);
temp=(nodeptr)malloc(sizeof(nodeptr));
temp->info=info;
temp->next=stack;
stack=temp;
return(stack);

display(stack);

display(nodeptr stack)
{
printf("TOP");
while(stack != NULL)
{
    printf("%d",stack->info);
    stack=stack->next;
    printf("->");
}
printf("NULL\n");
}
nodeptr pop(nodeptr stack)
{
```