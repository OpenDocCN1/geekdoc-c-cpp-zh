
每个客户的等待时间，然后将总和除以已到达的客户数。当客户到达时，他或她走到队列末尾，该客户的等待时间开始。如果队列为空且服务器空闲，则立即为该客户服务，因此该客户的等待时间为零。另一方面，如果客户到达且队列非空或所有服务器都忙，则该客户必须等待下一个可用的服务器，因此该客户的等待时间开始。我们可以通过为每个客户使用计时器来跟踪客户的等待时间。当客户到达时，计时器设置为 0，并在每个时间单位后递增。

假设平均而言，服务器服务一个客户需要五分钟。当服务器变为空闲且等待客户队列非空时，队列最前面的客户继续开始事务。因此，我们必须跟踪客户与服务器在一起的时间。当客户到达服务器时，事务时间设置为五，并在每个时间单位后递减。当事务时间变为零时，服务器被标记为空闲。因此，实现排队系统的时间驱动计算机模拟所需的两个对象是客户和服务器。

接下来，在设计实现模拟的主算法之前，我们设计类来实现这两个对象中的每一个：*客户*和*服务器*。

## 客户

每个客户都有一个客户编号、到达时间、等待时间、事务时间和离开时间。如果我们知道到达时间、等待时间和事务时间，就可以通过将这三个时间相加来确定离开时间。我们将实现客户对象的类称为 *customerType*。由此可知，类 **customerType** 有四个成员变量：**customerNumber**、**arrivalTime**、**waitingTime** 和 **transactionTime**，每个变量的数据类型均为 **int**。必须对 **customerType** 类型的对象执行的基本操作如下：设置客户的编号、到达时间和等待时间；将等待时间增加一个时间单位；返回等待时间；返回到达时间；返回事务时间；以及返回客户编号。以下类 **customerType** 将客户实现为 ADT：

```cpp
class customerType
{
public:
    customerType(int cN = 0, int arrvTime = 0, int wTime = 0,
                 int tTime = 0);

    //Constructor to initialize the instance variables
    //according to the parameters
    //If no value is specified in the object declaration,
    //the default values are assigned
    //Postcondition: customerNumber = cN;
    //               arrivalTime = arrvTime;
    //               waitingTime = wTime;
    //               transactionTime = tTime

    void setCustomerInfo(int customerN = 0, int inTime = 0,
                         int wTime = 0, int tTime = 0);
    //Function to initialize the instance variables.
    //Instance variables are set according to the parameters.
    //Postcondition: customerNumber = customerN;
    //              arrivalTime = arrvTime;
    //              waitingTime = wTime;
    //              transactionTime = tTime;

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

图 17-36 显示了类 `customerType` 的 UML 类图。

函数 `getWaitingTime` 返回当前等待时间。函数 `getWaitingTime` 的定义如下：

```cpp
int customerType::getWaitingTime() const
{
    return waitingTime;
}
```

函数 `incrementWaitingTime` 递增 `waitingTime` 的值。其定义是

```cpp
void customerType::incrementWaitingTime()
{
    waitingTime++;
}
```

函数 `setWaitingTime`、`getArrivalTime`、`getTransactionTime` 和 `getCustomerNumber` 的定义留作练习。

## 服务器

在任意给定时间单位，服务器要么正忙于服务客户，要么空闲。我们使用一个 `string` 变量来设置服务器的状态。每个服务器都有一个计时器，并且由于程序可能需要知道哪个客户由哪个服务器服务，服务器还存储正在服务的客户的信息。因此，有三个成员变量与服务器关联：状态、transactionTime 和 currentCustomer。必须对服务器执行的一些基本操作如下：检查服务器是否空闲；将服务器设置为空闲；将服务器设置为忙；设置事务时间（即服务该客户需要多长时间）；返回剩余事务时间（以确定是否应将服务器设置为空闲）；如果每个时间单位后服务器仍忙，则将事务时间递减一个时间单位；等等。以下类 serverType 将服务器实现为 ADT：

```cpp
class serverType
{
public:
    serverType();
    //Default constructor
    //Sets the values of the instance variables to their
    //    default values.
    //Postcondition: currentCustomer is initialized by its
    //                default constructor; status == "free"; and
    //                the transaction time is initialized to 0.

    bool isFree() const;
    //Function to determine if the server is free.
    //Postcondition: Returns true if the server is free,
    //              otherwise returns false.

    void setBusy();
    //Function to set the status of the server to busy.
    //Postcondition: status = "busy";

    void setFree();
    //Function to set the status of the server to "free".
    //Postcondition: status = "free";

    void setTransactionTime(int t);
    //Function to set the transaction time according to
    //the parameter t.
    //Postcondition: transactionTime = t;

    void setTransactionTime();
    //Function to set the transaction time according to
    //the transaction time of the current customer.
    //Postcondition:
    //              transactionTime = currentCustomer.transactionTime;

    int getRemainingTransactionTime() const;
    //Function to return the remaining transaction time.
    //Postcondition: The value of transactionTime is returned.

    void decreaseTransactionTime();
    //Function to decrease the transactionTime by 1 unit.
    //Postcondition: transactionTime--;

    void setCurrentCustomer(customerType cCustomer);
    //Function to set the info of the current customer
    //according to the parameter cCustomer.
    //Postcondition: currentCustomer = cCustomer;

    int getCurrentCustomerNumber() const;
    //Function to return the customer number of the current
    //customer.
    //Postcondition: The value of customerNumber of the
    //              current customer is returned.

    int getCurrentCustomerArrivalTime() const;
    //Function to return the arrival time of the current
    //customer.
    //Postcondition: The value of arrivalTime of the current
    //              customer is returned.

    int getCurrentCustomerWaitingTime() const;
    //Function to return the current waiting time of the
    //current customer.
    //Postcondition: The value of transactionTime is
    //              returned.

    int getCurrentCustomerTransactionTime() const;
    //Function to return the transaction time of the
    //current customer.
    //Postcondition: The value of transactionTime of the
    //              current customer is returned.
```
