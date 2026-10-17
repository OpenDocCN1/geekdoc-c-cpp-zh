
```cpp
    }

    WaitForMultipleObjects(Count(), hThreads, TRUE, INFINITE);

    delete[] hThreads;

}

void CThreadPool::RemoveAll()

{

    Cthread* pThread = NULL;
    while (pThread = threadlist->GetNext()) {
        delete pThread;
    }
    delete threadlist;
}

void CThreadPool::RemoveThread(DWORD dwThreadId)

{

    Cthread* pThread = NULL;
    while (pThread = threadlist->GetNext()) {
        if (pThread->dwThreadId() == dwThreadId) {
            threadlist->Remove(pThread);
            break;
        }
    }
}

void CThreadPool::RequestThread(LPTHREAD_START_ROUTINE lpThreadStart, LPVOID pParam)

{

    Cthread* pThread = NULL;
    if (Count() < dwMaxCount) {
        pThread = new Cthread(lpThreadStart);
        pThread->Start(pParam);
        threadlist->Add(pThread);
    }
}

#endif
```

- 打开解决方案管理器，右键点击源文件。添加一个名为 `main` 的源文件。打开 `main.cpp`。复制并粘贴以下代码：

```cpp
#include "main.h"
#include "CBankAccount.h"
#include "CThread.h"

double Random(double dMin, double dMax)
{
    double dValue = (double)rand() / RAND_MAX;
    return dMin + dValue * (dMax - dMin);
}

int main(void)
{
    srand((unsigned)time(NULL));
#define ACCOUNTS_COUNT 12
    CBankAccount* accounts[ACCOUNTS_COUNT];
    for (unsigned uIndex = 0; uIndex < ACCOUNTS_COUNT; uIndex++) {
        accounts[uIndex] = new CBankAccount(Random(10, 1000));
    }

    CThreadPool* pool = new CThreadPool();
#define TASK_COUNT 5
    for (unsigned uIndex = 0; uIndex < TASK_COUNT; uIndex++) {
        int nFirstIndex = rand() % ACCOUNTS_COUNT;
        int nSecondIndex = -1;
        while ((nSecondIndex = rand() % ACCOUNTS_COUNT) == nFirstIndex) {
            CParameters* params = new CParameters(accounts[nFirstIndex],
                accounts[nSecondIndex], Random(50, 200));
            pool->RequestThread(CBankAccount::Transfer)->Start(params);
        }
    }

#ifdef _DEBUG
    return system("pause");
#endif

    return 0;
}
```

`CThreadPool` 类实现了实际的线程池。它有两个属性：一个指向项目列表的指针，以及线程池可以创建的最大线程数。它有两个构造函数：其中一个使用机器的逻辑处理器数量默认设置最大线程数；第二个构造函数有一个参数——即线程池可以实例化的实际最大线程数。在析构函数中，我们将使用 `RemoveAll` 方法来释放资源。`Count` 方法返回列表中项目的计数。`RemoveThread` 方法搜索指定参数的线程，如果找到，则将其移除。`Thread` 创建了一个线程句柄数组，该句柄将用于 `WaitMultipleObjects` API，并将 `bWaitAll` 参数设置为 `TRUE` 以等待所有线程完成。在 `WaitMultipleObjects` 返回后，它会删除该句柄数组。`RemoveAll` 方法通过对列表中的每个线程调用 `RemoveThread` 方法来从列表中移除所有线程。`MaxCount` 方法返回或设置 `dwCount` 属性的值。线程池可以根据需要增加或减少其大小。`RequestThread` 方法搜索由 `dwThread` 参数指定的线程并返回该线程的句柄。`RequestThread` 方法用于获取空闲线程。如果没有达到最大线程数，该方法将创建一个新线程并插入列表。如果已经达到最大值，该方法将遍历整个列表并查询每个线程的退出代码。

如果所有线程都处于活动状态，它将等待 0.1 秒并重试，直到找到第一个线程或使用用户提供的地址创建一个新线程。

在 `main.cpp` 中，我们创建了 `Random` 函数来获取 `dmin` 到 `dmax` 范围内的随机双精度数字。在应用程序入口点处，我们将随机生成器设置为当前时间，并创建十二个具有随机余额值的银行账户。然后，我们将实例化带有五个待处理任务的线程池。对于每个任务，我们将选择一个随机银行账户并找到另一个与第一个不同的（随机）银行账户。找到两个账户后，我们将使用 `RequestThread` 和 `Start` 方法执行随机值的转账。在设置好所有任务后，我们将调用 `WaitAll` 方法来等待任务完成。当 `WaitAll` 返回时，我们可以删除线程池。

# 更多内容……

尽管我们仔细设计了线程池并注意了所有必要的细节（例如死锁），死锁仍然可能发生。这种情况非常罕见——几乎不可能，因为从账户 a 到账户 b 的转账必须与从账户 b 到账户 a 的转账完全同时发生——但这是可能的。我们的下一个示例将扩展线程池，使其更加智能，并带有解决死锁等潜在问题的功能。

# 自定义线程池调度器

在之前的示例中，我们必须创建线程池来管理某些任务——从一个银行账户到另一个账户的资金转账。我们的目标是使用足够的系统资源，而不是过度。同时，我们必须处理忙碌和可用线程并维护同步。接下来的示例将扩展线程池，使其变得智能得多，并具备解决执行过程中可能出现问题的能力。

我们将不再遍历线程列表并等待某些线程完成执行，而是使用消息传递来选择第一个完成任务的线程并通知该线程；我们将添加另一层抽象，以便对任务执行进行更多控制。我们不再简单地将用户定义的函数作为起始地址执行。

在下面的图中，我们说明了新方法背后的思想：

![](img/412b0f5bbb36adcce2ddd2d5b7416516_368_0.png)

尽管我们复制了许多线程，但对于每个任务我们将创建两个线程而不是一个，我们仍然会保持线程的数量。为执行任务而创建的线程将额外创建一个线程并等待它，以便对任务执行有更多控制。我们将第一个线程命名为工作线程（worker），并将创建的第二个线程命名为上下文线程（context thread）。这种方法背后的思想是我们将拥有更多控制权；如果上下文线程已终止，等待它的工作线程将查询其退出代码并通知调度器发生了错误。如果上下文线程挂起或无响应，工作线程将发现出现问题并采取适当操作，而我们则尝试解决调度器。这种粒度赋予了我们更多控制权，并让线程池更加智能。

我们的示例将针对一个故意创建死锁的场景，并尝试解决这种情况。

## 准备工作

确保 Visual Studio 已安装并运行。

# 如何操作……

现在，让我们创建程序并解释其结构。执行以下步骤：

- 1. 创建一个名为 `CThreadPool` 的新 C++ 控制台应用程序。
- 2. 打开资源管理器，右键点击“头文件”。添加一个名为 `Main.h` 的新头文件。复制并粘贴以下代码：

```
#ifndef __MAIN__
#define __MAIN__

#include <Windows.h>
#include <tchar.h>
#include <time.h>

#define MSG_ENDTASK 0x1000
#define MAX_WAIT_TIME 120 * 1000

#endif
```

- 3. 打开解决方案管理器，右键点击“头文件”。添加一个名为 `CBankAccount.h` 的新头文件。打开 `CBankAccount.h`。复制并粘贴以下代码：

```cpp
#ifndef _BANKACCOUNT__
#define _BANKACCOUNT__

#include "main.h"

class CBankAccount {
public:
    CBankAccount(double balance);
    ~CBankAccount();
    double getBalance() const;
    void deposit(double amount);
    void withdraw(double amount);
private:
    double balance;
};

class Clock {
public:
    Clock(const char* threadName);
    ~Clock();
    void start();
    void stop();
private:
    HANDLE hTimer;
    LARGE_INTEGER startTime;
    LARGE_INTEGER endTime;
    const char* threadName;
};

class Thread {
public:
    Thread(LP_START_ROUTINE routine, LPVOID parameter);
    ~Thread();
    void start();
    void join();
    DWORD getExitCode();
private:
    HANDLE hThread;
    LPVOID parameter;
};

class CThreadPool {
public:
    CThreadPool(int maxCount);
    ~CThreadPool();
    void RequestThread(DWORD dwThread);
    void WaitAll();
    void RemoveAll();
    int GetCount();
    void MaxCount(int dwCount);
private:
    void RemoveThread(DWORD dwThread);
    int dwCount;
    std::vector<Thread*> threads;
    std::vector<CBankAccount*> accounts;
};

class CParameters {
public:
    CParameters(CBankAccount* from, CBankAccount* to, double value);
    void execute();
private:
    CBankAccount* from;
    CBankAccount* to;
    double value;
};
```

*(注：后续重复的代码块已省略，以符合“不要重复输出原文”的要求)*

# 第8章

4. 打开解决方案管理器（Solution Explorer）并右键点击头文件（Header files）。添加一个名为 `CThread` 的新头文件。打开 `CThread.h`。复制并粘贴以下代码：

```cpp
#ifndef __THREAD__
#define __THREAD__

#include "main.h"

class CThread
{
public:
    CThread(LPTHREAD_START_ROUTINE lpThreadStart, DWORD dwDispatcherId);
    ~CThread();
    void Start(LPVOID lpContext = NULL)(pThreadContext->lpParameter = lpContext);
    bool StillAlive() const { return ExitStatus() == STILL_ACTIVE; }
    HANDLE Handle() const { return hThread; }
    HANDLE HandleContext() const { return pThreadContext->hThread; }
    DWORD ThreadId() const { return dwThreadId; }
    DWORD ThreadContext() const { return pThreadContext->dwThreadId; }
    DWORD ExitCode() const { return dwExitCode; }
protected:
    static DWORD GetThreadId(CThread* cThread);
private:
    typedef struct {
        LPTHREAD_START_ROUTINE lpThreadStart;
        LPVOID lpParameter;
        HANDLE hThread;
        DWORD dwThreadId;
        DWORD dwDispatcherId;
        DWORD dwWaitTime;
    } START_CONTEXT, *pThreadContext;
    HANDLE hThread;
    DWORD dwThreadId;
    DWORD dwExitCode;
};
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_373_0.png)

高级线程管理

```cpp
);

CThread::CThread(LPTHREAD_START_ROUTINE lpThreadStart, DWORD
dwDispatcherId) : dwExitCode(0)
{
    pThreadContext = new START_CONTEXT();
    pThreadContext->lpThreadStart = lpThreadStart;
    pThreadContext->dwDispatcherId = dwDispatcherId;
    pThreadContext->dwWaitTime = MAX_WAIT_TIME;
    hThread = CreateThread(NULL, 0, StartAddress, this,
    CREATE_SUSPENDED, &dwThreadId);
}

CThread::~CThread()
{
    delete pThreadContext;
    if (StillAlive())
    {
        TerminateThread(hThread, (DWORD)-1);
    }
    CloseHandle(hThread);
}

DWORD CThread::GetThreadId(CThread* cThread)
{
    return cThread->dwThreadId();
}

DWORD WINAPI CThread::StartAddress(LPVOID lpParam)
{
    thread = (CThread*)lpParam;
    thread->pThreadContext->Thread = CreateThread(NULL, 0,
    thread->pThreadContext->lpThreadStart,
    thread->pThreadContext->lpParam, 0,
    &thread->pThreadContext->dwThreadId);
    DWORD dwStatus = WaitSingleObject(
    thread->pThreadContext->hThread,
    thread->pThreadContext->dwWaitTime);
    CloseHandle(thread->pThreadContext->hThread);
    PostThreadMessage(thread->pThreadContext->dwDispatcherId,
    MSG_ENDTASK, (WPARAM)thread->dwThreadId, 0);
    return 0;
}
#endif
```
