# 17.5 Attributes for Interoperation

Note: This section is applicable only to the Microsoft .NET implementation of C#.

# 17.5.1 Interoperation with COM and Win32 Components

The .NET runtime provides a large number of attributes that enable C# programs to interoperate with components written using COM and Win32 DLLs. For example, the DllImport attribute can be used on a static extern method to indicate that the implementation of the method is to be found in a Win32 DLL. These attributes are found in the System.Runtime.InteropServices namespace, and detailed documentation for these attributes is found in the .NET runtime documentation.

# 17.5.2 Interoperation with Other .NET Languages

# 17.5.2.1 The IndexerName Attribute

Indexers are implemented in .NET using indexed properties, and have a name in the .NET metadata. If no IndexerName attribute is present for an indexer, then the name Item is used by default. The IndexerName attribute enables a developer to override this default and specify a different name.

```
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute : Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} }
    }
}
```