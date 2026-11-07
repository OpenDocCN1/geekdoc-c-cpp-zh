
函数 getFreeServerID 搜索服务器列表。如果找到空闲服务器，则返回该服务器的 ID；否则返回值 −1，表示所有服务器都忙。该函数的定义如下：

```cpp
int serverListType::getFreeServerID() const
{
    int serverID = -1;

    int i;

    for (i = 0; i < numOfServers; i++)
        if (servers[i].isFree())
        {
            serverID = i;
            break;
        }

    return serverID;
}
```

函数 getNumberOfBusyServers 搜索服务器列表，并确定和返回忙服务器的数量。该函数的定义如下：

```cpp
int serverListType::getNumberOfBusyServers() const
{
    int busyServers = 0;

    int i;

    for (i = 0; i < numOfServers; i++)
        if (!servers[i].isFree())
            busyServers++;

    return busyServers;
}
```

函数 setServerBusy 将一台服务器设置为忙。该函数是重载的。被设置为忙的服务器的 serverID 作为参数传递给该函数。一个函数根据参数 tTime 设置服务器的服务时间；另一个函数使用对象 cCustomer 中存储的服务时间来设置它。之后需要该服务时间来确定平均等待时间。这些函数的定义如下：

```cpp
void serverListType::setServerBusy(int serverID,
                                    customerType cCustomer,
                                    int tTime)
{
    servers[serverID].setBusy();
    servers[serverID].setTransactionTime(tTime);
    servers[serverID].setCurrentCustomer(cCustomer);
}

void serverListType::setServerBusy(int serverID,
                                    customerType cCustomer)
{
    int time;

    time = cCustomer.getTransactionTime();

    servers[serverID].setBusy();
    servers[serverID].setTransactionTime(time);
    servers[serverID].setCurrentCustomer(cCustomer);
}
```

函数 updateServers 的定义非常直接。它从第一台服务器开始，在服务器列表中搜索忙服务器。当找到一台忙服务器时，其 transactionTime 减 1。如果 transactionTime 减到零，则将服务器设置为空闲。如果一台忙服务器的 transactionTime 减到零，那么该服务器正在服务的顾客的业务就完成了。如果 outFile 对应的实参是 cout，则在屏幕上打印一条消息，指明哪位顾客已被服务，以及该顾客的离开时间。否则，输出被发送到用户指定的文件。该函数的定义如下：

```cpp
void serverListType::updateServers(ostream& outFile)
{
    int i;

    for (i = 0; i < numOfServers; i++)
        if (!servers[i].isFree())
        {
            servers[i].decreaseTransactionTime();

            if (servers[i].getRemainingTransactionTime() == 0)
            {
                outFile << "From server number " << (i + 1)
                        << " customer number "
                        << servers[i].getCurrentCustomerNumber()
                        << "\n        departed at time unit "
                        << servers[i].getCurrentCustomerArrivalTime()
                        + servers[i].getCurrentCustomerWaitingTime()
                        + servers[i].getCurrentCustomerTransactionTime()
                        << endl;
                servers[i].setFree();
            }
        }
}
```

## 等待顾客队列

当顾客到达时，他或她走到队列末尾。当一台服务器变为可用时，队列前端的顾客离开去办理业务。每经过一个时间单位，队列中每位顾客的等待时间就增加 1。本章设计的抽象数据类型 queueType 具有实现队列所需的所有操作，除了将队列中每位顾客的等待时间增加一个时间单位的操作。我们将从类 queueType 派生一个类 waitingCustomerQueueType，并添加额外的操作来实现顾客队列。类 waitingCustomerQueueType 的定义如下：

```cpp
class waitingCustomerQueueType: public queueType<customerType>
{
public:
    waitingCustomerQueueType(int size = 100);
    //Constructor
    //Postcondition: The queue is initialized according to
    //              the parameter size. The value of size
    //              is passed to the constructor of queueType.

    void updateWaitingQueue();
    //Function to increment the waiting time of each
    //customer in the queue by one time unit.
};
```

> **注意** 类 waitingCustomerQueueType 派生自类 queueType，后者用数组实现队列。你也可以从类 linkedQueueType 派生它，后者用链表实现队列。我们将细节留作练习。

下面给出成员函数的定义。构造函数的定义如下：

```cpp
waitingCustomerQueueType::waitingCustomerQueueType(int size)
                                  : queueType<customerType>(size)
{
}
```

函数 updateWaitingQueue 将队列中每位顾客的等待时间增加一个时间单位。类 waitingCustomerQueueType 派生自类 queueType。由于 queueType 的成员变量是私有的，函数 updateWaitingQueue 不能直接访问队列元素。访问队列元素的唯一方式是使用 deleteQueue 操作。增加等待时间后，可以使用 addQueue 操作将该元素放回队列。

## 主程序

要运行模拟，我们首先需要获取以下信息：

- 模拟应运行的时间单位数。假设每个时间单位为一分钟。
- 服务器数量。
- 服务一位顾客所需的时间——即服务时间。
- 顾客到达之间的近似时间。

这些信息称为模拟参数。通过改变这些参数的值，我们可以观察系统性能的变化。我们可以编写一个函数 setSimulationParameters，提示用户指定这些值。该函数的定义如下：

```cpp
void setSimulationParameters(int& sTime, int& numOfServers,
                             int& transTime,
                             int& tBetweenCArrival)
{
    cout << "Enter the simulation time: ";
    cin >> sTime;
    cout << endl;

    cout << "Enter the number of servers: ";
    cin >> numOfServers;
    cout << endl;

    cout << "Enter the transaction time: ";
    cin >> transTime;
    cout << endl;

    cout << "Enter the time between customer arrivals: ";
    cin >> tBetweenCArrival;
    cout << endl;
}
```

当一台服务器变为空闲且顾客队列非空时，我们可以将队列前端的顾客移到空闲服务器上接受服务。此外，当顾客开始服务时，等待时间结束。该顾客的等待时间被加到总等待时间中。开始服务的一般算法（假设 serverID 表示空闲服务器的 ID）是：

1. 从队列前端移除该顾客。

   ```cpp
   customer = customerQueue.front();
   customerQueue.deleteQueue();
   ```

2. 通过将当前顾客的等待时间加到之前的总等待时间上，更新总等待时间。

   ```cpp
   totalWait = totalWait + customer.getWaitingTime();
   ```

3. 设置空闲服务器开始服务。

   ```cpp
   serverList.setServerBusy(serverID, customer, transTime);
   ```

要运行模拟，我们需要知道在给定时间单位内到达的顾客数量，以及服务该顾客需要多长时间。我们使用统计学中的泊松分布，它表明在给定时间发生 y 个事件的概率由以下公式给出：

$$P(y)=\frac{\lambda^y e^{-\lambda}}{y!},\quad y=0,1,2,\ldots,$$

其中 λ 是在该时间发生 y 个事件的期望值。假设平均每四分钟到达一位顾客。在这四分钟时间段内，顾客可能在这四分钟中的任意一分钟到达。假设这四分钟中每一分钟的可能性相同，因此顾客在这四分钟中每一分钟到达的期望值是 1/4 = .25。接下来，我们需要确定顾客是否真的在给定分钟到达。

现在，P(0) = e^{-λ} 是在给定时间没有事件发生的概率。泊松分布的基本假设之一是，在短时间间隔内发生多于一个结果的概率可以忽略。为简单起见，我们假设在给定时间单位内只有一位顾客到达。因此，我们使用 e^{-λ} 作为阈值来确定顾客是否在给定时间单位到达。假设平均每四分钟到达一位顾客。那么，λ = 0.25。我们可以使用一种算法生成一个 0 到 1 之间的数。如果生成的数的值 > e^{-0.25}，我们可以假设顾客在特定时间单位到达。例如，假设 rNum 是一个随机数，满足 0 ≤ rNum ≤ 1。如果 rNum > e^{-0.25}，则顾客在给定时间单位到达。

现在我们描述用于实现模拟的函数 runSimulation。假设我们运行模拟 100 个时间单位，顾客在时间单位 93、96 和 100 到达。平均服务时间为五分钟——即五个时间单位。为简单起见，假设我们只有一台服务器，并且该服务器在时间单位 97 变为空闲，而且在时间单位 93 之前到达的所有顾客都已被服务。当服务器在时间单位 97 变为空闲时，在时间单位 93 到达的顾客开始服务。因为在时间单位 93 到达的顾客的服务从时间单位 97 开始，而完成一次服务需要五分钟，所以当模拟循环结束时，在时间单位 93 到达的顾客仍在服务器上接受服务。此外，在时间单位 96 和 100 到达的顾客在队列中。为简单起见，我们假设当模拟循环结束时，位于服务器上的顾客被视为已服务。该函数的一般算法是：

1. 声明并初始化变量，例如模拟参数、顾客编号、时钟、总等待时间和平均等待时间、已到达顾客数、已服务顾客数、留在等待队列中的顾客数、仍在服务器上的顾客数、waitingCustomersQueue 以及服务器列表。
