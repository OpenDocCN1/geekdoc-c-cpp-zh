
![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_0.png)

**FIGURE 17-27** Queue after two more addQueue operations

Now consider the deleteQueue operation:

```cpp
deleteQueue();
```

After this operation, the array containing the queue is as shown in Figure 17-28.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_1.png)

**FIGURE 17-28** Queue after the `deleteQueue` operation

Will this queue design work? Suppose A stands for adding (that is, addQueue) an element to the queue, and D stands for deleting (that is, deleteQueue) an element from the queue. Consider the following sequence of operations:

```cpp
AAADADADADADA...
```

This sequence of operations would eventually set the index `queueRear` to point to the last array position, giving the impression that the queue is full. However, the queue has only two or three elements, and the front of the array is empty (see Figure 17-29).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1220_2.png)

**FIGURE 17-29** Queue after the sequence of operations `AAADADADADADA...`

One solution to this problem is that when the queue overflows to the rear (that is, `queueRear` points to the last array position), we can check the value of the index `queueFront`. If the value of `queueFront` indicates that there is room in the front of the array, then when `queueRear` gets to the last array position, we can slide all of the queue elements toward the first array position. This solution is good if the queue size is very small; otherwise, the program may execute more slowly.

Another solution to this problem is to assume that the array is circular—that is, the first array position immediately follows the last array position (see Figure 17-30).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1221_0.png)

We will consider the array containing the queue to be circular, although we will draw the figures of the array holding the queue elements as before.

Suppose that we have the queue as shown in Figure 17-31(a).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1221_1.png)

After the operation `addQueue(Queue, 'Z');`, the queue is as shown in Figure 17-31(b).

Because the array containing the queue is circular, we can use the following statement to advance `queueRear` (`queueFront`) to the next array position:

```cpp
queueRear = (queueRear + 1) % maxQueueSize;
```

If `queueRear < maxQueueSize - 1`, then `queueRear + 1 <= maxQueueSize - 1`, so `(queueRear + 1) % maxQueueSize = queueRear + 1`. If `queueRear = maxQueueSize - 1` (that is, `queueRear` points to the last array position), `queueRear + 1 = maxQueueSize`, so `(queueRear + 1) % maxQueueSize = 0`. In this case, `queueRear` will be set to 0, which is the first array position.

This queue design seems to work well. Before we write the algorithms to implement the queue operations, consider the following two cases.

**Case 1:** Suppose that after certain operations, the array containing the queue is as shown in Figure 17-32(a).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1222_0.png)

**FIGURE 17-32** Queue before and after the delete operation

After the operation `deleteQueue()`, the resulting array is as shown in Figure 17-32(b).

**Case 2:** Let us now consider the queue shown in Figure 17-33(a).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1222_1.png)

**FIGURE 17-33** Queue before and after the add operation

After the operation `addQueue(Queue, 'Z')`, the resulting array is as shown in Figure 17-33(b).

The arrays in Figures 17-32(b) and 17-33(b) have identical values for `queueFront` and `queueRear`. However, the resulting array in Figure 17-32(b) represents an empty queue, whereas the resulting array in Figure 17-33(b) represents a full queue. This latest queue design has brought up another problem of distinguishing between an empty and a full queue.

This problem has several solutions. One solution is to keep a count. In addition to the member variables `queueFront` and `queueRear`, we need another variable, `count`, to implement the queue. The value of `count` is incremented whenever a new element is added to the queue, and it is decremented whenever an element is removed from the queue. In this case, the function `initializeQueue` initializes `count` to 0. This solution is very useful if the user of the queue frequently needs to know the number of elements in the queue.

Another solution is to let `queueFront` indicate the index of the array position preceding the first element of the queue, rather than the index of the (actual) element itself. In this case, assuming `queueRear` still indicates the index of the last element in the queue, the queue is empty if `queueFront == queueRear`. In this solution, the slot indicated by the index `queueFront` (that is, the slot preceding the first true element) is reserved. The queue will be full if the next available space is the special reserved slot indicated by `queueFront`. Finally, because the array position indicated by `queueFront` is to be kept empty, if the array size is, say, 100, then 99 elements can be stored in the queue (see Figure 17-34).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1223_0.png)

**FIGURE 17-34** Array to store the queue elements with a reserved slot

Let us implement the queue using the first solution. That is, we use the variable `count` to indicate whether the queue is empty or full. The following class implements the functions of the abstract class `queueADT`. Because arrays can be allocated dynamically, we will leave it for the user to specify the size of the array to implement the queue. The default size of the array is 100.

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

We leave the UML class diagram of the class `queueType` as an exercise for you. (See Exercise 30 at the end of this chapter.)

Next, we consider the implementation of the queue operations.

### EMPTY QUEUE AND FULL QUEUE

As discussed earlier, the queue is empty if `count == 0`, and the queue is full if `count == maxQueueSize`. So the functions to implement these operations are:

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

### INITIALIZE QUEUE

This operation initializes a queue to an empty state. The first element is added at the first array position. Therefore, we initialize `queueFront` to 0, `queueRear` to `maxQueueSize - 1`, and `count` to 0 (see Figure 17-35).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1225_0.png)

The definition of the function `initializeQueue` is:

```cpp
template <class Type>
void queueType<Type>::initializeQueue()
{
    queueFront = 0;
    queueRear = maxQueueSize - 1;
    count = 0;
} //end initializeQueue
```

### FRONT

This operation returns the first element of the queue. If the queue is nonempty, the element of the queue indicated by the index `queueFront` is returned; otherwise, the program terminates.
