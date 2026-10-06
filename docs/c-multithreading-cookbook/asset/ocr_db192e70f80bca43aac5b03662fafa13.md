# Chapter 5

WS_CHILD | WS_VISIBLE | SS_CENTERIMAGE | SS_LEFT | WS_BORDER,
20, 20, 250, 25, hWnd, (HMENU) CONTROL_TEXT, wndEx.hInstance,
NULL;

SendMessage(hLabel, WM_SETFONT, (WPARAM) hFont, TRUE);

```
HWND hBrowse = CreateWindow(_T("BUTTON"), _T("Browse"), WS_CHILD |
WS_PUSHBUTTON, 190, 65, 80, 25, hWnd, (HMENU) CONTROL_BROWSE,
wndEx.hInstance, NULL);
SendMessage(hBrowse, WM_SETFONT, (WPARAM) hFont, TRUE);
```

```
HWND hStart = CreateWindow(_T("BUTTON"), _T("Start"), WS_CHILD |
WS_VISIBLE |
WS_PUSHBUTTON, 190, 115, 80, 25, hWnd, (HMENU) CONTROL_START,
wndEx.hInstance, NULL);
SendMessage(hStart, WM_SETFONT, (WPARAM) hFont, TRUE);
```

```
HWND hProgress = CreateWindow(_T("PROGRESS_CLASS"
```

```
ShowWindow(hWnd, nCmdShowShow);
```

```
HANDLE hMutex = CreateMutex(NULL, FALSE, szMutex);
SYSTEM_INFO sysInfo;
GetSystemInfo(&sysInfo);
LONG l1ProcessorCount = (LONG) sysInfo.dwNumberOfOfProcessors;
HAND hSemaphore = CreateSemaphore(NULL, 1ProcessorCount,
1ProcessorCount, szSemaphore);
```

```
MSG msg;
while(GetMessage(&msg, 0, 0, 0))
{
  TranslateMessage(&msg);
```

![](bbox=[0.745, 0.831, 0.805, 0.853])