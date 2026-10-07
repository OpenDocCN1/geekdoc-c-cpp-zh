

```cpp
public:
    Customer() { arrive = processstime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processstime; }
};
void Customer::set(long when) {
    processstime = std::rand() % 3 + 1;
    arrive = when;
}
```

默认构造函数创建一个客户。`set()` 成员函数将到达时间设置为其参数，并从 1 到 3 之间随机选择一个值作为处理时间。

列表 12.10 汇总了 `Queue` 和 `Customer` 类的声明，列表 12.11 提供了这些的方法。

# 列表 12.10 queue.h

```cpp
// queue.h -- 队列接口
#ifndef QUEUE_H_
#define QUEUE_H_
// 此队列将包含 Customer 项
class Customer {
private:
    long arrive; // 客户到达时间
    int processstime; // 客户处理时间
public:
    Customer() { arrive = processstime = 0; }
    void set(long when);
    long when() const { return arrive; }
    int ptime() const { return processstime; }
};
```

```cpp
class Queue {
private:
    // 类作用域定义
    // Node 是局部于此类的嵌套结构定义
    struct Node { Item item; struct Node * next; };
    enum {Q_SIZE = 10};
    // 私有类成员
    Node * front; // 指向队列头的指针
    Node * rear; // 指向队列尾的指针
    int items; // 队列中当前的项数
    const int qsize; // 队列的最大项数
    // 防止公共拷贝的抢占定义
    Queue(const Queue & q) : qsize(0) {}
    Queue &operator=(const Queue & q) { return *this; }
public:
    Queue(int qs = Q_SIZE); // 创建具有 qs 限制的队列
    ~Queue();
    bool empty() const;
    bool isfull() const;
    int queuecount() const;
    bool enqueue(const Item&item); // 将项添加到末尾
    bool dequeue(Item&item); // 从头部移除项
};
#endif
```

# 列表 12.11 queue.cpp

```cpp
// queue.cpp -- Queue 和 Customer 方法
#include "queue.h"
#include <cstdlib> // (或 stdlib.h) 用于 rand()

// 队列方法
Queue::Queue(int qs) : qsize(qs)
{
    front = nullptr; // 或 nullptr
    items = 0;
}

Queue::~Queue()
{
    Node * temp;
    while (front != NULL) // 当队列尚未为空
    {
        temp = front; // 保存头部项的地址
        front = front->next; // 重置指针指向下一个项
        delete temp; // 删除原头部
    }
}

bool Queue::isEmpty() const
{
    return items == 0;
}

bool Queue::isfull() const
{
    return items == qsize;
}

int Queue::queuecount() const
{
    return items;
}

// 将项添加到队列

bool Queue::enqueue(const Item &item)
{
    if (isfull())
        return false;
    Node *add = new Node; // 创建节点
    // 失败时，抛出 std::bad_alloc 异常
    add->item = item; // 设置节点指针
    add->next = NULL; // 或 nullptr;
    items++;
    if (front == NULL) // 如果队列为空
        front = add; // 将项放在头部
    else
        rear->next = add; // 否则放在尾部
    rear = add; // 让尾指向新节点
    return true;
}

// 将项放入 item 变量并从队列移除

bool Queue::dequeue(Item &item)
{
    if (front == NULL)
        return false;
    item = front->item; // 将项设置为队列中的第一个项
    items--;
    Node *temp = front; // 保存第一个项的位置
    front = front->next; // 重置头部为下一个项
    delete temp;
    if (front == NULL)
        rear = nullptr;
    return true;
}
```

