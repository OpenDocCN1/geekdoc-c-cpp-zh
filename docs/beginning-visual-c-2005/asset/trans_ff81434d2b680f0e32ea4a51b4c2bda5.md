

GetMessage() 函数的概念性操作如 图 11-3 所示。

![](img/2359b0c604600c58fba3539c738a356e_671_0.png)

图 11-3

在 while 循环中，对 TranslateMessage() 的第一次函数调用请求 Windows 为键盘相关消息执行一些转换工作。然后对 DispatchMessage() 函数的调用会导致 Windows 分发消息，或者换句话说，调用你程序中的 WindowProc() 函数来处理消息。DispatchMessage() 的返回不会在 WindowProc() 完成消息处理之前发生。WM_QUIT 消息表示程序应结束，因此这会导致返回 FALSE 给应用程序以停止消息循环。

## 一个完整的 WinMain() 函数

你已经查看了需要放入 WinMain() 函数的所有部分。现在你可以将它们组装成一个完整的函数：

```c
// Listing OFWIN_1
int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance,
                LPSTR lpCmdLine, int nCmdShow)
{
    WNDCLASSEX WindowClass;      // Structure to hold our window's attributes

    static LPCTSTR szAppName = L"OFWin";        // Define window class name
    HWND hWnd;                                   // Window handle
    MSG msg;                                     // Windows message structure

    WindowClass.cbSize = sizeof(WNDCLASSEX); // Set structure size

    // Redraw the window if the size changes
    WindowClass.style  = CS_HREDRAW | CS_VREDRAW;

    // Define the message handling function
    WindowClass.lpfnWndProc = WindowProc;

    WindowClass.cbClsExtra = 0;      // No extra bytes after the window class
    WindowClass.cbWndExtra = 0;      // structure or the window instance

    WindowClass.hInstance = hInstance;        // Application instance handle

    // Set default application icon
    WindowClass.hIcon = LoadIcon(0, IDI_APPLICATION);

    // Set window cursor to be the standard arrow
    WindowClass.hCursor = LoadCursor(0, IDC_ARROW);

    // Set gray brush for background color
    WindowClass.hbrBackground =
                    static_cast<HBRUSH>(GetStockObject(GRAY_BRUSH));

    WindowClass.lpszMenuName = 0;           // No menu
    WindowClass.lpszClassName = szAppName;  // Set class name
    WindowClass.hIconSm = 0;                // Default small icon

    // Now register our window class
    RegisterClassEx(&WindowClass);

    // Now we can create the window
    hWnd = CreateWindow(
        szAppName,                      // the window class name
        L"A Basic Window the Hard Way", // The window title
        WS_OVERLAPPEDWINDOW,            // Window style as overlapped
        CW_USEDEFAULT,                  // Default screen position of upper left
        CW_USEDEFAULT,                  // corner of our window as x,y...
        CW_USEDEFAULT,                  // Default window size
        CW_USEDEFAULT,                  // ...
        0,                              // No parent window
        0,                              // No menu
```

## WindowProc() 函数

我们 WindowProc() 函数的原型是：

```c
LRESULT CALLBACK WindowProc(HWND hWnd, UINT message,
                    WPARAM wParam, LPARAM lParam);
```

返回类型是 LRESULT，它是 Windows 定义的类型，通常等同于 long 类型。因为该函数是通过指针由 Windows 调用（你在 WinMain() 中在 WNDCLASSEX 结构中设置了该指针），你需要将函数限定为 CALLBACK。这是由 Windows 定义的另一个说明符，它决定函数参数的处理方式。传递的四个参数提供了有关导致函数被调用的特定消息的信息。以下表格描述了每个参数的含义：

| 参数 | 含义 |
|---|---|
| HWND hWnd | 发生导致消息的事件的窗口的句柄。 |
| UINT message | 消息 ID，是一个 32 位值，表示消息的类型。 |
| WPARAM wParam | 一个 32 位值，包含取决于消息类型的附加信息。 |
| LPARAM lParam | 一个 32 位值，包含取决于消息类型的附加信息。 |

与传入消息相关的窗口由传递给函数的第一个参数 hWnd 标识。在这种情况下，你只有一个窗口，因此可以忽略它。

消息由传递给 WindowProc() 的 message 值标识。你可以将此值与预定义的符号常量进行比较，每个常量都与特定消息相关。它们都以 WM_ 开头，典型示例是 WM_PAINT，对应于重绘窗口客户区的要求，以及 WM_LBUTTONDOWN，表示按下鼠标左键。你可以通过在 MSDN 库中搜索 WM_ 来找到全部集合。

## 解码 Windows 消息

解码 Windows 发送的消息的过程通常在 WindowProc() 函数中使用基于 message 值的 switch 语句来完成。选择要处理的消息类型只需在 switch 中为每种情况放置一个 case 语句即可。如下所示的 switch 语句的典型结构，其中包含任意 case：

```c
switch(message)
{
    case WM_PAINT:
        // Code to deal with drawing the client area
        break;

    case WM_LBUTTONDOWN:
        // Code to deal with the left mouse button being pressed
        break;

    case WM_LBUTTONUP:
        // Code to deal with the left mouse button being released
        break;

    case WM_DESTROY:
        // Code to deal with a window being destroyed
        break;

    default:
        // Code to handle any other messages
}
```

每个 *Windows* 程序在某处都有类似的东西，尽管它可能在你以后使用 MFC 编写的 Windows 程序中被隐藏起来。每个 case 对应于消息 ID 的特定值，并为该消息提供合适的处理。程序不希望单独处理的任何消息都由 default 语句处理，该语句应通过调用 `DefWindowProc()` 将消息交还给 Windows。这是提供默认消息处理的 Windows API 函数。

在专门处理各种可能的 Windows 消息的复杂程序中，这个 `switch` 语句可能会变得很大且相当笨重。当你使用应用程序向导生成 Windows 应用程序时，你不必担心这个问题，因为它都已为你处理好，你永远看不到 `WindowProc()` 函数。你所需要做的就是提供处理你感兴趣的特定消息的代码。

## 绘制窗口客户区

Windows 向程序发送 `WM_PAINT` 消息以发出应用程序的客户区应重绘的信号。因此在你的示例中，你需要在响应 `WM_PAINT` 消息时在窗口中绘制文本。

你不能随意在窗口中绘制。在写入应用程序窗口之前，你需要告诉 Windows 你想要这样做，并获得 Windows 的授权。你通过调用 Windows API 函数 `BeginPaint()` 来实现，这应该只在响应 `WM_PAINT` 消息时调用。用法如下：

```c
HDC hDC;                              // A display context handle
PAINTSTRUCT PaintSt;                  // Structure defining area to be redrawn

hDC = BeginPaint(hWnd, &PaintSt);     // Prepare to draw in the window
```

类型 HDC 定义了所谓的 **显示上下文**，或更一般地称为 **设备上下文**。设备上下文提供了在屏幕或打印机上输出信息的设备无关 Windows API 函数与支持向你的 PC 附加的特定设备写入的设备驱动程序之间的链接。你也可以将设备上下文视为一种授权令牌，它在你请求时由 Windows 授予你，并允许你输出一些信息。如果没有设备上下文，你根本无法生成任何输出。

`BeginPaint()` 函数以显示上下文作为返回值提供，并需要提供两个参数。窗口句柄标识你想要写入的窗口，

