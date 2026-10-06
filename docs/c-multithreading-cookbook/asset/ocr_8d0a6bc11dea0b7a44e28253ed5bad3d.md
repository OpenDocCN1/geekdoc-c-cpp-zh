Managing Threads

+   5. Add a new source file main.cpp. Add the following code to it:

```
#include "CThread.h"

class Thread : public CThread
{
protected:
    virtual void Run(LPVOID lParameter = 0);
};

LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM
wParam, LPARAM lParam);

void Thread::Run(LPVOID lParameter)
{
    WNDCLASSSEXWndEx = { 0 };

    WndEx.cbClExtra = 0;
    WndEx.cbSize = sizeof(WNDCLASSEX);
    WndEx.cbWndEx = 0;
    WndEx.hBackground = (HBRUSH) COLOR_BACKGROUND;
    WndEx.h = LoadCursor(NULL, IDC_ARROW);
    WndEx.hIcon = LoadIcon(NULL, IDC_APPLICATION);
    WndEx.hIconSm = LoadIcon(NULL, IDC_APPLICATION);
    WndEx.hInstance = GetModuleHandle(NULL);
    WndEx.lfnWndProc = WindowProcedure;
    WndEx.lpszClassName = (LPCTSTR) this->lParameter;
    WndEx.lpszMenuName = NULL;
    WndEx.style = CS_HREDRAW | CS_VREDRAW | CS_DBLCLKS;

    if (!RegisterClassEx(&WndEx))
    {
        return;
    }

    HWND hWnd = CreateWindow(WndEx.lpszClassName,
        TEXT("Basic Thread Management"), WS_OVERLAPPEDWINDOW,
        200, 200, 800, HWND_DESKTOP, NULL, WndEx.hInstance, NULL);

    UpdateWindow(hWnd);
    ShowWindow(hWnd, SW_SHOW);

    MSG msg = { 0 };
    while (GetMessage(&msg, 0, 0, 0))
```