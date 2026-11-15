between threads so that no synchronization is necessary (this approach has proven invaluable in functional programming languages such as F#). Similarly, avoid locking on operations on thread-safe operations such as simple reads and writes of an int.

# More Synchronization Types

In addition to System.Threading.Monitor and System.Threading.Interlocked, several more synchronization techniques are available.

# System.Threading.Mutex

System.Threading.Mutex is similar in concept to the System.Threading.Monitor class (without the Pulse() method support), except that the lock keyword does not use it and Mutexes can be named so that they support synchronization across multiple processes. Using the Mutex class, you can synchronize access to a file or some other cross-process resource. Since Mutex is a cross-process resource, .NET 2.0 added support to allow for setting the access control via a System.Security.AccessControl.MutexSecurity object. One use for the Mutex class is to limit an application so that it cannot run multiple times simultaneously, as Listing 19.8 demonstrates.

# LISTING 19.8 Creating a Single Instance Application

```
using System;
using System.Threading;
using System.Reflection;

class Program
{
    public static void Main()
    {
        // Indicates whether this is the first
        // application instance
        bool firstApplicationInstance;

        // Obtain the mutex name from the full
        // assembly name.
        string mutexName =
            Assembly.GetEntryAssembly().FullName;

        using (Mutex mutex = new Mutex(false, mutexName,
            out firstApplicationInstance )
        {
```