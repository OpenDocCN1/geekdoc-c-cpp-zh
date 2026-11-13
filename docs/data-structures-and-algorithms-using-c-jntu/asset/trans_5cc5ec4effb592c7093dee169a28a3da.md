

```cpp
{
    cout<<"Item Already Exists";
    return;
}
}
if (ptr==NULL)
{
    n=(struct BST*)malloc(sizeof(struct BST));
    n->data=item;n->lchild=n->rchild=NULL;
    if (ptr1->data<item)
    ptr1->rchild=n;
    else
    ptr1->lchild=n;
}
```

```cpp
void case1()
{
    if (ptr1->lchild==ptr)
    ptr1->lchild=NULL;
    else
    ptr1->rchild=NULL;
    cout<<"Element Is Successfully Deleted";
    ptr=NULL;
}
```

```cpp
void case2()
{
    struct BST*ptr2,*y;
    int x=0;
    ptr2=ptr->rchild;
    if (ptr2->lchild==NULL&&ptr2->rchild==NULL)
    {
    ptr1->lchild=ptr2;
    ptr1->lchild->lchild=ptr2->lchild;
    }
    else if (ptr2->lchild==NULL&&ptr2->rchild!=NULL)
    {
    ptr1->rchild=ptr2;
    ptr1->rchild->lchild=ptr2->lchild;
    ptr2=NULL;
    free(ptr);
    }
    else
    {
    while (ptr2->lchild!=NULL)
    ptr2=ptr2->lchild;
    if (ptr2->rchild!=NULL)
    {x=1;y=ptr2->rchild;}
    }
    ptr1->lchild=ptr2;
    ptr2->lchild=ptr->lchild;
    ptr2->rchild=ptr->rchild;
    if (x==1)
        ptr2->rchild->lchild=y;
    else
    {
        ptr2->rchild->lchild=NULL;
        ptr=NULL;
        free(ptr);
    }
}
```

```cpp
void case3()
{
    if (ptr1->lchild==ptr)
    {
        if (ptr->lchild==NULL)
        {
            ptr1->lchild=ptr->rchild;
        }
        else
        {
            ptr1->lchild=ptr->lchild;
        }
    }
    else
    {
        if (ptr1->rchild==ptr)
        {
            if (ptr->lchild==NULL)
            ptr1->rchild=ptr->rchild;
            else
            ptr1->rchild=ptr->lchild;
        }
    }
    cout<<"Element Is Successfully Deleted";
    ptr=NULL;
}
```

```cpp
void delet(int item)
{
    int c=0;
    struct BST*pt;
    ptr=root;
    if (ptr==NULL)
    {
        cout<<"Tree Is Empty";
        return;
    }
    if (ptr->data==item)
    {
        cout<<"item Is A Root Node Deletion Is Not Possible";
        return;
    }
    if (ptr->data==item&&ptr->lchild==NULL&&ptr->rchild==NULL)
    {
        root=NULL;
        cout<<"Item"<<item<<"Is Successfully Deleted";
        return;
    }
    while (ptr!=NULL && c==0)
    {
        if (item<ptr->data)
        {
            ptr1=ptr;
            ptr=ptr->lchild;
        }
        else if (item>ptr->data)
        {
            ptr1=ptr;
            ptr=ptr->rchild;
        }
        else
        c=1;
    }
    if (c==0)
    {
        cout<<"Item Does Not Exist.. Deletion Is Not Possible";
        return;
    }
    if (ptr->lchild==NULL&&ptr->rchild==NULL)
        case1();
    else if (ptr->lchild==NULL&&ptr->rchild!=NULL)
        case2();
    else
        case3();
}
```

```cpp
void traverse(struct BST*ptr)
{
    if (ptr!=NULL)
    {
        traverse (ptr->lchild);
        cout<<ptr->data<<" ";
        traverse (ptr->rchild);
    }
}
int searching(struct BST*p,int key)
{
    if (p!=NULL)
    {
        if (p->data==key)
        k=1;
    }
    else
    {
        searching(p->lchild,key);
        searching(p->rchild,key);
    }
    return k;
}
main()
{
    int ch;
    clrscr();
    while(1)
    {
        cout<<"\nBINARY SEARCH TREE OPERATIONS\n1.INSERTION\n2.DELETION\n";
        cout<<"3.TRAVERSE\n4.SEARCHING\n5.EXIT\n";
        cout<<"\nEnter Your Choice";
        cin>>ch;
        switch(ch)
        {
            case 1:insert();break;
            case 2:cout<<"Which Item You Want To Delete";cin>>item;
            delet(item);break;
            case 3:if(root==NULL){cout<<"Tree Is Empty";break;}
            cout<<"Tree Elements Are"; traverse(root);break;
            case 4:if(root==NULL){cout<<"Tree Is Empty";break;}
            s=k=0;cout<<"Which Item You Want To Search";
            cin>>item;
            s=searching(root,item);
            if(s==1)
            cout<<"Item"<<item<<"Is Found";
            else
            cout<<"Item"<<item<<"Is Not Found";
            break;
            case 5:exit(0);
            default:cout<<"Invalid Choice";
        }
    }
}
```

```
BINARY SEARCH TREE OPERATIONS
1. INSERTION
2. DELETION
3. TRAVERSE
4. SEARCHING
5. EXIT
Enter Your Choice1
Enter Element To Be Insert 35
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 20
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 40
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 10
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 24
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 22
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 21
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 23
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 25
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice1
Enter Element To Be Insert 30
Enter Your Choice3
Tree Elements Are 10 20 21 22 23 24 25 30 35 40
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSAL
4.SEARCHING
5.EXIT
Enter Your Choice2
Which Item You Want To Delete 24
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSAL
4.SEARCHING
5.EXIT
Enter Your Choice3
```

```
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSAL
4.SEARCHING
5.EXIT
Enter Your Choice3
```

```
Tree Elements Are 10 20 21 22 23 25 30 35 40
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice2
Which Item You Want To Delete 20
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice3
Tree Elements Are 10 21 22 23 25 30 35 40
BINARY SEARCH TREE OPERATIONS
1.INSERTION
2.DELETION
3.TRAVERSE
4.SEARCHING
5.EXIT
Enter Your Choice5
```

## 12.4 AVL 树

1962 年，Adelson-Velskii 和 Landis 提出了称为 AVL 树的平衡或高度平衡树。AVL 树是平衡树的一种，在最坏情况下树的高度为 O(log n)。AVL 树是二叉搜索树的高度平衡版本。

定义：空二叉树是 AVL 树。非空二叉树 T 是 AVL 树，当且仅当 (i) T 的左子树 T_L 和右子树 T_R 也是 AVL 树 (ii) |h(T_L) - h(T_R)| <= 1，其中 h(T_L) 和 h(T_R) 分别是 T 的左子树和右子树的高度。

节点 u 的平衡因子，表示为 bf(u)，可定义为 bf(u) = h(u_L) - h(u_R)，其中 h(u_L) 是 u 的左子树的高度，h(u_R) 是 u 的右子树的高度。

AVL 树中的每个节点 u 允许的平衡因子 bf(u) 为 -1、0 或 +1。

同时也是 AVL 树的二叉搜索树称为 AVL 搜索树。图 12.8 清楚地展示了上述讨论的术语。相应节点的平衡因子显示在节点旁边的括号内。观察平衡因子如何为 -1、0 或 1。

AVL 树和 AVL 搜索树的表示与使用链式表示的二叉树和 BST 非常相似。为了高效地进行插入和删除操作，可以在节点结构中添加一个名为平衡因子 bf 的附加字段，用于保存特定节点的平衡因子。

- (a) AVL 树
- (b) 非 AVL 树
- (c) AVL 搜索树
- (d) 非 AVL 搜索树
- 图 12.8 AVL 树和非 AVL 树的实例

## 12.5 AVL 搜索树的操作

对 AVL 搜索树执行的常见操作如下。

### 12.5.1 搜索

在 AVL 搜索树中搜索元素与在 BST 上的搜索操作非常相似。算法 12.1 及其在程序 12.1 中的实现也可用于从 AVL 搜索树中搜索元素。包含 n 个元素的 AVL 搜索树的高度为 O(log n)，因此在其上执行搜索操作的时间复杂度也为 O(log n)。

### 12.5.2 插入

向 AVL 搜索树插入元素遵循与向二叉搜索树插入元素相同的过程。但是，插入可能导致一种情况，即任何节点的平衡因子可能不是 -1、0 或 +1，树变得不平衡。

为了重新平衡树，即使所有平衡因子为 -1、0 或 1，需要对不平衡树的某些子树进行移位，这也称为旋转。这可以在图 12.9 中显示。

关于由于插入导致的不平衡树，可以作出以下观察：

- 1. 不平衡树的平衡因子只能是 -2、-1、0、1 和 +2 之一。
- 2. 插入后，对于平衡因子为 +2 或 -2 的节点，其插入前的相应平衡因子分别为 +1 或 -1。

