# LISTING 25.12  Continued

```
```cpp
//Signal background thread to quit
SetEvent(hQuitEvent);
wprintf(L"\nWaiting for I/O thread to exit...\n");
WaitForSingleObject(hThread,INFINITE);

//Close thread and event handles and return success
CloseHandle(hThread);
CloseHandle(hQuitEvent);
wprintf(L"Exiting...");
Sleep(3000);
return 0;
}

DWORD WINAPI HandleMessages( LPVOID pv )
{
    //Recover quit event handle
    HANDLE hQuitEvent = (HANDLE) pv;

    //Get the format name of the queue using the pathname
    HRESULT hr;                              //Return status
    WCHAR wcsFormatName[FORMATNAMESIZE];     //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE;  //Size of format name
    hr = MQPathNameToFormatName(             P,QMPATHNAME,
                                             wcsFormatName,
                                             &dwFormatNameLen );
    if ( FAILED(hr) )
        return hr;

    //Open the queue with receive access
    HANDLE hQueue;
    hr = MQOpenQueue( wcsFormatName,         //Queue format name
                      MQ_RECEIVE_ACCESS,     //Access requested
                      MQ_DENY_NONE,          //Share mode
                      &hQueue );             //Queue handle
    if ( FAILED(hr) )
        return hr;

    //Create the overlap event
    HANDLE hIOEvent = CreateEvent(NULL,false,false,NULL);
    if ( NULL == hIOEvent )
        return GetLastError();

    //Set up the Overlapped structure for async reads
    OVERLAPPED ol = {0,0,0,0, hIOEvent};

    //Set up array of wait handles
    HANDLE ah[2];
```
```