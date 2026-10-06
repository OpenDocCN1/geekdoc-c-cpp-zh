

# 第3章

现在让我们回顾一下主程序。首先，应用程序窗口所需的 `WNDCLASS` 对象通过 `RegisterClassEx` 调用进行创建、初始化并注册。在我们使用 `CreateWindow` API 创建窗口后，我们必须创建四个让线程在其中执行绘制操作的窗口。随后是调用 `UpdateWindow` 和 `ShowWindow`。我们将使用通过逻辑“或”运算符 `|` 合并的 `STATE_SYNC` 和 `STATE_CONTINUOUS` 标志，然后我们将使用指向窗口句柄的用户数据指针，该指针将用于标识窗口需要绘制的区域。

`SetWindowLongPtr` 调用将用户数据（带有提供的标志 `GWLP_USERDATA`）与第一个参数标识的窗口关联——在我们的案例中，就是主应用程序窗口。第三个参数用于与窗口关联的特定用户数据。我们将传递线程地址，以便在处理消息循环后在 `WindowProcedure` 中使用。

在 `WindowProcedure` 中，我们处理两种情况：用户关闭应用程序以及窗口需要销毁。`WM_CLOSE` 情况我们需要等待线程安全连接完成。首先，我们通过 `GetWindowLongPtr` 获取线程数组的地址，我们之前已经保存了它的地址。只需有一个线程调用 `Alert` 方法就足够了。所有监听事件信号的线程都会接收到它。然后，我们将为每个线程调用 `Join` 并退出程序。

# 更多内容...

如你所观察的，这是一个非常简单的示例，对于之前定义的 `CThread` 类提供了很好的补充。再次强调，当你需要利用代码复用时，面向对象的方法是非常有用的。

# 使用同步线程

与之前的配方不同，在许多情况下，并行任务需要相互依赖执行。这种情况可能会出现在带有用户界面对话框以显示客户以及所选客户支付历史的应用程序中。例如，应用程序窗口中有一个客户列表。下方是所选客户的支付历史列表。在加载初始客户集时，我们需要显示该客户（加载时选中的）的支付历史。我们将启动一个线程来加载客户列表。同时，另一个负责加载特定客户支付历史的线程也将启动。在第一个客户加载之前，支付历史必须等待客户 ID。

现在，让我们回到上一个配方的示例。我们假设情况相同，但这次由于系统资源有限，我们必须初始化主应用程序窗口，然后需要创建四个子窗口。对于每个窗口，我们将创建一个独立的线程；这次，我们分别为每个窗口只持一个画刷。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_141_0.png)

# 管理线程

# 准备工作

确保 Visual Studio 已经启动并运行。

# 如何操作...

现在，让我们创建程序并使用以下步骤解释其结构：

- 1. 创建一个名为 `SyncThreads` 的新空 C++ Windows 应用程序。
- 2. 添加名为 `SyncThreads.cpp` 的新源文件。打开 `SyncThreads.cpp`。
- 3. 将以下代码添加到文件中：

```cpp
#include <CThread.h>
#include <windows.h>
#include <char.h>
#include <time.h>

#define THREADS_NUMBER 4
#define WINDOWS_NUMBER 10
#define SLEEP_TIME 500
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam);
```

```cpp
class Thread : public CThread
protected:
    virtual void Run(LPVOID lpParameter = 0);
};

void Thread::Run(LPVOID lpParameter)
{
    // 重新种子随机生成器
    srand((unsigned)time(NULL));

    HWND hWnd = (HWND)GetUserData();
    RECT rect;

    // 获取窗口尺寸
    BOOL bError = GetClientRect(hWnd, &rect);
    if (!bError)
```

# 第3章

```cpp
return;
}
int iClientX = rect.right - rect.left;
int iClientY = rect.bottom - rect.top;
```

```cpp
// 如果窗口没有尺寸，则不绘制
if (!iClientX) || (!iClientY)
{
  return;
}
```

```cpp
// 获取绘图的设备上下文
HDC hDC = GetDC(hWnd);
```

```cpp
if (hDC)
{// 绘制十个随机图形
for (int iCount = 0; iCount < WINDOWS_NUMBER; iCount++)
{}
```

```cpp
// 设置坐标
int startX = (int)(rand() % iClientX);
int iStopX = (int)(rand() % iClientX);
int iStartY = (int)(rand() % iClientY);
int iStopY = (int)(rand() % iClientY);
// 设置颜色;
int iRed = rand() & 255;
int iGreen = rand() & 255;
int iBlue = rand() & 255;
```

```cpp
// 创建实色画刷
HANDLE hBrush = CreateSolidBrush(GetNearestColor(hDC, RGB(iRed, iGreen, iBlue));
HANDLE hBrOld = SelectBrush(hDC, hBrush);
```

```cpp
Rectangle(hDC, min(startX, iStopX), max(startX, iStopX),
min(startY, iStopY), max(startY, iStopY));

```cpp
// 删除画刷
DeleteObject(hBrOld);
```

```cpp
// 释放设备上下文
ReleaseDC(hWnd, hDC);

![](img/412b0f5bbb36adcce2ddd2d5b7416516_142_0.png)

# 管理线程

```cpp
int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
{
    WNDCLASSSEX wndEx = { 0 };
    wndEx.cbSize = sizeof(WNDCLASSSEX);
    wndEx.style = CS_HREDRAW | CS_VREDRAW;
    wndEx.hInstance = hInstance;
    wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
    wndEx.hbrBackground = (HBRUSH)GetObject(COLOR_WINDOW + 1);
    // 窗口过程
    wndEx.lpfnWndProc = WindowProcedure;
    wndEx.lpszClassName = TEXT("SyncThreads");

    if (!RegisterClassEx(&wndEx))
    {
        return 0;
    }

    HWND hWnd = CreateWindow(wndEx.lpszClassName, TEXT("SyncThreads"),
        WS_OVERLAPPEDWINDOW, CW_USEDEFAULT, CW_USEDEFAULT, 400, 600,
        NULL, NULL, hInstance, NULL);

    Thread threads[THREADS_NUMBER];
    for (int iIndex = 0; iIndex < THREADS_NUMBER; iIndex++)
    {
        SetWindowLongPtr(hWnd, GWLP_USERDATA, (LONG_PTR)&threads[iIndex]);
        threads[iIndex].Create(NULL, STATE_SYNC | STATE_CONTINUOUS);
    }

    UpdateWindow(hWnd);
    ShowWindow(hWnd, SW_SHOW);

    MSG msg = {0};
    while (GetMessage(&msg, 0, 0, 0))
    {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }

    for (int iIndex = 0; iIndex < THREADS_NUMBER; iIndex++)
    {
        threads[iIndex].Join();
    }

    UnregisterClass(wndEx.lpszClassName, hInstance);
    return 0;
}
```

