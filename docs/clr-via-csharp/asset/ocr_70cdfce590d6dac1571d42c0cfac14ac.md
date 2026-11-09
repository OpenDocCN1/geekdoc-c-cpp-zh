the Microsoft Visual Studio code analysis tool (FxCopCmd.exe) offers a **System.Diagnostics.CodeAnalysis.SuppressMessageAttribute** which you can apply to types and members in order to suppress the reporting of a specific static analysis tool rule violation. This attribute is only looked for by the code analysis utility; the attribute is never looked for when the program is running normally. When not using code analysis, having **SuppressMessage** attributes sitting in the metadata just bloats the metadata, which makes your file bigger, increases your process's working set, and hurts your application's performance. It would be great if there were an easy way to have the compiler emit the **SuppressMessage** attributes only when you intend to use the code analysis tool. Fortunately, there is a way to do this by using conditional attribute classes.

An attribute class that has the **System.Diagnostics.ConditionalAttribute** applied to it is called a *conditional attribute class*. Here is an example:

```
```csharp
//#define TEST
#define VERIFY

using System;
using System.Diagnostics;


[Conditional("TEST")][Conditional("VERIFY")]
public sealed class CondAttribute : Attribute {
}

[Cond]
public sealed class Program {
    public static void Main() {
        Console.WriteLine("CondAttribute is {0}applied to Program type.",
            Attribute.IsDefined(typeof(Program),
                typeof(CondAttribute)) ? "" : "not ");
    }
}
```
```

When a compiler sees an instance of the **CondAttribute** being applied to a target, the compiler will emit the attribute information into the metadata only if the **TEST** or **VERIFY** symbol is defined when the code containing the target is compiled. However, the attribute class definition metadata and implementation is still present in the assembly.