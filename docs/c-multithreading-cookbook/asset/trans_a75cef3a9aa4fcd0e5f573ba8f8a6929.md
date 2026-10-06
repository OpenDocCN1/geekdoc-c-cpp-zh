

# 第5章

```cpp
{
    if (!*szFilePath)
    {
        MessageBox(hWnd,
                   T("你必须先选择有效的文件路径！"),
                   T("错误!"), MB_OK | MB_TOPMOST | MB_ICONERROR);
        break;
    }

    ifstream infile(szFilePath);
    if (infile.is_open())
    {
        string line;
        while (std::getline(infile, line))
        {
            QueueElement* pElement = new QueueElement();
            stringstream iss(line);
            if (iss >> pElement->iA1 >> pElement->iB1 >>
                pElement->iC1 >> pElement->iA2 >> pElement->iB2 >> pElement->iC2)
            {
                break;
            }

            pElement->hWndProgress = GetDlgItem(hWnd, CONTROL_PROGRESS);
            pElement->hWndResult = GetDlgItem(hWnd, CONTROL_RESULT);
            queue.Enqueue(pElement);
        }
        infile.close();
    }
}

SendMessage(GetDlgItem(hWnd, CONTROL_PROGRESS), PBM_STRENG, 0, MAKELPARAM(0, queue.Count()));
int iCount = queue.Count();
for (int iIndex = 0; iIndex < iCount; iIndex++)
{
    HANDLE hThread = CreateThread(NULL, 0,
        (LPTHREAD_START_ROUTINE)StartAddress, &queue,
        0, NULL);
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_207_0.png)

# 线程同步与并发操作

```cpp
// ... (之前的逻辑)
}else {
    MessageBox(hWnd, _T("无法打开文件!"),
    _T("错误!"), MB_OK | MB_TOPMOST | MB_ICONERROR);
}
}
break;
}
default: {
    return DefWindowProc(hWnd, uMsg, wParam, lParam);
}
return 0;

DWORDAPI StartAddress (LPVOID lParameter)
{
    // 我们将使用克莱默法则求解线性方程组：
    CQueue<QueueElement>* pQueue = (CQueue<QueueElement>*)lpParameter;

    HANDLE hMutex = OpenMutex(MUTEX_ALL_ACCESS, FALSE, szMutex);
    HANDLE hSemaphore = OpenSemaphore(SEMAPHORE_ALL_ACCESS, FALSE, szSemaphore);
    QueueElement* pElement = NULL;

    while (true) {
        WaitForSingleObject(hSemaphore, INFINITE);
        ReleaseSemaphore(hSemaphore, 1, NULL);

        WaitForSingleObject(hMutex, INFINITE);
        pElement = pQueue->Dequeue();
        ReleaseMutex(hMutex);
        if (pElement == NULL) {
            break;
        }

        char szBuffer[1024];
        double dDeterminant = (pElement->iA1 * pElement->iB2) -
                              (pElement->iB1 * pElement->iA2);

        if (dDeterminant != 0) {
            double DX = (pElement->iC1 * pElement->iB2) -
                        (pElement->iB1 * pElement->iC2) / dDeterminant;
            double DY = (pElement->iA1 * pElement->iC2) -
                        (pElement->iC1 * pElement->iA2) / dDeterminant;
            sprintf_s(szBuffer, " %8.4f, y = %8.4f\n", DX, DY);
        } else {
            sprintf_s(szBuffer, " 行式为零.\n");
        }

        strcat_s(szResult, 4096, szBuffer);
        SetWindowTextA(pElement->hWndResult, szResult);

        SendMessage(pElement->hWndProgress, PBM_STEPIT, 0, 0);

        delete pElement;
        sleep(1000);
    }

    CloseHandle(hSemaphore);
    CloseHandle(hMutex);
    return 0L;
}

BOOL FileDialog(HWND hWnd, LPSTR szFileName) {
    OPENFILENAME ofn;
    char szFile[MAX_PATH];
    ZeroMemory(&ofn, sizeof(ofn));
    ofn.lStructSize = sizeof(ofn);
    ofn.hwndOwner = hWnd;
    ofn.lpstrFile = szFile;
    ofn.lpstrFile[0] = '\0';
    ofn.nMaxFile = sizeof(szFile);
    ofn.lpstrFilter = "所有文件\0*.*\0TXT\*\0";
    ofn.nFilterIndex = 1;
    ofn.lpstrFileTitle = NULL;
    ofn.nMaxFile = 0;
    ofn.lpstrInitialDir = NULL;
    ofn.Flags = OFN_MUSTEXIST;
    if (GetOpenFileNameA(&ofn) == TRUE)
    {
        strncpy_s(szFileName, MAX_PATH, szFile, _TRUNCATE);
        return TRUE;
    }
    return FALSE;
}
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_209_0.png)

# 工作原理

这种方法与上一个示例中使用的方法略有不同。我们不是根据处理器数量创建相应线程，而是实例化一个信号量对象，其初始计数不会超过 CPU 的数量。它们非常相似；唯一的区别在于 `StartAddress` 例程内部使用的技术和选择的方法。在操作成功后，我们通过递减计数来释放信号量：

```cpp
WaitForSingleObject(hSemaphore, INFINITE);
ReleaseSemaphore(hSemaphore, 1, NULL);
```

# 使用事件

事件对象充当信号，以特定方式提醒线程。它可以用于启动或停止执行、在执行用户输入时触发等。我们将使用相同的示例作为事件来通知线程用户想要取消并结束程序。通过这种方式，我们将使应用程序更加用户友好并对用户输入做出响应。

# 准备工作

确保 Visual Studio 正在运行。现在让我们创建程序并解释其结构。

1. 创建一个名为 `concurrent_operations` 的新 C++ 应用程序。
2. 打开解决方案管理器，右键点击头文件。添加名为 `CQueue.h` 的现有头文件。
3. 打开解决方案管理器，右键点击头文件。添加名为 `main.h` 的新头文件。
4. 添加以下代码：

```cpp
#pragma once

#include <windows.h>
#include <commctrl.h>
#include <tchar.h>
#include <psapi.h>
#include <strsafe.h>
#include <iostream>
#include <fstream>
#include <string>
#include <queue>

using namespace std;

#define CONTROL_PROGRESS 1
#define CONTROL_RESULT 2
#define CONTROL_BROWSE 3
#define CONTROL_START 4
#define CONTROL_TEXT 5

struct QueueElement {
    int iA1, iB1, iC1;
    int iA2, iB2, iC2;
    HWND hWndProgress;
    HWND hWndResult;
};

typedef queue<QueueElement*> CQueue;

DWORDAPI StartAddress(LPVOID lParameter);
BOOL FileDialog(HWND hWnd, LPSTR szFileName);
LRESULT CALLBACK WindowProc(HWND, UINT, WPARAM, LPARAM);

extern CQueue queue;
extern char szResult[4096];
extern TCHAR szEvent[];
```

5. 在**解决方案管理器**中右键点击**源文件**。添加名为 `main.cpp` 的源文件。
6. 添加以下代码：

```cpp
#include "main.h"

CQueue queue;
char szResult[4096];
TCHAR szEvent[] = _T("Event");

// (此处省略 main 函数及具体实现细节，以保持逻辑一致)
```

