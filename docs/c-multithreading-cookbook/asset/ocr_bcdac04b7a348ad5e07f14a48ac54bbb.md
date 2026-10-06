```
bool bPrintOutput();

class CBankAccount{
public:
    CBankAccount(double dBalance) : dBalance(dBalance) { uID =
    NewId();*szLock = 0; _tcscpy_s(szLock, LockName()); }
    CBankAccount(double dBalance, TCHAR* szLockName) :
dBalance(dBalance) { uID = NewId();*szLock = 0; _tcscpy_s(szLock,
szLockName); }
    static DWORD WINAPI Transfer(LPVOID lpParameter);
    double Balance()() { return dBalance; }
    unsigned AccountID() const { return uID; }
    static TCHAR LockName(void);

private:
    unsigned uID;
    double dBalance;
    TCHAR szLock[32];
    static unsigned NewId() { static unsigned uSeed = 61524; return uSeed++; }

TCHAR* CBankAccount::LockName(void)
{
    static int iCount = 0;
    static TCHAR szBuffer[32];

    if (*szLock == 0)
{
        wprintf(szBuffer, _T("_lock_%d"), +iCount);
    }
    else
{
        return szLock;
    }

    return szBuffer;
}

DWORD WINAPI CBankAccount::Transfer(LPVOID lpParameter)
{
    CParameters* parameters = (CParameters*)lpParameter;

    CClock* outerLock = new CClock(parameters->fromAccount->szLock);
```