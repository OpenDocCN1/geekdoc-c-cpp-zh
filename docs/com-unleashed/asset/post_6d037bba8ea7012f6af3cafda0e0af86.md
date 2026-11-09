
when security is turned off for a package, IsCallerInRole() always returns TRUE. Therefore, before using IsCallerInRole(), you must check to see if security is available. Listing 15.2 shows you how to test for security at the method level.

## LISTING 15.2 Testing for Security at a Method Level

```cpp
HRESULT MyObj::SecuredMethod()
{
    IObjectContext *pContext=NULL;
    HRESULT hr = GetObjectContext(&pContext);
    if (SUCCEEDED(hr))
    {
        if (!pContext->IsInTransaction())
            return E_ACCESSDENIED;
        BSTR bstrAdmin = SysAllocString(L"Admins");
        BOOL bInRole=FALSE;
        if (!pContext->IsCallerInRole(bstrAdmin,&bInRole))
        {
            SysFreeString(bstrAdmin);
            return E_ACCESSDENIED;
        }
        pContext->Release();
        return S_OK;
    }
    // Add your security code here
    return S_OK;
}
```

## Direct Caller Versus Original Caller

MTS performs role-based security when a client outside MTS communicates with an object inside MTS. When an object inside MTS makes a method call on another MTS object, MTS does not check security. Consider an example in which a client has access to method1 in objectA, but does not have access to method1 in objectB. If the client calls method1 in objectA, objectA has access to method1 in objectB and could potentially call it. Because MTS does not check security for MTS objects calling other MTS objects, the client will not be stopped from performing this type of sequence. This could pose a security problem.

However, MTS does provide several APIs to help you determine the identity of a client. MTS distinguishes between the original caller (the client that accessed the first COM object in the chain) and the direct caller (the caller that made the method call). You can obtain the security identifiers for both the Original Caller and the Direct Caller using the methods in the ISecurityProperty interface. This interface has five methods: GetDirectCreatorSID, GetOriginalCreatorSID, GetDirectCallerSID, GetOriginalCallerSID, and ReleaseSID. To reach this interface, call QueryInterface on the context object.

Listing 15.3 demonstrates how to use the ISecurityProperty interface.

## LISTING 15.3 The ISecurityProperty Interface

```cpp
IObjectContext* pContext = NULL;
ISecurityProperty* pISecProp = NULL;
PSID psid = NULL;
HRESULT hr = S_OK;
// Get the object context
hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    // Get a reference to the ISecurityProperty interface
    hr = pContext->QueryInterface( IID_ISecurityProperty,
        (void**)&pISecProp);
    // Obtain the creator's security ID
    hr = pISecProp->GetDirectCreatorSID(&psid);
    // Add your security code here
    // Release the security ID
    pISecProp->ReleaseSID(psid);
    // Release the interface
    pISecProp->Release();

    // Release the context
    pContext->Release();
}
```

## Load Balancing

This section discusses load balancing, and suggests a technique for programmatically performing load balancing. Chapter 20, “Load Balancing and Pooling,” goes into the nitty gritty details with a sample application. The basic goal behind load balancing is to improve server performance. Performance can be measured in many ways, but for the sake of this discussion, it means two things: more users and faster response.

There are two types of load balancing: dynamic and static. Dynamic load balancing occurs when the operating system can choose, based on performance statistics, which server will be most suited to run the components requested by the client. Static load balancing occurs when a program determines which server should handle a request based on fixed quantities (for example, if there are more than 50 users making requests, use server B).

Because MTS and Windows NT Server 4 cannot perform dynamic load balancing, the simplest way to perform load balancing is to make your distributed applications more scalable by having multiple servers export the same package and then letting the clients decide on which server they want to run. A more complicated and robust technique might involve creating a load-balancing package.

![](img/112c2326f49d26b8d59aa054e14c5747_420_0.png)

Using this technique, every client communicates with the load balancing package. The load balancing package’s job is to create instances of middle-tier components based on either an algorithm or a round-robin approach.

Microsoft offers several products that can help with load balancing, including Microsoft Cluster Server (MSCS). MSCS allows several Windows NT Enterprise Server computers to act as a single unit. Although a full discussion of MSCS is beyond the scope of this chapter, you can find more information about this product by visiting the Microsoft Web site, www.microsoft.com/Windows/server/Technical/management/ClusterArch.asp.

## Creating MTS-Based Applications

One of the key goals in transaction-based applications is to perform a transaction as quickly as possible. When the transaction is occurring, database systems place locks on the data to prevent other applications from looking at intermediate data.

Locking prevents concurrency, which is a detriment to scalability. To improve scalability, you must design your objects so that they do not spend much time in the actual transaction. Essentially, this can be best accomplished by method calls with finer granularity. Granularity is discussed at length in Chapter 20, and transaction optimization is discussed in Chapter 16, “COM+ as a Component Manager.”

Two aspects determine the longevity of a transaction. One involves the interception mechanism in MTS, specifically JIT. The other involves the timeout feature in MTS that automatically aborts a transaction in a specified amount of time. To understand these two forces, you must first understand how transactions operate in MTS.

Recall that activities are groups of objects with the same concurrency requirements. In MTS 2, when a base client creates an MTS object, MTS creates a new activity and puts the object instance in it. This object can, in turn, invite other objects to be part of the activity using the CreateInstance() function in the IObjectContext interface (recall that you obtain IObjectContext from the GetObjectContext() API).

Also, remember that only objects which are part of the same activity can vote on a transaction. Transactions have a single entry point and begin when an object marked Requires a Transaction or Requires a New Transaction is activated.

You might recall also that an object is activated when a client makes the first method call. Thus, an object is first created when the client requests to create the object, but is not activated until the first method call. The vote an object makes is stored in the context wrapper. Therefore, voting begins when the object is activated and ends when the object is deactivated.

When the root of the transaction is destroyed, MTS will either commit the transaction or abort it. If an object needs, more precisely, to be part of the transaction, it must be created from within the first object and it must be invited into the same activity. Because MTS 2 was built after COM was released, an object in an activity cannot use the standard COM APIs to create an MTS component within the same activity. If you were to use `CoGetClassObject()` or `CoCreateInstance()`, the object would be part of a separate activity. To create an object that is part of the same activity, use the `CreateInstance()` method in the `IObjectContext` interface.

The following example shows how to invite an object `CLSID_FriendObject` into the same activity.

```cpp
IObjectContext *pContext;
HRESULT hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    IFriendObject *pFriendObject;
    pContext->CreateInstance(CLSID_FriendObject,
        __uuidof(pFriendObject),
        (void **)&pFriendObject);
}
```

When an object’s context wrapper is gone, the vote cannot be changed. A context wrapper keeps track of the vote status on what is commonly called the “happy” flag. A vote of yes means the object is “happy,” a vote of no means the object is “unhappy.” If the context wrapper gets destroyed in an unhappy state, the transaction will be doomed. Two styles of voting can occur. One style is to make a temporary vote; another style is to make a final vote. With a temporary vote, an object is indicating that it can change its mind. (“I’m unhappy, but perhaps if you make another method call, I can be persuaded to be happy.”) With a permanent style, an object says, “I’m unhappy (or happy) and there is nothing anyone can do to change my mind.” The object controls the state of happiness by calling one of two methods in the `IObjectContext` interface: `EnableCommit()` and `DisableCommit()`. `EnableCommit()` sets the state of the “happy” flag to happy, and `DisableCommit()` sets the state to unhappy. The following code shows how to call these methods:

```cpp
IObjectContext *pContext;
HRESULT hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    pContext->EnableCommit();
    pContext->Release();
}
```

`EnableCommit()` and `DisableCommit()` do a temporary vote—they do not affect the lifetime of the context wrapper; they only affect the state of the happy bit. If the object is destroyed and the context wrapper with it, at that point the last vote will be final.
