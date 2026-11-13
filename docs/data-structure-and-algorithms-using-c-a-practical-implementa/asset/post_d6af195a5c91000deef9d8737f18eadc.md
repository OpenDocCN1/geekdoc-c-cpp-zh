
```c
{
   inorder(node->left);
   printf(" %d", node->info);
   inorder(node->right);
}
```

```c
void postorder (struct link *node)
{
   if (node)
   {
      postorder(node->left);
      postorder(node->right);
      printf(" %d", node->info);
   }
}
```

```c
void main()
{
   int list[100];
   int number = 0;
   int info;
   char ch='y';
   struct link *t;
   t = NULL;
   while(ch == 'y' || ch=='Y')
   {
      printf("\n Enter the value of the node");
      scanf("%d", &info);
      list[number++] = info;
      printf("\n DO YOU WANT TO CREATE MORE
NODES[Y/N]");
      scanf("%c",&ch);
   }
   number--;
   printf("\n Number of elements in the list is %d",
   number);
   t = binary(list, 0, number);
   output(t,1);
   printf("\n Pre-order traversal\n");
   preorder (t);
   printf("\n In-order traversal\n");
   inorder (t);
   printf("\n Post-order traversal\n");
   postorder (t);
}
```

## 8.6 Conversion of a Tree From Inorder and Preorder

INORDER : D B H E A F C I G
PREORDER : A B D E H C F G I
Choose the ROOT from the preorder and from inorder find the nodes in left and right and this process will continue up to all the elements are chosen from the preorder/inorder.

STEP1: From preorder A is the root and from inorder we will find that in the left of A (D,B,H,E) and in the right (F,C,I,G)

![](img/1faaa0256577c74e8a61f42967760aa8_267_0.png)

STEP2: Again from Preorder 'B' will be chosen as PARENT and from Inorder in the left of B (D) and in the right (H,E).

![](img/1faaa0256577c74e8a61f42967760aa8_267_1.png)

STEP3: From Preorder 'E' will chosen as the PARENT and from inorder on its left 'H' is present.

![](img/1faaa0256577c74e8a61f42967760aa8_267_2.png)

STEP4: From Preorder we will choose 'C' as the PARENT and from in-order we observe that in the left of 'C' (F) will placed and in the right (I,G)

![](img/1faaa0256577c74e8a61f42967760aa8_268_0.png)

STEP5: From the PREORDER we observe that 'G' is the parent and from the INORDER I will be used as the Left child of 'G':

![](img/1faaa0256577c74e8a61f42967760aa8_268_1.png)

## CONVERSION OF A TREE FROM INORDER AND POSTORDER

INORDER : D B H E A F C I G

POST ORDER : D H B E F I G C A

CHOOSE THE ROOT from the postorder (from the right) and from inorder find the nodes in left and right and this process will continue up to all the elements are chosen from the postorder/inorder.

STEP1 : From the right of POSTORDER 'A' will be chosen as the ROOT and from INORDER we observe that in the left of A (D,B,H,E) and in the right (F,C,I,G) will be there.

(D,B,H,E,A)       (F,C,I,G)

STEP2: From the POSTORDER 'C' will be chosen as the PARENT and from INORDER we observe that in the right of 'C' (I,G) and to the left (F) will be used.

![](img/1faaa0256577c74e8a61f42967760aa8_269_0.png)

STEP3: From the right of POSTORDER 'G' will be chosen as the PARENT and from inorder to the left of 'G' (I) will be used.

![](img/1faaa0256577c74e8a61f42967760aa8_269_1.png)

STEP4: From the right to postorder 'B' will be chosen as the PARENT and from the INORDER we observe that to the right of 'B' (H,E,A) and to the left (D) will be used.

![](img/1faaa0256577c74e8a61f42967760aa8_269_2.png)

STEP5: From the right to postorder we will choose 'E' as PARENT and from the Inorder to the left of 'E' (H) will be used.

![](img/1faaa0256577c74e8a61f42967760aa8_270_0.png)

## 8.7 Types of Binary Tree

There are different types of BINARY trees are found but some of them which are frequently used are

- Expression Tree
- Binary Search Tree
- Height Balanced Tree (AVL Tree)
- Threaded Binary Tree
- Heap Tree
- Huffman Tree
- Decision Tree
- Red Black Tree

## 8.8 Expression Tree

An expression tree is a Binary Tree which stores/represents the mathematical (arithmetic) expressions.

The leaves of an expression tree are operands, such as constants or variable names and all the internal nodes are the operators. An expression tree will be always a binary tree because an arithmetic expression contains either binary operators or unary operators.

Formally we can define an expression Tree as a special kind of binary tree in which:

- Each leaf is an operand. Examples: a, b, c, 6, 100
- The root and internal nodes are operators. Examples: +, -, *, /, ^
- Subtrees are subexpressions with the root being an operator.

### Construction of Expression Tree:

Now For constructing expression tree we use a stack. We loop through input expression and do following for every character.

- 1) If character is operand push that into stack.
- 2) If character is operator pop two values from stack make them its child and push current node again.

At the end only element of stack will be root of expression tree.

### EXAMPLE

### Represent an Expression Tree

A + (B*(C) - (D^E) / F + G * H

While constructing the TREE choose an operator in such a way that the terms in parenthesis will be in a side (for better construction) and choose a operator having higher precedence.

### STEP1:

![](img/1faaa0256577c74e8a61f42967760aa8_271_0.png)

### STEP2:

![](img/1faaa0256577c74e8a61f42967760aa8_271_1.png)

### Step3:

![](img/1faaa0256577c74e8a61f42967760aa8_272_0.png)

Depending on the expression used we have different types of expressions:

- Prefix expression
- Infix expression
- Postfix expression

### Example

Construct an expression tree for 5 7 - 3 /

Scan the symbols from left and since 5 and 7 are operands so push them into stack.

![](img/1faaa0256577c74e8a61f42967760aa8_272_1.png)

Next read '-'; since - is an operator so pop the stack and make these as child of the operator.

![](img/1faaa0256577c74e8a61f42967760aa8_272_2.png)

Next, '3' will read then push it into stack.

![](img/1faaa0256577c74e8a61f42967760aa8_273_0.png)

Last read the character '/' since it is an operator so pop the symbols from stack and add them into '/' as its child.

![](img/1faaa0256577c74e8a61f42967760aa8_273_1.png)

## 8.9 Binary Search Tree

A binary Search Tree is a Binary Tree that is either empty or in which each node possesses a key that satisfy the properties like

- The element in the left subtree are smaller than the key in the root
- The element in the right subtree are greater than or equal to the root
- The left and right subtrees are also the Binary Search Tree.

### OPERATIONS PERFORMED WITH A BST

The most commonly used operations with BST are

- Insertion
- Deletion
- Searching

![](img/1faaa0256577c74e8a61f42967760aa8_274_0.png)

### SEARCHING

To search any node in a Binary tree, initially the data item that is to be searched is compared with the data of the root node. If the data is equal to the data of the root node then the search is successful.

If the data is found to be greater than the data of the root node then the searching proceeds in the right sub-tree, otherwise searching process proceeds in the left sub-tree.

Repeat the same process till the element is found and while searching if Leaf node is found then print that the number is not found.

### INSERTION

To insert any node into a binary search tree, initially data item that is to be inserted is compared with the data of the root node.

If the data item is found to be greater than or equal to the data item of root node then the new node is inserted in the right sub tree of the root node, otherwise the new node is inserted in the left sub tree of the root node.

Now the root node of the right or left sub tree is taken and its data is compared with the data that is to be inserted and the same procedure is repeated. This is done till the left or right sub tree where the new node to be inserted is found to be empty. Finally the new node is made the appropriate child of this current node.

### DELETION

While deletion if the deleted node has only one sub tree, in this case simply link the parent of the deleted node to its sub tree.

When the deleted node has both left and right sub then the process is too complicated and there we have to follow the following four cases such as

- CASE1: No node in the tree contains the specified data item.
- CASE2: The node containing the data item has no children
- CASE3: The node containing the data item has exactly one child
- CASE4: The node containing the data item has two children.

### CASE1

In first case we have to check the condition whether tree is empty or not.

Condition is

```
IF (ROOT = NULL)
WRITE : "TREE IS EMPTY"
[END OF IF]
```

### CASE2

In this case where the node to be deleted is a leaf node i.e. its left and right node is not there then just delete it by assigning NULL to its parent node.

Condition is

```
IF ([left]item = NULL AND [RIGHT]ITEM = NULL)
```

Ex: If we want to delete 52 then add NULL to 49.

### CASE3

In this case where the node having either left sub tree or right sub tree.

Condition is

```
IF ([left]item != NULL AND [RIGHT]ITEM = NULL)
IF ([left]item = NULL AND [RIGHT]ITEM != NULL)
```

Ex: If we want to delete 49, which has only one child, so we can delete it simply by giving address of right child to its parent left pointer. Here 55 is the parent of 49 and 52 is the right child of 49. So after delete of 49, 52 will be added to left of 55.
