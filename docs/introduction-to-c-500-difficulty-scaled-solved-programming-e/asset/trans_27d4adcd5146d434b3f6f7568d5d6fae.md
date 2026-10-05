

```cpp
while (p != nullptr)
{
    if (p->code == code_a)
        tmp1 = p;
    else if (p->code == code_b)
        tmp2 = p;

    if (tmp1 && tmp2)
    {
        grd = tmp1->grd;
        tmp1->grd = tmp2->grd;
        tmp2->grd = grd;
        return 0;
    }
    p = p->next;
    return -1;
}
```

## C.14.12 接下来程序的输出是什么？

```cpp
#include <iostream>

struct Node
{
    int i;
    Node *next;
    Node *prev;
};

int main()
{
    Node a = {10}, b = {20}, c = {30}, d = {40};

    a.next = &b;
    a.prev = &d;

    b.next = &c;
    b.prev = &a;

    c.next = &d;
    c.prev = &b;

    d.next = &a;
    d.prev = &c;
    std::cout << a.next->prev->prev->next->i << '\n';
    return 0;
}
```

**注释：** 该程序是另一种列表类型——双向循环链的简单实现示例，其中每个节点除了指向下一个节点的指针外，还包含指向上一个节点的指针。注意，最后一个节点的 `next` 指针指向头节点，而头的 `prev` 指针指向最后一个节点。程序从节点 a 开始，顺序遍历 d、c 和 b 节点，返回回到 c 并输出 30。现在尝试练习 U.14.14。

## 二叉搜索树

为了按排序顺序组织数据，通常会使用一种名为“树”的灵活数据结构。这种结构出现在现实生活中的几个例子中，例如家族树、组织结构图或计算机的文件夹系统。树有许多类型；在这里，我们将描述二叉搜索树中的基本操作。

让我们介绍一些基本概念。带根的树是由边连接的节点组成的集合。只有一个节点没有父节点，即根节点。除了根节点外，每个节点只连接一个上层节点，即父节点。直接连接在下方的节点是它的子节点。每个节点最多有两个子节点的树被称为二叉树。这两个部分被称为左子树和右子树。如果每个节点都有一个键，且该键：

- 大于或等于其所有子树中所有节点的键
- 小于或等于其右子树中所有节点的键

则被称为二叉搜索树。使用它的主要优点是在插入和查找某个值等关键操作中具有高性能。相关的排序和搜索算法可以非常高效。下面的图展示了二叉搜索树的一个示例。

![](img/25e0e40b08b8016a58f1aab13ac2e812_455_0.png)

让我们看看二叉搜索树中最基本操作的一些实现示例。假设每个节点由以下结构表示：

```cpp
struct Node
{
    int key;
    Node *left;
    Node *right;
};
```

我们将存储不同的键。指针指向节点的子节点。如果缺失节点，指针为 `nullptr`。

```cpp
#include <iostream> // 示例 14.9
#include <string>
using std::cout;
using std::cin;
using std::string;
```

```cpp
struct Node
{
    int key;
    Node *left;
    Node *right;
};
```

## 442 C++ 简介

```cpp
Node* add_node(Node *p, int key);
void show_inorder(Node *p);
void delete_tree(Node *p);
```

```cpp
int main() {
    int sel, key;
    Node *root;

    root = nullptr;
    while (1) {
        cout << "\n菜单选择\n";
        cout << "--------------------\n";
        cout << "1. 添加节点\n";
        cout << "2. 显示树\n";
        cout << "3. 退出\n";

        cout << "\nEnter选择: ";
        cin >> sel;

        switch (sel) {
            case 1:
                cout << "键: ";
                cin >> key;
                root = add_node(root, key);
                break;
            case 2:
                cout << "已添加的键: ";
                show_inorder(root);
                break;
            case 3:
                cout << "\n已删除的键: ";
                delete_tree(root);
                return 0;
            default:
                cout << "\n错误选择\n";
                break;
        }
    }
    return 0;
}
```

```cpp
Node* add_node(Node *p, int key) {
    if (p == nullptr) {
        p = new Node;
        p->left = p->right = nullptr;
        p->key = key;
    }
```

```cpp
    else {
        if (key < p->key)
            p->left = add_node(p->left, key);
        else if (key > p->key)
            p->right = add_node(p->right, key);
        else
            cout << "错误: " << key << " 已存在\n";
    }
    return p;
}

void show_inorder(Node *p) {
    if (p == nullptr)
        return;
    show_inorder(p->left);
    cout << p->key << ' ';
    show_inorder(p->right);
}

void delete_tree(Node *p) {
    if (p == nullptr)
        return;
}
