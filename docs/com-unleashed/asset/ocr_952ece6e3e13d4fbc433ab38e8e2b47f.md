# Worker Threads

The most basic thread type is the worker thread. The worker thread is commonly used to simulate background processing. You can easily provide background-processing capabilities to your program by initiating sequences of code in a separate thread. Listing 7.1 shows how to use a worker thread to initiate background processing.

# **LISTING 7.1**  An Example of a Worker Thread

```
class WorkerThread
{
public:
    int DoWork();
    static DWORD WINAPI ThreadProc(void * p);
    WorkerThread();
    virtual ~WorkerThread();
};

WorkerThread::WorkerThread () {}

WorkerThread::~WorkerThread () {}

DWORD WINAPI Worker::ThreadProc(void *p)
{
    /////////////////////////////////
    // TODO
    // Add background processing code here
    //
    std::cout << "Hello World!" << std::endl;
    Sleep(1000);
    std::cout << "Goodbye World!" << std::endl;
    return 0;
}

int WorkerThread::DoWork()
{
    DWORD dw;
    HANDLE thread = ::CreateThread(NULL, 0, ThreadProc, NULL, 0, &dw);
    ::CloseHandle(thread);
    return 0;
}
```

Note that the DoWork() method returns to the caller before the real work has finished. This is one of the difficulties with creating Pausework() and Stopwork() methods; the thread is busy working and a simple method that stops the action must somehow signal the executing thread. The thread must be looking for the signal as well.