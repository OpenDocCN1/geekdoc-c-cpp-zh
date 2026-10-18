

换句话说，当变量被删除或重新赋值时，计数器会递减。如果计数器达到零，则可以安全地删除该对象并将分配的内存返回到自由存储区。这一切都是自动执行的，这使程序员无需编写自己的内存管理代码！

作为示例，请考虑以下实现 Node 类的简单链表的代码。该类仅存储一个整数。代码使用“旧”格式通过指针链接类，并且在 listTest 函数中没有显式释放分配的内存。这意味着当执行返回到 main 函数时，程序存在内存泄漏。如果程序没有立即退出，这可能会导致内存问题。

## DISPLAY 18.29  存在内存泄漏的节点链表 *(第 1 部分，共 2 部分)*

```
// Linked list of a simple Node class using traditional pointers.
// Note that this version has a memory leak when execution returns to
// main.
#include <iostream>
using std::cout;
using std::endl;

// A simple Node class. A full-featured class would have
// several more functions.
class Node
{
private:
    int num;
    Node *next;
public:
    Node();
    Node();
    Node(int num, Node *nextPtr);
    int getNum();
    Node* getNext();
    void setNext(Node *, *nextPtr);
};

Node::Node() : num(0), next(nullptr)
{
}

Node::Node(int numVal, Node *nextPtr) : num(numVal), next(nextPtr)
{
}

Node::~Node()
{
    cout << "Deleting " << num << endl;
}
```

## DISPLAY 18.29  存在内存泄漏的节点链表 *(第 2 部分，共 2 部分)*

```
int Node::getNum()
{
    return num;
}
Node* Node::getNext()
{
    return next;
}
void Node::setNext(Node *nextPtr)
{
    next = nextPtr;
}

void listTest()
{
    // Create a linked list with 10->20->30
    Node *root = new Node(10, nullptr);
    root->setNext(new Node(20, nullptr));
    root->getNext()->setNext(new Node(30, nullptr));

    // Output the list
    Node *temp;
    temp = root;
    while (temp != nullptr)
    {
        cout << temp->getNum() << endl;
        temp = temp->getNext();
    }
}

int main()
{
    listTest();
}
```

# Sample Dialogue

```
10
20
30
```

请注意，尽管 Node 类存在析构函数，但析构函数从未被调用。这是因为我们从未删除每个节点。listTest 中分配的内存从未被释放，因此 main 中存在内存泄漏。这并不是真正的问题，因为程序立即退出（此时内存会被回收），但如果在调用 listTest 之后还有进一步的处理，我们可能会遇到内存问题。

接下来，考虑使用 shared_ptr 类编写的相同程序。我们必须包含 <memory> 库。Node 类的每个指针出现都被替换为 shared_ptr<Node>。

请注意，链表会在 listTest 函数中变量超出作用域时由 shared_ptr 类自动为我们释放。这是在

## DISPLAY 18.30  使用智能指针的节点链表 *(第 1 部分，共 2 部分)*

```
1  // Linked list of a simple Node class using smart pointers.
2  // There is no memory leak since the shared_ptr class
3  // handles reference counting and memory deallocation.
4  #include <iostream>
5  #include <memory>
6  using std::cout;
7  using std::endl;
8  using std::shared_ptr;
9  
10 // Class modified to use shared_ptr of Nodes.
11 class Node
12 {
13 private:
14     int num;
15     shared_ptr<Node> next;
16 public:
17     Node();
18     ~Node();
19     Node(int num, shared_ptr<Node> nextPtr);
20     int getNum();
21     shared_ptr<Node> getNext();
22     void setNext(shared_ptr<Node> nextPtr);
23 };
24 Node::Node() : num(0), next(nullptr)
25 { }
26 
27 Node::~Node()
28 {
29     cout << "Deleting " << num << endl;
30 }
31 
32 Node::Node(int numVal, shared_ptr<Node> nextPtr) : num(numVal), next(nextPtr)
33 { }
34 
35 int Node::getNum()
36 {
37     return num;
38 }
```

## DISPLAY 18.30  使用智能指针的节点链表 *(第 2 部分，共 2 部分)*

```
39
40 shared_ptr<Node> Node::getNext()
41 {
42     return next;
43 }
44
45 void Node::setNext(shared_ptr<Node> nextPtr)
46 {
47     next = nextPtr;
48 }
49
50 void listTest()
51 {
52     shared_ptr<Node> root(new Node(10, nullptr));
53     shared_ptr<Node> next1(new Node(20, nullptr));
54     shared_ptr<Node> next2;
55     // After a shared_ptr is declared we can set it
56     // using the reset function
57     next2.reset(new Node(30, nullptr));
58     // Link the nodes together
59     root->setNext(next1);
60     next1->setNext(next2);
61
62     // Output the list
63     shared_ptr<Node> temp;
64     temp = root;
65     while (temp != nullptr)
66     {
67         cout << temp->getNum() << endl;
68         temp = temp->getNext();
69     }
70 }
71
72 int main()
73 {
74     listTest();
75     cout << "Exiting program." << endl;
76 }
```

# Sample Dialogue

```
10
20
30
Deleting 10
Deleting 20
Deleting 30
Exiting program.
```

在调用 listTest 退出后完成，如 Node 析构函数输出的消息所示，程序退出前已输出。

作为进一步的示例，考虑如果存在引用链表中第二项的全局变量会发生什么。在这种情况下，shared_ptr 类在 listTest 函数退出时不会删除列表中的其余项。这是因为只有在没有引用它们时节点才会被删除。请注意，全局变量的使用不被认为是良好的编程实践，但在这里仅用于说明引用计数的概念。

附加全局变量：

```
shared_ptr<Node> global_reference;
```

listTest 中修改后的代码：

```
void listTest()
{
    shared_ptr<Node> root(new Node(10, nullptr));
    shared_ptr<Node> next1(new Node(20, nullptr));
    shared_ptr<Node> next2;
    // After a shared_ptr is declared we can set it
    // using the reset function
    next2.reset(new Node(30, nullptr));
    // Link the nodes together
    root->setNext(next1);
    next1->setNext(next2);

    // Output the list
    shared_ptr<Node> temp;
    temp = root;
    while (temp != nullptr)
    {
        cout << temp->getNum() << endl;
        temp = temp->getNext();
    }
    // The line below creates a reference to the second item
    // in the linked list
    global_reference = root->getNext();
}
```

# Sample Dialogue

```
10
20
30
Deleting 10
Exiting program.
Deleting 20
Deleting 30
```

- set、map、multiset 和 multimap 容器模板类以排序顺序存储其元素，以便搜索算法高效。set 是元素的简单集合。map 允许通过键值存储和检索。multiset 类允许条目重复。multimap 类允许单个键与多个数据项相关联。
- STL 包含模板函数来实现具有最大运行时间保证的通用算法。
- C++11 中添加的功能包括 std::array 类、正则表达式、线程和智能指针。

## Answers to Self-Test Exercises

- 1. v.begin() 返回位于 v 的第一个元素的迭代器。v.end() 返回一个值，该值充当 v 所有元素末尾的哨兵值。
- 2. *p 是应用于 p 的解引用运算符。*p 是位置 p 处元素的引用。
- 3. vector<int>::iterator p;
   for (p = v.begin(), p++; p != v.end(); p++)
       cout << *p << " ";
- 4. D C C
- 5. B C
- 6. Either would work.
- 7. 一个主要区别是 vector 容器具有随机访问迭代器，而 list 只有双向迭代器。
- 8. All except slist.
- 9. vector and deque.
- 10. 它们都可以具有可变迭代器。
- 11. stack 模板适配器类没有迭代器。
- 12. queue 模板适配器类没有迭代器。
- 13. 没有返回值；pop 是一个 void 函数。
- 14. mymap 将包含两个条目。一个是从 5 映射到 "c++"，另一个是从 4 映射到默认字符串，即空白。
- 15. 是的，它们可以是任何类型，尽管每个 set 对象只有一个类型。模板类中的类型参数是存储元素的类型。

