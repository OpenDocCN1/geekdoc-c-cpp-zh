

伸展树不需要平衡或高度信息，因此更容易实现。在长检索序列上，伸展树比AVL树更便宜。这通过摊还分析的技术来证明。它是对一系列操作的分析，其中昂贵的操作与较便宜的操作进行平均。如果O(n)是一次访问的时间复杂度，那么对于m个操作的序列，伸展树中访问的摊还分析是O(mlog n)。

## 14.4.1 伸展旋转

对伸展树执行的所有操作与对二叉搜索树执行的操作相同。但是执行操作后，树会相对于引用节点进行伸展。也就是说，该节点使用称为伸展旋转的机制向上移动到根节点。它们与AVL树旋转相似，并遵循从节点到根节点的自下而上方法。

伸展树的目的是使引用或访问的节点成为根节点。在此过程中，受影响的包括被访问节点x及其父节点px和祖父节点gx。要执行伸展，x在每一步都应向上移动两层。当父节点px成为根节点时，伸展只剩下最后一步。即x在根节点下方一步，需要单次旋转才能使x成为根节点。为此，需要跟踪从根节点到引用节点x的路径。当路径向左转时称为zig，向右转时称为zag。

因此，当x在树中仅下方一步时，路径要么是zig，要么是zag。当需要考虑两步时，路径将是四次旋转，即zig-zig、zig-zag、zag-zig或zag-zag中的一种。在从根节点到引用节点x的路径长度为偶数的情况下，使用相应的两步旋转序列。在长度为奇数的情况下，最终旋转将是相应的单步序列之一。单步和两步序列如图14.19所示。

### Zig

![](img/45784b9f0334626143002ec0d63692fd_483_0.png)

### Zag

![](img/45784b9f0334626143002ec0d63692fd_483_1.png)

### Zig-zig

```
Before splaying:
      gX
     /  \
   pX   gX_R
  /  \
 x   pX_R
/ \
x_L x_R

After splaying:
      x
     /  \
   x_L   pX
        /  \
      x_R   gX
           /  \
         pX_R gX_R
```

### Zig-zag

```
Before splaying:
      gX
     /  \
   pX   gX_R
  /  \
pX_L   x
     /  \
   x_L  x_R

After splaying:
      x
     /  \
   pX   gX
  /  \   \
pX  x_L x_R gX_R
```

### Zag-zig

```
Before splaying:
      gX
     /  \
  gX_L  pX
        /  \
       x  pX_R
      / \
    x_L x_R

After splaying:
      x
     /  \
   gX   pX
  / \   \
gX_L x_L x_R pX_R
```

### Zag-zag

![](img/45784b9f0334626143002ec0d63692fd_485_0.png)

图14.19（续）

执行删除操作时，由于删除的节点不出现在结果树中，伸展作用于删除节点的父节点。

考虑图14.20(a)所示的二叉搜索树。要在节点D处伸展树，从根节点到节点D的路径涉及E-C-D。在自下而上过程中执行zig-zag旋转，伸展后的结果树如图14.20(b)所示。

考虑图14.20(b)所示的树；要在G处伸展，从根节点到节点G的路径涉及D-E-M-G。在自下而上过程中，第一步涉及zag-zig旋转。如图14.20(c)所示，G在根节点下方一步，因此现在应用zag旋转使G成为根节点。如图14.20(d)所示。

![](img/45784b9f0334626143002ec0d63692fd_485_1.png)

(a) 二叉搜索树

图14.20 伸展二叉搜索树

![](img/45784b9f0334626143002ec0d63692fd_486_0.png)

(b) 在D处伸展：Zig-zag

![](img/45784b9f0334626143002ec0d63692fd_486_1.png)

(c) 在G处伸展；步骤1：Zig-zig

![](img/45784b9f0334626143002ec0d63692fd_487_0.png)

### (d) 在G处伸展；步骤2：Zig

图14.20（续）

使用42、60、17、75构建伸展树。序列中的元素可以如图14.21所示。

![](img/45784b9f0334626143002ec0d63692fd_487_1.png)

图14.21 伸展树中插入操作的步骤

将42作为伸展树的根节点插入的步骤如图14.20(a)所示。插入60会导致zig旋转，如图14.20(b)所示。插入17会导致zig-zag旋转，如图14.20(c)所示。插入75需要两次伸展旋转；相应的步骤如图14.20(d)所示。

## 14.4.2 摊还分析

基于给定算法的输入实例，计算最佳、平均和最坏情况时间复杂度，这称为算法分析。

摊还分析分析一系列操作，以表明虽然序列中的单个操作可能很昂贵，但每个操作的平均成本较低。即使取平均值，也不涉及概率。摊还分析保证了每个操作在最坏情况下的平均性能。然而，摊还分析不是平均情况分析。在一组独立输入实例上，算法完成的工作由平均情况分析处理。但是，摊还分析在相关或关联实例上做同样的事情。

伸展树的摊还时间复杂度为O(log n)。单个操作可能不具有O(log n)，但伸展树中m个操作的摊还复杂度将是O(m log n)。

摊还分析用于建立在使用伸展技术的二叉搜索树中检索节点的效率。对于二叉搜索树t，设nodes(x)为以x为根节点的子树中的节点数：

- rank(x) = log(nodes(x))
- rank(root(t)) = log(n)，其中n是树中的节点数。
- potential(t) = \sum_{x is a node of t} rank(x)。
- 始终有 nodes(x) + 1 <= nodes(parent(x)) 且 rank(x) < rank(parent(x))。

访问节点x时，摊还成本可定义为函数 amCost(x) = cost(x) + potential(t) – potential(t)

其中potential(t)是势能，(t)指访问前后树的势能。应注意，旋转仅影响被访问节点x、其父节点px和祖父节点gx的秩。

## 程序14.2

```
/*To implement the following SPLAY TREE Operations
 1. Insertion 2.Deletion 3.Searching 4.Traversing*/
#define N 50
#include<iostream.h>
#include<conio.h>
#include<stdio.h>
struct SPLAY
{
int data;
struct SPLAY*lchild,*rchild;
}*root=NULL,*r=NULL,*ptr,*ptr1,*ne,*ptr2;
int item,k=0,s,a[N],i,*ptr,count=0,ele;
void splay(struct SPLAY*ptr)
{
if(ptr!=NULL)
{
splay1(ptr->lchild);
a[i++]=ptr->data;
splay1(ptr->rchild);
}
void splay2()
{
int j;
if(count>1)
{
splay1(r);
for(j=0;j<i;j++)
{
ptr=root;
if(ptr->data!=a[j]&&a[j]!=ele){
item=a[j];
while(ptr!=NULL)
{
if(item<ptr->data)
{
ptr1=ptr;
ptr=ptr->lchild;
}
else if(item>ptr->data)
{
ptr1=ptr;
ptr=ptr->rchild;
}
}
if(ptr==NULL)
{
ne=(struct SPLAY*)malloc(sizeof(struct SPLAY));
ne->data=item;ne->lchild=ne->rchild=NULL;
if(ptr1->data<item)
ptr1->rchild=ne;
else
ptr1->lchild=ne;
}
}
}
}
}
r=root;
if(count>1)
i=0;
void insert()
{
int j;
ne=(struct SPLAY*)malloc(sizeof(struct SPLAY));
ne->data=item;ne->lchild=ne->rchild=NULL;
root=ne;
count++;
splay2( );
}
void splay3( )
{
int c=0;
ptr=root;
while((ptr!=NULL)&&(c==0))
{
if(item<ptr->data)
ptr=ptr->lchild;
else if(item>ptr->data)
ptr=ptr->rchild;
else
c=1;
}
ne=(struct SPLAY*)malloc(sizeof(struct SPLAY));
ne->data=ptr->data;ne->lchild=ne->rchild=NULL;
root=ne;
splay2( );
}
void delet( int item)
{
int c=0;
struct SPLAY*pt;
ptr=root;
if(ptr==NULL)
{
cout<<"Tree Is Empty";
return;
}
if((ptr->data==item)&&(ptr->lchild==NULL&&ptr->rchild==NULL))
{
free(root);
root=NULL;
return;
}
else if(ptr->data==item)
{
cout<<"Deletion Is Not Possible(It Is Root Node)";
return;
}
else
while((ptr!=NULL)&&(c==0))
{
    if(item<ptr->data)
    {
        ptr1=ptr;
        ptr=ptr->lchild;
    }
    else if(item>ptr->data)
    {
        ptr1=ptr;
        ptr=ptr->rchild;
    }
    else
    {
        c=1;
    }
    if(c==0)
    {
        cout<<"Item Does Not Exist...,Deletion Is Not Possible";
        return;
    }
    ne=(struct SPLAY*)malloc(sizeof(struct SPLAY));
    ne->data=ptr1->data;ne->lchild=ne->rchild=NULL;
    root=ne;
    splay2();
    count--;
}
void traverse(struct SPLAY*ptr)
{
    if(ptr!=NULL)
    {
        cout<<ptr->data<<" ";
        traverse(ptr->lchild);
        traverse(ptr->rchild);
    }
}
int searching(struct SPLAY*p,int key)
{
    if(p!=NULL)
    {
        if(p->data==key)
        {
            k=1;
        }
        else
        {
            searching(p->lchild,key);
            searching(p->rchild,key);
        }
    }
    return k;
}
```

