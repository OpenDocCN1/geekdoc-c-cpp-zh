```
printf("\n 1. Push ");
printf("\n 2. Pop");
printf("\n 3. Quit");
printf("\n Input your choice :");
scanf("%d", &choice);
if(choice <1 || choice >3)
    printf("\n Incorrect choice-> Please retry");
} while(choice <1 || choice >3);

return(choice);
}

/* main function */

void main()
{
    struct link *start ;
    int choice;
    start = NULL;
    do
    {
        choice = main_menu();
        switch(choice)
        {
            case 1:
                start = push(start);
                printf("\n After push operation stack is as follows:\n");
                display(start);
                break;
            case 2:
                start = pop(start);
                break;
            default :
                printf("\n End of program");
        }
    } while(choice != 3);
}
```

Fig. 15.27

# Queues using Linked List

Like stacks, when implementing a queue using linked list, a node must be defined. As we know, the front end of a queue is used to remove data and the rear end is used to add data. The advantage of representing a queue using linked list is that it allows us to select any end to add and remove data items.

Removing the first node in a linked list is much easier than that of the last node. This is because, to remove the last node, we need to locate the previous node, which takes much time. So we can select the end of the linked list as rear and beginning of the list as front. Consider a list, which consists of three data items, as shown in Fig. 15.28.