```
if (mutex.WaitOne())
{
    try
    {
        // synchronized region
    }
    finally
    {
        mutex.ReleaseMutex();
    }
}
else
{
    // some problem happened while waiting
}
```

Because a named mutex is known system-wide, you can use it to keep an application from being started twice. In the following WPF application, the constructor of the Mutex object is invoked. Then it is verified whether the mutex with the name SingletonWinAppMutex exists already. If it does, the application exits (code file SingletonWPF/App.xaml.cs):

```
public partial class App : Application
{
    protected override void OnStartup(StartupEventArgs e)
    {
        bool mutexCreated;
        var mutex = new Mutex(false,"SingletonWinAppMutex", out mutexCreated);
        if (!mutexCreated)
        {
            MessageBox.Show("You can only start one instance of the application");
            Application.Current.Shutdown();
        }

        base.OnStartup(e);
    }
}
```

# Semaphore

A semaphore is very similar to a mutex, but unlike the mutex, the semaphore can be used by multiple threads at once. A semaphore is a counting mutex, meaning that with a semaphore you can define the number of threads that are allowed to access the resource guarded by the semaphore simultaneously. This is useful if you need to limit the number of threads that can access the available resources. For example, if a system has three physical I/O ports available, three threads can access them simultaneously, but a fourth thread needs to wait until the resource is released by one of the other threads.

.NET Core 1.0 provides two classes with semaphore functionality: Semaphore and SemaphoreSlim. Semaphore can be named, can use system-wide resources, and allows synchronization between different processes. SemaphoreSlim is a lightweight version that is optimized for