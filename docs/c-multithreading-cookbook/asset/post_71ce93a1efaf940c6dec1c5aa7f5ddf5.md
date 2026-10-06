
# Message Passing

## Getting ready

Make sure that Visual Studio is up and running.

## How to do it...

Now, let's create our program and Explain its structure. Perform the following steps:

- 1. Create a new Console named pipe_server.
- 2. Open Solution Explorer and right-click on Source file. Add a new source file named pipe_server.cpp. Open pipe_server.cpp.
- 3. Add the following code to: <windows.h>

```cpp
#include <windows.h>
#include <stdio.h>
#include <tchar.h>

#define BUFFER_SIZE 4096

WORD WINAPI StartAddress(LPVOID lParameter);

int _main(void)
{
    LPTSTR szPipeName = _T("\\\\pipe\\basicMPI");
  _printf(_T("Connection succeeded.\n"));

  HANDLE hThread = CreateThread(NULL, 0,
  (LPTHREAD_START_ROUTINE)StartAddress, hPipe, 0, NULL);

  CloseHandle(hThread);
}

  return 0;
}

WORD WINAPI StartAddress(LPVOID lpParameter)
{
  HANDLE hPipe = (HANDLE)malloc(lpParameter);
  PTCHAR szRequest = (TCHAR)HeapAlloc(GetProcessHeap(), 0,
  BUFFER_SIZE);
  PTCHAR szReply = (TCHAR)HeapAlloc(GetProcessHeap(), 0,
  BUFFER_SIZE);
  DWORD dwBytesRead = 0;
  DWORD dwBytesReply = 0;
  DWORD dwBytesWritten = 0;
  _printf(_T("Waiting messages.\n"));

  if (!ReadFile(hPipe, szRequest, BUFFER_SIZE * sizeof(TCHAR),
  &dwBytesRead, NULL))
  {
    _printf(_T("Readfile failed: Error code: [%u]\n"));
    GetLastError();
    return 2L;
  }

  // do some processing

  _printf(_T("Client request:%s\n"), szRequest);

  _tcscpy_s(szReply, BUFFER_SIZE,
  _T("default answer from server"));

  dwReplyBytes = (DWORD)(_tcslen(szReply) + 1) * sizeof(TCHAR);

  if (!WriteFile(hPipe, szReply, dwReplyBytes, &dwBytesWritten,
  NULL))
  {
    _tprintf(_T("WriteFile failed! Error code: [%u]\n"),
    GetLastError());
    return 2L;
  }

  FlushFileBuffers(hPipe);
  DisconnectNamedPipe(hPipe);
  CloseHandle(hPipe);

  HeapFree(GetProcessHeap(), 0, szRequest);
  HeapFree(GetProcessHeap(), 0, szReply);

  _tprintf(_T("Success.\n"));
  return 0L;
}
```

- 4. Open **Solution Explorer** and right-click on **Add New Project**. Create a new C++ Console application named `pipe_client`.
- 5. Open **Solution Explorer** and right-click on **Source file**. Add a new source file named `pipe_client.cpp`.
- 6. Add the following code to it:
```cpp
#include <windows.h>
#include <stdio.h>
#include <tchar.h>

#define BUFFER_SIZE 4096

int _main(void)
{
  TCHAR szBuffer[BUFFER_SIZE];
  DWORD dwRead = 0;
  DWORD dwWrite = 0;
  DWORD dwMode = PIPE_READMODE_MESSAGE;
  LPTSTR szPename = _T("\\\\pipe\\basicMPI");
  LPTSTR szMessage = _T("Message from client.");
  DWORD dwToWrite = sizeof(TCHAR);

  HANDLE hPipe = CreateFile(szPename, GENERIC_READ | GENERIC_WRITE, 0, NULL, OPEN_EXISTING, 0, NULL);

  WaitNamedPipe(szPename, INFINITE);
  SetNamedPipeHandleState(hPipe, &dwMode, NULL, NULL);

  if (!WriteFile(hPipe, szMessage, dwToWrite, &dwWritten, NULL))
  {
    _tprintf(_T("WriteFile failed! Error code: [%u]\n"),
    GetLastError());
    return -1;
  }

  _tprintf(_T("Message sent to server, receiving reply as follows:\n"));

  while (ReadFile(hPipe, szBuffer, BUFFER_SIZE * sizeof(TCHAR), &dwRead, NULL) && GetLastError() != ERROR_MORE_DATA) {
    _tprintf(_T("%s"), szBuffer);
  }

  _tprintf(_T("\nSuccess!\nPress ENTER to exit.\n"));
  scanf("%c", &szBuffer);

  CloseHandle(hPipe);
  return 0;
}
```

## How it works...

Let's explain the first. In order to use the pipe object, we need to create one using CreateNamedPipe API. The pipe name must be unique. The name must have \\pipe\\name format. Following is an example:

```cpp
HANDLE hPipe = CreateNamedPipe(szPename, PIPE_ACCESS_DUPLEX, PIPE_TYPE_MESSAGE | PIPE_WAIT, PIPE_UNLIMITED_INSTANCES, BUFFER_SIZE, 0, NULL);
```

For a complete reference of CreateNamedPipe API, refer to https://www.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-creatnamedpipe.

Our server must run forever in order to process the requests, so we will execute it in an infinite loop followed by a call to ConnectNamedPipe. This enables the pipe to wait for the client to connect. In other words, if the handle to the pipe object was obtained without specifying FILE_FLAG_OVERAPPED in CreateNamedPipe, the function will not return until the client connects. When the client connects, the execution continues. We will create a thread that will process the client while the main thread will be ready for the next request.

## Message Passing –

Now, let's review request processing. After obtaining a handle to pipe, we need to allocate enough memory for the request as well as for the response. We will use ReadFile from the other end of pipe and then do some processing. The response is sent using WriteFile in the following manner:

```cpp
WriteFile(hPipe, szReply, dwBytesWritten, NULL);
```

Now, let's review client: we can open the pipe in two ways: CreateFile or ConnectNamedPipe. The client needs to wait for the server until the pipe is available. The execution will continue when the server calls ConnectNamedPipe, and then the thread gets suspended. We are using WriteFile and ReadFile in the same manner like we did in server. When all processing is done, we must close the pipe handle.

## There's more...

All the techniques shown in this chapter have their advantages and disadvantages. Proper understanding of each of these techniques will give you the ability to use them in conjunction with each other and create the best solutions. The following chapters will demonstrate practical usage of these techniques to gain the best results.

# Thread Synchronization and Concurrent Operations

In this chapter, we will cover the following topics:

- Pseudoparallelism
- Process and thread priority
- Windows dispatcher and scheduling
- Using mutex
- Using semaphore
- Using events
- Using critical section
- Using pipes

## Introduction

In order to understand concurrent execution on different processors, we need to distinguish hardware parallelism and pseudoparallelism. Modern processors have more than one physical core for processing and these cores can process and compute in parallel, while older processors have only one core for processing and it is not always possible to get proper execution.

Furthermore, we will take a short look at Windows scheduling priority, which is necessary when we need to perform tasks with different priorities.

## Thread Synchronization and Concurrent Operations

By the end of the chapter, we will use and compare all previously explained synchronization techniques in order to conclude what we have learned so far.

## Pseudoparallelism

As we said before, modern processors have more than one physical core, and parallel processing is its native feature. What about older ones? Is it possible to create parallel execution in a single core environment?

Let's give a simple example; we need to calculate a certain mathematical equation. We will calculate the sum that will be implemented as loop with x iterations. In every iteration, certain expressions are calculated.

When we create a program where one thread will execute a certain task, the calculation time for the task execution is finite. Now let's assume that it is t. If we split the execution between two threads, the first thread will calculate the first half of the sum of iterations and the second thread will calculate the other half of the sum of the iterations, we will get faster execution and the approximate time to t/2.

Well, on a single processor, the answer is no because the operating system schedules both threads for execution, but there is no hardware to support such executions. Since there is only one core, only one thread can be executed on the CPU at any instant of time.

It is important to understand that creating threads not always provide benefit. If we split some task into eight threads and try to execute the program on a single core CPU, division of the task will only slow the process because unnecessary thread creation occurs, and separate executions will only waste time. If we add synchronization to such a program, we will waste a lot of time waiting between threads when only one thread can run.

Pseudoparallelism is a very important operating system feature. It gives you an illusion that all tasks (programs) are executed in parallel. For example, while you use Microsoft Word, you can play Winamp, print a file, and hunt DVD at the same. Either on multiple cores, all tasks are divided into separate threads, which are scheduled by the operating system for execution. Switching quickly among threads creates an illusion that all these threads are executed concurrently.

## Understanding process and thread priority

To be able to work with threads, you need to know more than just how to create or terminate a thread. It requires that threads interact effectively, which demands proper time control. Control has two forms: priority and synchronization. Priority controls how often a thread gets the CPU for execution, while synchronization controls competition for shared resources, and gives the sequence where threads must perform tasks in a specific order.
