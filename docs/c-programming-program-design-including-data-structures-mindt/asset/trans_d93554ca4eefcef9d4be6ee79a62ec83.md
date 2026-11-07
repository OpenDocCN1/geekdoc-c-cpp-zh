

`isFullQueue` 操作返回 `false`。（只有当内存耗尽时队列才会满。）

```cpp
template <class Type>
bool linkedQueueType<Type>::isEmptyQueue() const
{
    return (queueFront == nullptr);
} //end isEmptyQueue
```

```cpp
template <class Type>
bool linkedQueueType<Type>::isFullQueue() const
{
    return false;
} //end isFullQueue
```

注意，实际上在队列的链式实现中，`isFullQueue` 函数并不适用，因为从逻辑上讲，队列永远不会满。但是，由于父类 `queueADT` 中将其声明为抽象函数，你必须提供它的定义。

### 初始化队列

`initializeQueue` 操作将队列初始化为空状态。如果队列中没有元素，则队列为空。注意，构造函数在声明队列对象时已经对队列进行了初始化。因此，此操作必须移除队列中的所有元素（如果有的话）。因此，该操作从第一个节点开始遍历包含队列的链表，并释放这些元素占用的内存。该函数的定义如下：

```cpp
template <class Type>
void linkedQueueType<Type>::initializeQueue()
{
    nodeType<Type> *temp;

    while (queueFront != nullptr)    //while there are elements
                                    //left in the queue
    {
        temp = queueFront;          //set temp to point to the
                                    //current node
        queueFront = queueFront->link;  //advance first to
                                        //the next node
        delete temp;                //deallocate memory occupied by temp
    }

    queueRear = nullptr;            //set rear to nullptr
} //end initializeQueue
```

### addQueue、front、back 和 deleteQueue 操作

`addQueue` 操作在队列末尾添加一个新元素。为了实现该操作，我们需要访问指针 `queueRear`。

如果队列非空，`front` 操作返回队列的第一个元素，即返回由指针 `queueFront` 指示的队列元素。如果队列为空，`front` 函数终止程序。

如果队列非空，`back` 操作返回队列的最后一个元素，即返回由指针 `queueRear` 指示的队列元素。如果队列为空，`back` 函数终止程序。类似地，如果队列非空，`deleteQueue` 操作删除队列的第一个元素，因此我们需要访问指针 `queueFront`。

实现这些操作的函数定义如下：

```cpp
template <class Type>
void linkedQueueType<Type>::addQueue(const Type& newElement)
{
    nodeType<Type> *newNode;

    newNode = new nodeType<Type>;    //create the node

    newNode->info = newElement;      //store the info
    newNode->link = nullptr;         //initialize the link
                                     //field to nullptr

    if (queueFront == nullptr)       //if initially the queue is empty
    {
        queueFront = newNode;
        queueRear = newNode;
    }
    else                             //add newNode at the end
    {
        queueRear->link = newNode;
        queueRear = queueRear->link;
    }
}//end addQueue

template <class Type>
Type linkedQueueType<Type>::front() const
{
    assert(queueFront != nullptr);
    return queueFront->info;
}//end front

template <class Type>
Type linkedQueueType<Type>::back() const
{
    assert(queueRear != nullptr);
    return queueRear->info;
}//end back
```

```cpp
template <class Type>
void linkedQueueType<Type>::deleteQueue()
{
    nodeType<Type> *temp;

    if (!isEmptyQueue())
    {
        temp = queueFront;  //make temp point to the
                            //first node
        queueFront = queueFront->link; //advance queueFront

        delete temp;        //delete the first node

        if (queueFront == nullptr)    //if after deletion the
                                      //queue is empty
            queueRear = nullptr;      //set queueRear to nullptr
    }
    else
        cout << "Cannot remove from an empty queue" << endl;
}//end deleteQueue
```

默认构造函数的定义如下：

```cpp
template <class Type>
linkedQueueType<Type>::linkedQueueType()
{
    queueFront = nullptr;  //set front to nullptr
    queueRear = nullptr;   //set rear to nullptr
} //end default constructor
```

当队列对象超出作用域时，析构函数销毁队列；也就是说，它释放队列元素占用的内存。实现析构函数的函数定义与 `initializeQueue` 函数的定义类似。此外，实现复制构造函数和重载赋值运算符的函数与栈的对应函数类似。实现这些操作留给读者作为练习。

### 示例 17-5

下面的程序测试了队列的各种操作。它使用 `linkedQueueType` 类来实现队列。

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
    x = 20;
    y = 35;
    queue.addQueue(x);
    queue.addQueue(y);
    x = queue.front();
    queue.deleteQueue();
    queue.addQueue(x + 7);
    queue.addQueue(78);
    queue.addQueue(x);
    queue.addQueue(y - 6);

    cout << "Queue Elements: ";

    while (!queue.isEmptyQueue())
    {
        cout << queue.front() << " ";
        queue.deleteQueue();
    }

    cout << endl;

    return 0;
}

Sample Run:

Queue Elements: 35 27 78 20 29
```

## 从 `unorderedLinkedListType` 类派生的队列

从上述实现队列操作的函数定义可以看出，队列的链式实现类似于以正向方式创建的链表的实现（参见第16章）。`addQueue` 操作类似于 `insertFirst` 操作。同样，`initializeQueue` 与 `initializeList`、`isEmptyQueue` 与 `isEmptyList` 都是相似的。`deleteQueue` 操作可以按前述方式实现。指针 `queueFront` 等同于指针 `first`，指针 `queueRear` 等同于指针 `last`。这种对应关系表明，我们可以从 `linkedListType` 类（参见第16章）派生出实现队列的类。注意，`linkedListType` 类是一个抽象类，并未实现所有操作。然而，`unorderedLinkedListType` 类派生自 `linkedListType` 类，并提供了 `linkedListType` 类中抽象函数的定义。因此，我们可以从 `unorderedLinkedListType` 类派生出 `linkedQueueType` 类。

队列是实现 FIFO（先进先出）系统的有效方式。队列是计算机模拟中重要的数据结构。本节研究以队列为基本数据结构的计算机模拟。这些模拟对称为**排队系统**的系统行为进行建模，在排队系统中，对象队列正在等待被各种服务器（服务台）服务。换句话说，排队系统由服务器和等待被服务的对象队列组成。我们每天都要处理各种各样的排队系统。例如，杂货店和银行系统都是排队系统。此外，当你向一台多人共享的网络打印机发送打印请求时，你的打印请求会进入队列。在你的打印请求之前到达的打印请求通常会在你的请求之前完成。因此，当文档队列等待被打印时，打印机充当服务器的角色。

## 设计排队系统

在本节中，我们描述一种排队系统，它可以用于各种应用，例如银行、杂货店、电影院、打印机，或者多人试图使用同一批处理器来执行各自程序的大型机环境。为了描述排队系统，我们使用术语**服务器（server）**来表示提供服务的对象。例如，在银行中，柜员是服务器；在杂货店或电影院，收银员是服务器。我们将接受服务的对象称为**顾客（customer）**，将服务时间——即服务一名顾客所需的时间——称为**事务时间（transaction time）**。

由于排队系统由服务器和等待对象的队列组成，我们将对一个由服务器列表和保存待服务顾客的等待队列组成的系统进行建模。队列前面的顾客等待下一个可用的服务器。当某个服务器空闲时，队列前面的顾客移动到该空闲服务器接受服务。

当第一位顾客到达时，所有服务器都空闲，该顾客移动到第一台服务器。当下一位顾客到达时，如果有一台服务器可用，该顾客立即移动到可用的服务器；否则，该顾客在队列中等待。为了对排队系统建模，我们需要知道服务器的数量、顾客的预期到达时间、顾客到达之间的时间间隔，以及影响系统的事件数量。

让我们再次考虑电影院系统。系统的性能取决于有多少台服务器可用、服务一名顾客需要多长时间，以及顾客到达的频率。如果服务一名顾客花费的时间太长，而顾客到达又很频繁，那么就需要更多的服务器。该系统可以建模为**时间驱动模拟**。在时间驱动的模拟中，时钟被实现为一个计数器，例如，一分钟的流逝可以通过将计数器加1来实现。模拟固定运行一段时间。如果模拟需要运行100分钟，计数器从1开始，一直加到100，这可以通过使用循环来实现。

对于本节描述的模拟，我们希望确定顾客的平均等待时间。要计算顾客的平均等待时间，我们需要将

