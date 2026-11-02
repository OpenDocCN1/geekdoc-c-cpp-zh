

```cpp
/**
Gets all nodes of a subtree and fills them into a vector.
@param n the root of the subtree
@param nodes the vector into which to place the nodes
*/
void get_nodes(Node* n, vector<Node*> & nodes)
{
    if (n == nullptr) { return; }
    get_nodes(n->left, nodes);
    nodes.push_back(n);
    get_nodes(n->right, nodes);
}
```

```cpp
/**
Prints a detailed view of a binary tree.
@param n the root of the tree to print
@param level the indentation level for the root
*/
void print_detailed(Node* n, int level)
{
    if (n == nullptr) { return; }
    print_detailed(n->left, level + 1);
    for (int i = 0; i < level; i++) { cout << "  "; }
    cout << n->data << " " << n->color << endl;
    print_detailed(n->right, level + 1);
}
```

```cpp
/**
Populates a tree with the values A, B, C, ... .
@param t a red-black tree
@return the number of nodes in t
*/
int populate(RedBlackTree t)
{
    vector<Node*> nodes;
    get_nodes(t.root, nodes);
    for (int i = 0; i < nodes.size(); i++)
    {
        string d = "A";
        d[0] = d[0] + i;
        nodes[i]->data = d;
    }
    return nodes.size();
}
```

```cpp
/**
Checks that the tree with the given node is a red-black tree
and prints an error message if a structural error is found.
@param n the root of the subtree to check
@param is_root true if this is the root of the tree
@param report_errors whether error messages should be printed
@return the black depth of this subtree, or -1 if this is not a
valid red-black tree
*/
int check_red_black(Node* n, bool is_root, bool report_errors)
{
    if (n == nullptr) { return 0; }
    int nleft = check_red_black(n->left, false, report_errors);
    int nright = check_red_black(n->right, false, report_errors);
    if (nleft == -1 || nright == -1) return -1;
    if (nleft != nright)
    {
        if (report_errors)
        {
            cout << "Left and right children of " << n->data
                 << " have different black depths" << endl;
        }
        return -1;
    }
    if (n->parent == nullptr)
    {
        if (!is_root)
        {
            if (report_errors)
            {
                cout << n->data << " is not root and has no parent" << endl;
            }
            return -1;
        }
        if (n->color != BLACK)
        {
            if (report_errors)
            {
                cout << "Root " << n->data << " is not black";
            }
            return -1;
        }
    }
    else
    {
        if (is_root)
        {
            if (report_errors)
            {
                cout << n->data << " is root and has a parent" << endl;
            }
            return -1;
        }
        if (n->color == RED && n->parent->color == RED)
        {
            if (report_errors)
            {
                cout << "Parent of red " << n->data << " is red" << endl;
            }
            return -1;
        }
    }
    if (n->left != nullptr && n->left->parent != n)
    {
        if (report_errors)
        {
            cout << "Left child of " << n->data
                 << " has bad parent link" << endl;
        }
        return -1;
    }
    if (n->right != nullptr && n->right->parent != n)
    {
        if (report_errors)
        {

```

```cpp
{
    RedBlackTree rb;
    if (n == 0) { rb.root = copy(t.root); }
    else { rb.root = mirror(t.root); }
    vector<Node*> nodes;
    get_nodes(rb.root, nodes);
    Node* to_delete = nullptr;

    // Color with the bit pattern of k
    int bits = k;
    for (Node* n : nodes)
    {
        if (n == rb.root)
        {
            n->color = BLACK;
        }
        else if (n->color == BLACK)
        {
            to_delete = n;
        }
        else
        {
            n->color = bits % 2;
            bits = bits / 2;
        }
    }

    // Add children to make equal costs to nullptr
    int target_cost = cost_to_root(to_delete);
    for (Node* n : nodes)
    {
        int cost = target_cost - cost_to_root(n);
        if (n->left == nullptr)
        {
            n->set_left_child(full_tree(cost));
        }
        if (n->right == nullptr)
        {
            n->set_right_child(full_tree(cost));
        }
    }

    int filled_size = populate(rb);

    if (check_red_black(rb, false)) // Found a valid tree
    {
        string d = to_delete->data;
        rb.erase(d);
        bool pass = check_red_black(rb, true);
        for (int j = 0; j < filled_size; j++)
        {
            string s = "A";
            s[0] = s[0] + j;
            if (rb.count(s) == 0 && d != s)
            {
                cout << s << " deleted" << endl;
                pass = false;
            }
        }
        if (rb.count(d) > 0)
        {

```

## 第17章 优先队列与堆

![](img/d61019b035dd82beb581604273c0ee6b_900_0.png)

© tomazl/Stockphoto。

### 本章目标

- 熟悉优先队列数据类型
- 理解堆数据结构的实现与效率
- 使用堆实现优先队列和堆排序算法

### 本章内容

- 17.1 优先队列 554
- WE1 模拟等待中的顾客队列 557
- 17.2 堆 557
- 17.3 堆排序算法 567

### 表1 使用优先队列

| 代码 | 描述 |
| --- | --- |
| `priority_queue<int> q;` | 该优先队列存放整数对象。实际应用中，你会使用描述任务的对象。 |
| `q.push(3);`<br>`q.push(1);`<br>`q.push(2);` | 向优先队列中添加值。 |
| `int first = q.top();` | 返回优先队列中最大的元素。 |
| `q.pop();` | 移除最大的元素。 |
| `while (q.size() > 0)`<br>`{`<br>`  cout << q.top() << endl;`<br>`  q.pop();`<br>`}` | 按降序打印并移除所有元素。 |

下面是一个演示优先队列的简单程序。我们没有存储字符串，而是使用了 `Task` 类。如第13.1.2节所述，我们提供了一个用于比较任务的 `operator<` 函数，这样优先队列就能找到最重要的任务。

### sec01/task.h

```cpp
#ifndef TASK_H
#define TASK_H

#include <string>

using namespace std;

class Task
{
public:
    Task(string description, int priority);
    string get_description() const;
    int get_priority() const;
private:
    string description;
    int priority;
};
bool operator<(const Task& a, const Task& b);
#endif
```

### sec01/task.cpp

```cpp
#include "task.h"

Task::Task(string description, int priority)
{
    this->description = description;
    this->priority = priority;
}

string Task::get_description() const
{
    return description;
}

int Task::get_priority() const
{
    return priority;
}

bool operator<(const Task& a, const Task& b)
{
    return a.get_priority() < b.get_priority();
}
```

### sec01/pqueue.cpp

```cpp
#include <iostream>
#include <queue>
#include "task.h"

using namespace std;

int main()
{
    priority_queue<Task> tasks;
    tasks.push(Task("Shampoo carpets", 2));
    tasks.push(Task("Empty trash", 3));
    tasks.push(Task("Water plants", 2));
    tasks.push(Task("Remove pencil sharpener shavings", 1));
    tasks.push(Task("Replace light bulb", 4));
    tasks.push(Task("Fix overflowing sink", 9));
    tasks.push(Task("Clean coffee maker", 1));
    tasks.push(Task("Order cleaning supplies", 5));

    while (tasks.size() > 0)
    {
        Task most_important = tasks.top();
        tasks.pop();
        cout << most_important.get_priority() << " - "
             << most_important.get_description() << endl;
    }
    return 0;
}
```

### 程序运行

```text
9 - Fix overflowing sink
5 - Order cleaning supplies
4 - Replace light bulb
3 - Empty trash
2 - Water plants
2 - Shampoo carpets
1 - Remove pencil sharpener shavings
1 - Clean coffee maker
```

很容易看出，堆性质保证了树中最大的元素存储在根节点。

堆表面上看与二叉搜索树相似，但有两个重要区别：

1. 堆的形状非常规则。二叉搜索树的形状可以是任意的。
2. 在堆中，左子树和右子树存储的元素都小于根元素。相比之下，在二叉搜索树中，较小的元素存储在左子树，较大的元素存储在右子树。

![](img/d61019b035dd82beb581604273c0ee6b_905_0.png)

在近完全树中，除一层外所有层都被完全填满。© Lisa Marzano/iStockphoto。

假设我们有一个堆，想要插入一个新元素。插入之后，堆性质应该再次得到满足。下面的算法实现了插入操作（见图3）。

1. 首先，在树的末尾添加一个空位。
2. 接下来，如果空位的父节点小于要插入的元素，则将其降级。也就是说，将父节点的值移入空位，并将空位向上移动。只要空位的父节点仍然小于要插入的元素，就重复此降级操作。
3. 此时，空位要么位于根节点，要么空位的父节点大于要插入的元素。将元素插入空位。

![](img/d61019b035dd82beb581604273c0ee6b_905_1.png)

图3 向堆中插入元素

