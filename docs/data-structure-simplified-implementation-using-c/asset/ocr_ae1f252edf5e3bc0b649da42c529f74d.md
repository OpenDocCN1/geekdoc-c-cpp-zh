```
front=NULL;
rear=NULL;
}
template<class t>
void queue<t>::enqueue(t x)
{
if(rear==NULL)
{
rear=new qnode<t>;
rear->next=NULL;
rear->info=x;
front=rear;
}
else
{
qnode<t> *temp;
temp=new qnode<t>;
temp->info=x;
temp->next=NULL;
rear->next=temp;
rear=temp;
}
}
template<class t>
void queue<t>::display()
{
qnode<t> *current;
if(front==NULL)
{
cout<<"queue is empty"<<endl;
return;
}
current=front;
while(current!=rear)
{
```