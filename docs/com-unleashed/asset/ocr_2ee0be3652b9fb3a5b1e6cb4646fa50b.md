# LISTING 11.12 Continued

```
```cpp
    return S_OK;
}

void EventTrigger(void * marshaldata)
{
    SECURITY_ATTRIBUTES sa;
    SECURITY_DESCRIPTOR sd;
    sa.nLength = sizeof(SECURITY_ATTRIBUTES);
    sa.bInheritHandle = TRUE;
    sa.lpSecurityDescriptor = &sd;
    if(!InitializeSecurityDescriptor(&sd,
        SECURITY_DESCRIPTOR_REVISION))
    {
        ExitThread(1);
    }
    if(!SetSecurityDescriptorDacl(&sd, TRUE, (PACL)NULL, FALSE))
    {
        ExitThread(1);
    }
    OBJECTMARSHALDATA * p = (OBJECTMARSHALDATA*) marshaldata;
    HANDLE hevent = ::CreateEvent(&sa, FALSE, FALSE,
        p->szEventname);
    char sz[256];
    strcpy(sz, p->szEventname);
    strcat(sz, "_ACK");
    HANDLE hack = ::CreateEvent(&sa, FALSE, FALSE, sz);
    strcpy(sz, p->szEventname);
    strcat(sz, "_STOP");
    HANDLE hstop = ::CreateEvent(&sa, FALSE, FALSE, sz);

    HANDLE harray[2] = {hevent, hstop};
    while (1)
    {
        DWORD dw = ::WaitForMultipleObjects(2, harray, FALSE,
            INFINITE);
        if (dw!=WAIT_OBJECT_0)
        {
            break;
        }
        std::ifstream is;
        is.open(MyInterface::m_szFilename,
            std::ios_base::in | std::ios_base::binary);
        long recordnumber;
        is >> recordnumber;
        is.close();

        if (recordnumber==-1)
        {
            MyInterface::m_recordnumber++;
        }
```
```