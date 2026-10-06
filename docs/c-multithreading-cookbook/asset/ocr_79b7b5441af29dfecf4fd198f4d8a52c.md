```
wndEx.hbrBackground = (HBRUSH) (COLOR_WINDOW + 1);
wndEx.lpszMenuName = NULL;
wndEx.lpszClassName = szWindowClass;
wndEx.hIconSm = LoadIcon(wndEx.hInstance,
MAKEINTRESOURCE(IDI_APPLICATION));
```

```
if (!RegisterClass(&wndEx))
{
    return 1;
}
```

```
InitCommonControls();
```

```
HWND hwnd = CreateWindow(szWindowClass,
T("Concurrent operations"), WS_OVERLAPPED
| WS_CAPTION | WS_SYSMENU, 50, 50, 305, 250, NULL, NULL,
wndEx.hInstance, NULL);
```

```
if (!hwnd)
{
    return NULL;
}
```

```
HFONT hFont = CreateFont(14, 0, 0, 0, FW_NORMAL, FALSE,
FALSE, FALSE, BALTIC_CHARSET, DEFAULT_QUALITY, DEFAULT_PITCH
CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY, DEFAULT_PITCH
| FF_MODERN, T("Microsoft Sans Serif");
```

```
HWND hlabel = CreateWindow(T("STATIC"),
T("Press \Browse\
```

```
SendMessage(hlabel, WM_SETTEXT, (WPARAM) hFont, TRUE);
```

```
HWND hResult = CreateWindow(T("STATIC"), T("""""""),
WS_CHILD |
WS_VISIBLE | SS_LEFT | WS_BORDER, 20, 65, 150, 75, hwnd,
(HMENU) CONTROL_RESULT, wndEx.hInstance, NULL);
```

```
SendMessage(hResult, WM_SETTEXT, (WPARAM) hFont, TRUE);
```

```
HWND hBrowse = CreateWindow(T("BUTTON"), T("Browse"), WS_CHILD
| WS_VISIBLE
```

![](bbox=[0.763, 0.833, 0.806, 0.856])