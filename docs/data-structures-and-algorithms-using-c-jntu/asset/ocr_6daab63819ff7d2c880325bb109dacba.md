```
```c
while (loc!=NULL)
{
loc=loc->auxchild;
loc->height=max(findheight (loc->lchild),findheight (loc->rchild))+1;
}

void rrotate(tree*ptr,tree*prev)
{
tree*hold,*temp;
temp=ptr->lchild;
hold=temp->rchild;
temp->rchild=ptr;
ptr->lchild=hold;
ptr->rchild=hold;
if (ptr==root)
root=temp;
else if (ptr==prev->lchild)
prev->lchild=temp;
else
prev->rchild=temp;
ptr->height=max(findheight (ptr->lchild),findheight (ptr->rchild))+1;
temp->height=max(findheight (temp->lchild),findheight (temp->rchild))+1;
adheight (temp);
temp->auxchild=prev;
if (hold!=NULL)
{
hold->auxchild=ptr;
ptr->auxchild=temp;
}

void lcrotate(tree*ptr,tree*prev)
{
tree*hold,*temp;
temp=ptr->rchild;
hold=temp->lchild;
temp->lchild=ptr;
ptr->rchild=hold;
if (ptr==root)
root=temp;
else if (ptr==prev->rchild)
prev->rchild=temp;
else
prev->lchild=temp;
ptr->height=max(findheight (ptr->lchild),findheight (ptr->rchild))+1;
temp->height=max(findheight (temp->lchild),findheight (temp->rchild))+1;
adheight (temp);
temp->auxchild=prev;
if (hold!=NULL)
hold->auxchild=ptr;
ptr->auxchild=temp;
}
```
```