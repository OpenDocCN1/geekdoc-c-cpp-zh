

# 第 3 章

`Join` 方法设置 `STATE_READY` 标志并等待线程对象变为已信号状态，直到 `dwWaitInterval` 过期为止。`dwWaitInterval` 参数默认设置为 `INFINITE`。

`Suspend` 和 `Resume` 方法分别挂起和恢复线程。在 `Suspend` 和 `Resume` 中会设置 `STATE_BLOCKED` 标志。`thread` 类分配了 `lpUserData` 属性，用于在以后需要时设置用户特定的数据。`SetUserData` 和 `GetUserData` 方法分别设置和获取用户数据。`GetAsyncState` 方法返回对象的异步响应。

`GetState` 和 `SetState` 方法分别获取和设置 `dwState` 值或对象状态。它们用于额外的对象状态更改。

`Alert` 方法将事件状态更改为信号。它用于使用了 `STATE_CONTINUOUS` 的情况。如果一个线程旨在运行连续任务，则必须有某种机制以正常方式停止该线程。因此，当我们有一个或多个线程在持续运行时，我们只需要从其中一个实例调用 `Alert` 即可。它将通知所有线程停止连续工作并返回。

由于类成员函数（方法）有一个第一个隐式参数（未显示）`this`，我们必须将 `StartAddress` 方法声明为静态。然而，我们可以将对象地址（`this` 指针）传递给 `StartAddress` 方法，并使用纯虚函数 `Run` 使其行为像非静态方法。

`GetId` 和 `GetHandle` 方法分别返回唯一的线程标识符和线程句柄。这些方法被实现为内联例程。

# 更多...

在之前的线程实现中，由于代码复用和编程的简单性，我们非常精确地遵循了面向对象的方法。接下来的主题将演示如何非常方便地使用 `CThread`。

# 在没有同步的情况下实现线程

在许多情况下，并行任务需要相互依赖。这种情况可能出现在一个有更多用户界面对话框的应用程序中。例如，在主应用程序窗口上，有一个显示客户的列表视图。在另一个应用程序窗口（或应用程序标签页）上，有一个显示产品的列表视图。当我们启动这样一个应用程序时，先加载客户再加载产品是愚蠢的。我们可以启动两个线程，每个线程负责从数据库加载对象（第一个线程加载客户，另一个线程加载产品）。

![](img/412b0f5bbb36adcce2ddd2d5b7416516_135_0.png)

# 管理线程

现在，让我们回顾一个简单的示例。我们必须初始化主应用程序窗口，然后需要创建四个子窗口。对于每个窗口，我们将创建一个单独线程，且对系统资源没有限制——在我们的示例中，分别为每个窗口创建一个创建一个绘画的画刷。稍后在我们的下一个示例中，我们将假设只有一个可用的画刷，以演示同步操作。

# 准备工作

确保 Visual Studio 正在运行。

# 如何操作..

现在，让我们创建程序并使用以下步骤解释其结构：

- 1. 创建名为 `Async` 的新 C++ Windows 应用程序。
- 2. 添加名为 `AsyncThreads` 的新源文件。打开 `AsyncThreads.cpp`。
- 3. 将以下代码添加到其中：

```cpp
#include "CThread.h"
#include <windows.h>
#include <tchar.h>
#include <time.h>

#define THREADS_NUMBER 4
#define WINDOWS_NUMBER 10
#define SLEEP_TIME 500
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)

class Thread : public CThread
{
protected:
    virtual void Run(LPVOID lpParameter = 0);
}

void Thread::Run(LPVOID lpParameter)
{
    // 重新种子随机生成器
    srand((unsigned)time(NULL));
}

HWND hWnd = (HWND)GetUserData();
```

# 第 3 章

```cpp
RECT rect;

// 获取窗口尺寸
BOOL bError = GetClientRect(hWnd, &rect);
if (!bError)
{
    return;
}

int clientX = rect.right - rect.left;
int clientY = rect.bottom - rect.top;

// 如果窗口没有任何尺寸则不绘制
if ((clientX) || (!clientY))
{
    return;
}

// 获取绘图设备上下文
HDC hDC = GetDC(hWnd);

if (hDC)
{
    // 绘制十个随机图形
for (int iCount = 0; iCount < WINDOWS_NUMBER; iCount++)
    {
        // 设置坐标
        int startX = (int)(rand() % clientX);
        int stopX = (int)(rand() % clientX);
        int startY = (int)(rand() % clientY);
        int stopY = (int)(rand() % clientY);
        // 设置颜色
        int iRed = rand() & 255;
        int iGreen = rand() & 255;
        // 创建画刷
        HBRUSH hBrush = CreateSolidBrush(RGB(iRed, iGreen, rand()));
        HBRUSH hOld = (HBRUSH)SelectObject(hDC, hBrush);
        // 绘制矩形
        Rectangle(hDC, startX, startY, stopX, stopY);
        // 清理
        SelectObject(hDC, hOld);
        DeleteObject(hBrush);
    }
}
ReleaseDC(hWnd, hDC);
```

*(注：由于原文文本中代码块存在严重的乱序和重复，翻译部分已根据逻辑进行了整理，以确保完整性)*

