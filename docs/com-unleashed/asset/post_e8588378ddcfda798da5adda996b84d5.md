
## LISTING 27.3 Continued

```cpp
AfxMessageBox("The display name param is invalid");
}
else if (MK_E_NOBJECT == hr)
{
    AfxMessageBox("Object could not be found");
}
else if (MK_E_INTERMEDIATEINTERFACENOTSUPPORTED == hr)
{
    AfxMessageBox("Object does not support required interface");
}
else if (ERROR_NOT_AUTHENTICATED == hr)
{
    AfxMessageBox("auth");
}
else
{
    AfxMessageBox("Unknown error occurred");
}

return;
}

pInteraction->DisplayMessage(bstrMessage);
pInteraction->Release();
pInteraction = NULL;

::CoUninitialize();

AfxMessageBox("Your message has been queued");
}
else
{
    AfxMessageBox("please enter a string to send to the queued component.");
}
```

Because some of this code is not very obvious, take a minute to walk through it to understand what is required on the client side.

The first thing the function does is to call UpdateData(FALSE) in order to retrieve the value that is entered on the dialog into the m_strMessage member variable. When that is done, a simple trimming of white space and verification that the string wasn't NULL takes place.

Now, we get to some basic COM stuff. A pointer to the IInteraction interface is declared as well as an HRESULT variable. After that is done, the m_strMessage member function, AllocSysString is called in order to convert from a CString to a BSTR. After COM is initialized in this thread (using ::CoInitialize), the fun begins.

As you’re aware by now, you normally instantiate COM objects with a call to the ::CoCreateInstance or ::CoCreateInstanceEx functions or a call to a class factory’s CreateInstance method. So what is this ::CoGetObject function? It is used to create a connection to the component. Actually, this function creates and connects the client to a special Queued Component object called a Recorder. If you read the Queued Components Architecture section earlier in the chapter, you learned that this object acts as a proxy in the component’s stead. However, the key issue here is that this client application code has absolutely no idea that it isn’t talking directly to the component itself. Such is the beauty of the Queued Components service and the reason why the ::CoGetObject function is used. This function acts as a layer of abstraction so that the client code doesn’t have to worry about the details of how to connect to a component that might not even be available (because of being disconnected from the server) or how to deal with MSMQ (because this code might be used in a nondistributed environment one day). With Queued Components, you get the best of both worlds: a distributed solution for disconnected clients from a code base that works in both a distributed and a stand-alone environment.

Because this function is so instrumental in making this whole thing work, look at the ::CoGetObject function a bit more closely. The first thing you probably notice is the strangely formatted string as the first parameter. Actually, this string is really two parameters in one (delimited by a / character) and is called the component’s *display string*.

```text
queue:new:QCCompVC.Interaction.1
```

The first part of the string (up to the / character) is called the *queue moniker*. A moniker is a COM+ object that takes a string argument and from that knows how to create and initialize other COM/COM+ objects. As with all monikers, ProgID is associated with the queue moniker, and it is actually called—with the information after the colon being passed—an initialization string. Figure 27.17 shows an example Registry and the queue moniker entry in the HKEY_CLASSES_ROOT hive.

We will jump a bit ahead of ourselves and ask what values could be passed to the queue moniker. The most often-used parameter is the ComputerName. This value is how you specify where the component resides on your network. As an example, say that the component was installed on a server called MyBigBadNtServer. If that were the case, the line would read as follows:

```text
queue:ComputerName=MyBigBadNtServer/new:QCCompVC.Interaction.1
```

**FIGURE 27.17**  
All monikers have an entry in the Registry that enables the COM runtime to create the appropriate object.

![](img/112c2326f49d26b8d59aa054e14c5747_768_0.png)

Now, when the queue moniker creates the queue object, it passes the value `ComputerName=MyBigBadNtServer`. It is then up to the queue object to know what to do with that information. What happens if you simply omit the queue moniker? Because the queue moniker is simply used to activate MSMQ, Windows 2000 would not know to use MSMQ and would attempt to create the component for you. If the component were available on the local machine, the code would work. If the component were only available on a remote machine through which Windows 2000 would need to use MSMQ, the call would fail. Table 27.1 contains the other parameters you should be familiar with regarding the use of queue monikers.

The second part of the component’s display string is the new moniker. As you can probably guess from the context of the call, this moniker is used to create the specified component and to access the specified method.

### TABLE 27.1 — Queue Moniker Parameters and Descriptions

| Parameter | Description |
|---|---|
| `AppSpecific` | This is very similar to the “window word” that can be passed to a newly created window. It is completely up to the component developer as to what information needs to be passed here. The only constraint you have is that the value must be of type unsigned integer. |
| `AuthLevel` | This value is used to specify the level of authentication that MSMQ is to use in verifying the message. Authenticated messages are digitally signed and require a registered certificate.<br><br>**NOTE:** Although you can alter the authentication level for a COM+ application through Component Services, this parameter seems to be ignored. |
| `ComputerName` | As you saw, this parameter is used to resolve to the actual server where the target component resides. If this parameter is omitted, Windows 2000 assumes that the component exists on the client (or local) machine. |
| `Delivery` | Used to determine which mode of delivery MSMQ is to use for the message (MSMQ_DELIVERY_RECOVERABLE or MSMQ_DELIVERY_EXPRESS). |
| `EncryptAlgorithm` | This parameter enables the caller to specify the type of encryption algorithm being used. Valid entries are CALG_RC2 and CALG_RC4. |
| `FormatName` | Instructs MSMQ that a GUID is being used for the queue instead of the queue name. A MSMQ queue's GUID can be located by looking at its properties dialog from the Computer Management snap-in. |
| `HashAlgorithm` | Defines which hash algorithm is used to encrypt the message. Any of the following are valid: CALG_HMAC, CALG_MAC, CALG_MD2, CALG_MD4, CALG_MD5, CALG_SHA, CALG_SHA1, CALG_SHAMD5, CALG_SSL3, and CALG_TLS1PRF. |
| `Journal` | This specifies if a journal is to be used to track a message as it flows through a system. This value defaults to MSMQ_JOURNAL_NONE, which means no journal. You can track all messages by specifying MSMQ_JOURNAL. However, one really useful value is MSMQ_DEADLETTER, which allows you to track only messages that are sent to the dead letter queue. |
| `Label` | This value is for message tracking. For example, if you created a convention for labeling all your messages, it wouldn’t be difficult to write an administrator application that could provide information on the types of messages being routed to the dead letter queue. |
| `MaxTimeToReachQueue` | As its name implies, this value allows you to specify (in seconds) the amount of time a message can take in reaching its destination. Aside from a numeric value, you can also use the values LONG_LIVED or INFINITE. |
| `MaxTimeToReceive` | This value is slightly different from MaxTimeToReachQueue. Although that value is only concerned with how long the message takes in reaching the queue, this value is concerned with how long it takes the message to be dequeued, or to be read out of the queue. Once again, the valid values are a numeric value indicating the time in seconds, LONG_LIVED or INFINITE. |
