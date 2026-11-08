
```cpp
// server is decremented by one unit. If
// the transaction time of a busy server
// is reduced to zero, the server is set
// to "free". Moreover, if the actual
// parameter corresponding to outFile is
// cout, a message indicating which customer
// has been served is printed on the screen,
// together with the customer's departing
// time. Otherwise, the output is sent to
// a file specified by the user.

private:
    int numOfServers;
    serverType * servers;
};
```

图17-38展示了类`serverListType`的UML类图。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1244_0.png)

**图17-38** 类`serverListType`的UML类图

以下是类`serverListType`的成员函数定义。构造函数和析构函数的定义很直接。

```cpp
serverListType::serverListType(int num)
{
    numOfServers = num;
    servers = new serverType[num];
}

serverListType::~serverListType()
{
    delete [] servers;
}
```

函数getFreeServerID搜索服务器列表。如果找到空闲服务器，则返回该服务器的ID；否则返回-1，表示所有服务器都忙。该函数的定义如下：

```
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

函数getNumberOfBusyServers搜索服务器列表，确定并返回忙服务器的数量。该函数的定义如下：

```
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

函数setServerBusy将服务器设置为忙。该函数被重载。被设置为忙的服务器的serverID作为参数传递给该函数。一个函数根据参数tTime设置服务器的事务时间；另一个函数使用对象cCustomer中存储的事务时间来设置。之后需要事务时间来确定平均等待时间。这些函数的定义如下：

```
void serverListType::setServerBusy(int serverID,
                                   customerType cCustomer,
                                   int tTime)
{
    servers[serverID].setBusy();
    servers[serverID].setTransactionTime(tTime);
    servers[serverID].setCurrentCustomer(cCustomer);
}
```

```
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

函数updateServers的定义相当直接。从第一个服务器开始，它在服务器列表中搜索忙服务器。当找到忙服务器时，其事务时间减1。如果transactionTime减到零，服务器被设置为空闲。如果忙服务器的transactionTime减到零，那么该服务器正在服务的顾客的事务就完成了。如果对应outFile的参数是cout，则在屏幕上打印一条消息，指示哪个顾客已被服务，并连同该顾客的离开时间一起输出。否则，输出发送到用户指定的文件。该函数的定义如下：

```
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
                        << "\n departed at time unit "
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

当顾客到达时，他或她走到队列末尾。当服务器变得可用时，队首的顾客离开去进行事务。每经过一个时间单位，队列中每个顾客的等待时间增加1。本章设计的ADT queueType具有实现队列所需的所有操作，除了将队列中每个顾客的等待时间增加一个时间单位的操作。我们将从类queueType派生类waitingCustomerQueueType，并添加额外操作来实现顾客队列。类waitingCustomerQueueType的定义如下：

```cpp
class waitingCustomerQueueType: public queueType<customerType>
{
public:
    waitingCustomerQueueType(int size = 100);
    //Constructor
    //Postcondition: The queue is initialized according to
    //               the parameter size. The value of size
    //               is passed to the constructor of queueType.

    void updateWaitingQueue();
    //Function to increment the waiting time of each
    //customer in the queue by one time unit.
};
```

> 注意，类waitingCustomerQueueType派生自类queueType，后者用数组实现队列。你也可以从类linkedQueueType派生它，后者用链表实现队列。我们将细节留作练习。

下面给出成员函数的定义。构造函数的定义如下：

```cpp
waitingCustomerQueueType::waitingCustomerQueueType(int size)
    :queueType<customerType>(size)
{
}
```

函数updateWaitingQueue将队列中每个顾客的等待时间增加一个时间单位。类waitingCustomerQueueType派生自类queueType。由于queueType的成员变量是私有的，函数updateWaitingQueue不能直接访问队列元素。访问队列元素的唯一方式是使用deleteQueue操作。增加等待时间后，可以使用addQueue操作将该元素放回队列。

addQueue操作将元素插入队列末尾。如果对队列中的每个元素执行deleteQueue操作，随后执行addQueue操作，那么最终队首元素会再次成为队首元素。既然每个deleteQueue操作之后都跟着一个addQueue操作，我们如何确定队列中的所有元素都已处理完毕？我们不能对队列使用isEmptyQueue或isFullQueue操作，因为队列永远不会为空或为满。

这个问题的一种解决方案是创建一个临时队列。原队列的每个元素都被移除、处理并插入临时队列。当原队列变为空时，队列中的所有元素都已处理完毕。然后我们可以将元素从临时队列复制回原队列。然而，这种解决方案要求我们使用额外的内存空间，这可能相当可观。此外，如果队列很大，将元素从临时队列复制回原队列需要额外的计算机时间。让我们研究另一种解决方案。

在第二种解决方案中，在开始更新队列元素之前，我们可以插入一个等待时间例如为-1的哑顾客。在更新过程中，当遇到等待时间为-1的顾客时，我们可以停止更新过程，而不处理等待时间为-1的顾客。如果我们不处理等待时间为-1的顾客，该顾客会从队列中移除，并且在处理完队列中的所有元素之后，队列将不包含额外元素。这种解决方案不需要我们创建临时队列，因此不需要额外的计算机时间将元素复制回原队列。我们将使用这种解决方案来更新队列。因此，函数updateWaitingQueue的定义是：

```cpp
void waitingCustomerQueueType::updateWaitingQueue()
{
    customerType cust;

    cust.setWaitingTime(-1);
    int wTime = 0;

    addQueue(cust);

    while (wTime != -1)
    {
        cust = front();
        deleteQueue();

        wTime = cust.getWaitingTime();
        if (wTime == -1)
            break;
        cust.incrementWaitingTime();
        addQueue(cust);
    }
}
```

