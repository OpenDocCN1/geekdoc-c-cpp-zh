
Parameters defined by a constructor are called positional parameters because they must be specified in a defined order and cannot be omitted. Attributes also make use of named parameters, which are optional and can be specified in any order. Positional parameters must always be specified first. For example, the attributes shown in Listing 20.3 are all equivalent.

### **LISTING 20.3 Attribute Parameters**

```csharp
[DllImport("kernel32.dll")]
[DllImport("kernel32.dll", SetLastError = false, ExactSpelling = true)]
[DllImport("kernel32.dll", ExactSpelling = true, SetLastError = false)]
```

> **Named Attribute Parameters**
The named parameters used by attributes are not the same as the named parameters you learned about in Hour 3, "Understanding Classes and Objects the C# Way." When used with attributes, they are really more like object initializers (which you also learned about in Hour 3); they actually correspond to public read-write properties of the attribute, easily allowing you to set the property value.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_449_0.png)

The type of code declaration to which an attribute is applied is called the target. Table 20.1 shows the possible target values.

### **TABLE 20.1 Attribute Targets**

| Target | Applies to |
|:---|:---|
| assembly | Entire assembly |
| module | Current assembly module |
| field | Class field |
| event | Event |
| method | Method, property get accessor, or property set accessor |
| param | Method or property set accessor parameter |
| property | Property |
| return | Return value of a method, indexer property, or property get accessor |
| type | Struct, class, interface, or enum |

Although an attribute normally applies to the element it precedes, you can also explicitly identify the target to which it applies. For example, you can identify whether an attribute applies to a method, its parameter, or its return value, as shown in Listing 20.4.

### **LISTING 20.4 Attribute Parameters**

```csharp
[CustomAttribute]
string Method()
{
    return String.Empty;
}

[method: CustomAttribute]
string Method()
{
    return String.Empty;
}

[return: CustomAttribute]
string Method()
{
    return String.Empty;
}
```

## Working with the Common Attributes

The .NET Framework defines many attributes that you can use in your own applications. The most common ones are the *Obsolete* attribute, the *Conditional* attribute, and the set of global attributes.

### The Obsolete Attribute

The *Obsolete* attribute indicates that a code declaration should no longer be used and causes the compiler to generate a warning or error, depending on how the attribute is configured. This attribute can be used with no parameters, but it is recommended to supply an explanation and indicate if a compiler warning or error should be generated. Listing 20.5 shows an example of using the *Obsolete* attribute.

### **LISTING 20.5 Obsolete Attribute**

```csharp
public class Example
{
    [Obsolete("Consider using OtherMethod instead.", false)]
    public string Method()
    {
        return String.Empty;
    }

    public string OtherMethod()
    {
        return "Test";
    }
}
```

### The Conditional Attribute

The **Conditional** attribute indicates that a code declaration is dependent on a preprocessor conditional compilation symbol, such as DEBUG, and can be applied to a class or a method. The compiler uses this attribute to determine if the call is included or left out. If the conditional symbol is present during compilation, the call is included; otherwise, it is not. If the **Conditional** attribute is applied to a method, the method must not have a return value. Listing 20.6 shows an example of using the **Conditional** attribute.

### **LISTING 20.6 Conditional Attribute**

```csharp
public class Example
{
    [Conditional("DEBUG")]
    public void DisplayDiagnostics()
    {
        Console.WriteLine("Diagnostic information.");
    }

    public string Method()
    {
        return "Test";
    }
}
```

The **Conditional** attribute can also be applied to custom attributes, in which case the attribute adds metadata information only if the compilation symbol is defined.

### The #if and #endif Preprocessor Symbols

Using the **Conditional** attribute is similar to using the #if and #endif preprocessor symbols but can provide a cleaner alternative that leads to fewer bugs. The class shown in Listing 20.6 using #if/#endif instead of the **Conditional** attribute is shown here.

> **By the Way**

```csharp
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

### Global Attributes

Although most attributes apply to specific code declarations, some apply to an entire assembly or module. These attributes appear in the source code after any using directives but before any code declarations (such as class or namespace declarations).

> **By the Way**
>
> **Assembly Manifest**
> The assembly manifest contains the data that describes how the elements in the assembly are related, including version and security information. The manifest is typically included with the compiled file.

Typically, global attributes are placed in an AssemblyInfo.cs file, but they can appear in multiple files if those files are compiled in a single compilation pass. The common global attributes are shown in Table 20.2.

### **TABLE 20.2 Global Attributes**

| Attribute | Purpose |
| :--- | :--- |
| **Assembly Identity Attributes** | |
| AssemblyName | Full name of the assembly |
| AssemblyVersion | Version of the assembly |
| AssemblyCulture | Culture the assembly supports |
| AssemblyFlags | Indicates if multiple copies of the assembly can coexist |
| **Informational Attributes** | |
| AssemblyProduct | Specifies a product name for the assembly |
| AssemblyTrademark | Specifies a trademark for the assembly |
| AssemblyInformationalVersion | Specifies an information version for the assembly |
| AssemblyCompany | Specifies a company name for the assembly |
| AssemblyCopyright | Specifies a copyright for the assembly |
| AssemblyFileVersion | Specifies a version number for the Windows file version resource |
| CLSCompliant | Indicates if the assembly is CLS-compliant |
| **Assembly Manifest Attributes** | |
| AssemblyTitle | Specifies a title for the assembly manifest |
| AssemblyDescription | Specifies a description for the assembly manifest |
| AssemblyConfiguration | Specifies the configuration for the assembly manifest |
| AssemblyDefaultAlias | Specifies a friendly default alias for the assembly manifest |

## Using Custom Attributes

If you need to provide custom metadata for your own applications, you can create custom attributes by defining an attribute class that derives from **Attribute**, either directly or indirectly.

For example, you can define a custom attribute that contains the Team Foundation Server Work Item number associated with a code change, as shown in Listing 20.7.

### **LISTING 20.7 Creating a Custom Attribute**

```csharp
[AttributeUsage(AttributeTargets.All, Inherited = false, AllowMultiple = true)]
public sealed class WorkItemAttribute : System.Attribute
{
    private int workItemId;

    public WorkItemAttribute(int workItemId)
    {
        this.workItemId = workItemId;
    }

    public int WorkItemId
    {
        get
        {
            return this.workItemId;
        }
    }

    public string Comment
    {
        get;
        set;
    }
}
```

The custom attribute has a single public constructor whose parameters form the attributes positional parameters. Any public read-write fields or properties—in this case, the Comment property—become named parameters. Finally, the AttributeUsage attribute indicates that the WorkItem attribute is valid on any declaration, that it can be applied more than once, and that it is not automatically applied to derived types.

You can then use this attribute as shown in Listing 20.8.

### **LISTING 20.8 Applying a Custom Attribute**

```csharp
[WorkItem(1234,
        Comment = "Created a test class to show how attributes can be used.")]
public class Test
{
    [WorkItem(5678, Comment = "Changed property to use auto-property syntax.")]
    public int P
    {
        get;
        set;
    }
}
```

## Accessing Attributes at Runtime

Adding metadata to your application through attributes doesn't do much if you can't access that information at runtime. The .NET Framework provides access to the runtime type information, including metadata provided by attributes, through a process called reflection. Because attributes provide metadata, the code associated with an attribute is not actually executed until the attributes are queried.

Retrieving custom attributes is easy using the Attribute.GetCustomAttribute method. Listing 20.9 shows an example of accessing the custom attribute defined in Listing 20.7 and the simple class defined in Listing 20.8 at runtime. Figure 20.1 shows the output of Listing 20.9.
