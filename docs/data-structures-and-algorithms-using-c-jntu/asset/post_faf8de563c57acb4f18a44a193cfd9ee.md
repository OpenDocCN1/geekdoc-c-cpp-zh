
R1 rotation: The general representation of R1 rotation is depicted in Figure 12.22. Deleting a node from the right subtree C_r of an ancestor node C causes its balance factor to become +2. If the root of its left subtree has a balance factor as 1 then to rebalance the tree R1 rotation is to be invoked.

![](img/45784b9f0334626143002ec0d63692fd_405_0.png)

![](img/45784b9f0334626143002ec0d63692fd_405_1.png)

Consider the instance of R1 rotation depicted in Figure 12.23. After deleting node R, bf(Q) is updated to 0 and p to +2. Imbalance occurred and bf(M)=+1. So invoke R1 rotation. This balances the tree with M as the root node as depicted in Figure 12.23(c).

R-1 rotations: General representation of R-1 rotation is shown in Figure 12.24. The general representation of R-1 rotation is depicted in Figure 12.24. Deleting a node from the right subtree C_R of an ancestor node C causes its balance factor to become +2. If the root of its left subtree has a balance factor of -1 then to rebalance the tree R-1 rotation is to be invoked.

![](img/45784b9f0334626143002ec0d63692fd_406_0.png)

(a) Balanced AVL search tree before deletion

![](img/45784b9f0334626143002ec0d63692fd_406_1.png)

(b) Unbalanced AVL search tree after deletion

![](img/45784b9f0334626143002ec0d63692fd_406_2.png)

(c) Balanced AVL search tree after R-1 rotation

Figure 12.24 General representation of R-1 rotation

![](img/45784b9f0334626143002ec0d63692fd_406_3.png)

(a) Balanced AVL search tree before deletion

![](img/45784b9f0334626143002ec0d63692fd_406_4.png)

(b) Unbalanced AVL search tree after deletion

![](img/45784b9f0334626143002ec0d63692fd_406_5.png)

(c) Balanced AVL search tree after R-1 rotation

Figure 12.25 Example of R-1 rotation

Consider Figure 12.25 instance of R-1 rotation. Here node R is marked for deletion. After deleting it, bf(Q) the parent node is updated to 0 and that of its ancestor node P is bf(P) = +2. Now the tree is imbalanced as shown in Figure 12.25(b). As K the left subtree of P has its balance factor as -1 invoke R-1 rotation. After the rotation the AVL search tree is balanced with N as the root node as shown in Figure 12.25(c).

### L category rotations

When a node is deleted from the left subtree of A, the first ancestor node in the path to the root in upward direction leads bf(A) to -2. Then to rebalance an unbalanced AVL search tree, L category rotations are used. With respect to balance factor of the root of the right subtree of A these rotations can be further classified as L0 when its balance factor is 0, L1 when its balance factor is +1 and L-1 when its balance factor is -1. General representations of L0, L1 and L-1 rotations are depicted in Figure 12.26. Here $B'_L$ is the left subtree of B after deletion.

![](img/45784b9f0334626143002ec0d63692fd_407_0.png)

An AVL search tree may require more than one rotation to rebalance it after deletion, whereas insertion requires a single rotation.

![](img/45784b9f0334626143002ec0d63692fd_407_1.png)

(a) Balanced AVL search tree before deletion

(b) Unbalanced AVL search tree after deletion

(c) Balanced AVL search tree after L1 rotation

(iii) L1 rotation

Figure 12.26 L Category rotations

Program 12.2 gives the implementation of operations on AVL search trees.

## Program 12.2 AVL SEARCH TREE OPERATIONS

```c
/*AVL SEARCH TREE OPERATIONS
 * 1.INSERTION 2.DELETION 3.TRAVERSING 4.SEARCHING*/
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
#include<iostream.h>
struct AVLTREE
{
 struct AVLTREE*lchild,*rchild,*auxchild;
 int height,data;
};
typedef struct AVLTREE tree;
tree*root=NULL,*ptr,*ptr1;
int s,k=0,item;
int findheight(tree*ptr)
{
 if(ptr==NULL)
 return -1;
 else
 return ptr->height;
}
int max(int item1,int item2)
{
 if(item1>item2)
 return item1;
 else
 return item2;
}
void adheight(tree*loc)
{
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

void lrotate(tree*ptr,tree*prev)
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

void inorder(tree*ptr)
{
 if (ptr!=NULL)
 {
 inorder (ptr->lchild) ;
 cout<<ptr->data<<" " ;
 inorder (ptr->rchild) ;
 }
}
void checkbal(tree*ptr, int item)
{
 int hlchild,hrchild,bal;
 while (ptr->auxchild!=NULL)
 {
 ptr=ptr->auxchild;
 hlchild=findheight (ptr->lchild) ;
 hrchild=findheight (ptr->rchild) ;
 bal=hlchild-hrchild;
 if (bal>1)
 {
 if (item>ptr->lchild->data)
 {
 lrotate (ptr->lchild,ptr) ;
 rrotate (ptr,ptr->auxchild) ;
 }
 else
 rrotate (ptr,ptr->auxchild) ;
 }
 else if (bal < -1)
 {
 if (item<ptr->rchild->data)
 {
 rrotate (ptr->rchild,ptr) ;
 lrotate (ptr,ptr->auxchild) ;
 }
 else
 lrotate (ptr,ptr->auxchild) ;
 }
 }
}
void case1 ()
{
 if (ptr1->lchild == ptr)
 ptr1->lchild=NULL;
 else ptr1->rchild=NULL;
 adheight (ptr1) ;
 checkbal (ptr1,item) ;
 cout<<"Element Is Successfully deleted" ;
}

void case2()
{
if (ptr1->lchild == ptr)
{
if (ptr->lchild == NULL)
ptr1->lchild=ptr->rchild;
else
ptr1->lchild=ptr->lchild;
}
else
{
if (ptr1->rchild == ptr)
{
if (ptr->lchild == NULL)
ptr1->rchild=ptr->rchild;
else
ptr1->rchild=ptr->lchild;
}
}
adheight(ptr1);
checkbal(ptr1,item);
cout<<"Element Is Successfully deleted";
}

void delet()
{
int c=0;
ptr=root;
if (ptr==NULL)
{
cout<<"Tree Is Empty";
return;
}
cout<<"Which Item You Want To delete";
cin>>item;
if (ptr->data==item)
{
cout<<item<<"Is A Root Node Deletion Is Not Possible";
return;
}
if (ptr->data==item&&ptr->lchild == NULL&&ptr->rchild == NULL)
{
root=NULL;
cout<<item<<"Is Successfully deleted";
return;
}
while ((ptr!=NULL)&&(c==0))
{
if (item>ptr->data)
{
ptr1=ptr;
ptr=ptr->lchild;
}
else if (item < ptr->data)
{
ptr1=ptr;
ptr=ptr->rchild;
}
else
c=1;
}
if (c == 0)
{
cout<<"Item Does Not Exist..,Deletion Is Not Possible";
return;
}
}
void deleaf()
{
delet();
if (ptr->lchild==NULL&&ptr->rchild==NULL)
case1();
else
cout<<"Your Input Data Is Invalid";
}
void delone()
{
delet();
if ((ptr->lchild!=NULL&&ptr->rchild==NULL) || (ptr->lchild==NULL&&ptr->rchild!=NULL))
case2();
else
cout<<"Your Input Data Is Invalid";
}
void traverse(struct AVLTREE*ptr)
{
if (ptr!=NULL)
{
traverse(ptr->lchild);
cout<<ptr->data<<" ";
traverse(ptr->rchild);
}
}
void insert()
{
tree*loc,*prev;
cout<<"Enter Item To Be Insert";
cin>>item;
tree *tree=malloc(sizeof (tree));
ptr->data=item;
ptr->auxchild=ptr->lchild=ptr->rchild=NULL;
ptr->height=0;
if(root==NULL)
{
    root=ptr;
    cout<<"Item"<<item<<"Is Successfully Inserted";
    return;
}
loc=root;
while(loc!=NULL)
{
    prev=loc;
    if(item >= loc->data)
        loc=loc->lchild;
    else
        loc=loc->rchild;
}
ptr->auxchild=prev;
if(item >= prev->data)
    prev->lchild=ptr;
else
    prev->rchild=ptr;
adheight(ptr);
checkbal(ptr,item);
cout<<"Item"<<item<<"Is Successfully Inserted";
}
```

int searching(tree *p,int key)
{
    if(p!=NULL)
    {
        if(p->data==key)
            k=1;
        else
        {
            searching(p->lchild,key);
            searching(p->rchild,key);
        }
    }
    return k;
}
```

void main()
{
    int n,height,op,x;
    clrscr();
    x:
    {
        while(1)
        {
