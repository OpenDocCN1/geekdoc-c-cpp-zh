```
```cpp
void marklist::del()
{
    node *ptr=head;
    int rollno;
    cout<<"\nEnter the roll no to be deleted:";
    cin>>rollno;
    if(rollno==ptr->data.rollno)
    {
        head=head->link;
        delete(ptr);
    }
    else
        while((rollno!=ptr->link->data.rollno)&&(ptr->link!=NULL))
            ptr=ptr->link;
    node *p=ptr->link;
    ptr->link=p->link;
    delete(p);
    display();
}

void marklist::sort()
{ int flag = 0;
    node *dptr=head;
    student data1;
    do
    {
        node *ptr=head;
        while(ptr->link!=NULL)
        {
            if(ptr->data.t<ptr->link->data.t)
                flag =1;
            else
                if (ptr->data.t==ptr->link->data.t)
                {
                    if (ptr->data.m1<ptr->link->data.m1)
                        flag =1;
                }
                else
                    if (ptr->data.m1==ptr->link->data.m1)
                    {
                        if (ptr->data.m2<ptr->link->data.m2)
                            flag =1;
                    }
                    else
                        if(ptr->data.m2==ptr->link->data.m2)
                        {
                            if(ptr->data.m3<ptr->link->data.m3)
                                flag = 1;
```
```