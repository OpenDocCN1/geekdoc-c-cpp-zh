
## TABLE 27.1 Continued

| Parameter | Description |
|---|---|
| **PathName** | This parameter allows you to fully qualify a path to the server queue (specifying both computer name and queue name) in the format `<server name>/<queue name>`. |
| **Priority** | One of the most important values in any distributed system, this enables the application to prioritize the outgoing messages so that the server can be used as efficiently as possible. If you don't specify a value for this parameter, the Priority setting for the queue is used. |
| **PrivLevel** | Used to define the message's "privacy level." The valid values are `MQMSG_PRIV_LEVEL_NONE`, `MQMSG_PRIV_LEVEL_BODY`, `MQMSG_PRIV_LEVEL_BODY_BASE`, and `MQMSG_PRIV_LEVEL_BODY_ENHANCED`. |
| **QueueName** | Explicitly tells MSMQ which queue to use. If you don't specify this parameter (which the demo doesn't), the queue associated with the server application is used. Specifying both the ComputerName and the QueueName parameters is the functional equivalent of using the PathName parameter. |
| **Trace** | The value determines if the message gets traced as it moves from the client to its destination (the server application). The valid values are `MQMSG_TRACE_NONE` and `MQMSG_SEND_ROUTE_TO_REPORT_QUEUE`. |

After the `::CoGetObject` call, the function verifies that everything succeeded by checking the returned HRESULT structure. You can find a full list of the possible error types in the winerror.h header file.

If you get past the checking of the returned HRESULT structure, the function succeeded and the Queued Component Recorder object has been created. At this point, it can be used just as if you had a pointer to the actual object itself, which is exactly why the next call is to the IInteraction::DisplayMessage method (passing to it the BSTR value converted earlier).

Finally, in the name of good housekeeping, the interface pointer is released and `::CoUninitialize` is called. If all went well, you will see a message box proclaiming, "Your message has been queued".

The last thing you need to do before building the demo test application is to include a couple of files at the top of the QCClientVCDlg.cpp file. These files are the QCCompVC.h header file (which defines the IInteraction interface) and QCCompVC_i.c file (which defines the IID_IInteraction structure).

## Testing the Component and Client Code

And now, we have arrived at the moment of truth. It’s time to test the application. To test the application, simply run your client, type in the necessary information, and click OK. If you do that, you should see results similar to those shown in Figure 27.18.

**FIGURE 27.18**

If everything works correctly, the fact that the server application isn’t running won’t stop the client from functioning properly.

![](img/112c2326f49d26b8d59aa054e14c5747_771_0.png)

> **Tip**
>
> If you are receiving an error trying to send the message, the problem might be that you are running in a Workgroup installation. For security to work, you must be running on a Windows 2000 domain. The way around this problem is simple: From Component Services, right-click the COM+ application and select the Properties menu option. From there, click on the Security tab and set the Authentication Level for Calls to None.

After clicking OK and waiting a minute or two, you might be wondering where the message is from the server confirming that the message was received. The reason you don’t see that message is that we haven’t started the server application yet. First I wanted you to see that the client application would proceed along just fine without the server application/component even running.

At this point, switch to the Component Services and right-click your COM+ application. From the context menu, select the Start menu option. Depending on how impatient you were in getting your messages to display, you should now see something similar to what is shown in Figure 27.19.

*FIGURE 27.19* When the server application starts up, it begins to read in its queued messages and responds accordingly.

![](img/112c2326f49d26b8d59aa054e14c5747_772_0.png)

## Exporting the COM+ Application

Up to now, we've worked almost exclusively on one machine (except when you learned how to use the queue moniker to resolve to a different computer name). In other words, you created the demo server application/component and installed it on the same machine as the client application. However, what happens when the client application gets moved or copied to another machine? The task is referred to as COM+ Application exporting and as you might suspect, Component Services has a tool for handling this obvious need.

To export a COM+ Application, simply select and right-click the desired COM+ application from the Component Services tree view. When the context menu is displayed, select the Export menu option. This action will invoke the COM+ Application Export Wizard. When the first page of this wizard is displayed, click the Next button. You should now see a page that enables you to specify where you want the exported application file to be created. Simply browse to the selected folder and enter the name of the installation file. As you can see in Figure 27.20, the demo uses the name QCCompInst.msi (MSI is the extension for a Microsoft Installation file). Another change you need to make to the page is the application type. Select the Application Proxy radio button so that requests for your component are directed to the server and not the local machine.

*FIGURE 27.20* Installing a COM+ Application on another machine requires the use of the COM+ Application Export Wizard.

![](img/112c2326f49d26b8d59aa054e14c5747_772_1.png)

Now, click the Next button to create the installation file. This shouldn’t take long because the demo application you’ve built is small. After the installation file is built, you will see a page confirming that fact. Click the Finish button to exit the wizard.

Go to the client machine where you want to install the COM+ Application. Assuming that you have either copied the installation file to a client machine or the client machine has access to the installation file (such as on a network), browse to the installation file in an Explorer window and right-click it. From the file’s context menu, select the Install option. As shown in Figure 27.21, you will see a small dialog with a progress bar that shows the application being installed on the client machine.

**FIGURE 27.21**

*In order to deploy your COM+ Applications to the client machines, create an installation application using the COM+ Application Export Wizard and then run that application on the target client.*

![](img/112c2326f49d26b8d59aa054e14c5747_773_0.png)

At this point, if you open the Component Services, you will see a new application called QCCompInst. The only thing to keep in mind here is that this is not the real application that exists on the server. Rather, it is a proxy that allows the client to function properly without the presence of the real server-side application. One key point to also make is that you will find your development cycle to be much easier if you completely test the component and client on one machine before deploying the application.

## Summary

In this chapter, you began your quest for COM+ Queued Components knowledge by being introduced to a high-level overview of the service and when it would be applicable to use. You then went much deeper and discovered the Queued Components architecture and data flow involving the three main objects: Recorder, ListenerHelper, and Player. After this information had been dispensed, you then learned how to write both the client and component side of a queued component arrangement. Finally, you discovered how to test your client and component and how to deploy your application to production clients.

## INDEX

- method-timing, 534-536
- response time, 521
- optimization, 544
- **Apache**, 21
- **apartment-threaded server model**, 156
  - concurrency issues, 162
  - creating, 156
  - objects, 161
- **apartments**, 60-61, 155
- **API functions**
  - access tokens, 310
  - security descriptors, 303
  - SIDs, 309
- **APIs, 440. See also interfaces**
  - MOM system, 567
  - MSMQ, 588, 592
  - registry API (Registry class), 172-179
  - SafeRef() function, 440-441
  - StringFromCLSID(), 182
  - WideCharToMultiByte(), 182
- **AppID registry subkeys**, 327
- **AppIDs** *(HKEY_CLASSES_ROOT key)*
  - identity, 188
  - objects as services, 188
  - permissions, 186
  - remote activation, 187
  - remote in-process servers, 186
  - remote out-of-process servers, 186
  - security descriptors, 186-187
- **applets, Services**, 250-251
- **applications. See also packages; software**, 418
  - asynchronous communication, 23
  - ATL, #import directive, 620
  - availability
    - defined, 518
    - load balancing, 518-519
  - canceling outstanding calls, 70
  - client, 128
    - creating in Visual C++. See client applications
  - MSMQ, 572
  - storing CLSID, 75
  - components
    - adding, 739
    - changing Transaction property settings, 391
- coordinating transactions, 375
- **creating**
  - CASE tools, 49
  - COM+, 65
  - constraints, 43
  - consumer considerations, 45-46
  - DNA, 8
  - leveraging technology and skills, 44
  - MSMQ applications with smart pointers, 620
  - portability, 48
  - RAD, 44
  - raw COM+ interfaces, 606
  - reliability, 46
  - reusability, 49
  - scalability, 47
  - Visual Basic executables, 135
- **database**, 383
  - DCOM98 functionality, 362
  - defining, 736-738
  - deployment, 63
  - designing in MTS, 401
  - development, 561
- **distributed**
  - load balancing, 397
  - MSMQ, 378
- **DNA**
  - browsers, 20
  - compliance, 11
  - security, 13
  - Windows Registry, 12
- **enterprise**, 374
  - transactions, 444
  - troubleshooting, 542
- **exporting**, 749-750
- **Internet**
  - ASP, 22-23
  - interactivity, 20
  - stateless environments, 10
- **load balancing**, 15
- **maintainability**, 46
- **marking as queued**, 738-739
- **messaging**, 560, 565, 610
- **MSMQ**, 589
  - compiling, 589
  - creating with VBScript, 632
  - Hello, 590
  - MSMQ Explorer, 573
- multitiered design, 37-39
  - constraints, 43
  - identifying components, 41-42
  - interfaces, 43
  - layers, 40
- **names**, 737
- **PersistClient()**, 88
- **presentation code**, 32
- **prototypes**, 18
- **queued component**, 66
- **receiving messages**, 611
- **registry access**, 545
- **roles**, 477
- **scalability**, 389, 409, 567
  - deactivating standard COM+ components, 416-417
  - defined, 517
  - early deactivation, 409, 415, 426
  - just-in-time (JIT) activation, 409, 426, 522, 538-539
  - load balancing, 517-518
  - MTS, 401
  - pooling, 409-410, 415, 426
  - resource management, 409
  - standard COM+ component problems, 415-417
- **SecureSum**, 480
- **security**, 478
  - server security, 69
- **testing**, 748
- **three-tiered design**, 33-35
- **time-critical**, 44
- **TPS**, 542
- **transactions, concurrency**, 398
- **validation domain**, 39
- **version concerns**, 543
- **Web**, 9
- **AppSpecific parameter**, 745
- **aPropID field**, 591
- **aPropVar field**, 591
- **architectures**
  - COM+, 56, 58
  - coupled, 32
  - loosely, 33
  - multitiered, 40
  - constraints, 43
  - identifying components, 41-42
  - interfaces, 43
