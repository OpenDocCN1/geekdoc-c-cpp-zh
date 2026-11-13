```
{
    cout<<"memory allocation error\n";
    return;
}
if(head->flink==NULLL)
{
    temp->data=ele;
    head->blink=head;
    head->flink=temp;
    temp->flink=NULLL;
}
else
{
    for(temp1=head->flink;temp1->flink!=NULLL;temp1=temp1->flink)
    {
        temp1->flink=temp;
        temp->data=ele;
        temp->flink=NULLL;
        temp->blink=temp1;
    }
}
template<class t>
void listt<t>::inserta()
{
    t ele;
    int pos,i;
    cout<<"enter the element\n";
    cin>>ele;
    cout<<"enter the position\n";
    cin>>pos;
    temp=(struct node*)malloc(sizeof(struct node));
    if(temp==NULLL)
    {
        cout<<"memory allocation error\n";
        return;
    }
    if(head->flink==NULLL)
    {
        temp->data=ele;
        head->flink=temp;
        head->blink=head;
        temp->flink=NULLL;
    }
    else
    {
        for(temp1=head,i=1;i<pos;i++)
        {
            temp1=temp1->flink;
        }
```