```
void insert(struct link *node)
{
    int no= 0;
    int ins;
    node = start.next;
    before = &start;
    cout<<" \n Input value node the node you want to
insert :";
    fflush(stdin);
    cin>>ins;
    while(node)
    {
        if(node->info <= ins)
        {
            New = (struct link *) malloc(sizeof(struct
link));
            New->next = node;
            before->next = New;
            New->info = ins;
            break ;
        }
        else
        {
            node = node->next;
            before= before->next;
            no++;
        }
    }
}
```