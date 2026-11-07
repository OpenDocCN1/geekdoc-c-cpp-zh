
第4行的语句执行后，第2行的循环条件被重新计算。因为 `current` 不是 `nullptr`，循环条件的计算结果为 `true`，所以第3行和第4行的语句执行（见图 17-21）。

![](img/b217c421655b51e7494cf3b89bb5432d_1276_0.png)

**图 17-21** 语句 `stack.push(current);` 和 `current = current->link;` 执行后的列表和栈

第4行的语句执行后，第2行的循环条件再次被计算。因为 `current` 不是 `nullptr`，循环条件的计算结果为 `true`，所以第3行和第4行的语句执行（见图 17-22）。

![](img/b217c421655b51e7494cf3b89bb5432d_1276_1.png)

**图 17-22** 语句 `stack.push(current);` 和 `current = current->link;` 执行后的列表和栈

第4行的语句执行后，第2行的循环条件再次被计算。因为 `current` 是 `nullptr`，循环条件的计算结果为 `false`，第2行的 `while` 循环终止。从图 17-22 可知，指向每个节点的指针

第8行的语句输出 `current->info`，其值为 10。接下来，第5行的循环条件被计算。因为循环条件的计算结果为 true，第6、7、8行的语句执行。第6行和第7行的语句执行后，结果如图 17-25 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1278_0.png)

第8行的语句输出 `current->info`，其值为 5。接下来，第5行的循环条件被计算。因为循环条件的计算结果为 false，while 循环终止。第5行的 while 循环产生以下输出：

15 10 5

## 队列

本节讨论另一种重要的数据结构，称为**队列**。计算机科学中的队列概念与日常生活中的队列概念相同。银行或杂货店里有顾客队列，收费站前有等待通过的汽车队列。类似地，因为计算机发送打印请求的速度可以比打印机打印的速度快，所以经常有文档队列在打印机前等待打印。处理队列元素的一般规则是，排在队首的顾客下一个被服务，而当新顾客到达时，他或她排在队尾。也就是说，队列是一种先进先出（FIFO）数据结构。

队列在计算机科学中有着广泛的应用。只要系统按照 FIFO 原则建模，就会使用队列。在本节末尾，我们将讨论队列最广泛的应用之一——计算机模拟。然而，首先我们需要开发实现队列所需的工具。接下来的几节将讨论如何设计以 ADT 方式实现队列的类。

队列是相同类型元素的集合，元素在一端添加，该端称为**后端**或**队尾**，在另一端删除，该端称为**队首**。例如，考虑银行中一排顾客，他们正在等待取款/存款或办理其他业务。每个新顾客都排在队尾。每当柜员准备好接待新顾客时，队首的顾客就会得到服务。

每当向队列添加新元素时，会访问队列的队尾；每当从队列中删除元素时，会访问队列的队首。

与栈一样，队列的中间元素是不可访问的，即使队列元素存储在数组中也是如此。

**队列：** 一种数据结构，元素在一端（称为队尾）添加，在另一端（称为队首）删除；是一种先进先出（FIFO）数据结构。

### 队列操作

从队列的定义可以看出，两个关键操作是添加和删除。我们将添加操作称为 addQueue，将删除操作称为 deleteQueue。由于既不能从空队列中删除元素，也不能向满队列中添加元素，为了成功实现 addQueue 和 deleteQueue 操作，我们还需要另外两个操作：isEmptyQueue（检查队列是否为空）和 isFullQueue（检查队列是否已满）。

我们还需要一个 initializeQueue 操作来将队列初始化为空状态。此外，为了获取队列的第一个和最后一个元素，我们包含 front 和 back 操作，如下列表所述。队列的一些操作如下：

- **initializeQueue：** 将队列初始化为空状态。
- **isEmptyQueue：** 确定队列是否为空。如果队列为空，则返回 `true`；否则返回 `false`。
- **isFullQueue：** 确定队列是否已满。如果队列已满，则返回 `true`；否则返回 `false`。
- **front：** 返回队首，即队列的第一个元素。此操作的输入由队列组成。在执行此操作之前，队列必须存在且不为空。
- **back：** 返回队列的最后一个元素。此操作的输入由队列组成。在执行此操作之前，队列必须存在且不为空。
- **addQueue：** 将新元素添加到队列的队尾。此操作的输入由队列和新元素组成。在执行此操作之前，队列必须存在且未满。
- **deleteQueue：** 从队列中移除队首元素。此操作的输入由队列组成。在执行此操作之前，队列必须存在且不为空。

与栈的情况一样，队列可以存储在数组或链式结构中。我们将考虑这两种实现。由于元素在一端添加而在另一端移除，我们需要两个指针来跟踪队列的队首和队尾，称为 queueFront 和 queueRear。

下面的抽象类 `class queueADT` 将这些操作定义为 ADT：

```cpp
template <class Type>
class queueADT
{
public:
    virtual bool isEmptyQueue() const = 0;
    //Function to determine whether the queue is empty.
    //Postcondition: Returns true if the queue is empty,
    //              otherwise returns false.

    virtual bool isFullQueue() const = 0;
    //Function to determine whether the queue is full.
    //Postcondition: Returns true if the queue is full,
    //              otherwise returns false.

    virtual void initializeQueue() = 0;

    virtual Type front() const = 0;
    //Function to return the first element of the queue.
    //Precondition: The queue exists and is not empty.
    //Postcondition: If the queue is empty, the program
    //              terminates; otherwise, the first
    //              element of the queue is returned.

    virtual Type back() const = 0;
    //Function to return the last element of the queue.
    //Precondition: The queue exists and is not empty.
    //Postcondition: If the queue is empty, the program
    //              terminates; otherwise, the last
    //              element of the queue is returned.

    virtual void addQueue(const Type& queueElement) = 0;
    //Function to add queueElement to the queue.
    //Precondition: The queue exists and is not full.
    //Postcondition: The queue is changed and queueElement
    //              is added to the queue.

    virtual void deleteQueue() = 0;
    //Function to remove the first element of the queue.
    //Precondition: The queue exists and is not empty.
    //Postcondition: The queue is changed and the first
    //              element is removed from the queue.
};
```

我们留给你作为练习：画出 `class queueADT` 的 UML 类图。

### 用数组实现队列

在给出将队列实现为 ADT 的类定义之前，我们需要确定实现队列需要多少个成员变量。当然，我们需要一个数组来存储队列元素，需要变量 **queueFront** 和 **queueRear** 来跟踪队列的第一个和最后一个元素，还需要变量 **maxQueueSize** 来指定队列的最大容量。因此，我们至少需要四个成员变量。

在编写实现队列操作的算法之前，我们需要决定如何使用 **queueFront** 和 **queueRear** 来访问队列元素。**queueFront** 和 **queueRear** 如何指示队列为空或已满？假设 **queueFront** 给出队列第一个元素的下标，**queueRear** 给出队列最后一个元素的下标。要向队列中添加元素，首先将 **queueRear** 前进到下一个数组位置，然后将元素添加到 **queueRear** 指向的位置。要从队列中删除元素，首先获取 **queueFront** 指向的元素，然后将 **queueFront** 前进到队列的下一个元素。因此，每次 **deleteQueue** 操作后，**queueFront** 都会改变；每次 **addQueue** 操作后，**queueRear** 都会改变。

让我们看看当 **queueFront** 在 **deleteQueue** 操作后改变、**queueRear** 在 **addQueue** 操作后改变时会发生什么。假设用于存储队列元素的数组大小为 100。

最初，队列为空。执行以下操作后

```
addQueue(Queue, 'A');
```

数组如图 17-26 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1281_0.png)

图 17-26 第一次 addQueue 操作后的队列

再执行两次 **addQueue** 操作

```
addQueue(Queue, 'B');
addQueue(Queue, 'C');
```

数组如图 17-27 所示。

