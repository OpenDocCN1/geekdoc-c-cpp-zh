```
```cpp
}

ptr2=obj.head;

for(i=1;i<obj.count;i++)       //include the remaining of the second
                                polynomial nodes
{
flag=0;
node *ptr1=head;
for(j=1;j<=count;j++)
{
if(ptr2->coef==ptr1->coef)
{
flag=1;break;
}
ptr1=ptr1->link;
}
if(flag!=1)
{
ptr->val=ptr2->val;
ptr->coef=ptr2->coef;
node *p=new node;
ptr->link=p;
back=ptr;
ptr=p;
p4.count=p4.count+1;
ptr1=ptr1->link;
}
ptr2=ptr2->link;
}
ptr->link=NULL;
return(p4);
}
void main()
{
polynomial p1;
polynomial p2;
polynomial p3;

p1.create();              //create the first polynomial
p2.create();              //create the second polynomial

cout<<"The structure of first polynomial"<<endl;
p1.display();
```
```