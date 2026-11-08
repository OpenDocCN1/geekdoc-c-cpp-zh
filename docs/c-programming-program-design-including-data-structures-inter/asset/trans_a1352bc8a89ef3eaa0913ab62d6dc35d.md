
![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_0.png)

**图 17-27** 又执行两次 addQueue 操作后的队列

现在考虑 deleteQueue 操作：

```cpp
deleteQueue();
```

经过此操作后，包含该队列的数组如图 17-28 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_1.png)

**图 17-28** 执行 `deleteQueue` 操作后的队列

这种队列设计可行吗？假设 A 表示向队列添加（即 addQueue）一个元素，D 表示从队列删除（即 deleteQueue）一个元素。考虑以下操作序列：

```cpp
AAADADADADADA...
```

这个操作序列最终会使索引 `queueRear` 指向数组的最后一个位置，给人队列已满的印象。然而，队列中只有两三个元素，且数组的前部是空的（见图 17-29）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_2.png)

**图 17-29** 执行操作序列 `AAADADADADADA...` 后的队列

此问题的一种解决方案是：当队列在尾部溢出（即 `queueRear` 指向数组的最后一个位置）时，我们可以检查索引 `queueFront` 的值。如果 `queueFront` 的值表明数组前部有空间，那么当 `queueRear` 到达数组的最后一个位置时，我们可以将所有队列元素向数组的第一个位置滑动。如果队列规模非常小，这种解决方案很好；否则，程序可能会执行得更慢。

此问题的另一种解决方案是假设数组是环形的——也就是说，数组的第一个位置紧跟在最后一个位置之后（见图 17-30）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1221_0.png)

我们将认为包含队列的数组是环形的，尽管我们在绘制容纳队列元素的数组图形时仍与之前相同。

假设我们有一个如图 17-31(a) 所示的队列。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1221_1.png)

执行 `addQueue(Queue, 'Z');` 操作后，队列如图 17-31(b) 所示。

由于包含队列的数组是环形的，我们可以使用以下语句将 `queueRear`（`queueFront`）推进到下一个数组位置：

```cpp
queueRear = (queueRear + 1) % maxQueueSize;
```

如果 `queueRear < maxQueueSize - 1`，那么 `queueRear + 1 <= maxQueueSize - 1`，所以 `(queueRear + 1) % maxQueueSize = queueRear + 1`。如果 `queueRear = maxQueueSize - 1`（即 `queueRear` 指向数组的最后一个位置），则 `queueRear + 1 = maxQueueSize`，所以 `(queueRear + 1) % maxQueueSize = 0`。在这种情况下，`queueRear` 将被设置为 0，即数组的第一个位置。

这种队列设计似乎效果不错。在编写实现队列操作的算法之前，请考虑以下两种情况。

**情况 1：** 假设经过某些操作后，包含队列的数组如图 17-32(a) 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1222_0.png)

**图 17-32** 删除操作前和操作后的队列

执行 `deleteQueue()` 操作后，生成的数组如图 17-32(b) 所示。

**情况 2：** 现在让我们考虑图 17-33(a) 所示的队列。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1222_1.png)

**图 17-33** 添加操作前和操作后的队列

执行 `addQueue(Queue, 'Z')` 操作后，生成的数组如图 17-33(b) 所示。

图 17-32(b) 和图 17-33(b) 中的数组具有相同的 `queueFront` 和 `queueRear` 值。然而，图 17-32(b) 中的结果数组表示空队列，而图 17-33(b) 中的结果数组表示满队列。这种最新的队列设计又带来了另一个问题：如何区分空队列和满队列。

此问题有几种解决方案。一种解决方案是保留一个计数。除了成员变量 `queueFront` 和 `queueRear`，我们还需要另一个变量 `count` 来实现队列。每当向队列添加新元素时，`count` 的值就递增；每当从队列中移除一个元素时，`count` 的值就递减。在这种情况下，函数 `initializeQueue` 将 `count` 初始化为 0。如果队列用户经常需要知道队列中的元素个数，这种解决方案非常有用。

另一种解决方案是让 `queueFront` 指示队列第一个元素之前的数组位置的索引，而不是（实际）元素本身的索引。在这种情况下，假设 `queueRear` 仍然指示队列中最后一个元素的索引，那么如果 `queueFront == queueRear`，队列为空。在这种解决方案中，由索引 `queueFront` 指示的槽位（即第一个真正元素之前的槽位）被保留。如果下一个可用空间是由 `queueFront` 指示的特殊保留槽位，则队列为满。最后，由于 `queueFront` 指示的数组位置需要保持为空，如果数组大小，比方说是 100，那么队列中可以存储 99 个元素（见图 17-34）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1223_0.png)

**图 17-34** 用于存储队列元素且带有保留槽位的数组

让我们使用第一种解决方案来实现队列。也就是说，我们使用变量 `count` 来指示队列为空还是满。下面的类实现了抽象类 `queueADT` 的函数。因为数组可以动态分配，我们将由用户指定用于实现队列的数组大小。数组的默认大小是 100。

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
    //                otherwise returns false.

    bool isFullQueue() const;
    //Function to determine whether the queue is full.
    //Postcondition: Returns true if the queue is full,
    //                otherwise returns false.

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
    int maxQueueSize; //variable to store the maximum queue size
    int count;        //variable to store the number of
                      //elements in the queue
    int queueFront;   //variable to point to the first
                      //element of the queue
    int queueRear;    //variable to point to the last
                      //element of the queue
    Type *list;       //pointer to the array that holds
                      //the queue elements
};
```

我们将类 `queueType` 的 UML 类图留作练习。（参见本章末尾的练习 30。）

接下来，我们考虑队列操作的实现。

### 空队列和满队列

如前所述，如果 `count == 0`，则队列为空；如果 `count == maxQueueSize`，则队列为满。因此，实现这些操作的函数如下：

```cpp
template <class Type>
bool queueType<Type>::isEmptyQueue() const
{
    return (count == 0);
} //end isEmptyQueue

template <class Type>
bool queueType<Type>::isFullQueue() const
{
    return (count == maxQueueSize);
} //end isFullQueue
```

### 初始化队列

该操作将队列初始化为空状态。第一个元素被添加到数组的第一个位置。因此，我们将 `queueFront` 初始化为 0，将 `queueRear` 初始化为 `maxQueueSize - 1`，并将 `count` 初始化为 0（见图 17-35）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1225_0.png)

函数 `initializeQueue` 的定义如下：

```cpp
template <class Type>
void queueType<Type>::initializeQueue()
{
    queueFront = 0;
    queueRear = maxQueueSize - 1;
    count = 0;
} //end initializeQueue
```

### 队首

该操作返回队列的第一个元素。如果队列非空，则返回由索引 `queueFront` 指示的队列元素；否则，程序终止。

