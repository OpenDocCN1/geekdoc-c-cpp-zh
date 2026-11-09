# LISTING 9.4  Continued

```
```cpp
HRESULT GetInterface(IUnknown * pUnknown, REFIID riid,
                    IUnknown ** ppUnknown)
{
    HRESULT hRes = pUnknown->QueryInterface(riid, (void **)ppUnknown);
    if (FAILED(hRes))
    {
        // QueryInterface failed
        std::cout << "QueryInterface failed = " << ltoa(hRes, s, 16)
                  << std::endl;
        ATLASSERT(FALSE);
        return hRes;
    }

    return S_OK;
};
int main()
{
    CoInitialize(NULL);
    std::cout << "Start" << std::endl;

    IUnknown * pUnknown;
    HRESULT hRes = GetUnknown(L"process.MyInterface.1", &pUnknown);
    if (FAILED(hRes))
    {
        CoUninitialize();
        // GetUnknown failed
        return hRes;
    }

    IMyInterface * pi
    hRes = GetInterface(pUnknown, IID_IMyInterface, (IUnknown **)&p);
    if (FAILED(hRes))
    {
        pUnknown->Release();
        CoUninitialize();

        // GetUnknown failed
        return hRes;
    }

    long l=0;
    p->get_processid(&l);
    std::cout << "Object Process = " << l << std::endl;
    p->get_threadid(&l);
    std::cout << "Object Thread = " << l << std::endl;

    std::cout << "Process = " << ::GetCurrentProcessId() << std::endl;
    std::cout << "Thread = " << ::GetCurrentThreadId() << std::endl;
```
```