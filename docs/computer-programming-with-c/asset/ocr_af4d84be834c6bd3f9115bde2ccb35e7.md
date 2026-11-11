```
```cpp
while(temp!=NULL && temp->data.getId()!=id)
{
    prev=temp;        /*store the old value of temp in
prev*/
    temp=temp->next;  /*move temp ahead*/
}
if(temp==NULL)
{
    cout<<"Employee with id="<<id<<"does not exists
in the list"<<endl;
}
else
{
    if(temp==head)
    {
        /*Node to be deleted is the first node*/
        head=head->next;
    }
    else
    {
        /*Node to be deleted is not the first node*/
        prev->next=temp->next;
    }
    cout<<"Employee Deleted"<<endl;
}
}
}
void main()
{
Node obj;
int answer =1;
int choice,x;
cout<<"Please select one of the following choices:"<<endl;
cout<<"1.Insert a node"<<endl;
cout<<"2.Traverse the list"<<endl;
cout<<"3.Delete a node"<<endl;
do
{
cout<<"Enter your choice"<<endl;
cin>>choice;
switch(choice)
{
```

```