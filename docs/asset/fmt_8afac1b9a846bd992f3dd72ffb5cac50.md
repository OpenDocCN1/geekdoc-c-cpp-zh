
`&dwFileSize`, `NULL`);

`dwBytesWritten` += `dwBytesSize`;

`SendMessage`( `hProcess`, `WM_STEPIT`, 0, 0 );

```
当线程遇到互斥锁（mutex）后，它就可以执行写入操作。然而，存在一种可能性，即它在读取线程之前被调度，而缓冲区可能是空的。每当读取线程获取内容时，它会将读取的字节数加到 `dwBytesRed` 变量中，如果需要写入的线程写入的字节少于读取的，它就可以写入。否则，它将跳过本次循环的写入，并简单释放互斥锁给另一个线程。

## 更多...

生产者-消费者问题也称为边界缓冲区问题。两个进程共享一个共同的固定大小缓冲区。其中一个生产者将信息放入缓冲区，另一个消费者则将其取出。该问题也可以被推广到 n 个生产者和 n 个消费者，但我们只考虑一个生产者和一个消费者的情况，因为这个假设简化了解决方案。当生产者想要向缓冲区放入新项但缓冲区已满时，就会出现问题。解决方案是让生产者睡眠，并在消费者移除一个或多个项时将其唤醒。同样，如果消费者想要清空缓冲区，它会睡眠，直到生产者向缓冲区放入东西并唤醒它。这种方法看似简单，但它会导致与我们之前在打印机目录（spooler directory）中看到的同样的竞态条件。这留给读者去尝试解决。

# 在内核中实现线程

内核中的一个互斥锁可以允许线程执行写入操作。然而，存在一种可能性，即它在读取线程之前被调度，而缓冲区可能是空的。每当读取线程获取内容时，它会将读取的字节数加到 `dwBytesRed` 变量中，如果需要写入的线程写入的字节少于读取的，它就可以写入。否则，它将跳过本次循环的写入，并简单释放互斥锁给另一个线程。

内核维护一个表来跟踪进程。内核执行的系统调用比系统调用的开销更大。当线程被销毁时，它被标记为非运行。当需要创建新线程时，会重新激活资源。线程管理的开销要更小。

## 准备工作

对于下一个示例，你需要安装 DDK（驱动开发包）。详细说明请见附录。安装 DDK 后，启动 Visual Studio。

1. 创建一个新的 Win32 项目。
2. 在解决方案管理器中添加一个头文件，命名为 `ThreadApp.h`。
打开 `ThreadApp.h` 并粘贴以下代码：

```cpp
#include <windows.h>
#include <tchar.h>
#define DRIVER_NAME TEXT("Test.sys") 
#define DRIVER_SERVICE_NAME TEXT("TestDriver") 
#define Message(n) MessageBox(0
```

## 与线程的概念

```cpp
ShellAbout(0, DRIVER_SERVICE_NAME, TEXT(**), NULL);
StopDriver();
  return 0;
}
BOOL StartDriver(LPTSTR szCurrentDriver)
{
  HANDLE  hFile = 0;
  DWORD   dwReturn = 0;
  SC_HANDLE hSCManager = 0;
  SC_HANDLE hService = 0;
  SERVICE_STATUS Status = { 0 };
  TCHAR   szDriverPath[MAX_PATH] = { 0 };
  GetSystemDirectory(szDriverPath);
  TCHAR   szUNICODE[MAX_PATH + 1];
#ifdef _UNICODE
  wsprintf(szDriver, L"\\drivers\\%s", DRIVER_NAME);
#else
  sprintf(szDriver, "\\drivers\\%s", DRIVER_NAME);
#endif
  tccat(szDriverPath, tcslen(szDriver) + 1) * sizeof(TCHAR), szDriver);
  BOOL bSuccess = CopyFile(szCurrentDriver, szDriverPath, FALSE);
  if (bSuccess == FALSE)
  {
    Message("copy driver failed!");
    return bSuccess;
  }
  hSCManager = OpenSCManager(NULL, NULL, SC_MANAGER_CREATE_SERVICE);
  if (hSCManager == 0)
  {
    Message("open sc manager failed!");
    return FALSE;
  }
  hService = CreateService(hSCManager, DRIVER_SERVICE_NAME, DRIVER_SERVICE_NAME, SERVICE_START | DELETE | SERVICE_STOP, SERVICE_KERNEL_DRIVER, SERVICE_DEMAND_START, SERVICE_ERROR_IGNORE, szDriverPath, NULL, NULL, NULL, NULL, NULL);
  if (hService == 0)
  {
    hService = OpenService(hSCManager, DRIVER_SERVICE_NAME, SERVICE_START | DELETE | SERVICE_STOP);
    Message("create service failed!");
  }
}
```

```cpp
Message("open service failed!");
return FALSE;
}
BOOL startSuccess = StartService(hService, 0, NULL);
if (startSuccess == FALSE) {
    Message("start service failed!");
    return startSuccess;
}
CloseHandle(hFile);
return TRUE;
}
BOOL StopDriver(void) {
    SC_HANDLE hSCManager = { 0 };
    SC_HANDLE hService = { 0 };
    SERVICE_STATUS Status = { 0 };
    TCHAR szPath[MAX_PATH] = { 0 };
    GetSystemDirectory(szPath, MAX_PATH);
    TCHAR szDriver[MAX_PATH + 1];
    #if UNICODE
    sprintf(szDriver, L"%s\\%s", DRIVER_NAME);
    #else
    sprintf(szDriver, "%s\\%s", DRIVER_NAME);
    #endif
    strcatat_s(szDriver, (_tcslen(szDriver) + 1) * sizeof(TCHAR), szDriver);
    hSCManager = OpenSCManager(NULL, NULL,
    SC_MANAGER_CREATE_SERVICE);
    if (hSCManager == 0) {
        return FALSE;
    }
    hService = OpenService(hSCManager, DRIVER_SERVICE_NAME,
    SERVICE_START | DELETE | SERVICE_STOP);
    if (hService) {
        ControlService(hService, SERVICE_CONTROL_STOP, &ServiceStatus);
        DeleteService(hService);
        CloseHandle(hService);
        BOOL ifSuccess = DeleteFile(szDriverPath);
        return TRUE;
    }
    return FALSE;
}
```

## 进程与线程的概念

4. 现在，打开解决方案管理器（Solution explorer）并创建一个 Win32 控制台项目。将其命名为 `DriverApp`。

5. 添加一个新的头文件，将其命名为 `DriverApp.h`。打开 `DriverApp.h` 并粘贴以下代码：

```cpp
#include <ntdk.h>
DRIVER_INITIALIZE DriverEntry;
DRIVER_UNLOAD OnUnload;
```

6. 现在，打开解决方案，并在 `DriverApp` 项目下添加一个新的源文件，命名为 `DriverApp.cpp`。打开 `DriverApp.cpp` 并粘贴以下代码：

```cpp
#include "DriverApp.h"
VOID ThreadStart(PVOID lpStartContext) {
    KEVENT pEvent = (KEVENT)lpStartContext;
    DbgPrint("Hello! I am kernel thread. My ID is %u. Regards..",
    (ULONG)PsGetCurrentThreadId());
    SetEvent(pEvent, 0, 0);
    PostTerminateSystemThread(STATUS_SUCCESS);
}
NTSTATUS DriverEntry(PDRIVER_OBJECT theDriverObject,
PUNICODE_STRING String=RegistryPath)
{
    HANDLE hThread = NULL;
    NTSTATUS ntStatus = 0;
    OBJECT_ATTRIBUTES ThreadAttributes;
    KEVENT kEvent = { 0 };
    PTHREAD pThread = 0;
    theDriverObject->Driverload = OnUnload;
    DbgPrint("Entering KERNEL mode..");
    InitializeObjectAttributes(&ThreadAttributes, NULL,
    OBJ_KERNEL_HANDLE, NULL, NULL);
    try {
        KeInitializeEvent(&kEvent, SynchronizationEvent, 0);
        ntStatus = PsCreateSystemThread(&hThread, GENERIC_ALL,
        &ThreadAttributes, NULL, NULL, (PKSTART_ROUTINE) &ThreadStart,
        &kEvent);
        if (NT_SUCCESS(ntStatus))
        {
            WaitForSingleObject(&kEvent, Executive, KernelMode, FALSE,
            NULL);
            ZwClose(hThread);
        }
        else
        {
            DbgPrint("Could not create system thread!");
        }
    }
    except (EXCEPTION_EXECUTE_HANDLER)
    {
        DbgPrint("Error while creating system thread!");
        return STATUS_SUCCESS;
    }
VOID OnUnload(PDRIVER_OBJECT DriverObject)
{
    DbgPrint("Leaving KERNEL mode...");
}
```

## 工作原理

首先，我们创建了一个 Win32 应用，但仅用于演示。我们没有 UI，也没有消息日志。我们只是想将驱动加载到内核中；然后我们将显示 `ShellAbout` 对话框，给用户留出时间阅读 DbgView 输出（关于 DbgView 的详细说明可以在附录），在用户关闭 `ShellAbout` 对话框后，驱动将被卸载，应用程序之结束。

我们创建的 Win32 应用只能加载和卸载驱动，因此不再有进一步的解释。现在，让我们查看 `DriverApp` 项目。在为驱动编译正确设置了 Visual Studio 项目后（关于 Visual Studio 编译设置的详细说明可以参见附录），我们在 `DriverApp.h` 头文件中声明了每个驱动程序必须具备的两个主例程序：

```cpp
DRIVER_INITIALIZE DriverEntry;
DRIVER_UNLOAD Onload;
```

这两个例程序是驱动入口点和驱动卸载例程序。我们将使用驱动入口点来初始化驱动对象并启动内核线程。新创建的线程将立即返回唯一标识符。此外，内核探索和开发不是本书的内容。我们只是想让大家体验一下内核线程。由于驱动被编译为 `/TC2`，我们必须确保在第一条命令之前声明所有变量。如下代码所示：

```cpp
HANDLE hThread = NULL;
NTSTATUS ntStatus = 0;
OBJECT_ATTRIBUTES ThreadAttributes;
KEVENT kEvent = { 0 };
PTHREAD pThread = 0;
```

然后，我们必须有卸载例程序：

```cpp
theDriverObject->DriverUnload = OnUnload;
```

现在，在创建内核线程之前，我们需要先调用 `InitializeObjectAttributes` 例程序来初始化 `ThreadAttribute` 对象：

```cpp
InitializeObjectAttributes(&Threadattributes, NULL,
OBJ_KERNEL_HANDLE, NULL, NULL);
```

内核开发必须极其谨慎地进行，即使是最微小的错误也可能导致蓝屏（BSOD）或机器崩溃。这就是为什么我们使用 *try -except* 块，它与我们熟悉的 catch 略有不同。

在内核中创建的句柄与在用户态创建的句柄不同。`PsCreateSystemThread` 返回的空间不能用于 `KeWaitForSingleObject` 例程序。我们需要初始化一个事件，当 `KeWaitForSingleObject` 返回时，由线程本身发出信号（事件将在第 3 章“管理线程”中详细解释）。每次调用 `PsCreateSystemThread`，我们都需要处理该线程。例如：

```cpp
VOID ThreadStart(PVOID lpStartContext) {
    KEVENT pEvent = (KEVENT)lpStartContext;
    DbgPrint("Hello! I am kernel thread. My ID is %u. Regards..",
    (ULONG)PsGetCurrentThreadId());
    SetEvent(pEvent, 0, 0);
    PostTerminateSystemThread(STATUS_SUCCESS);
}
```

# 第3章

另一方面，线程的创建速度快得多，开销更小，且不会发生从磁盘加载。你只需要提供地址指针，这是一个用户定义的例程（函数）。不要忘记，守护进程、监听器（服务器）等任务仍然需要进程。然而，在谈到较小的并发操作时，在许多情况下线程应该是你的首选。

由于我们在之前的示例中已经使用过进程和线程，接下来的示例将展示创建和使用两者时的巨大差异。

## 准备工作

确保 Visual Studio 正在运行。

# 如何操作...

现在，让我们通过以下步骤创建程序并解释其结构：

1. 创建名为 `tmpThread` 的新 C++ 控制台应用程序。
2. 打开 `tmpThread.cpp`。
3. 将以下代码添加：

```cpp
#include <afx.h>
#include <windows.h>
#include <iostream>
using namespace std;
DWORD WINAPI StartAddress(LPVOID lpParameter)
{
    cout << "Hello. I am a very simple thread." << endl;
    cout << "I am used to demonstrate thread creation." << endl;
    return 0;
}
int main(int argc, TCHAR* argv[])
{
    // 线程创建。注意，我们只需要
    // 在与主函数相同的代码段中
    // 定义 StartAddress 例程以启动线程
    // 并执行并发操作。
    HANDLE hThread = CreateThread(NULL, 0, StartAddress, NULL, 0,
```

## 管理线程

```cpp
// 进程创建。注意 CreateProcess 的第一个
// 参数指向包含需要从磁盘加载
// 内容的文件。
STARTUPINFO startupInfo = { 0 };
PROCESS_INFORMATION processInformation = { 0 };
```
```cpp
```
