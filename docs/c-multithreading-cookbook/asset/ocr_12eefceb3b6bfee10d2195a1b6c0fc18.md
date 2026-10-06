# Message Passing

```
}
default:
{
    return DefWindowProc(hWnd, uMsg, wParam, lParam);
}
return 0;
}
```

```
DWORD WINAPI StartAddress(LPOVOID lpParameter)
{
    MSG msg;
    PeekMessage(&msg, NULL, WM_USER, WM_USER, PM_NOREMOVE);

    HANDLE hEvent = OpenEvent(EVENT_ALL_ACCESS, FALSE, EVENT_NAME);

    if (hEvent != NULL)
    {
        SetEvent(hEvent);
    }
    CloseHandle(hEvent);

while (GetMessage(&msg, NULL, 0, 0))
{
    switch (msg.message)
    case T_MESSAGE:
        {
            // TO DO
            // add some message processing here
            MessageBox(NULL, T("Hi.\nI've just received a message."), T("OK"));
            break;
        }
    case T_ENDTASK:
        {
            // main thread is exiting
            // return immediately
            return 0;
        }
    }
}
return 0;
```