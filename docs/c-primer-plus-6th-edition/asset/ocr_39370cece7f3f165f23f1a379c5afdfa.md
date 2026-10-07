# Chapter 12 Classes and Dynamic Memory Allocation

```
// time set to a random value in the range 1 - 3
void Customer::set(long when)
{
    processstime = std::rand() % 3 + 1;
    arrive = when;
}
```

# The ATM Simulation

You now have the tools needed for the ATM simulation.The program should allow the user to enter three quantities: the maximum queue size, the number of hours the program will simulate, and the average number of customers per hour.The program should use a loop in which each cycle represents one minute. During each cycle, the program should do the following:

+   * Determine whether a new customer has arrived. If so, add the customer to the queue if there is room; otherwise, turn the customer.
* If no one is being processed, take the first person from the queue. Determine how long the person has been waiting and set wait_time counter to the processing time that the new customer will need.
* If a customer is being processed, decrement the wait_time counter by one minute.
* Track various quantities, such as the number of customers served, the number of customers turned away, cumulative time spent waiting in line, and cumulative queue length.

When the simulation cycle is finished, the program should report various statistical findings.
An interesting matter is how the program determines whether a new customer has arrived. Suppose that on average, 10 customers arrive per hour. This amounts to a customer every 6 minutes. The program computes and stores that in the variable min_per_cust. However, having a customer show up exactly 6 minutes is unrealistic. What really (at most of the time) is a more random process that averages to a customer every 6 minutes. The program uses this function to determine whether a customer shows up during a cycle:

```
bool newcustomer(double x)
{
    return (std::rand() * x / RAND_MAX < 1);
}
```

Here is how it works.The value RAND_MAX is defined in the cstdlib file (formerly stdlib.h) and represents the largest value the rand() function can return (0 is the lowest value). Suppose that x, the average time between customers, is 6. Then the value of rand() x / RAND_MAX will be somewhere between 0 and 6. In particular, it will be less than