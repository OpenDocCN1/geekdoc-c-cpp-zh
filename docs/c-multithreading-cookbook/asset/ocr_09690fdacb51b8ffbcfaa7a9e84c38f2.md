# Introduction to C++ Concepts and Features

The CreateWindow API creates an overlapped, pop-up, or child window. It specifies the window class, window title, window style, and (optionally) the initial position and size of the window. The function also specifies the window's parent or owner, if any, the window's menu, as shown in the following code:

```
HWND hWnd = CreateWindow(wndEx.pszClassName, TEXT("GUI Project"),
WS_OVERLAPPEDWINDOW, 200, 200, 400, 300, HWND_DESKTOP,NULL, hThis, 0);
```

```
if (!hWnd)
{
    return -1;
}
```

The UpdateWindow function updates the client area of the specified window by sending a WM_PAINT message if the window's update region is not empty. The function sends a WM_PAINT message directly to the window procedure of the specified window bypassing the message queue. The usage is shown in the following code:

```
UpdateWindow(hWnd);
```

The following code sets the specified window's state:

```
ShowWindow(hWnd, iCmdShow);
```

Now, we need the instance of the MSG structure that represents the window message.

```
MSG msg = { 0 };
```

Here, we need the message loop. Windows-based applications are event driven. They do not make explicit function calls (such as C runtime library) to obtain input. Instead, they wait for the system to pass input to them. The system passes all input for an application to the various windows in the application. Each window has a function, called a window procedure, which the system calls whenever it has input for the window. The GetMessage API retrieves a message from the calling thread's message queue, as shown in the following code:

```
while ( GetMessage(&msg, NULL, NULL, NULL ) )
{
    // Translates virtual-key messages into character messages.
    TranslateMessage(&msg);
    // Dispatches a message to a window procedure.
    DispatchMessage(&msg);
}
```

32