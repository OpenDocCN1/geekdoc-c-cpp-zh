These restrictions ensure that all threads will observe volatile writes performed by any other thread in the order in which they were performed. A conforming implementation is not required to provide a single total ordering of volatile writes as seen from all threads of execution. The type of a volatile field shall be one of the following:

+   - A reference-type.
+   - A type-parameter that is known to be a reference type (§15.2.5).
+   - The type byte, sbyte, short, ushort, int, uint, char, float, bool, System.IntPtr, or System.UIntPtr.
+   - An enum-type having an enum base type of byte, sbyte, short, ushort, int, or uint.

```
[Example: The example
using System;
using System.Threading;
class Test
{
    public static int result;
    public static volatile bool finished;
    static void Thread2() {
        result = 143;
        finished = true;
    }
    static void Main() {
        finished = false;
        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();
        // wait for Thread2 to signal that it has a result by setting
        // finished to true.
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
```

produces the output:

result = 143

In this example, the method Main starts a new thread that runs the method Thread2. This method stores a value into a non-volatile field called result, then stores true in the volatile field finished. The main thread waits for the field finished to be set to true, then reads the field result. Since finished has been declared volatile, the main thread shall read the value 143 from the field result. If the field finished had not been declared volatile, then it would be permissible for the store to result to be visible to the main thread after the store to finished, and hence for the main thread to read the value 0 from the field result. Declaring finished as a volatile field prevents any such inconsistency. end example

# 15.5.5 Field initialization

The initial value of a field, whether it be a static field or an instance field, is the default value (§10.3) of the field's type. It is not possible to observe the value of a field before this default initialization has occurred, and a field is thus never "uninitialized". [Example: The example

```
using System;
class Test
{
    static bool b;
    int i;
```