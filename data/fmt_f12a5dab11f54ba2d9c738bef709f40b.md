
让我们使用第一种方案来实现。也就是说，我们使用变量 `count` 来指示队列是否为空或满。以下类实现了抽象类 `queueADT` 的函数。由于数组可以动态分配，我们将实现队列的数组大小留给用户。数组的默认大小为 100。

```cpp
template <class Type>
class queueType: public queueADT<Type>{
public:
    const queueType<Type>& operator=(const queueType<Type>&);
    // 重载赋值运算符。
```

```cpp
bool isEmptyQueue() const;
// 判断队列是否为空的函数。
// 后置条件：如果队列为空，则返回 true，
// 否则返回 false。
```

```cpp
bool isFullQueue() const;
// 判断队列是否满的函数。
// 后置条件：如果队列满了，则返回 true，
// 否则返回 false。
```

```cpp
void initializeQueue();
// 将队列初始化为空状态的函数。
// 后置条件：队列为空的。
```

```cpp
Type front() const;
// 返回队列的第一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：如果队列为空，程序将
//终止；否则返回第一个
//元素。
```

```cpp
Type back() const;
// 返回队列的最后一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：如果队列为空，程序将
//终止；否则返回队列的最后一个
//元素。 
```

```cpp
void addQueue(const Type& queueElement);
// 将 queueElement 添加到队列的函数。
// 前置条件：队列存在且未满。
// 后置条件：队列发生了变化，queueElement
// 被添加到队列中。
```

```cpp
void deleteQueue();
// 移除队列第一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：队列发生了变化，第一个
//元素从队列中移除。 
```

```cpp
queueType(int queueSize = 100);
// 构造函数
```

```cpp
queueType(const queueType<Type>& otherQueue);
// 拷贝构造函数
```

```cpp
~queueType();
// 析构函数
```

```cpp
private:
int maxQueueSize; //存储队列最大大小的变量
int count; //存储队列中
//元素的数量变量
int queueFront; // 指向队列第一个
//元素的变量
int queueRear; // 指向队列最后一个
//元素的变量
Type *list; // 指向持有队列
//元素的数组的指针
```

我们将 `queueType` 类的 UML 类图留给你们作为练习题。（参见本章末尾的第 28 题。）

接下来，我们考虑队列操作的实现。

# 空队列与满队列

正如之前讨论的，当 `count == 0` 时队列为空，当 `count == maxSize` 时队列满。实现这些操作的函数有：

```cpp
template <class Type>
bool queueType<Type>::isEmpty() const
{
    return (count == 0);
} // isEmptyQueue
```

```cpp
template <class Type>
bool queueType<Type>::isFullQueue() const
{
    return (count == maxSize);
} // isFullQueue
```

# 初始化队列

此操作将队列初始化为空状态。第一个元素被添加到数组的第一个位置。因此，我们将 `queueFront` 初始化为 0，`queueRear` 初始化为 `QueueSize - 1`，`count` 初始化为 0。见图 19-35。

| [0] | [1] | [2] | | [97] | [98] | [99] |

|---|---|---|---|---|---|---|

| queueFront | | | queueRear | count | | |

图 19-35 空队列

函数 `initializeQueue` 的定义如下：

```cpp
template <class Type>
void queueType<Type>::initializeQueue()
{
    queueFront = 0;
    queueRear = maxSize - 1;
    count = 0;
} // initializeQueue
```

# 前端 (FRONT)

此操作返回队列的第一个元素。如果队列不为空，则返回索引 `queueFront` 指向的队列元素；否则程序终止。

```cpp
template <class Type>
queueType<Type>::front() const
{
    assert(!isEmptyQueue());
    return list[queueFront];
} //end front
```

# 后端 (BACK)

此操作返回队列的最后一个元素。如果队列不为空，则返回索引 `queueRear` 指定的队列元素；否则程序终止。

```cpp
template <class Type>
Type queueType<Type>::back() const
{
    assert(!isEmptyQueue());
    return list[queueRear];
} //end back
```

# addQueue

接下来，我们实现 `addQueue` 操作。因为 `queueRear` 指向队列的最后一个元素，为了向队列添加新元素，我们将 `queueRear` 移动到数组的下一个位置，然后将新元素添加到 `queueRear` 指向的数组位置。我们还将 `count` 加 1。函数 `addQueue` 如下：

```cpp
template <class Type>
void queueType<Type>::addQueue(const Type& newElement)
{
    if (!isEmptyQueue())
    {
        queueRear = (queueRear + 1) % maxQueueSize;//使用
                    // 模运算符来移动 queueRear
                    // 因为数组是循环的

        count++;
        list[queueRear] = newElement;
    }
    else
        cout << "Cannot add to a full queue." << endl;
} //addQueue
```

# deleteQueue

为了实现 `deleteQueue` 操作，我们访问索引 `queueFront`。因为 `queueFront` 指向包含队列第一个元素的数组位置，为了移除第一个队列元素，我们将 `count` 减 1 并 `queueFront` 移动到下一个队列元素。函数 `deleteQueue` 为：

# 构造函数与析构函数

为了完成队列操作的实现，接下来我们考虑构造函数和析构函数的实现。构造函数从用户处获取 `maxSize`，将变量 `maxSize` 设置为用户指定的值，并创建一个为 `maxSize` 的数组。如果用户没有指定大小，构造函数将使用默认值（100）来创建一个大小为 100 的数组。构造函数还初始化了 `queueFront` 和 `queueRear` 表示队列为空。实现构造函数的函数定义如下：

```cpp
template <class Type>
queueType<Type>::queueType(int queueSize)
{
    if (queueSize <= 0) {
        cout << "Size of the array to hold the queue must "
             << "positive." << endl;
        cout << "Creating an array of size 100." << endl;
        maxSize = 100;
    } else {
        maxSize = queueSize; //设置 maxSize
    }

    queueFront = 0; //初始化 queueFront
    queueRear = maxSize - 1; //初始化 queueRear
    count = 0;
    list = new Type[maxSize]; //创建持有
               //元素的数组
} //end constructor
```

存储队列元素的数组是动态创建的。因此，当队列对象超出作用范围时，析构函数只需释放数组所占用的内存。析构函数的函数定义如下：

```cpp
template <class Type>
queueType<Type> ::~queueType()
{
  delete [] list;
}
```

拷贝构造函数的实现和赋值运算符的重载留给你们作为练习题。（这些函数的定义与链表和栈相似。）

```cpp
void initializeQueue();
// 将队列初始化为空空状态的函数。
// 后置条件：queueFront = NULL; queueRear = NULL
```

```cpp
Type front() const;
// 返回队列中第一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：如果队列为空，程序将
//终止；否则，返回队列的第一个
//元素。
```

```cpp
Type back() const;
// 返回队列最后一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：如果队列为空，程序将
//终止；否则，返回队列的最后一个
//元素。
```

```cpp
void addQueue(const Type& queueElement);
// 将 queueElement 添加到队列中的函数。
// 前置条件：队列存在且未满。
// 后置条件：队列发生了变化，且 queueElement
// 被添加到队列中。
```

```cpp
void deleteQueue();
// 移除队列第一个元素的函数。
// 前置条件：队列存在且不为空。
// 后置条件：队列发生了变化，且第一个
//元素从队列中移除。
```

```cpp
linkedQueueType();
// 默认构造函数
```

```cpp
linkedQueueType(const linkedQueueType<Type>& otherQueue);
// 拷贝构造函数
```

```cpp
~linkedQueueType();
// 析构函数
```

```cpp
private:
node<Type>* queueFront;//指向队列头的
// 指针
node<Type>* queueRear;//指向队列尾部的
// 指针

};
```

`linkedQueueType` 类的 UML 类图留给你们作为练习。

（参见本章末尾的练习 29）。

接下来，我们编写 `linkedQueueType` 类成员函数的定义。

## 空队列与满队列

如果 `queueFront` 为 `NULL`，则队列为空。用于存储队列元素的内存是动态分配的。因此，队列永远不会是满的，所以实现 `isFull` 操作的函数返回值为 `false`。（只有当内存耗尽时，队列才满满。）

```cpp
template <class Type>
bool linkedQueueType<Type>::isEmpty() const
{
    return (queueFront == NULL);}//结束
```

```cpp
template <class Type>
bool linkedQueueType<Type>::isFull() const
{
    return false;}//isFullQueue
```

注意，实际上，在队列的链式实现中，`isFull` 函数并不适用，因为从逻辑上讲，队列永远是满的。然而，你必须提供它的定义，因为它是父类 `queueADT` 中的一个抽象函数。

## 初始化队列

`initializeQueue` 将队列初始化为空状态。如果队列中没有元素，则队列为空。注意，构造函数在声明队列对象时会初始化队列。此操作必须移除队列中的所有元素（如果有的话）。因此，此操作从第一个节点开始遍历包含队列的列表，并分配队列元素所占的内存。该函数的定义如下：

```cpp
template <class Type>
void linkedQueueType<Type>::initializeQueue()
{
    nodeType<Type> *temp;
    while (queueFront() != NULL) // 当队列中还有
                                // 元素时
    {
        temp = queueFront; // 将 temp 指向
                           // 当前节点
        queueFront = queueFront->link; // 移动到
                                       // 下一个节点
        delete temp; // 释放 temp 占用的内存
    }
    queueRear = NULL; // 将尾部设置为 NULL}//结束 initializeQueue
```

## addQueue, front, back, deleteQueue 操作

`addQueue` 操作在队列末尾添加新元素。为了实现此操作，我们访问指针 `queueRear`。

如果队列不为空，`front` 操作返回队列的第一个元素，因此返回指针 `queueFront` 指向的队列元素。如果队列为空，`front` 函数将终止程序。

如果队列不为空，`back` 操作返回队列的最后一个元素，因此返回指针 `queueRear` 指向的队列元素。如果队列为空，`back` 函数将终止程序。同样，如果 `deleteQueue` 操作移除队列的第一个元素，我们需要访问指针 `queueFront`。

实现这些操作的函数定义：

```cpp
template <class Type>
void linkedQueue<Type>::addQueue(const Type& newElement)
{
    nodeType<Type>* newNode;
    newNode = new nodeType<Type>(); // 创建节点

    newNode->info = newElement; // 存储信息
    newNode->link = NULL; // 将 link 字段初始化为 NULL

    if (queueFront == NULL) // 如果初始队列为空
    {
        queueFront = newNode;
        queueRear = newNode;
    }
    else{
        queueRear->link = newNode;
        queueRear = queueRear->link;
    }
} // 在末尾添加新节点
```

```cpp
template <class Type>
Type linkedQueue<Type>::front() const
{
    assert(queueFront != NULL);
    return queueFront->info;
} //结束 front
```

```cpp
template <class Type>
Type linkedQueue<Type>::back() const
{
    assert(queueRear != NULL);
    return queueRear->info;
} //结束 back
```

```cpp
template <class Type>
void linkedQueue<Type>::deleteQueue()
{
    nodeType<Type> *temp;

    if (!isEmptyQueue()) {
        temp = queueFront; // 让 temp 指向
        第一个节点
        queueFront = queueFront->link; // 移动 queueFront

        delete temp; // 释放节点

        if (queueFront == NULL) // 如果删除后
            队列为空
            queueRear = NULL; // 将尾部设置为 NULL
        }
    } else {
        cout << "无法从空队列中删除" << endl;
    }
}//结束 deleteQueue
```

```cpp
template<class Type>
linkedQueueType<Type>::linkedQueueType()
{
    queueFront = NULL; // 将头部设置为空
    queueRear = NULL; // 将尾部设置为空}//结束默认构造
```
