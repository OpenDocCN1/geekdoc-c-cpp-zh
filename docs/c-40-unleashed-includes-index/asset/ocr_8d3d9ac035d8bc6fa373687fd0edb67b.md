# Object Browser

With the .NET Framework class libraries ever growing and lots of other libraries being used in managed code applications, the ability to browse through available libraries becomes quite important. We've already seen IntelliSense as a way to show available types and their available members, but for more global searches, different visualizations are desirable. Visual Studio's built-in Object Browser is one such tool (see Figure 3.38).

![](bbox=[0.08, 0.31, 0.66, 0.68])

FIGURE 3.38 Object Browser visualizing the System.Core assembly.

This tool feels a lot like .NET Reflector, with the ability to add assemblies for inspection, browse namespaces, types, and members, and a way to search across all of those. It doesn't have decompilation support, though.

# .NET FRAMEWORK SOURCE CODE

Want to see the .NET Framework source code itself? This has been a longstanding request from the community to help boost the understanding of framework functionality and, in answer to this request, Microsoft has started to make parts of the source code for the .NET Framework available through a shared source program starting from .NET 3.5. Even more so, Visual Studio has been enhanced to be able to step through .NET Framework source code available from the Microsoft servers.

You can find more information on the Microsoft Shared Source Initiative for the .NET Framework site at http://referencesource.microsoft.com/netframework.aspx.

# Code Insight

An all-important set of features that form an integral part of IDE functionality today is what we can refer to collectively as “code insight” features. No matter how attractive the act of writing code may look—because that’s what we, developers, are so excited about,