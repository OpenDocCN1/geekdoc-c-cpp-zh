# A. Program to create BST (Non-recursive)

First we would like to define the structure of the BST. The structure of the BST comprise of three items i.e. left child pointer, right child pointer, and the data part. Structure of the BST, as discussed above has been defined as follows:

```
class tnode
{
public:
int info;
tnode *left, *right;
};
```

It is significant to understand that the member created here must be public, otherwise they will not be accessible outside the class.

Class to create the BST, along with the members has been shown below:

```
class bst
{
tnode *root;
void create(int);
};
```

Creation of a tree is started with the root node. This can be accomplished by the following statements.

```
root=new tnode;
root->left=root->right=NULL;
root->data=element;
```

Consequently, structure as illustrated in the following diagram will be created.

```
// Program to create a BST
void bst::create(int element)
{
//creating the root of bst
if(root==NULL)
{
root=new bnode;
root->info=element;
root->left=root->right=NULL;
return;
}
```