

这展示了如何进行这种转换。与类模板的常见情况一样，头文件包含类模板以及方法函数模板。

**清单15.5 `queuept.h`**

```cpp
// queuept.h -- queue template with a nested class
#ifndef QUEUEPT_H
#define QUEUEPT_H

template <class Item>
class QueueTP
{
private:
    enum { Q_SIZE = 10};
    // Node is a nested class definition
    class Node
    {
    public:
        Item item;
        Node * next;
        Node(const Item & i): item(i), next(0) { }
    };
    Node * front;       // pointer to front of Queue
    Node * rear;        // pointer to rear of Queue
    int items;          // current number of items in Queue
    const int qsize;    // maximum number of items in Queue
    QueueTP(const QueueTP & q) : qsize(0) { }
public:
    QueueTP(int qs = Q_SIZE);
    ~QueueTP();
    bool isempty() const
    {
        return items == 0;
    }
    bool isfull() const
    {
        return items == qsize;
    }
    int queuecount() const
    {
        return items;
    }
    bool enqueue(const Item &item); // add item to end
    bool dequeue(Item &item);       // remove item from front
};

// QueueTP methods
template <class Item>
QueueTP<Item>::QueueTP(int qs) : qsize(qs)
{
    front = rear = 0;
    items = 0;
}

template <class Item>
QueueTP<Item>::~QueueTP()
{
    Node * temp;
    while (front != 0)       // while queue is not yet empty
    {
        temp = front;        // save address of front item
        front = front->next; // reset pointer to next item
        delete temp;         // delete former front
    }
}

// Add item to queue
template <class Item>
bool QueueTP<Item>::enqueue(const Item & item)
{
    if (isfull())
        return false;
    Node * add = new Node(item);    // create node
    // on failure, new throws std::bad_alloc exception
    items++;
    if (front == 0)            // if queue is empty,
        front = add;           // place item at front
    else
        rear->next = add;      // else place at rear
    rear = add;                // have rear point to new node
    return true;
}

// Place front item into item variable and remove from queue
template <class Item>
bool QueueTP<Item>::dequeue(Item & item)
{
    if (front == 0)
        return false;
    item = front->item;       // set item to first item in queue
    items--;
    Node * temp = front;      // save location of first item
    front = front->next;    // reset front to next item
    delete temp;            // delete former first item
    if (items == 0)
        rear = 0;
    return true;
}
#endif
```

清单15.5中的模板有一个有趣之处：Node是根据泛型类型Item定义的。因此，像下面这样的声明会导致Node被定义为保存double类型的值：

```cpp
QueueTP<double> dq;
```

而下面的声明则会导致Node被定义为保存char类型的值：

```cpp
QueueTP<char> cq;
```

这两个Node类分别定义在两个独立的QueueTP类中，因此二者之间没有名称冲突。也就是说，一个节点是`QueueTP<double>::Node`类型，另一个是`QueueTP<char>::Node`类型。

清单15.6提供了一个用于测试新类的简短程序。

**清单15.6 `nested.cpp`**

```cpp
// nested.cpp -- using a queue that has a nested class
#include <iostream>

#include <string>
#include "queuetp.h"

int main()
{
    using std::string;
    using std::cin;
    using std::cout;

    QueueTP<string> cs(5);
    string temp;

    while (!cs.isfull())
    {
        cout << "Please enter your name. You will be "
                "served in the order of arrival.\n"
                "name: ";
        getline(cin, temp);
        cs.enqueue(temp);
    }
    cout << "The queue is full. Processing begins!\n";

    while (!cs.isempty())
    {
        cs.dequeue(temp);
        cout << "Now processing " << temp << "...\n";
    }
    return 0;
}
```

下面是清单15.5和15.6中程序的示例运行：

```text
Please enter your name. You will be served in the order of arrival.
name: Kinsey Millhone
Please enter your name. You will be served in the order of arrival.
name: Adam Dalgliesh
Please enter your name. You will be served in the order of arrival.
name: Andrew Dalziel
Please enter your name. You will be served in the order of arrival.
name: Kay Scarpetta
Please enter your name. You will be served in the order of arrival.
name: Richard Jury
The queue is full. Processing begins!
Now processing Kinsey Millhone...
Now processing Adam Dalgliesh...
Now processing Andrew Dalziel...
Now processing Kay Scarpetta...
Now processing Richard Jury...
```

## 异常

程序有时会遇到运行时问题，导致无法正常继续。例如，程序可能试图打开一个不可用的文件，或者请求超出可用范围的内存，或者遇到无法接受的值。通常，程序员会尝试预见这类灾难。C++异常提供了一种强大而灵活的工具来处理这些情况。异常是C++较新加入的特性，因此一些较老的编译器尚未实现它们。另外，一些编译器默认关闭了该特性，因此你可能需要使用编译器选项将其打开。

在考察异常之前，先来看看程序员可用的几种更基本的选项。作为一个测试用例，我们来看一个计算两个数调和平均数的函数。两个数的*调和平均数*定义为两个数的倒数的平均值的倒数。它可以化简为以下表达式：

`2.0 × x × y / (x + y)`

注意，如果y是x的相反数，这个公式会导致除以零，这是一种相当不可取的操作。许多较新的编译器通过生成一个表示无穷大的特殊浮点值来处理除以零；`cout`会把这个值显示为`Inf`、`inf`、`INF`或类似形式。其他编译器生成的程序可能在发生除以零时崩溃。最好编写在所有系统上都能以同样受控方式运行的代码。

### 调用`abort()`

处理这个问题的一种方法是，如果一个参数是另一个参数的相反数，就让函数调用`abort()`函数。`abort()`函数的原型位于`cstdlib`（或`stdlib.h`）头文件中。一个典型的实现被调用时，会向标准错误流（与`cerr`使用的相同）发送一条诸如“异常程序终止”的消息，并终止程序。它还会返回一个依赖于实现的值，向操作系统（或者，如果程序是由另一个程序启动的，则向父进程）指示失败。`abort()`是否刷新文件缓冲区（即用于存储与文件进行传输的数据的内存区域）取决于实现。如果愿意，可以使用`exit()`，它会刷新文件缓冲区，但不会显示消息。清单15.7展示了一个使用`abort()`的简短程序。

**清单15.7 `error1.cpp`**

```cpp
//error1.cpp -- using the abort() function
#include <iostream>
#include <cstdlib>
double hmean(double a, double b);

int main()
{
    double x, y, z;

    std::cout << "Enter two numbers: ";
    while (std::cin >> x >> y)
    {
        z = hmean(x,y);
        std::cout << "Harmonic mean of " << x << " and " << y
                  << " is " << z << std::endl;
        std::cout << "Enter next set of numbers <q to quit>: ";
    }
    std::cout << "Bye!\n";
    return 0;
}

double hmean(double a, double b)
{
    if (a == -b)
    {
        std::cout << "untenable arguments to hmean()\n";
        std::abort();
    }
    return 2.0 * a * b / (a + b);
}
```

下面是清单15.7中程序的示例运行：

```text
Enter two numbers: 3 6
Harmonic mean of 3 and 6 is 4
Enter next set of numbers <q to quit>: 10 -10
untenable arguments to hmean()
abnormal program termination
```

注意，从`hmean()`中调用`abort()`函数会直接终止程序，而不会先返回到`main()`。通常，不同的编译器会发出不同的中止消息。下面是另一条这样的消息：

```text
This application has requested the Runtime to terminate it
in an unusual way. Please contact the application's support
team for more information.
```

（或许你会觉得，我们这个小程序居然是一个支持团队，这种构思很有趣。）程序可以通过在调用`hmean()`函数之前检查x和y的值来避免中止。然而，依赖程序员足够了解（或在意）并执行这样的检查并不安全。

### 返回错误码

比中止更灵活的方法是使用函数的返回值来指示问题。例如，`ostream`类的`get(void)`成员通常返回下一个输入字符的ASCII码，但如果遇到文件结尾，则返回特殊值`EOF`。这种方法对`hmean()`并不适用。任何数值都可能是有效的返回值，因此没有可用的特殊值来指示问题。在这种情况下，可以使用指针参数或引用参数将值返回给调用程序，并使用函数返回值来指示成功或失败。`istream`家族的重载`>>`运算符使用了这种技术的一种变体。通过告知调用程序成功或失败，可以让程序选择中止以外的操作。清单15.8展示了这种方法的一个示例。它将`hmean()`重新定义为一个bool函数，其返回值指示成功或失败。它还增加了第三个参数来获取结果。

