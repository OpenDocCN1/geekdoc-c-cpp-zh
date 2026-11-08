
如果队列非空，操作 `front` 返回队列的第一个元素，因此返回由指针 `queueFront` 所指示的队列元素。如果队列为空，函数 `front` 将终止程序。

如果队列非空，操作 `back` 返回队列的最后一个元素，因此返回由指针 `queueRear` 所指示的队列元素。如果队列为空，函数 `back` 将终止程序。类似地，如果队列非空，操作 `deleteQueue` 删除队列的第一个元素，因此我们访问指针 `queueFront`。

实现这些操作的函数定义如下：

```cpp
template <class Type>
void linkedQueueType<Type>::addQueue(const Type& newElement)
{
    nodeType<Type> *newNode;

    newNode = new nodeType<Type>;    //create the node

    newNode->info = newElement; //store the info
    newNode->link = NULL;      //initialize the link field to NULL

    if (queueFront == NULL) //if initially the queue is empty
    {
        queueFront = newNode;
        queueRear = newNode;
    }
    else                 //add newNode at the end
    {
        queueRear->link = newNode;
        queueRear = queueRear->link;
    }
}//end addQueue

template <class Type>
Type linkedQueueType<Type>::front() const
{
    assert(queueFront != NULL);
    return queueFront->info;
} //end front

template <class Type>
Type linkedQueueType<Type>::back() const
{
    assert(queueRear != NULL);
    return queueRear->info;
} //end back

template <class Type>
void linkedQueueType<Type>::deleteQueue()
{
    nodeType<Type> *temp;

    if (!isEmptyQueue())
    {
        temp = queueFront;          //make temp point to the
                                    //first node
        queueFront = queueFront->link; //advance queueFront

        delete temp;    //delete the first node

        if (queueFront == NULL) //if after deletion the
                                 //queue is empty
            queueRear = NULL;   //set queueRear to NULL
    }
    else
        cout << "Cannot remove from an empty queue" << endl;
}//end deleteQueue
```

默认构造函数的定义如下：

```cpp
template<class Type>
linkedQueueType<Type>::linkedQueueType()
{
    queueFront = NULL; //set front to null
    queueRear = NULL;  //set rear to null
} //end default constructor
```

当队列对象超出作用域时，析构函数会销毁队列；也就是说，它会释放队列元素所占用的内存。实现析构函数的函数定义与函数 initializeQueue 的定义类似。此外，实现复制构造函数和重载赋值运算符的函数与栈的对应函数类似。实现这些操作留作你的练习。

### 示例 17-5

下面的程序测试队列的各种操作。它使用类 linkedQueueType 实现一个队列。

```cpp
//Test Program linked queue

#include <iostream>
#include "linkedQueue.h"

using namespace std;
int main()
{
    linkedQueueType<int> queue;
    int x, y;

    queue.initializeQueue();
    x = 4;
    y = 5;
    queue.addQueue(x);
    queue.addQueue(y);
    x = queue.front();
    queue.deleteQueue();
    queue.addQueue(x + 5);
    queue.addQueue(16);
    queue.addQueue(x);
    queue.addQueue(y - 3);

    cout << "Queue Elements: ";

    while (!queue.isEmptyQueue())
    {
        cout << queue.front() << " ";
        queue.deleteQueue();
    }

    cout << endl;

    return 0;
}
```

**示例运行：**

队列元素：5 9 16 4 2

## 从 `class unorderedLinkedListType` 派生的队列

从实现队列操作的函数定义可以清楚地看出，队列的链式实现类似于以正向方式创建的链表的实现（见第16章）。addQueue 操作类似于 insertFirst 操作。同样，initializeQueue 和 initializeList 操作以及 isEmptyQueue 和 isEmptyList 操作也类似。deleteQueue 操作可以像以前一样实现。指针 queueFront 与指针 first 相同，指针 queueRear 与指针 last 相同。这种对应关系表明，我们可以从类 linkedListType 派生类 linkedQueueType（见第16章）。注意，类 linkedListType 是一个抽象类，并没有实现所有操作。然而，类 unorderedLinkedListType 派生自类 linkedListType，并提供了类 linkedListType 的抽象函数的定义。因此，我们可以从类 unorderedLinkedListType 派生类 linkedQueueType。

我们把它留作你的练习：编写从类 `unorderedLinkedListType` 派生的类 `linkedQueueType` 的定义。见本章末尾的编程练习 17。

## 队列的应用：模拟

一种用一个系统模拟另一个系统行为的技术称为模拟。例如，物理模拟器包括用于试验车身设计的风洞和用于训练航空公司飞行员的飞行模拟器。当对真实系统进行实验过于昂贵或危险时，就使用模拟技术。你也可以设计计算机模型来研究真实系统的行为。（我们很快就会描述一些由计算机建模的真实系统。）

使用计算机模型模拟昂贵或危险实验的行为，通常比使用真实系统成本更低，并且是在不危及人的生命的情况下获得洞见的好方法。此外，当难以构建数学模型时，计算机模拟对复杂系统特别有用。对于这类系统，计算机模型可以保持描述准确性。在计算机模拟中，程序的步骤被用来模拟真实系统的行为。让我们考虑一个这样的问题。

当地一家电影院的经理不断听到顾客抱怨买票排队等待的时间太长。该影院目前只有一名收银员。另一家影院正准备在附近开业，经理担心失去顾客。经理想雇佣足够的收银员，使顾客不必等太久就能买票，但又不想以试用方式雇佣额外收银员，从而可能浪费时间和金钱。经理想知道的一件事是顾客等待服务的平均时间。经理希望有人编写一个程序来模拟该影院的行为。

在计算机模拟中，被研究的对象通常表示为数据。对于影院问题，一些对象是顾客和收银员。收银员为顾客服务，我们想要确定顾客的平均等待时间。动作通过编写算法来实现，而在编程语言中，算法是借助函数来实现的。因此，函数被用来实现对象的动作。在 C++ 中，我们可以借助类将数据及对数据的操作组合成一个单元。因此，对象可以表示为类。类的成员变量描述对象的属性，函数成员描述对数据的操作。如果我们改变数据的值或修改函数的定义（即修改实现动作的算法），模拟结果也可能发生这种变化。计算机模拟的主要目标要么是生成显示现有系统性能的结果，要么是预测拟议系统的性能。

在影院问题中，当收银员正在为一位顾客服务时，其他顾客必须等待。因为顾客按照先到先服务的原则接受服务，而队列是
