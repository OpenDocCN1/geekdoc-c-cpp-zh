# LISTING 25.13 Continued

```
QUEUEHANDLE hSource,
DWORD dwTimeout,
DWORD dwAction,
MQMSGPROPS* pMessageProps,
LPOVERLAPPED lpOverlapped,
HANDLE hCursor );

//Application entry point
int main()
{
    //Masthead
    wprintf(L"Pong messages receiving applications\n\r");

    //Create the quit event
    HANDLE hQuitEvent = CreateEvent(NULL,true,false,NULL);
    if ( NULL == hQuitEvent )
        return GetLastError();

    //Create the message handling thread
    DWORD dwThreadId;
    HANDLE hThread = CreateThread(
        NULL,
        0,
        HandleMessages,
        hQuitEvent,
        0,
        &dwThreadId);

    if ( NULL == hThread )
        return GetLastError();
    wprintf(L"Created message handler thread %x\n",dwThreadId);

    //Wait for user to exit
    wprintf(L"\nPress any key to exit\n\n");
    getch();

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
```