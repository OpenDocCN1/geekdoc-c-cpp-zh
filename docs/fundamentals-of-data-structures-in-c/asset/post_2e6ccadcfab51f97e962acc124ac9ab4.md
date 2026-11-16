
Enter the Data : 6
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 9
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 12
Do u wish to Add Data in the Tree (y/n) ? n
TREE TRAVERSAL
1. Preorder Traversal
2. Inorder Traversal
3. Postorder Traversal
4. Levelorder Traversal
? 3
Postorder Binary tree traversal is ...
3 6 5 9 12 10 7

RUN
Enter data to Create a New Binary Tree ...
Enter the Data : 7
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 5
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 10
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 3
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 6
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 9
Do u wish to Add Data in the Tree (y/n) ? y
Enter the Data : 12
Do u wish to Add Data in the Tree (y/n) ? n
TREE TRAVERSAL
1. Preorder Traversal
2. Inorder Traversal
3. Postorder Traversal
4. Levelorder Traversal
? 4
Level Binary tree traversal is ...
7 5 10 3 6 9 12

## 4.5 Binary Search Trees

A binary search tree is a special binary tree, that satisfy the following characteristics.

- Every node has a value and no two nodes should have the same value (i.e., the values in the binary search tree are distinct).
- The values in any left subtree is less than the value of its parent node.
- The values in any right subtree is greater than the value of its parent node.
- The left and right subtrees of each node are again binary search trees.

Fig. 4.15 shows the structure of a binary search tree.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_250_0.png)

Fig. 4.15 : A binary search tree.

### 4.5.1 Basic Operations in a Binary Search Tree

The basic operations that can be performed on a binary search tree are,

- Creation of a binary search tree.
- Insertion of a node
- Deletion of a node
- Searching a node
- Modification of a node
- View the contents of the binary search tree.

#### Creation of a Binary Search Tree

Every node of a binary search tree have two parts, data part and the link part.

Creation of binary search tree involves three processes. They are,

- Creating a node.
- Read details for the node from the user.
- Insert the node in the binary search tree.

In Program 4.2, getNode() function is used to create a node. After allocating memory for the structure of type node, the information for the node has to be read from the user. In Program 4.2, readNode() function is used for reading details for the node from the user. In Program 4.2, insertNode() function is used for inserting a new node in the binary search tree. The functions getNode(), readNode() and insertNode() are called repeatedly, to insert any number of nodes in the binary search trees.

#### Insertion of a node

One of the most primitive operations that can be done in a binary search tree is the insertion of a node. Memory is to be allocated for the new node (in a similar way that is done while creating a tree) before reading the data. The new node will contain empty data field and empty link field. The data field of the new node is then stored with the information read from the user. The link field of the new node is assigned to NULL.

- Check whether the root node of the binary search tree is NULL.
- If the condition is true, it means, that the binary search tree is empty, hence consider the new node as the root node. Otherwise, follow the next steps.
- Compare the new node data with root node data, for the following three conditions.
- If content of the new node data is equal to the root node data, insertion operation is terminated (because of duplication).
- If the content of the new node data is lesser than the root node data, check whether the left child of the root node is NULL. If the condition is true, insert the new data and terminate the process. Otherwise, consider the left child of the root node as the root node and check for the three conditions again.
- If the content of the new node data is greater than the root node data, check whether the right child of the root node is NULL. If the condition is true, insert the new data and terminate the process. Otherwise, consider the right child of the root node as the root node and check for the three conditions again.

In Program 4.2, insertNode() function is used for inserting a new node in the binary search tree. Fig. 4.16 explains insertion operation in a binary search in detail.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_251_0.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_251_1.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_251_2.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_251_3.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_252_0.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_252_1.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_252_2.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_252_3.png)

Fig. 4.16 : Steps for insertion operation in a binary search tree.

#### Deletion of a Node

Another primitive operation that can be done in a binary search tree is the deletion of a node. Memory is to be released for the node to be deleted. A node can be deleted from the tree from three different places namely,

- Deleting the leaf node
- Deleting the node with only one child
- Deleting the node with two children.

##### Deleting the leaf node

Steps followed to delete a leaf node from the binary search tree.

- Search the parent of the leaf node, and make the link to the leaf node as NULL.
- Release the memory for the deleted node.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_253_0.png)

Fig. 4.17a : Before deleting the leaf node 6. Fig. 4.17b : After deleting the leaf node 6. Fig. 4.17 : Steps for deleting the leaf node.

##### Deleting the node with only one child

Steps followed to delete the node (with only one child) from the binary search tree.

- Search the parent of the node to be deleted (with only one child).
- Assign the link of the parent node to the child of the node to be deleted.
- Release the memory for deleted node.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_253_1.png)

Fig. 4.18a : Before deleting the node 5, Fig. 4.18b : After deleting the node 5. Fig. 4.18 : Steps for deleting a node that has only one children.

##### Deleting the node with two children

Steps followed to delete the node (with two children) from the binary search tree.

- Search the parent of the node to be deleted (with two children).
- Copy the content of the inorder successor to the node to be deleted (with two children).
- Delete the inorder successor node. If the inorder successor node has no child, follow the steps given in the deleting the leaf node. If the inorder successor node has only one child, follow the steps given in the deleting node with one child.
- Release the memory for the inorder successor node.
- Replace the contents of the node to be deleted with the copy of the content of the inorder successor node.

In Program 4.2, deleteNode() function is used for deleting the node from binary search tree.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_254_0.png)

#### Searching a node

One of the most important operations that can be done in a binary search tree is searching a node.

- Check whether the root node of the binary search tree is NULL. If yes, binary search tree is empty and hence terminate the search operation.
- If the binary search tree is not empty, compare the new node data with root node data, for the following three conditions.
- If the content of the new node data is equal to the root node data, search element is found and hence terminate the process.
- If the content of the new node data is lesser than the root node data, check whether the left child of the root node is NULL. If the condition is true, search element is not found and terminate the process. Otherwise, consider the left child of the root node as the root node and check for the three conditions again.
- If the content of the new node data is greater than the root node data, check whether the right child of the root node is NULL. If the condition is true, search element is not found, and terminate the process. Otherwise, consider the right child of the root node as the root node and check for the three conditions again.

In Program 4.2 searchNode() function is used for searching a node in the binary search tree.

#### Modification of a Node

Steps followed to modify a node in a binary search tree.

- First search the node in the binary search tree using the steps given in the searching of a node and then modify the content of the node.

In Program 4.2, modifyNode() function is used for modifying a node in the binary search tree.
