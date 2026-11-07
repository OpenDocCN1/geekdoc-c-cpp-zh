```
```cpp
void initializeQueue();
//Function to initialize the queue to an empty state.
//Postcondition: queueFront = nullptr; queueRear = nullptr

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

linkedQueueType();
//Default constructor

linkedQueueType(const linkedQueueType<Type>& otherQueue);
//Copy constructor

~linkedQueueType();
//Destructor

private:
    nodeType<Type> *queueFront;  //pointer to the front of
                                 //the queue
    nodeType<Type> *queueRear;   //pointer to the rear of
                                 //the queue
};
```
```

The UML class diagram of the class `linkedQueueType` is left as an exercise for you. (See Exercise 35 at the end of this chapter.)

Next, we write the definitions of the functions of the class `linkedQueueType`.

# EMPTY AND FULL QUEUE

The queue is empty if `queueFront` is `nullptr`. Memory to store the queue elements is allocated dynamically. Therefore, the queue is never full, so the function to implement