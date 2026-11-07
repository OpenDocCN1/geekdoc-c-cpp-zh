
```cpp
//Postcondition: The value of transactionTime is
// returned.

int getCurrentCustomerTransactionTime() const;
//Function to return the transaction time of the
//current customer.
//Postcondition: The value of transactionTime is the
// current customer is returned.

private:
    customerType currentCustomer;
    string status;
    int transactionTime;
};
```

Figure 19–37 shows the UML class diagram of the class `serverType`.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1230_0.png)

**FIGURE 19–37**  UML class diagram of the class `serverType`

The definitions of some of the member functions of the class `serverType` are:

```cpp
serverType::serverType()
{
    status = "free";
    transactionTime = 0;
}

bool serverType::isFree() const
{
    return (status == "free");
}

void serverType::setBusy()
{
    status = "busy";
}

void serverType::setFree()
{
    status = "free";
}

void serverType::setTransactionTime(int t)
{
    transactionTime = t;
}

void serverType::setTransactionTime()
{
    int time;

    time = currentCustomer.getTransactionTime();

    transactionTime = time;
}

void serverType::decreaseTransactionTime()
{
    transactionTime--;
}
```

We leave the definitions of the functions getRemainingTransactionTime, setCurrentCustomer, getCurrentCustomerNumber, getCurrentCustomerArrivalTime, getCurrentCustomerWaitingTime, and getCurrentCustomerTransactionTime as an exercise for you.

Because we are designing a simulation program that can be used in a variety of applications, we need to design two more classes: one to create and process a list of servers and one to create and process a queue of waiting customers. The next two sections describe each of these classes.

## Server List

A server list is a set of servers. At any given time, a server is either free or busy. For the customer at the front of the queue, we need to find a server in the list that is free. If all of the servers are busy, then the customer must wait until one of the servers becomes free. Thus, the class that implements a list of servers has two member variables: one to store the number of servers and one to maintain a list of servers. Using dynamic arrays, depending on the number of servers specified by the user, a list of servers is created during program execution. Some of the operations that must be performed on a server list are as follows:

- return the number of a free server;
- when a customer gets ready to do business and a server is available, set the server to busy;
- when the simulation ends, some of the servers might still be busy, so return the number of busy servers;
- after each time unit, reduce the transactionTime of each busy server by one time unit;
- and if the transactionTime of a server becomes zero, set the server to free.

The following class, serverListType, implements the list of servers as an ADT.

```cpp
class serverListType
{
public:
    serverListType(int num = 1);
        //Constructor to initialize a list of servers
        //Postcondition: numOfServers = num
        //              A list of servers, specified by num,
        //              is created and each server is
        //              initialized to "free".

    ~serverListType();
        //Destructor
        //Postcondition: The list of servers is destroyed.

    int getFreeServerID() const;
        //Function to search the list of servers.
        //Postcondition: If a free server is found, returns
        //              its ID; otherwise, returns -1.

    int getNumberOfBusyServers() const;
        //Function to return the number of busy servers.
        //Postcondition: The number of busy servers is returned.

    void setServerBusy(int serverID, customerType cCustomer,
                       int tTime);
        //Function to set a server as busy.
        //Postcondition: The server specified by serverID is set
        //              to "busy", to serve the customer
        //              specified by cCustomer, and the
        //              transaction time is set according to the
        //              parameter tTime.

    void setServerBusy(int serverID, customerType cCustomer);
        //Function to set a server as busy
        //Postcondition: The server specified by serverID is set
        //              to "busy", to serve the customer
        //              specified by cCustomer.

    void updateServers(ostream& outFile);
        //Function to update the status of a server.
        //Postcondition: The transaction time of each busy
        //              server is decremented by one unit. If
        //              the transaction time of a busy server
        //              is reduced to zero, the server is set
        //              to "free". Moreover, if the actual
        //              parameter corresponding to outFile is
        //              cout, a message indicating which customer
        //              has been served is printed on the screen,
        //              together with the customer's departing
        //              time. Otherwise, the output is sent to
        //              a file specified by the user.

private:
    int numOfServers;
    serverType *servers;
};
```

Figure 19-38 shows the UML class diagram of the class serverListType.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_1233_0.png)

FIGURE 19-38  UML class diagram of the class serverListType

Following are the definitions of the member functions of the class serverListType. The definitions of the constructor and destructor are straightforward.

```cpp
serverListType::serverListType(int num)
{
    numOfServers = num;
    servers = new serverType[num];
}

serverListType::~serverListType()
{
    delete [] servers;
}
```

The function `getFreeServerID` searches the list of servers. If a free server is found, it returns the server’s ID; otherwise, the value −1 is returned, which indicates that all of the servers are busy. The definition of this function is:

```cpp
int serverListType::getFreeServerID() const
{
    int serverID = -1;

    int i;

    for (i = 0; i < numOfServers; i++)
        if (servers[i].isFree())
        {
            serverID = i;
            break;
        }

    return serverID;
}
```

The function `getNumberOfBusyServers` searches the list of servers and determines and returns the number of busy servers. The definition of this function is:

```cpp
int serverListType::getNumberOfBusyServers() const
{
    int busyServers = 0;

    int i;

    for (i = 0; i < numOfServers; i++)
        if (!servers[i].isFree())
            busyServers++;

    return busyServers;
}
```

The function `setServerBusy` sets a server to busy. This function is overloaded. The serverID of the server that is set to busy is passed as a parameter to this function. One function sets the server’s transaction time according to the parameter `tTime`; the other function sets it by using the transaction time stored in the object `cCustomer`. The transaction time is later needed to determine the average wait time. The definitions of these functions are:

```cpp
void serverListType::setServerBusy(int serverID,
                                    customerType cCustomer,
                                    int tTime)
{
    servers[serverID].setBusy();
    servers[serverID].setTransactionTime(tTime);
    servers[serverID].setCurrentCustomer(cCustomer);
}

void serverListType::setServerBusy(int serverID,
                                  customerType cCustomer)
{
    int time;

    time = cCustomer.getTransactionTime();

    servers[serverID].setBusy();
    servers[serverID].setTransactionTime(time);
    servers[serverID].setCurrentCustomer(cCustomer);
}
```

The definition of the function updateServers is quite straightforward. Starting at the first server, it searches the list of servers for busy servers. When a busy server is found, its transactionTime is decremented by 1. If the transactionTime reduces to zero, the server is set to free. If the transactionTime of a busy server reduces to zero, then the transaction of the customer being served by the server is complete. If the actual parameter corresponding to outFile is cout, a message indicating which customer has been served is printed on the screen, together with the customer’s departing time. Otherwise, the output is sent to a file specified by the user. The definition of this function is as follows:

```cpp
void serverListType::updateServers(ostream& outFile)
{
    int i;

    for (i = 0; i < numOfServers; i++)
        if (!servers[i].isFree())
        {
            servers[i].decreaseTransactionTime();

            if (servers[i].getRemainingTransactionTime() == 0)
            {
                outFile << "From server number " << (i + 1)
                        << " customer number "
                        << servers[i].getCurrentCustomerNumber()
                        << "\n     departed at time unit "
                        << servers[i].
                           getCurrentCustomerArrivalTime()
                           + servers[i].
                           getCurrentCustomerWaitingTime()
                           + servers[i].
                           getCurrentCustomerTransactionTime()
                        << endl;
                servers[i].setFree();
            }
        }
}
```
