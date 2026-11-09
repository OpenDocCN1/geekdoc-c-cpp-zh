
are scheduled in a FIFO fashion as their objects of desire become available. This is only fair in the context of thread scheduling, but in the context of IOCPs, it’s a context-switching nightmare. One of the best things you can do to improve overall system performance is to let any thread that is running continue to run. Saving the current thread and then selecting and loading a new thread is not a cheap operation, nor is faulting all the new thread’s resources back into memory. In the case of an IOCP application, we don’t care which thread runs, just as long as the messages get handled. For this reason, NT schedules threads waiting on IOCPs in LIFO order. Threads that have been waiting the shortest period of time (sometimes not at all) are the most likely to have all their necessary state in cache or at least main memory.

Okay, how do we use these miraculous IOCPs? I’m sure that you’ll like the fact that there are only three functions directly associated with IOCPs:

- `CreateIoCompletionPort()`
- `PostQueuedCompletionStatus()`
- `GetQueuedCompletionStatus()`

`CreateIoCompletionPort()` creates a new IOCP, as you might expect. It is also the routine used to associate logical device (file) handles with the port. Simply call `CreateIoCompletionPort()` to create the IOCP and get a handle to it; then pass the handle back in on subsequent calls with the handle of the logical device to associate with the port.

When creating a thread within, the process can start several asynchronous I/O operations and then wait on the IOCP by calling `GetQueuedCompletionStatus()`. If an asynchronous I/O completes while your threads are waiting on the IOCP, the NT scheduler will select the best thread to wake up, leaving the threads that are scheduled to disk sleeping. The `GetQueuedCompletionStatus()` supplies a key to your application when it returns. This key is set when you originally called `CreateIoCompletionPort()` and can be different with each `CreateIoCompletionPort()` call. Developers often use this to identify which logical device has completed I/O.

The final routine, `PostQueuedCompletionStatus()`, is used to send I/O completion messages to waiting threads. This is most handy for waking up the I/O threads when it’s time to quit.

The sample program in Listing 25.14 is a variation on the Shipping Server for our sweater company that makes use of four threads and I/O completion ports to improve message processing speed. The main routine creates the IOCP and associates it with the shipping queue. The main function goes on to create four threads and set them about retrieving orders. At this point, the main routine waits for you to instruct it to exit the process. When you do, it sends a message to the shipping threads indicating they should quit, and then waits for them to do so before exiting.

The threads in the Ship() routine set up their message buffer as usual and prepare to receive. The MQReceiveMessage() called here is a little different from the usual in that it is asynchronous. You are thus obliged to pass it an overlapped structure that has been initialized to the defaults. Because your Receive call is asynchronous, you can wait for the completion port. When the completion port routine returns, you check status and then continue processing the message. When you're done, it starts all over again. Have a look.

### LISTING 25.14 Using I/O Completion Ports to Process MSMQ Messages

```cpp
// Shipper.cpp
//
// Order shipping application

//Dependencies
#include <windows.h>
#include <stdio.h>
#include <conio.h>
#include <transact.h>
#include <mq.h>


//Symbols
#define FORMATNAMESIZE    64
#define MSGBODYSIZE       128
#define MSGLABELSIZE      64
#define QUEUEPATHNAME     L".\\ShippingQueue"
#define THREADCOUNT       4
#define QUITKEY           0
#define MSMQKEY           5


//Data structures
struct ShippingRequest
{
    long Account;
    long Product;
    long Quantity;
};
struct ThreadInfo
{
    QUEUEHANDLE hQueue;
    HANDLE hIOCP;
};

//Prototypes
DWORD WINAPI Ship( LPVOID pv );
bool ExecuteSlowestLinkShippingRequest( long, long, long );

//Application entry point
int main()
{
    ThreadInfo ti; // Thread information structure used by IO threads

    //Masthead
    wprintf(L"I/O Completion Port Sweater Shipping Application\n\n");

    //Get the format name of the queue using the pathname
    HRESULT hr;                         //Return status
    WCHAR wcsFormatName[FORMATNAMESIZE]; //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE; //Size of format name
    hr = MQPathNameToFormatName(
                         QUEUEPATHNAME,
                         wcsFormatName,
                         &dwFormatNameLen );

    if ( FAILED(hr) )
        return hr;

    //Open the queue with receive access
    hr = MQOpenQueue( wcsFormatName,       //Queue format name
                      MQ_RECEIVE_ACCESS,  //Access requested
                      MQ_DENY_NONE,       //Share mode
                      &(ti.hQueue) );     //Queue handle

    if ( FAILED(hr) )
        return hr;

    //Create IOCP that lets SYSTEM_PROCESS many threads run
    ti.hIOCP = CreateIoCompletionPort(ti.hQueue,NULL,MSMQKEY,0);
    if ( NULL == ti.hIOCP )
        return GetLastError();

    //Create I/O threads
    HANDLE ahThreads[THREADCOUNT];
    for ( int i = 0; i < THREADCOUNT; i++ )
    {
        DWORD dwThreadId;
        ahThreads[i] = CreateThread(NULL,0,&Ship,&ti,0,&dwThreadId);
        if ( NULL == ahThreads[i] )
            return GetLastError();
        wprintf(L"Created thread %d\n", dwThreadId);
    }

    //Wait for user to exit
    wprintf(L"\nPress a key to exit\n\n");
    getch();

    //Notify threads that supper's ready and wait for them to quit
    for ( int i = 0; i < THREADCOUNT; i++ )
        PostQueuedCompletionStatus(ti.hIOCP,0,QUITKEY,NULL);
    wprintf(L"Waiting for I/O threads to exit...\n");
    WaitForMultipleObjects(THREADCOUNT,ahThreads,true,INFINITE);

    //Close completion port and queue and return success
    CloseHandle(ti.hIOCP);
    MQCloseQueue(ti.hQueue);
    wprintf(L"Exiting...");
    Sleep(3000);
    return 0;
}

DWORD WINAPI Ship( LPVOID pv )
{
    HRESULT hr;
    ThreadInfo * pti = (ThreadInfo *) pv;

    //Create the overlapped event
    HANDLE hEvent = CreateEvent(NULL,false,false,NULL);
    if ( NULL == hEvent )
        return GetLastError();

    //Set up Overlapped structure for async reads
    OVERLAPPED ol = {0,0,0,0, hEvent};
    LPOVERLAPPED pol = &ol;

    //Allocate message property objects
    MQMSGPROPS MsgProps;        //Message properties struct
    MSGPROPID aMsgPropId[4];    //Message property id array
    PROPVARIANT aMsgPropVar[4]; //Message property value array

    //Set up message property struct
    MsgProps.cProp = 4;         //Number of properties
    MsgProps.aPropID = aMsgPropId; //Ids of properties
    MsgProps.aPropVar = aMsgPropVar; //Values of properties
    MsgProps.aStatus = NULL;    //NO error reports

    //Set up message label and length
    WCHAR wcsLabel[MSGLABELSIZE]; //Message label buffer
    aMsgPropId[0] = PROPID_M_LABEL;
    aMsgPropVar[0].vt = VT_LPWSTR;
    aMsgPropVar[0].pwszVal = wcsLabel;
    aMsgPropId[1] = PROPID_M_LABEL_LEN;
    aMsgPropVar[1].vt = VT_UI4;

    //Set up message body and length
    WCHAR wcsBody[MSGBODYSIZE];        //Message body buffer
    aMsgPropId[2] = PROPID_M_BODY;
    aMsgPropVar[2].vt = VT_UI4;
    aMsgPropVar[2].caub.cElems = (LPBYTE)wcsBody;
    aMsgPropVar[2].caub.pElems = sizeof(WCHAR);
    aMsgPropId[3] = PROPID_M_BODY_SIZE;
    aMsgPropVar[3].vt = VT_UI4;

    //Get messages
    while ( TRUE )
    {
        //We have to reset these because they are [in,out] params
        aMsgPropVar[1].ulVal = MSGLABELSIZE;
        aMsgPropVar[3].ulVal = MSGBODYSIZE;

        //Get message from queue
        hr = MQReceiveMessage(
            pti->hQueue,      //Queue to receive from
            INFINITE,         //Timeout
            MQ_ACTION_RECEIVE, //Receive or peek
            &MsgProps,        //Message properties
            &ol,              //Overlapped structure
            NULL,             //Callback routine
            NULL,             //Queue cursor
            NULL );           //Transaction

        //Check results
        if ( FAILED(hr) )
        {
            wprintf(L"Error receiving message: %x\n\n", hr);
            break;
        }

        if ( MQ_INFORMATION_OPERATION_PENDING == hr )
            wprintf(L"IO pending on thread %x\n", GetCurrentThreadId());

        //Wait for IO
        DWORD dwBytesIn;
        DWORD dwKey;
        BOOL b = GetQueuedCompletionStatus( pti->hIOCP,
                                            &dwBytesIn,
                                            &dwKey,
                                            &pol,
                                            INFINITE );

        if ( !b )
        {
            wprintf(L"IO Port error %x\n", GetLastError());
            break;
        }

        //Check for quit message from main thread
```
