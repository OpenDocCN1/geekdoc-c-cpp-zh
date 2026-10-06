

# 第 4 章

```cpp
#include <tchar.h>

#include <cmctrl.h>
```

```cpp
#pragma comment ( lib, "/comctl32.lib" )
#pragma comment ( linker, "/manifestdependency:type='win32'\nname='Microsoft.Windows.Controls'\/
version='6.0.0.0' processorArchitecture='*'\/
publicKeyToken='659b64144ccf1df' language='*'" )
```

```cpp
#define BUTTON_MSG 100
#define BUTTON_CLOSE 101
#define LABEL_TEXT 102
```

```cpp
LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM
wParam, LPARAM lParam);

int WINAPI _tWinMain(HINSTANCE hThis, INSTANCE hPrev, LPTSTR
szCommandLine, int nCmdShow)
{

UNREFERENCED_PARAMETER(hPrev);
UNREFERENCED_PARAMETER(szCommandLine);

TCHAR* szWindowClass = _T("__basic_MPI_Wnd_class__");

WNDCLASSSEX wndEx = { 0 };
wndEx.style = sizeof(WNDCLASSSEX) | CS_HREDRAW;
wndEx.lpfnWndProc = WindowProcedure;
wndEx.cbSize = 0;
wndEx.cbClExtra = 0;
wndEx.hInstance = hThis;
wndEx.hIcon = LoadIcon(wndEx.hInstance,
MAKEINTRESOURCE(IDI_APPLICATION));
wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
wndEx.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
wndEx.lpszMenuName = NULL;
wndEx.lpszClassName = szWindowClass;
wndEx.hIconSm = LoadIcon(wndEx.hInstance,
MAKEINTRESOURCE(IDI_APPLICATION));
```

```cpp
if (!RegisterClassEx(&wndEx))
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_157_0.png)

# 消息传递

```cpp
{
    return 1;
}
```

```cpp
InitCommonControls();
```

```cpp
HWND hWnd = CreateWindow(szWindowClass, _T("Basic Message
Passing Interface"), WS_OVERLAPPED | WS_CAPTION | WS_SYMENU
WS_MINIMIZEBOX, 200, 200, 440, 340, NULL, NULL, wndEx.hInstance,
NULL);
```

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

![](img/412b0f5bbb36adcce2ddd2d5b7416516_159_0.png)

  case WM_DESTROY:
  {
    PostQuitMessage(0);
    break;
  }
  default:
  {
    return DefWindowProc(hWnd, uMsg, wParam, lParam);


# 它是如何工作的...

此示例的目的是演示基础的消息传递。你需要注意我们之前定义的 BUTTON_CLOSE 和 LABEL 宏。我们稍后需要它们作为子控件标识符。对于子窗口，hMenu 指定了子窗口标识符。

> 子控件标识符是窗口用于通知父窗口事件的整数值。应用程序确定子窗口标识符，对于同一个父窗口的所有子窗口，它必须是唯一的（参考 MSDN）。

现在让我们检查 WinMain 入口。我们创建了 WNDCLASS 实例并对其初始化。在成功注册窗口类并随后调用 RegisterClass 后，我们创建了主窗口，然后调用 CreateWindow。

然后，我们需要创建一个文本标签和按钮控件。按钮和标签也是具有预定义系统类的窗口（如 BUTTON、STATIC 等）。有关完整的系统类参考，请参 http://msdn.microsoft.com/en-us/library/windows/ ...

