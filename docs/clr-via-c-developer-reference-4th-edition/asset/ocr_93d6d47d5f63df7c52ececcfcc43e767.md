# Ch02-3-MultiFileLibrary.dll Properties

| Property | Value |
|---|---|n File description | MultiFileLibrary.dll |
 Type | Application extension |
 File version | 1.0.0 |
 Product name | Winterlect (R) MultiFileLibrary's Type Lib... |
 Product version | 2.0.0 |
 Copyright | Copyright (c) Winterlect 2013 |
 Size | 5.00 KB |
 Date modified | Neutral |
 Legal trademarks | MultiFileLibrary is a registered trademark... |
 Original filename | Ch02-3-MultiFileLibrary.dll |

FIGURE 2-4 The Details tab of the Ch02-3-MultiFileLibrary.dll Properties dialog box.

When building an assembly, you should set the version resource fields by using custom attributes that you apply at the assembly level in your source code. Here's what the code that produced the version information in Figure 2-4 looks like.

using System.Reflection;

```
// FileDescription version information:
[assembly:AssemblyTitle("MultiFileLibrary.dll")

// Comments version information:
[assembly:AssemblyDescription("This assembly contains MultiFileLibrary's types")];

// CompanyName version information:
[assembly:AssemblyCompany("Winterlect")];

// ProductName version information:
[assembly:AssemblyProduct("Winterlect (R) MultiFileLibrary's Type Library")];

// LegalCopyright version information:
[assembly:AssemblyCopyright("Copyright (c) Winterlect 2013")];

// LegalTrademarks version information:
[assembly:AssemblyTrademark("MultiFileLibrary is a registered trademark of Winterlect")];

// AssemblyVersion version information:
[assembly:AssemblyVersion("3.0.0.0")];
```

CHAPTER 2 Building, Packaging, Deploying, and Administering Applications and Types 55