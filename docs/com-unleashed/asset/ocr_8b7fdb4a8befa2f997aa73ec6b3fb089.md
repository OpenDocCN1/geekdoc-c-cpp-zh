# LISTING 7.10  Continued

```
```cpp
long l = object->Get(L"Thread").lVal;
::EnterCriticalSection(&cs);
std::cout << "Thread ID " << l << "\t";
::LeaveCriticalSection(&cs);
return 0;
}

int main(int argc, char* argv[])
{
  ::CoInitializeEx(NULL, COINIT_MULTITHREADED);
  {
    std::vector<Automation> v;
    int i=0;
    for (i=0;i<10;i++)
    {
      Automation object;
      object.CreateObject(L"Singlethreaded.STObject");
      v.push_back(object);
    }
    for (i=0;i<10;i++)
    {
      Automation object;
      object.CreateObject(L"Apartmentthreaded.ATObject");
      v.push_back(object);
    }
    for (i=0;i<10;i++)
    {
      Automation object;
      object.CreateObject(L"Freethreaded.FTObject");
      v.push_back(object);
    }

    ::InitializeCriticalSection(&cs);
    std::vector<Automation>::iterator j = v.begin();
    for (j!=v.end();j++)
    {
      DWORD dw;
      HANDLE thread = ::CreateThread(NULL, 0, ThreadProc,
                                     (void *)(&Automation *j), 0, &dw);
      ::CloseHandle(thread);
    }

    j = v.begin();
    for (j!=v.end();j++)
    {
      DWORD dw;
      HANDLE thread = ::CreateThread(NULL, 0, ThreadProc,
                                     (void *)(&Automation *j), 0, &dw);
      ::CloseHandle(thread);
    }
  }
```
```