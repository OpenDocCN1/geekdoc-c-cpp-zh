```
C# equivalent
public static void printAll<a>(IIEnumerable<<a> aSeq)
{
    foreach (a i in aSeq)
    {
        <your function call>
    }
}
```

If you're not convinced yet, List 1-82 demonstrates how to use type inference and a tuple to create a general swap function. The function can handle any data type. If you try to use C# to implement the same function, you'll find the F# code is more clean and elegant. If you use Visual Studio or MonoDevelop, type information can be shown when hovering over the function.

# LISTING 1-82 A tuple and swap function

```
// swap a and b
let swap(a,b) = (b,a)
```

# Interop and Function Parameters

Some F# users start to use F# as a library authoring tool. The F# library is then referenced and invoked from some C# library or application. Because F# is a .NET language, using interop with other .NET languages is seamless. Adding a reference to an F# project is exactly as same as adding one to a C# project. The only thing that needs to be explained is how to add a reference to FSI:

+   1. Use #r to reference a DLL.

+   2. Open the namespace.

Listing 1-83 shows how to reference System.Core.dll, open the System.Collections.Generic namespace, and use the HashSet<T> type.

# LISTING 1-83 Creating a HashSet in an F# script file or in FSI

```
#r "System.Core.dll"
open System.Collections.Generic
let a = HashSet<int>()()
```

> Note F# does not need new to instantiate an object. However, the new keyword is recommended when the class type implements the IDisposable interface.