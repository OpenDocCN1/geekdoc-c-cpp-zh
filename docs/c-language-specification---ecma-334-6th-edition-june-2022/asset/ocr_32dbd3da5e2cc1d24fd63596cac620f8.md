```
```csharp
using System;
using System.Reflection;

public sealed class InterrogateHelpUrls
{
    public static void Main(string[] args)
    {
        Type helpType = typeof(HelpAttribute);
        string assemblyName = args[0];
        foreach (Type t in Assembly.Load(assemblyName).GetTypes())
        {
            Console.WriteLine($"Type : {t}");
            HelpAttribute[] helpers =
                (HelpAttribute[])t.GetCustomAttributes(helpType, false);
            for (int at = 0; at != helpers.Length; at++)
            {
                Console.WriteLine($"\tUrl : {helpers[at].Url}");
            }
        }
    }
}
end example
```
```

# 21.5 Reserved attributes

# 21.5.1 General

A small number of attributes affect the language in some way. These attributes include:

+   - System.AttributeUsageAttribute (§21.5.2), which is used to describe the ways in which an attribute class can be used.
+   - System.Diagnostics.ConditionalAttribute (§21.5.3), is a multi-use attribute class which is used to define conditional methods and conditional attribute classes. This attribute indicates a condition by testing a conditional compilation symbol.
+   - System.ObsoleteAttribute (§21.5.4), which is used to mark a member as obsolete.
+   - System.Runtime.CompilerServices.CallerLineNumberAttribute (§21.5.5.2), System.Runtime.CompilerServices.CallerFilePathAttribute (§21.5.5.3), and System.Runtime.CompilerServices.CallerMemberNameAttribute (§21.5.5.4), which are used to supply information about the calling context to optional parameters.

An execution environment may provide additional implementation-specific attributes that affect the execution of a C# program.

# 21.5.2 The AttributeUsage attribute

The attribute AttributeUsage is used to describe the manner in which the attribute class can be used.

A class that is decorated with the AttributeUsage attribute shall derive from System.Attribute, either directly or indirectly. Otherwise, a compile-time error occurs.

*Note:* For an example of using this attribute, see §21.2.2. *end note*