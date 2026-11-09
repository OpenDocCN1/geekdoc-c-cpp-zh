performance. Since a generic algorithm can now be created to work with a specific value type, the instances of the value type can be passed by value, and the CLR no longer has to do any boxing. In addition, since casts are not necessary (see the previous bullet), the CLR doesn't have to check the type safety of the attempted cast, and this results in faster code too.

To drive home the performance benefits of generics, I wrote a program that tests the performance of the generic `List` algorithm against the FCL's non-generic `ArrayList` algorithm. In fact, I tested the performance of these two algorithms by using both value type objects and reference type objects. Here is the program itself:

```
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;

public static class Program {
    public static void Main() {
        ValueTypePerfTest();
        ReferenceTypePerfTest();
    }

    private static void ValueTypePerfTest() {
        const Int32 count = 10000000;

        using (new OperationTimer("List<Int32>")) {
            List<Int32> l = new List<Int32>(count);
            for (Int32 n = 0; n < count; n++) {
                l.Add(n);
                Int32 x = l[n];
            }
            l = null;   // Make sure this gets GC'd
        }

        using (new OperationTimer("ArrayList of Int32")) {
            ArrayList a = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                a.Add(n);
                Int32 x = (Int32) a[n];
            }
            a = null;   // Make sure this gets GC'd
        }
    }

    private static void ReferenceTypePerfTest() {
        const Int32 count = 10000000;

        using (new OperationTimer("List<String>")) {
            List<String> l = new List<String>();
            for (Int32 n = 0; n < count; n++) {
                l.Add("X");
                String x = l[n];
            }
        }
    }
}
```
```