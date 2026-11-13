

```cpp
x->color=1;
}
void delete(node* z)
{
    node* y, * x;
    y = z;
    if (z == NULL)
        cout << "No Node to Delete";
    else
    {
        if (z->lchild == NULL || z->rchild == NULL)
            y = z;
        else
            y = successor(z);
        if (y->lchild == NULL)
            x = y->lchild;
        else
            x = y->rchild;
        setparent(x, y->parent);
        if (y->parent == NULL)
            root = x;
        else if (y == y->parent->lchild)
            y->parent->lchild = x;
        else
            y->parent->rchild = x;
        if (y != z)
            z->data = y->data;
        delete y;
        RBDeleteFixup(x);
    }
}
```

```cpp
void RBInsertFixup(node* x)
{
    node* y;
    while (x->parent != NULL && x->parent->color == 0)
    {
        if (x->parent == x->parent->parent->lchild)
        {
            y = x->parent->parent->rchild;
            if (y != NULL)
            {
                if (y->color == 0)
                {
                    x->parent->color = 1;
                    y->color = 1;
                    x->parent->parent->color = 0;
                    x = x->parent->parent;
                }
                else
                {
                    if (x == x->parent->rchild)
                    {
                        x = x->parent;
                        llrotate(x);
                    }
                    else
                    {
                        x->parent->color = 1;
                        x->parent->parent->color = 0;
                        rrrotate(x->parent->parent);
                    }
                }
            }
        }
        else
        {
            y = x->parent->parent->lchild;
            if (y != NULL)
            {
                if (y->color == 0)
                {
                    x->parent->color = 1;
                    y->color = 1;
                    x->parent->parent->color = 0;
                    x = x->parent->parent;
                }
                else
                {
                    if (x == x->parent->lchild)
                    {
                        x = x->parent;
                        llrotate(x);
                    }
                    else
                    {
                        x->parent->color = 1;
                        x->parent->parent->color = 0;
                        rrrotate(x->parent->parent);
                    }
                }
            }
        }
    }
    root->color = 1;
}
```

```cpp
void insert(node* z)
{
    node* x, * y;
    y = NULL;
    x = root;
    while (x != NULL)
    {
        y = x;
        if (z->data < x->data)
            x = x->lchild;
        else
            x = x->rchild;
    }
    z->parent = y;
    if (y == NULL)
        root = z;
    else
    {
        z->parent = y;
        if (z->data < y->data)
            y->lchild = z;
        else
            y->rchild = z;
    }
    RBInsertFixup(z);
}
```

```cpp
int height(node* ptr)
{
    if (ptr != NULL)
        return ((height(ptr->rchild) > height(ptr->lchild) ? height(ptr->rchild) + 1 : height(ptr->lchild) + 1));
    else
        return -1;
}
```

```cpp
void inorder(node* ptr)
{
    node* z;
    if (ptr->lchild != NULL)
        inorder(ptr->lchild);
    cout << endl << ptr->data << " ";
    cout << "Height: " << height(ptr) << " ";
    cout << "Successor: " << z->data << " ";
    z = successor(ptr);
    cout << "Successor: " << z->data << " ";
    z = predecessor(ptr);
    cout << "Predecessor: " << z->data << " ";
    if (ptr->color == 0)
        cout << "Red";
    else
        cout << "Black";
    if (ptr->parent != NULL)
        cout << "Parent: " << ptr->parent->data;
    if (ptr->rchild != NULL)
        inorder(ptr->rchild);
}
```

```cpp
int search(int key, node* ptr)
{
    if (ptr != NULL)
    {
        if (ptr->data == key)
            k = 1;
        else
        {
            search(key, ptr->lchild);
            search(key, ptr->rchild);
        }
    }
    return k;
}
```

```cpp
void main()
{
    node* z;
    int op, item;
    clrscr();
    root = NULL;
    while (1)
    {
        cout << "\nRed Black Tree Operations";
        cout << "\n1.Insertion\n2.Deletion\n3.Searching\n4.Traversing\n5.Exit";
        cout << "\nEnter your option.";
        cin >> op;
        switch (op)
        {
        case 1:
            z = (node*)malloc(sizeof(node));
            cout << "\nEnter Item To Be Insert";
            cin >> item;
            z->data = item;
            z->color = 0;
            z->rchild = NULL;
            z->lchild = NULL;
            z->parent = NULL;
            insert(z);
            break;
        case 2:
            if (root == NULL)
                cout << "Tree Is Empty";
            else
            {
                cout << "Enter Item To Be Delete";
                cin >> item;
                delete(binarysearch(item, root));
            }
            break;
        case 3:
            s = 0;
            cout << "Enter Element To Search: ";
            cin >> item;
            s = search(item, root);
            if (s == 1)
                cout << "Search Is Found";
            else
                cout << "Search Is Not Found";
            break;
        case 4:
            cout << "Inorder Traversal:\n";
            inorder(root);
            break;
        case 5:
            exit(0);
        }
    }
}
```

## 输出

红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目11
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目2
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目14
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目1
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目7
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目15
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目5
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:1
请输入要插入的项目8
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:4
请输入您的选项:4
中序遍历:
1 高度:0 后继:2 前驱:1 颜色:黑色 父节点:2
2 高度:2 后继:5 前驱:1 颜色:红色 父节点:11
5 高度:0 后继:7 前驱:5 颜色:红色 父节点:7
7 高度:1 后继:8 前驱:2 颜色:黑色 父节点:2
8 高度:0 后继:11 前驱:7 颜色:红色 父节点:7
11 高度:3 后继:14 前驱:8 颜色:黑色
14 高度:1 后继:15 前驱:11 颜色:黑色 父节点:11
15 高度:0 后继:11 前驱:14 颜色:红色 父节点:14
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:2
请输入要删除的项目:7
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出

遍历:
1 高度:0 后继:2 前驱:1 颜色:黑色 父节点:2
2 高度:2 后继:5 前驱:1 颜色:红色 父节点:11
5 高度:0 后继:8 前驱:5 颜色:红色 父节点:8
8 高度:1 后继:11 前驱:2 颜色:黑色 父节点:2
11 高度:3 后继:14 前驱:8 颜色:黑色
14 高度:1 后继:15 前驱:11 颜色:黑色 父节点:11
15 高度:0 后继:11 前驱:14 颜色:红色 父节点:14
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:3
请输入要查找的元素:8
查找成功
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出

请输入您的选项:3
请输入要查找的元素:10
查找失败
红黑树操作
1.插入
2.删除
3.查找
4. 遍历
5. 退出
请输入您的选项:2
请输入要删除的项目2
红黑树操作
1. 插入
2. 删除
3. 查找
4. 遍历
5. 退出
请输入您的选项:4
中序遍历:

| | 高度:0 | 后继:5 | 前驱:1 | 颜色:黑色 | 父节点:5 |
|---|---|---|---|---|---|
| 5 | 高度:1 | 后继:8 | 前驱:1 | 颜色:红色 | 父节点:11 |
| 8 | 高度:0 | 后继:11 | 前驱:5 | 颜色:黑色 | 父节点:5 |
| 11 | 高度:2 | 后继:14 | 前驱:8 | 颜色:黑色 | |
| 14 | 高度:1 | 后继:15 | 前驱:11 | 颜色:黑色 | 父节点:11 |
| 15 | 高度:0 | 后继:11 | 前驱:14 | 颜色:红色 | 父节点:14 |

红黑树操作
1. 插入
2. 删除
3. 查找
4. 遍历
5. 退出
请输入您的选项:2
请输入要删除的项目11
红黑树操作
1. 插入
2. 删除
3. 查找
4. 遍历
5. 退出
请输入您的选项:4
中序遍历:

| | 高度:0 | 后继:5 | 前驱:1 | 颜色:黑色 | 父节点:5 |
|---|---|---|---|---|---|
| 5 | 高度:1 | 后继:8 | 前驱:1 | 颜色:红色 | 父节点:14 |
| 8 | 高度:0 | 后继:11 | 前驱:5 | 颜色:黑色 | 父节点:5 |
| 14 | 高度:2 | 后继:14 | 前驱:8 | 颜色:黑色 | |

红黑树操作
1. 插入
2. 删除
3. 查找
4. 遍历
5. 退出
请输入您的选项:1
请输入要插入的项目13
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:4
中序遍历:
1   高度:0   后继:5   前驱:1   颜色:黑色   父节点:5
5   高度:2   后继:8   前驱:1   颜色:红色     父节点:14
8   高度:1   后继:13  前驱:5   颜色:黑色   父节点:5
13  高度:0   后继:14  前驱:8   颜色:红色     父节点:8
14  高度:3   后继:14  前驱:13  颜色:黑色   父节点:8
红黑树操作
1.插入
2.删除
3.查找
4.遍历
5.退出
请输入您的选项:5

操作的时间复杂度：红黑树上的查找操作与二叉搜索树上的查找操作完全相同，时间复杂度为 O(log n)。插入和/或删除操作可能会触发颜色变更，该变更可能向上传播直到根节点，并且还可能触发旋转以重新平衡树。旋转和颜色变更仅需要常数时间 O(1)。在最坏情况下，插入或删除操作的时间复杂度为 O(log n)。红黑树的最大高度为 2log2(n+1)。因此，需要 O(h) 的查找、插入和删除操作的时间复杂度为 O(log n)。

## 14.4 伸展树

二叉搜索树、AVL 树或红黑树的最坏情况时间复杂度均为 O(n)。二叉搜索树用于存储一组记录或元素。如果其中某个元素被检索 m 次，则此操作序列的最坏情况时间复杂度为 O(m·n)。在许多日常应用（如字典）中，一旦某个元素被访问，频繁访问同一元素的可能性大于访问未访问过的元素。

如果被访问的元素位于叶节点，则其时间复杂度为 O(n)。由于同一元素在不久的将来可能会被多次访问，如果它位于根节点以供进一步访问，则其时间复杂度将为 O(1)。虽然以这种方式调整树代价高昂，但它使进一步的访问更快、更便宜。在此调整过程中，树中深处的其他元素可能会上移，从而使其访问变得相对更便宜。

Daniel Dominic Sleator 和 Robert Endre Tarjan 发明了一种称为伸展树的数据结构，它提供了上述讨论的机制。伸展树是二叉搜索树，具有某种奇妙的特性，可以针对一系列树操作进行最优适应。当对某个节点执行任何操作（如查找、插入和删除）时，该节点会向根节点移动。在此过程中，不活跃的元素会被移离根节点。

