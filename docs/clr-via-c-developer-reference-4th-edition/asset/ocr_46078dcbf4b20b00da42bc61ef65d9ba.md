```
// Note: m_value could be read before m_flag
if (m_flag == 1)
    Console.WriteLine(m_value);

```

The problem with this code is that the compilers/CPU could translate the code in such a way as reverse the two lines of code in the Thread1 method. After all, reversing the two lines of code does not change the intention of the method. The method needs to get a 5 in m_value and a 1 in m_flag. From a single-threaded application's perspective, the order of executing this is important. If these two lines execute in reverse order, then another executing the Thread2 method could see m_value as 1 and then display

Look at this code another way. Let's say that the code in the Thread1 method executes in program order (the way it was written). When compiling in the Thread2 method, the compiler must generate code to read m_flag and m_value from CPU into registers. It is possible that RAM will deliver the m_value first, which would change a 0. The Thread1 method could execute, changing m_value to 5 and m_flag to 1. But Thread2's CPU register doesn't see that m_value has been changed to 5 by this other thread, and then the value in m_flag could be read from RAM to a CPU register and the value of m_flag becomes 1, causing Thread2 to display 0.

This is all very scary stuff and is likely to cause problems in a release of your program in a debug build of your program, making it particularly tricky to detect these and correct your code. Let's talk about how to correct your code.

The System.Threading.Volatile class offers two static methods that look like this.

```
public static class Volatile {
    public static void Write(ref Int32 location, Int32 value);
    public static Int32 Read(ref Int32 location);

```

These methods are special. In effect, these methods disable some optimizations usually performed by the C# compiler, the JIT compiler, and the CPU itself. Here's how the methods work:

+   - The Volatile.Write method forces the value in location to be written to the point of the call. In addition, any earlier program-order loads and stores occurs before the call to Volatile.Write.

+   - The Volatile.Read method forces the value in location to be read from the point of the call. In addition, any later program-order loads and stores occur after the call to Volatile.Read.

> 5 There are also overloads of Read and Write that operate on the following types: Boolean, (S)Byte, (U)Int16, UInt32, (U)Int64, (U)IntPtr. Single, Double, and where T is a generic type constrained to 'class' (reference types).