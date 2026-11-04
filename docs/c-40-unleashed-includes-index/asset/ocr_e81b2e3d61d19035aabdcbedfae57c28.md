![](bbox=[0.059, 0.085, 0.377, 0.32])

FIGURE 26.10 System.Core’s framework enrichment.

In .NET 4.0, the System.Core assembly was kept even though this latest version of the framework supports a complete side-by-side installation alongside earlier versions of the runtime and the libraries. Strictly speaking, the functionality in System.Core could have been merged into traditional and special BCL containers like the mscorlib and System assemblies. For reasons of discovery of features (people have gotten used to associating, say, LINQ with System.Core) and performance (size of core assemblies that are loaded by every application), System.Core was kept.

A few commonly used types were relocated, though (for example, the Func delegate types), as shown in Figure 26.11. This use of forwarding allows applications compiled against the .NET 3.5 System.Core assembly to continue working even though some of the types have been moved to mscorlib. Such a refactoring was deemed useful to avoid having to load System.Core for other portions of the framework that depend on those commonly used types.

![](bbox=[0.059, 0.675, 0.412, 0.86])

FIGURE 26.11 Types forwarded from System.Core to mscorlib in .NET 4.

In summary, when targeting .NET 3.5 or later, System.Core is the third big member of the BCL assembly triad, alongside mscorlib and System. When looking for commonly used