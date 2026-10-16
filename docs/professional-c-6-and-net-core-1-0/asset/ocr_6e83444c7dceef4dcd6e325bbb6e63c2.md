```
```csharp
public void DoThat()
{
    lock (_syncRoot)
    {
    }
}
```
```

Using locks costs time and is not always necessary. You can create two versions of a class: synchronized and nonsynchronized. This is demonstrated in the next example code by changing the class `Demo`. The class `Demo` is not synchronized, as shown in the implementation of the `DoThis` and `DoThat` methods. The class also defines the `IsSynchronized` property, whereby the client can get information about the synchronization option of the class. To make a synchronized variant of the `Demo` class, you use the static method `Synchronized` to pass a nonsynchronized object, and this method returns an object of type `SynchronizedDemo`. `SynchronizedDemo` is implemented as an inner class that is derived from the base class `Demo` and overrides the virtual members of the base class. The overridden members make use of the SyncRoot pattern:

```
```csharp
public class Demo
{
    private class SynchronizedDemo: Demo
    {
        private object _syncRoot = new object();
        private Demo _d;

        public SynchronizedDemo(Demo d)
        {
            _d = d;
        }

        public override bool IsSynchronized => true;

        public override void DoThis()
        {
            lock (_syncRoot)
            {
                _d.DoThis();
            }
        }
        public override void DoThat()
        {
            lock (_syncRoot)
            {
                _d.DoThat();
            }
        }
    }
    public virtual bool IsSynchronized => false;

    public static Demo Synchronized(Demo d)
    {
        if (!d.IsSynchronized)
        {
            return new SynchronizedDemo(d);
        }
        return d;
    }
}
```
```