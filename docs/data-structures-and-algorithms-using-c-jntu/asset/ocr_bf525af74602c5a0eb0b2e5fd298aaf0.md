```
template<class t>
void queuee<t>::display()
{
    if(rear==NULL)
    {
        cout<<"linked list is empty\n";
        return;
    }
    for(temp=front;temp!=rear;temp=temp->link)
    {
        cout<<temp->data<<" ";
    }
    cout<<temp->data<<" ";
}

void main()
{
    int ch;
    queuee<int>q;
    clrscr();
    while(1)
    {
        cout<<"\nmenu\n";
        cout<<"1.push\n";
        cout<<"2.pop\n";
        cout<<"3.display\n";
        cout<<"4.exit\n";
        cout<<"enter your choice\n";
        cin>>ch;
        switch(ch)
        {
            case 1:
            g.push();
            break;
            case 2:
            g.pop();
            break;
            case 3:
            g.display();
            break;
            case 4:
            exit(0);
            break;
        }
    }
}
```