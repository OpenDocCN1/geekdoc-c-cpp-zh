```
{p->lchild=ptr->lchild,ptr->rchild=NULL;}
else[p->rchild=ptr->rchild,ptr->rchild=NULL;]
else
{
if (ptr->lchild=NULL&&ptr->rchild==NULL)
{
p->rchild=NULL,ptr=rNULL;}
else if (ptr->rchild!=NULL)
{
p->rchild=ptr->lchild,ptr=rNULL;}
else[p->rchild=ptr->rchild,ptr=rNULL;]
}
}
cout<<"<nitem<<"<"Is Successfully Deleted";
}
void traverse(struct BTREE *ptr)
{
if(ptr!=NULL)
{
cout<<ptr->data<<" ";
traverse (ptr->lchild);
traverse (ptr->rchild);
}
}
int searchele(struct BTREE*p,int key)
{
if (p!=NULL)
{
if (p->data==key)
k=1;
else
{
searchele (p->lchild,key) ;
searchele (p->rchild,key) ;
}
}
return k;
}
void main()
{
int ch,s;
clrscr();
while(1)
{
cout<<"<nBINARY TREE OPERATIONS\n1.CREATION\n2.INSERTION\n3.DELETION\n";
cout<<"4.TRAVERSE\n5.SEARCHING\n6.EXIT";
cout<<"nEnter Your Choice";
cin>>ch;
switch(ch)
```