```
if ((hWnd) = InitInstance(hInstance, nCmdShow))
{
    return FALSE;
}
pCommObject->bExitApplication = false;
pCommObject->hWnd = hWnd;
memset(pCommObject->iPhilosopherArray, 0, sizeof(*pCommObject->iPhilosopherArray));
pCommObject->iPhilosopherCount = PHILOSOPHER_COUNT;
HANDLE hSemaphore = CreateSemaphore(NULL, NULL, 2, szPhilosopherName);
STARTUPINFO startupInfo[PHILOSOPHER_COUNT] =
{0}, {0}, {0}, {0}, {0}};
PROCESS_INFORMATION processInformation[PHILOSOPHER_COUNT] =
{0}, {0}, {0}, {0}, {0}};
H hProcesses[PHILOSOPHER_COUNT]
TCHAR szBuffer[8];
for (int i = 0; i < PHILOSOPHER_COUNT; i++)
{
#if UNICODE
    sprintf(szBuffer, L"%d", i);
#else
    sprintf(szBuffer, "%d", i);
#endif
if (CreateProcess(TEXT(".*\\\\Debug\\\\Philosopher.exe"),
szBuffer, NULL, NULL,
FALSE, 0, NULL, NULL, &startupInfo[i],
&processInformation[i])
{
    hProcesses[i] = processInformation[i].hProcess;
}
MSG msg = { 0 };
while (GetMessage(&msg), NULL, 0, 0))
{
    TranslateMessage(&msg);
    DispatchMessage(&msg);
}
pCommObject->bExitApplication = true;
UnmapViewOfFile(pCommObject);
WaitForMultipleObjects(PHILOSOPHER_COUNT, hProcesses, TRUE, INFINITE);
for (int iIndex = 0; iIndex < PHILOSOPHER_COUNT; iIndex++)
```