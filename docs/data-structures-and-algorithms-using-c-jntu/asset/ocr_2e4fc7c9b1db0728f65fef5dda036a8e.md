(a) Balanced AVL search tree before deletion

(b) Unbalanced AVL search tree after deletion

(c) Balanced AVL search tree after L1 rotation

(iii) L1 rotation

# Figure 12.26 L Category rotations

Program 12.2 gives the implementation of operations on AVL search trees.

# Program 12.2 AVL SEARCH TREE OPERATIONS

```
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
```