
# Chapter 3

The Join method sets the STATE_READY flag and wait for the thread object to become signaled, until the dwWaitInterval expires. The dwWaitInterval parameter is set to INFINITE by default.

The Suspend and Resume methods suspend and resume the thread respectively. The STATE_BLOCKED flag is set in Suspend and in Resume. The thread class has the lpUserData attribute assigned for the future user-specific data to be set if necessary. The SetUserData and Get methods set and get the user data respectively. The GetAsyncState method returns the object asynchronous response.

The GetState and SetState methods get and set the dwState value or object state respectively. It is meant for additional object state change.

The Alert method changes the event's state to signaled. It is meant for a situation WHERE STATE_CONTINUOUS is used. If a thread is meant to run a continuous task, there has to be some mechanism to stop the thread in a normal manner. So when we have one or more threads running continuously, we only have to call Alert from one instance. It will alert all the threads to stop continuous work and return.

As the class member functions (methods) have a first implicit argument (not shown) this, we must declare the StartAddress method as static. However, we can pass the object address (the this pointer) to the StartAddress method and make it behave a non-static method using the pure virtual function, Run.

The GetId and GetHandle methods return a unique thread identifier and a thread handle respectively. The methods are implemented as inline routines.

# There's more...

We were following the object-oriented approach very precisely in the previous thread implementation due to code reuse and simplicity of programming. The following topic will demonstrate the use of CThread with very little difficulty.

# Implementing threads without synchronization

In a lot of situations, parallel tasks need to occur depending on each other. Such situations could have happened in an application with more user-interface dialogs. For example, on a primary application window, there is a list view with customers shown. On another application window (or application tab), there is a list view with products shown. When we start such an application, it would be foolish to load the customers first and then the products. We can start two threads, each responsible for loading the object from the database (the first thread would load the customers, and the other would load the products).

![](img/412b0f5bbb36adcce2ddd2d5b7416516_135_0.png)

# Managing Threads

Now, let's review a simple example. We have to initialize the main application window and then need to create four child windows. For each window, we will create a separate thread with no constraints on system resources—in our example, a brush for painting each window respectively. Later, in our next example, we will assume that only one brush is available to demonstrate the synchronization action.

# Getting ready

Make sure that Visual Studio is up and running.

# How to do it..

Now, let's create our program and explain its structure using the following steps:

- 1. Create a new C++ Windows application named Async.
- 2. Add a new source file named AsyncThreads. Open AsyncThreads.cpp.
- 3. Add the following code to it:

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
    // reseed random generator
    srand((unsigned)time(NULL));
}

HWND hWnd = (HWND)GetUserData();
```

# Chapter 3

```cpp
RECT rect;

// get window's dimensions
BOOL bError = GetClientRect(hWnd, &rect);
if (!bError)
{
    return;
}

int clientX = rect.right - rect.left;
int clientY = rect.bottom - rect.top;

// do not draw if the window does not have any dimensions
if ((clientX) || (!clientY))
{
    return;
}

// get device context for drawing
HDC hDC = GetDC(hWnd);

if (hDC)
{
    // draw the ten random figures
for (int iCount = 0; iCount < WINDOWS_NUMBER; iCount++)
    {
        // set coordinates
        int startX = (int)(rand() % clientX);
        int stopX = (int)(rand() % clientX);
        int startY = (int)(rand() % clientY);
        int stopY = (int)(rand() % clientY);
        // set the color
        int iRed = rand() & 255;
        int iGreen = rand() & 255;
        int iBlue = rand() & 255;

        // create a solid brush
        HANDLE hBrush = CreateSolidBrush(GetNearestColor(hDC,
RGB(iRed, iGreen, iBlue)));
        HANDLE hbrOld = SelectBrush(hDC, hBrush);

        Rectangle(hDC, min(startX, stopX), max(startX, stopX),
min(startY, stopY), max(startY, stopY));

    // delete the brush
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_137_0.png)

# Managing Threads

```cpp
DeleteBrush(SelectBrush(hDC, hbrOld));
}

// release the Device Context
ReleaseDC(hWnd, hDC);
}

Sleep(SLEEP_TIME);

return;
}

int WINAPI tWinMain(HINSTANCE hThis, INSTANCE hPrev, LPTSTR
szCommandLine, int iCmdShow)
{
    WNDCLASS wndEx = { 0 };

wndEx.clsExtra = 0;
wndEx.cbSize = sizeof(WNDCLASS);
wndEx.cbWndExtra = 0;
wndEx.hbrBackground = (HBRUSH) COLOR_BACKGROUND;
wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
wndEx.hIcon = LoadIcon(NULL, IDI_APPLICATION);
wndEx.hIconSm = LoadIcon(NULL, IDI_APPLICATION);
wndEx.hInstance = hThis;
wndEx.lfnWndProc = WindowProcedure;
wndEx.lpszClassName = _T("async_thread");
wndEx.lpszMenuName = NULL;
wndEx.style = CS_HREDRAW | CS_VREDRAW | CS_DBLCLKS;
```

```cpp
if (!RegisterClassEx(&wndEx))
{
    return 1;
}
```

```cpp
HWND hWnd = CreateWindow(wndEx.lpszClassName,
TEXT("Basic Thread Management"), WS_OVERLAPPEDWINDOW, 200,
200, 840, 440, HWND_DESKTOP, NULL, wndEx.hInstance, NULL);
```

```cpp
HWND hRects[THREADS_NUMBER];
```

```cpp
hRects[0] = CreateWindow(_T("STATIC"), _T(""), WS_BORDER |
WS_CHILD | WS_VISIBLE | WS_CLIPCHILDREN, 20, 20, 180,
350, NULL, hTitle, NULL);
hRects[1] = CreateWindow(_T("STATIC"), _T(""), WS_BORDER |
WS_CHILD | WS_VISIBLE | WS_CLIPCHILDREN, 20, 20, 180,
350, NULL, hTitle, NULL);
hRects[2] = CreateWindow(_T("STATIC"), _T(""), WS_BORDER |
WS_CHILD | WS_VISIBLE | WS_CLIPCHILDREN, 20, 20, 180,
350, NULL, hTitle, NULL);
hRects[3] = CreateWindow(_T("STATIC"), _T(""), WS_BORDER |
WS_CHILD | WS_VISIBLE | WS_CLIPCHILDREN, 20, 20, 180,
350, NULL, hTitle, NULL);

UpdateWindow(hwnd);
ShowWindow(hwnd, SW_SHOW);

MSG msg = { 0 };
while (GetMessage(&msg, NULL, 0, 0)) {
    TranslateMessage(&msg);
    DispatchMessage(&msg);
}

UnregisterClass(wndEx.lpszClassName, wndEx.hInstance);
return 0;
}

RESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam) {
    switch (uMsg) {
        case WM_DESTROY:
        {
            PostQuitMessage(0);
            break;
        }
        case WM_CLOSE:
        {
            Thread* pThread = (Thread*)GetWindowLongPtr(hWnd, GWLP_USERDATA);
            pThread->Alert(0);
            for (int iIndex = 0; iIndex < THREADS_NUMBER; iIndex++)
            {
                hRects[iIndex]->Join();
            }
            DestroyWindow(hWnd);
            break;
        }
        default:
        {
            return DefWindowProc(hWnd, uMsg, wParam, lParam);
        }
    }
    return 0;
}
```
