# Threads in the .NET Framework

```
bState = true;
}
static void GetMethod( )
{
    if (bState)
    {
        MessageBox::Show( Convert::ToString(iValue) );
    }
private:
    static bool bState;
    static int iValue;
}
```

```
ref class TestWorker
public:
    TestWorker()
{
    TestClass_t
    Task*_t1 = gcnew Task(gcnew Action (& &t.SetMethod ) );
    _t1->Start();
    Task*_t2 = gcnew Task(gcnew Action (& &t.GetMethod ) );
    _t2->Start();
}
```

In your opinion, is it possible that GetMethod shows 0 for iValue? Well, the mentioned reasons-yes. The simplest solution is to create a memory fence or surround usage of the attribute bState with MemoryBarrier statements, as shown in the following code:

```
static void SetMethod()
{
    iValue = 5;
    Thread::MemoryBarrier();
    bState = true;
}
static void GetMethod()
{
    if (bState)

```