```
```cpp
customerType::customerType(int customerN, int arrvTime,
                           int wTime, int tTime)
{
    setCustomerInfo(customerN, arrvTime, wTime, tTime);
}
```
```

The function getWaitingTime returns the current waiting time. The definition of the function getWaitingTime is:

```
```cpp
int customerType::getWaitingTime() const
{
    return waitingTime;
}
```
```

The function incrementWaitingTime increments the value of waitingTime. Its definition is:

```
```cpp
void customerType::incrementWaitingTime()
{
    waitingTime++;
}
```
```

The definitions of the functions setWaitingTime, getArrivalTime, getTransactionTime, and getCustomerNumber are left as an exercise for you.

# Server

At any given time unit, the server is either busy serving a customer or is free. We use a string variable to set the status of the server. Every server has a timer and, because the program might need to know which customer is served by which server, the server also stores the information of the customer being served. Thus, three member variables are associated with a server: the status, the transactionTime, and the currentCustomer. Some of the basic operations that must be performed on a server are as follows: check whether the server is free; set the server as free; set the server as busy; set the transaction time (that is, how long it takes to serve the customer); return the remaining transaction time (to determine whether the server should be set to free); if the server is busy after each time unit, decrement the transaction time by one time unit; and so on. The following class, serverType, implements the server as an ADT.

```
```cpp
class serverType
{
public:
    serverType();
        //Default constructor
        //Sets the values of the instance variables to their default
        //values.
        //Postcondition: currentCustomer is initialized by its
        //              default constructor, status = "free", and
        //              the transaction time is initialized to 0.
        //
```
```