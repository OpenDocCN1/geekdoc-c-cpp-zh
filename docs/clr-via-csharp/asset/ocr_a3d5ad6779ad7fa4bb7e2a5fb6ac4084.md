![](bbox=[0.1, 0.08, 0.14, 0.13])

**Important** I'm frequently asked why C# requires that a call to a method must specify **out** or **ref**. After all, the compiler knows whether the method being called requires **out** or **ref** and should be able to compile the code correctly. It turns out that the compiler can indeed do the right thing automatically. However, the designers of the C# language felt that the caller should explicitly state its intention. This way at the call site, it's obvious that the method being called is expected to change the value of the variable being passed.

In addition, the CLR allows you to overload methods based on their use of **out** and **ref** parameters. For example, in C#, the following code is legal and compiles just fine:

```
~~~
public sealed class Point {
    static void Add(Point p) { ... }
    static void Add(ref Point p) { ... }
}
~~~
```

It's not legal to overload methods that differ only by **out** and **ref** because the metadata representation of the method's signature for the methods would be identical. So I couldn't also define the following method in the preceding **Point** type:

```
~~~
static void Add(out Point p) { ... }
~~~
```

If you attempt to include the last **Add** method in the **Point** type, the C# compiler issues this message: **error CS0663: 'Add' cannot define overloaded methods that differ only on ref and out.**

Using **out** and **ref** with value types gives you the same behavior that you already get when passing reference types by value. With value types, **out** and **ref** allow a method to manipulate a single value type instance. The caller must allocate the memory for the instance, and the callee manipulates that memory. With reference types, the caller allocates memory for a pointer to a reference object, and the callee manipulates this pointer. Because of this behavior, using **out** and **ref** with reference types is useful only when the method is going to "return" a reference to an object that it knows about. The following code demonstrates:

```
~~~
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs;   // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        // Continue while there are more files to process.
        for (; fs != null; ContinueProcessingFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }
}
~~~
```