```
```text
for (double i = 0; i < short.MaxValue; i++)
{
    Count--;
}
Console.WriteLine(
    "Decrement Count = {0}", Count);
}
```
```

```
**OUTPUT 20.7**
```text
Decrement Count = -32767.01134
Main Count = 32767.01134
```
```

As Output 20.7 demonstrates, the value of Count for the thread executing Main() is never decremented by the thread executing Decrement(). For Main()’s thread, the initial value is 0.01134 and the final value is 32767.01134. Decrement() has similar values, except that they are negative. As Count is based on the static field of type ThreadLocal<T>, the thread running Main() and the thread running Decrement() have independent values stored in _Count.Value.

# ## Thread Local Storage with ThreadStaticAttribute

Decorating a static field with ThreadStaticAttribute, as in Listing 20.12, is a second way to designate a static variable as an instance per thread. This technique has a few caveats relative to ThreadLocal<T>, but it also has the advantage of being available prior to Microsoft .NET Framework 4. (Also, since ThreadLocal<T> is based on the ThreadStaticAttribute, it would consume less memory and give a slight performance advantage given frequently enough repeated small iterations.)

```
**LISTING 20.12: Using ThreadStaticAttribute for Thread Local Storage**
```csharp
using System;
using System.Threading;

public class Program
{
    [ThreadStatic]
    static double _Count = 0.01134;
    public static double Count
    {
        get { return Program._Count; }
        set { Program._Count = value; }
    }
```
```