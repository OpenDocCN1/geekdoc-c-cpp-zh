
So, you can already have critical sections defined for your objects. These can be used to implement concurrency control for per-object data. Unfortunately, this critical section—applied without any thought—might cause another bottleneck as each thread waits its turn to acquire the critical section. If this situation arises, you can create additional critical sections to reduce the bottleneck.

### Mutexes

The mutex kernel object enables you to create and manage access to a resource that cannot be guarded by critical sections. Resources that span process boundaries cannot be guarded by a critical section, but can be guarded by a mutex. Listing 7.16 shows an example of using the mutex object. Note that mutexes are shared by name among different processes, but this is not the case for critical sections.

### LISTING 7.16 Using Mutexes

```cpp
class Pool
{
public:
    static DWORD WINAPI ThreadProc(void * p);
    int DoWork();
    Pool();
    virtual ~Pool();

private:
    static HANDLE sm_mutex;
    std::queue<DWORD> m_qidThread;
};

#define MYMESSAGE (WM_USER+1000)
#define NUMTHREADS 10

HANDLE Pool::sm_mutex;

Pool::Pool()
{
    sm_mutex = ::CreateMutex(NULL, FALSE, "MYMUTEX");
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
    ::WaitForSingleObject(m_qidThread.front(), 5000);
    ::CloseHandle(sm_mutex);
}

DWORD WINAPI Pool::ThreadProc(void *p)
{
    MSG msg;
    while (GetMessage(&msg, NULL, 0, 0))
    {
        switch (msg.message)
        {
        case MYMESSAGE:
            /////////////////////////////////////////
            // TODO
            // Add background processing code here
            // ::WaitForSingleObject(sm_mutex, INFINITE);
            std::cout << "Hello World from Thread Number: "
                      << GetCurrentThreadId() << std::endl;
            ::ReleaseMutex(sm_mutex);
            break;
        default:
            break;
        }
    };
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

Remember that critical sections are process local objects and, therefore, cannot limit access to a resource that spans more than one process.

With the mutexes in Listing 7.16, you could have one or more processes running one instance each of the Pool class, and they would share the same named mutex called MYMUTEX. With the critical section example in Listing 7.11, each process has its own distinct critical section.

### Semaphores and Events

Semaphores and events are more complex kernel objects that limit access to resources. Semaphores are actually a more generalized implementation that enables the programmer to specify how many threads can have simultaneous access to a resource. A semaphore has a counter that moves between zero and a minimum amount specified by the programmer. The semaphore is nonsignaled when the count reaches zero and signaled when the count is non-zero.

The event object is also a two-state object like the mutex; that is, it is either signaled or nonsignaled. But the event and semaphore objects can be moved from nonsignaled to signaled by any thread. The mutex object can be moved from nonsignaled to signaled only by the thread that originally moved the mutex’s state from signaled to nonsignaled. Your choice of which synchronization object works best for you depends primarily on your concurrency problems. Some concurrency problems lend themselves well to critical sections, others to mutexes, semaphores, or events.

### Summary

In this chapter, you learned how COM+ fits into the various Windows threading paradigms. You should understand which thread types, threading models, and synchronization objects are available to you, the programmer, and which one is best for your project. The next time you write a COM+ server or implement concurrency control, you’ll have some added knowledge to justify your design.

We spent a good deal of time discussing concurrency issues, which should help you prevent and resolve the problems in your programming. These issues can be the most difficult to deal with in multithreaded applications.

## COM and the Registry

### IN THIS CHAPTER

- Registry API 172
- Regedit and Regedt32 179
- COM Registry Structure 181
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole 193
- Registering a COM+ Server 195

## CHAPTER 8

This chapter talks about the registry as it relates to COM+. If you've ever wondered how applications know how to find COM+ objects when they are instantiated, you'll find this chapter enlightening. As you will see, the registry is the repository for information about COM+ servers. This information is used to locate and know about COM+ servers that are used by applications.

### Registry API

Reading and writing to the registry tends to be a lot more difficult than it should be. An example is the RegCreateKeyEx() API, which clearly has too many parameters. With one function, you can create and open registry keys and set security permissions for registry keys. This can all be done in one call. This is nice if your performance is evaluated by how much you can accomplish with the least amount of code.

In Listing 8.1, I've coded a small C++ class, CRegistry, that removes most of the complexity from the registry APIs. This class has three functions that perform the three basic operations needed: setting values in the registry, retrieving values from the registry, and deleting registry keys. The class constructor automatically opens the specified key and creates the key if it does not already exist.

### LISTING 8.1 Easy-to-Use Registry Class

```cpp
class CRegistry
{
public:
    CRegistry();
    CRegistry(HKEY, const char *);
    ~CRegistry();

    BOOL Open(HKEY, const char *);
    BOOL Close(void);

    BOOL ReadDWORD(const char *, DWORD *, DWORD *pdwLastError = NULL);
    BOOL ReadString(const char *, LPVOID, int, DWORD *pdwLastError = NULL);

    BOOL WriteDWORD(const char *, DWORD, DWORD *pdwLastError = NULL);
    BOOL WriteString(const char *, LPVOID, DWORD *pdwLastError = NULL);
    BOOL Write(const char *, LPVOID, DWORD, int);

    void BuildList(const char *, CStringArray&);
    void StoreList(const char *, CStringArray&);

protected:
    HKEY m_hKey;
    DWORD m_dwLastError;
    BOOL Read(const char *, LPVOID);
    DWORD m_dwSize;
};

CRegistry::CRegistry()
{
    // Member variable m_hKey set to NULL so
    // we know we don't have to close it when Close()
    // is called from the destructor.
    m_hKey = NULL;
}

CRegistry::CRegistry(HKEY hKey, const char *lpszSubKey)
{
    // Member variable m_hKey set to NULL so
    // we know we don't have to close it when Close()
    // is called from the destructor.
    m_hKey = NULL;

    // This constructor opens the registry key.
    Open(hKey, lpszSubKey);
}

CRegistry::~CRegistry()
{
    // Call the close function from the destructor
    // to make sure the registry key is closed (if it
    // was opened).
    Close();
}

BOOL CRegistry::Open(HKEY hKey, const char *lpszSubKey)
{
    // First try to close the registry. (It may not be
    // opened, but we want to be sure.)
    Close();

    // Reset our error variable.
    m_dwLastError = 0;

    // Open the registry key. We use KEY_ALL_ACCESS to avoid
    // any problems.
    if(::RegOpenKeyEx(hKey, lpszSubKey, 0,
        KEY_ALL_ACCESS, &m_hKey) != ERROR_SUCCESS) {

        // Get the error and return.
        m_dwLastError = GetLastError();
        return(FALSE);

    }

    // Return success.
    return(TRUE);

}

BOOL CRegistry::Close(void)
{
    BOOL bRet = TRUE;

    // If m_hKey is NULL then the registry key
    // isn't opened. If this is the case, return
    // indicating that Close() wasn't successful.
    if(m_hKey == NULL)
        return(FALSE);

    // Close the registry key.
    bRet = (::RegCloseKey(m_hKey) == ERROR_SUCCESS);

    // Get the error (if any).
    m_dwLastError = GetLastError();

    // Set the key handle to NULL so we don't accidentally
    // close it again.
    m_hKey = NULL;

    // Return success or failure
    return(bRet);

}

BOOL CRegistry::Read(const char *lpszValueName, LPVOID lpReturnBuffer)
{
    // Generic read function.

    // If the key is not opened, return with failure.
    if(m_hKey == NULL)
        return(FALSE);
}
```
