
```cpp
void setCustomerInfo(int customerN = 0, int arrvTime = 0,
                     int wTime = 0, int tTime = 0);
    //Function to initialize this instance variables.
    //Instance variables are set according to the parameters.
    //Postcondition: customerNumber = customerN;
    //                arrivalTime = arrvTime;
    //                waitingTime = wTime;
    //                transactionTime = tTime;

int getWaitingTime() const;
    //Function to return the waiting time of a customer.
    //Postcondition: The value of waitingTime is returned.

void setWaitingTime(int time);
    //Function to set the waiting time of a customer.
    //Postcondition: waitingTime = time;

void incrementWaitingTime();
    //Function to increment the waiting time by one time unit.
    //Postcondition: waitingTime++;

int getArrivalTime() const;
    //Function to return the arrival time of a customer.
    //Postcondition: The value of arrivalTime is returned.

int getTransactionTime() const;
    //Function to return the transaction time of a customer.
    //Postcondition: The value of transactionTime is returned.

int getCustomerNumber() const;
    //Function to return the customer number.
    //Postcondition: The value of customerNumber is returned.

private:
    int customerNumber;
    int arrivalTime;
    int waitingTime;
    int transactionTime;
};
```

图 17–36 展示了类 `customerType` 的 UML 类图。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1287_0.png)

**图 17-36** 类 `customerType` 的 UML 类图

类 `customerType` 的成员函数定义可轻松地由其描述得出。接下来，我们给出类 `customerType` 的成员函数的定义。

函数 `setCustomerInfo` 使用参数值初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。`setCustomerInfo` 的定义为：

```cpp
void customerType::setCustomerInfo(int customerN, int arrvTime,
                                   int wTime, int tTime)
{
    customerNumber = customerN;
    arrivalTime = arrvTime;
    waitingTime = wTime;
    transactionTime = tTime;
}
```

构造函数的定义与函数 `setCustomerInfo` 的定义类似。它使用参数值初始化 `customerNumber`、`arrivalTime`、`waitingTime` 和 `transactionTime`。为使调试更容易，我们使用函数 `setCustomerInfo` 来编写构造函数的定义，如下所示：

```cpp
customerType::customerType(int customerN, int arrvTime,
                           int wTime, int tTime)
{
    setCustomerInfo(customerN, arrvTime, wTime, tTime);
}
```

函数 getWaitingTime 返回当前等待时间。函数 getWaitingTime 的定义为：

```cpp
int customerType::getWaitingTime() const
{
    return waitingTime;
}
```

函数 incrementWaitingTime 将 waitingTime 的值递增。其定义为：

```cpp
void customerType::incrementWaitingTime()
{
    waitingTime++;
}
```

函数 setWaitingTime、getArrivalTime、getTransactionTime 和 getCustomerNumber 的定义留作练习。

## 服务器

在任意给定时间单位，服务器要么正忙于服务顾客，要么空闲。我们使用一个字符串变量来设置服务器的状态。每个服务器都有一个计时器；并且，由于程序可能需要知道哪个顾客由哪个服务器服务，服务器还存储正在服务的顾客的信息。因此，一个服务器关联三个成员变量：status、transactionTime 和 currentCustomer。必须对服务器执行的一些基本操作如下：检查服务器是否空闲；将服务器设置为空闲；将服务器设置为忙；设置交易时间（即服务顾客需要多长时间）；返回剩余交易时间（以判断是否应将服务器设置为空闲）；在每个时间单位之后，如果服务器忙，则将交易时间减少一个时间单位；等等。下面的类 serverType 将服务器实现为 ADT：

```cpp
class serverType
{
public:
    serverType();
    //Default constructor
    //Sets the values of the instance variables to their default
    //values.
    //Postcondition: currentCustomer is initialized by its
    //               default constructor; status = "free"; and
    //               the transaction time is initialized to 0.

    bool isFree() const;
    //Function to determine if the server is free.
    //Postcondition: Returns true if the server is free,
    //               otherwise returns false.

    void setBusy();
    //Function to set the status of the server to busy.
    //Postcondition: status = "busy";

    void setFree();
    //Function to set the status of the server to "free".
    //Postcondition: status = "free";

    void setTransactionTime(int t);
    //Function to set the transaction time according to the
    //parameter t.
    //Postcondition: transactionTime = t;

    void setTransactionTime();
    //Function to set the transaction time according to
    //the transaction time of the current customer.
    //Postcondition:
    //    transactionTime = currentCustomer.transactionTime;

    int getRemainingTransactionTime() const;
    //Function to return the remaining transaction time.
    //Postcondition: The value of transactionTime is returned.

    void decreaseTransactionTime();
    //Function to decrease the transactionTime by one unit.
    //Postcondition: transactionTime--;

    void setCurrentCustomer(customerType cCustomer);
    //Function to set the info of the current customer
    //according to the parameter cCustomer.
    //Postcondition: currentCustomer = cCustomer;

    int getCurrentCustomerNumber() const;
    //Function to return the customer number of the current
    //customer.
    //Postcondition: The value of customerNumber of the
    //                current customer is returned.

    int getCurrentCustomerArrivalTime() const;
    //Function to return the arrival time of the current
    //customer.
    //Postcondition: The value of arrivalTime of the current
    //                customer is returned.

    int getCurrentCustomerWaitingTime() const;
    //Function to return the current waiting time of the
    //current customer.
    //Postcondition: The value of waitingTime is
    //                returned.

    int getCurrentCustomerTransactionTime() const;
    //Function to return the transaction time of the
    //current customer.
    //Postcondition: The value of transactionTime of the
    //                current customer is returned.

private:
    customerType currentCustomer;
    string status;
    int transactionTime;
};
```

图 17–37 展示了类 `serverType` 的 UML 类图。

![](img/d0be7fc6d804b63484835c6c8bc67a07_1290_0.png)

**图 17-37** 类 `serverType` 的 UML 类图

类 `serverType` 的部分成员函数的定义为：

```cpp
serverType::serverType()
{
    status = "free";
    transactionTime = 0;
}
```

```cpp
bool serverType::isFree() const
{
    return (status == "free");
}
```

```cpp
void serverType::setBusy()
{
    status = "busy";
}
```

```cpp
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

函数 `getRemainingTransactionTime`、`setCurrentCustomer`、`getCurrentCustomerNumber`、`getCurrentCustomerArrivalTime`、`getCurrentCustomerWaitingTime` 和 `getCurrentCustomerTransactionTime` 的定义留作练习。

因为我们正在设计一个可用于多种应用的模拟程序，所以还需要设计另外两个类：一个用于创建和处理服务器列表，另一个用于创建和处理等待顾客队列。接下来的两节分别描述这两个类。

## 服务器列表

服务器列表是一组服务器。在任意给定时间，一个服务器要么空闲，要么忙。对于队列前端的顾客，我们需要在列表中找到一台空闲的服务器。如果所有服务器都忙，那么该顾客必须等到其中一台服务器变为空闲。因此，实现服务器列表的类有两个成员变量：一个存储服务器数量，另一个维护服务器列表。使用动态数组，根据用户指定的服务器数量，在程序执行期间创建服务器列表。必须对服务器列表执行的一些操作如下：返回空闲服务器的服务器编号；当顾客准备办理业务且服务器可用时，将服务器设置为忙；当模拟结束时，一些服务器可能仍处于忙状态，因此返回忙服务器的数量；在每个时间单位之后，将每个忙服务器的 `transactionTime` 减少一个时间单位；如果某台服务器的 `transactionTime` 变为零，则将该服务器设置为空闲。下面的类 `serverListType` 将服务器列表实现为 ADT：
