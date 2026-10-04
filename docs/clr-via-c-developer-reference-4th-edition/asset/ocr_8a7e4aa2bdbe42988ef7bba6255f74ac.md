# Conditional Attribute Classes

Over time, the ease of defining, applying, and reflecting over attributes has caused developers to use them more and more. Using attributes is also a very easy way to annotate your code using attributes to assist them with implementing features. Lately, developers have used them with design and debugging. For example, the Microsoft Visual Studio code analysis tool (FxCop.nd) offers a System.CodeAnalysis.SuppressAttribute that you can apply to types and members in order to suppress the reporting of a static analysis tool rule violation. This attribute is only looked for by the code analysis tool; the attribute is never looked for the program running. When not using code analysis, SuppressMessage attributes sitting in the metadata bloats what makes your file bigger, increases your process's working set, and hurts your application's performance. It would be great if there were an easy way to have the compiler emit the SuppressMessage attributes only when you intend to use the code analysis tool. Frankly, there is a way to do this by using conditional attribute classes.

An attribute that has the System.Diagnostics.ConditionalAttribute applied to it is called a conditional attribute class. Here is an example.

```
##define TEST
#define VERIFY

using System;
using System.Diagnostics;

[Conditional("TEST")][Conditional("VERIFY")]
public sealed class CondAttribute : Attribute {
}\}

[Cond]
public sealed class Program {
    public static void Main() {
        Console.WriteLine("Attribute is " + "applied to Program type.",
        Attribute.IsDefined(typeof(Program),
        typeof(CondAttribute)) ? " " : "not ");
    }
}
```

When a compiler sees an instance of the CondAttribute applied to a target, the compiler will emit the attribute information into the metadata only if the TEST or VERIFY symbol is defined when the code containing the target is compiled. However, the attribute class definition metadata and implementation is still present in the assembly.