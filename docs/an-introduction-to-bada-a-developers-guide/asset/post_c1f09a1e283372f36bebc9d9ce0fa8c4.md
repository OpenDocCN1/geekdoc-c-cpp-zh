
## Example 2: Using the Player Base Application

An alternative approach to playing a sound is to use the built-in media player, which can be accessed using the App::AppControl class. More information about accessing base applications can be found in the ‘Create an AppControl to interact with a base application’ recipe.
Figure R4.2 shows a sound playing in the built in player.
The built in media player can be launched using the following code:

```
ArrayList* pDataList = null;
pDataList = new ArrayList();
pDataList->Construct();
String* pData = null;
pData = new String(L"type:audio");
pDataList->Add(*pData);
String* pData2 = null;
pData2 = new String(L"/path:/Res/CanYouHearMe.mp3");
pDataList->Add(*pData2);
AppControl* pAc = AppManager::FindAppControlN
    (APPCONTROL_AUDIO, OPERATION_PLAY);
if(pAc)
{
    pAc->Start(pDataList, null);
    delete pAc;
}
pDataList->RemoveAll(true);
delete pDataList;
```

![](img/a257d5fd53a79a244a20e587cd2f08f6_396_0.png)

Figure R4.2 Playing a sound using the built-in media player base application.

## Hints, Pitfalls, and Related Topics

In this example we’ve played an audio file stored in the application’s /Res directory. We add this file to the project’s /Res directory in the bada IDE and this will be copied to the application’s /Res directory on the device or in the simulator.
bada supports up to 10 simultaneous player Media::Player instances, although the number of players that can actually be opened at one time will depend on the resources of the device.
Note that when playing a sound using both the Media::Player namespace and the built-in player application, bada does not check whether the device is

set to Silent Mode. The application needs to check whether Silent Mode is set using the System::SettingInfo class, and ask the user how they want to proceed.

## Related Recipes

- Add a Form to a Frame-based App
- Create an AppControl to Interact with a Base App

A network connection is a runtime session for a data network service, configured with network account settings. This recipe explains how to create either a default or custom network connection.

## Example 1: Create a Default Network Connection

To reduce the difficulties in setting up network connections, bada manages the default network connection (see Figure R5.1). If you do not specify a network connection when your application uses features such as sockets or HTTP, the default connection will be used.

![](img/a257d5fd53a79a244a20e587cd2f08f6_399_0.png)

Figure R5.1 Create a default network connection.

The following are the steps for creating and using a default network connection:

- 1. Request network services without specifying a network connection.
- 2. The network services receive the request and start the default network connection.
- 3. The network services access a remote network.

bada handles all of the work in creating a default network connection and all you need to do is use the APIs provided by classes such as Net::Socket and Net::Http without specifying a network connection. Using the default network connection does not require the NET privilege to be set; you only need to ensure that the appropriate privileges are set for any services you use such as SNS_SERVICE to use the SNS Gateway and HTTP to set up HTTP sessions.

## Example 2: Create a Custom Network Connection

If you need to specify a particular configuration in place of the defaults, you should create a custom network connection (see Figure R5.2).

The workflow for creating a custom network connection is as follows:

- 1. Use a NetAccountManager and NetAccountInfo object to configure the required connection settings.
- 2. Create and start a custom network connection using the custom settings.
- 3. Request network services with the network connection.
- 4. Network services accesses the remote network.

![](img/a257d5fd53a79a244a20e587cd2f08f6_400_0.png)

Figure R5.2 Creating a custom network connection.

The classes required to create a custom connection are part of the Net namespace. NetAccountManager and NetAccountInfo encapsulate the information necessary for the NetConnection class to create a connection. NetAccountManager is used to get the list of NetAccountIds that are later used to construct the NetConnection.

The NET and NET_ACCOUNT privileges are required to create a custom net connection.

This recipe consists of the following steps:

- 1. Implement an INetConnectionEventListener.
- 2. Construct NetAccountManager object.
- 3. Get the list of NetAccountIds from NetAccountManager object.
- 4. You can now start the connection with any of the NetAccountIds provided by this list.

Now we'll look at the code.

- 1. Derive your class from INetConnectionEventListener.

```
#include <FNet.h>

class MyClass :
public Osp::Net::INetConnectionEventListener
{
Osp::Net::NetConnection* pNetConnection;

void InitiateNetConnection();
void CloseNetConnection();

//NetConnection
void OnNetConnectionStarted(Osp::Net::NetConnection& netConnection,
result r);
```

```
void OnNetConnectionStopped(Osp::Net::NetConnection& netConnection, result r);
void OnNetConnectionSuspended(Osp::Net::NetConnection& netConnection);
void OnNetConnectionResumed(Osp::Net::NetConnection& netConnection);
};
```

## 2. Call the InitiateNetConnection() function:

- a. Construct a NetAccountManager object.
- b. Get the list of NetAccountIds via the NetAccountManager.
- c. Create the net connection instance with the NetAccountId of the desired net account.
- d. Register with NetConnectionListener.
- e. Call the start function of NetConnection.

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

namespace. To receive asynchronous notifications of `SecureSocket` events, you must register and maintain an event listener `ISecureSocketEventListener`. The `ISecureSocketEventListener` interface specifies the methods used for responding to different kinds of socket events. These events are only sent out when using a secure socket in a non-blocking mode. An event listener is added by calling `AddSecureSocketListener()`. When a secure socket event is generated, one of these methods is called.

This recipe consists of the following steps:

- 1. Derive a class from `ISecureSocketEventListener`.
- 2. Create secure client socket and connect it with server.
- 3. Send data over the connected socket.
- 4. Receive data over the connected socket.
- 5. Close the socket at the end.

Now we’ll look at the code.

- 1. Derive a class from `ISecureSocketEventListener` interface.

```
```cpp
#include <FNet.h>

class SocketsSecureExample :
        public Osp::Net::Sockets::ISecureSocketEventListener
{
public:
  SocketsSecureExample(void) {}
  ~SocketsSecureExample(void) {}

public:
  void CreateSecureSocket(void);
  void CloseSecureSocket(void);
  void SecureSendData(void);
  void SecureReceiveData(void);

  // ISecureSocketEventListener
  void OnSecureSocketConnected(Osp::Net::Sockets::SecureSocket& socket);
  void OnSecureSocketClosed(Osp::Net::Sockets::SecureSocket& socket,
      Osp::Net::Sockets::NetSocketClosedReason reason);
  void OnSecureSocketReadyToReceive(Osp::Net::Sockets::SecureSocket& socket);
  void OnSecureSocketReadyToSend(Osp::Net::Sockets::SecureSocket& socket);
  void OnSecureSocketServCertFailed(Osp::Net::Sockets::SecureSocket& socket);

private:
  Osp::Net::Sockets::SecureSocket* pSocket;
};
```
```
