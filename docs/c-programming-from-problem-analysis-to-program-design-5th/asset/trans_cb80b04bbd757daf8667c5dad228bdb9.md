
下面的抽象 `class queueADT` 将以下操作定义为 ADT。

```cpp
template <class Type>
class queueADT
{
public:
    virtual bool isEmptyQueue() const = 0;
        //Function to determine whether the queue is empty.
        //Postcondition: Returns true if the queue is empty,
        //               otherwise returns false.

    virtual bool isFullQueue() const = 0;
        //Function to determine whether the queue is full.
        //Postcondition: Returns true if the queue is full,
        //               otherwise returns false.

    virtual void initializeQueue() = 0;
        //Function to initialize the queue to an empty state.
        //Postcondition: The queue is empty.
    virtual Type front() const = 0;
        //Function to return the first element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: If the queue is empty, the program
        //               terminates; otherwise, the first
        //               element of the queue is returned.

    virtual Type back() const = 0;
        //Function to return the last element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: If the queue is empty, the program
        //               terminates; otherwise, the last
        //               element of the queue is returned.

    virtual void addQueue(const Type& queueElement) = 0;
        //Function to add queueElement to the queue.
        //Precondition: The queue exists and is not full.
        //Postcondition: The queue is changed and queueElement
        //               is added to the queue.

    virtual void deleteQueue() = 0;
        //Function to remove the first element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: The queue is changed and the first
        //               element is removed from the queue.
};
```

我们把绘制 `queueADT` 类的 UML 类图留作练习。

## 队列的数组实现

在给出将队列作为 ADT 实现的类定义之前，我们需要确定实现该队列需要多少个成员变量。当然，我们需要一个数组来存储队列元素，需要变量 queueFront 和 queueRear 来跟踪队列的第一个和最后一个元素，还需要变量 maxQueueSize 来指定队列的最大大小。因此，我们至少需要四个成员变量。

在编写实现队列操作的算法之前，我们需要决定如何使用 queueFront 和 queueRear 来访问队列元素。queueFront 和 queueRear 如何表示队列为空或已满？假设 queueFront 给出队列第一个元素的索引，queueRear 给出队列最后一个元素的索引。要向队列添加元素，首先将 queueRear 前移到下一个数组位置，然后将元素添加到 queueRear 所指向的位置。要从队列删除元素，首先取出 queueFront 所指向的元素，然后将 queueFront 前移到队列的下一个元素。因此，每次 deleteQueue 操作后 queueFront 都会变化，每次 addQueue 操作后 queueRear 都会变化。

让我们看看在 deleteQueue 操作后 queueFront 发生变化、在 addQueue 操作后 queueRear 发生变化时会发生什么。假设用于保存队列元素的数组大小为 100。

初始时，队列为空。执行以下操作后：

```
addQueue(Queue, 'A');
```

数组如图 19–26 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1208_0.png)

**图 19–26** 第一次 `addQueue` 操作后的队列

再执行两次 addQueue 操作后：

```
addQueue(Queue, 'B');
addQueue(Queue, 'C');
```

数组如图 19–27 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1209_0.png)

**图 19-27** 再执行两次 addQueue 操作后的队列

现在考虑 deleteQueue 操作：

```
deleteQueue();
```

执行此操作后，包含该队列的数组如图 19-28 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1209_1.png)

**图 19-28** 执行 deleteQueue 操作后的队列

这种队列设计能行得通吗？假设 A 表示向队列添加（即 addQueue）一个元素，D 表示从队列删除（即 deleteQueue）一个元素。考虑以下操作序列：

```
AAADADADADADADADA...
```

这一操作序列最终会使索引 queueRear 指向数组的最后一个位置，给人一种队列已满的印象。然而，队列中只有两三个元素，而数组的前部是空的（见图 19-29）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1209_2.png)

**图 19-29** 执行操作序列 AAADADADADADADADA... 后的队列

这个问题的一种解决方案是：当队列向后溢出（即 queueRear 指向数组的最后一个位置）时，我们可以检查索引 queueFront 的值。如果 queueFront 的值表明数组前部还有空间，那么当 queueRear 到达数组的最后一个位置时，我们可以将所有队列元素向数组的第一个位置滑动。如果队列规模很小，这种解决方案很好；否则，程序执行可能会变慢。

这个问题的另一种解决方案是假定数组是环形的——也就是说，数组的第一个位置紧接在最后一个位置之后（见图 19-30）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1210_0.png)

**图 19-30** 循环队列

我们将把包含队列的数组视为环形的，尽管仍像之前那样绘制保存队列元素的数组示意图。

假设我们有如图 19-31(a) 所示的队列。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1210_1.png)

**图 19-31** 添加操作前后的队列

执行操作 `addQueue(Queue, 'Z');` 后，队列如图 19-31(b) 所示。

由于包含队列的数组是环形的，我们可以使用以下语句将 `queueRear`（`queueFront`）前移到下一个数组位置。

`queueRear = (queueRear + 1) % maxQueueSize;`

如果 `queueRear < maxQueueSize − 1`，那么 `queueRear + 1 <= maxQueueSize − 1`，所以 `(queueRear + 1) % maxQueueSize = queueRear + 1`。如果 `queueRear == maxQueueSize − 1`（即 `queueRear` 指向数组的最后一个位置），则 `queueRear + 1 == maxQueueSize`，所以 `(queueRear + 1) % maxQueueSize = 0`。在这种情况下，`queueRear` 将被设为 0，即数组的第一个位置。

这种队列设计似乎运行良好。在编写实现队列操作的算法之前，请考虑以下两种情况。

**情况 1：** 假设经过某些操作后，包含队列的数组如图 19–32(a) 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1211_0.png)

**图 19–32** 删除操作前后的队列

执行操作 `deleteQueue();` 后，所得数组如图 19–32(b) 所示。

**情况 2：** 现在我们考虑图 19–33(a) 所示的队列。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1211_1.png)

**图 19–33** 添加操作前后的队列

执行操作 `addQueue(Queue, 'Z');` 后，所得数组如图 19–33(b) 所示。

图 19–32(b) 和图 19–33(b) 中的数组具有相同的 queueFront 和 queueRear 值。然而，图 19–32(b) 中所得数组表示空队列，而图 19–33(b) 中所得数组表示满队列。最新的这种队列设计又引出了另一个问题：如何区分空队列和满队列。

这个问题有几种解决方案。一种解决方案是维护一个计数器。除了成员变量 queueFront 和 queueRear 之外，我们还需要另一个变量 count 来实现队列。每当向队列添加新元素时，count 的值就递增；每当从队列删除元素时，count 的值就递减。在这种情况下，函数 initializeQueue 将 count 初始化为 0。如果队列的使用者经常需要知道队列中的元素个数，这种解决方案非常有用。

另一种解决方案是让 queueFront 表示队列第一个元素之前那个数组位置的索引，而不是（实际的）第一个元素本身的索引。在这种情况下，假设 queueRear 仍表示队列中最后一个元素的索引，则如果 queueFront == queueRear，队列为空。在这种解决方案中，由索引 queueFront 指示的槽位（即第一个真实元素之前的槽位）被保留。如果下一个可用空间是由 queueFront 指示的特殊保留槽位，则队列将满。最后，由于 queueFront 指示的数组位置要保持为空，如果数组大小为 100，那么队列中最多可以存储 99 个元素（见图 19–34）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1212_0.png)

让我们使用第一种解决方案来实现队列。也就是说，我们使用变量 count 来表示队列是空还是满。下面的类实现了抽象类 queueADT 的功能。由于数组可以动态分配，我们将让用户指定用于实现队列的数组大小。数组的默认大小为 100。

```cpp
template <class Type>
class queueType: public queueADT<Type>
{
public:
    queueType<Type>& operator=(const queueType<Type>&);
    //Overload the assignment operator
```
