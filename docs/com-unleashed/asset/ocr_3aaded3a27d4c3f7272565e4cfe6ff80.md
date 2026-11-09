# LISTING 25.14 Continued

```
```cpp
//Notify threads that supper's ready and wait for them to quit
for ( i = 0; i < THREADCOUNT; i++ )
    PostQueuedCompletionStatus(ti.hIOCP,0,QUITKEY,NULL);
wprintf(L"Waiting for I/O threads to exit...\n");
WaitForMultipleObjects(THREADCOUNT,aThreads,true,INFINITE);

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
```
```