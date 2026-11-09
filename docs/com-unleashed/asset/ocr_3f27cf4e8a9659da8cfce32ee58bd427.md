# **LISTING 7.4** Continued

```
```cpp
{
    ::CoInitialize(NULL);
    ////////////////////////////////
    // TODO
    // Add background processing code here
    //
    std::cout << "Hello World!" << std::endl;
    Sleep(1000);
    std::cout << "Goodbye World!" << std::endl;

    ::CoUninitialize();
    return 0;
}

int Apartment::DoWork()
{
    DWORD dw;
    HANDLE thread = ::CreateThread(NULL, 0, ThreadProc, NULL, 0, &dw);
    ::CloseHandle(thread);
    return 0;
}
```
```

Note that this thread type does not appear to have a message loop or a window. The call to the CoInitialize() function automatically creates its own message queue where the COM+ subsystem can place calls to objects and receive COM+ calls from clients that exist in other threads. This queue is created the first time it is needed.

Originally, each thread had to have its own apartment in order to communicate with the COM/COM+ subsystem. These apartments were called single-threaded apartments (STAs). When COM introduced the multithreaded apartment (MTA), the apartment thread became a misnomer; that is, apartments were no longer actually tied to one thread.

If you call the CoInitializeEx(NULL, COINIT_MULTITHREADED) function, your thread will start a multithreaded apartment. All threads created in the same process automatically have access to this multithreaded apartment. Each thread can still initialize its own single-threaded apartment by calling the CoInitialize(NULL) function, but the thread can exist in only one apartment (either one STA or one MTA).

In a process, a thread must enter an apartment before being able to use a COM object (through a call to CoInitializeEx()). COINIT_MULTITHREADED lets a thread enter the one and only multithreaded apartment and CoInitialize() lets the thread enter a single-threaded apartment.

The advantages and disadvantages of your choice of single-threaded or multithreaded apartment are discussed in detail later in this chapter in the section, “COM+ Threading Models.”