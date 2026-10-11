
然后主线程将等待，直到新创建的线程开始执行，之后就可以调用它的句柄。现在，让我们检查 `StartAddress` 例程。主窗口句柄作为参数传递进来，因此我们需要将 `LPVOID` 强制转换为线程类型。我们将线程优先级设置为比 `NORMAL` 低一级（`THREAD_PRIORITY_BELOW_NORMAL`），因为主线程的优先级至少要比绘图线程高。解释一下：假设用户期望应用程序至少具有响应性。在这个示例中，我们的工作线程有一个非常简单的任务要执行：它绘制矩形，每 10 个矩形之间暂停 0.1 秒。在另一种情况下，如果绘图线程应该调用具有大量迭代的傅里叶级数，如果该线程优先级低于或等于主线程，应用程序将失去响应。这是因为调度器会根据其优先级和调度算法来选择下一个执行的线程。如果主线程优先级更高，应用程序将无法立即对用户输入做出响应。它仍然会处理用户输入，但要在工作线程获得 CPU 时间之后，这会导致应用程序运行缓慢。在设置优先级后，该线程将进入一个无限循环，不断绘制矩形，直到用户关闭应用程序。

> 傅里叶级数是周期函数的表示，通常表示为正弦和余弦函数的无限和。它在图形学、语音识别、手写等领域有许多应用。

让我们关注 `DrawProc` 绘图例程。在调用 `rand` 函数重新设定随机数生成器后，我们需要获取一个绘图上下文。然后我们将获取位于应用程序窗口边界内的坐标和随机颜色来绘制实际的矩形。`GetNextSeed` 例程在第一次调用时会将种子值设置为当前时间戳，因为静态变量只初始化一次，此后我们只需通过增加其值来确保时间值的唯一性。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_189_0.png)

## 线程同步与控制操作

当用户想要关闭应用程序时，我们将打开一个事件并将其状态设置为信号状态（signaled）。这样，线程将在下一次调用 `WaitForSingleObject` 时退出。然后我们将获取与主窗口关联的工作线程标识符，并使用 `WaitForSingleObject` 函数等待其退出。

## 更多内容...

我们可能会得出结论，认为如果我们为线程设置高优先级，应用程序将运行得更快。事实上，这是错误的。请注意，如果你增加了各种应用程序的优先级（无论是进程优先级还是线程优先级），系统将花费大量时间处理这些线程，但它们将无法完成任务，导致系统缓慢甚至无响应。如果你打开任务管理器，你会发现极少数窗口/进程的优先级高于 `NORMAL`。通常这些是 `dwm.exe`（桌面窗口管理器）和 `taskmgr.exe`（Windows 任务管理器）。Windows 设置了两个高优先级的桌面进程以响应用户命令，就像我们的应用程序优先考虑输入而非绘图（计算）一样。你必须谨慎使用优先级，我们的建议是只有在必须时才增加优先级。

# Windows 调度器对象与调度

正如我们之前学到的，为了选择下一个执行的线程，调度器从队列中选择线程，从高高到低排序。队列并不包含所有线程，其中某些线程处于挂起或阻塞状态。我们之前提到有三种状态：运行（Running）、就绪（Ready）和阻塞（Blocked）。这些是基本的条件状态。现在，让我们扩展并解释所有这些状态。

在任何时刻，线程都处于以下状态之一：

- 就绪（Ready）：它留留在队列中等待执行
- 待命（Standby）：它是下一个执行的线程
- 运行（Running）：它正在执行——它正在等待恢复信号
- 转换（Transition）：它将在系统加载其上下文后立即被执行
- 终止（Terminated）：它已执行完毕，但对象尚未被删除

当调度器选择下一个线程执行时，系统将其上下文加载到内存中。上下文包含一系列值，如机器寄存器值、内核栈、环境块和位于进程地址空间的用户数据，即使部分上下文被交换到磁盘，线程也会进入转换状态，尽管系统会收集这部分内容。切换线程意味着保存上下文的所有部分并加载下一个线程的所有部分。

新加载的线程执行一段时间，这被称为一个量子（quantum）。系统维护一个计数器来测量当前时间。每经过一个时钟周期，系统会将计数器递减一个特定值。当计数器归零时，调度器执行上下文切换，并为下一个线程执行做好准备。

## 使用互斥（mutex）

Windows 同步对象之一是互斥（mutex）。当我们想要获取某些共享对象的独占访问权限时，我们使用互斥。当我们想要保护某些由一次线程执行的代码段时，我们也使用互斥。在我们的示例中，我们将要求用户提供一个每行包含整数坐标的文本文件，以计算线性方程组：

```
$$\begin{cases}ax_x+b_y=c_1\\ax_x+b_y=c_2\end{cases}$$
```

我们使用在第一章中实现的 `CQueue` 类。我们的任务是从文件中加载所有值，然后将每组坐标加入队列。当每组加载后，我们将启动若干线程进行并发计算。这里需要做的决策是启动多少线程，以及哪些代码区域需要保护和同步。

## 准备工作

确保 Visual Studio 正在运行。

## 如何实现

现在，让我们创建程序并解释其结构。执行以下步骤：

- 1. 创建名为 `concurrent_operations` 的空 C++ 应用程序。
- 2. 在解决方案管理器中，右键点击头文件，添加第一章中使用的现有头文件，命名为 `Queue.h`。
- 3. 在解决方案管理器中，右键点击头文件，添加名为 `main.h` 的新头文件。打开 `main.h`。

# 线程同步与并发操作

4. 添加以下代码：

```cpp
#pragma once

#include <windows.h>

#include <commctrl.h>

#include <tchar.h>

#include <psapi.h>

#include <strsafe.h>

#include <string.h>

#include <iostream>

#include <fstream>

#include <cmmdlg.h>

#include "Queue.h"

#pragma comment ( lib, "comt132.lib" )

#pragma comment ( linker, "/manifestdependency:type='win32' /\
version='6.0.0.0' processorArchitecture='*' /\
publicKeyToken='E659B56E444ccf1d' language='*' )
```

```cpp
using namespace std;
```

```cpp
#define CONTROL_BROWSE 100

#define CONTROL_START 101

#define CONTROL_RESULT 103

#define CONTROL_TEXT 104

#define CONTROL_PROGRESS 105
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
WORD WINAPI StartAddress(LPVOID lpParameter)
BOOL FileDialog(HWND hWnd, LPSTR szFileName);
```

```cpp
typedef struct

{

int ia1;

int ib1;

int ic1;

int ia2;

int ib2;

int ic2;

HND hWndProgress;

HND hWndResult;

QueueElement, *PQueueElement;
```

5. 打开解决方案管理器并右键点击源文件。添加一个名为 main 的新源文件。打开 `main.cpp`。

6. 添加以下代码：
```cpp
#pragma once
```

```
* 你需要指定带有坐标的文本文件。
* 我们的示例将求解一个二元线性方程组
* a1 + b1 = c1;
* a2x + b2y = c2;
*
* 每行应恰好有六个坐标。
* 文件格式示例：
*
* 4 -3 2 -7 5 6
* 12 1 -7 9 -5 8
*
* 避免文件末尾有空行。
*/
```
```cpp
#include "main.h"
```

```cpp
char szFilePath[MAX_PATH] = { 0 };
char szResult[4096];
CQueueElement* queue = queue;
TCHAR* szMutex = _T("__mutex_132__");
int WINAPI _tWinMain(HINSTANCE INSTANCE hThis, HINSTANCE hPrev,
LPSTR szCommandLine, int nCmdShowShow)
{
UNREFERENCED_PARAMETER(hPrev)
UNREFERENCED_PARAMETER(szCommandLine);
TCHAR* szWindowClass = _T("__concurrent_operations__");
WNDCLASSEX wndEx = { 0 };
wndEx.cbSize = sizeof(WNDCLASS);
wndEx.style = CS_HREDRAW | CS_VREDRAW;
wndEx.lpWndProc = WindowProcedure;
wndEx.cbClExtra = 0;
wndEx.cbWndExtra = 0;
wndEx.hInstance = hThis;
wndEx.hIcon = LoadIcon(wndEx.hInstance, IDI_APPLICATION,
MAKEINSOURCE(IDI_APPLICATION));
```

# 线程同步与并发操作

```cpp
wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
wndEx.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
wndEx.lpszMenuName = NULL;
wndEx.lpszClassName = szWindowClass;
wndEx.hIconEm = LoadIcon(wndEx.hInstance,
MAKERESOURCE(IDC, ID_APPLICATION));
```

```cpp
if (!RegisterClassEx(&wndEx))
{
    return 1;
}
```

```cpp
InitCommonControls();
hwnd hWnd = CreateWindow(szWindowClass,
T("Concurrent operations"), WS_OVERLAPPED|WS_CAPTION | WS_SYSMENU, 50, 50, 305, 250, NULL, NULL,
wndEx.hInstance, NULL);
```

```cpp
if (hWnd)
{
    return NULL;
}
```

```cpp
HFONT hFont = CreateFont(14, 0, 0, FW_NORMAL, FALSE,
FALSE, FALSE, BALTIC_CHARSET, OUT_DEFAULT_PRECIS,
CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY, DEFAULT_PITCH
| FF_MODERN, T("Microsoft Sans Serif"));
```

```cpp
HWND hLabel = CreateWindow(T("STATIC"), T("浏览并选择带有坐标的文件: ****"),
WS_CHILD | WS_VISIBLE | SS_CENTERIMAGE | SS_LEFT | WS_BORDER,
20, 20, 250, 25, hWnd, (HMENU) CONTROL_TEXT, wndEx.hInstance,
NULL);
SendMessage(hLabel, WM_SETTEXT, (WPARAM)hFont, TRUE);
```

```cpp
HWND hResult = CreateWindow(T("STATIC"), T("*"),
WS_VISIBLE | SS_LEFT | WS_BORDER, 20, 65, 150, 75, hWnd,
(HMENU) CONTROL_RESULT, wndEx.hInstance, NULL);
SendMessage(hResult, WM_SETFONT, (WPARAM)hFont, TRUE);
```

```cpp
HWND hBrowse = CreateWindow(T("BUTTON"), T("浏览"), WS_CHILD
WS_VISIBLE
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_194_0.png)

# 第 5 章

```cpp
| BS_PUSHBUTTON, 190, 65, 80, 25, hWnd, (HMENU) CONTROL_BROWSE,
wndEx.hInstance, NULL);
SendMessage(hBrowse, WM_SETFONT, (WPARAM) hFont, TRUE);
```

```cpp
HWND hStart = CreateWindowEx(_T("BUTTON"), _T("开始"), WS_CHILD |
| WS_VISIBLE
| BS_PUSHBUTTON, 190, 115, 80, 25, hWnd, (HMENU) CONTROL_START,
wndEx.hInstance, NULL);
SendMessage(hStart, WM_SETFONT, (WPARAM) hFont, TRUE);
```

```cpp
HWND hProgress = CreateWindow(_PROGRESS_CLASS, _T(""), WS_CHILD |
WS_VISIBLE
| BS_BORDER, 20, 165, 250, 25, hWnd, (HMENU) CONTROL_PROGRESS,
wndEx.hInstance, NULL);
SendMessage(hProgress, PBM_SETSTEP, (WPARAM) 1, 0);
SendMessage(hProgress, PBM_SETPOS, (WPARAM) 0, 0);
```

```cpp
ShowWindow(hWnd, nCmdShow);
```

```cpp
HANDLE hMutex = CreateMutex(NULL, FALSE, szMutex);
MSG msg;
while (GetMessage(&msg, 0, 0))
{
  TranslateMessage(&msg);
  DispatchMessage(&msg);
}
```

```cpp
CloseHandle(hMutex);
UnregisterClass(wndEx.ClassName, wndEx.hInstance);
return (int)msg.wParam;
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
  switch (uMsg)
  {
    case WM_DESTROY:
      PostQuitMessage(0);
      break;
    case WM_COMMAND:
      switch (LOWORD(wParam)) {
        case CONTROL_BROWSE:
          if (!FileDialog(hWnd, szFilePath)) {
            MessageBox(hWnd, T("必须选择有效的路径！"), T("错误!"), MB_TOPMOST | MB_ICONERROR);
          }
          else {
            char szBuffer[MAX_PATH];
            sprintf(szBuffer, "\n文件: %s", strrchr(szFilePath, '\\') + 1);
            SetWindowTextA(GetDlgItem(hWnd, CONTROL_TEXT), szBuffer);
          }
          break;
        case CONTROL_START:
          if (!szFilePath) {
            MessageBox(hWnd, T("必须先选择有效路径！"), T("错误!"), MB_TOPMOST | MB_ICONERROR);
          }
          ifstream infile(szFilePath);
          if (infile.is_open()) {
            string line;
            while (std::getline(infile, line)) {
              QueueElement* pQueueElement = new QueueElement();
              istringstream iss(line);
```
