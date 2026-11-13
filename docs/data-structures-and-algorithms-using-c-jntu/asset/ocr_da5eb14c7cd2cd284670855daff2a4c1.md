![](bbox=[0.05, 0.08, 0.48, 0.28])

# (e) After Rb0 colour change

![](bbox=[0.52, 0.08, 0.94, 0.28])

# (d) No imbalance

![](bbox=[0.38, 0.33, 0.62, 0.45])

# (f) After Rb1(type 1) rotation

# Figure 14.18 (Continued)

Consider a red-black tree shown in Figure 14.18(a) Deleting the elements 42, 94, 86, 78 and 61 from the tree calls corresponding rotations and colour changes. Their snapshots are shown in Figures 14.18(b)–14.18 (f). They are all self-explanatory.

# Program 14.1

```
/*To Implement the following RED BLACK TREE Operations
1.Insertion 2.Deletion 3.Searching 4.Traversing */
#include<stdio.h>
#include<conio.h>
#include<iostream.h>
struct RBT
{
int data,*color;
struct RBT*lchild,*rchild,*parent;
}*root;
typedef struct RBT node;
int s,k;
node *minimum(node *ptr)
{
while (ptr->lchild!=NULL)
ptr=ptr->lchild;
```