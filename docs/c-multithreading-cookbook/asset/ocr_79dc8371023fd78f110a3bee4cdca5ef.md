# The Concepts of Process and Thread

```
{
  pCommObject = (PCOMMICATIONOBJECT) MapViewFile(hMapping,
FILE_MAP_WRITE, 0, 0, 0);
  if (pCommObject) {
    pCommObject->bExitLoop = TRUE;
    UnmapViewFile(pCommObject);
  }
  PostQuitMessage(0);
  break;
  default:
    return DefWindowProc(hWnd, uMsg, wParam, lParam);
  }
return 0;
}
```

```
HWND InitializeWnd()
{
  WNDCLASSSEX wndEx;
  WndEx.cbSize = sizeof(WNDCLASS);
  WndEx.style = CS_HREDRAW | CS_VREDRAW;
  WndEx.lpfnWndProc = WndProc;
  WndEx.cbClsExtra = 0;
  WndEx.cbInstance = GetModuleHandle(NULL);
  WndEx.hBackground = (HBRUSH) (COLOR_WINDOW + 1);
  WndEx.lppszName = NULL;
  WndEx.lpszClassName = WINDOW_CLASS_NAME;
  WndEx.hCursor = LoadCursor(NULL, IDC_ARROW);
  WndEx.hIcon = LoadIcon(WndEx.hInstance, IDI_APPLICATION);
  MAKEINRESOURCE(wndEx.hInstance,wndEx.hIcon);
  MAKEINRESOURCE(IDI_APPLICATION));
  if (!RegisterClassEx(&wndEx)) {
    return NULL;
  }
  HWND hWnd = CreateWindow(wndEx.lpszClassName,
TEXT("Interprocess communication Demo"),
```