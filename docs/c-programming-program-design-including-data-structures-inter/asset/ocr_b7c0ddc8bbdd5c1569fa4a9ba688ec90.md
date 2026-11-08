# Waiting Customers’ Queue

When a customer arrives, he or she goes to the end of the queue. When a server becomes available, the customer at the front of the queue leaves to conduct the transaction. After each time unit, the waiting time of each customer in the queue is incremented by 1. The ADT queueType designed in this chapter has all the operations needed to implement a queue, except the operation of incrementing the waiting time of each customer in the queue by one time unit. We will derive the class waitingCustomerQueueType, from the class queueType and add the additional operations to implement the customer queue. The definition of the class waitingCustomerQueueType is as follows:

```
```cpp
class waitingCustomerQueueType: public queueType<customerType>
{
public:
    waitingCustomerQueueType(int size = 100);
    //Constructor
    //Postcondition: The queue is initialized according to
    //               the parameter size. The value of size
    //               is passed to the constructor of queueType.

    void updateWaitingQueue();
    //Function to increment the waiting time of each
    //customer in the queue by one time unit.
};
```
```

> > Notice that the class waitingCustomerQueueType is derived from the class queueType, which implements the queue in an array. You can also derive it from the class linkedQueueType, which implements the queue in a linked list. We leave the details as an exercise for you.

The definitions of the member functions are given next. The definition of the constructor is as follows:

```
```cpp
waitingCustomerQueueType::waitingCustomerQueueType(int size)
    :queueType<customerType>(size)
{
}
```
```

The function updateWaitingQueue increments the waiting time of each customer in the queue by one time unit. The class waitingCustomerQueueType is derived from the class queueType. Because the member variables of queueType are private, the function updateWaitingQueue cannot directly access the elements of the queue. The only way to access the elements of the queue is to use the deleteQueue operation. After incrementing the waiting time, the element can be put back into the queue by using the addQueue operation.