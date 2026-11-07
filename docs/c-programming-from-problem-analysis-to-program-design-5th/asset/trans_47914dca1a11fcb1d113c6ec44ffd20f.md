

```cpp
//Postcondition: The value of transactionTime is
// returned.

int getCurrentCustomerTransactionTime() const;
//Function to return the transaction time of the
//current customer.
//Postcondition: The value of transactionTime is the
// current customer is returned.

private:
    customerType currentCustomer;
    string status;
    int transactionTime;
};
```

图 19–37 展示了类 `serverType` 的 UML 类图。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1230_0.png)

**图 19–37**  类 `serverType` 的 UML 类图

类 `serverType` 的一些成员函数的定义如下：

```cpp
serverType::serverType()
{
    status = "free";
    transactionTime = 0;
}

bool serverType::isFree() const
{
    return (status == "free");
}

void serverType::setBusy()
{
    status = "busy";
}

void serverType::setFree()
{
    status = "free";
}

void serverType::setTransactionTime(int t)
{
    transactionTime = t;
}

void serverType::setTransactionTime()
{
    int time;

    time = currentCustomer.getTransactionTime();

    transactionTime = time;
}

void serverType::decreaseTransactionTime()
{
    transactionTime--;
}
```

我们将函数 getRemainingTransactionTime、setCurrentCustomer、getCurrentCustomerNumber、getCurrentCustomerArrivalTime、getCurrentCustomerWaitingTime 和 getCurrentCustomerTransactionTime 的定义留作练习。

因为我们正在设计一个可用于多种应用的模拟程序，所以还需要设计另外两个类：一个用于创建和处理服务器列表，另一个用于创建和处理等待顾客队列。接下来的两节将分别描述这两个类。

## 服务器列表

服务器列表是一组服务器。在任意给定时刻，一个服务器要么空闲，要么忙碌。对于位于队列前端的顾客，我们需要在列表中找到一台空闲服务器。如果所有服务器都忙碌，那么该顾客必须等待，直到某台服务器变为空闲。因此，实现服务器列表的类有两个成员变量：一个存储服务器数量，一个维护服务器列表。使用动态数组，根据用户指定的服务器数量，在程序执行期间创建服务器列表。必须在服务器列表上执行的一些操作如下：

- 返回一台空闲服务器的编号；
- 当顾客准备好办理业务且有一台服务器可用时，将该服务器设置为忙碌；
- 当模拟结束时，一些服务器可能仍然忙碌，因此返回忙碌服务器的数量；
- 在每个时间单位之后，将每台忙碌服务器的 transactionTime 减少一个时间单位；
- 并且如果某台服务器的 transactionTime 变为零，则将该服务器设置为空闲。

下面的类 serverListType 将服务器列表实现为 ADT。

```cpp
class serverListType
{
public:
    serverListType(int num = 1);
        //Constructor to initialize a list of servers
        //Postcondition: numOfServers = num
        //              A list of servers, specified by num,
        //              is created and each server is
        //              initialized to "free".

    ~serverListType();
        //Destructor
        //Postcondition: The list of servers is destroyed.

    int getFreeServerID() const;
        //Function to search the list of servers.
        //Postcondition: If a free server is found, returns
        //              its ID; otherwise, returns -1.

    int getNumberOfBusyServers() const;
        //Function to return the number of busy servers.
        //Postcondition: The number of busy servers is returned.

    void setServerBusy(int serverID, customerType cCustomer,
                       int tTime);
        //Function to set a server as busy.
        //Postcondition: The server specified by serverID is set
        //              to "busy", to serve the customer
        //              specified by cCustomer, and the
        //              transaction time is set according to the
        //              parameter tTime.

    void setServerBusy(int serverID, customerType cCustomer);
        //Function to set a server as busy
        //Postcondition: The server specified by serverID is set
        //              to "busy", to serve the customer
        //              specified by cCustomer.

    void updateServers(ostream& outFile);
        //Function to update the status of a server.
        //Postcondition: The transaction time of each busy
        //              server is decremented by one unit. If
        //              the transaction time of a busy server
        //              is reduced to zero, the server is set
        //              to "free". Moreover, if the actual
        //              parameter corresponding to outFile is
        //              cout, a message indicating which customer
        //              has been served is printed on the screen,
        //              together with the customer's departing
        //              time. Otherwise, the output is sent to
        //              a file specified by the user.

private:
    int numOfServers;
    serverType *servers;
};
```

图 19-38 展示了类 serverListType 的 UML 类图。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1233_0.png)

图 19-38  类 serverListType 的 UML 类图

以下是类 serverListType 的成员函数的定义。构造函数和析构函数的定义很直接。

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

函数 `getFreeServerID` 搜索服务器列表。如果找到一台空闲服务器，则返回该服务器的 ID；否则，返回值 −1，表示所有服务器都忙碌。该函数的定义如下：

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

函数 `getNumberOfBusyServers` 搜索服务器列表，确定并返回忙碌服务器的数量。该函数的定义如下：

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

函数 `setServerBusy` 将一台服务器设置为忙碌。该函数被重载。被设置为忙碌的服务器的 serverID 作为参数传递给该函数。一个函数根据参数 `tTime` 设置服务器的交易时间；另一个函数使用对象 `cCustomer` 中存储的交易时间进行设置。之后需要该交易时间来确定平均等待时间。这些函数的定义如下：

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

函数 updateServers 的定义非常直接。它从第一台服务器开始，在服务器列表中搜索忙碌服务器。当找到一台忙碌服务器时，其 transactionTime 减 1。如果 transactionTime 减到零，则将该服务器设置为空闲。如果一台忙碌服务器的 transactionTime 减到零，那么该服务器正在服务的顾客的交易就完成了。如果 outFile 对应的实参是 cout，则在屏幕上打印一条消息，指示哪位顾客已被服务，并同时打印该顾客的离开时间。否则，输出被发送到用户指定的文件。该函数的定义如下：

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
                        << "\n     departed at time unit "
                        << servers[i].
                           getCurrentCustomerArrivalTime()
                           + servers[i].
                           getCurrentCustomerWaitingTime()
                           + servers[i].
                           getCurrentCustomerTransactionTime()
                        << endl;
                servers[i].setFree();
            }
        }
}
```

