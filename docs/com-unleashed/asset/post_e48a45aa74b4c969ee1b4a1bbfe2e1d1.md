
#### **LISTING 7.3** Continued

```cpp
// Add background processing code here
//
std::cout << "Hello World!" << std::endl;
Sleep(1000);
std::cout << "Goodbye World!" << std::endl;
break;
default:
    return DefWindowProc (hwnd, idMessage, wParam, lParam);
}
return (0L);
}

DWORD WINAPI Window::ThreadProc(void *p)
{
    WNDCLASSEX wndclass;
    static char szWndClassName[] = "Threading Example";

    wndclass.cbSize = sizeof (wndclass);
    wndclass.style = CS_HREDRAW | CS_VREDRAW;
    wndclass.lpfnWndProc = WndProc;
    wndclass.cbClsExtra = 0;
    wndclass.cbWndExtra = 0;
    wndclass.hInstance = ::GetModuleHandle(NULL);
    wndclass.hIcon = ::LoadIcon(NULL, IDI_APPLICATION);
    wndclass.hCursor = ::LoadCursor(NULL, IDC_ARROW);
    wndclass.hbrBackground = (HBRUSH) ::GetStockObject(WHITE_BRUSH);
    wndclass.lpszMenuName = NULL;
    wndclass.lpszClassName = szWndClassName;
    wndclass.hIconSm = ::LoadIcon(NULL, IDI_APPLICATION);

    RegisterClassEx (&wndclass);

    HWND hwnd;
    MSG msg;

    hwnd = CreateWindow (
        szWndClassName,
        "The Hello Program",
        WS_OVERLAPPEDWINDOW,
        CW_USEDEFAULT,
        CW_USEDEFAULT,
        CW_USEDEFAULT,
        CW_USEDEFAULT,
        NULL,
        NULL,
        GetModuleHandle(NULL),
        NULL);

    *(HWND *)p = hwnd;

    ShowWindow(hwnd, SW_SHOWNORMAL);
    UpdateWindow(hwnd);

    while (GetMessage(&msg, hwnd, 0, 0))
    {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }
    return msg.wParam;
}

int Window::DoWork()
{
    ::PostMessage(m_hwnd, MYMESSAGE, 0, 0);
    return 0;
}
```

You can see how the example differs from the previous message queue thread in that the thread creates a window and retrieves messages for that window.

### Apartment Threads

The last basic thread type is the apartment thread. Any thread used to execute calls to component objects is configured as “apartment threaded.” Each object “lives in an apartment” (thread) for the life of the object. All calls to that object execute on the apartment thread.

Listing 7.4 shows an example of a minimal apartment thread.

#### **LISTING 7.4** A Minimal Apartment Thread

```cpp
class Apartment
{
public:
    static DWORD WINAPI ThreadProc(void * p);
    int DoWork();
    Apartment();
    virtual ~Apartment();

};

Apartment::Apartment() {}

Apartment::~Apartment() {}

DWORD WINAPI Apartment::ThreadProc(void *p)
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

Note that this thread type does not appear to have a message loop or a window. The call to the CoInitialize() function automatically creates its own message queue where the COM+ subsystem can place calls to objects and receive COM+ calls from clients that exist in other threads. This queue is created the first time it is needed.

Originally, each thread had to have its own apartment in order to communicate with the COM/COM+ subsystem. These apartments were called single-threaded apartments (STAs). When COM introduced the multithreaded apartment (MTA), the apartment thread became a misnomer; that is, apartments were no longer actually tied to one thread.

If you call the CoInitializeEx(NULL, COINIT_MULTITHREADED) function, your thread will start a multithreaded apartment. All threads created in the same process automatically have access to this multithreaded apartment. Each thread can still initialize its own single-threaded apartment by calling the CoInitialize(NULL) function, but the thread can exist in only one apartment (either one STA or one MTA).

In a process, a thread must enter an apartment before being able to use a COM object (through a call to CoInitializeEx()). COINIT_MULTITHREADED lets a thread enter the one and only multithreaded apartment and CoInitialize() lets the thread enter a single-threaded apartment.

The advantages and disadvantages of your choice of single-threaded or multithreaded apartment are discussed in detail later in this chapter in the section, “COM+ Threading Models.”

### Thread Pools

Thread pools are not a thread type, but rather an implementation option. In other words, COM is using a thread pool to implement how COM calls to single- and multithreaded apartments. Any of the previous four thread types could be extended to provide for a thread pool. Listing 7.5 shows an example of a thread pool using message queue threads.

#### **LISTING 7.5** Worker Thread Pool

```cpp
class Pool
{
public:
    static DWORD WINAPI ThreadProc(void * p);
    int DoWork();
    Pool();
    virtual ~Pool();

private:
    std::queue<DWORD> m_qidThread;
};

#define MYMESSAGE (WM_USER+1000)
#define NUMTHREADS 10

Pool::Pool()
{
    for (int i=0;i<10;i++)
    {
        DWORD dw;
        HANDLE thread = ::CreateThread(NULL, 0, ThreadProc, NULL, 0, &dw);
        ::CloseHandle(thread);
        m_qidThread.push(dw);
    }
}

Pool::~Pool()
{
    while (!m_qidThread.empty())
    {
        ::PostThreadMessage(m_qidThread.front(), WM_QUIT, 0, 0);
        m_qidThread.pop();
    }
}

DWORD WINAPI Pool::ThreadProc(void *p)
{
    MSG msg;
    while (::GetMessage(&msg, NULL, 0, 0))
    {
        switch (msg.message)
        {
            case MYMESSAGE:
                //////////////////////////////////////
                // TODO
                // Add background processing code here
                //
                std::cout << "Hello World!" << std::endl;
                std::cout << "From Thread Number: " << ::GetCurrentThreadId()
                          << std::endl;

            default:
                break;
        }
    }
    return 0;
}

int Pool::DoWork()
{
    DWORD dw = m_qidThread.front();
    ::PostThreadMessage(dw, MYMESSAGE, 0, 0);
    m_qidThread.pop();
    m_qidThread.push(dw);
    return 0;
}
```

An important implementation of thread pool is apartment thread pooling. In the apartment-threading model, COM+ allocates several apartment threads where COM+ objects can be created. This type of model can provide for a multithreaded server where each individual object is single-threaded and, therefore, does not need to consider concurrency issues. You learn this threading model in more detail in the next section.

## COM+ Threading Models

The following are the four most common types of COM+ threading models:

- Single-threaded
- Apartment-threaded
- Neutral-threaded
- Free-threaded

### The Apartment-Threaded Server

The second type of COM+ server that is used by experienced COM+ programmers is the apartment-threaded server. This server type differs from the single-threaded server in that the COM+ server has one or more apartment threads (STAs).

Each object exists in only one apartment thread (STA), and incoming calls are still serialized on the apartment thread’s message queue. That means no concurrency issues exist for per-object data. Because objects running in separate apartment threads can share global data and run concurrently, a concurrency problem now exists for global data.

Once again, to relate the discussion to a concrete example, we’ll take some time out to use ATL and work through an example. Creating an ATL server that uses the apartment-threaded model is slightly more difficult than creating a single-threaded server. Follow the same steps as for creating a single-threaded server, except select Apartment as the Threading Model on the Attributes property page of the ATL Object Wizard Properties form (refer to Figure 7.1). Three additional changes are required. You must modify your CExeModule class to inherit from the CComAutoThreadModule template class (see Listing 7.6).

#### **LISTING 7.6** Inherit from CComAutoThreadModule Template Class

```cpp
class CExeModule : public CComAutoThreadModule<CComSimpleThreadAllocator>
{
public:
    LONG Unlock();
    DWORD dwThreadID;
    HANDLE hEventShutdown;
    void MonitorShutdown();
    bool StartMonitor();
    bool bActivity;
};
```

You must modify the CExeModule::Unlock() method to call the CComAutoThreadModule::Unlock() method (see Listing 7.7).

#### **LISTING 7.7** Call CComAutoThreadModule::Unlock Method

```cpp
LONG CExeModule::Unlock()
{
    LONG l = CComAutoThreadModule<CComSimpleThreadAllocator>::Unlock();
    if (l == 0)
    {
        bActivity = true;
```
