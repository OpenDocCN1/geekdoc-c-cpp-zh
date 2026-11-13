
- (h) 插入 DC。

![](img/a99ec79093c067f0bed8f1086197950e_520_0.png)

- (i) 插入 DS。DS 被放置在 MBS 左侧的右侧，导致 MBS 不平衡。因此使用 LR 旋转进行重新平衡。

![](img/a99ec79093c067f0bed8f1086197950e_520_1.png)

![](img/a99ec79093c067f0bed8f1086197950e_520_2.png)

- (j) 插入 OOP。

![](img/a99ec79093c067f0bed8f1086197950e_521_0.png)

- (k) 插入 OOMD。OOMD 被放置在 OOCS 右侧的左侧，导致 OOCS 不平衡。因此使用 RL 旋转进行重新平衡。

![](img/a99ec79093c067f0bed8f1086197950e_521_1.png)

## 10.3.1 AVL 技术的实现

示例 10.4 演示了平衡 BST 的工作过程。让我们为其编写一个算法。一般来说，树中的一个节点存储数据以及指向左孩子和右孩子的指针。在 AVL 树中，每个节点存储这三个字段。为了简化工作，我们可以在每个节点中存储其子树的高度。因此，我们将定义每个 AVL 树节点具有四个字段。

考虑具有以下结构的 AVL 树节点：

```
class AVLNode
{
    KeyType key;
```

```
AVLNode *Left, *Right;
 int height;
 };
```

假设 getNode( ) 是一个函数，它为新的 AVLNode 分配内存，初始化所有字段，并返回指向它的指针。

设 height( n ) 为一个函数，返回根为 n 的子树的高度，如果为 null 则返回 –1。设 balancefactor( n ) 为一个函数，返回其树中节点 n 的平衡因子。请注意，在示例 10.3 中我们考虑了以下情况：当节点 n 的平衡因子为 +2 时，由于左子树高度增加导致树不平衡，且只有两种可能性，即 LL 或 LR。当节点 n 的平衡因子为 –2 时，由于右子树高度增加导致树不平衡，且只有两种可能性，即 RR 或 RL。

让我们编写一个 insert( ) 函数，它将给定键插入 AVL 树的适当位置，并在需要时使用四种旋转之一（LL、RR、LR、RL）重新平衡树。这在程序代码 10.2 中有所说明。

### 程序代码 10.2

```
AVLNode *AVLNode :: insert(int NewKey, AVLNode *root)
{
    AVLNode *NewNode;
    int lh, rh;
    root->height = height(root);
    if(root == null)
    {
        NewNode = new AVLNode;
        NewNode->key = NewKey;
        NewNode->left = null;
        NewNode->right = null;
        root = NewNode;
    }
    else
    {
        if(NewKey < root->key)
        {
            root->left = insert(NewKey,root->left);
            if(balancefactor(root) == 2)
            {
            // Tree is unbalanced due to increase
```

```
// in height of left subtree
if(NewKey < root->left->key)
{
    cout << "\n LL rotation \n";
    root = LL(root);
}
else
{
    cout << "\n LR rotation \n";
    root = LR(root);
}
}
else if(NewKey > root->key)
{
    root->right = insert(NewKey, root->right);
    if(balancefactor(root) == -2)
    {
        // Tree is unbalanced due to increase
        // in height of right subtree
        if(NewKey > root->right->key)
        {
            cout << "\n RR rotation \n";
            root = RR(root);
        }
        else
        {
            cout << "\n RL rotation \n";
            root = RL(root);
        }
    }
}
else
    cout << "Duplicate key";
// After insertion, modify field height of the root
root->height = height(root);
return root;
}
```

我们现在了解四条旋转规则。让我们为情况 1：LL 编写代码。考虑图 10.21 中的场景，其中程序代码 10.3 模拟其操作。

![](img/a99ec79093c067f0bed8f1086197950e_524_0.png)

图 10.21 情况 LL 的场景

### 程序代码 10.3

```
// rotation: Left
AVLNode *AVLNode :: Left (AVLNode *A)
//function is called with unbalanced node as a parameter
{
    AVLNode *B;
    B = A->right;
    A->right = B->left;
    B->left = A;
    A->height = height (A);
    B->height = height (B);
    return B; // Set new root to B
}

// Rotation : Right
AVLNode *AVLNode ::Right (AVLNode *A)
{
    AVLNode *B;
    B = A->left;
    A->left = B->right;
    B->right = A;
    A->height = height (A);
    B->height = height (B);
```

```
return B; // Set new root to B
}
// Case 1 of rotation : LL
AVLNode *AVLNode :: LL(AVLNode *root)
{
root = Right(root);
return root;
}
// Case 2 of rotation : RR
AVLNode *AVLNode :: RR(AVLNode *root)
{
root = Left(root);
return root;
}
```

同样，可以为情况 2 编写函数 RR( )。程序代码 10.3 显示了 RR 的模拟。现在，考虑情况 3：LR（图 10.22a）和情况 4：RL（图 10.22b）。

![](img/a99ec79093c067f0bed8f1086197950e_525_0.png)

图 10.22 情况 (a) LR (b) RL 的场景

我们使用函数 LL() 和 RR() 来编写 LR() 和 RL() 函数，如程序代码 10.4 所示。

```
// Case 3 of rotation:LR
AVLNode *AVLNode :: LR(AVLNode *root)
{
    root->left = Left(root->left);
    root = Right(root);
    return root;
}

// Case 4 of rotation : RL
AVLNode *AVLNode :: RL(AVLNode *root)
{
    root->right = Right(root->right);
    root = Left(root);
    return root;
}
```

同样，可以为情况 4 编写函数 RL()。程序代码 10.4 描绘了其模拟。

## 10.3.2 AVL 树中的插入和删除

AVL 树中的插入和删除操作与 BST 相同，随后进行旋转以纠正结果树中的不平衡。在插入的情况下，一次旋转就足够了。在删除的情况下，从第一个不一致点向上到根节点，最多需要 O(logn) 次旋转。

图 10.23 演示了在给定 AVL 树中删除一个节点。原始树如图 10.23(a) 所示。图 10.23(b) 显示了删除节点 4 后的树。请注意，在图 10.23(c) 中，节点 3 的不平衡意味着围绕节点 2 进行 LL 旋转，图 10.23(d) 中节点 5 的不平衡意味着围绕节点 8 进行 RR 旋转。

程序代码 10.5 说明了从 AVL 树中删除元素的函数。

示例 10.5–10.7 说明了为不同数据集构建 AVL 树。

![](img/a99ec79093c067f0bed8f1086197950e_527_0.png)

### 图 10.23 AVL 树中删除一个节点 (a) 原始树 (b) 删除 4 后 (c) 围绕节点 2 的 LL 旋转 (d) 围绕节点 8 的 RR 旋转

### 程序代码 10.5

```
//Function to delete an element from AVL tree
AVLNode *AVLNode :: del(AVLNode *root,int dval)
{
    AVLNode *temp;
    if (root != null)
    {
        if (dval < root->key)
        {
            root->left = del(root->left,dval);
            if(balancefactor(root) == -2)
            {
                if(balancefactor(root->right) <= 0)
```

```
{
    cout << "\n RR rotation \n";
    root = RR(root);
    }
    else
    {
        cout << "\n RL rotation \n";
        root = RL(root);
        }
    }
}
else if(dval > root->key)
{
    root->right = del(root->right, dval);
    if(balancefactor(root) == 2)
    {
    if(balancefactor(root->left) >= 0)
    {
        cout << "\n LL rotation \n";
        root = LL(root);
    }
    else
    {
        cout << "\n LR rotation \n";
        root = LR(root);
        }
    }
}
else
{
    if(root->right == null)      // No right tree
    return(root->left);
    else
    {
    // find leftmost of right
    // temp = root->right;
    while(temp->left != null)
    {
    temp = temp->left;
    root->key = temp->key;
    temp->right = del(root->right, temp->key);
    if(balancefactor(root) == 2)
    {
    if(balancefactor(root->left) >= 0)
```

```
root = LL(root);
else
root = LR(root);
}
}
else
return null;
// Update height of root node
root->height = height(root);
return(root);
}
```

## 示例 10.5 为以下数据构建一个 AVL 树：
30, 31, 32, 23, 22, 28, 24, 29, 26, 27, 34, 36

解答 让我们求解并在每次插入时显示平衡因子和执行的旋转类型（如果有）。表 10.7 通过这里所述的步骤演示了相同内容。

### 表 10.7 示例 10.5 的 AVL 树构建

| 已插入数据 | 插入后的 AVL 树 (BF) | 执行的旋转 | 重新平衡后的 AVL 树 |
|---|---|---|---|
| 30 | 30 (BF 0) | | 无需重新平衡 |
| 31 | 30 -> 31 (BF -1, 0) | | 无需重新平衡 |
| 32 | 30 -> 31 -> 32 (BF -2, -1, 0) | RR | 31 (根) -> 30, 32 |
| 23 | 31 -> 30 -> 23 (BF 1, 1, 0) | | 无需重新平衡 |
