# Thread Synchronization and Concurrent Operations

```
Sleep(100);
CloseHandle(hThread);
}
else {
    MessageBox(hWnd, _T("Cannot open file!"),
    _T("Error!"), MB_OK | MB_TOPMOST | MB_ICONERROR);
}
}
break;
}
default: {
    return DefWindowProc(hWnd, uMsg, wParam, lParam);
}
return 0;
```

DWORDAPI StartAddress (LPVOID lParameter)
{
    // We'll solve the linear system using Cramer's rule:
    CQueue<QueueElement>* pQueue = (CQueue<QueueElement>*)
lpParameter;

```
HANDLE hMutex = OpenMutex(MUTEX_ALL_ACCESS, FALSE, szMutex);
HANDLE h = OpenSemaphore(SEMAPHORE_ALL_ACCESS, FALSE,
szSemaphore);
QueueElement* pElement = NULL;
```

```
while (true) {
    WaitForSingleObject(hSemaphore, INFINITE);
    ReleaseSemaphore(hSemaphore, 1, NULL);

    WaitForSingleObject(hMutex, INFINITE);
    pElement = pQueue->Dequeue();
    ReleaseMutex(hMutex);
    if (pElement == NULL) {
        break;
}
```