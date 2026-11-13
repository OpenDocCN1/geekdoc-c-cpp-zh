```
{
    cout<<"Item Already Exists";
    return;
}
}
if (ptr==NULL)
{
    n=(struct BST*)malloc(sizeof(struct BST));
    n->data=item;n->lchild=n->rchild=NULL;
    if (ptr1->data<item)
    ptr1->rchild=n;
    else
    ptr1->lchild=n;
}
```

```
void case1()
{
    if (ptr1->lchild==ptr)
    ptr1->lchild=NULL;
    else
    ptr1->rchild=NULL;
    cout<<"Element Is Successfully Deleted";
    ptr=NULL;
}
```

```
void case2()
{
    struct BST*ptr2,*y;
    int x=0;
    ptr2=ptr->rchild;
    if (ptr2->rchild==NULL&&ptr2->rchild==NULL)
    {
    ptr1->lchild=ptr2;
    ptr1->lchild->lchild=ptr2->lchild;
    }
    else if (ptr2->rchild==NULL&&ptr2->rchild!=NULL)
    {
    ptr1->rchild=ptr2;
    ptr1->rchild->lchild=ptr2->lchild;
    ptr2=NULL;
    free(ptr);
    }
    else
    {
    while (ptr2->lchild==NULL)
    ptr2=ptr2->lchild;
    if (ptr2->rchild!=NULL)
    {x=1;y=ptr2->rchild;}
    }
```