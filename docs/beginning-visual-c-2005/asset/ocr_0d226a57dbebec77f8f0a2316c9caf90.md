# Chapter 11

The hWnd argument identifies your program window, and the second argument is the address of the PAINTSTRUCT structure that was filled in by the BeginPaint () function.



You might assume that closing the window closes the application, but to get this behavior you actually have to add some more code. The reason that the application won’t close by default when the window is closed is that you may need to do some clearing up. It is also possible that the application may have more than one window. When the user closes the window by double-clicking the title bar icon or clicking the Close button, this causes a WM_DESTROY message to be generated. Therefore, to close the application, you need to process the WM_DESTROY message in the WindowProc() function. You do this by generating a WM_QUIT message with the following statement:

```
PostQuitMessage(0);
```

The argument here is an exit code. This Windows API function does exactly what its name suggests — it posts a WM_QUIT message in the message queue for your application. This results in the GetMessage () function in WinMain() returning FALSE and ending the message loop, so ending the program.



```
// Listing OFWIN_2
LRESULT WINAPI WindowProc(HWND hWnd, UINT message,
    WPARAM wParam, LPARAM lParam)
{
    HDC hDC;                  // Display context handle
    PAINTSTRUCT PaintSt;      // Structure defining area to be drawn
    RECT aRect;               // A working rectangle
    switch(message)           // Process selected messages
    {
    case WM_PAINT:            // Message is to redraw the window
        hDC = BeginPaint(hWnd, &PaintSt);// Prepare to draw the window
        // Get upper left and lower right of client area
        GetClientRect(hWnd, &aRect);
        SetBkMode(hDC, TRANSPARENT);  // Set text background mode
        // Now draw the text in the window client area
        DrawText(
            hDC,                     // Device context handle
            L"But, soft! What light through yonder window breaks?",
            -1,                      // Indicate null terminated string
            &aRect,                  // Rectangle in which text is to be drawn
            DT_SINGLELINE|           // Text format - single line
            DT_CENTER|               // - centered in the line
            DT_VCENTER);             // - line centered in aRect
        EndPaint(hWnd, &PaintSt); // Terminate window redraw operation
    }
    return DefWindowProc(hWnd, message, wParam, lParam);
}
```