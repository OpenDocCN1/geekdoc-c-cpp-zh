resources must be managed by developers: you and the users of your classes. Two mechanisms help developers control the lifetimes of unmanaged resources: finalizers and the IDisposable interface. A finalizer is a defensive mechanism that ensures your objects always have a way to release unmanaged resources. Finalizers have many drawbacks, so you also have the IDisposable interface that provides a less intrusive way to return resources to the system in a timely manner.

Finalizers are called by the Garbage Collector. They will be called at some time after an object becomes garbage. You don't know when that happens. All you know is that it happens sometime after your object cannot be reached. That is a big change from C++, and it has important ramifications for your designs. Experienced C++ programmers wrote classes that allocated a critical resource in its constructor and released it in its destructor:

```
// Good C++, bad C#:
class CriticalSection
{
    // Constructor acquires the system resource.
    public CriticalSection()
    {
        EnterCriticalSection();
    }

    // Destructor releases system resource.
    ~CriticalSection()
    {
        ExitCriticalSection();
    }

    private void ExitCriticalSection()
    {
        throw new NotImplementedException();
    }
    private void EnterCriticalSection()
    {
        throw new NotImplementedException();
    }
}
```