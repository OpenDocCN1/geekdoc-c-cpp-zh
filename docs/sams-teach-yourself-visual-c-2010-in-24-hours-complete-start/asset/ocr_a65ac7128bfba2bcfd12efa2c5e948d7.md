```
public string OtherMethod()
{
	return "Test";
}

```

# The Conditional Attribute

The **Conditional** attribute indicates that a code declaration is dependent on a preprocessor conditional compilation symbol, such as DEBUG, and can be applied to a class or a method. The compiler uses this attribute to determine if the call is included or left out. If the conditional symbol is present during compilation, the call is included; otherwise, it is not. If the **Conditional** attribute is applied to a method, the method must not have a return value. Listing 20.6 shows an example of using the **Conditional** attribute.

# LISTING 20.6		Conditional Attribute

```
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

# The #if and #endif Preprocessor Symbols

Using the **Conditional** attribute is similar to using the #if and #endif preprocessor symbols but can provide a cleaner alternative that leads to fewer bugs. The class shown in Listing 20.6 using #if/#endif instead of the **Conditional** attribute is shown here.

# By the Way