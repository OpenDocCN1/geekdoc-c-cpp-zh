
## 等待顾客队列

当顾客到达时，他或她走到队列末尾。当有服务器空闲时，位于队列前端的顾客离开队列去进行交易。每经过一个时间单位，队列中每个顾客的等待时间就增加 1。本章设计的 ADT `queueType` 具有实现队列所需的全部操作，唯独缺少将队列中每个顾客的等待时间增加一个时间单位的操作。我们将从类 `queueType` 派生一个类 `waitingCustomerQueueType`，并添加额外操作来实现顾客队列。类 `waitingCustomerQueueType` 的定义如下：

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

> **注意** 请注意，类 `waitingCustomerQueueType` 派生自类 `queueType`，后者用数组实现队列。你也可以从类 `linkedQueueType` 派生它，后者用链表实现队列。我们将细节留作练习。

下面给出成员函数的定义。构造函数的定义如下：

```cpp
waitingCustomerQueueType::waitingCustomerQueueType(int size)
                                :queueType<customerType>(size)
{
}
```

函数 `updateWaitingQueue` 将队列中每个顾客的等待时间增加一个时间单位。类 `waitingCustomerQueueType` 派生自类 `queueType`。由于 `queueType` 的成员变量是私有的，函数 `updateWaitingQueue` 不能直接访问队列中的元素。访问队列元素的唯一方式是使用 `deleteQueue` 操作。在增加等待时间后，可以使用 `addQueue` 操作将该元素放回队列。

addQueue 操作将元素插入队列末尾。如果我们对队列中的每个元素执行 deleteQueue 操作，随后执行 addQueue 操作，那么最终队首元素会再次成为队首元素。既然每个 deleteQueue 操作之后都跟着一个 addQueue 操作，我们如何确定队列中的所有元素都已处理完毕？我们不能对队列使用 isEmptyQueue 或 isFullQueue 操作，因为队列永远不会为空或为满。

这个问题的一种解决方案是创建一个临时队列。将原队列中的每个元素移除、处理，并插入临时队列。当原队列变为空时，队列中的所有元素都已处理完毕。然后我们可以将元素从临时队列复制回原队列。然而，这种解决方案需要使用额外的内存空间，这可能相当可观。此外，如果队列很大，还需要额外的计算机时间将元素从临时队列复制回原队列。让我们研究另一种解决方案。

在第二种解决方案中，在开始更新队列元素之前，我们可以插入一个等待时间例如为 -1 的虚拟顾客。在更新过程中，当我们到达等待时间为 -1 的顾客时，我们可以停止更新过程，而不处理等待时间为 -1 的顾客。如果我们不处理等待时间为 -1 的顾客，该顾客就会从队列中移除，并且在处理完队列中的所有元素之后，队列将不包含额外元素。这种解决方案不需要我们创建临时队列，因此我们不需要额外的计算机时间将元素复制回原队列。我们将使用这种解决方案来更新队列。因此，函数 updateWaitingQueue 的定义如下：

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

## 主程序

要运行模拟，我们首先需要获取以下信息：

- 模拟应运行的时间单位数。假设每个时间单位为一分钟。
- 服务器数量。
- 服务一个顾客所需的时间——即交易时间。
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

当一个服务器变为空闲且顾客队列非空时，我们可以将队首顾客移到空闲服务器上接受服务。此外，当顾客开始交易时，等待时间结束。该顾客的等待时间会加到总等待时间中。开始交易的一般算法（假设 serverID 表示空闲服务器的 ID）如下：

- 1. 从队列前端移除该顾客。
  
  ```cpp
  customer = customerQueue.front();
  customerQueue.deleteQueue();
  ```
  
- 2. 将当前顾客的等待时间加到先前的总等待时间上，以更新总等待时间。
  
  ```cpp
  totalWait = totalWait + customer.getWaitingTime();
  ```
  
- 3. 设置空闲服务器开始交易。
  
  ```cpp
  serverList.setServerBusy(serverID, customer, transTime);
  ```

要运行模拟，我们需要知道在给定时间单位内到达的顾客数量，以及服务该顾客需要多长时间。我们使用统计学中的泊松分布，它表明在给定时间内发生 γ 个事件的概率由以下公式给出：

$$P(\gamma)=\frac{\lambda^\gamma e^{-\lambda}}{\gamma!},\ \gamma=0,1,2,\ldots$$

其中 λ 是在该时间发生 γ 个事件的期望值。假设平均每四分钟到达一位顾客。在这四分钟时间段内，顾客可以在四分钟中的任意一分钟到达。假设四分钟中每一分钟的可能性相等，因此顾客在四分钟中的每一分钟到达的期望值为 1 / 4 = 0.25。接下来，我们需要确定顾客是否真的在给定分钟到达。

现在，$P(0)=e^{-\lambda}$ 是在给定时间不发生任何事件的概率。泊松分布的基本假设之一是，在短时间间隔内发生多个结果的概率可以忽略不计。为简单起见，我们假设在给定时间单位内只有一位顾客到达。因此，我们使用 $e^{-\lambda}$ 作为截止点，来判断顾客是否在给定时间单位到达。假设平均每四分钟到达一位顾客。那么，$\lambda=0.25$。我们可以使用算法生成一个 0 到 1 之间的数。如果生成的数值 > $e^{-0.25}$，我们可以假设顾客在该特定时间单位到达。例如，假设 $rNum$ 是一个满足 $0 \le rNum \le 1$ 的随机数。如果 $rNum > e^{-0.25}$，则顾客在给定时间单位到达。

我们现在描述函数 runSimulation 来实现模拟。假设我们运行模拟 100 个时间单位，顾客在时间单位 93、96 和 100 到达。平均交易时间为五分钟——即五个时间单位。为简单起见，假设我们只有一个服务器，并且该服务器在时间单位 97 变为空闲，而且在时间单位 93 之前到达的所有顾客都已被服务。当服务器在时间单位 97 变为空闲时，在时间单位 93 到达的顾客开始交易。由于在时间单位 93 到达的顾客的交易从时间单位 97 开始，并且完成一次交易需要五分钟，所以当模拟循环结束时，在时间单位 93 到达的顾客仍在服务器上。此外，在时间单位 96 和 100 到达的顾客在队列中。为简单起见，我们假设当模拟循环结束时，服务器上的顾客被视为已服务。该函数的一般算法如下：

- 1. 声明并初始化变量，例如模拟参数、顾客编号、时钟、总等待时间和平均等待时间、已到达顾客数、已服务顾客数、仍在等待队列中的顾客数、仍在服务器上的顾客数、waitingCustomersQueue 以及服务器列表。

