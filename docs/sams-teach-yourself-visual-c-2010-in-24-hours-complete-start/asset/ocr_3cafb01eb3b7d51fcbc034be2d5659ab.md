```
public class Example
{
    #if DEBUG
        public void DisplayDiagnostics()
        {
            Console.WriteLine("Diagnostic information.");
        }
    #endif

    public string Method()
    {
        return "Test";
    }
}
```

Although you can mix the Conditional attribute and the #if/#endif preprocessor symbols, you need to be very careful if you do so. Removing code using #if/#endif occurs earlier in the compilation process and may cause the compiler to be unable to compile the Conditional method.

# Global Attributes

Although most attributes apply to specific code declarations, some apply to an entire assembly or module. These attributes appear in the source code after any using directives but before any code declarations (such as class or namespace declarations).

# By the Way

# Assembly Manifest

The assembly manifest contains the data that describes how the elements in the assembly are related, including version and security information. The manifest is typically included with the compiled file.

Typically, global attributes are placed in an AssemblyInfo.cs file, but they can appear in multiple files if those files are compiled in a single compilation pass. The common global attributes are shown in Table 20.2.

TABLE 20.2 Global Attributes
| Attribute | Purpose |
| :--- | :--- |
| **Assembly Identity Attributes** | |
| AssemblyName | Full name of the assembly |
| AssemblyVersion | Version of the assembly |
| AssemblyCulture | Culture the assembly supports |
| AssemblyFlags | Indicates if multiple copies of the assembly can coexist |