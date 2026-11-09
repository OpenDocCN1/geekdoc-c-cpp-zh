The static `System.Threading.Volatile` class offers two static methods that look like this:<sup>68</sup>

```
```
public static class Volatile {
   public static void Write(ref Int32 location, Int32 value);
   public static Int32 Read(ref Int32 location);
}
```
```

These methods are special. In effect, these methods disable some optimizations usually performed by the C# compiler, the JIT compiler, and the CPU itself. Here's how the methods work:

+   - The `Volatile.Write` method forces the value in location to be written to at the point of the call. In addition, any earlier program-order loads and stores must occur before the call to `Volatile.Write`.
+   - The `Volatile.Read` method forces the value in location to be read from at the point of the call. In addition, any later program-order loads and stores must occur after the call to `Volatile.Read`.

**Important** I know that this can be very confusing, so let me summarize it as a simple rule. When threads are communicating with each other via shared memory, write the last value by calling `Volatile.Write` and read the first value by calling `Volatile.Read`.

So now we can fix the `ThreadsSharingData` class using these methods:

```
```
internal sealed class ThreadsSharingData {
   private Int32 m_flag = 0;
   private Int32 m_value = 0;

   // This method is executed by one thread
   public void Thread1() {
      // Note: 5 must be written to m_value before 1 is written to m_flag
      m_value = 5;
      Volatile.Write(ref m_flag, 1);
   }

   // This method is executed by another thread
   public void Thread2() {
      // Note: m_value must be read after m_flag is read
      if (Volatile.Read(ref m_flag) == 1)
         Console.WriteLine(m_value);
   }
}
```
```

First, notice that we are following the rule. The `Thread1` method writes two values out to fields that

<sup>68</sup> There are also overloads of `Read` and `Write` that operate on the following types: `Boolean`, `(S)Byte`, `(U)Int16`, `UInt32`, `(U)Int64`, `(U)IntPtr`, `Single`, `Double`, and `T` where `T` is a generic type constrained to `'class'` (reference types).