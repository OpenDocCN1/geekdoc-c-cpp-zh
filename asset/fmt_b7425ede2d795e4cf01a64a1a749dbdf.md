
第一个节点

`queueFront = queueFront->link;`

`delete temp; // 释放节点`

}

else

{

`cout << "无法从空队列中删除" << endl;`

}

//end deleteQueue

```cpp
template <class Type>
linkedQueueType<Type>::linkedQueueType()
{
    queueFront = nullptr; // 将头部设置为 nullptr
    queueRear = nullptr; // 将尾部设置为 nullptr
}//end 构造函数
```

当队列对象离开范围时，析构函数会销毁队列；即释放元素占用的内存。析构函数的定义与 `initializeQueue` 相似。此外，实现拷贝构造和赋值运算符的操作与栈相似。这些操作留给你们练习。

## 示例 18-5

以下程序测试队列的不同操作。它使用 `linkedType` 类来实现队列。

```cpp
// 测试队列程序
#include <iostream>
#include "linkedQueue.h"
using namespace std;
int main() {
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
  cout << "Queue Elements: \n";
  while (!queue.isEmpty()) {
    cout << queue.front() << " ";
    queue.deleteQueue();
  }
  cout << endl;
  return 0;
}
```

样例运行：

Queue Elements: 35 27 78 20 29

## 源自 unorderedLinkedList 类的队列

从实现队列操作的函数定义可以看出，队列的链表实现与正向创建的链表实现相似（见第 17 章）。`addQueue` 操作与 `insertFirst` 操作相似。同样，`initializeQueue` 和 `isEmpty` 操作也是类似的。`deleteQueue` 操作可以像之前一样实现。`queueFront` 指针相当于 `first` 指针，`queueRear` 指针相当于 `last`。这种对应关系表明我们可以从 `linkedType` 类派生实现队列的类。注意 `linkedType` 类是一个抽象类，并没有实现所有操作。然而，`unorderedLinkedList` 类派生自 `linkedType` 并提供了 `linkedType` 类的抽象函数。因此，我们可以从 `unorderedLinkedList` 类派生 `linkedQueue` 类。

队列的应用：模拟 | 1277

我们将编写派自 `unorderedLinkedListType` 类的 `linkedQueueType` 类定义留给你们作为练习。请参考本章末尾的编程练习-17。

## 队列的应用：模拟

用一个系统模拟另一个系统的行为的技术称为模拟。例如，物理模拟器包括用于测试车身设计的风洞，以及用于训练航空公司飞行员的飞行模拟器。当对真实系统进行实验成本过高或过于危险时，就会使用模拟技术。你也可以设计计算机模型来研究真实系统的行为。（我们将很快描述一些由计算机建模的真实系统。）

使用计算机模型模拟昂贵或危险环境的行为，通常比使用真实系统成本更低，而且是在在不危及人类生命的情况下获得洞察的好方法。此外，对于难以构建数学模型的复杂系统，计算机模拟 特别有用。对于此类系统，计算机模型可以保持准确性。在计算机模拟中，程序的步骤被用于模拟真实系统的行为。让我们考虑这样一个问题。

当地一家电影院的经理收到了客户关于购买门票等待时间过长的投诉。电影院目前只有一名收银员。另一家电影院正准备在附近开业，经理担心失去客户。经理想雇用额外的收银员，以便客户不需要等待太久买票，但又不想以试验的方式雇用额外的收银员并可能浪费时间和金钱。经理想知道一个模拟电影院行为的程序。

在模拟中，被研究的对象通常表示为数据。对于电影院问题，某些对象是客户和收银员。收银员服务客户，我们需要确定客户的平均等待时间。动作通过编写算法来实现，算法在编程语言中通过函数的帮助实现。因此，函数被用于实现对象上的动作。在 C++ 中，我们可以通过类将数据和对数据的操作组合成单个单元。因此，对象可以表示为类。类的成员变量描述对象的属性，而成员函数描述对该数据的操作。在模拟中，如果我们改变数据的值或修改函数的定义（即修改实现动作的算法），也会产生模拟结果。计算机模拟的主要目标是生成显示现有系统性能的结果，或预测所提议系统的性能。

在电影院问题中，当收银员正在服务客户时，其他客户必须等待。由于客户是按先来顺序服务的，队列是实现 FIFO（先进先出）系统的有效方法，队列是计算机模拟中重要的数据结构。本节检查了队列作为基本数据结构的计算机模拟。这些模拟模拟了被称为队列系统的系统行为，其中对象队列正在等待各种服务器的服务。在其他情况下，队列系统由服务器和等待被服务的对象队列组成。我们每天处理各种队列系统。例如，杂货店和银行都是队列系统。此外，当你向由许多人共享的网络打印机发送打印打印请求时，你的打印请求会进入队列。在你的打印请求之前到达的打印请求通常会在你的请求之前完成。因此，当文档队列正在等待打印时，打印机充当了服务器的角色。

## 设计队列系统

在本节中，我们描述了一种可以用于各种应用的队列系统，例如银行、杂货店、电影院、打印机或几个人正尝试使用相同处理器执行其程序的主机环境。为了描述队列系统，我们使用“服务器”（server）一术称为提供服务的对象。例如，在银行中，出纳员是一个服务器；在杂货店或电影院中，收银员是一个服务器。我们将接收服务的对象称为客户（customer），并将服务时间——服务客户所需的时间称为交易时间（transaction time）。

由于队列系统由服务器和等待对象队列组成，我们将建模一个由服务器列表和一个持有待服务客户的等待队列组成的系统。客户等待下一个可用的服务器。当服务器空闲时，队列头部的客户将移动到该服务器。当服务器空闲且队列头部的客户继续开始交易时。因此，我们必须跟踪与服务器相关的时间。当客户到达时，等待时间被设置为五，并在每个时间单位后递减。当交易时间变为零时，服务器被标记为空闲。因此，需要实现队列系统时间驱动模拟的两个对象是客户和服务器。

接下来，在设计实现模拟的主算法之前，我们设计了类来实现这两个对象中的每一个：客户和服务器。

### 客户

每个客户都拥有一个编号、到达时间、等待时间、交易时间和离开时间。如果我们知道到达时间、等待时间和交易时间，就可以通过这三个时间之和来确定离开时间。让我们把实现客户对象的类称为 `customerType`。由此，`customerType` 类具有成员变量：`customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`，每个类型均为 `int`。在 `customerType` 类型对象上必须执行的基本操作如下：获取客户编号、到达时间和等待时间；将等待时间增加一个时间单位；返回等待时间；返回到达时间；返回交易时间；返回客户编号。以下 `customerType` 类将客户作为抽象数据类型（ADT）实现：

队列的应用：模拟 | 1279

对于本节描述的模拟，我们需要确定客户的平均等待时间。为了计算客户的平均等待时间，我们需要相加客户的等待时间，并除以客户人数。当客户到达时，他或她进入队列尾，客户的等待时间开始。如果队列为空且服务器空闲，客户立即获得服务，该客户的等待时间为零。另一方面，如果客户到达且队列不为空或所有服务器都忙碌，客户必须等待可的服务器，因此客户的等待时间开始。我们使用每个客户的计时器来跟踪等待时间。当客户到达时，计时器被设置为 0，并在每个时间单位后递增。

假设服务器平均需要五分钟服务一个客户。当服务器空闲且等待客户队列不为空时，队列头部的客户将继续开始交易。

# 第 18 章：栈与队列

```cpp
void setCustomerInfo(int customerN = 0, int arrTime = 0,
    int wTime = 0, int tTime = 0);
// 初始化实例变量的函数。
// 根据参数设置实例变量。
// 后置条件：customerNumber = customerN;
//    arrivalTime = arrTime;
//    waitingTime = wTime;
//    transactionTime = tTime;
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
void incrementWaitingTime();
// 将等待时间增加一个时间单位的函数。
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

```cpp
private:
    int customerNumber;
    int arrivalTime;
    int waitingTime;
    int transactionTime;
```

图 18-36 展示了 customerType 的 UML 类图。

| customerType |
| :--- |
| -customerNumber: int |
| -arrivalTime: int |
| -waitingTime: int |
| -transactionTime: int |
| +setCustomerInfo(int = 0, int = 0, int = 0, int = 0): void |
| +getWaitingTime() const: int |
| +setWaitingTime(int): void |
| +incrementWaitingTime() void |
| +getArrivalTime() const: int |
| +getTransactionTime() const: int |
| +getCustomerNumber(int) const: int |
| +setCustomerType(int = 0, int = 0, int = 0, int = 0) |

![](img/d998292a174f7bfd8a26bfbada3d454e_1330_0.png)

`customerType` 类成员函数的定义可以根据其描述很容易地得出。接下来，我们给出 `customerType` 类成员函数的定义。

函数 `setCustomerInfo` 使用参数的值来初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。`setCustomerInfo` 的定义如下：

```cpp
void customerType::setCustomerInfo(int customerN, int arrTime, int wTime, int tTime)
{
    customerNumber = customerN;
    arrivalTime = arrTime;
    waitingTime = wTime;
    transactionTime = tTime;
}
```

构造函数的定义与函数 `setCustomerInfo` 的定义相似。它使用参数的值来初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。为了方便调试，我们使用 `setCustomerInfo` 函数来编写构造函数的定义，其如下所示：

```cpp
customerType::customerType(int customerN, int arrTime, int wTime, int tTime)
{
    setCustomerInfo(customerN, arrTime, wTime, tTime);
}
```

函数 `getWaitingTime` 返回当前的等待时间。`getWaitingTime` 的定义如下：

```cpp
int customerType::getWaitingTime() const
{
    return waitingTime;
}
```

函数 `incrementWaitingTime` 增加 `waitingTime` 的值。它的定义为：

```cpp
void customerType::incrementWaitingTime()
{
    waitingTime++;
}
```

函数 `setWaitingTime`、`getArrivalTime`、`getTransactionTime` 和 `getCustomerNumber` 的定义留给你们练习。

## 服务器

在任何给定时刻，服务器要么正在服务客户，要么处于空闲状态。我们使用字符串来设置服务器的状态。每个服务器都有一个计时器，因为程序可能需要知道哪个客户由哪个服务器服务，所以服务器还存储正在服务的客户的信息。因此，服务器与三个变量关联：状态、transactionTime 和 currentCustomer。在服务器上执行的一些基本操作包括：检查服务器是否空闲；将服务器设置为空闲；将服务器设置为忙碌；设置交易时间（即服务客户所需的时间）；每个时间后返回剩余时间（以确定是否将服务器设置为空闲）；如果服务器忙碌，则将交易时间减少一个单位；以此此类推。以下 `serverType` 类作为抽象数据类型（ADT）实现了服务器：

```cpp
class serverType{
public:
    serverType();
    // 默认构造函数
    // 将实例变量的值设置为
    // 默认值。
    // 后置条件：currentCustomer 由其
    // 默认构造函数初始化；status = "free"; 且
    //
    // 交易时间为
    bool isFree() const;
    void setFree();
    void setBusy();
    void setTransactionTime(int time);
    int getRemainingTime();
    void decreaseTransactionTime();
    void setCurrentCustomer(customerType c);
private:
    string status;
    int transactionTime;
    customerType currentCustomer;
};
```

```cpp
void serverType::setTransactionTime(int t)
{
    transactionTime = t;
}
```

```cpp
void serverType::setTransactionTime()
{
    int time;
    time = currentCustomer.getTransactionTime();
    transactionTime = time;
}
```

```cpp
void serverType::decreaseTransactionTime()
{
    transactionTime--;
}
```

```cpp
void serverType::setCurrentCustomer(customerType c)
{
    currentCustomer = c;
}
```

```cpp
int serverType::getRemainingTime()
{
    return transactionTime;
}
```

```cpp
bool serverType::isFree() const
{
    return (status == "free");
}
```

```cpp
void serverType::setFree()
{
    status = "free";
}
```

```cpp
void serverType::setBusy()
{
    status = "busy";
}
```

```cpp
serverType::serverType()
{
    status = "free";
    transactionTime = 0;
    currentCustomer = customerType();
```
