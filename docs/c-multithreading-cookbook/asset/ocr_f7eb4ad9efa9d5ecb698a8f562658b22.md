# Thread Synchronization and Concurrent Operations

| BS_PUSHBUTTON, 190, 65, 80, 25, hWnd, (HMENU) CONTROL_BROWSE,
wndEx.hInstance, NULL);
SendMessage(hbrowse, WM_SETFONT, (WPARAM) hFont, TRUE);
HWND hStart = CreateWindow(_T("BUTTON"), _T("Start"), WS_CHILD |
WS_VISIBLE
| BS_PUSHBUTTON, 190, 115, 80, 25, hwnd, (HMENU) CONTROL_START,
wndEx.hInstance, NULL);
SendMessage(hStart, WM_SETFONT, (WPARAM) hFont, TRUE);
hWND hProgress = CreateWindow(PROGRESS_CLASS, _T(""), WS_CHILD
| WS_VISIBLE | WS_BORDER, 20, 165, 250, 25, hWnd,
(HMENU) CONTROL_PROGRESS, wndEx.hInstance, NULL);
SendMessage(hProgress, PMS_SETSTEP, (WPARAM) 1, 0);
SendMessage(hProgress, PMS_SEPOS, (WPARAM) 0, 0);

```
void* params[2] = { hProgress, hResult };
HANDLE hThread = CreateThread(NULL, 0, (LPTHREAD_ROUTINE)
ListenerThread, 0, NULL);
Sleep(100);
CloseHandle(hThread);

ShowWindow(hwnd, nCmdShow);
HANDLE hEvent = CreateEvent(NULL, TRUE, FALSE, EVENT_NAME);
HAND hMutex = CreateMutex(NULL, FALSE, MUTEX_NAME);
HAND hMapping = CreateFileMapping((HANDLE )-1, NULL,
PAGE_READWRITE, 0, sizeof(QueueElement), MAPPING_NAME);
```

MSG msg;
while (GetMessage(&msg), 0, 0, 0)
{
TranslateMessage(&msg);
DispatchMessage(&msg);
}

CloseHandle(hMapping);
CloseHandle(hMutex);
CloseHandle(hEvent);
UnregisterClass(wndEx.pszClassName, wndEx.hInstance);
return (int)msg.wParam;

LRESULT CALLBACK WindowProcedure(HWND hWnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
wParam, LPARAM lParam)