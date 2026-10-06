# Chapter 5

unsigned GetNextSeed(void);

int WINAPI _tWinMain(HINSTANCE hThis, HINSTANCE hPrev, LPTSTR
szCommandLine, int iWndShow)
(

```
UNREFERENCED_PARAMETER(hPrev)
UNREFERENCED_PARAMETER(szCommandLine);

TCHAR* szWindowClass = _T("__priority_wnd_class_");

WNDCLASS wndEx = { 0 };

wndEx.cbSize = sizeof(WNDCLASS);

wndEx.style = CS_HREDRAW | CS_VREDRAW;
wndEx.lfnWndProc = WindowProcedure;
wndEx.cbClsExtra = 0;
wndEx.hInstance = hThis;
wndEx.hIcon = LoadIcon(hInstance, (IDR)MAKERESOURCE(NULL, IDI_APPLICATION));
wndEx.hCursor = LoadImage(hInstance, (IDCT)MAKERESOURCE(NULL, IDI_APPLICATION));
wndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
wndEx.hbrBackground = (HBRUSH)(COLOR_WINDOW + 1);
wndEx.lpszMenuName = NULL;
wndEx.lpszClassName = szWindowClass;
```

if (!RegisterClassEx(&wndEx))
{
  return 1;
}

HANDLE hEvent = CreateEvent(NULL, TRUE, FALSE, RESET_EVENT);

InitCommonControls();

HWND hndw = CreateWindow(szWindowClass,
T("Basic thread priority"), WS_OVERLAPPED | WS_CAPTION
| WS_SYSMENU | WS_MINIMIZEBOX, 50, 50, WINDOW_WIDTH,
WINDOW_HEIGHT, NULL, NULL, wndEx.hInstance, NULL);

if (!hndw)
{