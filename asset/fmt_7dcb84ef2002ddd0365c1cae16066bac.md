
# 17 Windows 编程

- 消息框的作用
- 窗口来了...
- 更多窗口
- 真实世界的窗口创建、显示与窗口交互（窗口对消息做出响应）
- 程序实例
- 总结
- 练习

# 562

# 让我们学习 C 语言

事件驱动编程需要思维的转变。我希望第 16 章已经带了这种转变。然而，通过编写事件驱动程序可以进一步加强这种变化。这正是本章想要完成的。我希望当你读到本章末尾时，你会发现自己对它就像已经用它了一辈子一样从容。

# 消息框的作用

在程序执行过程中，我们通常需要在屏幕上显示某些结果。这样做是为了确认我们获得的结果是否符合预期。在基于 DOS 的顺序执行程序中，我们可以轻松地使用 `printf` 语句实现这一点。但在 Windows 下，屏幕是一个共享资源。因此，你可以想象一下如果允许所有运行的应用程序直接向屏幕写入内容会造成多大的混乱。你无法判断哪个输出属于哪个应用程序。因此，没有任何 Windows 程序被允许直接向屏幕写入任何内容。这就是消息框登场的地方。使用它可以在程序执行过程中显示中间结果。可以通过点击其标题栏中的“关闭按钮”或点击其包含的“确定”按钮来关闭它。你可以尝试 `MessageBox()` 的许多变体。其中一些如文所示：

```c
MessageBox (0, "Are you sure", "Caption", MB_YESNO);
MessageBox (0, "Print to the Printer", "MB_YESNO | CANCEL);
MessageBox (0, "icon is all style", "Caption", MB_OK | MB_ICONINFORMATION);
```

你可以将这些语句放在 `WinMain()` 中并亲眼观察结果。虽然上面的消息框在显示结果、按钮、图标方面提供了灵活性，但它们能伸展的程度是有极限的。如果我们想在消息框中绘制手绘图形或显示图像等怎么办？这是不可能的。

# 第 17 章：Windows 编程

为了实现这一点，我们需要创建一个完整的窗口。下一节将讨论如何实现。

# 窗口来了...

在开始实际创建窗口之前，识别窗口的各种元素将是一个好主意。这些元素如图 17.1 所示。

![](img/0a2b9a1d8482fa3ff7aa8a4a25b7ce2b_586_0.png)

图 17.1

注意，绘制在屏幕上的每个窗口并不一定包含上述图中显示的所有元素。例如，窗口可能不包含最小化框、最大化框、滚动条和菜单。

现在让我们创建一个在屏幕上创建窗口的简单程序。这里是程序...

```c
#include <windows.h>

int _stdcall WinMain ( HINSTANCE hInstance, HINSTANCE hPrevInstance,
    LPSTR lpszCmdLine, int nCmdShow )
{
    HWND h;

    h = CreateWindow ( "BUTTON", "Hit Me", WS_OVERLAPPEDWINDOW,
    10, 10, 150, 100, 0, 0, hInstance, 0 );
    ShowWindow ( h, nCmdShow );
    MessageBox ( "Hi!", "Waiting", MB_OK );
    return 0;
}
```

这是程序的输出结果...

![](img/0a2b9a1d8482fa3ff7aa8a4a25b7ce2b_587_0.png)

图 17.2

现在让我们理解这个程序。每个窗口都拥有某些属性——背景颜色、光标形状、图标等。所有这些属性合在一起被称为窗口类。窗口类要求在尝试创建窗口之前进行注册。一旦注册了窗口类，我们就可以创建许多许多该类型的窗口。预定义的窗口类有 `BUTTON`、`EDIT`、`LISTBOX` 等。为了实际创建一个窗口，我们需要调用 `CreateWindow()`。该函数需要多个参数。第二个参数指示窗口样式。接下来的四个参数指定窗口的左上角坐标、宽度和高度（像素）。最后一个参数是父窗口的指针。`ShowWindow()` 参数指示窗口将如何显示。如果是 `SW_NORMAL`，我们得到一个正常窗口；如果是 `SW_MINIMIZED`，我们得到一个最小化窗口；如果是 `SW_MAXIMIZED`，我们得到一个最大化窗口。参数的值是 `nCmdShow`。

# 566

# 让我们学习 C 语言

`WS_OVERAPPED` 样式包含以下内容的集合：

- `WS_CAPTION`
- `WS_SMENU`
- `WS_THICKFRAME`
- `WS_MINIMBOX`
- `WS_MAXIMBOX`

这些宏定义在 `Windows.h` 头文件中。执行此程序时，会出现如图 17.2 所示的消息框。一旦点击“确定”，消息框就会消失。这是因为这样做 `WinMain()` 就结束了，而且我们没有与窗口进行交互。

## 更多窗口

既然我们已经知道了如何创建窗口，让我们在屏幕上创建多个窗口。实现此点的程序如下：

```c
#include <windows.h>

int _stdcall WinMain ( HINSTANCE hInstance, HINSTANCE hPrevInstance,
LPSTR lpszCmdline, int nCmdShow )
{
  HWND h[10];
    int x;

    for ( x = 0 ; x <= 9 ; x++ )
  {
    h[x] = CreateWindow ( "BUTTON", "Press Me", WS_OVERAPPEDWINDOW,
      x * 20, x * 20, 150, 100, 0, 0, hInstance, 0 );
    ShowWindow( h[x], nCmdShow );
  }
  return 0;
}
```

# 真实世界的窗口

假设我们想创建一个窗口并在其中绘制一些形状。对于创建这样的窗口，没有标准的窗口类可用。因此，我们必须创建自己的窗口类，将其注册到 Windows 系统，然后根据它创建窗口。与其直接编写在窗口中绘制形状的程序，让我们先写一个使用我们的窗口类创建窗口并允许我们与其交互的程序。这里是程序...

```c
#include <windows.h>
#include <helper.h>

void OnDestroy ( HWND );

int _stdcall WinMain ( HINSTANCE hInstance, HINSTANCE hPrevInstance,
LPSTR lpszCmdline, int nCmdShow )
{
  MSG m ;
/* 执行应用程序初始化 */
  InitInstance ( hInstance, nCmdShow, "title" );
/* 消息循环 */
  while ( GetMessage ( &m, 0, 0, 0 ) )
    DispatchMessage ( &m );
return 0;
}

LRESULT CALLBACK WndProc ( HWND hWnd, UINT message,
  WPARAM wParam, LPARAM iParam )
{
  switch ( message )
  {
    case WM_DESTROY:
      OnDestroy ( hWnd );
      break;
    default:
      return DefWindowProc ( hWnd, message, wParam,
iParam ); }
  return
0; }
```

# 第 17 章：Windows 编程

```cpp
void OnDestroy ( HWND )
{
  PostQuitMessage(0);
}
```

执行此程序时，屏幕上会显示图 17.4 所示的窗口。我们可以使用标题栏上的最小化和最大化按钮来最小化和最大化窗口。我们可以通过拖动边界来伸缩窗口大小。最后，我们可以点击标题栏上的关闭按钮来关闭窗口。

![](img/0a2b9a1d8482fa3ff7aa8a4a25b7ce2b_592_0.png)

图 17.4

现在让我们一步步尝试理解这个程序。

## 窗口的创建与显示

在屏幕上创建并显示窗口是一个 4 步骤的过程。这些步骤是：

- (a) 创建窗口类。
- (b) 向操作系统注册窗口类。
- (c) 根据已注册的类创建窗口。
- (d) 在屏幕上显示窗口。

创建窗口类涉及设置一个名为 `WNDCLASSSEX` 的结构体元素。该结构体包含多个元素，它们决定了窗口的属性。注册窗口类、创建窗口和显示窗口分别涉及调用 API 函数 `RegisterClassEx()`、`CreateWindow()` 和 `ShowWindow()`。由于本章中的几乎每个程序都需要上述所有 4 个步骤，因此我将这些代码写在 `helper.h` 文件中一个名为 `InitInstance()` 的用户定义函数中。

尽管在头文件中编写代码不符合惯例，但为了实现简单起见，我仍然这样做了。`helper.h` 文件的完整列表可见附录 F。或者，你也可以从以下链接下载：

`www.kicit.com/books/letusc/sourcecode/helper.h`

如预期的那样，`WinMain` 开始调用位于 `helper.h` 中的 `InitInstance()` 函数。该文件在程序开头已被 `#included`。请记住将此文件复制到你的项目目录中——即你准备用来创建此程序的目录。

一旦窗口被创建并显示，让我们看看如何与它交互。

## 与窗口的交互

当用户与窗口交互时（例如通过拉伸边界或点击标题栏中的按钮等），一个适当的消息会被发送到我们应用程序的消息队列中。我们的应用程序现在应该从消息队列中获取这些消息并处理它们。

消息包含一个消息 ID 和一些关于消息的其他额外信息。例如，鼠标点击消息将包含额外信息，如用户交互的窗口句柄、鼠标光标的坐标以及鼠标按钮的状态。由于很难记忆消息 ID，因此它们在 `windows.h` 中被适宜地 `#defined` 了。消息 ID 和额外信息存储在一个名为 `MSG` 的结构体内。

**在 `WinMain()` 中**，通过调用 API 函数 `GetMessage()` 从消息队列中获取此 `MSG` 结构体。传递给函数的第一个参数是 `MSG` 结构体变量的地址。`GetMessage()` 会从消息队列中提取消息信息并放入传递给它的结构体变量中。现在不用担心其他参数。

从消息队列中获取消息后，我们需要处理它。这是通过调用 `DispatchMessage()` API 函数实现的。该函数执行了几项活动，具体如下：

- (a) 从传递给它的 `MSG` 结构体中，`DisplayMessage()` 提取出它所属的窗口句柄。
- (b) 根据句柄判断出创建该窗口的窗口类。
- (c) 从窗口类结构体中获取名为 `WndProc()` 的函数地址（window procedure 的缩写）。我之前没告诉过你，在 `InitInstance()` 填充 `WNDCLASS` 结构体时，其中一个元素被设置了名为 `WndProc()` 的用户定义函数的地址。
- (d) 使用此地址调用该函数。

由于消息被发送到消息队列中，`GetMessage()` 会使用此地址调用 `WndProc()`。当 `GetMessage()` 遇到特定的退出消息时，它会返回 0。`WinMain()` 结束。

## 消息的响应

当用户与窗口交互时（例如通过拉伸边界或点击标题栏中的按钮等），一个适当的消息会被发送到我们应用程序的消息队列中。我们的应用程序现在应该从消息队列中获取这些消息并处理它们。

消息包含一个消息 ID 和一些关于消息的其他额外信息。例如，鼠标点击消息将包含额外信息，如用户交互的窗口句柄、鼠标光标的坐标以及鼠标按钮的状态。由于很难记忆消息 ID，因此它们在 `windows.h` 中被适宜地 `#defined` 了。消息 ID 和额外信息存储在一个名为 `MSG` 的结构体内。

**在 `WinMain()` 中**，通过调用 API 函数 `GetMessage()` 从消息队列中获取此 `MSG` 结构体。传递给函数的第一个参数是 `MSG` 结构体变量的地址。`GetMessage()` 会从消息队列中提取消息信息并放入传递给它的结构体变量中。现在不用担心其他参数。

从消息队列中获取消息后，我们需要处理它。这是通过调用 `DispatchMessage()` API 函数实现的。该函数执行了几项活动，具体如下：

- (a) 从传递给它的 `MSG` 结构体中，`DisplayMessage()` 提取出它所属的窗口句柄。
- (b) 根据句柄判断出创建该窗口的窗口类。
- (c) 从窗口类结构体中获取名为 `WndProc()` 的函数地址（window procedure 的缩写）。我之前没告诉过你，在 `InitInstance()` 填充 `WNDCLASS` 结构体时，其中一个元素被设置了名为 `WndProc()` 的用户定义函数的地址。
- (d) 使用此地址调用该函数。

由于消息被发送到消息队列中，`GetMessage()` 会使用此地址调用 `WndProc()`。当 `GetMessage()` 遇到特定的退出消息时，它会返回 0。`WinMain()` 结束。

# 程序实例

Windows 允许你同时运行多个程序的副本。这在两个记事本副本之间进行剪贴，或者运行多个终端模拟器会话时非常有用。每个运行的程序副本都被称为“程序实例”。

Windows 执行了一项有趣的内存优化技巧。它在所有运行实例之间共享一份程序代码。例如，如果你运行了三个记事本实例，内存中只有一份 Notepad 代码。所有三个实例共享相同的代码，但会有独立的内存区域来存储文本数据。处理代码和数据的区别是逻辑层面的，因为每个记事本实例可能编辑不同的文件，因此数据对每个实例来说是唯一的。编辑文件的逻辑对于每个实例都是相同的，因此没有理由不共享一份 Notepad 代码。

# 576

# 让我们学习 C

- (h) 当用户点击窗口或在窗口上移动鼠标指针时，系统会生成消息并将其投递到应用程序消息队列中。
- (i) 消息包含消息 ID 以及关于消息的额外信息。
- (j) 当 `GetMessage()-DispatchMessage()` 循环遇到 `GetMessage()` 遇到 `WM_QUIT` 消息时终止。
- (k) 如果我们不处理应用程序接收到的消息，将调用 `DefWindowProc()` 函数进行默认处理。

## 练习

- [A] 判断对对错：
    - (a) `MessageBox()` 是一个 API 函数。
    - (b) 调用 `MessageBox()` 函数会在控制台窗口显示指定的字符串。
    - (c) `CreateWindow()` 函数会在屏幕上创建并显示窗口。
    - (d) `ShowWindow()` 函数只能显示最大化窗口。
    - (e) 每个窗口都必须使用预注册的窗口类来创建。
    - (f) 窗口类类似于 C++ 中的类。
    - (g) 我们可以使用预定义的窗口类，但不能创建自己的类。
    - (h) 样式 `WS_OVERLAPPED | WS_CAPTION | WS_MINIMIZEBOX` 将创建一个带有标题栏和最小化框的窗口。
    - (i) 为了能够与窗口交互，必须实现消息循环。

- [B] 回答以下问题：
    - (a) 概述典型的 Windows 程序在执行期间遵循的步骤。
    - (b) 运行任何基于 Windows 的程序，看看是否能识别应用程序窗口的所有元素。
    - (c) 你如何通过程序手段最小化窗口？
    - (d) 当用户尝试关闭窗口时，如果我们不在消息队列中放置 `WM_QUIT` 消息会发生什么？
    - (e) 解释 `RegisterClassEx()` 函数的用途。
    - (f) `GetMessage()` 和 `DispatchMessage()` 函数之间有什么区别？
    - (g) 写一个程序，接收一个整数作为命令行参数，创建一个按钮窗口，并根据整数的值将按钮窗口显示为最大化/正常状态。
    - (h) 尝试用不同的窗口样式组合显示窗口并观察结果。

# 第 17 章：Windows 编程 577

## 18 Windows 图形学

- 现在的图形
- 设备无关性绘制
- Hello Windows
- 绘制形状
- 画笔的类型
- 画刷的类型
- 代码与资源
- 自由绘画，画笔风格
- 捕捉鼠标
- 设备上下文（Device Context），深入观察
- 显示位图
- 工作中的动画
- `WM_CREATE` 和 `OnCreate()`
- `WM_TIMER` 和 `OnTimer()`
- 其他几点……
- Windows，无限的世界……
- 总结
- 练习

# 580

# 让我们学习 C

自，颜色和形状比任何事物都吸引着人类。否则，人们可能仍在使用 MS-DOS 或 Unix 的面向字符界面。事实上，Windows 的图形能力在其成功故事中发挥了至关重要的作用。一旦你掌握了如何在其中绘制窗口，它将为你开启你从未想过的巨大可能性。

## 现在的图形

世界已经超越了 Turbo C/C++ 编译器在 MS-DOS 环境下提供的 16 色和 640 x 480 分辨率图形。今天，我们生活在一个分辨率为 1024 x 768、提供 1670 万色的世界里。图形菜单、图标、彩色光标、位图、波形文件和动画已成为常态。以至于使用 Turbo C 构建的在低分辨率下运行的 16 色图形程序非常伤眼睛。此外，由于大量的 Windows API 支持图形活动，在 Windows 下的图形程序中可以实现很多功能。我确定这一章将帮助你理解并欣赏这些新能力。

# 设备无关性绘制

Windows 允许程序员编写程序，在屏幕上显示文本或图形，无需担心视频硬件的细节。在 VGA 显示器上运行的 Windows 程序可以在不修改的情况下在 Windows 支持的 SVGA 或 XGA 显示器上运行。
