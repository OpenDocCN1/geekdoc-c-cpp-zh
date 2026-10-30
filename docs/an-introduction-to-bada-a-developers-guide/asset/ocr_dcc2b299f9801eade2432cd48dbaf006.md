```
void OnNetConnectionStopped(Osp::Net::NetConnection& netConnection, result r)()
void OnNetConnectionSuspended(Osp::Net::NetConnection& netConnection)()
void OnNetConnectionResumed(Osp::Net::NetConnection& netConnection)
{};
;
```

# 2. Call the InitiateNetConnection() function:

+   a. Construct a NetAccountManager object.
+   b. Get the list of NetAccountIds via the NetAccountManager.
+   c. Create the net connection instance with the NetAccountId of the desired net account.
+   d. Register with NetConnectionListener.
+   e. Call the start function of NetConnection.

Note that this is an asynchronous function, and you will get a response in the callback function OnNetConnectionStarted().

```
void
MyClass::InitiateNetConnection()
{

    result r;

    NetAccountManager netMgr;

    r = netMgr.Construct();

    NetAccountId id;
    id = netMgr.GetNetAccountId(NET_BEARER_WIFI);
    pNetConnection = new NetConnection();
    r = pNetConnection->Construct(id);

    pNetConnection->AddNetConnectionListener(*this);
    pNetConnection->Start();

    if (null != pNetAccIdList)
    {
        pNetAccIdList->RemoveAll();
        delete pNetAccIdList;
        pNetAccIdList = null;
    }
}
```

3. As a result of calling pNetConnection->Start(), when the connection is started you will get a response in OnNetConnectionStarted().