
```c
break;
}
} while(choice != 4);

return 0;
}

void deQueueInsert(int *queue, int item, int pos)
{
    if((rear >= MAXQUEUESIZE) && (front == 0))
    {
        printf("\n\n\t Queue Overflow ");
        return;
    }
    if(!pos)
    {
        if(front > 0)
        {
            front = front - 1;
            queue[front] = item;
        }
        else
        {
            printf("\n\n\t Queue Overflow ");
            return;
        }
    }
    else
    {
        if(rear < MAXQUEUESIZE)
        {
            rear = rear + 1;
            queue[rear] = item;
        }
        else
        {
            printf("\n\n\t Queue Overflow ");
            return;
        }
    }
}

void deQueueDelete(int *queue, int pos)
{
    int item;

    if((front == 0) && (rear == 0))
    {
        printf("\n\n\t Queue Underflow ");
        return;
    }

    if(!pos)
    {
        if(front > 0)
        {
```

Next, let’s learn about trees, in detail.

## Tree

A tree is a connected acyclic graph, which can be used in various real-life applications. A tree data structure is used to emulate any hierarchical relationship in the real life. For example, the hierarchical structure in an organization can be represented by a tree data structure. The file system in Windows or Linux can also be represented by using a tree data structure, where a folder contains several files and folders, which in turn contain another level of files and folders. A tree data structure came into reality after realizing that with large amount of input data, the linear access time of arrays and linked lists is a bottleneck. Although the primary reason for applying a tree data structure is to organize the data into the hierarchical order, the basic need for trees arises in the searching applications. As data volumes are getting bulkier by each passing day, it is nearly impossible to respond to a search query within few milliseconds, if we are searching the database in linear order. However, by using the searching order can be reduced from O(N) to O(log N).

One of the best ways to define a tree is to define it recursively. A tree is a finite set that is either empty or is partitioned into two disjoint sub-sets: a root and a non-empty set of sub-trees, where each sub-tree is a tree in itself connected to the root by an edge. Figure 24.11 shows a typical tree:

![](img/43c5f409f9b17790a628c4b4df854b61_862_0.png)

**Figure 24.11: Showing a Tree**

The file organization structures in UNIX and Windows are implemented by using generic trees. Moreover, the organizational hierarchies are implemented using generic trees. However, to get the maximum benefit from a tree data structure, we must take the advantage of its natural ordering mechanism, which helps in searching the records easily and conveniently in a lesser amount of time. Following code snippet shows how to map a generic tree to a structure definition in C:

```c
struct genericTreeNode {
    char                         nodeName[20];
    struct genericTreeNode      *ptrToFirstChild;
    struct genericTreeNode      *ptrToNextSibling;
};
```

As shown in the preceding code snippet, we can easily implement a generic tree with a root and a non-empty set of sub-trees, which are trees in themselves. The three members (per node) in the genericTreeNode structure are as follows:

- **nodeName**—Contains the name of a node or any pertinent information related to a node, based on which the tree is generated

### Binary Tree Traversal

One of the popular uses of binary tree is the file organization structure in various common operating systems, such as UNIX and DOS. Directory structures are huge and heavily nested for common operating systems, but how do we handle a query that comes from a user to list all the files under a particular user? This is where tree traversal algorithms come into play. Tree traversal techniques for binary trees are recursive in nature and each of the nodes has similar structure by definition. Following three types of traversal techniques exist for binary trees that traverse the entire tree, but each has its own method:

- **Preorder Traversal**—Traverses the tree by first visiting the root, then the left sub-tree, and finally the right sub-tree. The following code snippet presents the preorder traversal method with a pointer to the root of struct binaryTreeNode:

```c
void preorder (struct binaryTreeNode *root)
{
    if (root != NULL) {
        printf("%s\n", root->info);
        preorder (root->ptrToLeftSubtree);
        preorder (root->ptrToRightSubtree);
    }
}
```

- **Inorder Traversal**—Traverses the tree by first visiting the left sub-tree, then the root, and finally the right sub-tree. The following code snippet presents the inorder traversal method with a pointer to the root of struct binaryTreeNode:

```c
void inorder (struct binaryTreeNode *root)
{
    if (root != NULL) {
        inorder (root->ptrToLeftSubtree);
        printf("%s\n", root->info);
        inorder (root->ptrToRightSubtree);
    }
}
```

- **Postorder Traversal**—Traverses the tree by first visiting the left sub-tree, then the right sub-tree, and finally the root. The following code snippet presents the postorder traversal method with a pointer to the root of struct binaryTreeNode:

```c
void postorder (struct binaryTreeNode *root)
{
    if (root != NULL) {
        postorder (root->ptrToLeftSubtree);
        postorder (root->ptrToRightSubtree);
        printf("%s\n", root->info);
    }
}
```

An important use of binary trees is in the case of searching; therefore, let’s learn about binary search tree.

### Binary Search Tree

Suppose that each key in a tree is assigned an integer value. The property that converts a binary tree into a binary search tree is that for every node in the tree, the values of all the keys in its left sub-tree are smaller than the value of nodeptr and the values of all the keys in its right sub-tree are larger than the value of nodeptr. Due to the recursive definition of trees, it is common to write these routines in the recursive manner. As the average depth of a binary search tree is O(log n) for n number of depths, we do not need to worry about running out of stack space.

Following is the structure of the binary search tree in C:

```c
struct BSTreeNode {
    int info;
    struct BSTreeNode *left;
    struct BSTreeNode *right;
};
```

The basic operations performed on a binary search tree are listed in the form of functions, as follows:

- 1. **emptyTree** (struct BSTreeNode *tree)—Checks whether a binary search tree is empty or not; if not empty, then we need to make it empty before reusing it. The primary purpose for this operation is to re-initialize a tree that has already been used before. The code snippet for the operation is given as follows:

```c
struct BSTreeNode *emptyTree (struct BSTreeNode *tree)
{
    if (tree != NULL) {
        emptyTree (tree->left);
        emptyTree (tree->right);
        free (tree);
    }
    return NULL;
}
```

The preceding function takes a pointer to the root of the binary search tree and checks whether it is NULL or not. If it is NULL, then the function returns as it is, since the root points to a NULL tree. In case the root pointer is not NULL, the function recursively calls itself for both left and right sub-trees and frees up the tree to make it empty.

- 2. **findVal** (int element, struct BSTreeNode *tree)—Finds an element in a binary search tree. The code snippet for the operation is given as follows:

```c
struct BSTreeNode *findVal (int element, struct BSTreeNode *tree)
{
    if (tree == NULL)
        return NULL;
    if (element < tree->info)
        return findVal (element, tree->left);
    else if (element > tree->info)
        return findVal (element, tree->right);
    else
        return tree;
}
```

The preceding function takes an integer element as an input along with the root pointer to the tree, which in this case is *tree. Now, the function checks whether the tree is empty. If the tree is empty, then it returns NULL, as the element is not present in the tree. If the root element has any element, then the pointer to the root element is returned. For the cases where the item might be in the left or right sub-tree of the root node, we recursively call the function on the left and right sub-trees of the root node, whichever is applicable.

- 3. **findMin** (struct BSTreeNode *tree)—Takes a pointer to the tree as input and finds the minimum element as output, that is, the element with the minimum value. To perform this operation, we need to start at the root of the tree and go left as long as there is a left child. The code snippet for the operation is given as follows:

```c
struct BSTreeNode *findMin (struct BSTreeNode *tree)
{
    if (tree == NULL)
        return NULL;
    else if (tree->left == NULL)
        return tree;
```
