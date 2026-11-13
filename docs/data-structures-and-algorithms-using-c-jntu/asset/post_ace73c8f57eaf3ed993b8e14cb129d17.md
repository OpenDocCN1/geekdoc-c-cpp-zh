
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

## Output

Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert11
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert2
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert14
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert1
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert7
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert15
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert5
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:1
Enter Item To Be Insert8
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:4
Enter your option:4
Inorder Traversal:
1 Height:0 Successor:2 Predecessor:1 Color:Black Parent:2
2 Height:2 Successor:5 Predecessor:1 Color:Red Parent:11
5 Height:0 Successor:7 Predecessor:5 Color:Red Parent:7
7 Height:1 Successor:8 Predecessor:2 Color:Black Parent:2
8 Height:0 Successor:11 Predecessor:7 Color:Red Parent:7
11 Height:3 Successor:14 Predecessor:8 Color:Black
14 Height:1 Successor:15 Predecessor:11 Color:Black Parent:11
15 Height:0 Successor:11 Predecessor:14 Color:Red Parent:14
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:2
Enter Item To Be Delete:7
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit

Traversal:
1 Height:0 Successor:2 Predecessor:1 Color:Black Parent:2
2 Height:2 Successor:5 Predecessor:1 Color:Red Parent:11
5 Height:0 Successor:8 Predecessor:5 Color:Red Parent:8
8 Height:1 Successor:11 Predecessor:2 Color:Black Parent:2
11 Height:3 Successor:14 Predecessor:8 Color:Black
14 Height:1 Successor:15 Predecessor:11 Color:Black Parent:11
15 Height:0 Successor:11 Predecessor:14 Color:Red Parent:14
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:3
Enter Element To Search:8
Search Is Found
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit

Enter your option:3
Enter Element To Search:10
Search Is Not Found
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4. Traversing
5. Exit
Enter your option:2
Enter Item To Be Delete2
Red Black Tree Operations
1. Insertion
2. Deletion
3. Searching
4. Traversing
5. Exit
Enter your option:4
Inorder Traversal:

| | Height:0 | Successor:5 | Predecessor:1 | Color:Black | Parent:5 |
|---|---|---|---|---|---|
| 5 | Height:1 | Successor:8 | Predecessor:1 | Color:Red | Parent:11 |
| 8 | Height:0 | Successor:11 | Predecessor:5 | Color:Black | Parent:5 |
| 11 | Height:2 | Successor:14 | Predecessor:8 | Color:Black | |
| 14 | Height:1 | Successor:15 | Predecessor:11 | Color:Black | Parent:11 |
| 15 | Height:0 | Successor:11 | Predecessor:14 | Color:Red | Parent:14 |

Red Black Tree Operations
1. Insertion
2. Deletion
3. Searching
4. Traversing
5. Exit
Enter your option:2
Enter Item To Be Delete11
Red Black Tree Operations
1. Insertion
2. Deletion
3. Searching
4. Traversing
5. Exit
Enter your option:4
Inorder Traversal:

| | Height:0 | Successor:5 | Predecessor:1 | Color:Black | Parent:5 |
|---|---|---|---|---|---|
| 5 | Height:1 | Successor:8 | Predecessor:1 | Color:Red | Parent:14 |
| 8 | Height:0 | Successor:11 | Predecessor:5 | Color:Black | Parent:5 |
| 14 | Height:2 | Successor:14 | Predecessor:8 | Color:Black | |

Red Black Tree Operations
1. Insertion
2. Deletion
3. Searching
4. Traversing
5. Exit
Enter your option:1
Enter Item To Be Insert13
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:4
Inorder Traversal:
1   Height:0   Successor:5   Predecessor:1   Color:Black   Parent:5
5   Height:2   Successor:8   Predecessor:1   Color:Red     Parent:14
8   Height:1   Successor:13  Predecessor:5   Color:Black   Parent:5
13  Height:0   Successor:14  Predecessor:8   Color:Red     Parent:8
14  Height:3   Successor:14  Predecessor:13  Color:Black   Parent:8
Red Black Tree Operations
1.Insertion
2.Deletion
3.Searching
4.Traversing
5.Exit
Enter your option:5

Time complexity of operations: The search operation on a red-black tree is exactly the same as is on a binary search tree with the time complexity of O(log n). Insertion and/or deletion operations may invoke colour change which may spread in the upward direction till the root node and may also invoke the rotations to rebalance the tree. The rotations and colour change require only a constant time O(1). In the worst case the insertion or deletion operation will have the time complexity of O(log n). The maximum height of the red-black tree is 2log2(n+1). So, the operations search, insert and delete that require O(h) will have a time complexity of O(log n).

## 14.4 Splay Trees

The worst case time complexity of either binary search trees or AVL trees or red-black tree is O(n). A binary search tree is used to store a set of records or elements. If one of them is retrieved for m number of times then the worst case time complexity of this operation sequence will be O(m.n). In many day-to-day applications such as dictionary, once an element is accessed, the likelihood to access the same element frequently is more than to an unaccessed element.

If the accessed element is in a leaf node then its time complexity is O(n). As the same element may be accessed for many times in the near future, if it is available in the root node for further accesses its time complexity will be O(1). Though adjusting the tree in this manner is expensive, it makes further accesses faster and cheaper. In this process of adjustment other elements which are deep down in the tree may come up and allows their accesses to be relatively cheaper.

Daniel Dominic Sleator and Robert Endre Tarjan invented a data structure called a splay tree, which provides the above-discussed mechanism. Splay trees are binary search trees and they are with a wonderful property that can be adapted optimally to a sequence of tree operations. When any operation (such as search, insert and delete) performed on a node, it is moved towards the root node. In due course, the inactive elements are moved far away from the root node.
