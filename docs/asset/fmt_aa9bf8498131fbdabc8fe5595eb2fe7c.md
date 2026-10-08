
13 | int index; |

14 | // 打印十进制数字 |

15 | do |

16 | { |

17 | cout << "Enter a positive integer: "; |

18 | cin >> decimal; |

19 | } while (decimal <= 0); |

20 | cout << "The decimal number: " << decimal << endl;

21 | // 循环直到商为0

22 | while (decimal > 0) |

23 | { |

24 | index = decimal % 16; |

25 | stack.push(converter[index]); |

26 | decimal /= 16; |

27 | } |

28 | |

29 | // 从栈中弹出以构建十六进制字符串 |

30 | while (stack.size() > 0) |

31 | { |

32 | hexadecimal = stack.top() + hexadecimal; |

33 | stack.pop(); |

34 | } |

35 | cout << "The hexadecimal equivalent: " << hexadecimal << endl; |

36 | return 0;

37 | }

```

18.3 栈与队列 831

# 程序 18.7 从十进制转换为十六进制（续接）

| 行号 | 代码 |
| :--- | :--- |
| 2.3 | // 创建十六进制字符并将它们推入栈 |
| 24 | while (decimal != 0) |
| 25 | { |
| 26 | stack.push(converter [decimal % 16]); |
| 27 | decimal = decimal / 16; |
| 28 | } |
| 29 | // 将栈中的字符推入十六进制字符串 |
| 30 | while (stack.size() > 0) |
| 31 | { |
| 32 | hexadecimal.push_back(stack.top()); |
| 33 | stack.pop(); |
| 34 | } |
| 35 | // 打印十六进制数 |
| 36 | cout << "The hexadecimal number : " << hexadecimal; |
| 37 | return 0; |
| 38 | } |

运行：
输入一个正整数：124
十进制数：124
十六进制数：7C

运行：
输入一个正整数：1345
十进制数：1345
十六进制数：541

运行：
输入一个正整数：11
十进制数：11
十六进制数：8

**反转字符串** 栈作为反转器的本质可以帮助我们完成许多应用。我们曾使用递归来反转字符串中字符的顺序。我们可以改用栈来代替递归。我们可以从输入字符串中逐个地获取字符，并将它们推入一个字符栈中。然后，我们可以从栈中取出字符并创建输出字符串，如程序 18.8 所示。

# 程序 18.8 使用栈反转字符串

| 行号 | 代码 |
| :--- | :--- |
| 1 | /**************************************************** |
| 2 | * 使用栈而非递归反转字符串的应用程序 * |
| 3 | * |
| 4 | /**************************************************** / |
| 6 | #include "stack.cpp" |

（续接）

# 程序 18.8 使用栈反转字符串（续接）

```
7 int main ()

8 {

9 // 实例化一个栈对象两个字符串对象

10 Stack<char> stack;

11 string origin;

12 string reversed;

13 // 输入一个字符串

14 cout << "Enter a string to be reversed: ";

15 getline(cin, origin);

16 // 将源字符串中的字符拷贝推入栈

17 for (int i=0; i<origin.size(); i++)

18 {

19 stack.push(origin[i]);

20 }

21 // 从栈中弹出并将字符添加到结果字符串中

22 while (stack.size() > 0)

23 {

24 reversed.push_back(stack.top());

25 stack.pop();

26 }

27 // 打印两个字符串进行比较

28 cout << "Original: " << origin << endl;

29 cout << "Reversed: " << reversed << endl;

30 return 0;

31 }

```

运行：
输入要反转的字符串：Hello my friends.
原始字符串：Hello my friends.
反转字符串：sdneir ym olleh

运行：
输入要反转的字符串：rotor
原始字符串：rotor
反转字符串：rotor

## 18.3.2 队列

队列是一种列表，其中数据只能在其中端（称为队尾 back）插入，并从另一端（称为队头 front）删除。这些限制确保了数据按照其输入顺序进行输出。换句话说，队列是一种先进先出（FIFO）结构。

队列就像排队。在车站等候公交的人群列表是一个队列；被拦截等待接线员回答的电话列表是一个队列；等待计算机处理的任务列表也是队列。

图 18.14 显示了队列的两种表示形式：一种是人，另一种是数据项。人和数据都从队尾进入队列，并不断移动直到到达头部。一旦到达头部，他们就可以离开队列。

![](img/ce9c99d45f71111839bc062830bd19fd_851_0.png)

图 18.14 队列

![](img/ce9c99d45f71111839bc062830bd19fd_851_1.png)

图 18.15 链表实现的队列

尽管文献有时将 push 操作称为 enqueue（入队），将 pop 操作称为 dequeue（出队），但我们使用与 STL 库相同的术语。我们还使用 `front` 和 `back` 来访问队头元素和队尾元素。

## 实现

队列可以使用数组或链表实现。虽然数组实现更简单，但数组的大小必须在编译时固定。链表实现允许大小动态增长和缩小。图 18.15 显示了我们如何使用链表实现队列。

图 18.15 表明，我们可以使用为链表类开发的代码来创建一个队列。队列类不能派生自链表类，因为队列不是链表；它的功能更少。我们通过私有方式从链表类派生队列（代码复用），或者让队列组合一个链表对象。第一种选择（我们在讨论栈案例时提到过）在类模板类时可能会很麻烦。我们采用第二种选择：组合。

## 代码

我们为队列对象创建了一个接口文件、一个实现和一个简单的应用程序。

## 接口文件

程序 18.9 显示了接口文件。注意，我们使用了我们列表类的接口文件。

# 程序 18.9 queue.h

```
**************************************************

* 使用 List 对象作为唯一数据成员 

* 定义 Queue 类的接口文件

************************************************** (续接)
```

# 程序 18.9 queue.h（续接）

```cpp
#ifndef QUEUE_H
#define QUEUE_H
#include "list.cpp"
template<class T>
class Queue
{
private:
    List<T> data;
public:
    void push(const T& value);
    void pop();
    T& front() const;
    T& back() const;
    int size() const;
    void print() const;
};
#endif
```

正如在栈的章节中讨论的那样，`Queue` 类使用一个数据成员，即 `List` 类的实例。没有必要声明构造函数和析构函数。`Queue` 类使用默认的。

## 实现文件

`Queue` 类的实现非常简单；成员函数的定义基于 `List` 类的成员函数给出的，如程序 18.10 所示。

# 程序 18.10 queue.cpp

```
************************************************
* 根据 List 类定义的操作 
* 对 Queue 类的实现
************************************************
#ifndef QUEUE_CPP
#define QUEUE_CPP
#include "queue.h"
#include "list.cpp"
// push 操作定义
template<typename T>
void Queue<T>::push(const T& value) {
    data.insert(data.size(), value);
} (续接)
```

# 程序 18.10 queue.cpp（续接）

```cpp
// pop 操作定义
template<typename T>
void Queue<T>::pop() {
    data.erase(0);
}
// front 操作定义
template<typename T>
T& Queue<T>::front() const {
    return data.get(0);
}
// back 操作定义
template<typename T>
T& Queue<T>::back() const {
    return data.get(data.size() - 1);
}
// size 操作定义
template<typename T>
int Queue<T>::size() const {
    return data.size();
}
// print 操作定义
template<typename T>
void Queue<T>::print() const {
    data.print();
}
#endif
```

## 应用文件

我们使用一个简单的应用程序来测试队列对象的接口和实现，如程序 18.11 所示。

# 程序 18.11 测试 Queue 类的应用程序

```
************************************
* 测试 Queue 类的应用程序
***********************************
#include "queue.cpp"
int main ()
{
    (续接)
```

# 程序 18.11 应用程序文件（续接）

```cpp
// 实例化一个队列对象
queue<string> queue;
// 将四个节点推入队列
queue.push("Henry");
queue.push("William");
queue.push("Tara");
queue.push("Richard");
// 检查队列的头部和尾部元素
cout<<"Checking front and back elements:" << endl;
cout<<"after four operations:" << endl;
cout<<"Element at the front: " << queue.front() << endl;
cout<<"Element at the back: " << queue.back() << endl;
// 从队列中弹出两个元素
queue.pop();
queue.pop();
// 在两次弹出操作后检查头部和尾部节点
cout<<"Checking front and back elements:" << endl;
cout<<"after two pop operations:" << endl;
cout<<"Element at the front: " << queue.front() << endl;
cout<<"Element at the back: " << queue.back() << endl;
}
```

运行：
在 push 操作后检查头部和尾部元素：
头部：Henry
尾部：Richard

在两次弹出操作后检查头部和尾部元素：
头部：Tara
尾部：Richard

## 队列应用

队列是所有数据处理结构中最常见的结构之一。它们存在于每一个操作系统和网络以及无数其他领域。例如，队列被用于业务在线应用程序，如处理客户请求、作业和订单。

事件模拟 队列作为先进先出结构的本质，使得它在实体等待服务的应用程序中非常有帮助。例如，在银行中，客户排队（队列）等待一个或多个柜台员的服务。程序 18.12 允许使用队列进行模拟。我们模拟只有一个柜台员的银行。客户到达并排队（队列）等待柜台员的服务。模拟所需的两个信息是到达时间和服务周期。然而，为了避免到达时间，我们假设模拟从第一个客户到达开始。我们假设

# 18.3 栈与队列

第二个客户在比前一个客户随机几分钟后到达。服务时间也是一个随机数。换句话说，每个客户都由两个随机生成的整数定义。这两个随机数被封装在一个 `pair` 对象中，该对象定义在 `<utility>` 头文件中。在这种情况下，队列对象使用 `pair` 作为数据部分。

## 程序 18.12 使用队列模拟排队等待

```cpp
****************************************************************/
* 一个使用队列模拟银行客户排队
* 并查找相应统计数据的程序\****************************************************************/
#include "queue.cpp"
#include <cstdlib>
#include <ctime>
#include <iostream>
#include <utility>
// randNum 的定义
int randNum(int low, int high)
{
    int temp = rand();
    int num = temp % (high - low + 1);
    return num;
}
int main ()
{
    // 变量声明
    int size = 15;
    int arriveDelay;
    int serveTime;
    int arrive = 0;
    int start = 0;
    int leave = 0;
    int wait = 0;
    int totalServeTime = 0;
    int totalWait = 0;
    // 模拟名为 line 的队列对象
    Queue<pair<int, int>> line;
    // 模拟客户到达并入队
    for (int i = 0; i < size; i++)
    {
        pair<int, int> p(randNum(1, 6), randNum(5, 10));
        line.push(p);
```

## 程序 18.12 使用队列对象模拟排队等待（续）

```cpp
// 打印统计数据的表头
cout << left << setw(10) << "Arrive" << setw(10) << "Start";
cout << left << setw(10) << "Delay" << setw(10) << "Leave";
cout << left << setw(10) << "Serve time" << endl;
// 计算并打印统计数据
while (line.size() > 0) {
    arrive = line.front().first;
    serveTime = line.front().second;
    arrive = arrive + arriveDelay;
    if (arrive >= leave) {
        start = arrive;
    } else {
        start = start + line.front().second;
    }
    leave = start;
    wait = leave - arrive;
    cout << left << setw(10) << arrive << setw(10) << start;
    cout << left << setw(10) << leave;
    cout << left << setw(12) << serveTime << endl;
    totalServeTime += serveTime;
    totalWait += wait;
    line.pop();
}
// 打印总结
double averageWait = static_cast<double>(totalWait) / size;
cout << "--------------------------------" << endl;
cout << "Total serve time: " << totalServeTime << endl;
cout << "Average Delay: " << averageWait << endl;
```
