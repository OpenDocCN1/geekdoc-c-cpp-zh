
Passing Interface"), `WS_OVERLAPPED` | `WS_CAPTION` | `WS_SYMENU`

`WS_MINIMIZEBOX`, 200, 200, 440, 340, `NULL`, `NULL`, `wndEx.hInstance`,

`NULL`);

```cpp
if (!hWnd) {
    return NULL;
}
```

```cpp
HFONT hFont = CreateFont(14, 0, 0, FW_NORMAL, FALSE,
FALSE, FALSE, BALTIC_CHARSET, OUT_DEFAULT_PRECIS,
CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY, DEFAULT_PITCH
| FF_MODERN, _T("Microsoft Sans Serif"));
```

```cpp
hWnd buttonMsg = CreateWindow(_T("BUTTON"), _T("Show msg"),
WS_CHILD | WS_VISIBLE | BS_PUSHBUTTON | WS_TABSTOP, 190,
260, 100, 25, hWnd, (HMENU)BUTTON_MSG, wndEx.hInstance, NULL);
```

```cpp
hWnd buttonClose = CreateWindow(_T("BUTTON"), _T("Close me"),
WS_CHILD | WS_VISIBLE | BS_PUSHBUTTON | WS_TABSTOP, 310, 260,
100, 25, hWnd, (HMENU)BUTTON_CLOSE, wndEx.hInstance, NULL);
```

```cpp
HWND hText = CreateWindow(_T("STATIC"), NULL, WS_CHILD |
WS_VISIBLE | SS_BORDER, 15, 20, 390, 220, hWnd,
(HMENU)LABEL_TEXT, wndEx.hInstance, NULL);
```

```cpp
SendMessage(buttonMsg, WM_SETFONT, (WPARAM)hFont, TRUE);
SendMessage(buttonClose, WM_SETFONT, (WPARAM)hFont, TRUE);
SendMessage(hText, WM_SETFONT, (WPARAM)hFont, TRUE);
```

```cpp
ShowWindow(hWnd, hWndShow);
UpdateWindow(hWnd);
```

```cpp
MSG msg;
while (GetMessage(&msg, 0, 0, 0)) {
    TranslateMessage(&msg);
```

# 第 4 章

```cpp
DispatchMessage(&msg);
}
```

```cpp
UnregisterClass(wndEx.lpszClassName, wndEx.hInstance);
```

```cpp
return (int)msg.wParam;
}
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM
wParam, LPARAM lParam)
{
    switch (uMsg)
    {
    switch (LOWWORD(wParam))
    {
        case BUTTON_MSG:
            MessageBox(hWnd, _T("Hello!"), _T("Basic MPI"), MB_OK |
MB_TOPMOST);
            break;
        }
        case BUTTON_CLOSE:
        {
            PostMessage(hWnd, WM_CLOSE, 0, 0);
            break;
        }
    }
    break;
    case WM_MOUSEMOVE:
    {
        int xPos = GET_X_LPARAM(lParam);
        int yPos = GET_Y_LPARAM(lParam);
        TCHAR szBuffer[4096];
        sprintf(szBuffer,
            _T("Cursor X: %d\nCursor Y position: %d"), xPos,
            yPos);
        HWND hText = GetDlgItem(hWnd, LABEL_TEXT);
        break;
    }
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_159_0.png)

  case WM_DESTROY:
  {
    PostQuitMessage(0);
    break;
  }
  default:
  {
    return DefWindowProc(hWnd, uMsg, wParam, lParam);

## 它是如何工作的...

此示例的目的是演示基础的消息传递。你需要注意我们之前定义的 `BUTTON_CLOSE` 和 `LABEL` 宏。我们稍后需要它们作为子控件标识符。对于子窗口，`hMenu` 指定了子窗口标识符。

> 子控件标识符是窗口用于通知父窗口事件的整数值。应用程序确定子窗口标识符，对于同一个父窗口的所有子窗口，它必须是唯一的（参考 MSDN）。

现在让我们检查 `WinMain` 入口。我们创建了 `WNDCLASS` 实例并对其初始化。在成功注册窗口类并随后调用 `RegisterClass` 后，我们创建了主窗口，然后调用 `CreateWindow`。

然后，我们需要创建一个文本标签和按钮控件。按钮和标签也是具有预定义系统类的窗口（如 `BUTTON`、`STATIC` 等）。有关完整的系统类参考，请参 http://msdn.microsoft.com/en-us/library/windows/ ...

# 第 4 章

```cpp
#define DRAWING_TIME    2300
#define EVENT_NAME      T("__t_event__")
typedef struct tagPLOTDATA
{
    int value;
    DWORD dwThreadId;
    int imMsgID;
} PLOTDATA, *PPLOTDATA;
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam);
WORD WINAPI StartAddress(LPVOID lpParameter);
WORD WINAPI DrawPlot(LPVOID lpParameter);
int iMessageID = NULL;
int iMessageID = 0;
HANDLE gEvent = NULL;
HANDLE hThreads = [THREAD_NUMBER];
HANDLE hThread = NULL;
CRITICAL_SECTION cs;
CQueue<PLOTDATA> queue;
int WINAPI _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR szCommandLine, int nShow)
{
    UNREFERENCED_PARAMETER(hPrev);
    UNREFERENCED_PARAMETER(szCommandLine);
    InitializeCriticalSection(&cs);
    TCHAR* szWindowClass = T("__basic_MPI_Wnd_class__");
    WNDCLASSSEX wndEx = { 0 };
    wndEx.cbSize = sizeof(WNDCLASSSEX);
    wndEx.style = CS_HREDRAW | CS_VREDRAW;
    wndEx.lpWndProc = WindowProcedure;
    wndEx.cbClExtra = 0;
    wndEx.cbWndExtra = 0;
    wndEx.hInstance = hThis;
    wndEx.hIcon = LoadIcon(wndEx.hInstance, MAKEINRESOURCE(IDI_APPLICATION));
    wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
```

## 消息传递

```cpp
    wndEx.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
    wndEx.lpszMenuName = NULL;
    wndEx.lpszClassName = szWindowClass;
    wndEx.hIcon = LoadIcon(wndEx.hInstance, MAKEINTRESOURCEINFO(IDI_APPLICATION));
```

```cpp
    if (!RegisterClassEx(&wndEx))
    {
        return 1;
    }
```

InitCommonControls();

```cpp
    HWND hWnd = CreateWindow(szWindowClass, _T("Basic Message Passing Interface"), WS_OVERLAPPED | WS_CAPTION | WS_SYSMENU | WS_MINIMIZEBOX, 200, 200, 440, 300, NULL, NULL, wndEx.hInstance, NULL);
```

```cpp
    if (!hWnd)
    {
        return NULL;
    }
```

```cpp
    hFont = CreateFont(14, 0, 0, 0, FW_NORMAL, FALSE, FALSE, FALSE, BALTIC_CHARSET, OUT_DEFAULT_PRECIS, CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY, DEFAULT_PITCH | FF_MODERN, _T("Microsoft Sans Serif"));
```

```cpp
    hText = CreateWindow(_T("STATIC"), NULL, WS_CHILD | WS_VISIBLE | SS_LEFT | SS_BORDER, 15, 20, 300, 220, hWnd, (HMENU)LABEL_TEXT, wndEx.hInstance, NULL);
```

```cpp
    SendMessage(hText, WM_SETFONT, (WPARAM)hFont, TRUE);
```

```cpp
    Show(hWnd, nCmdShow);
    MSG msg;
    while (GetMessage(&msg, 0, 0, 0))
    {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
```

}

    UnregisterClass(wndEx.pszClassName, wndEx.hInstance);
    WaitForMultipleObjects(THREAD_NUMBER, hThreads, TRUE, INFINITE);
    CloseHandle(hThread);
    CloseHandle(gEvent);
    DeleteCriticalSection(&cs);
    return (int)msg.wParam;
}
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
    switch (uMsg)
    {
    case WM_CREATE:
        gEvent = CreateEvent(NULL, TRUE, FALSE);
        for (int iIndex = 0; iIndex < THREAD_NUMBER; iIndex++)
            hThreads[iIndex] = CreateThread(NULL, 0, (LPTHREAD_ROUTINE)StartAddress, hWnd, 0, NULL);
        return 0;
    case WM_PAINT:
        hThread = CreateThread(NULL, 0, (LPTHREAD_ROUTINE)DrawPlot, hWnd, 0, NULL);
        return 0;
    case WM_PLOTDATA:
    {
        PPLOTDATA pData = (PPLOTDATA)lParam;
        HWND hLabel = GetDlgItem(hWnd, LABEL_TEXT);
        TCHAR szBuffer[BUFFER_SIZE];
        GetWindowText(hLabel, szBuffer, BUFFER_SIZE);
        sprintf(szBuffer, "%s\n\nMessage has been received. Msg ID:\t%d", szBuffer, pData->iMsgID);
        SetWindowText(hLabel, szBuffer);
        free(pData);
        break;
    }
    case WM_ENDTASK:
    {
        HWND hLabel = GetDlgItem(hWnd, LABEL_TEXT);
        TCHAR szBuffer[BUFFER_SIZE];
        sprintf(szBuffer, "%s\n\nPlot is drawn. You can close the window.");
        SetWindowText(hLabel, szBuffer);
        break;
    }
    case WM_DESTROY:
    {
        PostQuitMessage(0);
        break;
    }
    default:
    {
        return DefWindowProc(hWnd, uMsg, wParam, lParam);
    }
    }
    return 0;
}
WORD WINAPI StartAddress(LPVOID lpParameter)
{
    HWND hWnd = (HWND)lpParameter;
```

```cpp
    HANDLE hEvent = OpenEvent(EVENT_ALL_ACCESS, FALSE, EVENT_NAME);
```

```cpp
    if (hEvent != NULL)
    {
        SetEvent(hEvent);
    }
    CloseHandle(hEvent);
```

```cpp
    int iCount = 0;
    while (iCount++ < MAX_COUNT)
    {
        PLOTDATA* pData = (PLOTDATA*)malloc(sizeof(PLOTDATA));
        pData->iMsgID = rand() % 100;
        SendMessage(hWnd, WM_PLOTDATA, 0, (LPARAM)pData);
        WaitForSingleObject(gEvent, INFINITE);
    }
    return 0;
}
WORD WINAPI DrawPlot(LPVOID lpParameter)
{
    HWND hWnd = (HWND)lpParameter;
    // 绘图逻辑...
    SendMessage(hWnd, WM_ENDTASK, 0, 0);
    return 0;
}
```

## 使用线程消息队列

正如我们之前提到的，我们可以在不创建窗口（UI）的情况下向线程发送消息。在在上一个示例中，我们简单地使用了为线程创建的消息队列，因为它拥有一个窗口。在这里，我们将解释如何在不使用窗口消息队列的情况下传递消息。

由于示例的简单性，我们将在用户每次点击按钮时都向线程发送一条消息。

此类任务的类比是：如果我们想创建一个显示天气预报信息的应用程序，我们将有两个线程：一个线程负责压力计、风速计等物理设备，而另一个线程则需要等待从第一个线程收集的数据。在获取数据后，它可以对其进行处理并显示给用户。

## 准备工作

确保 `Visual Studio` 已启动运行。

# 如何实现...

现在，让我们创建程序并解释其结构。执行以下步骤：

- 1. 创建一个名为 `threadMPI` 的新 C++ Windows 应用程序。

- 2. 打开解决方案管理器（Solution Explorer），右键点击头文件（Header files）。从第1章“C++概念与特性简介”添加头文件 `CQueue.h`。
