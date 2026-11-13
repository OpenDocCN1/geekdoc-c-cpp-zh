

```c
tree = deleteElement(tree, val);
break;
case 8:
    printf("\n Total no. of nodes = %d", totalNodes(tree));
    break;
case 9:
    printf("\n Total no. of external nodes = %d",
    totalExternalNodes(tree));
    break;
case 10:
    printf("\n Total no. of internal nodes = %d",
    totalInternalNodes(tree));
    break;
case 11:
    printf("\n The height of the tree = %d",Height(tree));
    break;
case 12:
    tree = mirrorImage(tree);
    break;
case 13:
    tree = deleteTree(tree);
    break;
}
}while(option!=14);
getch();
return 0;
}
void create_tree(struct node **tree)
{
    tree = NULL;
}
struct node *insertElement(struct node *tree, int val)
{
    struct node *ptr, *nodeptr, *parentptr;
    ptr = (struct node*)malloc(sizeof(struct node));
    ptr->data = val;
    ptr->left = NULL;
    ptr->right = NULL;
    if(tree==NULL)
    {
        tree=ptr;
        tree->left=NULL;
        tree->right=NULL;
    }
    else
    {
        parentptr=NULL;
        nodeptr=tree;
        while(nodeptr!=NULL)
        {
            parentptr=nodeptr;
            if(val<nodeptr->data)
                nodeptr = nodeptr->left;
            else
                nodeptr = nodeptr->right;
        }
        if(val<parentptr->data)
            parentptr->left = ptr;
        else
            parentptr->right = ptr;
    }
    return tree;
}
void preorderTraversal(struct node *tree)
{
    if(tree != NULL)
    {
        printf("%d\t", tree->data);
        preorderTraversal(tree->left);
        preorderTraversal(tree->right);
    }
}

void inorderTraversal(struct node *tree)
{
    if(tree != NULL)
    {
        inorderTraversal(tree->left);
        printf("%d\t", tree->data);
        inorderTraversal(tree->right);
    }
}

void postorderTraversal(struct node *tree)
{
    if(tree != NULL)
    {
        postorderTraversal(tree->left);
        postorderTraversal(tree->right);
        printf("%d\t", tree->data);
    }
}

struct node *findSmallestElement(struct node *tree)
{
    if((tree == NULL) || (tree->left == NULL))
        return tree;
    else
        return findSmallestElement(tree->left);
}

struct node *findLargestElement(struct node *tree)
{
    if((tree == NULL) || (tree->right == NULL))
        return tree;
    else
        return findLargestElement(tree->right);
}

struct node *deleteElement(struct node *tree, int val)
{
    struct node *cur, *parent, *suc, *psuc, *ptr;

    if(tree->left == NULL)
    {
        printf("\n The tree is empty ");
        return(tree);
    }

    parent = tree;
    cur = tree->left;
    while(cur != NULL && val != cur->data)
    {
        parent = cur;
        cur = (val < cur->data) ? cur->left : cur->right;
    }

    if(cur == NULL)
    {
        printf("\n The value to be deleted is not present in the tree");
        return(tree);
    }

    if(cur->left == NULL)
    {
        ptr = cur->right;
    }
    else if(cur->right == NULL)
    {
        ptr = cur->left;
    }
    else
    {
        // Find the in-order successor and its parent
        psuc = cur;
        cur = cur->left;
        while(suc->left!=NULL)
        {
            psuc = suc;
            suc = suc->left;
        }
        if(cur!=psuc)
        {
            // Situation 1
            // suc->left = cur->right;
        }
        else
        {
            // Situation 2
            suc->left = cur->left;
            psuc->left = suc->right;
            suc->right = cur->right;
        }
        ptr = suc;
        // Attach ptr to the parent node
        // if(parent->left == cur)
        parent->left=ptr;
        else
        parent->right=ptr;
        free(cur);
        return tree;
    }
}
int totalNodes(struct node *tree)
{
    if(tree==NULL)
    return 0;
    else
    return(totalNodes(tree->left) + totalNodes(tree->right) + 1);
}
int totalExternalNodes(struct node *tree)
{
    if(tree==NULL)
    return 0;
    else if((tree->left==NULL) && (tree->right==NULL))
    return 1;
    else
    return (totalExternalNodes(tree->left) +
    totalExternalNodes(tree->right));
}
int totalInternalNodes(struct node *tree)
{
    if ((tree==NULL) || ((tree->left==NULL) && (tree->right==NULL)))
    return 0;
    else
    return (totalInternalNodes(tree->left) +
    totalInternalNodes(tree->right) + 1);
}
int Height(struct node *tree)
{
    int leftheight, rightheight;
    if(tree==NULL)
    return 0;
    else
    {
        leftheight = Height(tree->left);
        rightheight = Height(tree->right);
        if(leftheight > rightheight)
        return (leftheight + 1);
        else
        return (rightheight + 1);
    }
}
struct node *mirrorImage(struct node *tree)
{
    struct node *ptr;
    if(tree!=NULL)
    {
        mirrorImage(tree->left);
        mirrorImage(tree->right);
        ptr=tree->left;
        ptr->left = ptr->right;
        tree->right = ptr;
    }
}
struct node *deleteTree(struct node *tree)
{
    if(tree!=NULL)
    {
        deleteTree(tree->left);
        deleteTree(tree->right);
        free(tree);
    }
}
```

## Output

```
********** MAIN MENU**********
1. Insert Element
2. Preorder Traversal
3. Inorder Traversal
4. Postorder Traversal
5. Find the smallest element
6. Find the largest element
7. Delete an element
8. Count the total number of nodes
9. Count the total number of external nodes
10. Count the total number of internal nodes
11. Determine the height of the tree
12. Find the mirror image of the tree
13. Delete the tree
14. Exit
Enter your option : 1
Enter the value of the new node : 1
Enter the value of the new node : 2
Enter the value of the new node : 4
Enter your option : 3
2 1 4
Enter your option : 14
```

## 10.3 线索二叉树

线索二叉树与二叉树相同，但在存储 NULL 指针方面有所不同。请考虑图 10.28 所示的二叉树链式表示。

![](img/be6359df08208122bec6fad1103de211_325_0.png)

图 10.28 二叉树的链式表示

在链式表示中，许多节点在其左字段或右字段或两者中包含 NULL 指针。存储 NULL 指针浪费的这部分空间可以高效地用于存储其他有用信息。例如，可以将 NULL 项替换为指向节点的中序前驱或中序后继的指针。这些特殊指针称为线索，包含线索的二叉树称为线索二叉树。在二叉树的链式表示中，线索将使用箭头表示。线索化二叉树有多种方式，每种类型可能会根据树的遍历方式而有所不同。在本书中，我们将讨论树的中序遍历。除此之外，线索二叉树可能对应单向线索化或双向线索化。

![](img/be6359df08208122bec6fad1103de211_325_1.png)

图 10.29 (a) 未线索化的二叉树

![](img/be6359df08208122bec6fad1103de211_325_2.png)

图 10.29 (b) 二叉树的链式表示（未线索化）

将指向节点的中序后继。这种单向线索化树称为右线索二叉树。在双向线索树（也称为双线索树）中，线索将出现在节点的左字段和右字段中。左字段将指向节点的中序前驱，而右字段将指向其后继。双向线索二叉树也称为完全线索二叉树。下面将解释二叉树的单向线索化和双向线索化。图 10.29 显示了一个未线索化的二叉树及其相应的链式表示。该树的中序遍历如下：8, 4, 9, 2, 5, 1, 10, 11, 3, 7, 12

### 单向线索化

![](img/be6359df08208122bec6fad1103de211_325_3.png)

图 10.30 (a) 带单向线索化的二叉树链式表示

在单向线索化中，线索将出现在节点的右字段或左字段中。单向线索化树也称为单线索树。如果线索出现在左字段，则左字段将被指向节点的中序前驱。这种单向线索化树称为左线索二叉树。相反，如果线索出现在右字段，则它

图 10.30 显示了一个带单向线索化的二叉树及其相应的链式表示。节点 5 在其 RIGHT 字段中包含一个 NULL 指针，因此将被替换为指向节点 1，即其中序后继。同样，节点 8 的 RIGHT 字段将指向节点 4，节点 9 的 RIGHT 字段将指向节点 2，节点 10 的 RIGHT 字段将指向节点

