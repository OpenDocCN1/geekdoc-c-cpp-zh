```
```cpp
// server is decremented by one unit. If
// the transaction time of a busy server
// is reduced to zero, the server is set
// to "free". Moreover, if the actual
// parameter corresponding to outFile is
// cout, a message indicating which customer
// has been served is printed on the screen,
// together with the customer's departing
// time. Otherwise, the output is sent to
// a file specified by the user.

private:
    int numOfServers;
    serverType * servers;
};
```
```

Figure 17-38 shows the UML class diagram of the class `serverListType`.

![](bbox=[0.278, 0.403, 0.79, 0.617])

**FIGURE 17-38** UML class diagram of the class `serverListType`

Following are the definitions of the member functions of the class `serverListType`. The definitions of the constructor and destructor are straightforward.

```
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
```