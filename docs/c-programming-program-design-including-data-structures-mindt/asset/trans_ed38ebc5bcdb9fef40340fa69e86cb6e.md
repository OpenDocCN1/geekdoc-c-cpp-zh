

![](img/b217c421655b51e7494cf3b89bb5432d_1282_0.png)

**图 17-27**  再进行两次 `addQueue` 操作后的队列

现在考虑 `deleteQueue` 操作：

```
deleteQueue();
```

执行该操作后，包含队列的数组如图 17-28 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1282_1.png)

**图 17-28**  执行 `deleteQueue` 操作后的队列

这种队列设计可行吗？假设 A 表示向队列中添加（即 `addQueue`）一个元素，D 表示从队列中删除（即 `deleteQueue`）一个元素。考虑以下操作序列：

```
AAADADADADADADA...
```

该操作序列最终会使索引 `queueRear` 指向数组的最后一个位置，从而让人以为队列已满。然而，队列中只有两三个元素，并且数组前端是空的（见图 17-29）。

![](img/b217c421655b51e7494cf3b89bb5432d_1282_2.png)

**图 17-29**  执行操作序列 `AAADADADADADADA...` 后的队列

这个问题的一种解决方案是：当队列在尾部溢出（即 **queueRear** 指向数组的最后一个位置）时，我们可以检查索引 **queueFront** 的值。如果 **queueFront** 的值表明数组前端还有空间，那么当 **queueRear** 到达数组的最后一个位置时，我们可以将所有队列元素向数组的第一个位置滑动。如果队列规模非常小，这种解决方案很好；否则，程序执行可能会更慢。

这个问题的另一种解决方案是假设数组是环形的——即数组的第一个位置紧跟在最后一个位置之后（见图 17-30）。

![](img/b217c421655b51e7494cf3b89bb5432d_1283_0.png)

**图 17-30**  环形队列

我们将把包含队列的数组视为环形，尽管绘制保存队列元素的数组示意图时仍和以前一样。

假设我们有如图 17-31(a) 所示的队列。

![](img/b217c421655b51e7494cf3b89bb5432d_1283_1.png)

**图 17-31**  添加操作前后的队列

执行操作 **addQueue(Queue, 'Z');** 后，队列如图 17-31(b) 所示。

由于包含队列的数组是环形的，我们可以使用以下语句将 `queueRear`（`queueFront`）推进到下一个数组位置：

```
queueRear = (queueRear + 1) % maxQueueSize;
```

如果 `queueRear < maxQueueSize − 1`，那么 `queueRear + 1 <= maxQueueSize − 1`，所以 `(queueRear + 1) % maxQueueSize = queueRear + 1`。如果 `queueRear == maxQueueSize − 1`（即 `queueRear` 指向数组的最后一个位置），则 `queueRear + 1 == maxQueueSize`，所以 `(queueRear + 1) % maxQueueSize = 0`。在这种情况下，`queueRear` 将被设置为 0，即数组的第一个位置。

这种队列设计似乎运行良好。在编写实现队列操作的算法之前，请考虑以下两种情况。

### 情况 1：

假设经过某些操作后，包含队列的数组如图 17-32(a) 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_1284_0.png)

**图 17-32**  删除操作前后的队列

执行操作 `deleteQueue();` 后，结果数组如图 17-32(b) 所示。

### 情况 2：

现在让我们考虑图 17-33(a) 所示的队列。

![](img/b217c421655b51e7494cf3b89bb5432d_1284_1.png)

**图 17-33**  添加操作前后的队列

执行操作 `addQueue(Queue, 'Z');` 后，结果数组如图 17-33(b) 所示。

图 17-32(b) 和图 17-33(b) 中的数组具有相同的 `queueFront` 和 `queueRear` 值。然而，图 17-32(b) 中的结果数组表示空队列，而图 17-33(b) 中的结果数组表示满队列。这种最新的队列设计又带来了另一个问题：如何区分空队列和满队列。

这个问题有几种解决方案。一种解决方案是维护一个计数。除了成员变量 `queueFront` 和 `queueRear` 之外，我们还需要另一个变量 `count` 来实现队列。每当向队列添加新元素时，`count` 的值递增；每当从队列中删除元素时，`count` 的值递减。在这种情况下，函数 `initializeQueue` 将 `count` 初始化为 0。如果队列的使用者经常需要知道队列中元素的数量，这种解决方案非常有用。

另一种解决方案是让 `queueFront` 表示队列第一个元素*之前*的数组位置的索引，而不是（实际的）第一个元素本身的索引。在这种情况下，假设 `queueRear` 仍然表示队列中最后一个元素的索引，如果 `queueFront == queueRear`，则队列为空。在这种解决方案中，索引 `queueFront` 所指示的槽位（即第一个真实元素之前的槽位）被保留。如果下一个可用空间是 `queueFront` 所指示的特殊保留槽位，则队列将满。最后，由于由 `queueFront` 指示的数组位置要保持为空，因此如果数组大小是，比如说，100，那么队列中可以存储 99 个元素（见图 17-34）。

![](img/b217c421655b51e7494cf3b89bb5432d_1285_0.png)

**图 17-34**  带保留槽位的用于存储队列元素的数组

让我们使用第一种解决方案来实现队列。也就是说，我们使用变量 `count` 来表示队列是空还是满。下面的类实现了抽象类 `queueADT` 的功能。由于数组可以动态分配，我们将让用户指定用于实现队列的数组大小。数组的默认大小为 100。

```cpp
template <class Type>
class queueType: public queueADT<Type>
{
public:
    const queueType<Type>& operator=(const queueType<Type>&);
        //Overload the assignment operator.

    bool isEmptyQueue() const;
        //Function to determine whether the queue is empty.
        //Postcondition: Returns true if the queue is empty,
        //              otherwise returns false.

    bool isFullQueue() const;
        //Function to determine whether the queue is full.
        //Postcondition: Returns true if the queue is full,
        //              otherwise returns false.

    void initializeQueue();
        //Function to initialize the queue to an empty state.
        //Postcondition: The queue is empty.

    Type front() const;
        //Function to return the first element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: If the queue is empty, the program
        //              terminates; otherwise, the first
        //              element of the queue is returned.

    Type back() const;
        //Function to return the last element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: If the queue is empty, the program
        //              terminates; otherwise, the last
        //              element of the queue is returned.

    void addQueue(const Type& queueElement);
        //Function to add queueElement to the queue.
        //Precondition: The queue exists and is not full.
        //Postcondition: The queue is changed and queueElement
        //              is added to the queue.

    void deleteQueue();
        //Function to remove the first element of the queue.
        //Precondition: The queue exists and is not empty.
        //Postcondition: The queue is changed and the first
        //              element is removed from the queue.

    queueType(int queueSize = 100);
        //Constructor

    queueType(const queueType<Type>& otherQueue);
        //Copy constructor

    ~queueType();
        //Destructor

private:
    int maxQueueSize;   //variable to store the maximum queue size
    int count;          //variable to store the number of
                        //elements in the queue
    int queueFront;     //variable to point to the first
                        //element of the queue
    int queueRear;      //variable to point to the last
                        //element of the queue
    Type *list;          //pointer to the array that holds
                        //the queue elements
};
```

