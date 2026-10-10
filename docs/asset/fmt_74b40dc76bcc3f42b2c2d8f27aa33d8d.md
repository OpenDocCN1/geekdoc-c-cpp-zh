
当队列离开范围时，析构函数会销毁队列；即释放元素所占的内存。析构函数的定义与 `initializeQueue` 函数相似。此外，实现拷贝构造函数和重载赋值运算符与栈相似。实现这些操作留给你们作为练习。

## 示例 1-5

下面的程序测试了队列的各种操作。它使用 `linkedType` 类来实现队列。

```cpp
// 测试队列

#include <iostream>
#include "linkedQueue.h"

using namespace std;
int main()
{
  linkedQueueType<int> queue;
  int x, y;

  queue.initialize();
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

  cout << "队列元素: ";
  while (!queue.isEmptyQueue()) {
    cout << queue.front() << " ";
    queue.deleteQueue();
  }

  cout << endl;
  return 0;
}
```

### 样例运行

队列元素: 5 9 16 4 2

## 从 `unorderedLinkedListType` 类派生的队列

从实现队列操作的函数定义可以看出，队列的链式实现与正向创建的链表实现相似（参见第 18 章）。`addQueue` 操作与 `insertFirst` 操作相似。同样，`initializeQueue` 和 `isEmptyList` 操作相似。`deleteQueue` 可以像之前一样实现。指针 `queueFront` 等同于指针 `first`，指针 `queueRear` 等同于指针 `last`。这种对应关系表明我们可以派生实现 `linkedLinkedList` 的类（参见第 18 章）。注意 `linkedListType` 类是一个抽象类，没有实现所有操作。然而，`unorderedLinkedListType` 类派生自 `LinkedListType`，并提供了 `LinkedListType` 类抽象函数的定义。因此，我们可以从 `unorderedLinkedListType` 类派生出 `linkedQueueType` 类。

队列的应用：仿真 | 1183

我们将留一个练习，让你定义派生自 `unorderedLinkedListType` 类的 `linkedQueueType`。请参见本章末尾的编程练习 17。

## 队列的应用：仿真

用一个系统模拟另一个系统的行为的技术称为仿真。例如，物理模拟器包括用于实验车身设计的风洞，以及用于训练航空公司飞行员的飞行模拟器。当对真实系统进行实验成本高昂或极其危险时，就会使用仿真技术（我们将很快描述一些由计算机建模的真实系统）。

使用计算机模型模拟昂贵或危险实验的行为通常比使用真实系统成本更低，而且是在不危及人类生命的情况下获得洞察的好方法。此外，对于难以构建数学模型的复杂系统，计算机仿真特别有用。对于此类系统，计算机模型可以保持描述的准确性。在计算机仿真中，程序的步骤被用于模拟真实系统的行为。让我们考虑一个：

某当地电影院的经理正在听到顾客关于排队购票等待时间长的投诉。电影院目前只有一名收银员。另一家电影院准备在该附近开业，经理担心流失客户。经理希望确保有足够的收银员，让顾客不需要等待太久就能买票，但不想雇用额外的收银员或可能浪费金钱。经理想知道的一点是顾客的平均等待时间。经理希望有人写一个程序来模拟电影院的行为。

在计算机仿真中，被研究的对象通常表示为数据。对于电影院问题，某些对象是顾客和收银员。收银员服务顾客，我们想要确定顾客的平均等待时间。动作通过编写算法来实现，算法在编程语言中通过函数的帮助实现。在 C++ 中，我们可以借助类将数据和操作组合成单个单元。因此，对象可以表示为类。类的成员描述了对象的属性，而函数成员描述了对该数据的操作。如果我们改变数据的值或修改函数的定义（实现动作的算法），仿真的结果也会发生变化。计算机仿真的主要目标是生成显示现有系统性能的结果，或预测提议系统的性能。

在电影院问题中，当收银员服务顾客时，其他顾客必须等待。由于顾客是按照先来后到的原则接受服务的，而队列是实现先进先出（FIFO）系统的有效方法，因此队列是计算机仿真中的重要数据结构。本节研究了以队列作为基本数据结构的计算机仿真。这些仿真模拟了被称为“队列系统”的系统行为，在系统中，对象队列将由各种服务器服务。换句话说，一个队列系统由服务器和等待服务的对象队列组成。我们每天都会处理各种队列系统。例如，超市和银行系统都是队列系统。此外，当你向一个由多人共享的网络打印机发送打印请求时，你的打印请求会进入队列。在你的打印请求之前到达的打印请求通常会在你的请求之前完成。因此，当文档队列等待打印时，打印机充当了服务器的角色。

### 设计队列系统

在本节中，我们描述了一种可以使用各种场景的队列系统，例如银行、超市、电影院、打印机，或几个人试图使用相同处理器执行其程序的主机环境。为了描述队列系统，我们使用“服务器”一词来描述提供服务的对象。例如，在银行中，出纳员是服务器；在超市或电影院中，收银员是服务器。我们将接收服务的对象称为“顾客”，将服务时间——服务顾客所需的时间——称为“交易时间”。

由于队列系统由服务器和等待对象的队列组成，我们将建模一个由服务器列表和一个持有待服务顾客的等待队列组成的系统。队列头的顾客等待下一个可用的服务器。当服务器空闲时，队列头的顾客移动到空闲服务器处接受服务。

当第一个顾客到达时，所有服务器都是空闲的，顾客移动到第一个服务器。当下一个顾客到达时，如果有可用服务器，顾客立即移动到可用服务器；否则，顾客在队列中等待。为了建模队列系统，我们需要知道服务器的数量、顾客的预期到达时间、顾客到达之间的时间间隔以及影响系统的事件数量。

让我们考虑电影院系统。系统的性能取决于有多少个可用服务器、服务一个顾客需要多久以及顾客到达的频率。如果服务一个顾客花费的时间太长，就需要更多的服务器。该系统可以被建模为时间驱动的仿真。在时间驱动的仿真中，时钟被实现为一个计数器，例如一分钟的流逝可以通过计数器加 1 来实现。仿真运行固定的时间。如果仿真需要运行 100 分钟，计数器从 1 开始到 100，这通过循环来实现。

对于本节描述的仿真，我们想要确定顾客的平均等待时间。要计算平均等待时间，我们需要相加每个顾客的等待时间，然后将总和除以到达的顾客人数。当顾客到达时，他进入队列末尾，顾客的等待时间开始。如果队列为空且服务器空闲，顾客立即获得服务，因此该顾客的等待时间为零。相反，如果顾客到达时队列不为空或所有服务器都忙，顾客必须等待下一个可用的服务器，因此该顾客的等待时间开始。我们可以使用每个顾客的计时器来跟踪其等待时间。当顾客到达时，计时器设置为 0，并在每个单位后递增。

假设服务器到位需要五分钟。当服务器变空闲且顾客的等待时间不为空时，队列头的顾客将开始交易。因此，当顾客到达服务器时，交易时间被设置为 5，并在每个单位后递减。当交易时间变为 0 时，服务器被标记为空闲。因此，实现时间驱动仿真所需的两个对象是顾客和服务器。

接下来，在设计实现仿真的主算法之前，我们设计了类来实现这两者每一个：顾客和服务器。

### 顾客

每个顾客都有顾客编号、到达时间、等待时间、交易时间和离开时间。如果我们知道到达时间、等待时间和交易时间，就可以通过相加这三个时间来确定离开时间。我们将实现顾客对象的类命名为 `customerType`。由此 `customerType` 有四个成员变量：`customerNumber`、`arrivalTime`、`waitingTime` 和 `elapsedTime`。在 `customerType` 类型对象上执行的基本操作如下：设置顾客的编号、时间和等待时间；等待时间增加一个单位；返回等待时间；返回交易时间；返回顾客编号。以下 `customerType` 类作为抽象数据类型（AD）实现了它。

```cpp
class customerType {
public:
    customerType(int cN = 0, int arrvTime = 0, int wTime = 0,
        int time = 0);
    // 根据参数初始化实例变量构造函数
    // 如果在对象声明中没有指定值
    // 则分配默认值。
    // 后置条件：customerNumber = cN;
        arrivalTime = arrvTime;
        waitingTime = wTime;
        transactionTime = tTime
```

```cpp
void setCustomerInfo(int customerN = 0, int inTime = 0,
    int wTime = 0, int tTime = 0);
// 初始化实例变量的函数。
// 根据参数设置实例变量。
// 后置条件：customerNumber = customerN;
    arrivalTime = arrvTime;
    waitingTime = wTime;
//
    transactionTime = tTime;
```

```cpp
int getWaitingTime() const;
// 返回客户等待时间的函数。
// 后置条件：返回 waitingTime 的值。
```

```cpp
void setWaitingTime(int time);
// 设置客户等待时间的函数。
// 后置条件：waitingTime = time;
```

```cpp
void incrementWaitingTime() const
// 将等待时间增加一个单位的函数。
// 后置条件：waitingTime++;
```

```cpp
int getArrivalTime() const;
// 返回客户到达时间的函数。
// 后置条件：返回 arrivalTime 的值。
```

```cpp
int getTransactionTime() const;
// 返回客户交易时间的函数。
// 后置条件：返回 transactionTime 的值。
```

```cpp
int getCustomerNumber() const;
// 返回客户编号的函数。
// 后置条件：返回 customerNumber 的值。
```

private:

```cpp
int customerNumber;
int arrivalTime;
int waitingTime;
int transactionTime;
```

图 19-36 显示了 `customerType` 类的 UML 类图。

### 1186 | 第 19 章：栈与队列

![](img/abc25bb507ebb3eb05460d88ce0e0fde_1227_0.png)

**图 19-36** `customerType` 类的 UML 类图

`customerType` 类成员函数的定义可以根据其描述很容易推推出。接下来，我们给出 `customerType` 类成员函数的定义。

`setCustomerInfo` 函数使用参数值来初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。`setCustomerInfo` 的定义如下：

```cpp
void customerType::setCustomerInfo(int customerN, int arrvTime, int wTime, int tTime)
{
    customerNumber = customerN;
    arrivalTime = arrvTime;
    waitingTime = wTime;
    transactionTime = tTime;
}
```

构造函数的定义与函数 `setCustomerInfo` 的定义相似。它使用参数值来初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。为了方便调试，我们使用 `setCustomerInfo` 函数来编写构造函数的定义，其如下如下：

1188 | 第 19 章：栈与队列

```cpp
customerType::customerType(int customerN, int arrvTime,
int wTime, int tTime)
{
    setCustomerInfo(customerN, arrvTime, wTime, tTime);
}
```

`getWaitingTime` 函数返回当前的等待时间。`getWaitingTime` 函数的定义如下：

```cpp
int customerType::getWaitingTime() const
{
    return waitingTime;
}
```

`incrementWaitingTime` 函数增加等待时间的值。它的定义为：

```cpp
void customerType::incrementWaitingTime()
{
    waitTime++;
}
```

`setWaitingTime`、`getArrivalTime`、`getTransactionTime` 和 `getCustomerNumber` 函数的定义留给你们练习。

### 服务器

在任何时刻，服务器要么正在为客户提供服务，要么处于空闲状态。我们使用一个字符串变量来设置服务器的状态。每个服务器都有计时器，由于程序可能需要知道哪个客户由哪个服务器服务，因此服务器还存储了正在被服务的客户的信息。因此，服务器与三个成员变量相关：状态、`transactionTime` 和 `currentCustomer`。在服务器上必须执行的一些基本操作如下：检查服务器是否空闲；将服务器设为空闲；将服务器设为忙碌；设置交易时间（即服务客户所需的时间）；返回剩余的交易时间（以确定是否应该将服务器设置为空闲）；如果服务器在每个时间单位后仍忙碌，则将交易时间减一个单位，以此此类推。以下类 `serverType` 将抽象数据类型（ADT）实现了服务器。

```cpp
class serverType
{
public:
    serverType();
    // 将实例变量的值设置为它们的默认值。
    // 后置条件：currentCustomer 由其默认构造函数初始化；status = "free"；
    // 交易时间初始化为 0。
```

```cpp
bool isFree() const;
// 判断服务器是否空闲的函数。
// 后置条件：如果服务器空闲则返回 true，
// 否则返回 false。
```

```cpp
void setBusy();
// 将服务器状态设为忙碌的函数。
// 后置条件：status = "busy";
```

```cpp
void setFree();
// 将服务器状态设为 "free" 的函数。
// 后置条件：status = "free";
```

```cpp
void setTransactionTime(int t);
// 根据参数 t 设置交易时间的函数；
// 后置条件：transactionTime = t;
```

```cpp
void getTransactionTime();
// 返回交易时间的函数。
// 注意：此处原文为 getTransactionTime 但逻辑上可能返回剩余时间，按原文翻译。
// 返回剩余交易时间的函数（以确定是否应该将服务器设置为空闲）；
```

如果服务器在每个时间单位后仍忙碌，则将交易时间减一个单位，以此此类推。以下类 `serverType` 将抽象数据类型（ADT）实现了服务器。

```cpp
class serverType
{
public:
    serverType();
    // 将实例变量的值设置为它们的默认值。
    // 后置条件：currentCustomer 由其默认构造函数初始化；status = "free"；
    // 且交易时间初始化为 0。
```

```cpp
bool isFree() const;
// 判断服务器是否空闲的函数。
// 后置条件：如果服务器空闲则返回 true，
// 否则返回 false。
```

```cpp
void setBusy();
// 将服务器状态设为忙碌的函数。
// 后置条件：status = "busy";
```

```cpp
void setFree();
// 将服务器状态设为 "free" 的函数。
// 后置条件：status = "free";
```

```cpp
void setTransactionTime(int t);
// 根据参数 t 设置交易时间的函数；
// 后置条件：transactionTime = t;
```

```cpp
void getTransactionTime();
// 返回交易时间的函数。
```

注：由于原文中代码块与描述存在错位或重复，此处严格遵循原文行进行翻译

重新对齐原文 `server` 部分翻译：

# 服务器
