```
using Contoso.CashFlow.Client;

class Program
{
    static void Main()
    {
        var t = new Terminal();
    }
}
```

![](bbox=[0.12, 0.42, 0.78, 0.64])

FIGURE 24.4 Namespaces are merely an illusion created by front-end languages.

On the first line of this C# fragment, we're importing the namespace, such that we can simply write Terminal rather than the long type name (including the namespace). At the IL level, though, the full type name is used.

In front of the fully qualified type name Contoso.CashFlow.Client.Terminal, another name is specified in between brackets. This corresponds to the name of the assembly defining the type. Here we've compiled the Terminal type into an assembly with the name ContosoCFC1ient. For the CLR to know where to find the type being referred to, it needs to know what assembly to look in.

This brings us to a discussion about the difference between namespaces and assemblies. In short, the two are mostly unrelated concepts. The name of an assembly doesn't dictate what namespaces can be defined inside it, nor does the name of a type (and its namespace) pose restrictions on which assembly it can be defined in. The only real relationship between both concepts is the fact that assemblies contain types and types live in namespaces, and therefore assemblies contain namespaces. In fact, the definition of a namespace can be spread across multiple assemblies, as exemplified by the framework assemblies System.dll (which, for instance, contains the System.Uri class) and mscorlib.dll (containing types like System.String).

# MSCORLIB VERSUS SYSTEM

Why are there multiple assemblies defining types of the Framework's top-level System namespace? The answer is partly historical and partly technical.