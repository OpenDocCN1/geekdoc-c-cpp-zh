
node of a binary tree. There are many operations that are often performed on a tree such as search a node, print some information, insert a node, delete a node, and so on. All such operations need the traversal through a tree.

This operation is used to visit each node (exactly once). A full traversal of a tree visits nodes of a tree in a certain linear order. This linear order could be familiar and useful. For example, if the binary tree contains an arithmetic expression, then its traversal may give us the expression in infix, postfix, or prefix notations.

There are various traversal methods. For a systematic traversal, it is better to visit each node (starting from the root) and its two subtrees in the same way. In other words, when traversing, we need to treat each node and its subtree in the same fashion. If we let L, D, and R stand for moving left, data, and moving right, respectively Fig. 7.32, when a node is left, then there are six possible combinations—LDR, LRD, DLR, DRL, RLD, and RDL.

![](img/a99ec79093c067f0bed8f1086197950e_317_0.png)

Fig. 7.32 Components of a subtree

Consider the binary tree shown in Fig. 7.33. This tree represents a binary tree. We have studied all the notations of an expression tree and its inter-conversions in Chapter 3.

![](img/a99ec79093c067f0bed8f1086197950e_317_1.png)

Fig. 7.33 A binary tree representing an arithmetic expression

Let us see the result of each of the six traversals.

| Traversal | Result |
| :--- | :--- |
| LDR: | 5-6+3x8/4 |
| LRD: | 56-384/x+ |
| DLR: | +-56x3/84 |
| DRL: | +x/483-65 |
| RDL: | 4/8x3-6-5 |
| RLD: | 48/3x65-+ |

We can notice that DLR and RLD, LDR and RDL, and LRD and DRL are mirror symmetric. If we adopt the convention that traversing is done left before right, only then, the three traversals, that is, LDR, LRD, and DLR, are fundamental. These are called as inorder, postorder, and preorder traversals because there is a natural correspondence between these traversals producing the infix, postfix, and prefix forms of an arithmetic expression, respectively.

## 7.7.1 Preorder Traversal

In this traversal, the root is visited first followed by the left subtree in preorder and then the right subtree in preorder. The tree characteristics lead to naturally implement the tree traversals recursively. It can be defined in the following steps:

### Preorder (DLR) Algorithm

- 1. Visit the root node, say D.
- 2. Traverse the left subtree of the node in preorder.
- 3. Traverse the right subtree of the node in preorder.

Let us consider the tree in Fig. 7.34.

A preorder traversal of the tree in Fig. 7.34 visits the node in a sequence: A B D E G C F. For an expression tree, the preorder traversal yields a prefix expression (Fig. 7.35).

![](img/a99ec79093c067f0bed8f1086197950e_318_0.png)

![](img/a99ec79093c067f0bed8f1086197950e_318_1.png)

The preorder says, ‘visit a node, traverse left, and continue moving. When you cannot continue, move right and begin again or move back, until you can move right and stop’. The Preorder() function can be written as both recursive and non recursive.

```
void BinaryTree :: Preorder(TreeNode*)
{
if (Root != Null)
{
cout << Root->Data;
Preorder(Root->Lchild);
Preorder(Root->Rchild);
}
}
```

![](img/a99ec79093c067f0bed8f1086197950e_318_2.png)

Let us consider the tree in Fig. 7.36. This tree contains an arithmetic expression with the binary operators add (+), multiply (x), divide (/), exponentiation (^), and variables A, B, C, D, and E.

![](img/a99ec79093c067f0bed8f1086197950e_319_0.png)

Fig. 7.36 Binary tree for expression

It gives us the prefix expression +x/^A ^BCDE. The preorder traversal is also called as depth-first traversal.

## 7.7.2 Inorder Traversal

In this traversal, the left subtree is visited first in inorder followed by the root and then the right subtree in inorder. This can be defined as the following:

### Inorder (LDR) Algorithm

- 1. Traverse the left subtree of the root node in inorder.
- 2. Visit the root node.
- 3. Traverse the right subtree of the root node in inorder.

Let us consider the binary tree in Fig. 7.34. An inorder traversal of a tree visits the node in the following sequence.

**Inorder sequence: D B E G A F C** An inorder expression traversal of the tree in Fig. 7.35, which is an expression tree, yields an inorder expression as A x B + D and for Fig. 7.36 yields an inorder expression as ((A / B ^ C) x D) + E.

The Inorder() function simply calls for moving down the tree towards the left until it can no longer proceed. So next, we visit the node, move one node to the right, and continue again. If we cannot move, move one node to the right and continue again. If we cannot move to the right, go back one more node and then continue. The inorder traversal is also called as symmetric traversal. This traversal can be written as a recursive function as follows:

```
void BinaryTree :: Inorder(TreeNode*)
{
if (Root != Null)
{
Inorder(Root->Lchild);
cout << Root->Data;
Inorder(Root->Rchild);
}
}
```

![](img/a99ec79093c067f0bed8f1086197950e_319_1.png)

## 7.7.3 Postorder Traversal

In this traversal, the left subtree is visited first in postorder followed by the right subtree in postorder and then the root. This is defined as the following:

### Postorder (LRD) Algorithm

- 1. Traverse the root's left child (subtree) of the root node in postorder.
- 2. Traverse the root's right child (subtree) of the root node in postorder.
- 3. Visit the root node.

Let us consider the binary tree in Fig. 7.34. The postorder traversal yields the following sequence:

**Postorder sequence: D G E B F C A** For the expression tree in Fig. 7.35, the postorder traversal yields a postfix expression as the following:
= A x B x D +

For the tree in Fig. 7.36, the postfix expression by the postorder traversal is ABCx// DxE+. The postorder traversal says, “traverse left and continue again. When you cannot continue, move right and begin again or move back until you can move right and visit the node.”

```
void BinaryTree :: Postorder(TreeNode*)
{
    if (Root != Null)
    {
        Postorder(Root->LChild);
        Postorder(Root->RChild);
        cout << Root->Data;
    }
}
```

![](img/a99ec79093c067f0bed8f1086197950e_320_0.png)

## 7.7.4 Non-recursive Implementation of Traversals

We have defined the recursive traversals. These are easy to read and understand. However, a language translator such as a compiler will be burdened to carry out the execution. Let us go for the other non-recursive approach for these algorithms. Let us write a non-recursive implementation using stacks. Here, at the time of left or right traversal, when the left or right node is the root of the other subtree, the current node is to be stacked for further traversal.

### Non-recursive Preorder Algorithm

- 1. Tmp = Root
- 2. while (stack not empty) do
-     begin
-     if (Tmp is not null) then
-     begin
-     visit(Tmp->data)
-     Push(Tmp->LChild)

```
Tmp = Tmp->Lchild
else if (stack is empty)
then exit
else
Tmp = Pop()
Tmp = Tmp->Rchild
end
end
3. stop
```

The C++ implementation of the non-recursive preorder algorithm is given in Program Code 7.3.

```
PROGRAM CODE 7.3
void BinaryTree :: Preorder_Non_Recursive()
{
TreeNode *Tmp = Root;
stack S;
while(1)
{
while(Tmp != Null)
// traverse left till left is null and push
{
S.Push(Tmp);
cout << Tmp->Data;
Tmp = Tmp->Lchild;
}
if(S.IsEmpty()) return;
// if stack is not empty then pop one and go to right
Tmp = S.Pop();
Tmp = Tmp->Rchild;
// if stack is empty stop the process
}
}
```

We need stack and queue for tree operations such as depth-first and breadth-first traversals. Program Code 7.4 uses these two data structures:

```
PROGRAM CODE 7.4
class stack
{
public:
TreeNode *stk[max];
int data, top;
stack *S;
public:
stack()
{
    top = -1;
}
int IsEmpty()
{
    if(top == -1)
        return 1;
    else
        return 0;
}
void Push(TreeNode *x)
{
    stk[top++] = x;
}
TreeNode *Pop()
{
    TreeNode *x;
    x = stk[top--];
    return(x);
}
};
class stack1
{
public:
    char stk1[max];
    int data, top;
public:
    stack1()
    {
        top = -1;
    }
    int IsEmpty1()
    {
        if(top == -1)
            return 1;
        else
            return 0;
    }
```
