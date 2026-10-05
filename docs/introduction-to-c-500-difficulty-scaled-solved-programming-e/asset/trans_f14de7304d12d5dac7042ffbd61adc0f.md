
为了简单起见，我选择使用全局指针来处理栈。该指针始终指向栈的头部。

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::cin;
using std::string;
```

```cpp
struct Node
{
    string name;
    int code;
    float grd;
    Node *next; /* 指向下一个节点的指针。注意，结构的
存在允许我们声明它的类型。 */
};
```

```cpp
Node *head; // 始终指向栈头部的全局指针。

void add_stack(const Node *p);
void show_stack();
void pop();
int size_stack();
void free_stack();
```

```cpp
int main()
{
    int sel;
    Node n;

    head = nullptr; /* 头指针的初始值，声明栈为空。 */
    while (1)
    {
        cout << "\n菜单选择\n";
        cout << "------------------------------------\n";

        cout << "1. 添加学生\n";
        cout << "2. 查看所有学生\n";
        cout << "3. 查看顶部学生\n";
        cout << "4. 删除顶部学生\n";
        cout << "5. 学生人数\n";
        cout << "6. 退出\n";

        cout << "\n输入选择: ";
        cin >> sel;

        switch (sel)
        {
            case 1:
                cin.get();
```

```cpp
        cout << "姓名: ";
        getline(cin, n.name);

        cout << "代码: ";
        cin >> n.code;
        cout << "成绩: ";
        cin >> n.grd;

        add_stack(&n);
        break;
        case 2:
            if (head != nullptr)
                show_stack();
            else
                cout << "\n栈为空\n";
            break;
        case 3:
            if (head != nullptr)
                cout << "\nC: " << head->code << " N: " << head->name << " G:" << head->grd << "\n";
            else
                cout << "\n栈为空\n";
            break;
        case 4:
            if (head != nullptr)
                pop();
            else
                cout << "\n栈为空\n";
            break;
        case 5:
            if (head != nullptr)
                cout << size_stack() << " 学生存在于栈中\n";
            else
                cout << "\n栈为空\n";
            break;
        case 6:
            if (head != nullptr)
                free_stack();
            return 0;
        default:
            cout << "\n选择错误\n";
            break;
    }
    return 0;
}
```

```cpp
void add_stack(const Node *p)
{
    Node *new_node;
    new_node = new Node; // 分配内存创建一个新节点。
    *new_node = *p; // 将学生数据拷贝到新节点中。
    new_node->next = head; // 新节点插入到栈的开头。例如，当插入第一个节点时，
new_node->next 的值将等于 head 的初始值，即 nullptr。
    head = new_node; // head 指向新节点，因此该新
节点成为栈的新头部。
}
```

```cpp
void show_stack()
{
    Node *p;

    p = head;
    cout << "\n**** 学生数据 *****\n";
    while(p != nullptr)
    {
        cout << "C:" << p->code << " N:" << p->name << " G:" << p->grd
        << "\n";
        p = p->next; /* 在每次迭代中，p指向下一个节点。
当它变为 nullptr 时，意味着没有其他节点了，循环终止。 */
    }
}
```

```cpp
void pop()
{
    Node *p;

    p = head->next; /* p指向头部之后的节点。该节点
将成为栈的新头部。 */
    cout << "\n代码为 " << p->code << "的学生已删除\n";
    delete head; /* 释放内存。下一个节点的
信息不会丢失，因为它已保存在 p 中。 */
    head = p; // head 指向栈的新头部。
}
```

```cpp
int size_stack()
{
    Node *p;
    int num;

    num = 0;
    p = head;
    while(p != nullptr)
    {
        p = p->next;
        num++; // 该变量计算节点。
    }
    return num;
}
```

```cpp
void free_stack()
{
    Node *p, *next_node;

    p = head;
    while (p != nullptr) {
        next_node = p->next; /* next node指向被删除节点
之后的节点。 */
        delete p; /* 释放内存。下一个节点的
信息不会丢失，因为它已保存在 p 中。 */
        p = next_node; // p 指向下一个节点。
    }
}
```

注释：
a. 在 add_stack() 中，我们传递节点的指针。
b. 显示队列时，我们使用指向头的指针。
c. 如果变量是局部声明的，它成为尾。

实现队列（先进先出）
在本节中，我们将使用链表创建一个队列。第一个元素插入到队列的末尾，而第一个元素从队列前端移除。

练习：
1. 添加学生。
2. 显示所有学生。
3. 显示最后一个学生。
4. 删除第一个学生。
5. 学生人数。

