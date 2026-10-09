
Named parameters allow for assigning attribute data without providing constructors for every conceivable combination of which attribute properties are specified and which are not. Given that many of an attribute's properties may be optional, this is a useful construct in many cases.

## BEGINNER TOPIC

## FlagsAttribute

Chapter 9 introduced enums and included an Advanced Topic covering FlagsAttribute. This framework-defined attribute targets enums that represent flag type values. The Beginner Topic here also addresses FlagsAttribute, starting with the sample code shown in Listing 18.22.

```csharp
// FileAttributes defined in System.IO
[Flags] // Decorating an enum with FlagsAttribute
public enum FileAttributes
{
    ReadOnly = 1<<0, // 00000000000001
    Hidden = 1<<1, // 00000000000010
    // ...
}

using System;
using System.Diagnostics;
using System.IO;

class Program
{
    public static void Main()
    {
        // ...
        string fileName = @"enumtest.txt";
        FileInfo file = new FileInfo(fileName);

        file.Attributes = FileAttributes.Hidden | FileAttributes.ReadOnly;

        Console.WriteLine("{0}\" outputs as \"{1}\"",
            file.Attributes,
            file.Attributes);

        FileAttributes attributes =
            (FileAttributes)Enum.Parse(typeof(FileAttributes),
            file.Attributes.ToString());

        Console.WriteLine(attributes);

        // ...
    }
}
```

Output 18.6 shows the results of Listing 18.22.

**OUTPUT 18.6**

"ReadOnly | Hidden" outputs as "ReadOnly, Hidden"

The flag documents that the enumeration values can be combined. Furthermore, it changes the behavior of the ToString() and Parse() methods. For example, calling ToString() on an enumeration that is decorated with FlagsAttribute writes out the strings for each enumeration flag that is set. In Listing 18.22, file.Attributes.ToString() returns "ReadOnly, Hidden" rather than the 3 it would have returned without the FlagsAttribute flag. If two enumeration values are the same, the ToString() call would return the first one. As mentioned earlier, however, you should use caution when relying on this outcome because it is not localizable.

Parsing a value from a string to the enumeration also works, provided each enumeration value identifier is separated by a comma.

Note that FlagsAttribute does not automatically assign the unique flag values or check that flags have unique values. The values of each enumeration item still must be assigned explicitly.

## Predefined Attributes

The AttributeUsageAttribute attribute has a special characteristic that you haven't seen yet in the custom attributes you have created in this book. This attribute affects the behavior of the compiler, causing the compiler to sometimes report an error. Unlike the reflection code you wrote earlier for retrieving CommandLineRequiredAttribute and CommandLineSwitchAliasAttribute, AttributeUsageAttribute has no runtime code; instead, it has built-in compiler support.

AttributeUsageAttribute is a predefined attribute. Not only do such attributes provide additional metadata about the constructs they decorate, but the runtime and compiler also behave differently to facilitate these attributes' functionality. Attributes such as AttributeUsageAttribute, FlagsAttribute, ObsoleteAttribute, and ConditionalAttribute are examples of predefined attributes. They implement special behavior that only the CLI provider or compiler can offer because there are no extension points for additional noncustom attributes. In contrast, custom attributes are entirely passive. Listing 18.22 includes a couple of predefined attributes; Chapter 19 includes a few more.

## System.ConditionalAttribute

Within a single assembly, the System.Diagnostics.ConditionalAttribute attribute behaves a little like the #if/#endif preprocessor identifier. However, instead of eliminating the CIL code from the assembly, System.Diagnostics.ConditionalAttribute will optionally cause the call to behave like a no-op, an instruction that does nothing. Listing 18.23 demonstrates the concept, and Output 18.7 shows the results.

**LISTING 18.23: Using ConditionalAttribute to Eliminate a Call**

```csharp
#define CONDITION_A

using System;
using System.Diagnostics;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Begin...");
        MethodA();
        MethodB();
        Console.WriteLine("End...");
    }

    [Conditional("CONDITION_A")]
    static void MethodA()
    {
        Console.WriteLine("MethodA() executing...");
    }

    [Conditional("CONDITION_B")]
    static void MethodB()
    {
        Console.WriteLine("MethodB() executing...");
    }
}
```

**OUTPUT 18.7**

```text
Begin...
MethodA() executing...
End...
```

This example defined CONDITION_A, so MethodA() executed normally. CONDITION_B, however, was not defined either through #define or by using the csc.exe /Define option. As a result, all calls to Program.MethodB() from within this assembly will do nothing.

Functionally, ConditionalAttribute is similar to placing an #if/#endif around the method invocation. The syntax is cleaner, however, because developers create the effect by adding the ConditionalAttribute attribute to the target method without making any changes to the caller itself.

The C# compiler notices the attribute on a called method during compilation, and assuming the preprocessor identifier exists, it eliminates any calls to the method. ConditionalAttribute, however, does not affect the compiled CIL code on the target method itself (besides the addition of the attribute metadata). Instead, it affects the call site during compilation by removing the calls. This further distinguishes ConditionalAttribute from #if/#endif when calling across assemblies. Because the decorated method is still compiled and included in the target assembly, the determination of whether to call a method is based not on the preprocessor identifier in the callee’s assembly but rather on the caller’s assembly. In other words, if you create a second assembly that defines CONDITION_B, any calls to Program.MethodB() from the second assembly will execute. This is a useful characteristic in many tracing and testing scenarios. In fact, calls to System.Diagnostics.Trace and System.Diagnostics.Debug use this trait with ConditionalAttributes on TRACE and DEBUG preprocessor identifiers.

Because methods don’t execute whenever the preprocessor identifier is not defined, ConditionalAttribute may not be used on methods that include an out parameter or specify a return other than void. Doing so causes a compile-time error. This makes sense because potentially none of the code within the decorated method will execute, so it is unknown what to return to the caller. Similarly, properties cannot be decorated with ConditionalAttribute. The AttributeUsage (see the section titled “System.AttributeUsageAttribute” earlier in this chapter) for ConditionalAttribute is AttributeTargets.Class and AttributeTargets.Method, which allows the attribute to be used on either a method or a class. However, the class usage is special because ConditionalAttribute is allowed only on System.Attribute-derived classes.

When ConditionalAttribute decorates a custom attribute, the latter can be retrieved via reflection only if the conditional string is defined in the calling assembly. Without such a conditional string, reflection that looks for the custom attribute will fail to find it.

## System.ObsoleteAttribute

As mentioned earlier, predefined attributes affect the compiler's and/or the runtime's behavior. ObsoleteAttribute provides another example of attributes affecting the compiler's behavior. Its purpose is to help with the versioning of code, providing a means of indicating to callers that a member or type is no longer current. Listing 18.24 is an example of ObsoleteAttribute usage. As Output 18.8 shows, any callers that compile code that invokes a member marked with ObsoleteAttribute will cause a compile-time warning, optionally an error.

**LISTING 18.24: Using ObsoleteAttribute**

```csharp
class Program
{
    public static void Main()
    {
        ObsoleteMethod();
    }

    [Obsolete]
    public static void ObsoleteMethod()
    {
    }
}
```

2. A feature started in Microsoft .NET Framework 2.0.
