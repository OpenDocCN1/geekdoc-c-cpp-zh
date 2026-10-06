# Thread Synchronization and Concurrent Operations

```
break;
}

ifstream infile(szFilePath);

if (infile.is_open()) {
    string line;
    while (std::getline(infile, line)) {
        QueueElement* pElement = new QueueElement();
        istringstream iss(line);
        if ((iss >> pElement->iA1 >> pElement->iB1 >> pElement->iC1 >> pElement->iA2 >> pElement->iB2 >> pElement->iC2)) {
            break;
        }
        pElement->hwnd = GetDlgItem(hwnd, CONTROL_PROGRESS);
        pElement->hwndResult = GetDlgItem(hwnd, CONTROL_RESULT);
    }
    queue.Enqueue(pElement);
}

infile.close();

SendMessage(GetDlgItem(hwnd, CONTROL_PROGRESS), PBM_STRANGE, 0, MAKELPARAM(0, queue.Count()));

SYSTEM_INFO sysInfo;
GetSystemInfo(&sysInfo);

for (DWORD dwIndex = 0; dwIndex < sysInfo.dwNumberOfProcessors; dwIndex++) {
    HANDLE hThread = CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)StartAddress, &queue, 0, NULL);
    SetThreadIdealProcessor(hThread, dwIndex);
    Sleep(100);
    CloseHandle(hThread);
}
```