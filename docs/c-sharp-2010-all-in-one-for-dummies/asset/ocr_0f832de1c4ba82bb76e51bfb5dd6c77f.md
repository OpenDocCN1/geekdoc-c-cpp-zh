```
```csharp
public string FixNamespaceLine(string line)
{
    const string COMPANY_PREFIX = "CMSCo";
    int spaceIndex = line.IndexOf(' ');
    int nameStart = GetNameStartAfterNamespaceKeyword(line, spaceIndex);
    string newline = string.Empty;
    newline = PlugInNamespaceCompanyQualifier(line, COMPANY_PREFIX, nameStart);
    return newline.Trim();
}
```
```

Given a C# file, this method is part of some code intended to find the namespace keyword in the file and insert a string representing a company name (one of ours) as a prefix on the namespace name. (See Book II, Chapter 10 for information about namespaces.) The following example illustrates where the namespace keyword is likely to be found in a C# file:

```
```csharp
using System;
namespace SomeName
{
    // Code within the namespace . . .
}
```
```

The result of running the FixNamespaceLine() method on this type of file should convert the first line into the second:

```
```
namespace SomeName
namespace CmsCo.SomeName
```
```

The overall program reads .CS files. Then it steps through the lines one by one, feeding each one to the FixNamespaceLine() method. Given a line of code, the method calls String.IndexOf() to find the index of the namespace name (normally, 10). Then it calls GetNameStartAfterNamespaceKeyword() to locate the beginning of the namespace name. Finally, it calls another method, PlugInNamespaceCompanyQualifier() to plug the company name into the correct spot in the line, which it then returns. Much of the work is done by the subordinate methods.

First, even without knowing what this code is for or what the two called methods do, consider the input. The line argument could have at least one problem for the call to String.IndexOf(). If line is null, the IndexOf() call results in an ArgumentNullException. You can't call a method on a null object. Also, at first blush, will calling IndexOf() on an empty string work? It turns out that it will, so no exception occurs there, but what happens if you pass an empty line to one of those methods with the long names? We recommend adding, if warranted, a guard clause before the first line of code in FixNamespaceLine() — and at least checking for null:

```
```csharp
if(String.IsNullOrEmpty(name))  // A handy string method
{
    return name;  // You can get away with a reasonable return value here
    // instead of throwing an exception.
}
```
```