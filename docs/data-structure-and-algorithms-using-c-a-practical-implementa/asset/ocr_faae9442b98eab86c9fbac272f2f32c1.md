```
scanf("%d", &insert_node);
while(count--)
{
    if(node_number == insert_node)
    {
        newl = (struct link* )
        malloc(sizeof(struct link));
        first->next=newl;
        newl->next = node;
        printf("\n Input the node value: ");
        scanf("%d", &newl->info);
        opt=1;
        break;
    }
    else
    {
        node = node->next;
        first=first->next;
    }
    node_number ++;
}
if (opt==1)
{
    node = &start; /* Points to header node */
    node->info = node->info+1;
}
}
```

```
/* Display the list */
void display()
{
    node=&start;
    int count = node->info;
    do
    {
        printf( "\n%d ", node->info);
        node = node->next;
    }while(count--);
}
```

```
int main()
{
    create();
    printf("\n Before inserting a node list is as follows:\n");
    display();
    insertion();
    printf("\n After inserting a node list is as follows:\n");
    display();
}
```