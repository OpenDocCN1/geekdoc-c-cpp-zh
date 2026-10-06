
当一个线程结束时，调度器会寻找下一个将执行的线程。在选择下一个线程时，优先级较高的线程更具优势。某些活动（如对断电的响应）始终以较高的优先级执行。执行系统中断的元素优先级高于用户进程。底线是，每个进程都有一个优先级列表，而线程的基础优先级来自于其所属的进程。

如之前所示，线程对象的属性包括基础优先级和动态优先级。当我们使用命令更改优先级时，我们只能更改基础优先级。尽管如此，仍然无法将线程优先级改变超过两个级别，即使是向上或向下移动两个级别也不行。这是因为线程重要性不能超过其父进程。通过线程本身，无法将其优先级改变超过两个步骤，但系统可以。系统允许对需要执行的线程进行某种改进——动态优先级。当线程在应用程序窗口中执行某些操作（如击键或鼠标点击）时，系统始终会增加其所属进程的优先级。当等待硬盘数据的线程获取到数据时，系统也会增加该线程的优先级。这些临时的优先级提升加上基础优先级，就构成了动态优先级。调度程序（或负责调度的元素）、基础优先级和动态优先级的关系如下所示：

| | | | | | | 线程绑定到前台类进程的基础优先级优先级范围 | 同一个线程的优先级范围 |
|---|---|---|---|---|---|---|---|
| 固定优先级 | | | | | | | | |
| | 30 | | | | | | | |
| | 29 | | | | | | | |
| | 28 | | | | | | | |
| | 27 | | | | | | | |
| | 26 | | | | | | | |
| | 25 | | | | | | | |
| | 24 | 实时优先级类 | | | | | | |
| | 23 | | | | | | | |
| | 22 | | | | | | | |
| | 21 | | | | | | | |
| | 20 | | | | | | | |
| | 19 | | | | | | | |
| | 18 | | | | | | | |
| | 17 | | | | | | | |
| | 16 | | | | | | | |
| | 15 | | | | | | | |
| | 14 | | | | | | | |
| | 13 | 高优先级类 | | | | | | |
| | 12 | | | | | | | |
| | 11 | | | | | | | |
| | 10 | 前台类 | | | | | | |
| | 9 | | | | | | | |
| | 8 | | | | | | | |
| | 7 | | | | | | | |
| | 6 | | | | | | | |
| | 5 | | | | | | | |
| | 4 | | | | | | | |
| | 3 | 后台类 | | | | | | |
| | 2 | | | | | | | |
| | 1 | 普通类 | | | | | | |
| | 可更改优先级 | 不同进程的级别 | | | | | | | |

## 线程同步与并发操作

动态优先级的降低在任务完成后立即开始。每当线程在 CPU 上请求时间时，动态优先级就会降低一级，最终稳定在基础优先级上。下面的示例演示了进程和线程的基本用法。我们将创建一个应用程序，其中主线程将拥有主窗口，而另一个线程将负责绘制图形。主线程的优先级至少比绘图线程高一级，这是必要的，因为主线程必须响应任何用户输入，例如移动或关闭应用程序。请确保 Visual Studio 已启动运行。

## 如何实现...

现在，让我们创建我们的程序并解释其结构。

1. 创建一个名为 `basic_priority` 的 C++ Win32 项目。
2. 打开解决方案并右键点击“源文件”。添加一个名为 `basic_priority.cpp` 的新文件。打开 `basic_priority.cpp`。
3. 添加以下代码：

```cpp
#include <windows.h>
#include <windows.h>
#include <time.h>
#include <char.h>
#include <math.h>
#include <comctrl.h>

#pragma comment (lib,"manifest:type='win32'")
#pragma comment (linker,"Microsoft.Common-Controls version='6.0.0.0'")

#define RESET_EVENT _T("reset_event")
#define WINDOW_WIDTH 800
#define WINDOW_HEIGHT 600
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT Msg, WPARAM wParam, LPARAM lParam);
void WINAPI StartAddress(LPVOID lpParameter);
void DrawProc(HWND hWnd);
unsigned GetNextSeed(void);

int WINAPI _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR szCommandLine, int iWndShow)
{
    UNREFERENCED_PARAMETER(hPrev);
    UNREFERENCED_PARAMETER(szCommandLine);

    TCHAR* szWindowClass = _T("priority_wnd_class");

    WNDCLASS wndEx = { 0 };

    wndEx.cbSize = sizeof(WNDCLASS);
    wndEx.style = CS_HREDRAW | CS_REDRAW;
    wndEx.fnWndProc = WindowProc;
    wndEx.cbExtra = 0;
    wndEx.hInstance = hThis;
    wndEx.lpszClassName = szWindowClass;

    if (!RegisterClassEx(&wndEx))
    {
        return 0;
    }

    HWND hndw = CreateWindow(szClassName, T("Basic priority"), WS_OVERLAPPEDWINDOW | WS_VISIBLE, CW_USEDEFAULT, CW_USEDEFAULT, WINDOW_WIDTH, WINDOW_HEIGHT, NULL, NULL, hThis, NULL);

    if (!hndw)
    {
        return 0;
    }

    HANDLE hEvent = CreateEvent(NULL, TRUE, FALSE, RESET_EVENT);

    CREATETHREAD ti;
    HANDLE hThread;
    if (CreateThread(&ti, 0, (LPTHREAD_START_ROINE)StartAddress, (LPVOID)hndw, 0, NULL, &hThread))
    {
        SetThreadPriority(hThread, THREAD_PRIORITY_NORMAL);
        SetWindowLongPtr(hndw, GWLP_USERDATA, (LONG_PTR)hThread);
    }

    MSG msg;
    while (GetMessage(&msg, 0, 0, 0))
    {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }

    return 0;
}

LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT Msg, WPARAM wParam, LPARAM lParam)
{
    switch (Msg)
    {
        case WM_CREATE:
        {
            SetWindowLongPtr(hWnd, GWLP_USERDATA, (LONG_PTR)lParam);
            SetThreadPriority(GetCurrentThread(), THREAD_PRIORITY_NORMAL);
            return 0;
        }
        case WM_SIZE:
        {
            LONG_PTR pThreadData = (LONG_PTR)GetWindowLongPtr(hWnd, GWLP_USERDATA);
            if (pThreadData) {
                // Handle resize
            }
            return 0;
        }
        case WM_PAINT:
        {
            PAINTSTRUCT ps;
            HDC hDC = BeginPaint(hWnd, &ps);
            LONG_PTR pThreadData = (LONG_PTR)GetWindowLongPtr(hWnd, GWLP_USERDATA);
            if (pThreadData) {
                DrawProc(hDC);
            }
            EndPaint(hWnd, &ps);
            return 0;
        }
        case WM_DESTROY:
        {
            PostQuitMessage(0);
            break;
        }
        default:
        {
            return DefWindowProc(hWnd, Msg, wParam, lParam);
        }
    }
    return 0;
}

void WINAPI StartAddress(LPVOID lpParameter)
{
    HWND hWnd = (HWND)lpParameter;
    SetThreadPriority(GetCurrentThread(), THREAD_PRIORITY_HIGH);

    while (true)
    {
        if (WaitForSingleObject(hEvent, 0) == WAIT_OBJECT_0)
        {
            SetThreadPriority(GetCurrentThread(), THREAD_PRIORITY_NORMAL);
            break;
        }
        Sleep(10);
    }
}

void DrawProc(HDC hDC)
{
    for (int i = 0; i < 10; i++) {
        int x = rand() % WINDOW_WIDTH;
        int y = rand() % WINDOW_HEIGHT;
        int size = 10 + rand() % 50;
        HBRUSH brush = CreateSolidBrush(RGB(rand() % 255, rand() % 255, rand() % 255));
        SelectObject(hDC, brush);
        Rectangle(hDC, x, y, x + size, y + size);
        DeleteObject(brush);
    }
}
```
