

## 显示 17.25 树模板类的实现文件（第 2 部分，共 2 部分）

```
44        inorderShow(subTreeRoot->rightLink);
45    }
46 }

47    template<class T> //uses iostream:
48    void SearchTree<T>::inorderShow( ) const
49    {
50        inorderShow(root);
51    }

52    template<class T>
53    void SearchTree<T>::deleteSubtree(TreeNode<T>*& subTreeRoot)
54    {
55        if (subTreeRoot != NULL)
56        {
57            deleteSubtree(subTreeRoot->leftLink);
58
59            deleteSubtree(subTreeRoot->rightLink);
60
61            //subTreeRoot now points to a one node tree.
62            delete subTreeRoot;
63            subTreeRoot = NULL;
64        }
65    }

64    template<class T>
65    SearchTree<T>::~SearchTree( )
66    {
67        deleteSubtree(root);
68    }
69 }//TreeSavitch
```

使用树的后序遍历。

## 自测练习

20. 定义以下成员函数，可将其添加到显示 17.24 中的类 SearchTree。这些函数分别显示树的前序和后序遍历中遇到的數據。分别为每个函数定义一个私有帮助函数，就像我们为 SearchTree<T>::inorderShow 所做的那样。

void SearchTree<T>::preorderShow( ) const
void SearchTree<T>::postorderShow( ) const

## 显示 17.26 树模板类的演示程序

```
//Demonstration program for the Tree template class.
#include <iostream>
#include "tree.h"
#include "tree.cpp"
using std::cout;
using std::cin;
using std::endl;
using TreeSavitch::SearchTree;

int main()
{
    SearchTree<int> t;

    cout << "Enter a list of nonnegative integers.\n"
         << "Place a negative integer at the end.\n";
    int next;
    cin >> next;
    while (next >= 0)
    {
        t.insert(next);
        cin >> next;
    }

    cout << "In sorted order: \n";
    t.inorderShow();
    cout << endl;

    return 0;
}
```

### 示例对话

Enter a list of nonnegative integers.
Place a negative integer at the end.
40 30 20 10 11 22 33 44 -1
In sorted order:
10 11 20 22 30 33 40 44

## 章节总结

+   - 一个节点是一个结构体或类对象，它有一个或多个成员变量为指针变量。这些节点可以通过其成员指针变量连接起来，产生可以在程序运行期间增长和缩小的数据结构。
+   - 链表是一个节点列表，其中每个节点包含指向列表中下一个节点的指针。
+   - 链表（或其他链接数据结构）的末尾通过将指针成员变量设为 NULL 来指示。
+   - 栈是一个后进先出的数据结构。队列是一个先进先出的数据结构。两者都可以使用链表实现。
+   - 迭代器是一个构造（通常是某个迭代器类的对象），它允许你遍历存储在数据结构中的数据项。
+   - 树是一种数据结构，其节点有两个（或更多）成员变量指向其他节点。如果一棵树满足二叉搜索树存储规则，则可以设计一个函数来快速在树中找到数据。

## 自测练习答案

1. Sally
Sally
18
18

请注意 (*head).name 和 head->name 含义相同。同样，(*head).number 和 head->number 含义相同。

2. 最佳答案是

```
head->next = NULL;
```

但是以下也是正确的：

```
(*head).next = NULL;
```

3. head->item = "Wilbur's brother Orville";

```
4. class NodeType
{
public:
NodeType() {}
NodeType(char theData, NodeType* theLink)
: data(theData), link(theLink){}
NodeType* getLink() const { return link; }
char getData() const { return data; }
void setData(char theData) { data = theData; }
```

```
void setLink(NodeType* pointer) { link = pointer; }
private:
    char data;
    NodeType *link;
};

typedef NodeType* PointerType;
```

+   5. 值 NULL 用于指示空列表。

+   6. p1 == p1->next;

+   7. Pointer discard;
+      discard = p2->next; // discard 指向要删除的节点。
+      p2->next = discard->next;
+   
+      这足以从链表中删除该节点。但是，如果你没有将此节点用于其他用途，你应该使用 delete 调用销毁该节点，如下所示：
+   
+      delete discard;

+   8. p1 = p1->getLink( );

+   9. Pointer discard;
+      discard = p2->getLink( ); // 指向要删除的节点。
+      p2->setLink(discard->getLink( ));
+   
+      这足以从链表中删除该节点。但是，如果你没有将此节点用于其他用途，你应该使用 delete 调用销毁该节点，如下所示：
+   
+      delete discard;

+   10. a. 在大型链表的已知位置插入新项比在大型数组中插入更有效。如果你插入到列表中，大约有五次操作，其中大部分是指针赋值，与列表大小无关。如果你插入到数组中，平均需要移动大约一半的数组条目来插入一个数据项。
+   
+       对于小型列表，答案是 c，差不多。

+   11. 请注意，此函数本质上与显示 17.11 中的 headInsert 相同。

```
template<class T>
void Stack<T>::push(T stackFrame)
{
    top = new Node<T>(stackFrame, top);
}
```

+   12. //Uses cstddef:
+       template<class T>
+       Stack<T>::Stack(const Stack<T>& aStack)
+       {
+           if (aStack.isEmpty( ))

```
top = NULL;
else
{
    Node<Ts> *temp = aStack.top;//temp moves
    //through the nodes from top to bottom of aStack.
    Node<Ts> *end;//Points to end of the new stack.

    end = new Node<T>(temp->getData(), NULL);
    top = end;
    //First node created and filled with data.
    //New nodes are now added AFTER this first node.

    temp = temp->getLink();//move temp to second node
    //or NULL if there is no second node.
    while (temp != NULL)
    {
        end->setLink(
            new Node<T>(temp->getData(), NULL));
        temp = temp->getLink();
        end = end->getLink();
    }
    //end->link == NULL;
}

13. template<class Ts>
Stack<T>& Stack<T>::operator =(const Stack<T>& rightSide)
{
    if (top == rightSide.top) //if two stacks are the same
        return *this;
    else //send left side back to freestore
    {
        T next;
        while (! isEmpty())
            next = pop();//remove calls delete.
    }

    if (rightSide.isEmpty())
    {
        top = NULL;
        return *this;
    }
    else
    {
        Node<Ts> *temp = rightSide.top;//temp moves through
        //the nodes from front top to bottom of rightSide.
        Node<Ts> *end;//Points to end of the left-side stack.
        end = new Node<T>(temp->getData(), NULL);
```

```
top = end;;
//First node created and filled with data.
//New nodes are now added AFTER this first node.

temp = temp->getLink();//Move temp to second node
//or set to NULL if there is no second node.

while (temp != NULL)
{
    end->setLink(
        new Node<T>(temp->getData(), NULL));
    temp = temp->getLink();
    end = end->getLink();
}
//end->link == NULL;

    return *this;
}
```

14. 以下内容应放在命名空间 QueueSavitch 中：

```
//Uses cstddef:
template<class T>
Queue<T>::Queue() : front(NULL), back(NULL)
{
    //Intentionally empty.
}

//Uses cstddef:
template<class T>
bool Queue<T>::isEmpty() const
{
    return (back == NULL);//front == NULL would also work
}
```

15. 以下内容应放在命名空间 QueueSavitch 中：

```
//Uses cstddef:
template<class T>
void Queue<T>::add(T item)
{
    if (isEmpty())
        front = back = new Node<T>(item, NULL);//Sets both
        //front and back to point to the only node
    else
    {
        back->setLink(new Node<T>(item, NULL));
        back = back->getLink();
```

```
//Uses cstdlib and iostream:
template<class T>
T Queue<T>::remove()
{
    if (isEmpty())
    {
        cout << "Error: Removing an item from an empty queue.\n";
        exit(1);
    }

    T result = front->getData();

    Node<T> *discard;
    discard = front;
    front = front->getLink();
    if (front == NULL) //if you removed the last node
        back = NULL;

    delete discard;

    return result;
}
```

16. 以下内容应放在命名空间 QueueSavitch 中：

```
template<class T>
Queue<T>::Queue()
{
    T next;
    while (! isEmpty())
        next = remove();//remove calls delete.
}
```

17. 以下内容应放在命名空间 QueueSavitch 中：

```
//Uses cstddef:
template<class T>
Queue<T>::Queue(const Queue<T>& aQueue)
{
    if (aQueue.isEmpty())
        front = back = NULL;
    else
    {
        Node<T> *temp = aQueue.front;//temp moves
        //through the nodes from front to back of aQueue.
        back = new Node<T>(temp->getData(), NULL);
```

