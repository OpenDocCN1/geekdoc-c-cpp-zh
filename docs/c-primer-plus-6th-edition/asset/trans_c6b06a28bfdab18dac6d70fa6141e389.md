
展示了如何进行这种转换。与类模板常见一样，头文件包含了类模板，以及方法函数模板。

# 列表 15.5 queuetp.h

```
// queuetp.h -- 带有嵌套类的队列模板
#ifndef QUEUETP_H_
#define QUEUETP_H_

template <class Item>
class QueueTP
{
private:
    enum {Q_SIZE = 10};
    // Node 是一个嵌套类定义
    class Node
    {
public:
    Item item;
    Node * next;
    Node(const Item &i):item(i), next(0) {}
    };
    Node * front; // 指向队头的指针
    Node * rear; // 指向队尾的指针
    int items; // 队列当前的元素数量
    const int qsize; // 队列中元素的最大数量
    QueueTP(const QueueTP & q) : qsize(0) {}
    QueueTP & operator=(const QueueTP & q) { return *this; }
public:
    QueueTP(int qs = Q_SIZE);
    ~QueueTP();
    bool isEmpty() const {
        return items == 0;
    }
    bool isFull() const {
        return items == qsize;
    }
    int queuecount() const
    {
        return items;
    }
    bool enqueue(const Item &item); // 将元素添加到末尾
    bool dequeue(Item &item); // 从队头移除元素
};
```

```cpp
// QueueTP 方法
template <class Item>
QueueTP::QueueTP(int qs) : qsize(qs)
{
    front = rear = 0;
    items = 0;
}
```

```cpp
template <class Item>
QueueTP::~QueueTP()
{
    Node * temp; 
    while (front != 0)
    {
        temp = front; // 保存队头元素的地址
        front = front->next; // 重置指针到下一个元素
        delete temp; // 删除原来的队头
    }
}
```

```cpp
// 将元素添加到队列
template <class Item>
bool QueueTP<Item>::enqueue(const Item &item)
{
    if (isfull())
        return false;
    Node * add = new Node(item); // 创建节点
    // 如果失败，new 会抛出 std::bad_alloc 异常
    items++;
    if (front == 0) // 如果队列为空
        front = add; // 将元素放在队头
    else
        rear->next = add; // 否则放在队尾
    rear = add; // 让队尾指向新节点
    return true;
}
```

```cpp
// 将队头放入 item 变量并从队列移除
template <class Item>
bool QueueTP<Item>::dequeue(Item &item)
{
    if (front == 0)
        return false;
    item = front->item; // 将元素设置为队列中的第一个元素
    items--;
    Node * temp = front; // 保存第一个元素的位置
    front = front->next;   // 重置队头到下一个元素
    delete temp;               // 删除原来的第一个元素
    if (items == 0) {
        rear = 0;
        return true;
    }
    return true;
}
#endif
```

列表 15.5 中模板的一个有趣点是，Node 是根据泛型类型 Item 定义的。因此，如下所示的声明将定义一个用于存储 `double` 类型值的 Node：

```
QueueTP<double> dq;
```

接下来的声明将定义一个用于存储 `char` 类型值的 Node：

```
QueueTP<char> cq;
```

这两个 Node 类定义在两个不同的 QueueTP 类中，因此它们之间没有名称冲突。也就是说，其中一个节点类型为 `QueueTP<double>::Node`，另一个节点类型为 `QueueTP<char>::Node`。
列表 15.6 提供了一个测试该新类的短程序。

# 列表 15.6 nested.cpp

```cpp
// nested.cpp -- 使用带有嵌套类的队列
#include <iostream>
#include <string>
#include "queuetp.h"

using namespace std;

int main() {
    string name;
    QueueTP<string> cs(5);
    string temp;

    while(!cs.isFull()) {
        cout << "请输入您的名字。您将“按到达顺序服务”。\nname: \"";
        getline(cin, temp);
        cs.enqueue(temp);
    }
    cout << "队列已满。开始处理!\n";

    while (!cs.isEmpty()) {
        cs.dequeue(temp);
        cout << "正在处理 " << temp << "...\n";
    }
    return 0;
}
```

以下是列表 15.5 和 15.6 中程序的示例运行：

```text
请输入您的名字。您将“按到达顺序服务”。
name: Kinsey Millhome
请输入您的名字。您将“按到达顺序服务”。
name: Adam Dalglish
请输入您的名字。您将“按到达顺序服务”。
name: Andrew Dalziel
请输入您的名字。您将“按到达顺序服务”。
name: Kay Scaretta
请输入您的名字。您将“按到达顺序服务”。
name: Richard Jury
队列已满。开始处理！
正在处理 Kinsey Millhome...
正在处理 Adam Dalglish...
正在处理 Andrew Dalziel...
正在处理 Kay Scaretta...
正在处理 Richard Jury...
```

# 异常

程序会遇到阻止其正常运行的运行时问题。例如，程序可能会尝试打开一个不可用的文件，或者可能请求比可用内存更多的内存，或者可能会遇到它无法处理的值。通常，程序员会尝试预测这些情况。C++ 异常提供了一个强大且灵活的工具来处理这些情况。异常是 C++ 之后添加的功能，因此某些旧版本的编译器尚未实现它们。

在检查异常之前，让我们看看程序员可用的一些基础选项。作为一个测试用例，让我们来看计算两个数调和平均数的函数。两个数的调和平均数定义为倒数平均值的倒数。这可以简化为以下表达式：

```
2.0 * x * y / (x + y)
```

## 调用 abort()

注意，如果 y 是 x 的负数，会导致除以零。许多编译器通过生成类似 Inf 的特殊浮点值来处理除以零。注意，如果 y 是 x 的负数，会导致除以零。许多编译器通过生成类似 Inf 的特殊浮点值来处理除以零。处理这种情况的方法是使用 `abort()` 函数，它的原型在 `stdlib` 头文件中，并终止程序。通常，不同的编译器会产生不同的终止信息。在这种情况下，依赖程序员在调用 `hmean()` 函数之前检查 x 和 y 的值是不安全的。

## 返回错误代码

比中止更灵活的方法是使用函数的返回值来指示问题。例如，`ofstream` 类的 `get(void)` 成员函数在遇到文件结束时通常返回 EOF 值。对于 `hmean()`，任何数值都可能是有效的返回值，因此没有值可以指示问题。在这种情况下，你使用指针或引用参数将值传回给调用程序，并使用函数返回值指示成功或失败。`ifstream` 使用重载的 `>>` 运算符是这种技术的变体。通过告知调用程序成功或失败，你为程序提供了除了中止之外的操作。列表 15.8 显示了这种方法的示例。它将 `hmean()` 重定义为一个指示成功或失败的 bool 函数，并增加第三个参数来获取答案。

# 列表 15.7 error.cpp

```cpp
// error.cpp -- 使用 abort()
#include <iostream>
// // ...

int main()
{
    double x, y, z;

    cout << "输入两个数字：";
    while (cin >> x >> y)
    {
        if (hmean(x, y, z))
            cout << x << " 和 " << y << " 的调和平均数是 " << z << endl;
        cout << "输入下一个数字退出：";
    }
    return 0;
}

bool hmean(double a, double b, double &result)
{
    if (a == -b)
    {
        cout << "参数无效，调用 hmean()\n";
        abort();
    }
    result = 2.0 * a * b / (a + b);
    return true;
}
```

### 示例运行：

```text
输入两个数字：3 6
3 和 6 的调和平均数是 4
输入下一个数字退出：10 -10
参数无效，调用 hmean()
异常程序终止
```

