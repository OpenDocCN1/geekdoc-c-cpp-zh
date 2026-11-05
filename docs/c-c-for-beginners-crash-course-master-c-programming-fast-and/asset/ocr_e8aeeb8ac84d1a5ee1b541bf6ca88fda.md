# 14.3 Main thread

The **System.Threading.Thread** class is used for working with threads. The main thread is created as soon as program starts execution. The **Thread** class is used for creating threads. They are known as child threads. The user can access the main thread by using the **CurrentThread** property of the Thread class.

**Example:**

```
**Example 53:**
```csharp
using System;
namespace thread
{
    class MainThread
    {
        static void Main(string[] args)
        {
            Thread t1 = new Thread();
            t1.Name="Thread1";
            Console.WriteLine("Thread is:{0}",t1.Name);
            Console.Read();
        }
    }
}
```
```

**When the code is compiled and executed, the output is:**

Thread is: Thread1