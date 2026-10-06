```
{
    return lpUserData;
}
```

```
DWORD CThread::GetAsyncState() const
{
    if (dwState & STATE_ASYNC) {
        return STATE_ASYNC;
    }
    return STATE_SYNC;
}
```

```
DWORD CThread::GetState() const
{
    return dwState;
}
```

```
void CThread::SetState(DWORD dwNewState)
{
    dwState = 0;
    dwState |= dwNewState;
}
```

```
BOOL CThread::Alert()
{
    return SetEvent(hEvent);
}
```

```
DWORD WINAPI CThread::*StartAddress (LPVOID lpParameter)
{
    CThread* cthread = (CThread*)lpParameter;
    if (cthread->GetAsyncState() == STATE_SYNC) {
        if (cthread->dwState & STATE_CONTINUOUS) {
            DWORD dwWaitStatus = 0;
            while (TRUE)
```