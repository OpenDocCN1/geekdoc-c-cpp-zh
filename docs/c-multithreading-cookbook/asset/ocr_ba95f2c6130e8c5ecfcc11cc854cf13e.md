# Thread Synchronization and Concurrent Operations

```
UNREFERENCED_PARAMETER (szCommandLine);

TCHAR* szWindowClass = _T("concurrent_operations__");
```

```
WNDCLASSSEX wdex = { 0 };
wndex.cbSize = sizeof(WNDCLASS)
wndex.style = CS_HREDRAW | CS_VREDRAW
wndex.lpfnWndProc = WindowProcedure;
wndex.cbClsExtra = 0;
wndex.cbWndExtra = 0;
wndex.hInstance = hThis;
wndex.hicon = LoadIcon(wdex.hinstance, MAKERESOURCE(IDI_, APPLICATION));
wndex.hCursor = LoadCursor(NULL, IDC_ARROW);
wndex.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
wndex.lppszClassName = szWindowClass;
wndex.hIconSm = LoadIcon(wdex.hinstance, MAKERESOURCE(IDI_, APPLICATION));

```

```
if (!RegisterClassEx(&wdex))
{
    return R;
}
```

```
InitCommonControls();

hWND hWnd = CreateWindow(szWindowClass,
    T("Concurrent operations"), WS_OVERLAPPED
    WS_CAPTION | WS_MENU, 50, 50, 305, 250, NULL, NULL,
wndex.hinstance, NULL);
```

```
if (hWnd)
{
    return NULL;
}
```

```
HFONT hFont = CreateFont(14, 0, 0, 0, FW_NORMAL, FALSE,
FALSE, FALSE, BALTIC_CHARSET, OUT_DEFAULT_PRECIS,
CLIP_DEFAULT_PRECIS, DEFAULT_QUALITY, DEFAULT_PITCH
FF_MODERN, _T("Microsoft Sans Serif"));
```

```
HWND hLabel = CreateWindow(_T("STATIC",
    _T(" Press \Browse\" and choose file with coordinates: ");
```