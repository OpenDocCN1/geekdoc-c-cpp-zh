
```cpp
void updateWaitingQueue();
    // Function to increment the waiting time of each
    // customer in the queue by one time unit.
};
```

> **NOTE**
>
> Notice that the class waitingCustomerQueueType is derived from the class queueType, which implements the queue in an array. You can also derive it from the class linkedQueueType, which implements the queue in a linked list. We leave the details as an exercise for you.

The definitions of the member functions are given next. The definition of the constructor is as follows:

```cpp
waitingCustomerQueueType::waitingCustomerQueueType(int size)
    : queueType<customerType>(size)
{
}
```

The function updateWaitingQueue increments the waiting time of each customer in the queue by one time unit. The class waitingCustomerQueueType is derived from the class queueType. Because the member variables of queueType are private, the function updateWaitingQueue cannot directly access the elements of the queue. The only way to access the elements of the queue is to use the deleteQueue operation. After incrementing the waiting time, the element can be put back into the queue by using the addQueue operation.

The addQueue operation inserts the element at the end of the queue. If we perform the deleteQueue operation followed by the addQueue operation for each element of the queue, then eventually the front element again becomes the front element. Given that each deleteQueue operation is followed by an addQueue operation, how do we determine that all of the elements of the queue have been processed? We cannot use the isEmptyQueue or isFullQueue operations on the queue, because the queue will never be empty or full.

One solution to this problem is to create a temporary queue. Every element of the original queue is removed, processed, and inserted into the temporary queue. When the original queue becomes empty, all of the elements in the queue are processed. We can then copy the elements from the temporary queue back into the original queue. However, this solution requires us to use extra memory space, which could be significant. Also, if the queue is large, extra computer time is needed to copy the elements from the temporary queue back into the original queue. Let us look into another solution.

In the second solution, before starting to update the elements of the queue, we can insert a dummy customer with a wait time of, say, -1. During the update process, when we arrive at the customer with the wait time of -1, we can stop the update process without processing the customer with the wait time of -1. If we do not process the customer with the wait time of -1, this customer is removed from the queue and, after processing all of the elements of the queue, the queue will contain no extra elements. This solution does not require us to create a temporary queue, so we do

```cpp
cout << "Enter the transaction time: ";
cin >> transTime;
cout << endl;

cout << "Enter the time between customer arrivals: ";
cin >> interCustomerArrival;
cout << endl;
}
```

When a server becomes free and the customer queue is nonempty, we can move the customer at the front of the queue to the free server to be served. Moreover, when a customer starts the transaction, the waiting time ends. The waiting time of the customer is added to the total waiting time. The general algorithm to start the transaction (supposing that serverID denotes the ID of the free server) is as follows:

- 1. Remove the customer from the front of the queue.

    ```cpp
    customer = customerQueue.front();
    customerQueue.deleteQueue();
    ```

- 2. Update the total wait time by adding the current customer’s wait time to the previous total wait time.

    ```cpp
    totalWait = totalWait + customer.getWaitingTime();
    ```

- 3. Set the free server to begin the transaction.

    ```cpp
    serverList.setServerBusy(serverID, customer, transTime);
    ```

To run the simulation, we need to know the number of customers arriving at a given time unit and how long it takes to serve the customer. We use the Poisson distribution from statistics, which says that the probability of y events occurring at a given time is given by the following formula:

$$P(y)=\frac{\lambda^y e^{-\lambda}}{y!},\quad y=0,1,2,\ldots,$$

in which λ is the expected value that y events occur at that time. Suppose that, on average, a customer arrives every four minutes. During this four-minute period, the customer can arrive at any one of the four minutes. Assuming an equal likelihood of each of the four minutes, the expected value that a customer arrives in each of the four minutes is, therefore, 1/4 = 0.25. Next, we need to determine whether or not the customer actually arrives at a given minute.

Now, $P(0)=e^{-\lambda}$ is the probability that no event occurs at a given time. One of the basic assumptions of the Poisson distribution is that the probability of more than one outcome occurring in a short time interval is negligible. For simplicity, we assume that only one customer arrives at a given time unit. Thus, we use $e^{-\lambda}$ as the cutoff point to determine whether a customer arrives at a given time unit. Suppose that, on average, a customer arrives every four minutes. Then, $\lambda=0.25$. We can use an algorithm to generate a number between 0 and 1. If the value of the number generated is $>e^{-0.25}$, we can assume that the customer arrived at a particular time unit. For example, suppose that *rNum* is a random number such that 0 ≤ *rNum* ≤ 1. If *rNum* > $e^{-0.25}$, the customer arrived at the given time unit.

We now describe the function `runSimulation` to implement the simulation. Suppose that we run the simulation for 100 time units and customers arrive at time units 93, 96, and 100. The average transaction time is five minutes—that is, five time units. For simplicity, assume that we have only one server and that the server becomes free at time unit 97, and that all customers arriving before time unit 93 have been served. When the server becomes free at time unit 97, the customer arriving at time unit 93 starts the transaction. Because the transaction of the customer arriving at time unit 93 starts at time unit 97 and it takes five minutes to complete a transaction, when the simulation loop ends, the customer arriving at time unit 93 is still at the server. Moreover, customers arriving at time units 96 and 100 are in the queue. For simplicity, we assume that when the simulation loop ends, the customers at the servers are considered served. The general algorithm for this function is as follows:

- 1. Declare and initialize the variables, such as the simulation parameters, customer number, clock, total and average waiting times, number of customers arrived, number of customers served, number of customers left in the waiting queue, number of customers left with the servers, `waitingCustomersQueue`, and a list of servers.

- 2. The main loop is

    ```cpp
    for (clock = 1; clock <= simulationTime; clock++)
    {
    ```

    - 2.1. Update the server list to decrement the transaction time of each busy server by one time unit.
    - 2.2. If the customer's queue is nonempty, increment the waiting time of each customer by one time unit.
    - 2.3. If a customer arrives, increment the number of customers by 1 and add the new customer to the queue.
    - 2.4. If a server is free and the customer's queue is nonempty, remove a customer from the front of the queue and send the customer to the free server.

    ```cpp
    }
    ```

- 3. Print the appropriate results. Your results must include the number of customers left in the queue, the number of customers still with servers, the number of customers arrived, and the number of customers who actually completed a transaction.

Once you have designed the function `runSimulation`, the definition of the function `main` is simple and straightforward because the function `main` calls only the function `runSimulation`. Programming Exercise 18 asks you to write the definition of the function `runSimulation`.
